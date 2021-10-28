---
copyright:
  years: 2019, 2021
lastupdated: "2021-10-28"

subcollection: mqcloud

keywords: certificates, admin, administration, SSL, TLS, expiry, generated
---

{{site.data.keyword.attribute-definition-list}}

# Queue manager certificate administration
{: #mqoc_qm_certs}

When using {{site.data.keyword.mq_full}} it is important to protect data that flows through your queue managers.  Public certificates and private keys can be used to encrypt data in transit and at rest using transport layer security (TLS) and Advanced Message Security (AMS).
{{site.data.keyword.mq_full}} provides a default certificate and private key pair for your queue manager on creation. The certificate and private key pair can be used to authenticate the queue manager to connecting MQ clients and encrypt/decrypt data.
The {{site.data.keyword.mq_full}} service provides the ability for administrators to use their own customer generated certificates and manage their use within the queue manager.
This document covers how the provided certificates are managed by the service, steps administrators will need to follow to manage expiring certificates and how to import your own customer generated certificates.

## IBM certificate management policy
{: #cert_policy_mqoc_qm_certs}

When a queue manager is created a default certificate chain is added to the queue manager's key store and trust store. The key store contains the certificate used by the queue manager and the trust store contains the intermediate and root CA certificates used to sign the queue manager certificate.  The default certificate is configured for use on the queue manger, the MQ Console and REST APIs. Only the queue manager certificate can be replaced.

Certificates can be viewed in the service by selecting a queue manager and clicking the `Key store` tab.  The image below shows a certificate in the key store, the icons (which are greyed out when not in use) from left to right represent:

- Queue manager default certificate (used when no explicit certificate is chosen in configuration)
- Used in TLS channel configuration
- Used in AMS channel configuration
- Used by MQ Console and REST APIs

![Image showing default queue manager certificate](./images/mqoc_cert_icons.png)

The default certificate has a 90 day expiration period. When nearing expiry the following process is invoked by the service:

- Approximately 30 days before expiration a new certificate is added to the queue manager key store
    - Queue managers that have not been configured to enable TLS will use the new certificate by default
    - Queue managers that are configured to use TLS will continue to use the old certificate, the new certificate is made available for use
    - The MQ Console and REST APIs for existing queue managers continue to the use the old certificate
    - The MQ Console and REST APIs for new queue managers use the new certificate
- Approximately 14 days before expiration the new certificate becomes the default
    - Queue managers that are configured to use TLS or AMS will have the default certificate replaced with the new certificate (*MQ clients will be disconnected for a short time, while the security configuration is refreshed*)
    - The MQ Console and REST APIs use the new certificate
    - The old certificate is removed from the queue manager key store

Queue managers that have been configured to use a customer generated certificate remain unaffected by the above process. Customer generated certificate expiry is the responsibility of the queue manager administrator
{: note}

Certificates originally had an expiration period of 1 year. This has been reduced to 90 days
{: note}

## Handling certificate expiry
{: #cert_expiry_mqoc_qm_certs}

The {{site.data.keyword.mq_full}} service will provide notifications in the service console user interface when IBM provided certificates near expiry. If you wish to configure notification of certificate expiry via other channels such as Slack or PagerDuty then please use the IBM Cloud [Certificate Manager](https://cloud.ibm.com/docs/services/certificate-manager?topic=certificate-manager-about-certificate-manager) service.

Within 30 and 14 days of expiry increasingly severe warnings are displayed in the queue manager list view and on the queue manager details pages. During this period TLS and AMS enabled MQ clients and connected queue managers will require their trust stores to be updated to include the new certificate.  To download the new certificate from the service follow these steps:

1. Open the `Key store` tab for the required queue manager
2. Select the `...` icon on the new certificate
3. Click the `Download public certificate` button to download the PEM file
4. Import the certificate into the MQ client trust store

![Image showing download of certificate](./images/mqoc_cert_download.png)

An example of importing a certificate into another queue manager trust store

```
# First convert the PEM file to pkcs12
# Choose a password when prompted
openssl pkcs12 -export -out qmgrcert_YYYYMM.pfx -in qmgrcert_YYYYMM.pem -nokeys

# Import the certificate into the queue manager trust store
runmqckm -cert -import -file qmgrcert_YYYYMM.pem -type pkcs12 -target /var/mqm/qmgrs/<QM>/ssl/key.kdb -target_pw <password> -target_type cms -label <label>
```

An example of importing a certificate into a Java client trust store

```
# First convert the PEM file to DER
openssl x509 -outform der -in qmgrcert_YYYYMM.pem -out qmgrcert_YYYYMM.der

# Import the certificate into the Java trust store
keytool -import -alias <label> -keystore cacerts -file qmgrcert_YYYYMM.der
```

Once the MQ client or connected queue manager trust stores have been updated, the {{site.data.keyword.mq_full}} queue manager can be configured to use the new certificate.

1. Open the `Key store` tab for the required queue manager
2. Select the `...` icon on the new certificate
3. Click the `Manage` button
4. Select the TLS and AMS configuration required
5. Now refresh the queue manager SSL Security:
    1. On the queue manager page, select **Configuration**.
      ![Image showing entering cipher spec](./images/mqoc_webconsole_qm_configuration.png)
    2. Select the **Security** tab.
      ![Image showing entering cipher spec](./images/mqoc_webconsole_qm_securitytab.png)
    3. Select the three dots, then **Refresh SSL**
      ![Image showing entering cipher spec](./images/mqoc_webconsole_qm_refreshsecurity.png)
    4. Confirm by clicking **Refresh**

If using a customer generated certificate a new version will need to be imported into the queue manager key store before the current certificate expires. TLS and AMS enabled MQ clients and connected queue managers will also require the new certificate to be added to their trust stores before the {{site.data.keyword.mq_full}} queue manager configuration is updated to use the new certificate.  See the section below for details on using customer generated certificates.

## Using your own certificate
{: #own_cert_mqoc_qm_certs}

{{site.data.keyword.mq_full}} supports the use of customer generated certificates when using TLS to connect the queue manager.  Customer generated certificates need to be imported into the queue manager key store in the PEM format.  Both public certificate and private key need to be contained in the same file.

In some organizations TLS signed certificates are generated for you by a central certificate authority (CA).  In this scenario the CA public certificates must also be included in the PEM file in the order:

- private key
- customer generated certificate
- signer CA certificates

The example below generates a self-signed client certificate and private key and merges them into a single PEM file.

```
# Generate a new self-signed public certificate and private key
# (fill in the segments of the certificate as you wish when prompted)
openssl req -newkey rsa:2048 -nodes -keyout clientKey.pem -x509 -days 365 -out clientCert.pem

# Combine the private key and public certificate into a single file
cat clientKey.pem > clientCombined.pem
cat clientCert.pem >> clientCombined.pem
```

If the private key is encrypted you will need to decode it before importing it
{: important}

Encrypted private keys look like this:

```
*-----BEGIN RSA PRIVATE KEY-----
Proc-Type: 4,ENCRYPTED DEK-Info: DES-EDE3-CBC
```

To decrypt the private key run the following command supplying the passphrase when prompted.

```
openssl rsa -in [encrypted.key] -out [decrypted.key]
```

To import your certificate into the queue manager key store:

1. In the service select the queue manager to configure
2. Click on the `Key store` tab
3. Click on the `Import` button
    ![Image showing how to import a certificate](./images/mqoc_cert_import.png)
4. Click `Browse Files` and select your PEM file
5. Click `Next`
6. Give your certificate a label and click `Save`
7. Tick the box indicating you understand a security refresh is required and click `Finish`
8. Now refresh the queue manager SSL Security:
    1. On the queue manager page, select **Configuration**.
    ![Image showing entering cipher spec](./images/mqoc_webconsole_qm_configuration.png)
    2. Select the **Security** tab.
    ![Image showing entering cipher spec](./images/mqoc_webconsole_qm_securitytab.png)
    3. Select the three dots, then **Refresh SSL**
    ![Image showing entering cipher spec](./images/mqoc_webconsole_qm_refreshsecurity.png)
    4. Confirm by clicking **Refresh**

Your certificate can now be used when configuring TLS and AMS for your queue manager.

## Using certificates for TLS
{: #cert_tls_mqoc_qm_certs}

For details on how to use certificates for TLS see [this documentation](/docs/services/mqcloud?topic=mqcloud-mqoc_jms_tls)

## Using certificates for AMS
{: #cert_ams_mqoc_qm_certs}

For details on how to use certificates for AMS see [this documentation](/docs/services/mqcloud?topic=mqcloud-mqoc_qm_ams)
