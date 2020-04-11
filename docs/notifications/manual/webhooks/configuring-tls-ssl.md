# Configuring TLS / SSL

A properly secured webhook is needed in to receive RingCentral webhook eventss with production data.

This guide provides some quick information on how to configure TLS / SSL on a webserver and includes the following ssections:

1. Creating a Key Pair and Requesting a TLS / SSL Server Certificate
1. Installing the certificate in a server

This tutorial will use [Let's Encrypt](https://letsencrypt.org/) for certificates. Other Certificate Authorities will have their own ways to process Certificate Signing Requests (CSRs) and return Certificates for use.

## Creating a Key Pair and Requesting a TLS / SSL Server Certificate

When using Let's Encrypt, there are a number of ways to create a certificate and key pair which can be done with any [ACME protocol compliant client](https://letsencrypt.org/docs/client-options/).

> Terminology: The key pair is the asymmetric cryptographic security devices used in the TLS protocol, consisting of a private key and a public key. The certificate is a cryptographically signed document by a Certificate Authority that attests to the ownership of the private key.

Many AMCE clients make the job of retrieving and renewing certificates painless. For this tutorial we will show the manual approach using the popular [EFF Certbot](https://certbot.eff.org/) client since it is the mostly broadly applicable. We will follow this by showing an automated approach to demonstrate how easy this can be.

### Manual Approach

To create a key pair and certificate manually, there are 3 steps:

1) Request the certificate.

The following command will promopt you to create a file on a server you control.

`$ certbot certonly --manual --preferred-challenges http -d mysite.com`

2) Add a challenge file to the server.

```
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Create a file containing just this data:

hm-Fjvqk7U37Nw2SMyKfAD_CE8sDsGrHczJmvUkzuxI.ReoGCSKTofBLRj97vINiQ8jZ39IMLvSmKhaXulMzA0I

And make it available on your web server at this URL:

http://example.com/.well-known/acme-challenge/hh-Fjzqk7V37Nw2SLyKfZD_CE8sDsQrHczVovUkzuxI

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
```

After you create that file, `certbot` will create two files:

```
 - Congratulations! Your certificate and chain have been saved at:
   /etc/letsencrypt/live/example.com/fullchain.pem
   Your key file has been saved at:
   /etc/letsencrypt/live/example.com/privkey.pem
```

3) Install the certificates.

Use the following configurations to install your key and certificate in your webserver.

```http tab="Apache"
SSLEngine on
SSLProtocol -all +TLSv1.2 +TLSv1.3
SSLCertificateFile /etc/letsencrypt/live/example.com/fullchain.pem
SSLCertificateKeyFile /etc/letsencrypt/live/example.com/privkey.pem
```

### Automatic Approach

With Let's Encrypt, there are also ways to fully automate the process for certificate management.

For example, [CertMagic](https://github.com/caddyserver/certmagic) for Go handles the entire process requesting, loading, and renewing certificates transparently.

```http tab="Go"
import "github.com/caddyserver/certmagic"

// Replace the following:
// http.ListenAndServe(":80", mux)

// with encrypted HTTPS with HTTP->HTTPS redirects 🔒😍
certmagic.HTTPS([]string{"example.com"}, mux)
```



