# Apache-version-hide-php-version-hide-linux


 Security Settings --------------------------#<br>
# Disallow weak SSLCipherSuite<br>
SSLCipherSuite AES256+EECDH:AES256+EDH:AES128+EECDH:AES128+EDH<br>
SSLProtocol -ALL -SSLv3 +TLSv1 +TLSv1.1 +TLSv1.2<br>

#Reduce Server HTTP Header to the minimum product (Apache) rather than showing detailed version information of the server and operating system<br>
ServerTokens Prod<br>

#Remove the footer from error pages, which details the version numbers:<br>
ServerSignature Off<br>

<IfModule mod_headers.c><br>
 # Hide X-Powered-By and Server headers, sent by downstream application servers:<br>
 # Note you need both below as the "always" one doesn't work with Jboss for some reason<br>
   Header always unset "X-Powered-By"<br>
   Header unset "X-Powered-By"<br>
 #Clickjacking<br>
 #Header always append X-Frame-Options DENY<br>
   Header always set X-Frame-Options SAMEORIGIN<br>
   #Header always append X-Frame-Options ALLOW-FROM=eatrightindia.gov.in<br>

 #XSS Protection<br>
   Header set X-XSS-Protection "1; mode=block"<br>
 #MIME Sniffing<br>
   Header set X-Content-Type-Options nosniff<br>
 #Cache Poisoning<br>
   Header set Cache-Control "max-age=0, must-revalidate, no-cache, no-store, post-check=0"<br>
 #Insecure Session Cookie Parameters<br>
   Header edit Set-Cookie ^(.*)$ $1;HttpOnly;Secure<br>
</IfModule><br>
