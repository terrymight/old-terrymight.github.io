+++
title = "How To Install Composer Globally In Lammp Ubuntu"
date = "2022-08-09T09:50:46+02:00"
tags = ["PHP","COMPOSER","FRAMEWORK"]
categories = ["PHP","COMPOSER","FRAMEWORK"]
description = "How to Install Composer in Lammp in Linux, without installing others packages"
authors = ["Tejiri Mayone"]
banner = "img/banners/banner-5.jpg"
+++

## Introduction
Composer is an application-level dependency manager for the PHP programming language that provides a standard format for managing dependencies of PHP software and required libraries. 

In this tutorials I will be showing you how to install Composer in Lammp in Ubuntu. 

I will assume you have already install Lammp from it offical website [Lammp offical site](https://www.apachefriends.org/download.html) for details.


## Steps to get started

Open your terminal and input the code below install composer using the following command like so.

```
$ sudo curl -s https://getcomposer.org/installer | /opt/lampp/bin/php
```

Composer was installed perfectly. After that, input this command to make composer global:

```
sudo ln -s /opt/lampp/bin/php /usr/local/bin/php
```
Then run the command below to allow the 'composer' command to be run globally (this will be run from within the folder where you've just installed composer in which a composer.phar file has just been created):

```
sudo mv composer.phar /usr/local/bin/composer
```

![image alt text](/images/tn.png)



Leave us a comment if you have any questions.