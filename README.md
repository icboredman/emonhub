emonHub
=======

Development branch
------------------

This branch is where the development version of emonHub is maintained

[Released version is on the Master branch](https://github.com/emonhub/emonhub/blob/master/README.md)

This development version can be installed in one line using [dev-emonhub](https://github.com/emonhub/dev-emonhub/blob/master/README.md)

    git clone https://github.com/emonhub/dev-emonhub.git ~/dev-emonhub && ~/dev-emonhub/install

This software is part of OpenEnergyMonitor project.

[Visit emonHub Documentation !](http://emonhub.org)

Changes in this fork
------------------
* Increased number of nodes from 31 to 49
* Added posting to EmonCMS over HTTPS. This also works with client side SSL certificate

The SSL support was enabled by replacing urllib2 with pycurl calls, since, for some reason, I was unable to get results with urllib2.

In order to properly configure pycurl, I used this procedure: 

    sudo apt-get install python-pycurl
    sudo apt-get install libcurl4-openssl-dev        (OpenSSL seems to have better SSL support than GnuTLS)
    curl-config --version
    sudo apt-get install python-dev
    sudo git clone https://github.com/pycurl/pycurl.git    (as opposed to apt-get install, this installs the latest version)
    cd pycurl
    sudo python setup.py install 

To use client side SSL certificates, two additional entries were added to emonhub.conf: sslcertfile and sslkeyfile

Here's the procedure I used to generate certificate files that pyCurl understands:

    openssl pkcs12 -in client.p12 -out pycurl.client.pem -clcerts
    openssl rsa -in pycurl.client.pem -out pycurl.nopwd.client.pem

