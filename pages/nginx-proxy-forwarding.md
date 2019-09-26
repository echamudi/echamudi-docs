## Nginx Proxy Forwarding

This guide is mainly for local development. It requires some additional steps for production use.

1. Install Nginx
    ```
    brew install nginx
    ```

1. Add domains to host file for local development
    ```
    127.0.0.1 mysite1.com
    127.0.0.1 www.mysite1.com
    127.0.0.1 mysite2.com
    127.0.0.1 www.mysite2.com
    ```

1. Generate certificats
    ```sh
    # Create temporary folder
    mkdir myssl
    cd myssl
    # Generate a Private Key
    openssl genrsa -des3 -out server.key 1024
    # Generate a CSR (Certificate Signing Request)
    openssl req -new -key server.key -out server.csr
    # Remove Passphrase from Key
    cp server.key server.key.org
    openssl rsa -in server.key.org -out server.key
    # Generating a Self-Signed Certificate
    openssl x509 -req -days 365 -in server.csr -signkey server.key -out server.crt
    # Installing the Private Key and Certificate
    cp server.crt /usr/local/etc/nginx/server.crt
    cp server.key /usr/local/etc/nginx/server.key
    ```

1. Edit config
    Config file at `/usr/local/etc/nginx/nginx.conf`

    ```conf
    # ...
    http {
        # ...

        # mysite1 HTTP
        server {
            listen       80;
            server_name  mysite1.com www.mysite1.com;

            location / {
                proxy_pass   http://127.0.0.1:8881;
            }

            error_page   500 502 503 504  /50x.html;
            location = /50x.html {
                root   html;
            }
        }

        # mysite1 HTTPS
        server {
            listen       443 ssl;
            server_name  mysite1.com www.mysite1.com;
            
            ssl_protocols TLSv1.2 TLSv1.1 TLSv1;
            
            ssl_certificate      server.crt;
            ssl_certificate_key  server.key;

            ssl_session_cache shared:SSL:10m;
            ssl_session_timeout 10m;

            add_header Strict-Transport-Security "max-age=31536000; includeSubDomains; preload" always;

            ssl_ciphers 'kEECDH+ECDSA+AES128 kEECDH+ECDSA+AES256 kEECDH+AES128 kEECDH+AES256 kEDH+AES128 kEDH+AES256 DES-CBC3-SHA +SHA !aNULL !eNULL !LOW !kECDH !DSS !MD5 !RC4 !EXP !PSK !SRP !CAMELLIA !SEED';
            ssl_prefer_server_ciphers  on;

            location / {
                proxy_pass          http://127.0.0.1:8881;
                
            #   proxy_set_header    Host             $host;
            #   proxy_set_header    X-Real-IP        $remote_addr;
            #   proxy_set_header    X-Forwarded-For  $proxy_add_x_forwarded_for;
            #   proxy_set_header    X-Client-Verify ss SUCCESS;
            #   proxy_set_header    X-Client-DN      $ssl_client_s_dn;
            #   proxy_set_header    X-SSL-Subject    $ssl_client_s_dn;
            #   proxy_set_header    X-SSL-Issuer     $ssl_client_i_dn;
            #   proxy_read_timeout 1800;
            #   proxy_connect_timeout 1800;
            }
        }

        # Repeat mysite1 for mysite2

        # ...
    }

    # ...
    ```

1. Restart Nginx
    ```sh
    nginx -s stop
    nginx
    ```

> References
> https://www.akadia.com/services/ssh_test_certificate.html
>
> https://community.letsencrypt.org/t/howto-a-with-all-100-s-on-ssl-labs-test-using-nginx-mainline-stable/55033/2
>
> https://medium.com/@aditya.vssut/setting-up-nginx-configuration-to-get-an-a-in-ssl-labs-server-test-e0e25098d634