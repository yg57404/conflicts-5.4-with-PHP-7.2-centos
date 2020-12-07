# conflicts-5.4-with-PHP-7.2-centos
CentOS installs problems with PHP 7.2


CentOS comes with PHP5, and there are some conflicts when installing PHP 7.2.

First get the rpm:

    rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm   
    rpm -Uvh https://mirror.webtatic.com/yum/el7/webtatic-release.rpm
    
Then you can use sudo yum list php* to see what version of php is currently available. You can find that there are versions from 7.2. The 7.2 version is named 72w, so you can install this version:

    sudo yum -y install php72w

Encounter problems:
    Transaction check error:
  file /etc/httpd/conf.d/php.conf from install of mod_php72w-7.2.14-1.w7.x86_64 conflicts with file from package php-5.4.16-46.el7.x86_64
  file /etc/httpd/conf.modules.d/10-php.conf from install of mod_php72w-7.2.14-1.w7.x86_64 conflicts with file from package php-5.4.16-46.el7.x86_64
   Error summary
   
   solve:
         
    yum -y remove php-5.4.16-46.el7.x86_64
    
But after the installation is complete, enter php -v and find that there is no such command, because php72w just installed the smallest php library, some applications have not    been installed, so install some expansion packages:

    yum -y install php72w-cli php72w-common php72w-devel php72w-mysql 
Encounter problems:

 Error: php72w-common conflicts with php-common-5.4.16-46.el7.x86_64
   You can try to add the --skip-broken option to fix the problem
   You can try to execute: rpm -Va --nofiles --nodigest

solve:
      
    yum -y remove php-common-5.4.16-46.el7.x86_64
    
Then enter 
   
     php -v 

The following message appears:

PHP 7.2.14 (cli) (built: Jan 12 2019 12:47:33) ( NTS )
Copyright (c) 1997-2018 The PHP Group
Zend Engine v3.2.0, Copyright (c) 1998-2018 Zend Technologies
