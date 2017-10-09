---
title: "высокий уровень доступности виртуальных машин для SAP NetWeaver в SUSE Linux Enterprise Server для приложений SAP aaaAzure | Документы Microsoft"
description: "Руководство по обеспечению высокой доступности для SAP NetWeaver на SUSE Linux Enterprise Server для приложений SAP"
services: virtual-machines-windows,virtual-network,storage
documentationcenter: saponazure
author: mssedusch
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 5e514964-c907-4324-b659-16dd825f6f87
ms.service: virtual-machines-windows
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 04/27/2017
ms.author: sedusch
ms.openlocfilehash: e944103df92d5ffec9196189f138e25972bea79f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="high-availability-for-sap-netweaver-on-azure-vms-on-suse-linux-enterprise-server-for-sap-applications"></a>Руководство по обеспечению высокого уровня доступности виртуальных машин Azure для SAP NetWeaver на SUSE Linux Enterprise Server для приложений SAP

[dbms-guide]:dbms-guide.md
[deployment-guide]:deployment-guide.md
[planning-guide]:planning-guide.md

[2205917]:https://launchpad.support.sap.com/#/notes/2205917
[1944799]:https://launchpad.support.sap.com/#/notes/1944799
[1928533]:https://launchpad.support.sap.com/#/notes/1928533
[2015553]:https://launchpad.support.sap.com/#/notes/2015553
[2178632]:https://launchpad.support.sap.com/#/notes/2178632
[2191498]:https://launchpad.support.sap.com/#/notes/2191498
[2243692]:https://launchpad.support.sap.com/#/notes/2243692
[1984787]:https://launchpad.support.sap.com/#/notes/1984787
[1999351]:https://launchpad.support.sap.com/#/notes/1999351
[1410736]:https://launchpad.support.sap.com/#/notes/1410736

[sap-swcenter]:https://support.sap.com/en/my-support/software-downloads.html

[suse-hana-ha-guide]:https://www.suse.com/docrep/documents/ir8w88iwu7/suse_linux_enterprise_server_for_sap_applications_12_sp1.pdf
[suse-drbd-guide]:https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha_techguides/book_sleha_techguides.html

[template-multisid-xscs]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-xscs-md%2Fazuredeploy.json
[template-converged]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-converged-md%2Fazuredeploy.json
[template-file-server]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-file-server-md%2Fazuredeploy.json

[sap-hana-ha]:sap-hana-high-availability.md

В этой статье описывается toodeploy hello виртуальных машин, Настройка hello виртуальных машин, установите framework кластера hello и установка высокой доступности системы SAP NetWeaver 7,50.
В конфигурациях hello пример команды для установки и т. д. используется экземпляр ASCS номер 00, экземпляр ERS номер 02 и идентификатор системы SAP NWS. Hello имена hello ресурсов (например, виртуальных машин, виртуальных сетей), в примере hello предполагается, что используется hello [схождение выполнено шаблона] [ template-converged] с ресурсы hello toocreate NWS идентификатор системы SAP.

Следующие примечания по SAP и документы сначала hello чтения

* примечание к SAP [1928533], которое содержит:
  * Список размеров виртуальных Машин Azure, которые поддерживаются для развертывания по SAP hello
  * важные сведения о доступных ресурсах для каждого размера виртуальной машины Azure;
  * сведения о поддерживаемом программном обеспечении SAP и сочетаниях операционных систем и баз данных;
  * сведения о требуемой версии ядра SAP для Windows и Linux в Microsoft Azure.

* примечание к SAP [2015553], в котором описываются предварительные требования к SAP при развертывании программного обеспечения SAP в Azure;
* Примечание SAP [2205917] содержит рекомендуемые параметры ОС для SUSE Linux Enterprise Server для приложений SAP.
* Примечание SAP [1944799] содержит рекомендации для SAP HANA в SUSE Linux Enterprise Server для приложений SAP.
* примечание к SAP [2178632], содержащее подробные сведения обо всех доступных метриках мониторинга для SAP в Azure;
* Примечание SAP [2191498] имеет hello требуемая версия агента узла SAP для Linux в Azure.
* примечание к SAP [2243692], содержащее сведения о лицензировании SAP в Linux в Azure;
* примечание к SAP [1984787], содержащее общие сведения о SUSE Linux Enterprise Server 12;
* Примечание SAP [1999351] имеет дополнительные диагностические сведения для hello расширение мониторинга Azure для SAP.
* [вики-сайт сообщества SAP](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes), содержащий все необходимые примечания к SAP для Linux;
* [SAP NetWeaver на виртуальных машинах Windows. Руководство по планированию и внедрению][planning-guide]
* [Развертывание программного обеспечения SAP на виртуальных машинах Linux в Azure (эта статья)][deployment-guide]
* [SAP NetWeaver на виртуальных машинах Windows. Руководство по развертыванию СУБД][dbms-guide]
* [Сценарий оптимизации производительности системной репликации SAP HANA][suse-hana-ha-guide]:  
  Справочник по Hello содержит все необходимые сведения tooset копирование репликации системы SAP HANA в локальной среде. Используйте это руководство как основу.
* [Высокой доступные хранилища NFS с DRBD и Pacemaker] [ suse-drbd-guide] hello руководство содержит все необходимые сведения tooset высокой доступности сервер NFS. Используйте это руководство как основу.


## <a name="overview"></a>Обзор

tooachieve высокого уровня доступности и SAP NetWeaver требует NFS-сервера. Hello NFS-сервер настраивается в отдельный кластер и может использоваться несколькими системами SAP.

![Общие сведения о высоком уровне доступности SAP NetWeaver](./media/high-availability-guide-suse/img_001.png)

Hello NFS-сервера, SAP NetWeaver ASCS, SAP NetWeaver SCS, ющих Методов SAP NetWeaver и база данных SAP HANA hello с помощью виртуального имени узла и виртуальных IP-адресов. В Azure подсистемы балансировки нагрузки является обязательным toouse виртуальный IP-адрес. Hello ниже перечислены hello конфигурации подсистемы балансировки нагрузки hello.

### <a name="nfs-server"></a>Сервер NFS
* Конфигурация внешнего интерфейса:
  * IP-адрес 10.0.0.4.
* Конфигурация серверной части:
  * Подключенных сетевых интерфейсах tooprimary всех виртуальных машин, которые должны быть частью кластера NFS hello
* Порт пробы:
  * порт 61000.
* Правила балансировки нагрузки:
  * 2049 TCP; 
  * 2049 UDP.

### <a name="ascs"></a>(A)SCS
* Конфигурация внешнего интерфейса:
  * IP-адрес 10.0.0.10.
* Конфигурация серверной части:
  * Сетевые интерфейсы подключенных tooprimary всех виртуальных машин, которые должны быть частью кластера hello (A) SCS/ющих Методов
* Порт пробы:
  * порт 620**&lt;nr&gt;**.
* Правила балансировки нагрузки:
  * 32**&lt;nr&gt;** TCP;
  * 36**&lt;nr&gt;** TCP;
  * 39**&lt;nr&gt;** TCP;
  * 81**&lt;nr&gt;** TCP;
  * 5**&lt;nr&gt;**13 TCP;
  * 5**&lt;nr&gt;**14 TCP;
  * 5**&lt;nr&gt;**16 TCP.

### <a name="ers"></a>ERS
* Конфигурация внешнего интерфейса:
  * IP-адрес 10.0.0.11.
* Конфигурация серверной части:
  * Сетевые интерфейсы подключенных tooprimary всех виртуальных машин, которые должны быть частью кластера hello (A) SCS/ющих Методов
* Порт пробы:
  * Порт 621**&lt;nr&gt;**.
* Правила балансировки нагрузки:
  * 33**&lt;nr&gt;** TCP;
  * 5**&lt;nr&gt;**13 TCP;
  * 5**&lt;nr&gt;**14 TCP;
  * 5**&lt;nr&gt;**16 TCP.

### <a name="sap-hana"></a>SAP HANA
* Конфигурация внешнего интерфейса:
  * IP-адрес 10.0.0.12.
* Конфигурация серверной части:
  * Подключенных сетевых интерфейсах tooprimary всех виртуальных машин, которые должны быть частью кластера HANA hello
* Порт пробы:
  * порт 625**&lt;nr&gt;**.
* Правила балансировки нагрузки:
  * 3**&lt;nr&gt;**15 TCP;
  * 3**&lt;nr&gt;**17 TCP.

## <a name="setting-up-a-highly-available-nfs-server"></a>Настройка сервера NFS высокой доступности

### <a name="deploying-linux"></a>Развертывание Linux

Hello Azure Marketplace содержит изображение для SUSE Linux Enterprise Server 12 приложений SAP, которые используются toodeploy новых виртуальных машин.
Можно использовать один из шаблонов hello быстрого запуска на github toodeploy все необходимые ресурсы. шаблон Hello развертывает hello виртуальных машин, подсистемы балансировки нагрузки hello, доступности, и т. д. Выполните эти шаги toodeploy hello шаблона.

