# Apache-version-hide-php-version-hide-linux

1
 Security Settings --------------------------#
# Disallow weak SSLCipherSuite
SSLCipherSuite AES256+EECDH:AES256+EDH:AES128+EECDH:AES128+EDH
SSLProtocol -ALL -SSLv3 +TLSv1 +TLSv1.1 +TLSv1.2

#Reduce Server HTTP Header to the minimum product (Apache) rather than showing detailed version information of the server and operating system
ServerTokens Prod

#Remove the footer from error pages, which details the version numbers:
ServerSignature Off

<IfModule mod_headers.c>
 # Hide X-Powered-By and Server headers, sent by downstream application servers:
 # Note you need both below as the "always" one doesn't work with Jboss for some reason
   Header always unset "X-Powered-By"
   Header unset "X-Powered-By"
 #Clickjacking
 #Header always append X-Frame-Options DENY
   Header always set X-Frame-Options SAMEORIGIN
   #Header always append X-Frame-Options ALLOW-FROM=eatrightindia.gov.in

 #XSS Protection
   Header set X-XSS-Protection "1; mode=block"
 #MIME Sniffing
   Header set X-Content-Type-Options nosniff
 #Cache Poisoning
   Header set Cache-Control "max-age=0, must-revalidate, no-cache, no-store, post-check=0"
 #Insecure Session Cookie Parameters
   Header edit Set-Cookie ^(.*)$ $1;HttpOnly;Secure
</IfModule>
