#Steps:
Enable  ssl apache mod
`sudo a2enmod ssl`

Copy conf file to a destination (example):
`mkdir /etc/apache2/ssl`
`cp cert.conf /etc/apache2/ssl`

Create cert using ssl:
`sudo openssl req -x509 -nodes -newkey rsa:2048 -keyout /etc/apache2/ssl/apache.key -out /etc/apache2/ssl/apache.crt -config /etc/apache2/ssl/cert.conf`

And follow the steps.

Create a new vhost (or edit an existing):
`cp default-ssl.conf /etc/apache2/site-availables`

And enable it:
`sudo a2ensite default-ssl.conf`

Restart apache:
`sudo service apache2 restart`

Now, you can enter to the site (anysite.local) and add a cert exception following this steps:

- Using Chrome, hit a page on your server via HTTPS and continue past the red warning page (assuming you haven't done this already).
- Open up Chrome Settings > Show advanced settings > HTTPS/SSL > Manage Certificates.
- Click the Authorities tab and scroll down to find your certificate under the Organization Name that you gave to the certificate.
- Select it, click Edit, check all the boxes and click OK. You may have to restart Chrome.

If the cert doesn't appear in the list, you can export it:
- On the page with the untrusted certificate (https:// is crossed out in red), click the lock > Certificate Information.
- Click the Details tab > Export. Choose PKCS #7, single certificate as the file format.
- Then follow my original instructions to get to the Manage Certificates page. Click the Authorities tab > Import and choose the file to which you exported the certificate, and make sure to choose PKCS  #7, single certificate as the file type.
- If prompted certification store, choose Trusted Root Certificate Authorities
- Check all boxes and click OK. Restart Chrome.