1. Откройте hello [шаблона сервера SAP файл] [ template-file-server] в hello портал Azure   
1. Введите следующие параметры hello
   1. Префикс ресурса  
      Введите префикс hello требуется toouse. Hello значение используется как префикс для hello ресурсы, которые развертываются.
   2. Тип ОС  
      Выберите один из hello ОС Linux. Для этого примера выберите SLES 12.
   3. Имя пользователя и пароль администратора  
      Создать нового пользователя, можно использовать toolog на компьютере toohello.
   4. Идентификатор подсети  
      Идентификатор Hello hello подсети toowhich hello виртуальных машин должен быть подключен к. Оставьте пустым, если требуется toocreate новую виртуальную сеть или выберите подсеть hello VPN или Express Route виртуальной сети tooconnect hello виртуальной машины tooyour в локальной сети. Идентификатор Hello обычно выглядит /subscriptions/**&lt;код_подписки&gt;**/resourceGroups/**&lt;имя группы ресурсов&gt;**/providers/ Microsoft.Network/virtualNetworks/**&lt;имя виртуальной сети&gt;**/subnets/**&lt;имя подсети&gt;**

### <a name="installation"></a>Установка

Hello следующие элементы имеют префикс либо **[A]** -узлы применимо tooall **[1]** -только применимые toonode 1 или **[2]** -только применимые toonode 2.

1. **[A]** Обновите SLES.

   <pre><code>
   sudo zypper update
   </code></pre>

1. **[1]** Включите доступ по протоколу SSH.

   <pre><code>
   sudo ssh-keygen -tdsa
   
   # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
   # Enter passphrase (empty for no passphrase): -> ENTER
   # Enter same passphrase again: -> ENTER
   
   # copy hello public key
   sudo cat /root/.ssh/id_dsa.pub
   </code></pre>

2. **[2]** Включите доступ по протоколу SSH.

   <pre><code>
   sudo ssh-keygen -tdsa

   # insert hello public key you copied in hello last step into hello authorized keys file on hello second server
   sudo vi /root/.ssh/authorized_keys
   
   # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
   # Enter passphrase (empty for no passphrase): -> ENTER
   # Enter same passphrase again: -> ENTER
   
   # copy hello public key   
   sudo cat /root/.ssh/id_dsa.pub
   </code></pre>

1. **[1]** Включите доступ по протоколу SSH.

   <pre><code>
   # insert hello public key you copied in hello last step into hello authorized keys file on hello first server
   sudo vi /root/.ssh/authorized_keys
   </code></pre>

1. **[A]** Установите расширение для обеспечения высокого уровня доступности.
   
   <pre><code>
   sudo zypper install sle-ha-release fence-agents
   </code></pre>

1. **[A]** Установите разрешения имен.   

   Можно использовать DNS-сервер или измените hello/etc/hosts, на всех узлах. В этом примере показано, как toouse hello файл/etc/hosts.
   Замените hello IP-адрес и имя узла hello в hello, следующие команды

   <pre><code>
   sudo vi /etc/hosts
   </code></pre>
   
   Вставьте следующие строки слишком/и т. д/узлы hello. Изменение среды toomatch hello IP адрес и имя узла   
   
   <pre><code>
   # IP address of hello load balancer frontend configuration for NFS
   <b>10.0.0.4 nws-nfs</b>
   </code></pre>

1. **[1]** Установите кластер.
   
   <pre><code>
   sudo ha-cluster-init
   
   # Do you want toocontinue anyway? [y/N] -> y
   # Network address toobind too(for example: 192.168.1.0) [10.79.227.0] -> ENTER
   # Multicast address (for example: 239.x.x.x) [239.174.218.125] -> ENTER
   # Multicast port [5405] -> ENTER
   # Do you wish toouse SBD? [y/N] -> N
   # Do you wish tooconfigure an administration IP? [y/N] -> N
   </code></pre>

1. **[2]**  Добавить узел toocluster
   
   <pre><code> 
   sudo ha-cluster-join

   # WARNING: NTP is not configured toostart at system boot.
   # WARNING: No watchdog device found. If SBD is used, hello cluster will be unable toostart without a watchdog.
   # Do you want toocontinue anyway? [y/N] -> y
   # IP address or hostname of existing node (for example: 192.168.1.1) [] -> IP address of node 1 for example 10.0.0.10
   # /root/.ssh/id_dsa already exists - overwrite? [y/N] N
   </code></pre>

1. **[A]**  Toohello пароль hacluster изменить пароль

   <pre><code> 
   sudo passwd hacluster
   </code></pre>

1. **[A]**  Настройка corosync toouse других транспорта и добавьте набору узлов. Иначе кластер не будет работать.
   
   <pre><code> 
   sudo vi /etc/corosync/corosync.conf   
   </code></pre>

   Добавьте следующие полужирным содержимого toohello файл hello.
   
   <pre><code> 
   [...]
     interface { 
        [...] 
     }
     <b>transport:      udpu</b>
   } 
   <b>nodelist {
     node {
      # IP address of <b>prod-nfs-0</b>
      ring0_addr:10.0.0.5
     }
     node {
      # IP address of <b>prod-nfs-1</b>
      ring0_addr:10.0.0.6
     } 
   }</b>
   logging {
     [...]
   </code></pre>

   Затем перезапустите службу corosync hello

   <pre><code>
   sudo service corosync restart
   </code></pre>

1. **[A]** Установите компоненты DRBD.

   <pre><code>
   sudo zypper install drbd drbd-kmp-default drbd-utils
   </code></pre>

1. **[A]**  Создание раздела для hello drbd устройства

   <pre><code>
   sudo sh -c 'echo -e "n\n\n\n\n\nw\n" | fdisk /dev/sdc'
   </code></pre>

1. **[A]** Создайте конфигурации LVM.

   <pre><code>
   sudo pvcreate /dev/sdc1   
   sudo vgcreate vg_NFS /dev/sdc1
   sudo lvcreate -l 100%FREE -n <b>NWS</b> vg_NFS
   </code></pre>

1. **[A]**  Создание hello NFS drbd устройства

   <pre><code>
   sudo vi /etc/drbd.d/<b>NWS</b>_nfs.res
   </code></pre>

   Вставка hello конфигурации для нового устройства drbd hello и выход

   <pre><code>
   resource <b>NWS</b>_nfs {
      protocol     C;
      disk {
         on-io-error       pass_on;
      }
      on <b>prod-nfs-0</b> {
         address   <b>10.0.0.5</b>:7790;
         device    /dev/drbd0;
         disk      /dev/vg_NFS/NWS;
         meta-disk internal;
      }
      on <b>prod-nfs-1</b> {
         address   <b>10.0.0.6</b>:7790;
         device    /dev/drbd0;
         disk      /dev/vg_NFS/NWS;
         meta-disk internal;
      }
   }
   </code></pre>

   Создание устройства drbd hello и запустите ее

   <pre><code>
   sudo drbdadm create-md <b>NWS</b>_nfs
   sudo drbdadm up <b>NWS</b>_nfs
   </code></pre>

1. **[1]** Пропустите начальную синхронизацию.

   <pre><code>
   sudo drbdadm new-current-uuid --clear-bitmap <b>NWS</b>_nfs
   </code></pre>

1. **[1]**  Основного узла набора hello

   <pre><code>
   sudo drbdadm primary --force <b>NWS</b>_nfs
   </code></pre>

1. **[1]**  Подождите, пока не синхронизируются новых устройств drbd hello

   <pre><code>
   sudo cat /proc/drbd

   # version: 8.4.6 (api:1/proto:86-101)
   # GIT-hash: 833d830e0152d1e457fa7856e71e11248ccf3f70 build by abuild@sheep14, 2016-05-09 23:14:56
   # 0: cs:Connected ro:Primary/Secondary ds:UpToDate/UpToDate C r-----
   #    ns:0 nr:0 dw:0 dr:912 al:8 bm:0 lo:0 pe:0 ua:0 ap:0 ep:1 wo:f oos:0
   </code></pre>

1. **[1]**  Создания drbd устройств hello файловых систем

   <pre><code>
   sudo mkfs.xfs /dev/drbd0
   </code></pre>


### <a name="configure-cluster-framework"></a>Настройка платформы кластера

1. **[1]**  Изменить параметры по умолчанию hello

   <pre><code>
   sudo crm configure

   crm(live)configure# rsc_defaults resource-stickiness="1"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

1. **[1]**  Toohello конфигурации кластера NFS drbd добавить hello устройства

   <pre><code>
   sudo crm configure

   crm(live)configure# primitive drbd_<b>NWS</b>_nfs \
     ocf:linbit:drbd \
     params drbd_resource="<b>NWS</b>_nfs" \
     op monitor interval="15" role="Master" \
     op monitor interval="30" role="Slave"

   crm(live)configure# ms ms-drbd_<b>NWS</b>_nfs drbd_<b>NWS</b>_nfs \
     meta master-max="1" master-node-max="1" clone-max="2" \
     clone-node-max="1" notify="true" interleave="true"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

1. **[1]**  Создание hello NFS-сервера

   <pre><code>
   sudo crm configure

   crm(live)configure# primitive nfsserver \
     systemd:nfs-server \
     op monitor interval="30s"

   crm(live)configure# clone cl-nfsserver nfsserver interleave="true"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

1. **[1]**  Создать ресурсы файловой системы NFS hello

   <pre><code>
   sudo crm configure

   crm(live)configure# primitive fs_<b>NWS</b>_sapmnt \
     ocf:heartbeat:Filesystem \
     params device=/dev/drbd0 \
     directory=/srv/nfs/<b>NWS</b>  \
     fstype=xfs \
     op monitor interval="10s"

   crm(live)configure# group g-<b>NWS</b>_nfs fs_<b>NWS</b>_sapmnt

   crm(live)configure# order o-<b>NWS</b>_drbd_before_nfs inf: \
     ms-drbd_<b>NWS</b>_nfs:promote g-<b>NWS</b>_nfs:start
   
   crm(live)configure# colocation col-<b>NWS</b>_nfs_on_drbd inf: \
     g-<b>NWS</b>_nfs ms-drbd_<b>NWS</b>_nfs:Master

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

1. **[1]**  Создание экспортирует NFS hello

   <pre><code>
   sudo mkdir /srv/nfs/<b>NWS</b>/sidsys
   sudo mkdir /srv/nfs/<b>NWS</b>/sapmntsid
   sudo mkdir /srv/nfs/<b>NWS</b>/trans

   sudo crm configure

   crm(live)configure# primitive exportfs_<b>NWS</b> \
     ocf:heartbeat:exportfs \
     params directory="/srv/nfs/<b>NWS</b>" \
     options="rw,no_root_squash" \
     clientspec="*" fsid=0 \
     wait_for_leasetime_on_stop=true \
     op monitor interval="30s"

   crm(live)configure# modgroup g-<b>NWS</b>_nfs add exportfs_<b>NWS</b>

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

1. **[1]**  Создание виртуального IP-ресурс и зонд работоспособности для hello внутренняя Подсистема балансировки нагрузки

   <pre><code>
   sudo crm configure

   crm(live)configure# primitive vip_<b>NWS</b>_nfs IPaddr2 \
     params ip=<b>10.0.0.4</b> cidr_netmask=24 \
     op monitor interval=10 timeout=20

   crm(live)configure# primitive nc_<b>NWS</b>_nfs anything \
     params binfile="/usr/bin/nc" cmdline_options="-l -k 610<b>00</b>" \
     op monitor timeout=20s interval=10 depth=0

   crm(live)configure# modgroup g-<b>NWS</b>_nfs add nc_<b>NWS</b>_nfs
   crm(live)configure# modgroup g-<b>NWS</b>_nfs add vip_<b>NWS</b>_nfs

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

### <a name="create-stonith-device"></a>Создание устройства STONITH

Hello STONITH устройство использует tooauthorize участника-службы для Microsoft Azure. Выполните эти шаги toocreate участника службы.

1. Go слишком<https://portal.azure.com>
1. Привет открыть колонку Azure Active Directory  
   Go tooProperties и запишите hello идентификатор каталога. Это hello **ИД клиента**.
1. Щелкните "Регистрация приложений".
1. Нажмите "Добавить"
1. Введите имя, выберите тип приложения "Веб-приложения или API", введите URL-адрес входа (например. http://localhost) и нажмите кнопку "Создать".
1. Hello URL-адрес входа не используется и может быть любой допустимый URL-адрес
1. Здравствуйте, выберите новое приложение и щелкните на вкладке Параметры hello ключи
1. Введите описание нового ключа, выберите "Срок действия не ограничен" и нажмите кнопку "Сохранить".
1. Запишите значение hello. Он используется как hello **пароль** для hello участника-службы
1. Запишите hello идентификатор приложения. Он используется как hello username (**идентификатора входа** в hello действия) для hello участника-службы

Hello участника-службы не имеет разрешения tooaccess ресурсам Azure по умолчанию. Необходимые субъекта-службы разрешений toogive hello toostart и остановить (освободить) всех виртуальных машин кластера hello.

1. Go toohttps://portal.azure.com
1. Здравствуйте, откройте колонку все ресурсы
1. Выберите виртуальную машину, hello
1. Выберите "Управление доступом (IAM)".
1. Нажмите "Добавить"
1. Выберите роль hello владельца
1. Введите имя приложения hello, созданной выше hello
1. Нажмите кнопку "ОК"

#### <a name="1-create-hello-stonith-devices"></a>**[1]**  Создайте hello STONITH устройства

После редактирования hello разрешения для виртуальных машин hello hello STONITH устройства можно настроить в кластере hello.

<pre><code>
sudo crm configure

# replace hello bold string with your subscription id, resource group, tenant id, service principal id and password

crm(live)configure# primitive rsc_st_azure_1 stonith:fence_azure_arm \
   params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

crm(live)configure# primitive rsc_st_azure_2 stonith:fence_azure_arm \
   params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

crm(live)configure# colocation col_st_azure -2000: rsc_st_azure_1:Started rsc_st_azure_2:Started

crm(live)configure# commit
crm(live)configure# exit
</code></pre>

#### <a name="1-enable-hello-use-of-a-stonith-device"></a>**[1]**  Включить использование hello STONITH устройства

<pre><code>
sudo crm configure property stonith-enabled=true 
</code></pre>

## <a name="setting-up-ascs"></a>Настройка (A)SCS

### <a name="deploying-linux"></a>Развертывание Linux

Hello Azure Marketplace содержит изображение для SUSE Linux Enterprise Server 12 приложений SAP, которые используются toodeploy новых виртуальных машин. образ marketplace Hello содержит hello ресурсов агента для SAP NetWeaver.

Можно использовать один из шаблонов hello быстрого запуска на github toodeploy все необходимые ресурсы. шаблон Hello развертывает hello виртуальных машин, подсистемы балансировки нагрузки hello, доступности, и т. д. Выполните эти шаги toodeploy hello шаблона.

1. Откройте hello [ASCS/SCS Multi SID шаблона] [ template-multisid-xscs] или hello [схождение выполнено шаблона] [ template-converged] ASCS/SCS шаблона на hello Azure портала hello Создает hello балансировки нагрузки правила для SAP NetWeaver ASCS/SCS hello и экземпляров ющих Методов (Linux), тогда как hello схождением шаблон также создает правила балансировки нагрузки hello для базы данных (например, Microsoft SQL Server или SAP HANA). Если планируется tooinstall системы на основе SAP NetWeaver, а также базы данных hello tooinstall на hello одной машины, используйте hello [схождение выполнено шаблона][template-converged].
1. Введите следующие параметры hello
   1. Префикс ресурса (только шаблон нескольких ИД безопасности ASCS/SCS).  
      Введите префикс hello требуется toouse. Hello значение используется как префикс для hello ресурсы, которые развертываются.
   3. Идентификатор системы SAP (только конвергированный шаблон).  
      Введите системы SAP hello идентификатор hello требуется tooinstall системы SAP. Hello идентификатор используется в качестве префикса для hello ресурсы, которые развертываются.
   4. Тип стека  
      Выберите тип стека SAP NetWeaver hello
   5. Тип ОС  
      Выберите один из hello ОС Linux. Для этого примера выберите SLES 12 BYOS.
   6. Тип базы данных.  
      Выберите HANA.
   7. Размер системы SAP  
      предоставляет Hello объем SAPS hello новую систему. Если вы не уверены, сколько SAPS hello система требует, попросите вашего партнера технологии SAP или системные интеграторы
   8. Доступность системы  
      Выберите высокую доступность
   9. Имя пользователя и пароль администратора  
      Создать нового пользователя, можно использовать toolog на компьютере toohello.
   10. Идентификатор подсети  
   Идентификатор Hello hello подсети toowhich hello виртуальных машин должен быть подключен к.  Оставьте пустым, если требуется, чтобы toocreate новую виртуальную сеть или выберите hello одной подсети, используемые или созданный как часть развертывания сервера для NFS hello. Идентификатор Hello обычно выглядит /subscriptions/**&lt;код_подписки&gt;**/resourceGroups/**&lt;имя группы ресурсов&gt;**/providers/ Microsoft.Network/virtualNetworks/**&lt;имя виртуальной сети&gt;**/subnets/**&lt;имя подсети&gt;**

### <a name="installation"></a>Установка

Hello следующие элементы имеют префикс либо **[A]** -узлы применимо tooall **[1]** -только применимые toonode 1 или **[2]** -только применимые toonode 2.

1. **[A]** Обновите SLES.

   <pre><code>
   sudo zypper update
   </code></pre>

1. **[1]** Включите доступ по протоколу SSH.

   <pre><code>
   sudo ssh-keygen -tdsa
   
   # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
   # Enter passphrase (empty for no passphrase): -> ENTER
   # Enter same passphrase again: -> ENTER
   
   # copy hello public key
   sudo cat /root/.ssh/id_dsa.pub
   </code></pre>

2. **[2]** Включите доступ по протоколу SSH.

   <pre><code>
   sudo ssh-keygen -tdsa

   # insert hello public key you copied in hello last step into hello authorized keys file on hello second server
   sudo vi /root/.ssh/authorized_keys
   
   # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
   # Enter passphrase (empty for no passphrase): -> ENTER
   # Enter same passphrase again: -> ENTER
   
   # copy hello public key   
   sudo cat /root/.ssh/id_dsa.pub
   </code></pre>

1. **[1]** Включите доступ по протоколу SSH.

   <pre><code>
   # insert hello public key you copied in hello last step into hello authorized keys file on hello first server
   sudo vi /root/.ssh/authorized_keys
   </code></pre>

1. **[A]** Установите расширение для обеспечения высокого уровня доступности.
   
   <pre><code>
   sudo zypper install sle-ha-release fence-agents
   </code></pre>

1. **[A]** Обновите агенты ресурсов SAP.  
   
   Исправление для hello агентов ресурсов пакета — необходимые toouse hello новой конфигурации, описанной в этой статье. Можно проверить, если уже установлено исправление hello с hello следующую команду

   <pre><code>
   sudo grep 'parameter name="IS_ERS"' /usr/lib/ocf/resource.d/heartbeat/SAPInstance
   </code></pre>

   Hello вывода должен быть аналогичен

   <pre><code>
   &lt;parameter name="IS_ERS" unique="0" required="0"&gt;
   </code></pre>

   Если команда grep hello не удается найти параметр IS_ERS hello, необходимо исправление tooinstall hello, перечисленные на [hello SUSE страницу загрузки](https://download.suse.com/patch/finder/#bu=suse&familyId=&productId=&dateRange=&startDate=&endDate=&priority=&architecture=&keywords=resource-agents)

   <pre><code>
   # example for patch for SLES 12 SP1
   sudo zypper in -t patch SUSE-SLE-HA-12-SP1-2017-885=1
   # example for patch for SLES 12 SP2
   sudo zypper in -t patch SUSE-SLE-HA-12-SP2-2017-886=1
   </code></pre>

1. **[A]** Установите разрешения имен.   

   Можно использовать DNS-сервер или измените hello/etc/hosts, на всех узлах. В этом примере показано, как toouse hello файл/etc/hosts.
   Замените hello IP-адрес и имя узла hello в hello, следующие команды

   <pre><code>
   sudo vi /etc/hosts
   </code></pre>
   
   Вставьте следующие строки слишком/и т. д/узлы hello. Изменение среды toomatch hello IP адрес и имя узла   
   
   <pre><code>
   # IP address of hello load balancer frontend configuration for NFS
   <b>10.0.0.4 nws-nfs</b>
   # IP address of hello load balancer frontend configuration for SAP NetWeaver ASCS/SCS
   <b>10.0.0.10 nws-ascs</b>
   # IP address of hello load balancer frontend configuration for SAP NetWeaver ERS
   <b>10.0.0.11 nws-ers</b>
   # IP address of hello load balancer frontend configuration for database
   <b>10.0.0.12 nws-db</b>
   </code></pre>

1. **[1]** Установите кластер.
   
   <pre><code>
   sudo ha-cluster-init
   
   # Do you want toocontinue anyway? [y/N] -> y
   # Network address toobind too(for example: 192.168.1.0) [10.79.227.0] -> ENTER
   # Multicast address (for example: 239.x.x.x) [239.174.218.125] -> ENTER
   # Multicast port [5405] -> ENTER
   # Do you wish toouse SBD? [y/N] -> N
   # Do you wish tooconfigure an administration IP? [y/N] -> N
   </code></pre>

1. **[2]**  Добавить узел toocluster
   
   <pre><code> 
   sudo ha-cluster-join

   # WARNING: NTP is not configured toostart at system boot.
   # WARNING: No watchdog device found. If SBD is used, hello cluster will be unable toostart without a watchdog.
   # Do you want toocontinue anyway? [y/N] -> y
   # IP address or hostname of existing node (for example: 192.168.1.1) [] -> IP address of node 1 for example 10.0.0.10
   # /root/.ssh/id_dsa already exists - overwrite? [y/N] N
   </code></pre>

1. **[A]**  Toohello пароль hacluster изменить пароль

   <pre><code> 
   sudo passwd hacluster
   </code></pre>

1. **[A]**  Настройка corosync toouse других транспорта и добавьте набору узлов. Иначе кластер не будет работать.
   
   <pre><code> 
   sudo vi /etc/corosync/corosync.conf   
   </code></pre>

   Добавьте следующие полужирным содержимого toohello файл hello.
   
   <pre><code> 
   [...]
     interface { 
        [...] 
     }
     <b>transport:      udpu</b>
   } 
   <b>nodelist {
     node {
      # IP address of <b>nws-cl-0</b>
      ring0_addr:     10.0.0.14
     }
     node {
      # IP address of <b>nws-cl-1</b>
      ring0_addr:     10.0.0.13
     } 
   }</b>
   logging {
     [...]
   </code></pre>

   Затем перезапустите службу corosync hello

   <pre><code>
   sudo service corosync restart
   </code></pre>

1. **[A]** Установите компоненты DRBD.

   <pre><code>
   sudo zypper install drbd drbd-kmp-default drbd-utils
   </code></pre>

1. **[A]**  Создание раздела для hello drbd устройства

   <pre><code>
   sudo sh -c 'echo -e "n\n\n\n\n\nw\n" | fdisk /dev/sdc'
   </code></pre>

1. **[A]** Создайте конфигурации LVM.

   <pre><code>
   sudo pvcreate /dev/sdc1   
   sudo vgcreate vg_<b>NWS</b> /dev/sdc1
   sudo lvcreate -l 50%FREE -n <b>NWS</b>_ASCS vg_<b>NWS</b>
   sudo lvcreate -l 50%FREE -n <b>NWS</b>_ERS vg_<b>NWS</b>
   </code></pre>

1. **[A]**  Создание hello SCS drbd устройства

   <pre><code>
   sudo vi /etc/drbd.d/<b>NWS</b>_ascs.res
   </code></pre>

   Вставка hello конфигурации для нового устройства drbd hello и выход

   <pre><code>
   resource <b>NWS</b>_ascs {
      protocol     C;
      disk {
         on-io-error       pass_on;
      }
      on <b>nws-cl-0</b> {
         address   <b>10.0.0.14</b>:7791;
         device    /dev/drbd0;
         disk      /dev/vg_NWS/NWS_ASCS;
         meta-disk internal;
      }
      on <b>nws-cl-1</b> {
         address   <b>10.0.0.13</b>:7791;
         device    /dev/drbd0;
         disk      /dev/vg_NWS/NWS_ASCS;
         meta-disk internal;
      }
   }
   </code></pre>

   Создание устройства drbd hello и запустите ее

   <pre><code>
   sudo drbdadm create-md <b>NWS</b>_ascs
   sudo drbdadm up <b>NWS</b>_ascs
   </code></pre>

1. **[A]**  Создание hello ющих Методов drbd устройства

   <pre><code>
   sudo vi /etc/drbd.d/<b>NWS</b>_ers.res
   </code></pre>

   Вставка hello конфигурации для нового устройства drbd hello и выход

   <pre><code>
   resource <b>NWS</b>_ers {
      protocol     C;
      disk {
         on-io-error       pass_on;
      }
      on <b>nws-cl-0</b> {
         address   <b>10.0.0.14</b>:7792;
         device    /dev/drbd1;
         disk      /dev/vg_NWS/NWS_ERS;
         meta-disk internal;
      }
      on <b>nws-cl-1</b> {
         address   <b>10.0.0.13</b>:7792;
         device    /dev/drbd1;
         disk      /dev/vg_NWS/NWS_ERS;
         meta-disk internal;
      }
   }
   </code></pre>

   Создание устройства drbd hello и запустите ее

   <pre><code>
   sudo drbdadm create-md <b>NWS</b>_ers
   sudo drbdadm up <b>NWS</b>_ers
   </code></pre>

1. **[1]** Пропустите начальную синхронизацию.

   <pre><code>
   sudo drbdadm new-current-uuid --clear-bitmap <b>NWS</b>_ascs
   sudo drbdadm new-current-uuid --clear-bitmap <b>NWS</b>_ers
   </code></pre>

1. **[1]**  Основного узла набора hello

   <pre><code>
   sudo drbdadm primary --force <b>NWS</b>_ascs
   sudo drbdadm primary --force <b>NWS</b>_ers
   </code></pre>

1. **[1]**  Подождите, пока не синхронизируются новых устройств drbd hello

   <pre><code>
   sudo cat /proc/drbd

   # version: 8.4.6 (api:1/proto:86-101)
   # GIT-hash: 833d830e0152d1e457fa7856e71e11248ccf3f70 build by abuild@sheep14, 2016-05-09 23:14:56
   # 0: cs:<b>Connected</b> ro:Primary/Secondary ds:<b>UpToDate/UpToDate</b> C r-----
   #     ns:93991268 nr:0 dw:93991268 dr:93944920 al:383 bm:0 lo:0 pe:0 ua:0 ap:0 ep:1 wo:f oos:0
   # 1: cs:<b>Connected</b> ro:Primary/Secondary ds:<b>UpToDate/UpToDate</b> C r-----
   #     ns:6047920 nr:0 dw:6047920 dr:6039112 al:34 bm:0 lo:0 pe:0 ua:0 ap:0 ep:1 wo:f oos:0
   # 2: cs:<b>Connected</b> ro:Primary/Secondary ds:<b>UpToDate/UpToDate</b> C r-----
   #     ns:5142732 nr:0 dw:5142732 dr:5133924 al:30 bm:0 lo:0 pe:0 ua:0 ap:0 ep:1 wo:f oos:0
   </code></pre>

1. **[1]**  Создания drbd устройств hello файловых систем

   <pre><code>
   sudo mkfs.xfs /dev/drbd0
   sudo mkfs.xfs /dev/drbd1
   </code></pre>


### <a name="configure-cluster-framework"></a>Настройка платформы кластера

**[1]**  Изменить параметры по умолчанию hello

   <pre><code>
   sudo crm configure

   crm(live)configure# rsc_defaults resource-stickiness="1"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

## <a name="prepare-for-sap-netweaver-installation"></a>Подготовка к установке SAP NetWeaver

1. **[A]**  Hello создание общих каталогов

   <pre><code>
   sudo mkdir -p /sapmnt/<b>NWS</b>
   sudo mkdir -p /usr/sap/trans
   sudo mkdir -p /usr/sap/<b>NWS</b>/SYS

   sudo chattr +i /sapmnt/<b>NWS</b>
   sudo chattr +i /usr/sap/trans
   sudo chattr +i /usr/sap/<b>NWS</b>/SYS
   </code></pre>

1. **[A]** Настройте autofs.
 
   <pre><code>
   sudo vi /etc/auto.master

   # Add hello following line toohello file, save and exit
   +auto.master
   /- /etc/auto.direct
   </code></pre>

   Создайте файл со следующим текстом:

   <pre><code>
   sudo vi /etc/auto.direct

   # Add hello following lines toohello file, save and exit
   /sapmnt/<b>NWS</b> -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/sapmntsid
   /usr/sap/trans -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/trans
   /usr/sap/<b>NWS</b>/SYS -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/sidsys
   </code></pre>

   Перезапустите toomount autofs hello новые общие папки

   <pre><code>
   sudo systemctl enable autofs
   sudo service autofs restart
   </code></pre>

1. **[A]** Настройте файл подкачки.
 
   <pre><code>
   sudo vi /etc/waagent.conf

   # Set hello property ResourceDisk.EnableSwap tooy
   # Create and use swapfile on resource disk.
   ResourceDisk.EnableSwap=<b>y</b>

   # Set hello size of hello SWAP file with property ResourceDisk.SwapSizeMB
   # hello free space of resource disk varies by virtual machine size. Make sure that you do not set a value that is too big. You can check hello SWAP space with command swapon
   # Size of hello swapfile.
   ResourceDisk.SwapSizeMB=<b>2000</b>
   </code></pre>

   Перезапустите hello агента tooactivate hello изменений

   <pre><code>
   sudo service waagent restart
   </code></pre>

### <a name="installing-sap-netweaver-ascsers"></a>Установка SAP NetWeaver ASCS/ERS

1. **[1]**  Создание виртуального IP-ресурс и зонд работоспособности для hello внутренняя Подсистема балансировки нагрузки

   <pre><code>
   sudo crm node standby <b>nws-cl-1</b>
   sudo crm configure

   crm(live)configure# primitive drbd_<b>NWS</b>_ASCS \
     ocf:linbit:drbd \
     params drbd_resource="<b>NWS</b>_ascs" \
     op monitor interval="15" role="Master" \
     op monitor interval="30" role="Slave"

   crm(live)configure# ms ms-drbd_<b>NWS</b>_ASCS drbd_<b>NWS</b>_ASCS \
     meta master-max="1" master-node-max="1" clone-max="2" \
     clone-node-max="1" notify="true"

   crm(live)configure# primitive fs_<b>NWS</b>_ASCS \
     ocf:heartbeat:Filesystem \
     params device=/dev/drbd0 \
     directory=/usr/sap/<b>NWS</b>/ASCS<b>00</b>  \
     fstype=xfs \
     op monitor interval="10s"

   crm(live)configure# primitive vip_<b>NWS</b>_ASCS IPaddr2 \
     params ip=<b>10.0.0.10</b> cidr_netmask=24 \
     op monitor interval=10 timeout=20

   crm(live)configure# primitive nc_<b>NWS</b>_ASCS anything \
     params binfile="/usr/bin/nc" cmdline_options="-l -k 620<b>00</b>" \
     op monitor timeout=20s interval=10 depth=0
   
   crm(live)configure# group g-<b>NWS</b>_ASCS nc_<b>NWS</b>_ASCS vip_<b>NWS</b>_ASCS fs_<b>NWS</b>_ASCS \
      meta resource-stickiness=3000

   crm(live)configure# order o-<b>NWS</b>_drbd_before_ASCS inf: \
     ms-drbd_<b>NWS</b>_ASCS:promote g-<b>NWS</b>_ASCS:start
   
   crm(live)configure# colocation col-<b>NWS</b>_ASCS_on_drbd inf: \
     ms-drbd_<b>NWS</b>_ASCS:Master g-<b>NWS</b>_ASCS
   
   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

   Убедитесь, что состояние кластера hello в норме и что запущены все ресурсы. Не важно, на какие ресурсы узла hello выполняются.

   <pre><code>
   sudo crm_mon -r

   # Node nws-cl-1: standby
   # <b>Online: [ nws-cl-0 ]</b>
   # 
   # Full list of resources:
   # 
   #  Master/Slave Set: ms-drbd_NWS_ASCS [drbd_NWS_ASCS]
   #      <b>Masters: [ nws-cl-0 ]</b>
   #      Stopped: [ nws-cl-1 ]
   #  Resource Group: g-NWS_ASCS
   #      nc_NWS_ASCS        (ocf::heartbeat:anything):      <b>Started nws-cl-0</b>
   #      vip_NWS_ASCS       (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-0</b>
   #      fs_NWS_ASCS        (ocf::heartbeat:Filesystem):    <b>Started nws-cl-0</b>
   </code></pre>

1. **[1]** Установите SAP NetWeaver ASCS.  

   Установите SAP NetWeaver ASCS в качестве корневого на первом узле hello, с помощью виртуального имени узла, например сопоставляет IP-адрес toohello hello конфигурации переднего плана подсистемы балансировки нагрузки для hello ASCS <b>nws ascs</b>, <b>10.0.0.10</b>и hello номера экземпляра, который использовался для hello пробы подсистемы балансировки нагрузки hello, например <b>00</b>.

   Можно использовать hello sapinst параметр SAPINST_REMOTE_ACCESS_USER tooallow toosapinst tooconnect непривилегированным пользователем.

   <pre><code>
   sudo &lt;swpm&gt;/sapinst SAPINST_REMOTE_ACCESS_USER=<b>sapadmin</b>
   </code></pre>

1. **[1]**  Создание виртуального IP-ресурс и зонд работоспособности для hello внутренняя Подсистема балансировки нагрузки

   <pre><code>
   sudo crm node standby <b>nws-cl-0</b>
   sudo crm node online <b>nws-cl-1</b>
   sudo crm configure

   crm(live)configure# primitive drbd_<b>NWS</b>_ERS \
     ocf:linbit:drbd \
     params drbd_resource="<b>NWS</b>_ers" \
     op monitor interval="15" role="Master" \
     op monitor interval="30" role="Slave"

   crm(live)configure# ms ms-drbd_<b>NWS</b>_ERS drbd_<b>NWS</b>_ERS \
     meta master-max="1" master-node-max="1" clone-max="2" \
     clone-node-max="1" notify="true"

   crm(live)configure# primitive fs_<b>NWS</b>_ERS \
     ocf:heartbeat:Filesystem \
     params device=/dev/drbd1 \
     directory=/usr/sap/<b>NWS</b>/ERS<b>02</b>  \
     fstype=xfs \
     op monitor interval="10s"

   crm(live)configure# primitive vip_<b>NWS</b>_ERS IPaddr2 \
     params ip=<b>10.0.0.11</b> cidr_netmask=24 \
     op monitor interval=10 timeout=20

   crm(live)configure# primitive nc_<b>NWS</b>_ERS anything \
    params binfile="/usr/bin/nc" cmdline_options="-l -k 621<b>02</b>" \
    op monitor timeout=20s interval=10 depth=0

   crm(live)configure# group g-<b>NWS</b>_ERS nc_<b>NWS</b>_ERS vip_<b>NWS</b>_ERS fs_<b>NWS</b>_ERS

   crm(live)configure# order o-<b>NWS</b>_drbd_before_ERS inf: \
     ms-drbd_<b>NWS</b>_ERS:promote g-<b>NWS</b>_ERS:start
   
   crm(live)configure# colocation col-<b>NWS</b>_ERS_on_drbd inf: \
     ms-drbd_<b>NWS</b>_ERS:Master g-<b>NWS</b>_ERS
   
   crm(live)configure# commit
   # WARNING: Resources nc_NWS_ASCS,nc_NWS_ERS,nc_NWS_nfs violate uniqueness for parameter "binfile": "/usr/bin/nc"
   # Do you still want toocommit (y/n)? y

   crm(live)configure# exit
   
   </code></pre>
 
   Убедитесь, что состояние кластера hello в норме и что запущены все ресурсы. Не важно, на какие ресурсы узла hello выполняются.

   <pre><code>
   sudo crm_mon -r

   # Node <b>nws-cl-0: standby</b>
   # <b>Online: [ nws-cl-1 ]</b>
   # 
   # Full list of resources:
   # 
   #  Master/Slave Set: ms-drbd_NWS_ASCS [drbd_NWS_ASCS]
   #      <b>Masters: [ nws-cl-1 ]</b>
   #      Stopped: [ nws-cl-0 ]
   #  Resource Group: g-NWS_ASCS
   #      nc_NWS_ASCS        (ocf::heartbeat:anything):      <b>Started nws-cl-1</b>
   #      vip_NWS_ASCS       (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-1</b>
   #      fs_NWS_ASCS        (ocf::heartbeat:Filesystem):    <b>Started nws-cl-1</b>
   #  Master/Slave Set: ms-drbd_NWS_ERS [drbd_NWS_ERS]
   #      <b>Masters: [ nws-cl-1 ]</b>
   #      Stopped: [ nws-cl-0 ]
   #  Resource Group: g-NWS_ERS
   #      nc_NWS_ERS (ocf::heartbeat:anything):      <b>Started nws-cl-1</b>
   #      vip_NWS_ERS        (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-1</b>
   #      fs_NWS_ERS (ocf::heartbeat:Filesystem):    <b>Started nws-cl-1</b>
   </code></pre>

1. **[2]** Установите SAP NetWeaver ERS.  

   Установите ющих Методов SAP NetWeaver в качестве корневого на второй узел hello, с помощью виртуального имени узла, которое сопоставляет IP-адрес toohello hello конфигурации переднего плана подсистемы балансировки нагрузки для hello ющих Методов, например <b>ющих методов nws</b>, <b>10.0.0.11</b> и hello номера экземпляра, который использовался для hello пробы подсистемы балансировки нагрузки hello, например <b>02</b>.

   Можно использовать hello sapinst параметр SAPINST_REMOTE_ACCESS_USER tooallow toosapinst tooconnect непривилегированным пользователем.

   <pre><code>
   sudo &lt;swpm&gt;/sapinst SAPINST_REMOTE_ACCESS_USER=<b>sapadmin</b>
   </code></pre>

   > [!NOTE]
   > Используйте SWPM SP 20 PL 05 или более поздней версии. Более ранние версии не правильно установить разрешения hello и hello установка завершится с ошибкой.
   > 

1. **[1]**  Адаптировать hello ASCS/SCS и ющих Методов экземпляра профили
 
   * Профиль ASCS/SCS

   <pre><code> 
   sudo vi /sapmnt/<b>NWS</b>/profile/<b>NWS</b>_<b>ASCS00</b>_<b>nws-ascs</b>

   # Change hello restart command tooa start command
   #Restart_Program_01 = local $(_EN) pf=$(_PF)
   Start_Program_01 = local $(_EN) pf=$(_PF)

   # Add hello following lines
   service/halib = $(DIR_CT_RUN)/saphascriptco.so
   service/halib_cluster_connector = /usr/bin/sap_suse_cluster_connector

   # Add hello keep alive parameter
   enque/encni/set_so_keepalive = true
   </code></pre>

   * Профиль ERS

   <pre><code> 
   sudo vi /sapmnt/<b>NWS</b>/profile/<b>NWS</b>_ERS<b>02</b>_<b>nws-ers</b>

   # Add hello following lines
   service/halib = $(DIR_CT_RUN)/saphascriptco.so
   service/halib_cluster_connector = /usr/bin/sap_suse_cluster_connector
   </code></pre>


1. **[A]** Настройте активность.

   Hello взаимодействие сервера приложений SAP NetWeaver hello и hello ASCS/SCS будет проходить через подсистему балансировки нагрузки программного обеспечения. Подсистема балансировки нагрузки Hello отключает неактивные соединения после истечения времени ожидания можно настроить. tooprevent это нужно tooset параметр в профиль SAP NetWeaver ASCS/SCS hello и изменить параметры системы Linux hello. Дополнительные сведения см. в примечании к SAP [1410736][1410736].
   
   на последнем шаге hello Hello параметр профиля ASCS/SCS поставить в очередь/encni/set_so_keepalive уже добавлена.

   <pre><code> 
   # Change hello Linux system configuration
   sudo sysctl net.ipv4.tcp_keepalive_time=120
   </code></pre>

1. **[A]**  Настройка пользователей SAP hello после установки hello
 
   <pre><code>
   # Add sidadm toohello haclient group
   sudo usermod -aG haclient <b>nws</b>adm   
   </code></pre>

1. **[1]**  Добавить hello ASCS и SAP ющих Методов службы toohello sapservice файл

   Добавьте hello ASCS службы запись toohello второй узел и копировать hello ющих Методов службы запись toohello первый узел.

   <pre><code>
   cat /usr/sap/sapservices | grep ASCS<b>00</b> | sudo ssh <b>nws-cl-1</b> "cat >>/usr/sap/sapservices"
   sudo ssh <b>nws-cl-1</b> "cat /usr/sap/sapservices" | grep ERS<b>02</b> | sudo tee -a /usr/sap/sapservices
   </code></pre>

1. **[1]**  Создать ресурсы кластера hello SAP

   <pre><code>
   sudo crm configure property maintenance-mode="true"

   sudo crm configure

   crm(live)configure# primitive rsc_sap_<b>NWS</b>_ASCS<b>00</b> SAPInstance \
    operations $id=rsc_sap_<b>NWS</b>_ASCS<b>00</b>-operations \
    op monitor interval=11 timeout=60 on_fail=restart \
    params InstanceName=<b>NWS</b>_ASCS<b>00</b>_<b>nws-ascs</b> START_PROFILE="/sapmnt/<b>NWS</b>/profile/<b>NWS</b>_ASCS<b>00</b>_<b>nws-ascs</b>" \
    AUTOMATIC_RECOVER=false \
    meta resource-stickiness=5000 failure-timeout=60 migration-threshold=1 priority=10

   crm(live)configure# primitive rsc_sap_<b>NWS</b>_ERS<b>02</b> SAPInstance \
    operations $id=rsc_sap_<b>NWS</b>_ERS<b>02</b>-operations \
    op monitor interval=11 timeout=60 on_fail=restart \
    params InstanceName=<b>NWS</b>_ERS<b>02</b>_<b>nws-ers</b> START_PROFILE="/sapmnt/<b>NWS</b>/profile/<b>NWS</b>_ERS<b>02</b>_<b>nws-ers</b>" AUTOMATIC_RECOVER=false IS_ERS=true \
    meta priority=1000

   crm(live)configure# modgroup g-<b>NWS</b>_ASCS add rsc_sap_<b>NWS</b>_ASCS<b>00</b>
   crm(live)configure# modgroup g-<b>NWS</b>_ERS add rsc_sap_<b>NWS</b>_ERS<b>02</b>

   crm(live)configure# colocation col_sap_<b>NWS</b>_no_both -5000: g-<b>NWS</b>_ERS g-<b>NWS</b>_ASCS
   crm(live)configure# location loc_sap_<b>NWS</b>_failover_to_ers rsc_sap_<b>NWS</b>_ASCS<b>00</b> rule 2000: runs_ers_<b>NWS</b> eq 1
   crm(live)configure# order ord_sap_<b>NWS</b>_first_start_ascs Optional: rsc_sap_<b>NWS</b>_ASCS<b>00</b>:start rsc_sap_<b>NWS</b>_ERS<b>02</b>:stop symmetrical=false

   crm(live)configure# commit
   crm(live)configure# exit

   sudo crm configure property maintenance-mode="false"
   sudo crm node online <b>nws-cl-0</b>
   </code></pre>

   Убедитесь, что состояние кластера hello в норме и что запущены все ресурсы. Не важно, на какие ресурсы узла hello выполняются.

   <pre><code>
   sudo crm_mon -r

   # Online: <b>[ nws-cl-0 nws-cl-1 ]</b>
   # 
   # Full list of resources:
   # 
   #  Master/Slave Set: ms-drbd_NWS_ASCS [drbd_NWS_ASCS]
   #      <b>Masters: [ nws-cl-0 ]</b>
   #      <b>Slaves: [ nws-cl-1 ]</b>
   #  Resource Group: g-NWS_ASCS
   #      nc_NWS_ASCS        (ocf::heartbeat:anything):      <b>Started nws-cl-0</b>
   #      vip_NWS_ASCS       (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-0</b>
   #      fs_NWS_ASCS        (ocf::heartbeat:Filesystem):    <b>Started nws-cl-0</b>
   #      rsc_sap_NWS_ASCS00 (ocf::heartbeat:SAPInstance):   <b>Started nws-cl-0</b>
   #  Master/Slave Set: ms-drbd_NWS_ERS [drbd_NWS_ERS]
   #      <b>Masters: [ nws-cl-1 ]</b>
   #      <b>Slaves: [ nws-cl-0 ]</b>
   #  Resource Group: g-NWS_ERS
   #      nc_NWS_ERS (ocf::heartbeat:anything):      <b>Started nws-cl-1</b>
   #      vip_NWS_ERS        (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-1</b>
   #      fs_NWS_ERS (ocf::heartbeat:Filesystem):    <b>Started nws-cl-1</b>
   #      rsc_sap_NWS_ERS02  (ocf::heartbeat:SAPInstance):   <b>Started nws-cl-1</b>
   </code></pre>

### <a name="create-stonith-device"></a>Создание устройства STONITH

Hello STONITH устройство использует tooauthorize участника-службы для Microsoft Azure. Выполните эти шаги toocreate участника службы.

1. Go слишком<https://portal.azure.com>
1. Привет открыть колонку Azure Active Directory  
   Go tooProperties и запишите hello идентификатор каталога. Это hello **ИД клиента**.
1. Щелкните "Регистрация приложений".
1. Нажмите "Добавить"
1. Введите имя, выберите тип приложения "Веб-приложения или API", введите URL-адрес входа (например. http://localhost) и нажмите кнопку "Создать".
1. Hello URL-адрес входа не используется и может быть любой допустимый URL-адрес
1. Здравствуйте, выберите новое приложение и щелкните на вкладке Параметры hello ключи
1. Введите описание нового ключа, выберите "Срок действия не ограничен" и нажмите кнопку "Сохранить".
1. Запишите значение hello. Он используется как hello **пароль** для hello участника-службы
1. Запишите hello идентификатор приложения. Он используется как hello username (**идентификатора входа** в hello действия) для hello участника-службы

Hello участника-службы не имеет разрешения tooaccess ресурсам Azure по умолчанию. Необходимые субъекта-службы разрешений toogive hello toostart и остановить (освободить) всех виртуальных машин кластера hello.

1. Go toohttps://portal.azure.com
1. Здравствуйте, откройте колонку все ресурсы
1. Выберите виртуальную машину, hello
1. Выберите "Управление доступом (IAM)".
1. Нажмите "Добавить"
1. Выберите роль hello владельца
1. Введите имя приложения hello, созданной выше hello
1. Нажмите кнопку "ОК"

#### <a name="1-create-hello-stonith-devices"></a>**[1]**  Создайте hello STONITH устройства

После редактирования hello разрешения для виртуальных машин hello hello STONITH устройства можно настроить в кластере hello.

<pre><code>
sudo crm configure

# replace hello bold string with your subscription id, resource group, tenant id, service principal id and password

crm(live)configure# primitive rsc_st_azure_1 stonith:fence_azure_arm \
   params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

crm(live)configure# primitive rsc_st_azure_2 stonith:fence_azure_arm \
   params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

crm(live)configure# colocation col_st_azure -2000: rsc_st_azure_1:Started rsc_st_azure_2:Started

crm(live)configure# commit
crm(live)configure# exit
</code></pre>

#### <a name="1-enable-hello-use-of-a-stonith-device"></a>**[1]**  Включить использование hello STONITH устройства

Разрешить использование hello STONITH устройства

<pre><code>
sudo crm configure property stonith-enabled=true 
</code></pre>

## <a name="install-database"></a>Установка базы данных

В этом примере устанавливается и настраивается репликация системы SAP HANA. SAP HANA будет выполняться в hello же кластера в качестве hello SAP NetWeaver ASCS/SCS и ющих Методов. SAP HANA можно также установить на выделенный кластер. Дополнительные сведения см. в статье [Высокий уровень доступности SAP HANA на виртуальных машинах Azure][sap-hana-ha].

### <a name="prepare-for-sap-hana-installation"></a>Подготовка к установке SAP HANA

Обычно для томов, предназначенных для хранения данных и файлов журнала, рекомендуется использовать LVM. В целях тестирования можно также выбрать toostore hello файла журнала и данных непосредственно на обычный диск.

1. **[A]** LVM.  
   Hello примере предполагается, что hello виртуальные машины имеют четыре дисков данных, следует использовать toocreate два тома.
   
   Создание физических томов для всех дисков, которые должны toouse.
   
   <pre><code>
   sudo pvcreate /dev/sdd
   sudo pvcreate /dev/sde
   sudo pvcreate /dev/sdf
   sudo pvcreate /dev/sdg
   </code></pre>
   
   Создание группы томов для файлов данных hello, одна группа томов для файлов журнала hello и один для общей папки hello SAP HANA
   
   <pre><code>
   sudo vgcreate vg_hana_data /dev/sdd /dev/sde
   sudo vgcreate vg_hana_log /dev/sdf
   sudo vgcreate vg_hana_shared /dev/sdg
   </code></pre>
   
   Создать логические тома hello
   
   <pre><code>
   sudo lvcreate -l 100%FREE -n hana_data vg_hana_data
   sudo lvcreate -l 100%FREE -n hana_log vg_hana_log
   sudo lvcreate -l 100%FREE -n hana_shared vg_hana_shared
   sudo mkfs.xfs /dev/vg_hana_data/hana_data
   sudo mkfs.xfs /dev/vg_hana_log/hana_log
   sudo mkfs.xfs /dev/vg_hana_shared/hana_shared
   </code></pre>
   
   Создайте каталоги подключения hello и скопируйте hello UUID всех логических томов
   
   <pre><code>
   sudo mkdir -p /hana/data
   sudo mkdir -p /hana/log
   sudo mkdir -p /hana/shared
   sudo chattr +i /hana/data
   sudo chattr +i /hana/log
   sudo chattr +i /hana/shared
   # write down hello id of /dev/vg_hana_data/hana_data, /dev/vg_hana_log/hana_log and /dev/vg_hana_shared/hana_shared
   sudo blkid
   </code></pre>
   
   Создайте записи autofs для hello трех логических томах.
   
   <pre><code>
   sudo vi /etc/auto.direct
   </code></pre>
   
   Вставьте этот /etc/auto.direct vi toosudo строки
   
   <pre><code>
   /hana/data -fstype=xfs :UUID=<b>&lt;UUID of /dev/vg_hana_data/hana_data&gt;</b>
   /hana/log -fstype=xfs :UUID=<b>&lt;UUID of /dev/vg_hana_log/hana_log&gt;</b>
   /hana/shared -fstype=xfs :UUID=<b>&lt;UUID of /dev/vg_hana_shared/hana_shared&gt;</b>
   </code></pre>
   
   Подключите новый тома hello
   
   <pre><code>
   sudo service autofs restart 
   </code></pre>

1. **[A]** Обычные диски.  

   Для небольших или демонстрационных систем файлы данных и журналов HANA можно поместить на один диск. Hello следующие команды создают секции на /dev/sdc и отформатируйте его xfs.
   ```bash
   sudo sh -c 'echo -e "n\n\n\n\n\nw\n" | fdisk /dev/sdd'
   sudo mkfs.xfs /dev/sdd1
   
   # write down hello id of /dev/sdd1
   sudo /sbin/blkid
   sudo vi /etc/auto.direct
   ```
   
   Вставьте этот too/etc/auto.direct строки
   <pre><code>
   /hana -fstype=xfs :UUID=<b>&lt;UUID&gt;</b>
   </code></pre>
   
   Создать каталог назначения hello и подключите диск hello.
   
   <pre><code>
   sudo mkdir /hana
   sudo chattr +i /hana
   sudo service autofs restart
   </code></pre>

### <a name="installing-sap-hana"></a>Установка SAP HANA

Hello следующие действия на основе главе 4 hello [SAP HANA SR производительности оптимизированных Scenario guide] [ suse-hana-ha-guide] tooinstall репликации системы SAP HANA. Прочитайте его перед продолжением установки hello.

1. **[A]**  Запустите hdblcm из hello HANA DVD-диска
   
   <pre><code>
   sudo hdblcm --sid=<b>HDB</b> --number=<b>03</b> --action=install --batch --password=<b>&lt;password&gt;</b> --system_user_password=<b>&lt;password for system user&gt;</b>

   sudo /hana/shared/<b>HDB</b>/hdblcm/hdblcm --action=configure_internal_network --listen_interface=internal --internal_network=<b>10.0.0/24</b> --password=<b>&lt;password for system user&gt;</b> --batch
   </code></pre>

1. **[A]** Обновите агент узла SAP.

   Загрузить последний архив агента узла SAP hello hello [SAP Softwarecenter] [ sap-swcenter] и выполнения hello следующие команды tooupgrade hello агента. Замените hello путь toohello архив toopoint toohello загруженный файл.
   <pre><code>
   sudo /usr/sap/hostctrl/exe/saphostexec -upgrade -archive <b>&lt;path tooSAP Host Agent SAR&gt;</b> 
   </code></pre>

1. **[1]** Создайте репликацию HANA (в качестве привилегированного пользователя).  

   Выполните следующую команду hello. Убедитесь, что tooreplace полужирным шрифтом строки (идентификатор HDB HANA системы и номера экземпляра 03) со значениями hello установки SAP HANA.
   <pre><code>
   PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
   hdbsql -u system -i <b>03</b> 'CREATE USER <b>hdb</b>hasync PASSWORD "<b>passwd</b>"' 
   hdbsql -u system -i <b>03</b> 'GRANT DATA ADMIN too<b>hdb</b>hasync' 
   hdbsql -u system -i <b>03</b> 'ALTER USER <b>hdb</b>hasync DISABLE PASSWORD LIFETIME' 
   </code></pre>

1. **[A]** Создайте запись хранилища ключей (в качестве привилегированного пользователя).

   <pre><code>
   PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
   hdbuserstore SET <b>hdb</b>haloc localhost:3<b>03</b>15 <b>hdb</b>hasync <b>&lt;passwd&gt;</b>
   </code></pre>

1. **[1]** Создайте резервную копию базы данных (в качестве привилегированного пользователя).

   <pre><code>
   PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
   hdbsql -u system -i <b>03</b> "BACKUP DATA USING FILE ('<b>initialbackup</b>')" 
   </code></pre>

1. **[1]**  Смена пользователя sapsid HANA toohello и создания hello первичного сайта.

   <pre><code>
   su - <b>hdb</b>adm
   hdbnsutil -sr_enable –-name=<b>SITE1</b>
   </code></pre>

1. **[2]**  Смена пользователя sapsid HANA toohello и создания вторичного сайта hello.

   <pre><code>
   su - <b>hdb</b>adm
   sapcontrol -nr <b>03</b> -function StopWait 600 10
   hdbnsutil -sr_register --remoteHost=<b>nws-cl-0</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE2</b> 
   </code></pre>

1. **[1]** Создайте кластерные ресурсы SAP HANA.

   Во-первых создайте hello топологии.
   
   <pre><code>
   sudo crm configure

   # replace hello bold string with your instance number and HANA system id
   
   crm(live)configure# primitive rsc_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b>   ocf:suse:SAPHanaTopology \
     operations $id="rsc_sap2_<b>HDB</b>_HDB<b>03</b>-operations" \
     op monitor interval="10" timeout="600" \
     op start interval="0" timeout="600" \
     op stop interval="0" timeout="300" \
     params SID="<b>HDB</b>" InstanceNumber="<b>03</b>"
    
   crm(live)configure# clone cln_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> rsc_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> \
     meta is-managed="true" clone-node-max="1" target-role="Started" interleave="true"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>
   
   Создайте hello HANA ресурсы
   
   <pre><code>
   sudo crm configure

   # replace hello bold string with your instance number, HANA system id and hello frontend IP address of hello Azure load balancer. 
    
   crm(live)configure# primitive rsc_SAPHana_<b>HDB</b>_HDB<b>03</b> ocf:suse:SAPHana \
     operations $id="rsc_sap_<b>HDB</b>_HDB<b>03</b>-operations" \
     op start interval="0" timeout="3600" \
     op stop interval="0" timeout="3600" \
     op promote interval="0" timeout="3600" \
     op monitor interval="60" role="Master" timeout="700" \
     op monitor interval="61" role="Slave" timeout="700" \
     params SID="<b>HDB</b>" InstanceNumber="<b>03</b>" PREFER_SITE_TAKEOVER="true" \
     DUPLICATE_PRIMARY_TIMEOUT="7200" AUTOMATED_REGISTER="false"
    
   crm(live)configure# ms msl_SAPHana_<b>HDB</b>_HDB<b>03</b> rsc_SAPHana_<b>HDB</b>_HDB<b>03</b> \
     meta is-managed="true" notify="true" clone-max="2" clone-node-max="1" \
     target-role="Started" interleave="true"
    
   crm(live)configure# primitive rsc_ip_<b>HDB</b>_HDB<b>03</b> ocf:heartbeat:IPaddr2 \ 
     meta target-role="Started" is-managed="true" \ 
     operations $id="rsc_ip_<b>HDB</b>_HDB<b>03</b>-operations" \ 
     op monitor interval="10s" timeout="20s" \ 
     params ip="<b>10.0.0.12</b>" 

   crm(live)configure# primitive rsc_nc_<b>HDB</b>_HDB<b>03</b> anything \ 
     params binfile="/usr/bin/nc" cmdline_options="-l -k 625<b>03</b>" \ 
     op monitor timeout=20s interval=10 depth=0 

   crm(live)configure# group g_ip_<b>HDB</b>_HDB<b>03</b> rsc_ip_<b>HDB</b>_HDB<b>03</b> rsc_nc_<b>HDB</b>_HDB<b>03</b>
    
   crm(live)configure# colocation col_saphana_ip_<b>HDB</b>_HDB<b>03</b> 2000: g_ip_<b>HDB</b>_HDB<b>03</b>:Started \ 
     msl_SAPHana_<b>HDB</b>_HDB<b>03</b>:Master  

   crm(live)configure# order ord_SAPHana_<b>HDB</b>_HDB<b>03</b> 2000: cln_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> \ 
     msl_SAPHana_<b>HDB</b>_HDB<b>03</b>
    
   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

   Убедитесь, что состояние кластера hello в норме и что запущены все ресурсы. Не важно, на какие ресурсы узла hello выполняются.

   <pre><code>
   sudo crm_mon -r

   # <b>Online: [ nws-cl-0 nws-cl-1 ]</b>
   # 
   # Full list of resources:
   # 
   #  Master/Slave Set: ms-drbd_NWS_ASCS [drbd_NWS_ASCS]
   #      <b>Masters: [ nws-cl-1 ]</b>
   #      <b>Slaves: [ nws-cl-0 ]</b>
   #  Resource Group: g-NWS_ASCS
   #      nc_NWS_ASCS        (ocf::heartbeat:anything):      <b>Started nws-cl-1</b>
   #      vip_NWS_ASCS       (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-1</b>
   #      fs_NWS_ASCS        (ocf::heartbeat:Filesystem):    <b>Started nws-cl-1</b>
   #      rsc_sap_NWS_ASCS00 (ocf::heartbeat:SAPInstance):   <b>Started nws-cl-1</b>
   #  Master/Slave Set: ms-drbd_NWS_ERS [drbd_NWS_ERS]
   #      <b>Masters: [ nws-cl-0 ]</b>
   #      <b>Slaves: [ nws-cl-1 ]</b>
   #  Resource Group: g-NWS_ERS
   #      nc_NWS_ERS (ocf::heartbeat:anything):      <b>Started nws-cl-0</b>
   #      vip_NWS_ERS        (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-0</b>
   #      fs_NWS_ERS (ocf::heartbeat:Filesystem):    <b>Started nws-cl-0</b>
   #      rsc_sap_NWS_ERS02  (ocf::heartbeat:SAPInstance):   <b>Started nws-cl-0</b>
   #  Clone Set: cln_SAPHanaTopology_HDB_HDB03 [rsc_SAPHanaTopology_HDB_HDB03]
   #      <b>Started: [ nws-cl-0 nws-cl-1 ]</b>
   #  Master/Slave Set: msl_SAPHana_HDB_HDB03 [rsc_SAPHana_HDB_HDB03]
   #      <b>Masters: [ nws-cl-0 ]</b>
   #      <b>Slaves: [ nws-cl-1 ]</b>
   #  Resource Group: g_ip_HDB_HDB03
   #      rsc_ip_HDB_HDB03   (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-0</b>
   #      rsc_nc_HDB_HDB03   (ocf::heartbeat:anything):      <b>Started nws-cl-0</b>
   # rsc_st_azure_1  (stonith:fence_azure_arm):      <b>Started nws-cl-0</b>
   # rsc_st_azure_2  (stonith:fence_azure_arm):      <b>Started nws-cl-1</b>
   </code></pre>

1. **[1]**  Экземпляр базы данных SAP NetWeaver hello установки

   Установка экземпляра базы данных SAP NetWeaver hello как корневой каталог с помощью виртуального имени узла, которое сопоставляет IP-адрес toohello hello конфигурации переднего плана подсистемы балансировки нагрузки для hello базы данных, например <b>nws db</b> и <b>10.0.0.12</b>.

   Можно использовать hello sapinst параметр SAPINST_REMOTE_ACCESS_USER tooallow toosapinst tooconnect непривилегированным пользователем.

   <pre><code>
   sudo &lt;swpm&gt;/sapinst SAPINST_REMOTE_ACCESS_USER=<b>sapadmin</b>
   </code></pre>

## <a name="sap-netweaver-application-server-installation"></a>Установка сервера приложений SAP NetWeaver

Выполните эти шаги tooinstall сервера приложений SAP. приведенных ниже шагов Hello предполагается установить hello сервера приложений на сервере отличается от hello ASCS/SCS и HANA серверов. В противном случае некоторые шаги hello ниже (например, при настройке разрешения имени узла) не требуются.

1. Настройте разрешение имен.    
   Можно использовать DNS-сервер или измените hello/etc/hosts, на всех узлах. В этом примере показано, как toouse hello файл/etc/hosts.
   Замените hello IP-адрес и имя узла hello в hello, следующие команды
   ```bash
   sudo vi /etc/hosts
   ```
   Вставьте следующие строки слишком/и т. д/узлы hello. Изменение среды toomatch hello IP адрес и имя узла    
    
   <pre><code>
   # IP address of hello load balancer frontend configuration for NFS
   <b>10.0.0.4 nws-nfs</b>
   # IP address of hello load balancer frontend configuration for SAP NetWeaver ASCS/SCS
   <b>10.0.0.10 nws-ascs</b>
   # IP address of hello load balancer frontend configuration for SAP NetWeaver ERS
   <b>10.0.0.11 nws-ers</b>
   # IP address of hello load balancer frontend configuration for database
   <b>10.0.0.12 nws-db</b>
   # IP address of hello application server
   <b>10.0.0.8 nws-di-0</b>
   </code></pre>

1. Создать каталог sapmnt hello

   <pre><code>
   sudo mkdir -p /sapmnt/<b>NWS</b>
   sudo mkdir -p /usr/sap/trans

   sudo chattr +i /sapmnt/<b>NWS</b>
   sudo chattr +i /usr/sap/trans
   </code></pre>

1. Настройте autofs:
 
   <pre><code>
   sudo vi /etc/auto.master

   # Add hello following line toohello file, save and exit
   +auto.master
   /- /etc/auto.direct
   </code></pre>

   Создайте файл со следующим текстом:

   <pre><code>
   sudo vi /etc/auto.direct

   # Add hello following lines toohello file, save and exit
   /sapmnt/<b>NWS</b> -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/sapmntsid
   /usr/sap/trans -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/trans
   </code></pre>

   Перезапустите toomount autofs hello новые общие папки

   <pre><code>
   sudo systemctl enable autofs
   sudo service autofs restart
   </code></pre>

1. Настройте файл подкачки:
 
   <pre><code>
   sudo vi /etc/waagent.conf

   # Set hello property ResourceDisk.EnableSwap tooy
   # Create and use swapfile on resource disk.
   ResourceDisk.EnableSwap=<b>y</b>

   # Set hello size of hello SWAP file with property ResourceDisk.SwapSizeMB
   # hello free space of resource disk varies by virtual machine size. Make sure that you do not set a value that is too big. You can check hello SWAP space with command swapon
   # Size of hello swapfile.
   ResourceDisk.SwapSizeMB=<b>2000</b>
   </code></pre>

   Перезапустите hello агента tooactivate hello изменений

   <pre><code>
   sudo service waagent restart
   </code></pre>

1. Установите сервер приложений SAP NetWeaver:

   Установите основной и дополнительный сервер приложений SAP NetWeaver:

   Можно использовать hello sapinst параметр SAPINST_REMOTE_ACCESS_USER tooallow toosapinst tooconnect непривилегированным пользователем.

   <pre><code>
   sudo &lt;swpm&gt;/sapinst SAPINST_REMOTE_ACCESS_USER=<b>sapadmin</b>
   </code></pre>

1. Обновите безопасное хранилище SAP HANA.

   Обновление hello SAP HANA безопасного хранения toopoint toohello виртуальное имя настройки репликации системы SAP HANA hello.
   <pre><code>
   su - <b>nws</b>adm
   hdbuserstore SET DEFAULT <b>nws-db</b>:3<b>03</b>15 <b>SAPABAP1</b> <b>&lt;password of ABAP schema&gt;</b>
   </code></pre>

## <a name="next-steps"></a>Дальнейшие действия
* [SAP NetWeaver на виртуальных машинах Windows. Руководство по планированию и внедрению][planning-guide]
* [Развертывание программного обеспечения SAP на виртуальных машинах Azure][deployment-guide]
* [SAP NetWeaver на виртуальных машинах Windows. Руководство по развертыванию СУБД][dbms-guide]
* tooestablish высокого уровня доступности и план аварийного восстановления из SAP HANA в Azure (большие экземпляры). в статье toolearn [SAP HANA (крупных экземпляров) высокой доступности и аварийного восстановления в Azure](hana-overview-high-availability-disaster-recovery.md).
* toolearn tooestablish высокий уровень доступности и план аварийного восстановления из SAP HANA на виртуальных машинах Azure, в статье [высокого уровня доступности SAP HANA на виртуальных машинах Azure (ВМ)][sap-hana-ha]
