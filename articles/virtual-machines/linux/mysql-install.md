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
# <a name="how-tooinstall-mysql-on-azure"></a><span data-ttu-id="c1dc8-103">Как tooinstall MySQL в Azure</span><span class="sxs-lookup"><span data-stu-id="c1dc8-103">How tooinstall MySQL on Azure</span></span>
<span data-ttu-id="c1dc8-104">В этой статье вы узнаете, как tooinstall и настройте MySQL на виртуальной машине Azure под управлением Linux.</span><span class="sxs-lookup"><span data-stu-id="c1dc8-104">In this article, you will learn how tooinstall and configure MySQL on an Azure virtual machine running Linux.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="install-mysql-on-your-virtual-machine"></a><span data-ttu-id="c1dc8-105">Установка MySQL в виртуальной машине</span><span class="sxs-lookup"><span data-stu-id="c1dc8-105">Install MySQL on your virtual machine</span></span>
> [!NOTE]
> <span data-ttu-id="c1dc8-106">Необходимо иметь уже виртуальной машины Microsoft Azure под управлением Linux в порядке toocomplete этого учебника.</span><span class="sxs-lookup"><span data-stu-id="c1dc8-106">You must already have a Microsoft Azure virtual machine running Linux in order toocomplete this tutorial.</span></span> <span data-ttu-id="c1dc8-107">См. в разделе [виртуальной Машине Linux Azure учебника](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toocreate и настроить виртуальную Машину Linux с `mysqlnode` как имя виртуальной Машины hello и `azureuser` имени пользователя, прежде чем продолжить.</span><span class="sxs-lookup"><span data-stu-id="c1dc8-107">Please see the [Azure Linux VM tutorial](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toocreate and set up a Linux VM with `mysqlnode` as hello VM name and `azureuser` as user before proceeding.</span></span>
> 
> 

<span data-ttu-id="c1dc8-108">В этом случае использование порта 3306, hello порт MySQL.</span><span class="sxs-lookup"><span data-stu-id="c1dc8-108">In this case, use 3306 port as hello MySQL port.</span></span>  

<span data-ttu-id="c1dc8-109">Подключите toohello виртуальных Машин Linux, созданных посредством putty.</span><span class="sxs-lookup"><span data-stu-id="c1dc8-109">Connect toohello Linux VM you created via putty.</span></span> <span data-ttu-id="c1dc8-110">Если это первое использование виртуальной Машине Linux Azure hello см. как toouse putty подключиться tooa ВМ Linux [здесь](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c1dc8-110">If this is hello first time you use Azure Linux VM, see how toouse putty connect tooa Linux VM [here](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="c1dc8-111">Мы будем использовать tooinstall пакета репозитория MySQL5.6 в качестве примера в этой статье.</span><span class="sxs-lookup"><span data-stu-id="c1dc8-111">We will use repository package tooinstall MySQL5.6 as an example in this article.</span></span> <span data-ttu-id="c1dc8-112">В настоящее время MySQL5.6 имеет улучшенную производительность по сравнению с MySQL5.5.</span><span class="sxs-lookup"><span data-stu-id="c1dc8-112">Actually, MySQL5.6 has more improvement in performance than MySQL5.5.</span></span>  <span data-ttu-id="c1dc8-113">Дополнительные сведения см. [здесь](http://www.mysqlperformanceblog.com/2013/02/18/is-mysql-5-6-slower-than-mysql-5-5/).</span><span class="sxs-lookup"><span data-stu-id="c1dc8-113">More information [here](http://www.mysqlperformanceblog.com/2013/02/18/is-mysql-5-6-slower-than-mysql-5-5/).</span></span>

### <a name="how-tooinstall-mysql56-on-ubuntu"></a><span data-ttu-id="c1dc8-114">Как tooinstall MySQL5.6 на Ubuntu</span><span class="sxs-lookup"><span data-stu-id="c1dc8-114">How tooinstall MySQL5.6 on Ubuntu</span></span>
<span data-ttu-id="c1dc8-115">Здесь мы будем использовать виртуальную машину Linux на базе Ubuntu от Azure.</span><span class="sxs-lookup"><span data-stu-id="c1dc8-115">We will use Linux VM with Ubuntu from Azure here.</span></span>

* <span data-ttu-id="c1dc8-116">Шаг 1: Установка MySQL Server 5.6 перейдите слишком`root` пользователя:</span><span class="sxs-lookup"><span data-stu-id="c1dc8-116">Step 1: Install MySQL Server 5.6   Switch too`root` user:</span></span>
  
            #[azureuser@mysqlnode:~]sudo su -
  
    <span data-ttu-id="c1dc8-117">Установите mysql-server 5.6:</span><span class="sxs-lookup"><span data-stu-id="c1dc8-117">Install mysql-server 5.6:</span></span>
  
            #[root@mysqlnode ~]# apt-get update
            #[root@mysqlnode ~]# apt-get -y install mysql-server-5.6
  
    <span data-ttu-id="c1dc8-118">Во время установки, вы увидите диалоговое окно poping копирование tooask вы tooset MySQL пароль учетной записи root ниже и требуется задать пароль hello здесь.</span><span class="sxs-lookup"><span data-stu-id="c1dc8-118">During installation, you will see a dialog window poping up tooask you tooset MySQL root password below, and you need set hello password here.</span></span>
  
    ![изображение](./media/mysql-install/virtual-machines-linux-install-mysql-p1.png)

    <span data-ttu-id="c1dc8-120">Пароль входного hello tooconfirm еще раз.</span><span class="sxs-lookup"><span data-stu-id="c1dc8-120">Input hello password again tooconfirm.</span></span>

    ![изображение](./media/mysql-install/virtual-machines-linux-install-mysql-p2.png)

* <span data-ttu-id="c1dc8-122">Шаг 2. Вход на MySQL Server</span><span class="sxs-lookup"><span data-stu-id="c1dc8-122">Step 2: Login MySQL Server</span></span>
  
    <span data-ttu-id="c1dc8-123">После завершения установки MySQL Server служба MySQL запустится автоматически.</span><span class="sxs-lookup"><span data-stu-id="c1dc8-123">When MySQL server installation finished, MySQL service will be started automatically.</span></span> <span data-ttu-id="c1dc8-124">Вы можете войти на MySQL Server как пользователь `root` .</span><span class="sxs-lookup"><span data-stu-id="c1dc8-124">You can login MySQL Server with `root` user.</span></span>
    <span data-ttu-id="c1dc8-125">Используйте hello ниже команда toologin и ввода пароля.</span><span class="sxs-lookup"><span data-stu-id="c1dc8-125">Use hello below command toologin and input password.</span></span>
  
             #[root@mysqlnode ~]# mysql -uroot -p
* <span data-ttu-id="c1dc8-126">Шаг 3: Управление службой MySQL hello</span><span class="sxs-lookup"><span data-stu-id="c1dc8-126">Step 3: Manage hello running MySQL service</span></span>
  
    <span data-ttu-id="c1dc8-127">(а) Для получения информации о состоянии службы MySQL выполните команду:</span><span class="sxs-lookup"><span data-stu-id="c1dc8-127">(a) Get status of MySQL service</span></span>
  
             #[root@mysqlnode ~]# service mysql status
  
    <span data-ttu-id="c1dc8-128">(б) Для запуска службы MySQL выполните команду:</span><span class="sxs-lookup"><span data-stu-id="c1dc8-128">(b) Start MySQL Service</span></span>
  
             #[root@mysqlnode ~]# service mysql start
  
    <span data-ttu-id="c1dc8-129">(в) Для остановки службы MySQL выполните команду:</span><span class="sxs-lookup"><span data-stu-id="c1dc8-129">(c) Stop MySQL service</span></span>
  
             #[root@mysqlnode ~]# service mysql stop
  
    <span data-ttu-id="c1dc8-130">(d) перезапустите службу MySQL hello</span><span class="sxs-lookup"><span data-stu-id="c1dc8-130">(d) Restart hello MySQL service</span></span>
  
             #[root@mysqlnode ~]# service mysql restart

### <a name="how-tooinstall-mysql-on-red-hat-os-family-like-centos-oracle-linux"></a><span data-ttu-id="c1dc8-131">Как CentOS, Oracle Linux tooinstall MySQL в семействе ОС Red Hat</span><span class="sxs-lookup"><span data-stu-id="c1dc8-131">How tooinstall MySQL on Red Hat OS family like CentOS, Oracle Linux</span></span>
<span data-ttu-id="c1dc8-132">Здесь мы будем использовать виртуальную машину Linux с CentOS или Oracle Linux.</span><span class="sxs-lookup"><span data-stu-id="c1dc8-132">We will use Linux VM with CentOS or Oracle Linux here.</span></span>

* <span data-ttu-id="c1dc8-133">Шаг 1: Добавление hello MySQL Yum репозитория коммутатора слишком`root` пользователя:</span><span class="sxs-lookup"><span data-stu-id="c1dc8-133">Step 1: Add hello MySQL Yum repository   Switch too`root` user:</span></span>
  
            #[azureuser@mysqlnode:~]sudo su -
  
    <span data-ttu-id="c1dc8-134">Загрузите и установите пакет выпуска hello MySQL.</span><span class="sxs-lookup"><span data-stu-id="c1dc8-134">Download and install hello MySQL release package:</span></span>
  
            #[root@mysqlnode ~]# wget http://repo.mysql.com/mysql-community-release-el6-5.noarch.rpm
            #[root@mysqlnode ~]# yum localinstall -y mysql-community-release-el6-5.noarch.rpm
* <span data-ttu-id="c1dc8-135">Шаг 2: Измените ниже репозитория MySQL hello tooenable файл для загрузки пакета MySQL5.6 hello.</span><span class="sxs-lookup"><span data-stu-id="c1dc8-135">Step 2: Edit below file tooenable hello MySQL repository for downloading hello MySQL5.6 package.</span></span>
  
            #[root@mysqlnode ~]# vim /etc/yum.repos.d/mysql-community.repo
  
    <span data-ttu-id="c1dc8-136">Обновление для каждого значения toobelow этот файл:</span><span class="sxs-lookup"><span data-stu-id="c1dc8-136">Update each value of this file toobelow:</span></span>
  
        \# *Enable toouse MySQL 5.6*
  
        [mysql56-community]
        name=MySQL 5.6 Community Server
  
        baseurl=http://repo.mysql.com/yum/mysql-5.6-community/el/6/$basearch/
  
        enabled=1
  
        gpgcheck=1
  
        gpgkey=file:/etc/pki/rpm-gpg/RPM-GPG-KEY-mysql
* <span data-ttu-id="c1dc8-137">Шаг 3. Установка MySQL из репозитория MySQL. Установите MySQL:</span><span class="sxs-lookup"><span data-stu-id="c1dc8-137">Step 3: Install MySQL from MySQL repository   Install MySQL:</span></span>
  
           #[root@mysqlnode ~]#yum install mysql-community-server
  
    <span data-ttu-id="c1dc8-138">Будут установлены пакет MySQL RPM и все связанные пакеты.</span><span class="sxs-lookup"><span data-stu-id="c1dc8-138">MySQL RPM package and all related packages will be installed.</span></span>
* <span data-ttu-id="c1dc8-139">Шаг 4: Управление службой MySQL hello</span><span class="sxs-lookup"><span data-stu-id="c1dc8-139">Step 4: Manage hello running MySQL service</span></span>
  
    <span data-ttu-id="c1dc8-140">(a) Проверьте состояние службы hello hello MySQL server.</span><span class="sxs-lookup"><span data-stu-id="c1dc8-140">(a) Check hello service status of hello MySQL server:</span></span>
  
           #[root@mysqlnode ~]#service mysqld status
  
    <span data-ttu-id="c1dc8-141">(b) Проверьте, работает ли сервер порта MySQL по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="c1dc8-141">(b) Check whether hello default port of  MySQL server is running:</span></span>
  
           #[root@mysqlnode ~]#netstat  –tunlp|grep 3306

    <span data-ttu-id="c1dc8-142">(c) сервер MySQL hello начала:</span><span class="sxs-lookup"><span data-stu-id="c1dc8-142">(c) Start hello MySQL server:</span></span>

           #[root@mysqlnode ~]#service mysqld start

    <span data-ttu-id="c1dc8-143">(d) остановите сервер MySQL hello:</span><span class="sxs-lookup"><span data-stu-id="c1dc8-143">(d) Stop hello MySQL server:</span></span>

           #[root@mysqlnode ~]#service mysqld stop

    <span data-ttu-id="c1dc8-144">(e) при включении системы hello установите MySQL toostart:</span><span class="sxs-lookup"><span data-stu-id="c1dc8-144">(e) Set MySQL toostart when hello system boot-up:</span></span>

           #[root@mysqlnode ~]#chkconfig mysqld on


### <a name="how-tooinstall-mysql-on-suse-linux"></a><span data-ttu-id="c1dc8-145">Как tooinstall MySQL в SUSE Linux</span><span class="sxs-lookup"><span data-stu-id="c1dc8-145">How tooinstall MySQL on SUSE Linux</span></span>
<span data-ttu-id="c1dc8-146">Здесь мы будем использовать виртуальную машину Linux с OpenSUSE.</span><span class="sxs-lookup"><span data-stu-id="c1dc8-146">We will use Linux VM with OpenSUSE here.</span></span>

* <span data-ttu-id="c1dc8-147">Шаг 1. Скачивание и установка MySQL Server</span><span class="sxs-lookup"><span data-stu-id="c1dc8-147">Step 1: Download and install MySQL Server</span></span>
  
    <span data-ttu-id="c1dc8-148">Переключение слишком`root` пользователя с помощью ниже команду:</span><span class="sxs-lookup"><span data-stu-id="c1dc8-148">Switch too`root` user through below command:</span></span>  
  
           #sudo su -
  
    <span data-ttu-id="c1dc8-149">Скачайте и установите пакет MySQL:</span><span class="sxs-lookup"><span data-stu-id="c1dc8-149">Download and install MySQL package:</span></span>
  
           #[root@mysqlnode ~]# zypper update
  
           #[root@mysqlnode ~]# zypper install mysql-server mysql-devel mysql
* <span data-ttu-id="c1dc8-150">Шаг 2: Управление службой MySQL hello</span><span class="sxs-lookup"><span data-stu-id="c1dc8-150">Step 2: Manage hello running MySQL service</span></span>
  
    <span data-ttu-id="c1dc8-151">(a) Проверьте состояние hello hello MySQL server.</span><span class="sxs-lookup"><span data-stu-id="c1dc8-151">(a) Check hello status of hello MySQL server:</span></span>
  
           #[root@mysqlnode ~]# rcmysql status
  
    <span data-ttu-id="c1dc8-152">(b) Проверьте, является ли hello порт по умолчанию hello MySQL server:</span><span class="sxs-lookup"><span data-stu-id="c1dc8-152">(b) Check whether hello default port of hello MySQL server:</span></span>
  
           #[root@mysqlnode ~]# netstat  –tunlp|grep 3306

    <span data-ttu-id="c1dc8-153">(c) сервер MySQL hello начала:</span><span class="sxs-lookup"><span data-stu-id="c1dc8-153">(c) Start hello MySQL server:</span></span>

           #[root@mysqlnode ~]# rcmysql start

    <span data-ttu-id="c1dc8-154">(d) остановите сервер MySQL hello:</span><span class="sxs-lookup"><span data-stu-id="c1dc8-154">(d) Stop hello MySQL server:</span></span>

           #[root@mysqlnode ~]# rcmysql stop

    <span data-ttu-id="c1dc8-155">(e) при включении системы hello установите MySQL toostart:</span><span class="sxs-lookup"><span data-stu-id="c1dc8-155">(e) Set MySQL toostart when hello system boot-up:</span></span>

           #[root@mysqlnode ~]# insserv mysql

### <a name="next-step"></a><span data-ttu-id="c1dc8-156">Дальнейшее действие</span><span class="sxs-lookup"><span data-stu-id="c1dc8-156">Next Step</span></span>
<span data-ttu-id="c1dc8-157">Дополнительные сведения и сведения об использовании MySQL см. [здесь](https://www.mysql.com/).</span><span class="sxs-lookup"><span data-stu-id="c1dc8-157">Find more usage and information regarding MySQL [Here](https://www.mysql.com/).</span></span>

