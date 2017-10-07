---
title: "aaaSet копирование MySQL на виртуальной Машине Linux в Azure | Документы Microsoft"
description: "Узнайте, как tooinstall hello MySQL стека на виртуальной машине Linux (Ubuntu или RedHat семейство ОС) в Azure"
services: virtual-machines-linux
documentationcenter: 
author: SuperScottz
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 153bae7c-897b-46b3-bd86-192a6efb94fa
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/01/2016
ms.author: mingzhan
ms.openlocfilehash: e47d0de7f0eb5bb873ad20e4bc35f1b5f8d33bdb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooinstall-mysql-on-azure"></a>Как tooinstall MySQL в Azure
В этой статье вы узнаете, как tooinstall и настройте MySQL на виртуальной машине Azure под управлением Linux.

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="install-mysql-on-your-virtual-machine"></a>Установка MySQL в виртуальной машине
> [!NOTE]
> Необходимо иметь уже виртуальной машины Microsoft Azure под управлением Linux в порядке toocomplete этого учебника. См. в разделе [виртуальной Машине Linux Azure учебника](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toocreate и настроить виртуальную Машину Linux с `mysqlnode` как имя виртуальной Машины hello и `azureuser` имени пользователя, прежде чем продолжить.
> 
> 

В этом случае использование порта 3306, hello порт MySQL.  

Подключите toohello виртуальных Машин Linux, созданных посредством putty. Если это первое использование виртуальной Машине Linux Azure hello см. как toouse putty подключиться tooa ВМ Linux [здесь](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Мы будем использовать tooinstall пакета репозитория MySQL5.6 в качестве примера в этой статье. В настоящее время MySQL5.6 имеет улучшенную производительность по сравнению с MySQL5.5.  Дополнительные сведения см. [здесь](http://www.mysqlperformanceblog.com/2013/02/18/is-mysql-5-6-slower-than-mysql-5-5/).

### <a name="how-tooinstall-mysql56-on-ubuntu"></a>Как tooinstall MySQL5.6 на Ubuntu
Здесь мы будем использовать виртуальную машину Linux на базе Ubuntu от Azure.

* Шаг 1: Установка MySQL Server 5.6 перейдите слишком`root` пользователя:
  
            #[azureuser@mysqlnode:~]sudo su -
  
    Установите mysql-server 5.6:
  
            #[root@mysqlnode ~]# apt-get update
            #[root@mysqlnode ~]# apt-get -y install mysql-server-5.6
  
    Во время установки, вы увидите диалоговое окно poping копирование tooask вы tooset MySQL пароль учетной записи root ниже и требуется задать пароль hello здесь.
  
    ![изображение](./media/mysql-install/virtual-machines-linux-install-mysql-p1.png)

    Пароль входного hello tooconfirm еще раз.

    ![изображение](./media/mysql-install/virtual-machines-linux-install-mysql-p2.png)

* Шаг 2. Вход на MySQL Server
  
    После завершения установки MySQL Server служба MySQL запустится автоматически. Вы можете войти на MySQL Server как пользователь `root` .
    Используйте hello ниже команда toologin и ввода пароля.
  
             #[root@mysqlnode ~]# mysql -uroot -p
* Шаг 3: Управление службой MySQL hello
  
    (а) Для получения информации о состоянии службы MySQL выполните команду:
  
             #[root@mysqlnode ~]# service mysql status
  
    (б) Для запуска службы MySQL выполните команду:
  
             #[root@mysqlnode ~]# service mysql start
  
    (в) Для остановки службы MySQL выполните команду:
  
             #[root@mysqlnode ~]# service mysql stop
  
    (d) перезапустите службу MySQL hello
  
             #[root@mysqlnode ~]# service mysql restart

### <a name="how-tooinstall-mysql-on-red-hat-os-family-like-centos-oracle-linux"></a>Как CentOS, Oracle Linux tooinstall MySQL в семействе ОС Red Hat
Здесь мы будем использовать виртуальную машину Linux с CentOS или Oracle Linux.

* Шаг 1: Добавление hello MySQL Yum репозитория коммутатора слишком`root` пользователя:
  
            #[azureuser@mysqlnode:~]sudo su -
  
    Загрузите и установите пакет выпуска hello MySQL.
  
            #[root@mysqlnode ~]# wget http://repo.mysql.com/mysql-community-release-el6-5.noarch.rpm
            #[root@mysqlnode ~]# yum localinstall -y mysql-community-release-el6-5.noarch.rpm
* Шаг 2: Измените ниже репозитория MySQL hello tooenable файл для загрузки пакета MySQL5.6 hello.
  
            #[root@mysqlnode ~]# vim /etc/yum.repos.d/mysql-community.repo
  
    Обновление для каждого значения toobelow этот файл:
  
        \# *Enable toouse MySQL 5.6*
  
        [mysql56-community]
        name=MySQL 5.6 Community Server
  
        baseurl=http://repo.mysql.com/yum/mysql-5.6-community/el/6/$basearch/
  
        enabled=1
  
        gpgcheck=1
  
        gpgkey=file:/etc/pki/rpm-gpg/RPM-GPG-KEY-mysql
* Шаг 3. Установка MySQL из репозитория MySQL. Установите MySQL:
  
           #[root@mysqlnode ~]#yum install mysql-community-server
  
    Будут установлены пакет MySQL RPM и все связанные пакеты.
* Шаг 4: Управление службой MySQL hello
  
    (a) Проверьте состояние службы hello hello MySQL server.
  
           #[root@mysqlnode ~]#service mysqld status
  
    (b) Проверьте, работает ли сервер порта MySQL по умолчанию hello.
  
           #[root@mysqlnode ~]#netstat  –tunlp|grep 3306

    (c) сервер MySQL hello начала:

           #[root@mysqlnode ~]#service mysqld start

    (d) остановите сервер MySQL hello:

           #[root@mysqlnode ~]#service mysqld stop

    (e) при включении системы hello установите MySQL toostart:

           #[root@mysqlnode ~]#chkconfig mysqld on


### <a name="how-tooinstall-mysql-on-suse-linux"></a>Как tooinstall MySQL в SUSE Linux
Здесь мы будем использовать виртуальную машину Linux с OpenSUSE.

* Шаг 1. Скачивание и установка MySQL Server
  
    Переключение слишком`root` пользователя с помощью ниже команду:  
  
           #sudo su -
  
    Скачайте и установите пакет MySQL:
  
           #[root@mysqlnode ~]# zypper update
  
           #[root@mysqlnode ~]# zypper install mysql-server mysql-devel mysql
* Шаг 2: Управление службой MySQL hello
  
    (a) Проверьте состояние hello hello MySQL server.
  
           #[root@mysqlnode ~]# rcmysql status
  
    (b) Проверьте, является ли hello порт по умолчанию hello MySQL server:
  
           #[root@mysqlnode ~]# netstat  –tunlp|grep 3306

    (c) сервер MySQL hello начала:

           #[root@mysqlnode ~]# rcmysql start

    (d) остановите сервер MySQL hello:

           #[root@mysqlnode ~]# rcmysql stop

    (e) при включении системы hello установите MySQL toostart:

           #[root@mysqlnode ~]# insserv mysql

### <a name="next-step"></a>Дальнейшее действие
Дополнительные сведения и сведения об использовании MySQL см. [здесь](https://www.mysql.com/).

