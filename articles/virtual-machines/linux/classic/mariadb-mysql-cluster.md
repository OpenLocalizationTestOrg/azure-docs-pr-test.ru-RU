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
# <a name="mariadb-mysql-cluster-azure-tutorial"></a>Кластер MariaDB (MySQL) — руководство по Azure
> [!IMPORTANT]
> В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель Azure Resource Manager](../../../resource-manager-deployment-model.md) и классическая модель. В этой статье рассматриваются hello классической модели развертывания. Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов Azure.

> [!NOTE]
> Кластер выпуска MariaDB Enterprise теперь доступен в hello Azure Marketplace. Hello новое предложение будет автоматически развернуть кластер MariaDB Galera от диспетчера ресурсов Azure. Следует использовать новое предложение hello из [Azure Marketplace](https://azure.microsoft.com/en-us/marketplace/partners/mariadb/cluster-maxscale/).
>
>

В этой статье показано, как toocreate несколькими Master [Galera](http://galeracluster.com/products/) кластер [MariaDBs](https://mariadb.org/en/about/) (сборка надежные, масштабируемые и надежные замена MySQL) toowork в среде высокой доступности в Azure виртуальные машины.

## <a name="architecture-overview"></a>Общие сведения об архитектуре
В этой статье описывается как hello toocomplete следующие шаги:

- Создать кластер с тремя узлами.
- Отдельные hello дисков данных с диска ОС hello.
- Создание дисков данных hello в RAID 0 или чередованием параметр tooincrease операций ввода-ВЫВОДА.
- Используйте нагрузки hello toobalance подсистемы балансировки нагрузки Azure для hello трех узлов.
- повторяющиеся toominimize, создание образа виртуальной Машины, который содержит MariaDB + Galera, необходимо использовать toocreate hello других ВМ кластера.

![Архитектура системы](./media/mariadb-mysql-cluster/Setup.png)

> [!NOTE]
> В этом разделе используется hello [Azure CLI](../../../cli-install-nodejs.md) средства, поэтому следует убедиться, что toodownload их и подключите их соответствующим инструкциям toohello tooyour подписки Azure. Ссылка toohello команд, доступных в hello Azure CLI, в статье hello [Справочник по командам Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2). Необходимо также слишком[создайте ключ SSH для проверки подлинности] и запишите расположение файла .pem hello.
>
>

## <a name="create-hello-template"></a>Создание шаблона hello
### <a name="infrastructure"></a>Инфраструктура
1. Создайте территориальную группу toohold hello ресурсы друг с другом.

        azure account affinity-group create mariadbcluster --location "North Europe" --label "MariaDB Cluster"
2. Создайте виртуальную сеть.

        azure network vnet create --address-space 10.0.0.0 --cidr 8 --subnet-name mariadb --subnet-start-ip 10.0.0.0 --subnet-cidr 24 --affinity-group mariadbcluster mariadbvnet
3. Создание учетной записи хранилища toohost все диски. Более 40 интенсивно используемых дисков не следует разместить на hello же tooavoid учетной записи хранилища, попадание учетной записи hello 20 000 операций ввода-ВЫВОДА хранилища. В этом случае вы гораздо ниже этого предела, поэтому все данные будут храниться на учетную запись для простоты hello.

        azure storage account create mariadbstorage --label mariadbstorage --affinity-group mariadbcluster
4. Найти имя образа виртуальной машины CentOS 7 hello hello.

        azure vm image list | findstr CentOS
   Hello вывода будет примерно `5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20140926`.

   Используйте это имя в даст hello.
5. Создание шаблона виртуальной Машины hello и замените /path/to/key.pem hello путь хранения hello созданный .pem SSH-ключ.

        azure vm create --virtual-network-name mariadbvnet --subnet-names mariadb --blob-url "http://mariadbstorage.blob.core.windows.net/vhds/mariadbhatemplate-os.vhd"  --vm-size Medium --ssh 22 --ssh-cert "/path/to/key.pem" --no-ssh-password mariadbtemplate 5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20140926 azureuser
6. Присоединение дисков toohello четыре 500 ГБ данных виртуальной Машины для использования в конфигурации RAID hello.

        FOR /L %d IN (1,1,4) DO azure vm disk attach-new mariadbhatemplate 512 http://mariadbstorage.blob.core.windows.net/vhds/mariadbhatemplate-data-%d.vhd
7. Использовать SSH toosign в toohello шаблона виртуальной Машины, созданной в mariadbhatemplate.cloudapp.net:22 и подключитесь с помощью закрытого ключа.

### <a name="software"></a>Программное обеспечение
1. Получите корень hello.

        sudo su

2. Установка поддержки RAID:

    а. Установите mdadm.

              yum install mdadm

    b. Создайте конфигурацию RAID0/stripe hello EXT4 файловой системе.

              mdadm --create --verbose /dev/md0 --level=stripe --raid-devices=4 /dev/sdc /dev/sdd /dev/sde /dev/sdf
              mdadm --detail --scan >> /etc/mdadm.conf
              mkfs -t ext4 /dev/md0
    c. Создайте каталог точки подключения hello.

              mkdir /mnt/data
    d. Получить hello UUID hello вновь созданные устройства RAID.

              blkid | grep /dev/md0
    д. Измените файл /etc/fstab.

              vi /etc/fstab
    f. Добавить hello устройства tooenable автоматическое подключение при перезагрузке, заменив значение hello hello UUID, полученный от предыдущего hello **блок идентификатором blkid** команды.

              UUID=<UUID FROM PREVIOUS>   /mnt/data ext4   defaults,noatime   1 2
    ж. Подключите новый раздел hello.

              mount /mnt/data

3. Установите MariaDB.

    а. Создайте файл MariaDB.repo hello.

                vi /etc/yum.repos.d/MariaDB.repo

    b. Заполните hello после содержимого файла hello репозитория:

              [mariadb]
              name = MariaDB
              baseurl = http://yum.mariadb.org/10.0/centos7-amd64
              gpgkey=https://yum.mariadb.org/RPM-GPG-KEY-MariaDB
              gpgcheck=1
    c. конфликты tooavoid удалите существующие постфиксная и mariadb библиотеки.

           yum remove postfix mariadb-libs-*
    d. Установите MariaDB с Galera.

           yum install MariaDB-Galera-server MariaDB-client galera

4. Переместите hello каталог данных MySQL toohello устройство блока RAID.

    а. Скопируйте текущий каталог MySQL hello в новое место и удалите прежний каталог hello.

           cp -avr /var/lib/mysql /mnt/data  
           rm -rf /var/lib/mysql
    b. Установите разрешения для нового каталога hello соответствующим образом.

           chown -R mysql:mysql /mnt/data && chmod -R 755 /mnt/data/

    c. Создайте символьную ссылку, указывающий hello старого каталога toohello новое расположение на hello RAID-массива.

           ln -s /mnt/data/mysql /var/lib/mysql

5. Так как [SELinux мешает операций кластера hello](http://galeracluster.com/documentation-webpages/configuration.html#selinux), это toodisable необходимые им для hello текущего сеанса. Изменить `/etc/selinux/config` toodisable его для последующей перезагрузки.

            setenforce 0

            then editing `/etc/selinux/config` tooset `SELINUX=permissive`
6. Убедитесь, что MySQL работает.

   а. Запустите MySQL.

           service mysql start
   b. Secure установки MySQL hello, задать пароль учетной записи root hello, удалить имя входа удаленного корневого элемента toodisable анонимных пользователей и удалить hello тестовую базу данных.

           mysql_secure_installation
   c. Создание пользователя в базе данных hello для операции кластера и при необходимости для приложений.

           mysql -u root -p
           GRANT ALL PRIVILEGES ON *.* too'cluster'@'%' IDENTIFIED BY 'p@ssw0rd' WITH GRANT OPTION; FLUSH PRIVILEGES;
           exit

   d. Остановите работу MySQL.

            service mysql stop
7. Создайте заполнитель конфигурации.

   а. Измените toocreate конфигурации MySQL hello заполнитель для настройки кластера hello. Не заменяйте hello  **`<Variables>`**  или раскомментируйте теперь. Это произойдет после создания виртуальной машины из этого шаблона.

            vi /etc/my.cnf.d/server.cnf
   b. Изменить hello  **[galera]**  статьи и ее необходимо очистить.

   c. Изменить hello **[mariadb]** раздела.

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
8. Необходимые порты в брандмауэре hello откройте с помощью FirewallD на CentOS 7.

   * MySQL: `firewall-cmd --zone=public --add-port=3306/tcp --permanent`
   * GALERA: `firewall-cmd --zone=public --add-port=4567/tcp --permanent`
   * GALERA IST: `firewall-cmd --zone=public --add-port=4568/tcp --permanent`
   * RSYNC: `firewall-cmd --zone=public --add-port=4444/tcp --permanent`
   * Перезагрузите hello брандмауэра:`firewall-cmd --reload`

9. Оптимизация производительности системы hello. Дополнительные сведения см. в статье [Оптимизация производительности MySQL в виртуальных машинах Azure Linux](optimize-mysql.md).

   а. Изменение файла конфигурации MySQL hello еще раз.

            vi /etc/my.cnf.d/server.cnf
   b. Изменить hello **[mariadb]** статьи и добавления hello после содержимого:

   > [!NOTE]
   > Рекомендуемое значение innodb\_buffer\_pool_size составляет 70 % от памяти виртуальной машины. В этом примере он был задан 2,45 ГБ для средних hello Azure VM with 3,5 ГБ ОЗУ.
   >
   >

           innodb_buffer_pool_size = 2508M # hello buffer pool contains buffered data and hello index. This is usually set too70 percent of physical memory.
           innodb_log_file_size = 512M #  Redo logs ensure that write operations are fast, reliable, and recoverable after a crash
           max_connections = 5000 # A larger value will give hello server more time toorecycle idled connections
           innodb_file_per_table = 1 # Speed up hello table space transmission and optimize hello debris management performance
           innodb_log_buffer_size = 128M # hello log buffer allows transactions toorun without having tooflush hello log toodisk before hello transactions commit
           innodb_flush_log_at_trx_commit = 2 # hello setting of 2 enables hello most data integrity and is suitable for Master in MySQL cluster
           query_cache_size = 0
10. Остановить MySQL, отключить службу MySQL по tooavoid запуска, приостановки hello кластера при добавлении узла и отменить подготовку компьютера hello.

        service mysql stop
        chkconfig mysql off
        waagent -deprovision
11. Запишите hello виртуальной Машины через портал hello. (В настоящее время [выдавать &#1268; в средствах Azure CLI hello](https://github.com/Azure/azure-xplat-cli/issues/1268) описывает hello факт, что образы, созданные средствами hello Azure CLI не выполняется сбор hello присоединенные диски данных.)

    а. Завершите работу hello машины через портал hello.

    b. Нажмите кнопку **захвата** и укажите имя образа hello как **mariadb galera изображениями**. Введите описание и установите флажок "команда waagent -deprovision запущена на виртуальной машине".
      
      ![Запись hello виртуальной машины](./media/mariadb-mysql-cluster/Capture2.PNG)

## <a name="create-hello-cluster"></a>Создание кластера hello
Создайте три виртуальные машины с hello шаблон создан и затем выполняется настройка и запуск hello кластера.

1. Создайте hello первой виртуальной Машины CentOS 7 из hello mariadb-galera образа образ был создан, предоставляя hello следующую информацию:

 - Имя виртуальной сети: mariadbvnet.
 - Подсеть: mariadb.
 - Размер машины: средний.
 - Имя облачной службы: mariadbha (или любое имя по требуется доступ через mariadbha.cloudapp.net toobe)
 - Имя машины: mariadb1.
 - Имя пользователя: azureuser.
 - SSH-доступ: включен.
 - Передача PEM-файл сертификата SSH hello и замены /path/to/key.pem hello путь, где хранится hello создан .pem SSH-ключ.

   > [!NOTE]
   > Hello следующие команды разбиваются на несколько строк для ясности, но сначала следует вводить как одну строку.
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
2. Создайте дополнительные виртуальные машины, подключив их toohello mariadbha облачной службы. Здравствуйте, изменить имя виртуальной Машины hello и hello порт tooa уникальный порт SSH не конфликтует с других виртуальных машин в одной облачной службе.

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
  Для MariaDB3:

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
3. Вам потребуется tooget hello внутренний IP-адрес каждого hello трех виртуальных машин для hello следующий шаг:

    ![Получение IP-адреса](./media/mariadb-mysql-cluster/IP.png)
4. Используйте SSH toosign в toohello три виртуальные машины и изменить файл конфигурации hello в каждой из них.

        sudo vi /etc/my.cnf.d/server.cnf

    Раскомментируйте  **`wsrep_cluster_name`**  и  **`wsrep_cluster_address`**  , удалив hello  **#**  в начале строки hello hello.
    Кроме того, замените  **`<ServerIP>`**  в  **`wsrep_node_address`**  и  **`<NodeName>`**  в  **`wsrep_node_name`**  с hello Виртуальной машины IP адрес и имя, соответственно, раскомментируйте эти строки также.
5. Запустите кластер hello на MariaDB1 и дать ему возможность работать во время запуска.

        sudo service mysql bootstrap
        chkconfig mysql on
6. Запустите MySQL в MariaDB2 и MariaDB3 и разрешите его выполнение при запуске.

        sudo service mysql start
        chkconfig mysql on

## <a name="load-balance-hello-cluster"></a>Кластер hello балансировки нагрузки
При создании hello кластеризованных виртуальных машин, их добавления в группу доступности, называется tooensure clusteravset, что они были помещены в разных доменах сбоя и обновления и что Azure никогда не выполняет обслуживания на всех компьютерах за один раз. Эта конфигурация требованиям hello toobe поддерживаемые hello соглашения об уровне обслуживания Azure (SLA).

Теперь с помощью подсистемы балансировки нагрузки Azure toobalance запросов между тремя узлами hello.

Выполните следующие команды на компьютере с помощью Azure CLI hello hello.

Структура параметров Hello команда выглядит так:`azure vm endpoint create-multiple <MachineName> <PublicPort>:<VMPort>:<Protocol>:<EnableDirectServerReturn>:<Load Balanced Set Name>:<ProbeProtocol>:<ProbePort>`

    azure vm endpoint create-multiple mariadb1 3306:3306:tcp:false:MySQL:tcp:3306
    azure vm endpoint create-multiple mariadb2 3306:3306:tcp:false:MySQL:tcp:3306
    azure vm endpoint create-multiple mariadb3 3306:3306:tcp:false:MySQL:tcp:3306

Hello CLI задает hello нагрузки балансировки выборки интервала too15 секундам, но может быть слишком длинный. Измените его на портале hello в **конечные точки** для всех виртуальных машин hello.

![Редактирование конечной точки](./media/mariadb-mysql-cluster/Endpoint.PNG)

Выберите **Load-Balanced задать hello Reconfigure**.

![Перенастройте hello-набор с балансировкой нагрузки](./media/mariadb-mysql-cluster/Endpoint2.PNG)

Изменение **интервал выборки** too5 секунд и сохраните изменения.

![Изменение интервала пробы](./media/mariadb-mysql-cluster/Endpoint3.PNG)

## <a name="validate-hello-cluster"></a>Проверка кластера hello
выполняется непростая работа Hello. Hello кластера должен быть теперь доступны в `mariadbha.cloudapp.net:3306`, которого достигает hello балансировки нагрузки и перенаправлять запросы между hello трех виртуальных машин и эффективность.

Использовать вашего любимого tooconnect клиента MySQL или подключение с одной из tooverify hello виртуальные машины, работа этого кластера.

     mysql -u cluster -h mariadbha.cloudapp.net -p

Затем создайте базу данных и заполните ее данными.

    CREATE DATABASE TestDB;
    USE TestDB;
    CREATE TABLE TestTable (id INT NOT NULL AUTO_INCREMENT PRIMARY KEY, value VARCHAR(255));
    INSERT INTO TestTable (value)  VALUES ('Value1');
    INSERT INTO TestTable (value)  VALUES ('Value2');
    SELECT * FROM TestTable;

Hello база данных, созданная возвращает hello в следующей таблице:

    +----+--------+
    | id | value  |
    +----+--------+
    |  1 | Value1 |
    |  4 | Value2 |
    +----+--------+
    2 rows in set (0.00 sec)

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Дальнейшие действия
В этой статье вы создали высокодоступный кластер MariaDB + Galera, состоящий из трех узлов, на виртуальных машинах Azure под управлением CentOS 7. виртуальные машины Hello распределяются с подсистемой балансировки нагрузки Azure.

Может потребоваться toolook на [toocluster другим способом MySQL в Linux](mysql-cluster.md) , а также способы слишком[оптимизировать и тестирование производительности MySQL на виртуальных машинах Azure Linux](optimize-mysql.md).

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
