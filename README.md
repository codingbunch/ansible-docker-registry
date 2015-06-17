ansible-docker-registry
=========

[![Build Status](https://travis-ci.org/codingbunch/ansible-docker-registry.png?branch=master)](https://travis-ci.org/codingbunch/ansible-docker-registry)

An Ansible role for installing a private Docker Registry

Requirements
------------

TODO

Role Variables
--------------

### Default

* ```domain```: Specify a domain name (default: ```localhost```)
* ```log_level```: Log level for the server (default: ```info```)
* ```storage_type```: Accepts either ```local``` or ```s3``` (default: ```local```)
* ```storage_path```: File path to store registry uploads (default: ```/var/docker-registry```)
* ```use_nginx```: Install Nginx and configure docker-registry vhost (default: ```true```)
* ```use_redis```: Install and configure Redis server as a cache (default: ```true```)

### SSL Settings
* ```registry_port```: Custom port to have nginx listen on (default: ```80```)
* ```registry_ssl```: Enable SSL on nginx (default: ```false```)
* ```registry_ssl_cert```: Specify a SSL certificate to use (default: ```/etc/ssl/certs/docker_registry.crt```)
* ```registry_ssl_key```: Specify a SSL key to use (default: ```/etc/ssl/private/docker_registry.key```)
* ```create_ssl_cert```: Create a self-signed certificate if ```registry_ssl_cert``` is not present on the system (default: ```true```)

### OpenSSL cert settings
* ```openssl_bits```: Bit length of the private key (default: ```2048```)
* ```openssl_countryName```: Country Code (default: ```ES```)
* ```openssl_stateOrProvinceName```: State or Province (default: ```Madrid```)
* ```openssl_localityName```: Locality name (default: ```Madrid```)
* ```openssl_organizationName```: Full company name (default: ```MyCompany```)
* ```openssl_organizationalUnitName```: Company sub-division or a product name (default: ```Docker Registry```)
* ```openssl_commonName```: Your domain name, or in case of wildcard certificates, use an astrisk, like this: *.mycompany.com (default: ```mycompany.com```)

### S3 Storage

* ```s3_region```: optional, will default to US Standard
* ```s3_bucket```: also provides the value for boto_bucket
* ```s3_storage_path```
* ```s3_access_key```
* ```s3_secret_key```

#### There are 2 ways to specify credentials for S3 storage:

**1. Using access and secret keys:**

By specifying ```s3_access_key``` and ```s3_secret_key```.

**2. Using IAM instance profiles**

By omitting ```s3_access_key``` and ```s3_secret_key``` it will use an IAM instance profile that has been attached to that virtual machine for [authorisation](http://docs.aws.amazon.com/IAM/latest/UserGuide/roles-usingrole-ec2instance.html).

### GCS Storage

* ```gcs_bucket```: Value for the bucket deing used.
* ```gcs_storage_path```: The path within th ebucket where to store data. (will be created if not exist).

#### There are 3 ways to specify credentials for GCS storage:

**1. Using Google Cloud Platform OAuth:**

* ```gcs_oauth2```: oauth2 value (default ```false```)

**2. Using Google Storage interoperability keys:**

* ```gcs_access_key```: only used when gcs_oauth2 is false and ```use_gcs_default_credentials``` is undefined.
* ```gcs_secret_key```: only used when gcs_oauth2 is false and ```use_gcs_default_credentials``` is undefined.

**3. Using Google service account authorization:**

* ```use_gcs_default_credentials```: use a service account that has been attached to that virtual machine for [authorisation](https://developers.google.com/identity/protocols/application-default-credentials) value (default ```undefined```)

## Note on SSL

If using a self-signed certificate, or no SSL certificate for recent docker versions, you must start the docker daemon with ```--insecure-registry```.

For boot2docker, see https://github.com/boot2docker/boot2docker#insecure-registry.


Example Playbook
----------------

    - hosts: docker-registry
      roles:
         - { role: codingbunch.ansible-docker-registry }

License
-------

MIT

Author Information
------------------

CodingBunch
