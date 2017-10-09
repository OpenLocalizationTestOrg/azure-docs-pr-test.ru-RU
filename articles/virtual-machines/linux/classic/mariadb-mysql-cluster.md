---
title: "aaaRun MariaDB (MySQL) кластера в Azure | Документы Microsoft"
description: "Создание кластеров MariaDB + Galera (MySQL) на виртуальных машинах Azure"
services: virtual-machines-linux
documentationcenter: 
author: sabbour
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: d0d21937-7aac-4222-8255-2fdc4f2ea65b
ms.service: virtual-machines-linux
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 04/15/2015
ms.author: asabbour
ms.openlocfilehash: f9a4d6c45d76478a8a3526b407c7bbe6aeb40423
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="mariadb-mysql-cluster-azure-tutorial"></a><span data-ttu-id="cfdd8-103">Кластер MariaDB (MySQL) — руководство по Azure</span><span class="sxs-lookup"><span data-stu-id="cfdd8-103">MariaDB (MySQL) cluster: Azure tutorial</span></span>
> [!IMPORTANT]
> <span data-ttu-id="cfdd8-104">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель Azure Resource Manager](../../../resource-manager-deployment-model.md) и классическая модель.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-104">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager](../../../resource-manager-deployment-model.md) and classic.</span></span> <span data-ttu-id="cfdd8-105">В этой статье рассматриваются hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-105">This article covers hello classic deployment model.</span></span> <span data-ttu-id="cfdd8-106">Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-106">Microsoft recommends that most new deployments use hello Azure Resource Manager model.</span></span>

