# Configuration-HTTPS-CertBot

Upon completion of certbot installation for the desired webserver it will present a message showing the path where the * .pem files are located. Enter the folder using the command "cd <path>" and execute the command below.<br/>
  
openssl pkcs12 -export -out bundle.pfx -inkey privkey.pem -in cert.pem -certfile chain.pem -password pass:xxx

chmod 777 -R <<Directory or File>>
  
# Documantation pattern of CertBot Apache
  https://certbot.eff.org/lets-encrypt/ubuntubionic-apache
  
# Documantation pattern of CertBot NGinx
  https://certbot.eff.org/lets-encrypt/ubuntubionic-nginx
