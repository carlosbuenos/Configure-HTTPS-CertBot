# Configuration-HTTPS-CertBot

Documentation for configuring digital certbot cerfic for safe environments.

Run the following command to generate a private key and a certificate signing request:

openssl req -config https.config -new -out csr.pem

Run the following command to create a self-signed certificate:

openssl x509 -req -days 365 -extfile https.config -extensions v3_req -in csr.pem -signkey key.pem -out https.crt

Run the following command to generate a pfx file containing the certificate and the private key that you can use with Kestrel.

openssl pkcs12 -export -out https.pfx -inkey key.pem -in https.crt -password pass:<<Password>>

chmod 777 -R <<Directory or File>>
  
# Documantation pattern of CertBot Apache
  https://certbot.eff.org/lets-encrypt/ubuntubionic-apache
  
# Documantation pattern of CertBot NGinx
  https://certbot.eff.org/lets-encrypt/ubuntubionic-nginx
