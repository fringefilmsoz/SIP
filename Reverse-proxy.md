### Reverse Proxy Support

Most people probably have OSPi exposed only on their internal network at something like http://xxx.xxx.xxx.xxx/ where xxx.xxx.xxx.xxx 
is an internal ip address issued by your home router. A reverse proxy is a web server that sits between a service on an
internal network (such as OSPi) and the open Internet. It allows you to host OSPi at a sub-path of a fully qualified domain name, or FQDN,
such as https://mydomain.com/some/path/to/OSPi. 

### Why a Reverse Proxy?

There are several simpler alternatives to a reverse proxy if you would like to expose your OSPi to the Internet. Alternatives include hosting
at the root domain (e.g. https://mydomain.com ), at a subdomain (e.g. https://ospi.mydomain.com) or on another port (e.g. https://mydomain.com:8080).
A reverse proxy is useful if you want meet the following 3 requirements.

* Host multiple web-based services from a single FQDN. (http://mydomain.com/ospi and https://mydomain.com/otherservice)
* Use standard web traffic ports for all services (80,443)
* Use a single SSL certificate for all services

The last point is really the key. Most of the simpler options mentioned above would require you to acquire a separate SSL certificates from a free
Central Authority (CA) such [Let's Encrypt](https://letsencrypt.org/) or a pay CA like Verisign, Network Solutions, etc for each service you wish to host securely. The exception is hosting on another port. 
You could use a single certificate for multiple ports, but you would need to configure your router to forward each new port to the correct internal IP. 

You could also use self-signed certificates but you would receive browser security warnings and trying to use the mobile app would most likely not work.

> Regardless of how you expose OSPi to the internet, iF you do it is HIGHLY RECOMMENDED that you access OSPi over an secure SSL connection. 

### Example setup

There are many different web servers which can provide reverse proxy support. Two popular, and free, ones are http://nginx.com/ and http://httpd.apache.org/.
Below is a sample NGINX configuration. Setting up NGINX and configuring it to forward traffic to your router is out of the scope of this documentation but can be found at http://nginx.org/en/docs/.

#### NGINX Example

```Nginx
    # This section permantly redirects all unsecure web traffic (HTTP to HTTPS)
    server {
      listen 80;
      server_name mydomain.com;
      return 301 https://mydomain.com$request_uri;
    }
    
    #This section sets up the ssl connection and the routing from the internet to OSPi
    server {
      listen			443 ssl;
      client_max_body_size    300M;
      server_name		mydomain.com;
      ssl_certificate		"/Volumes/hdd 1/docs/ssl_cert/mycert.crt"; #replace mycert with actual filename
      ssl_certificate_key	"/Volumes/hdd 1/docs/ssl_cert/mykey.key"; #replace mykey with actual filename

      #charset koi8-r;

      access_log  /usr/local/var/log/nginx/access.log upstreamlog;
   
      # sets up the sub-path to ospi (i.e. https://mydomain.com/ospi/)  by setting the location '/ospi/'
      # removing SSL (since OSPi isn't configured for it), and
      # adds information to the request that OPSi used to construct the correct links
      # in the OSPi application (i.e. https://mydomain/ospi/page.html instead of http://xxx.xxx.xxx.xxx:8080/page.html)
      location /ospi/ {
        proxy_pass http://xxx.xxx.xxx.xxx:8080/; #internal network location of your OSPi
        proxy_set_header Host $host;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
        proxy_set_header X-Scheme $scheme;
        proxy_set_header X-Script-Name /ospi;
      }
    }
```

### Reverse Proxy SSL Apache Example
```Apache

ProxyPass /sprinklers/ http://192.168.1.123:80/
ProxyPassReverse /sprinklers/ http://192.168.1.123:80/

<Location /sprinklers/>

AuthType Basic
AuthName "Restricted Area"
AuthUserFile /etc/apache2/passwd/passwords

Require user admin

ProxyPassReverseCookieDomain 192.168.1.123 myexternalssldomain.org
RequestHeader set X-SCRIPT-NAME /sprinklers
RequestHeader set X-SCHEME https

</Location>

```