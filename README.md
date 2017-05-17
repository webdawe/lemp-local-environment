# LEMP setup with Vagrant & Ansible #

----------

Webdawe Local Development Environment 

- Adminer
- Nginx
- Composer
- Git
- MySQL
- PHP 5.5
- Nodejs

## Requirements ##

- Vagrant 1.6.*
- Virtualbox 4.3.*

## Notes ##

## Vagrant File Variables 

Ip of the virtual machine - This will be the IP to which the virtual hosts point to
```
VM_IP = '192.168.100.206'
```
Add the following entry to the hosts file - /etc/hosts

```
#webdawe
192.168.100.206 webdawe.dev
192.168.100.206 www.webdawe.dev
192.168.100.206 adminer.localhost.com
```
Code Folder to share - Host Source and VM Destination 
as per following settings, each website's code should be placed inside sites folder on the root.
for webdawe website, code should be cloned to ~/sites/webdawe which will be the document root in the virtual machine.
```
VM_CODE_SOURCE = '/path/to/code/source/'
VM_CODE_DESTINATION = '/var/www/'
```
Virtual Host and MySQL Settings should be placed on config/config.yml File

```
config:
  vhost:
    webdawe:
      name: "webdawe.dev"
      template: "webdawe.dev.conf.j2"
  mysql:
    webdawe:
      user: "webdawe"
      password: "webdawe"
      database: "webdawe_magento"
      privileges: "ALL"
```