> [!NOTE]
> <span data-ttu-id="cfdd8-107">Кластер выпуска MariaDB Enterprise теперь доступен в hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-107">MariaDB Enterprise cluster is now available in hello Azure Marketplace.</span></span> <span data-ttu-id="cfdd8-108">Hello новое предложение будет автоматически развернуть кластер MariaDB Galera от диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-108">hello new offering will automatically deploy a MariaDB Galera cluster on Azure Resource Manager.</span></span> <span data-ttu-id="cfdd8-109">Следует использовать новое предложение hello из [Azure Marketplace](https://azure.microsoft.com/en-us/marketplace/partners/mariadb/cluster-maxscale/).</span><span class="sxs-lookup"><span data-stu-id="cfdd8-109">You should use hello new offering from [Azure Marketplace](https://azure.microsoft.com/en-us/marketplace/partners/mariadb/cluster-maxscale/).</span></span>
>
>

<span data-ttu-id="cfdd8-110">В этой статье показано, как toocreate несколькими Master [Galera](http://galeracluster.com/products/) кластер [MariaDBs](https://mariadb.org/en/about/) (сборка надежные, масштабируемые и надежные замена MySQL) toowork в среде высокой доступности в Azure виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-110">This article shows you how toocreate a multi-Master [Galera](http://galeracluster.com/products/) cluster of [MariaDBs](https://mariadb.org/en/about/) (a robust, scalable, and reliable drop-in replacement for MySQL) toowork in a highly available environment on Azure virtual machines.</span></span>

## <a name="architecture-overview"></a><span data-ttu-id="cfdd8-111">Общие сведения об архитектуре</span><span class="sxs-lookup"><span data-stu-id="cfdd8-111">Architecture overview</span></span>
<span data-ttu-id="cfdd8-112">В этой статье описывается как hello toocomplete следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="cfdd8-112">This article describes how toocomplete hello following steps:</span></span>

- <span data-ttu-id="cfdd8-113">Создать кластер с тремя узлами.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-113">Create a three-node cluster.</span></span>
- <span data-ttu-id="cfdd8-114">Отдельные hello дисков данных с диска ОС hello.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-114">Separate hello data disks from hello OS disk.</span></span>
- <span data-ttu-id="cfdd8-115">Создание дисков данных hello в RAID 0 или чередованием параметр tooincrease операций ввода-ВЫВОДА.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-115">Create hello data disks in RAID-0/striped setting tooincrease IOPS.</span></span>
- <span data-ttu-id="cfdd8-116">Используйте нагрузки hello toobalance подсистемы балансировки нагрузки Azure для hello трех узлов.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-116">Use Azure Load Balancer toobalance hello load for hello three nodes.</span></span>
- <span data-ttu-id="cfdd8-117">повторяющиеся toominimize, создание образа виртуальной Машины, который содержит MariaDB + Galera, необходимо использовать toocreate hello других ВМ кластера.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-117">toominimize repetitive work, create a VM image that contains MariaDB + Galera and use it toocreate hello other cluster VMs.</span></span>

![Архитектура системы](./media/mariadb-mysql-cluster/Setup.png)

> [!NOTE]
> <span data-ttu-id="cfdd8-119">В этом разделе используется hello [Azure CLI](../../../cli-install-nodejs.md) средства, поэтому следует убедиться, что toodownload их и подключите их соответствующим инструкциям toohello tooyour подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-119">This topic uses hello [Azure CLI](../../../cli-install-nodejs.md) tools, so make sure toodownload them and connect them tooyour Azure subscription according toohello instructions.</span></span> <span data-ttu-id="cfdd8-120">Ссылка toohello команд, доступных в hello Azure CLI, в статье hello [Справочник по командам Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="cfdd8-120">If you need a reference toohello commands available in hello Azure CLI, see hello [Azure CLI command reference](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span> <span data-ttu-id="cfdd8-121">Необходимо также слишком[создайте ключ SSH для проверки подлинности] и запишите расположение файла .pem hello.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-121">You will also need too[create an SSH key for authentication] and make note of hello .pem file location.</span></span>
>
>

## <a name="create-hello-template"></a><span data-ttu-id="cfdd8-122">Создание шаблона hello</span><span class="sxs-lookup"><span data-stu-id="cfdd8-122">Create hello template</span></span>
### <a name="infrastructure"></a><span data-ttu-id="cfdd8-123">Инфраструктура</span><span class="sxs-lookup"><span data-stu-id="cfdd8-123">Infrastructure</span></span>
1. <span data-ttu-id="cfdd8-124">Создайте территориальную группу toohold hello ресурсы друг с другом.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-124">Create an affinity group toohold hello resources together.</span></span>

        azure account affinity-group create mariadbcluster --location "North Europe" --label "MariaDB Cluster"
2. <span data-ttu-id="cfdd8-125">Создайте виртуальную сеть.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-125">Create a virtual network.</span></span>

        azure network vnet create --address-space 10.0.0.0 --cidr 8 --subnet-name mariadb --subnet-start-ip 10.0.0.0 --subnet-cidr 24 --affinity-group mariadbcluster mariadbvnet
3. <span data-ttu-id="cfdd8-126">Создание учетной записи хранилища toohost все диски.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-126">Create a storage account toohost all our disks.</span></span> <span data-ttu-id="cfdd8-127">Более 40 интенсивно используемых дисков не следует разместить на hello же tooavoid учетной записи хранилища, попадание учетной записи hello 20 000 операций ввода-ВЫВОДА хранилища.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-127">You shouldn't place more than 40 heavily used disks on hello same storage account tooavoid hitting hello 20,000 IOPS storage account limit.</span></span> <span data-ttu-id="cfdd8-128">В этом случае вы гораздо ниже этого предела, поэтому все данные будут храниться на учетную запись для простоты hello.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-128">In this case, you're well below that limit, so you'll store everything on hello same account for simplicity.</span></span>

        azure storage account create mariadbstorage --label mariadbstorage --affinity-group mariadbcluster
4. <span data-ttu-id="cfdd8-129">Найти имя образа виртуальной машины CentOS 7 hello hello.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-129">Find hello name of hello CentOS 7 virtual machine image.</span></span>

        azure vm image list | findstr CentOS
   <span data-ttu-id="cfdd8-130">Hello вывода будет примерно `5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20140926`.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-130">hello output will be something like `5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20140926`.</span></span>

   <span data-ttu-id="cfdd8-131">Используйте это имя в даст hello.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-131">Use that name in hello following step.</span></span>
5. <span data-ttu-id="cfdd8-132">Создание шаблона виртуальной Машины hello и замените /path/to/key.pem hello путь хранения hello созданный .pem SSH-ключ.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-132">Create hello VM template and replace /path/to/key.pem with hello path where you stored hello generated .pem SSH key.</span></span>

        azure vm create --virtual-network-name mariadbvnet --subnet-names mariadb --blob-url "http://mariadbstorage.blob.core.windows.net/vhds/mariadbhatemplate-os.vhd"  --vm-size Medium --ssh 22 --ssh-cert "/path/to/key.pem" --no-ssh-password mariadbtemplate 5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20140926 azureuser
6. <span data-ttu-id="cfdd8-133">Присоединение дисков toohello четыре 500 ГБ данных виртуальной Машины для использования в конфигурации RAID hello.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-133">Attach four 500-GB data disks toohello VM for use in hello RAID configuration.</span></span>

        FOR /L %d IN (1,1,4) DO azure vm disk attach-new mariadbhatemplate 512 http://mariadbstorage.blob.core.windows.net/vhds/mariadbhatemplate-data-%d.vhd
7. <span data-ttu-id="cfdd8-134">Использовать SSH toosign в toohello шаблона виртуальной Машины, созданной в mariadbhatemplate.cloudapp.net:22 и подключитесь с помощью закрытого ключа.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-134">Use SSH toosign in toohello template VM that you created at mariadbhatemplate.cloudapp.net:22, and connect by using your private key.</span></span>

### <a name="software"></a><span data-ttu-id="cfdd8-135">Программное обеспечение</span><span class="sxs-lookup"><span data-stu-id="cfdd8-135">Software</span></span>
1. <span data-ttu-id="cfdd8-136">Получите корень hello.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-136">Get hello root.</span></span>

        sudo su

2. <span data-ttu-id="cfdd8-137">Установка поддержки RAID:</span><span class="sxs-lookup"><span data-stu-id="cfdd8-137">Install RAID support:</span></span>

    <span data-ttu-id="cfdd8-138">а.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-138">a.</span></span> <span data-ttu-id="cfdd8-139">Установите mdadm.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-139">Install mdadm.</span></span>

              yum install mdadm

    <span data-ttu-id="cfdd8-140">b.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-140">b.</span></span> <span data-ttu-id="cfdd8-141">Создайте конфигурацию RAID0/stripe hello EXT4 файловой системе.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-141">Create hello RAID0/stripe configuration with an EXT4 file system.</span></span>

              mdadm --create --verbose /dev/md0 --level=stripe --raid-devices=4 /dev/sdc /dev/sdd /dev/sde /dev/sdf
              mdadm --detail --scan >> /etc/mdadm.conf
              mkfs -t ext4 /dev/md0
    <span data-ttu-id="cfdd8-142">c.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-142">c.</span></span> <span data-ttu-id="cfdd8-143">Создайте каталог точки подключения hello.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-143">Create hello mount point directory.</span></span>

              mkdir /mnt/data
    <span data-ttu-id="cfdd8-144">d.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-144">d.</span></span> <span data-ttu-id="cfdd8-145">Получить hello UUID hello вновь созданные устройства RAID.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-145">Retrieve hello UUID of hello newly created RAID device.</span></span>

              blkid | grep /dev/md0
    <span data-ttu-id="cfdd8-146">д.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-146">e.</span></span> <span data-ttu-id="cfdd8-147">Измените файл /etc/fstab.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-147">Edit /etc/fstab.</span></span>

              vi /etc/fstab
    <span data-ttu-id="cfdd8-148">f.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-148">f.</span></span> <span data-ttu-id="cfdd8-149">Добавить hello устройства tooenable автоматическое подключение при перезагрузке, заменив значение hello hello UUID, полученный от предыдущего hello **блок идентификатором blkid** команды.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-149">Add hello device tooenable auto mounting on reboot, replacing hello UUID with hello value obtained from hello previous **blkid** command.</span></span>

              UUID=<UUID FROM PREVIOUS>   /mnt/data ext4   defaults,noatime   1 2
    <span data-ttu-id="cfdd8-150">ж.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-150">g.</span></span> <span data-ttu-id="cfdd8-151">Подключите новый раздел hello.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-151">Mount hello new partition.</span></span>

              mount /mnt/data

3. <span data-ttu-id="cfdd8-152">Установите MariaDB.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-152">Install MariaDB.</span></span>

    <span data-ttu-id="cfdd8-153">а.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-153">a.</span></span> <span data-ttu-id="cfdd8-154">Создайте файл MariaDB.repo hello.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-154">Create hello MariaDB.repo file.</span></span>

                vi /etc/yum.repos.d/MariaDB.repo

    <span data-ttu-id="cfdd8-155">b.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-155">b.</span></span> <span data-ttu-id="cfdd8-156">Заполните hello после содержимого файла hello репозитория:</span><span class="sxs-lookup"><span data-stu-id="cfdd8-156">Fill hello repo file with hello following content:</span></span>

              [mariadb]
              name = MariaDB
              baseurl = http://yum.mariadb.org/10.0/centos7-amd64
              gpgkey=https://yum.mariadb.org/RPM-GPG-KEY-MariaDB
              gpgcheck=1
    <span data-ttu-id="cfdd8-157">c.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-157">c.</span></span> <span data-ttu-id="cfdd8-158">конфликты tooavoid удалите существующие постфиксная и mariadb библиотеки.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-158">tooavoid conflicts, remove existing postfix and mariadb-libs.</span></span>

           yum remove postfix mariadb-libs-*
    <span data-ttu-id="cfdd8-159">d.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-159">d.</span></span> <span data-ttu-id="cfdd8-160">Установите MariaDB с Galera.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-160">Install MariaDB with Galera.</span></span>

           yum install MariaDB-Galera-server MariaDB-client galera

4. <span data-ttu-id="cfdd8-161">Переместите hello каталог данных MySQL toohello устройство блока RAID.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-161">Move hello MySQL data directory toohello RAID block device.</span></span>

    <span data-ttu-id="cfdd8-162">а.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-162">a.</span></span> <span data-ttu-id="cfdd8-163">Скопируйте текущий каталог MySQL hello в новое место и удалите прежний каталог hello.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-163">Copy hello current MySQL directory into its new location and remove hello old directory.</span></span>

           cp -avr /var/lib/mysql /mnt/data  
           rm -rf /var/lib/mysql
    <span data-ttu-id="cfdd8-164">b.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-164">b.</span></span> <span data-ttu-id="cfdd8-165">Установите разрешения для нового каталога hello соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-165">Set permissions for hello new directory accordingly.</span></span>

           chown -R mysql:mysql /mnt/data && chmod -R 755 /mnt/data/

    <span data-ttu-id="cfdd8-166">c.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-166">c.</span></span> <span data-ttu-id="cfdd8-167">Создайте символьную ссылку, указывающий hello старого каталога toohello новое расположение на hello RAID-массива.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-167">Create a symlink that points hello old directory toohello new location on hello RAID partition.</span></span>

           ln -s /mnt/data/mysql /var/lib/mysql

5. <span data-ttu-id="cfdd8-168">Так как [SELinux мешает операций кластера hello](http://galeracluster.com/documentation-webpages/configuration.html#selinux), это toodisable необходимые им для hello текущего сеанса.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-168">Because [SELinux interferes with hello cluster operations](http://galeracluster.com/documentation-webpages/configuration.html#selinux), it is necessary toodisable it for hello current session.</span></span> <span data-ttu-id="cfdd8-169">Изменить `/etc/selinux/config` toodisable его для последующей перезагрузки.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-169">Edit `/etc/selinux/config` toodisable it for subsequent restarts.</span></span>

            setenforce 0

            then editing `/etc/selinux/config` tooset `SELINUX=permissive`
6. <span data-ttu-id="cfdd8-170">Убедитесь, что MySQL работает.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-170">Validate MySQL runs.</span></span>

   <span data-ttu-id="cfdd8-171">а.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-171">a.</span></span> <span data-ttu-id="cfdd8-172">Запустите MySQL.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-172">Start MySQL.</span></span>

           service mysql start
   <span data-ttu-id="cfdd8-173">b.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-173">b.</span></span> <span data-ttu-id="cfdd8-174">Secure установки MySQL hello, задать пароль учетной записи root hello, удалить имя входа удаленного корневого элемента toodisable анонимных пользователей и удалить hello тестовую базу данных.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-174">Secure hello MySQL installation, set hello root password, remove anonymous users toodisable remote root login, and remove hello test database.</span></span>

           mysql_secure_installation
   <span data-ttu-id="cfdd8-175">c.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-175">c.</span></span> <span data-ttu-id="cfdd8-176">Создание пользователя в базе данных hello для операции кластера и при необходимости для приложений.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-176">Create a user on hello database for cluster operations, and optionally for your applications.</span></span>

           mysql -u root -p
           GRANT ALL PRIVILEGES ON *.* too'cluster'@'%' IDENTIFIED BY 'p@ssw0rd' WITH GRANT OPTION; FLUSH PRIVILEGES;
           exit

   <span data-ttu-id="cfdd8-177">d.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-177">d.</span></span> <span data-ttu-id="cfdd8-178">Остановите работу MySQL.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-178">Stop MySQL.</span></span>

            service mysql stop
7. <span data-ttu-id="cfdd8-179">Создайте заполнитель конфигурации.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-179">Create a configuration placeholder.</span></span>

   <span data-ttu-id="cfdd8-180">а.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-180">a.</span></span> <span data-ttu-id="cfdd8-181">Измените toocreate конфигурации MySQL hello заполнитель для настройки кластера hello.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-181">Edit hello MySQL configuration toocreate a placeholder for hello cluster settings.</span></span> <span data-ttu-id="cfdd8-182">Не заменяйте hello  **`<Variables>`**  или раскомментируйте теперь.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-182">Do not replace hello **`<Variables>`** or uncomment now.</span></span> <span data-ttu-id="cfdd8-183">Это произойдет после создания виртуальной машины из этого шаблона.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-183">That will happen after you create a VM from this template.</span></span>

            vi /etc/my.cnf.d/server.cnf
   <span data-ttu-id="cfdd8-184">b.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-184">b.</span></span> <span data-ttu-id="cfdd8-185">Изменить hello  **[galera]**  статьи и ее необходимо очистить.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-185">Edit hello **[galera]** section and clear it out.</span></span>

   <span data-ttu-id="cfdd8-186">c.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-186">c.</span></span> <span data-ttu-id="cfdd8-187">Изменить hello **[mariadb]** раздела.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-187">Edit hello **[mariadb]** section.</span></span>

           wsrep_provider=/usr/lib64/galera/libgalera_smm.so
           binlog_format=ROW
           wsrep_sst_method=rsync
           bind-address=0.0.0.0 # When set too0.0.0.0, hello server listens tooremote connections
           default_storage_engine=InnoDB
           innodb_autoinc_lock_mode=2

           wsrep_sst_auth=cluster:p@ssw0rd # CHANGE: Username and password you created for hello SST cluster MySQL user
           #wsrep_cluster_name='mariadbcluster' # CHANGE: Uncomment and set your desired cluster name
           #wsrep_cluster_address="gcomm://mariadb1,mariadb2,mariadb3" # CHANGE: Uncomment and Add all your servers
           #wsrep_node_address='<ServerIP>' # CHANGE: Uncomment and set IP address of this server
           #wsrep_node_name='<NodeName>' # CHANGE: Uncomment and set hello node name of this server
8. <span data-ttu-id="cfdd8-188">Необходимые порты в брандмауэре hello откройте с помощью FirewallD на CentOS 7.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-188">Open required ports on hello firewall by using FirewallD on CentOS 7.</span></span>

   * <span data-ttu-id="cfdd8-189">MySQL: `firewall-cmd --zone=public --add-port=3306/tcp --permanent`</span><span class="sxs-lookup"><span data-stu-id="cfdd8-189">MySQL: `firewall-cmd --zone=public --add-port=3306/tcp --permanent`</span></span>
   * <span data-ttu-id="cfdd8-190">GALERA: `firewall-cmd --zone=public --add-port=4567/tcp --permanent`</span><span class="sxs-lookup"><span data-stu-id="cfdd8-190">GALERA: `firewall-cmd --zone=public --add-port=4567/tcp --permanent`</span></span>
   * <span data-ttu-id="cfdd8-191">GALERA IST: `firewall-cmd --zone=public --add-port=4568/tcp --permanent`</span><span class="sxs-lookup"><span data-stu-id="cfdd8-191">GALERA IST: `firewall-cmd --zone=public --add-port=4568/tcp --permanent`</span></span>
   * <span data-ttu-id="cfdd8-192">RSYNC: `firewall-cmd --zone=public --add-port=4444/tcp --permanent`</span><span class="sxs-lookup"><span data-stu-id="cfdd8-192">RSYNC: `firewall-cmd --zone=public --add-port=4444/tcp --permanent`</span></span>
   * <span data-ttu-id="cfdd8-193">Перезагрузите hello брандмауэра:`firewall-cmd --reload`</span><span class="sxs-lookup"><span data-stu-id="cfdd8-193">Reload hello firewall: `firewall-cmd --reload`</span></span>

9. <span data-ttu-id="cfdd8-194">Оптимизация производительности системы hello.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-194">Optimize hello system for performance.</span></span> <span data-ttu-id="cfdd8-195">Дополнительные сведения см. в статье [Оптимизация производительности MySQL в виртуальных машинах Azure Linux](optimize-mysql.md).</span><span class="sxs-lookup"><span data-stu-id="cfdd8-195">For more information, see [performance tuning strategy](optimize-mysql.md).</span></span>

   <span data-ttu-id="cfdd8-196">а.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-196">a.</span></span> <span data-ttu-id="cfdd8-197">Изменение файла конфигурации MySQL hello еще раз.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-197">Edit hello MySQL configuration file again.</span></span>

            vi /etc/my.cnf.d/server.cnf
   <span data-ttu-id="cfdd8-198">b.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-198">b.</span></span> <span data-ttu-id="cfdd8-199">Изменить hello **[mariadb]** статьи и добавления hello после содержимого:</span><span class="sxs-lookup"><span data-stu-id="cfdd8-199">Edit hello **[mariadb]** section and append hello following content:</span></span>

   > [!NOTE]
   > <span data-ttu-id="cfdd8-200">Рекомендуемое значение innodb\_buffer\_pool_size составляет 70 % от памяти виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-200">We recommend that innodb\_buffer\_pool_size is 70 percent of your VM's memory.</span></span> <span data-ttu-id="cfdd8-201">В этом примере он был задан 2,45 ГБ для средних hello Azure VM with 3,5 ГБ ОЗУ.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-201">In this example, it has been set at 2.45 GB for hello medium Azure VM with 3.5 GB of RAM.</span></span>
   >
   >

           innodb_buffer_pool_size = 2508M # hello buffer pool contains buffered data and hello index. This is usually set too70 percent of physical memory.
           innodb_log_file_size = 512M #  Redo logs ensure that write operations are fast, reliable, and recoverable after a crash
           max_connections = 5000 # A larger value will give hello server more time toorecycle idled connections
           innodb_file_per_table = 1 # Speed up hello table space transmission and optimize hello debris management performance
           innodb_log_buffer_size = 128M # hello log buffer allows transactions toorun without having tooflush hello log toodisk before hello transactions commit
           innodb_flush_log_at_trx_commit = 2 # hello setting of 2 enables hello most data integrity and is suitable for Master in MySQL cluster
           query_cache_size = 0
10. <span data-ttu-id="cfdd8-202">Остановить MySQL, отключить службу MySQL по tooavoid запуска, приостановки hello кластера при добавлении узла и отменить подготовку компьютера hello.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-202">Stop MySQL, disable MySQL service from running on startup tooavoid disrupting hello cluster when adding a node, and deprovision hello machine.</span></span>

        service mysql stop
        chkconfig mysql off
        waagent -deprovision
11. <span data-ttu-id="cfdd8-203">Запишите hello виртуальной Машины через портал hello.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-203">Capture hello VM through hello portal.</span></span> <span data-ttu-id="cfdd8-204">(В настоящее время [выдавать &#1268; в средствах Azure CLI hello](https://github.com/Azure/azure-xplat-cli/issues/1268) описывает hello факт, что образы, созданные средствами hello Azure CLI не выполняется сбор hello присоединенные диски данных.)</span><span class="sxs-lookup"><span data-stu-id="cfdd8-204">(Currently, [issue #1268 in hello Azure CLI tools](https://github.com/Azure/azure-xplat-cli/issues/1268) describes hello fact that images captured by hello Azure CLI tools do not capture hello attached data disks.)</span></span>

    <span data-ttu-id="cfdd8-205">а.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-205">a.</span></span> <span data-ttu-id="cfdd8-206">Завершите работу hello машины через портал hello.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-206">Shut down hello machine through hello portal.</span></span>

    <span data-ttu-id="cfdd8-207">b.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-207">b.</span></span> <span data-ttu-id="cfdd8-208">Нажмите кнопку **захвата** и укажите имя образа hello как **mariadb galera изображениями**.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-208">Click **Capture** and specify hello image name as **mariadb-galera-image**.</span></span> <span data-ttu-id="cfdd8-209">Введите описание и установите флажок "команда waagent -deprovision запущена на виртуальной машине".</span><span class="sxs-lookup"><span data-stu-id="cfdd8-209">Provide a description and check "I have run waagent."</span></span>
      
      ![Запись hello виртуальной машины](./media/mariadb-mysql-cluster/Capture2.PNG)

## <a name="create-hello-cluster"></a><span data-ttu-id="cfdd8-211">Создание кластера hello</span><span class="sxs-lookup"><span data-stu-id="cfdd8-211">Create hello cluster</span></span>
<span data-ttu-id="cfdd8-212">Создайте три виртуальные машины с hello шаблон создан и затем выполняется настройка и запуск hello кластера.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-212">Create three VMs with hello template you created, and then configure and start hello cluster.</span></span>

1. <span data-ttu-id="cfdd8-213">Создайте hello первой виртуальной Машины CentOS 7 из hello mariadb-galera образа образ был создан, предоставляя hello следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="cfdd8-213">Create hello first CentOS 7 VM from hello mariadb-galera-image image you created, providing hello following information:</span></span>

 - <span data-ttu-id="cfdd8-214">Имя виртуальной сети: mariadbvnet.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-214">Virtual network name: mariadbvnet</span></span>
 - <span data-ttu-id="cfdd8-215">Подсеть: mariadb.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-215">Subnet: mariadb</span></span>
 - <span data-ttu-id="cfdd8-216">Размер машины: средний.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-216">Machine size: medium</span></span>
 - <span data-ttu-id="cfdd8-217">Имя облачной службы: mariadbha (или любое имя по требуется доступ через mariadbha.cloudapp.net toobe)</span><span class="sxs-lookup"><span data-stu-id="cfdd8-217">Cloud service name: mariadbha (or whatever name you want toobe accessed through mariadbha.cloudapp.net)</span></span>
 - <span data-ttu-id="cfdd8-218">Имя машины: mariadb1.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-218">Machine name: mariadb1</span></span>
 - <span data-ttu-id="cfdd8-219">Имя пользователя: azureuser.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-219">Username: azureuser</span></span>
 - <span data-ttu-id="cfdd8-220">SSH-доступ: включен.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-220">SSH access: enabled</span></span>
 - <span data-ttu-id="cfdd8-221">Передача PEM-файл сертификата SSH hello и замены /path/to/key.pem hello путь, где хранится hello создан .pem SSH-ключ.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-221">Passing hello SSH certificate .pem file and replacing /path/to/key.pem with hello path where you stored hello generated .pem SSH key.</span></span>

   > [!NOTE]
   > <span data-ttu-id="cfdd8-222">Hello следующие команды разбиваются на несколько строк для ясности, но сначала следует вводить как одну строку.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-222">hello following commands are split over multiple lines for clarity, but you should enter each as one line.</span></span>
   >
   >
        azure vm create
        --virtual-network-name mariadbvnet
        --subnet-names mariadb
        --availability-set clusteravset
        --vm-size Medium
        --ssh-cert "/path/to/key.pem"
        --no-ssh-password
        --ssh 22
        --vm-name mariadb1
        mariadbha mariadb-galera-image azureuser
2. <span data-ttu-id="cfdd8-223">Создайте дополнительные виртуальные машины, подключив их toohello mariadbha облачной службы.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-223">Create two more virtual machines by connecting them toohello mariadbha cloud service.</span></span> <span data-ttu-id="cfdd8-224">Здравствуйте, изменить имя виртуальной Машины hello и hello порт tooa уникальный порт SSH не конфликтует с других виртуальных машин в одной облачной службе.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-224">Change hello VM name and hello SSH port tooa unique port not conflicting with other VMs in hello same cloud service.</span></span>

        azure vm create
        --virtual-network-name mariadbvnet
        --subnet-names mariadb
        --availability-set clusteravset
        --vm-size Medium
        --ssh-cert "/path/to/key.pem"
        --no-ssh-password
        --ssh 23
        --vm-name mariadb2
        --connect mariadbha mariadb-galera-image azureuser
  <span data-ttu-id="cfdd8-225">Для MariaDB3:</span><span class="sxs-lookup"><span data-stu-id="cfdd8-225">For MariaDB3:</span></span>

        azure vm create
        --virtual-network-name mariadbvnet
        --subnet-names mariadb
        --availability-set clusteravset
        --vm-size Medium
        --ssh-cert "/path/to/key.pem"
        --no-ssh-password
        --ssh 24
        --vm-name mariadb3
        --connect mariadbha mariadb-galera-image azureuser
3. <span data-ttu-id="cfdd8-226">Вам потребуется tooget hello внутренний IP-адрес каждого hello трех виртуальных машин для hello следующий шаг:</span><span class="sxs-lookup"><span data-stu-id="cfdd8-226">You will need tooget hello internal IP address of each of hello three VMs for hello next step:</span></span>

    ![Получение IP-адреса](./media/mariadb-mysql-cluster/IP.png)
4. <span data-ttu-id="cfdd8-228">Используйте SSH toosign в toohello три виртуальные машины и изменить файл конфигурации hello в каждой из них.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-228">Use SSH toosign in toohello three VMs and edit hello configuration file on each of them.</span></span>

        sudo vi /etc/my.cnf.d/server.cnf

    <span data-ttu-id="cfdd8-229">Раскомментируйте  **`wsrep_cluster_name`**  и  **`wsrep_cluster_address`**  , удалив hello  **#**  в начале строки hello hello.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-229">Uncomment **`wsrep_cluster_name`** and **`wsrep_cluster_address`** by removing hello **#** at hello beginning of hello line.</span></span>
    <span data-ttu-id="cfdd8-230">Кроме того, замените  **`<ServerIP>`**  в  **`wsrep_node_address`**  и  **`<NodeName>`**  в  **`wsrep_node_name`**  с hello Виртуальной машины IP адрес и имя, соответственно, раскомментируйте эти строки также.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-230">Additionally, replace **`<ServerIP>`** in **`wsrep_node_address`** and **`<NodeName>`** in **`wsrep_node_name`** with hello VM's IP address and name, respectively, and uncomment those lines as well.</span></span>
5. <span data-ttu-id="cfdd8-231">Запустите кластер hello на MariaDB1 и дать ему возможность работать во время запуска.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-231">Start hello cluster on MariaDB1 and let it run at startup.</span></span>

        sudo service mysql bootstrap
        chkconfig mysql on
6. <span data-ttu-id="cfdd8-232">Запустите MySQL в MariaDB2 и MariaDB3 и разрешите его выполнение при запуске.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-232">Start MySQL on MariaDB2 and MariaDB3 and let it run at startup.</span></span>

        sudo service mysql start
        chkconfig mysql on

## <a name="load-balance-hello-cluster"></a><span data-ttu-id="cfdd8-233">Кластер hello балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="cfdd8-233">Load balance hello cluster</span></span>
<span data-ttu-id="cfdd8-234">При создании hello кластеризованных виртуальных машин, их добавления в группу доступности, называется tooensure clusteravset, что они были помещены в разных доменах сбоя и обновления и что Azure никогда не выполняет обслуживания на всех компьютерах за один раз.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-234">When you created hello clustered VMs, you added them into an availability set called clusteravset tooensure that they were put on different fault and update domains and that Azure never does maintenance on all machines at once.</span></span> <span data-ttu-id="cfdd8-235">Эта конфигурация требованиям hello toobe поддерживаемые hello соглашения об уровне обслуживания Azure (SLA).</span><span class="sxs-lookup"><span data-stu-id="cfdd8-235">This configuration meets hello requirements toobe supported by hello Azure service level agreement (SLA).</span></span>

<span data-ttu-id="cfdd8-236">Теперь с помощью подсистемы балансировки нагрузки Azure toobalance запросов между тремя узлами hello.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-236">Now use Azure Load Balancer toobalance requests between hello three nodes.</span></span>

<span data-ttu-id="cfdd8-237">Выполните следующие команды на компьютере с помощью Azure CLI hello hello.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-237">Run hello following commands on your machine by using hello Azure CLI.</span></span>

<span data-ttu-id="cfdd8-238">Структура параметров Hello команда выглядит так:`azure vm endpoint create-multiple <MachineName> <PublicPort>:<VMPort>:<Protocol>:<EnableDirectServerReturn>:<Load Balanced Set Name>:<ProbeProtocol>:<ProbePort>`</span><span class="sxs-lookup"><span data-stu-id="cfdd8-238">hello command parameters structure is: `azure vm endpoint create-multiple <MachineName> <PublicPort>:<VMPort>:<Protocol>:<EnableDirectServerReturn>:<Load Balanced Set Name>:<ProbeProtocol>:<ProbePort>`</span></span>

    azure vm endpoint create-multiple mariadb1 3306:3306:tcp:false:MySQL:tcp:3306
    azure vm endpoint create-multiple mariadb2 3306:3306:tcp:false:MySQL:tcp:3306
    azure vm endpoint create-multiple mariadb3 3306:3306:tcp:false:MySQL:tcp:3306

<span data-ttu-id="cfdd8-239">Hello CLI задает hello нагрузки балансировки выборки интервала too15 секундам, но может быть слишком длинный.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-239">hello CLI sets hello load balancer probe interval too15 seconds, which might be a bit too long.</span></span> <span data-ttu-id="cfdd8-240">Измените его на портале hello в **конечные точки** для всех виртуальных машин hello.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-240">Change it in hello portal under **Endpoints** for any of hello VMs.</span></span>

![Редактирование конечной точки](./media/mariadb-mysql-cluster/Endpoint.PNG)

<span data-ttu-id="cfdd8-242">Выберите **Load-Balanced задать hello Reconfigure**.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-242">Select **Reconfigure hello Load-Balanced Set**.</span></span>

![Перенастройте hello-набор с балансировкой нагрузки](./media/mariadb-mysql-cluster/Endpoint2.PNG)

<span data-ttu-id="cfdd8-244">Изменение **интервал выборки** too5 секунд и сохраните изменения.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-244">Change **Probe Interval** too5 seconds and save your changes.</span></span>

![Изменение интервала пробы](./media/mariadb-mysql-cluster/Endpoint3.PNG)

## <a name="validate-hello-cluster"></a><span data-ttu-id="cfdd8-246">Проверка кластера hello</span><span class="sxs-lookup"><span data-stu-id="cfdd8-246">Validate hello cluster</span></span>
<span data-ttu-id="cfdd8-247">выполняется непростая работа Hello.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-247">hello hard work is done.</span></span> <span data-ttu-id="cfdd8-248">Hello кластера должен быть теперь доступны в `mariadbha.cloudapp.net:3306`, которого достигает hello балансировки нагрузки и перенаправлять запросы между hello трех виртуальных машин и эффективность.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-248">hello cluster should be now accessible at `mariadbha.cloudapp.net:3306`, which hits hello load balancer and route requests between hello three VMs smoothly and efficiently.</span></span>

<span data-ttu-id="cfdd8-249">Использовать вашего любимого tooconnect клиента MySQL или подключение с одной из tooverify hello виртуальные машины, работа этого кластера.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-249">Use your favorite MySQL client tooconnect, or connect from one of hello VMs tooverify that this cluster is working.</span></span>

     mysql -u cluster -h mariadbha.cloudapp.net -p

<span data-ttu-id="cfdd8-250">Затем создайте базу данных и заполните ее данными.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-250">Then create a database and populate it with some data.</span></span>

    CREATE DATABASE TestDB;
    USE TestDB;
    CREATE TABLE TestTable (id INT NOT NULL AUTO_INCREMENT PRIMARY KEY, value VARCHAR(255));
    INSERT INTO TestTable (value)  VALUES ('Value1');
    INSERT INTO TestTable (value)  VALUES ('Value2');
    SELECT * FROM TestTable;

<span data-ttu-id="cfdd8-251">Hello база данных, созданная возвращает hello в следующей таблице:</span><span class="sxs-lookup"><span data-stu-id="cfdd8-251">hello database you created returns hello following table:</span></span>

    +----+--------+
    | id | value  |
    +----+--------+
    |  1 | Value1 |
    |  4 | Value2 |
    +----+--------+
    2 rows in set (0.00 sec)

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="cfdd8-252">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="cfdd8-252">Next steps</span></span>
<span data-ttu-id="cfdd8-253">В этой статье вы создали высокодоступный кластер MariaDB + Galera, состоящий из трех узлов, на виртуальных машинах Azure под управлением CentOS 7.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-253">In this article, you created a three-node MariaDB + Galera highly available cluster on Azure virtual machines running CentOS 7.</span></span> <span data-ttu-id="cfdd8-254">виртуальные машины Hello распределяются с подсистемой балансировки нагрузки Azure.</span><span class="sxs-lookup"><span data-stu-id="cfdd8-254">hello VMs are load balanced with Azure Load Balancer.</span></span>

<span data-ttu-id="cfdd8-255">Может потребоваться toolook на [toocluster другим способом MySQL в Linux](mysql-cluster.md) , а также способы слишком[оптимизировать и тестирование производительности MySQL на виртуальных машинах Azure Linux](optimize-mysql.md).</span><span class="sxs-lookup"><span data-stu-id="cfdd8-255">You might want toolook at [another way toocluster MySQL on Linux](mysql-cluster.md) and ways too[optimize and test MySQL performance on Azure Linux VMs](optimize-mysql.md).</span></span>

<!--Anchors-->
[Architecture overview]:#architecture-overview
[Creating hello template]:#creating-the-template
[Creating hello cluster]:#creating-the-cluster
[Load balancing hello cluster]:#load-balancing-the-cluster
[Validating hello cluster]:#validating-the-cluster
[Next steps]:#next-steps

<!--Image references-->

<!--Link references-->
[Galera]:http://galeracluster.com/products/
[MariaDBs]:https://mariadb.org/en/about/
[создайте ключ SSH для проверки подлинности]:http://www.jeff.wilcox.name/2013/06/secure-linux-vms-with-ssh-certificates/
[issue #1268 in hello Azure CLI]:https://github.com/Azure/azure-xplat-cli/issues/1268
