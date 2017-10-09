---
title: "aaaClusterize MySQL с балансировкой нагрузки наборами | Документы Microsoft"
description: "Настройка балансировки нагрузки, высокий уровень доступности, создать кластер Linux MySQL с hello классической модели развертывания в Azure"
services: virtual-machines-linux
documentationcenter: 
author: bureado
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 6c413a16-e9b5-4ffe-a8a3-ae67046bbdf3
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 04/14/2015
ms.author: jparrel
ms.openlocfilehash: 1829fd877c4b0ed177b23a8e3404dbb3db746561
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-load-balanced-sets-tooclusterize-mysql-on-linux"></a>Использование наборов с балансировкой нагрузки tooclusterize MySQL в Linux
> [!IMPORTANT]
> В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель Azure Resource Manager](../../../resource-manager-deployment-model.md) и классическая модель. В этой статье описан с помощью hello классической модели развертывания. Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов. Объект [шаблона диспетчера ресурсов](https://azure.microsoft.com/documentation/templates/mysql-replication/) доступен, если вам требуется toodeploy кластер MySQL.

В этой статье исследуются и иллюстрируется hello различные подходы доступных toodeploy высокой доступности на базе Linux службы в Microsoft Azure, изучение высокого уровня доступности сервера MySQL как учебник. Видеоролик, демонстрирующий этот подход, см. на [канале 9](http://channel9.msdn.com/Blogs/Open/Load-balancing-highly-available-Linux-services-on-Windows-Azure-OpenLDAP-and-MySQL).

Мы рассмотрим не использующее общие ресурсы высокодоступное решение MySQL с двумя узлами и одним владельцем на основе DRBD, Corosync и Pacemaker. Одновременно MySQL работает только в одном узле. Чтение и запись из hello ресурсов DRBD ограниченного tooonly узлом является один одновременно.

Нет необходимости для решения виртуальных IP-адресов, как LVS, так как вы воспользуетесь балансировкой нагрузки наборов в Microsoft Azure tooprovide циклического функциональные возможности и конечной точки обнаружения, удаления, мягкое восстановление hello виртуальных IP-адресов. Hello виртуальных IP-адресов является глобально маршрутизируемым IPv4-адрес, назначенный при создании hello облачной службы Microsoft Azure.

Существуют и другие доступные архитектуры для MySQL, в том числе NBD Cluster, Percona и Galera, а также несколько решений ПО промежуточного слоя, включая по крайней мере одно, доступное в качестве виртуальной машины на сайте [VM Depot](http://vmdepot.msopentech.com). При условии, что эти решения можно реплицировать на одноадресной и многоадресной или широковещательной рассылки и не используют общее хранилище или несколько сетевых интерфейсов, hello сценариев должно быть легко toodeploy в Microsoft Azure.

Эти кластеризации архитектуры можно расширить tooother продуктах, например PostgreSQL и OpenLDAP таким же образом. Например, данная процедура балансировки нагрузки без использования общих ресурсов была успешно протестирована с OpenLDAP с несколькими хозяевами, и это можно увидеть в нашем блоге "Канал 9".

## <a name="get-ready"></a>Подготовка
Требуются следующие hello ресурсов и возможности:

  - Microsoft Azure счета с действительной подпиской, будет toocreate по крайней мере две виртуальные машины (в этом примере использовался XS)
  - сеть и подсеть;
  - территориальная группа;
  - группа доступности;
  - Здравствуйте возможность toocreate виртуальные жесткие диски в hello же регионе, что облачная служба hello и присоединить их toohello виртуальных машин Linux

### <a name="tested-environment"></a>Тестовая среда
* Ubuntu 13.10
  * DRBD
  * MySQL Server
  * Corosync и Pacemaker

### <a name="affinity-group"></a>Территориальная группа
Создание территориальной группы для решения hello при входе в toohello классический портал Azure, при выборе **параметры**и создать группу сходства. Выделенные ресурсы, созданные в более поздней версии будут назначаться toothis территориальную группу.

### <a name="networks"></a>Сети
Создать новую сеть и подсеть создается внутри сети hello. В этом примере используется сеть 10.10.10.0/24 только с одной подсетью /24.

### <a name="virtual-machines"></a>Виртуальные машины
Hello первая виртуальная машина 13.10 Ubuntu создается с помощью образа коллекции Ubuntu Endorsed и называется `hadb01`. В процесс hello, называемый hadb создается новой облачной службы. Это имя показан общий доступ, hello характера балансировки нагрузки, которые hello службы будет отображаться, если добавляются дополнительные ресурсы. Здравствуйте, создание `hadb01` имеет процедура и заполняется с помощью портала hello. Конечной точки для SSH создается автоматически, и выбран hello новой сети. Теперь можно создать набор доступности для виртуальных машин hello.

После hello первая виртуальная машина создается (с технической точки зрения при создании hello облачной службы), создайте второй ВМ hello `hadb02`. Для hello второй виртуальной Машины, используйте Ubuntu 13.10 ВМ из hello коллекции с помощью портала hello, но использовать существующую облачную службу, `hadb.cloudapp.net`, вместо создания нового. Hello сети и доступность набор должен быть выбран автоматически. Также будет создана конечная точка SSH.

После создания обе виртуальные машины, возьмите на заметку hello портом SSH для `hadb01` (TCP-ПОРТ 22) и `hadb02` (автоматически назначаемый в Azure).

### <a name="attached-storage"></a>Подключаемое хранилище
Подключить новый диск-tooboth виртуальные машины и создавать диски размером 5 ГБ в процессе hello. диски Hello размещаются в контейнере VHD hello используется для дисков основной операционной системы. После создаются и присоединенные диски, происходит без необходимости toorestart Linux, поскольку hello новое устройство будет отображено hello ядра. Обычно это `/dev/sdc`. Проверьте `dmesg` для вывода hello.

На каждой виртуальной Машины, создать раздел с помощью `cfdisk` (основной, раздел Linux) и записи hello новой секции таблицы. Файловую систему в этом разделе создавать не нужно.

## <a name="set-up-hello-cluster"></a>Настройка кластера hello
Используйте APT tooinstall Corosync, Pacemaker и DRBD на обоих Ubuntu виртуальных машинах. toodo с `apt-get`, запустите hello следующий код:

    sudo apt-get install corosync pacemaker drbd8-utils.

Откажитесь от установки MySQL в это время. Debian и Ubuntu сценарии установки будет инициализировать каталог данных MySQL на `/var/lib/mysql`, но поскольку hello каталогов будет заменен DRBD файловой системы, вам потребуется позже tooinstall MySQL.

Проверка (с помощью `/sbin/ifconfig`), обе виртуальные машины используют адресов в подсети 10.10.10.0/24 hello и что они могут выполнить команду ping друг с другом по имени. Можно также использовать `ssh-keygen` и `ssh-copy-id` toomake убедиться, что обе виртуальные машины могут взаимодействовать по протоколу SSH не требуется пароль.

### <a name="set-up-drbd"></a>Настройка DRBD
Создать DRBD ресурс, который использует базовый hello `/dev/sdc1` секции tooproduce `/dev/drbd1` ресурс, который отформатирован с помощью ext3 и использовать в первичных и вторичных узлах.

1. Откройте `/etc/drbd.d/r0.res` и копирования hello после определения ресурса на обеих виртуальных машин:

        resource r0 {
          on `hadb01` {
            device  /dev/drbd1;
            disk   /dev/sdc1;
            address  10.10.10.4:7789;
            meta-disk internal;
          }
          on `hadb02` {
            device  /dev/drbd1;
            disk   /dev/sdc1;
            address  10.10.10.5:7789;
            meta-disk internal;
          }
        }

2. Инициализация hello ресурсов с помощью `drbdadm` на обеих виртуальных машинах:

        sudo drbdadm -c /etc/drbd.conf role r0
        sudo drbdadm up r0

3. На основной виртуальной Машины hello (`hadb01`), принудительно владения hello DRBD ресурс (первичный):

        sudo drbdadm primary --force r0

Если изучить содержимое hello/proc/drbd (`sudo cat /proc/drbd`) на обеих виртуальных машинах, вы должны увидеть `Primary/Secondary` на `hadb01` и `Secondary/Primary` на `hadb02`, согласованные с hello решения на этом этапе. диск размером 5 ГБ Hello синхронизируются по сети 10.10.10.0/24 hello в toocustomers не взимается.

По завершении синхронизации hello диск можно создать hello файловой системы на `hadb01`. В целях тестирования мы использовали ext2, но после кода hello создаст ext3 файловой системы:

    mkfs.ext3 /dev/drbd1

### <a name="mount-hello-drbd-resource"></a>Подключить ресурс DRBD hello
Вы теперь готовы toomount hello DRBD ресурсов на `hadb01`. В Debian и производных дистрибутивах в качестве каталога данных MySQL используется `/var/lib/mysql` . Поскольку вы не установили MySQL, создайте каталог hello и подключения hello DRBD ресурсов. tooperform этот параметр запуска hello, следующий код `hadb01`:

    sudo mkdir /var/lib/mysql
    sudo mount /dev/drbd1 /var/lib/mysql

## <a name="set-up-mysql"></a>Настройка MySQL
Теперь вы готовы tooinstall MySQL на `hadb01`:

    sudo apt-get install mysql-server

Для `hadb02`существует два варианта. Можно установить mysql server, чтобы создать /var/lib/mysql, заполнить его в новый каталог данных и затем удалить содержимое hello. tooperform этот параметр запуска hello, следующий код `hadb02`:

    sudo apt-get install mysql-server
    sudo service mysql stop
    sudo rm –rf /var/lib/mysql/*

второй вариант Hello — toofailover слишком`hadb02` , а затем установите mysql server существует. Сценарии установки заметить hello существующую установку и не трогайте его.

Выполнения hello следующий код на `hadb01`:

    sudo drbdadm secondary –force r0

Выполнения hello следующий код на `hadb02`:

    sudo drbdadm primary –force r0
    sudo apt-get install mysql-server

Если вы не собираетесь toofailover DRBD, несмотря на то что возможно менее элегантное проще hello первый параметр. После выполнения этой установки можно начинать работу с базой данных MySQL. Выполнения hello следующий код на `hadb02` (или любым из серверов hello активен, в соответствии с tooDRBD):

    mysql –u root –p
    CREATE DATABASE azureha;
    CREATE TABLE things ( id SERIAL, name VARCHAR(255) );
    INSERT INTO things VALUES (1, "Yet another entity");
    GRANT ALL ON things.\* tooroot;

> [!WARNING]
> Это последняя инструкция эффективно отключает проверку подлинности для пользователя root hello в этой таблице. Она включена только для иллюстрации, и в инструкциях GRANT для рабочей среды это необходимо изменить.

Если требуется toomake запросы из виртуальных машин с внешней hello (что hello цель данного руководства), необходимо также tooenable сети для MySQL. Откройте на обе виртуальные машины `/etc/mysql/my.cnf` и перейти слишком`bind-address`. Измените hello адрес 127.0.0.1 too0.0.0.0. После сохранения файла hello выдавать `sudo service mysql restart` на вашей текущей первичной реплике.

### <a name="create-hello-mysql-load-balanced-set"></a>Создать набор балансировки нагрузки hello MySQL
Вернитесь toohello портала, go слишком`hadb01`и выберите **конечные точки**. toocreate конечной точки, выберите MySQL (порт TCP 3306) из раскрывающегося списка hello и выберите **набор с балансировкой нагрузки новый создать**. Конечная точка с балансировкой нагрузки hello имя `lb-mysql`. Задать **время** too5 секунд минимальным.

После создания конечной точки hello go слишком`hadb02`, выберите **конечные точки**и создайте конечную точку. Выберите `lb-mysql`и выберите из раскрывающегося списка hello MySQL. На этом шаге можно также использовать hello Azure CLI.

Теперь у вас есть все необходимое для ручной работы кластера hello.

### <a name="test-hello-load-balanced-set"></a>Проверить набор балансировки нагрузки hello
Тестирование можно выполнять с внешнего компьютера с помощью клиента MySQL или с использованием приложений, например приложения phpMyAdmin, работающего в качестве веб-сайта Azure. В этом случае использовалась программа командной строки MySQL, запущенная на другом компьютере Linux.

    mysql azureha –u root –h hadb.cloudapp.net –e "select * from things;"

### <a name="manually-failing-over"></a>Переход на другой ресурс вручную
Вы можете смоделировать отработку отказа, завершив работу MySQL, переключившись на владельца DRBD и запустив MySQL снова.

tooperform этой задачи, запустите следующий код на hadb01 hello:

    service mysql stop && umount /var/lib/mysql ; drbdadm secondary r0

Затем на hadb02:

    drbdadm primary r0 ; mount /dev/drbd1 /var/lib/mysql && service mysql start

После выполнения перехода на другой ресурс вручную вы можете повторить удаленный запрос, и он должен работать без проблем.

## <a name="set-up-corosync"></a>Установка Corosync
Corosync — hello базового кластера инфраструктуры для Pacemaker toowork. Для пульса (и другие виды как Ultramonkey) Corosync является разбиение функциональные возможности CRM hello, оставив более похожими tooHeartbeat Pacemaker функциональные возможности.

основным ограничением Hello для Corosync в Azure является Corosync предпочитает многоадресную рассылку через вещания одноадресной рассылки связи, что сеть Microsoft Azure поддерживает только одноадресной рассылки.

К счастью, в Corosync имеется рабочий одноадресный режим. единственной реальной ограничение Hello —, так как все узлы не обмениваются данными друг с другом, необходимость toodefine hello узлы в файлах конфигурации, включая их IP-адреса. Hello Corosync примеры файлов можно использовать для одноадресной рассылки или изменение привязки, адреса, списки узлов и каталогах ведения журнала (использует Ubuntu `/var/log/corosync` хотя пример hello файлами `/var/log/cluster`) и включить средства кворума.

> [!NOTE]
> Используйте следующие hello `transport: udpu` директивы и hello определенные вручную IP-адреса для обоих узлов.

Выполнения hello следующий код в `/etc/corosync/corosync.conf` для обоих узлов:

    totem {
      version: 2
      crypto_cipher: none
      crypto_hash: none
      interface {
        ringnumber: 0
        bindnetaddr: 10.10.10.0
        mcastport: 5405
        ttl: 1
      }
      transport: udpu
    }

    logging {
      fileline: off
      to_logfile: yes
      to_syslog: yes
      logfile: /var/log/corosync/corosync.log
      debug: off
      timestamp: on
      logger_subsys {
        subsys: QUORUM
        debug: off
        }
      }

    nodelist {
      node {
        ring0_addr: 10.10.10.4
        nodeid: 1
      }

      node {
        ring0_addr: 10.10.10.5
        nodeid: 2
      }
    }

    quorum {
      provider: corosync_votequorum
    }

Скопируйте этот файл конфигурации на обе виртуальные машины и запустите Corosync в обоих узлах.

    sudo service start corosync

Вскоре после запуска службы hello, hello кластера следует установить в текущей кольцо hello и следует круглую кворума. Эту функцию можно проверить, просмотрев журналы или запустив hello, следующий код:

    sudo corosync-quorumtool –l

Вы увидите примерно toohello выходных данных после изображения.

![corosync-quorumtool -l sample output](./media/mysql-cluster/image001.png)

## <a name="set-up-pacemaker"></a>Установка Pacemaker
Использует pacemaker hello toomonitor кластера для ресурсов, определить, когда в источниках вышли из строя и переключение toosecondaries эти ресурсы. Ресурсы можно задавать с помощью ряда доступных скриптов или с помощью скриптов LSB (подобных init), а также другими способами.

Мы хотим Pacemaker ресурсов DRBD слишком «собственные» hello, точки подключения hello и службу MySQL hello. Если Pacemaker можно включать и отключать DRBD, подключения и отключить его и затем запускать и останавливать MySQL в hello правой порядок каких-либо неправильный происходит с hello первичных, Настройка завершена.

При первой установке Pacemaker конфигурация должна быть довольно простой, как показано ниже:

    node $id="1" hadb01
      attributes standby="off"
    node $id="2" hadb02
      attributes standby="off"

1. Проверьте конфигурацию hello, запустив `sudo crm configure show`.
2. Затем создайте файл (например `/tmp/cluster.conf`) с hello следующие ресурсы:

        primitive drbd_mysql ocf:linbit:drbd \
              params drbd_resource="r0" \
              op monitor interval="29s" role="Master" \
              op monitor interval="31s" role="Slave"

        ms ms_drbd_mysql drbd_mysql \
              meta master-max="1" master-node-max="1" \
                clone-max="2" clone-node-max="1" \
                notify="true"

        primitive fs_mysql ocf:heartbeat:Filesystem \
              params device="/dev/drbd/by-res/r0" \
              directory="/var/lib/mysql" fstype="ext3"

        primitive mysqld lsb:mysql

        group mysql fs_mysql mysqld

        colocation mysql_on_drbd \
               inf: mysql ms_drbd_mysql:Master

        order mysql_after_drbd \
               inf: ms_drbd_mysql:promote mysql:start

        property stonith-enabled=false

        property no-quorum-policy=ignore

3. Загрузите hello в конфигурации hello. Требуется только toodo это в один узел.

        sudo crm configure
          load update /tmp/cluster.conf
          commit
          exit

4. Убедитесь, что Pacemaker запускается при загрузке в обоих узлах.

        sudo update-rc.d pacemaker defaults

5. С помощью `sudo crm_mon –L`, убедитесь, что один из узлов становится master hello для кластера hello и управлением ресурсами hello. Можно использовать подключения и ps toocheck работающие ресурсы hello.

Привет, следуя снимке экрана показано `crm_mon` с одним узлом остановлена (выход, нажав сочетание клавиш Ctrl + C):

![crm_mon node stopped](./media/mysql-cluster/image002.png)

На следующем снимке экрана показаны оба узла, один из которых главный, а второй подчиненный.

![crm_mon operational master/slave](./media/mysql-cluster/image003.png)

## <a name="testing"></a>Тестирование
Теперь все готово для моделирования автоматической отработки отказа. Существует два способа toodo это: мягких и жестких.

Hello мягкий способ использует функции завершения работы кластера hello: ``crm_standby -U `uname -n` -v on``. Если вы используете образец hello, переходит ведомый hello. Помните, tooset этот toooff назад. Если вы этого не сделаете, crm_mon будет сообщать, что один из узлов находится в резервном режиме.

Hello трудным способом завершает работу hello основной ВМ (hadb01) через портал hello или изменяя hello runlevel на hello виртуальной Машины (то есть, остановка, завершение работы). Это помогает Corosync и Pacemaker путем передачи сигналов, образец hello переход вниз. Это можно проверить (полезно для окна обслуживания), но можно также принудительно сценарий hello, закрепление hello виртуальной Машины.

## <a name="stonith"></a>STONITH
Оно должно быть возможно tooissue завершение работы виртуальной Машины через hello Azure CLI вместо STONITH скрипт, который управляет физического устройства. Можно использовать `/usr/lib/stonith/plugins/external/ssh` как базового и включить STONITH в конфигурации кластера hello. Azure CLI глобально должны быть установлены и параметры публикации hello и загружать профиль пользователя hello кластера.

Образцы кода для hello ресурс доступен на [GitHub](https://github.com/bureado/aztonith). Изменения конфигурации кластера hello, добавив hello слишком следующие`sudo crm configure`:

    primitive st-azure stonith:external/azure \
      params hostlist="hadb01 hadb02" \
      clone fencing st-azure \
      property stonith-enabled=true \
      commit

> [!NOTE]
> сценарий Hello не выполняет проверок вверх или вниз. Исходный ресурс SSH Hello присутствовал 15 проверки ping, однако время восстановления для виртуальной Машины Azure может быть несколько переменной.

## <a name="limitations"></a>Ограничения
применяются следующие ограничения Hello.

* Здравствуйте, linbit DRBD ресурсов скрипт, который управляет DRBD как ресурс в Pacemaker использует `drbdadm down` при выключении узел, даже если просто hello узел в режим ожидания. Это не идеальное решение, поскольку ведомый hello не синхронизироваться будут hello DRBD ресурсов во время записи возвращает образец hello. Образец hello не позволяет любезно, ведомый hello может взять на себя более старые состояния файловой системы. Имеется два способа разрешения этой проблемы:
  * принудительное выполнение `drbdadm up r0` во всех узлах кластера с помощью локальной (не кластерной) программы наблюдения watchdog;
  * Изменение сценария DRBD linbit hello, убедившись, что `down` не вызывается в`/usr/lib/ocf/resource.d/linbit/drbd`
* Подсистема балансировки нагрузки Hello требуется toorespond по крайней мере пять секунд, приложения должны быть кластеры и должны быть более нечувствительного к ошибкам времени ожидания. Другие архитектуры, например очереди в приложении и ПО промежуточного слоя запроса, также могут быть полезными.
* MySQL тонкая настройка — необходимые tooensure, запись осуществляется в управляемую темпе и кэшей будут сброшены toodisk так же часто, как потеря возможных toominimize памяти.
* Запись в виртуальной Машине зависит производительность соединений hello виртуального коммутатора, поскольку это hello механизм, используемый устройством hello DRBD tooreplicate.
