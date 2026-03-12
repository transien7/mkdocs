# Creating an Apache Web Server

## Initial Steps
### Install Apache Web Server

``` bash
sudo apt install -y apache2
```
### Start the web server
``` bash
sudo systemctl enable apache2.service
sudo systemctl start apache2.service
```
### Create a website
#### Create a domain
``` bash
sudo mkdir /var/www/<domain_name>           # e.g. example.com
```
#### Create index.html
``` bash
sudo vim /var/www/<domain_name>/index.html
```
#### Insert HTML into index.html
``` html
<html>
	<head>
		<title>Example.com</title>
		<style>
			body {background-color: black}
			h1 {font-size:3cm; text-align: center; color: white;
				text-shadow: 0 0 3mm yellow}
		</style>
	</head>
	
	<body>
		<h1>Example.com!</h1>
	</body>
</html>
```

## Create SSL certificate and private key
### Install gnoMint
``` bash
sudo apt install -y gnomint
```
### Use gnoMint to create a CA and SSL certificate
1. Launch gnoMint
2. Add self-signed CA
3. Follow the prompts to create a root CA
4. Next, add a certificate request and sign the certificate with the root CA
5. Export the new public certificate as bank32.crt
6. Export the new private key (encrypted) as bank32.key
### Export the certificate and key to /etc/ssl/certs
``` bash
sudo mv bank32* /etc/ssl/certs
```

## Configure the web server

1. Open the Apache configuration file
``` bash
sudo vim /etc/apache2/apache2.conf
```

2. Insert the SSL information
```
<VirtualHost *:443>
    DocumentRoot /var/www/example.com
    ServerName www.example.com
    DirectoryIndex index.html
    SSLEngine On
    SSLCertificateFile    /etc/ssl/certs/bank32.crt
    SSLCertificateKeyFile /etc/ssl/certs/bank32.key
</VirtualHost>
}
```

## Enable SSL

On the server, execute the following commands to enable SSL on the Apache HTTP server
``` bash
sudo a2enmod ssl
sudo systemctl restart apache2.service
```

## Add hosts

On each client device requiring access to the web server:

1. Open the hosts file
``` bash
sudo vim /etc/hosts
```

2. Insert the IP address and domain name of the website, e.g.
``` bash
# webserver IP  domain name
192.168.1.30    www.example.com
```