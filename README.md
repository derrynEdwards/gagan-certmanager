# Generating Wildcard Certificates with Cert-Manager

## do-secret.yml

Populate the access token by encrypting your DigitalOcean API Token with base64.

`echo -n "<api_token>" | base64`

Copy the output and replace `<base64 encoded dns token>` for `access-token`  

## issuer.yml

Replace the following with your values:  
- `name: <issuer_name>` with the name you want to assign to the Issuer, to be referenced in the `cert.yml` template.  
- `email: <your_email>` with your e-mail for LetsEncrypt.  
- `name: <privatekey_name>` Secret name to use for your private key.  

## cert.yml

Repalce the following with your values:  
- `name: <certname>` with name you want to assign to the `Certificate` object.
- `secretName: <secret_name>` with the secretName that will store your certificate and to be referenced by your Ingress templates.  
- `name: <issuer_name>` witht he name you assigned to your Issuer.  
- `dnsNames: <domain_name>` with the DNS names that your certificate will cover. Example:  
```
dnsNames:
- example.com
- "*.example.com"
```