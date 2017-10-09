---
title: "aaaHigh доступности из SAP HANA на виртуальных машинах Azure (ВМ) | Документы Microsoft"
description: "Обеспечение высокого уровня доступности SAP HANA на виртуальных машинах Azure."
services: virtual-machines-linux
documentationcenter: 
author: MSSedusch
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 04/25/2017
ms.author: sedusch
ms.openlocfilehash: dcb9bb70594f9d97f8a888cec76300bcbe0bf1ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="high-availability-of-sap-hana-on-azure-virtual-machines-vms"></a>Высокий уровень доступности SAP HANA на виртуальных машинах Azure

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

[hana-ha-guide-replication]:sap-hana-high-availability.md#14c19f65-b5aa-4856-9594-b81c7e4df73d
[hana-ha-guide-shared-storage]:sap-hana-high-availability.md#498de331-fa04-490b-997c-b078de457c9d

[suse-hana-ha-guide]:https://www.suse.com/docrep/documents/ir8w88iwu7/suse_linux_enterprise_server_for_sap_applications_12_sp1.pdf
[sap-swcenter]:https://launchpad.support.sap.com/#/softwarecenter
[template-multisid-db]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-db%2Fazuredeploy.json
[template-converged]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-converged%2Fazuredeploy.json

Локально, можно использовать либо HANA системы репликации или использовать общее хранилище tooestablish высокого уровня доступности для SAP HANA.
В настоящее время в Azure поддерживается только настройка системной репликации HANA. Для репликации SAP HANA используются один главный узел и по крайней мере один подчиненный узел. Toohello изменения данных на главном узле hello, реплицируются узлы ведомый toohello синхронно или асинхронно.

В этой статье описывается, как toodeploy hello виртуальных машин, Настройка hello виртуальных машин, установите framework hello кластера, Установка и настройка репликации системы SAP HANA.
В конфигурациях пример hello установки команд номер экземпляра и т.д. 03 и используется идентификатор HDB HANA системы.

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
* [Сценарии оптимизированными SAP HANA SR производительности] [ suse-hana-ha-guide] hello руководство содержит все необходимые сведения tooset копирование репликации системы SAP HANA в локальной среде. Используйте это руководство как основу.

## <a name="deploying-linux"></a>Развертывание Linux

агент Hello ресурсов для SAP HANA включается в SUSE Linux Enterprise Server для приложений SAP.
Hello Azure Marketplace содержит изображение для SUSE Linux Enterprise Server 12 приложений SAP с BYOS (переведите свои собственные подписки), можно использовать toodeploy новых виртуальных машин.

### <a name="manual-deployment"></a>Развертывание вручную

1. Создание группы ресурсов
1. Создайте виртуальную сеть
1. Создание двух учетных записей хранения.
1. Создание группы доступности.  
   Настройка максимального числа доменов обновления.
1. Создание подсистемы балансировки нагрузки (внутренней).  
   Выбор виртуальной сети, созданной ранее.
1. Создание виртуальной машины 1.  
   https://portal.azure.com/#create/suse-byos.sles-for-sap-byos12-sp1  
   SLES For SAP Applications 12 SP1 (BYOS).  
   Выбор учетной записи хранения 1.  
   Выбор группы доступности.  
1. Создание виртуальной машины 2.  
   https://portal.azure.com/#create/suse-byos.sles-for-sap-byos12-sp1  
   SLES For SAP Applications 12 SP1 (BYOS).  
   Выбор учетной записи хранения 2.   
   Выбор группы доступности.  
1. Добавление дисков данных.
1. Настройка балансировки нагрузки hello
    1. Создание пула внешних IP-адресов.
        1. Откройте hello балансировки нагрузки, выберите пул IP-адресов переднего плана и нажмите кнопку Добавить
        1. Введите имя hello hello нового внешнего интерфейса пула IP-адресов (например, hana-frontend)
       1. Нажмите кнопку "ОК"
        1. После создания hello нового внешнего интерфейса пула IP-адресов, запишите его IP-адрес
    1. Создание внутреннего пула.
        1. Откройте hello балансировки нагрузки, выберите внутренние пулы и нажмите кнопку Добавить
        1. Введите имя hello hello нового внутреннего пула (например hana-серверное приложение)
        1. Щелкните "Добавить виртуальную машину".
        1. Выберите группу доступности, созданной ранее hello
        1. Выберите hello виртуальных машин кластера hello SAP HANA
        1. Нажмите кнопку "ОК"
    1. Создание пробы работоспособности
       1. Откройте hello балансировки нагрузки, выберите проверках работоспособности и нажмите кнопку Добавить
        1. Введите имя hello hello новые проверки работоспособности (например, hana-hp)
        1. Выберите протокол TCP, порт 625**03**, интервал, равный 5, и порог состояния неработоспособности, равный 2.
        1. Нажмите кнопку "ОК"
    1. Создание правил балансировки нагрузки.
        1. Откройте hello балансировки нагрузки, выберите правил балансировки нагрузки и нажмите кнопку Добавить
        1. Введите имя hello hello новое правило подсистемы балансировки нагрузки (например hana-балансировки нагрузки-3**03**15)
        1. Выберите hello интерфейсный IP-адрес, внутренний пул и работоспособности проверки, созданную ранее (например, hana-frontend)
        1. Оставьте выбранным протокол TCP и введите порт 3**03**15.
        1. Увеличьте время ожидания простоя too30 минут
       1. **Убедитесь, что tooenable плавающий IP-адрес**
        1. Нажмите кнопку "ОК"
        1. Повторите приведенные выше действия hello для порта 3**03**17

### <a name="deploy-with-template"></a>Развертывание с помощью шаблона
Можно использовать один из шаблонов hello быстрого запуска на github toodeploy все необходимые ресурсы. шаблон Hello развертывает hello виртуальных машин, подсистемы балансировки нагрузки hello, доступности, и т. д. Выполните эти шаги toodeploy hello шаблона.

1. Откройте hello [шаблона базы данных] [ template-multisid-db] или hello [схождение выполнено шаблона] [ template-converged] на портале Azure hello hello шаблона базы данных создает только hello правила балансировки нагрузки для базы данных, а также создает шаблон схождением hello hello правила балансировки нагрузки для ASCS/SCS и экземпляр ющих Методов (Linux). Если планируется tooinstall системы на основе SAP NetWeaver, а также tooinstall hello ASCS/SCS экземпляра на hello же машины, используйте hello [схождение выполнено шаблона][template-converged].
1. Введите следующие параметры hello
    1. Идентификатор системы SAP  
       Введите системы SAP hello идентификатор hello требуется tooinstall системы SAP. Hello идентификатор будет использоваться в качестве префикса hello ресурсы, которые развертываются.
    1. Тип стека (применимо, только если используется шаблон конвергентной hello).  
       Выберите тип стека SAP NetWeaver hello
    1. Тип ОС  
       Выберите один из hello ОС Linux. Для этого примера выберите SLES 12 BYOS.
    1. Тип базы данных.  
       Выберите HANA.
    1. Размер системы SAP  
       предоставляет Hello объем SAPS hello новую систему. Если вы не уверены, сколько SAPS hello систему необходимо, попросите вашего партнера технологии SAP или системные интеграторы
    1. Доступность системы  
       Выберите высокую доступность
    1. Имя пользователя и пароль администратора  
       Создать нового пользователя, можно использовать toolog на компьютере toohello.
    1. Новая или имеющаяся подсеть  
       Определяет, следует ли создать виртуальную сеть и подсеть или использовать имеющуюся подсеть. При наличии виртуальной сети, подключенной tooyour локальную сеть, выберите существующий.
    1. Идентификатор подсети  
    Идентификатор Hello hello подсети toowhich hello виртуальных машин должен быть подключен к. Выберите подсеть hello VPN или Express Route виртуальной сети tooconnect hello виртуальной машины tooyour в локальной сети. Идентификатор Hello обычно выглядит /subscriptions/`<subscription id`> /resourceGroups/`<resource group name`> /providers/Microsoft.Network/virtualNetworks/`<virtual network name`> /subnets/`<subnet name`>

## <a name="setting-up-linux-ha"></a>Настройка высокого уровня доступности Linux

Hello следующих элементов начинаются с префикса либо [A] - применимо tooall узлов, [1] применяется только в случае toonode - применяется только в случае toonode 1 "или" [2] - 2.

1. [A] SLES для SAP BYOS только - регистрация SLES toobe может toouse hello репозиториев
1. [A] Только SLES for SAP BYOS. Добавьте модуль public-cloud.
1. [A] Обновите SLES.
    ```bash
    sudo zypper update

    ```

1. [1] Включите доступ по протоколу SSH.
    ```bash
    sudo ssh-keygen -tdsa
    
    # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
    # Enter passphrase (empty for no passphrase): -> ENTER
    # Enter same passphrase again: -> ENTER
    
    # copy hello public key
    sudo cat /root/.ssh/id_dsa.pub
    ```

2. [2] Включите доступ по протоколу SSH.
    ```bash
    sudo ssh-keygen -tdsa

    # insert hello public key you copied in hello last step into hello authorized keys file on hello second server
    sudo vi /root/.ssh/authorized_keys
    
    # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
    # Enter passphrase (empty for no passphrase): -> ENTER
    # Enter same passphrase again: -> ENTER
    
    # copy hello public key    
    sudo cat /root/.ssh/id_dsa.pub
    ```

1. [1] Включите доступ по протоколу SSH.
    ```bash
    # insert hello public key you copied in hello last step into hello authorized keys file on hello first server
    sudo vi /root/.ssh/authorized_keys
    
    ```

1. [A] Установите расширение для обеспечения высокого уровня доступности.
    ```bash
    sudo zypper install sle-ha-release fence-agents
    
    ```

1. [A] Настройте разметку дисков.
    1. Диспетчер логических томов  
    Как правило, рекомендуется toouse LVM для томов, которые хранят данные и файлы журнала. Hello примере предполагается, что hello виртуальные машины имеют четыре дисков данных, следует использовать toocreate два тома.
        * Создание физических томов для всех дисков, которые должны toouse.
    <pre><code>
    sudo pvcreate /dev/sdc
    sudo pvcreate /dev/sdd
    sudo pvcreate /dev/sde
    sudo pvcreate /dev/sdf
    </code></pre>
        * Создание группы томов для файлов данных hello, одна группа томов для файлов журнала hello и один для общей папки hello SAP HANA
    <pre><code>
    sudo vgcreate vg_hana_data /dev/sdc /dev/sdd
    sudo vgcreate vg_hana_log /dev/sde
    sudo vgcreate vg_hana_shared /dev/sdf
    </code></pre>
        * Создать логические тома hello
    <pre><code>
    sudo lvcreate -l 100%FREE -n hana_data vg_hana_data
    sudo lvcreate -l 100%FREE -n hana_log vg_hana_log
    sudo lvcreate -l 100%FREE -n hana_shared vg_hana_shared
    sudo mkfs.xfs /dev/vg_hana_data/hana_data
    sudo mkfs.xfs /dev/vg_hana_log/hana_log
    sudo mkfs.xfs /dev/vg_hana_shared/hana_shared
    </code></pre>
        * Создайте каталоги подключения hello и скопируйте hello UUID всех логических томов
    <pre><code>
    sudo mkdir -p /hana/data
    sudo mkdir -p /hana/log
    sudo mkdir -p /hana/shared
    # write down hello id of /dev/vg_hana_data/hana_data, /dev/vg_hana_log/hana_log and /dev/vg_hana_shared/hana_shared
    sudo blkid
    </code></pre>
        * Создайте записи fstab для hello трех логических томах.
    <pre><code>
    sudo vi /etc/fstab
    </code></pre>
    Вставьте этот строки слишком/и т. д/fstab
    <pre><code>
    /dev/disk/by-uuid/<b>&lt;UUID of /dev/vg_hana_data/hana_data&gt;</b> /hana/data xfs  defaults,nofail  0  2
    /dev/disk/by-uuid/<b>&lt;UUID of /dev/vg_hana_log/hana_log&gt;</b> /hana/log xfs  defaults,nofail  0  2
    /dev/disk/by-uuid/<b>&lt;UUID of /dev/vg_hana_shared/hana_shared&gt;</b> /hana/shared xfs  defaults,nofail  0  2
    </code></pre>
        * Подключите новый тома hello
    <pre><code>
    sudo mount -a
    </code></pre>
    1. Обычные диски  
       Для небольших или демонстрационных систем файлы данных и журналов HANA можно поместить на один диск. Hello следующие команды создают секции на /dev/sdc и отформатируйте его xfs.
    ```bash
    sudo fdisk /dev/sdc
    sudo mkfs.xfs /dev/sdc1
    
    # <a name="write-down-hello-id-of-devsdc1"></a>Запишите идентификатор hello /dev/sdc1
    sudo /sbin/blkid  sudo vi /etc/fstab
    ```

    Insert this line too/etc/fstab
    <pre><code>
    /dev/disk/by-uuid/<b>&lt;UUID&gt;</b> /hana xfs  defaults,nofail  0  2
    </code></pre>

    Create hello target directory and mount hello disk.

    ```bash
    sudo mkdir /hana
    sudo mount -a
    ```

1. [A] Настройте разрешение имен узлов для всех узлов.  
    Можно использовать DNS-сервер или измените hello/etc/hosts, на всех узлах. В этом примере показано, как toouse hello файл/etc/hosts.
   Замените hello IP-адрес и имя узла hello в hello, следующие команды
    ```bash
    sudo vi /etc/hosts
    ```
    Вставьте следующие строки слишком/и т. д/узлы hello. Изменение среды toomatch hello IP адрес и имя узла    
    
    <pre><code>
    <b>&lt;IP address of host 1&gt; &lt;hostname of host 1&gt;</b>
    <b>&lt;IP address of host 2&gt; &lt;hostname of host 2&gt;</b>
    </code></pre>

1. [1] Установите кластер.
    ```bash
    sudo ha-cluster-init
    
    # Do you want toocontinue anyway? [y/N] -> y
    # Network address toobind too(e.g.: 192.168.1.0) [10.79.227.0] -> ENTER
    # Multicast address (e.g.: 239.x.x.x) [239.174.218.125] -> ENTER
    # Multicast port [5405] -> ENTER
    # Do you wish toouse SBD? [y/N] -> N
    # Do you wish tooconfigure an administration IP? [y/N] -> N
    ```
        
1. [2] Добавление toocluster узла
    ```bash
    sudo ha-cluster-join
        
    # WARNING: NTP is not configured toostart at system boot.
    # WARNING: No watchdog device found. If SBD is used, hello cluster will be unable toostart without a watchdog.
    # Do you want toocontinue anyway? [y/N] -> y
    # IP address or hostname of existing node (e.g.: 192.168.1.1) [] -> IP address of node 1 e.g. 10.0.0.5
    # /root/.ssh/id_dsa already exists - overwrite? [y/N] N
    ```

1. [A] toohello пароль hacluster изменить пароль
    ```bash
    sudo passwd hacluster
    
    ```

1. [A] настройте corosync toouse других транспорта и добавьте набору узлов. Иначе кластер не будет работать.
    ```bash
    sudo vi /etc/corosync/corosync.conf    
    
    ```

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
        ring0_addr:     < ip address of node 1 >
      }
      node {
        ring0_addr:     < ip address of node 2 > 
      } 
    }</b>
    logging {
      [...]
    </code></pre>

    Затем перезапустите службу corosync hello

    ```bash
    sudo service corosync restart
    
    ```

1. [A] Установите пакеты для обеспечения высокого уровня доступности HANA.  
    ```bash
    sudo zypper install SAPHanaSR
    
    ```

## <a name="installing-sap-hana"></a>Установка SAP HANA

Выполните главе 4 hello [SAP HANA SR производительности оптимизированных Scenario guide] [ suse-hana-ha-guide] tooinstall репликации системы SAP HANA.

1. [A] Запустите hdblcm из hello HANA DVD-диска
    * Выберите установку (1).
    * Выберите дополнительные компоненты для установки (1).
    * Введите путь установки [/hana/shared] и нажмите клавишу "ВВОД".
    * Введите имя локального узла [..] и нажмите клавишу "ВВОД".
    * Вы хотите, чтобы система toohello tooadd дополнительных узлов? (Вы хотите добавить дополнительные узлы в систему? (Да/нет)). Нажмите клавишу n и клавишу "ВВОД".
    * Введите идентификатор системы SAP HANA: <SID of HANA e.g. HDB>
    * Введите номер экземпляра [00].   
  Номер экземпляра HANA. Используйте 03 при использовании hello шаблона Azure или за приведенном выше примере hello
    * Выберите режим базы данных и введите индекс [1], затем нажмите клавишу "ВВОД".
    * Выберите использование системы и введите индекс [4].  
  Выберите систему hello использования
    * Введите расположение томов данных [/hana/data/HDB], затем нажмите клавишу "ВВОД".
    * Введите расположение томов журнала [/hana/log/HDB], затем нажмите клавишу "ВВОД".
    * "Restrict maximum memory allocation?" (Перезапустить систему после перезагрузки компьютера?) Нажмите клавишу n и клавишу "ВВОД".
    * Введите имя узла сертификат для узла «...» [...]: Введите "->"
    * Введите пароль пользователя агента узла SAP (sapadm).
    * Подтвердите пароль пользователя агента узла SAP (sapadm).
    * Введите пароль системного администратора (hdbadm).
    * Подтвердите пароль системного администратора (hdbadm).
    * Введите домашний каталог системного администратора [/usr/sap/HDB/home], затем нажмите клавишу "ВВОД".
    * Укажите оболочку для входа администратора системы [/bin/sh] и нажмите клавишу "ВВОД".
    * Введите идентификатор пользователя администратора системы [1001] и нажмите клавишу "ВВОД".
    * Введите идентификатор для группы пользователей (sapsys) [79], затем нажмите клавишу "ВВОД".
    * Введите пароль пользователя базы данных (SYSTEM).
    * Подтвердите пароль пользователя базы данных (SYSTEM).
    * "Restart system after machine reboot?" (Перезапустить систему после перезагрузки компьютера?) Нажмите клавишу n и клавишу "ВВОД".
    * Вы хотите, чтобы toocontinue? (Вы действительно хотите продолжить? (Да/нет)).  
  Проверьте сводки hello и введите y toocontinue
1. [A] Обновите агент узла SAP.  
  Загрузить последний архив агента узла SAP hello hello [SAP Softwarecenter] [ sap-swcenter] и выполнения hello следующие команды tooupgrade hello агента. Замените hello путь toohello архив toopoint toohello загруженный файл.
    ```bash
    sudo /usr/sap/hostctrl/exe/saphostexec -upgrade -archive <path tooSAP Host Agent SAR>
    ```

1. [1] Создайте репликацию HANA (в качестве привилегированного пользователя).  
    Выполните следующую команду hello. Убедитесь, что tooreplace полужирным шрифтом строки (идентификатор HDB HANA системы и номера экземпляра 03) со значениями hello установки SAP HANA.
    <pre><code>
    PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
    hdbsql -u system -i <b>03</b> 'CREATE USER <b>hdb</b>hasync PASSWORD "<b>passwd</b>"' 
    hdbsql -u system -i <b>03</b> 'GRANT DATA ADMIN too<b>hdb</b>hasync' 
    hdbsql -u system -i <b>03</b> 'ALTER USER <b>hdb</b>hasync DISABLE PASSWORD LIFETIME' 
    </code></pre>

1. [A] Создайте запись хранилища ключей (в качестве привилегированного пользователя).
    <pre><code>
    PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
    hdbuserstore SET <b>hdb</b>haloc localhost:3<b>03</b>15 <b>hdb</b>hasync <b>passwd</b>
    </code></pre>
1. [1] Создайте резервную копию базы данных (в качестве привилегированного пользователя).
    <pre><code>
    PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
    hdbsql -u system -i <b>03</b> "BACKUP DATA USING FILE ('<b>initialbackup</b>')" 
    </code></pre>
1. [1] коммутатора toohello sapsid пользователя (например hdbadm), а для создания первичного сайта hello.
    <pre><code>
    su - <b>hdb</b>adm
    hdbnsutil -sr_enable –-name=<b>SITE1</b>
    </code></pre>
1. [2] коммутатора toohello sapsid пользователя (например hdbadm), а для создания вторичного сайта hello.
    <pre><code>
    su - <b>hdb</b>adm
    sapcontrol -nr <b>03</b> -function StopWait 600 10
    hdbnsutil -sr_register --remoteHost=<b>saphanavm1</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE2</b> 
    </code></pre>

## <a name="configure-cluster-framework"></a>Настройка платформы кластера

Изменение параметров по умолчанию hello

<pre>
sudo vi crm-defaults.txt
# enter hello following toocrm-defaults.txt
<code>
property $id="cib-bootstrap-options" \
  no-quorum-policy="ignore" \
  stonith-enabled="true" \
  stonith-action="reboot" \
  stonith-timeout="150s"
rsc_defaults $id="rsc-options" \
  resource-stickiness="1000" \
  migration-threshold="5000"
op_defaults $id="op-options" \
  timeout="600"
</code>

# <a name="now-we-load-hello-file-toohello-cluster"></a>Теперь мы можем загрузить hello файл toohello кластера
sudo crm configure load update crm-defaults.txt
</pre>

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

После редактирования hello разрешения для виртуальных машин hello hello STONITH устройства можно настроить в кластере hello.

<pre>
sudo vi crm-fencing.txt
# enter hello following toocrm-fencing.txt
# replace hello bold string with your subscription id, resource group, tenant id, service principal id and password
<code>
primitive rsc_st_azure_1 stonith:fence_azure_arm \
    params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

primitive rsc_st_azure_2 stonith:fence_azure_arm \
    params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

colocation col_st_azure -2000: rsc_st_azure_1:Started rsc_st_azure_2:Started
</code>

# <a name="now-we-load-hello-file-toohello-cluster"></a>Теперь мы можем загрузить hello файл toohello кластера
sudo crm configure load update crm-fencing.txt
</pre>

### <a name="create-sap-hana-resources"></a>Создание ресурсов SAP HANA

<pre>
sudo vi crm-saphanatop.txt
# enter hello following toocrm-saphana.txt
# replace hello bold string with your instance number and HANA system id
<code>
primitive rsc_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> ocf:suse:SAPHanaTopology \
    operations $id="rsc_sap2_<b>HDB</b>_HDB<b>03</b>-operations" \
    op monitor interval="10" timeout="600" \
    op start interval="0" timeout="600" \
    op stop interval="0" timeout="300" \
    params SID="<b>HDB</b>" InstanceNumber="<b>03</b>"

clone cln_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> rsc_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> \
    meta is-managed="true" clone-node-max="1" target-role="Started" interleave="true"
</code>

# <a name="now-we-load-hello-file-toohello-cluster"></a>Теперь мы можем загрузить hello файл toohello кластера
sudo crm configure load update crm-saphanatop.txt
</pre>

<pre>
sudo vi crm-saphana.txt
# enter hello following toocrm-saphana.txt
# replace hello bold string with your instance number, HANA system id and hello frontend IP address of hello Azure load balancer. 
<code>
primitive rsc_SAPHana_<b>HDB</b>_HDB<b>03</b> ocf:suse:SAPHana \
    operations $id="rsc_sap_<b>HDB</b>_HDB<b>03</b>-operations" \
    op start interval="0" timeout="3600" \
    op stop interval="0" timeout="3600" \
    op promote interval="0" timeout="3600" \
    op monitor interval="60" role="Master" timeout="700" \
    op monitor interval="61" role="Slave" timeout="700" \
    params SID="<b>HDB</b>" InstanceNumber="<b>03</b>" PREFER_SITE_TAKEOVER="true" \
    DUPLICATE_PRIMARY_TIMEOUT="7200" AUTOMATED_REGISTER="false"

ms msl_SAPHana_<b>HDB</b>_HDB<b>03</b> rsc_SAPHana_<b>HDB</b>_HDB<b>03</b> \
    meta is-managed="true" notify="true" clone-max="2" clone-node-max="1" \
    target-role="Started" interleave="true"

primitive rsc_ip_<b>HDB</b>_HDB<b>03</b> ocf:heartbeat:IPaddr2 \ 
    meta target-role="Started" is-managed="true" \ 
    operations $id="rsc_ip_<b>HDB</b>_HDB<b>03</b>-operations" \ 
    op monitor interval="10s" timeout="20s" \ 
    params ip="<b>10.0.0.21</b>" 
primitive rsc_nc_<b>HDB</b>_HDB<b>03</b> anything \ 
    params binfile="/usr/bin/nc" cmdline_options="-l -k 625<b>03</b>" \ 
    op monitor timeout=20s interval=10 depth=0 
group g_ip_<b>HDB</b>_HDB<b>03</b> rsc_ip_<b>HDB</b>_HDB<b>03</b> rsc_nc_<b>HDB</b>_HDB<b>03</b>
 
colocation col_saphana_ip_<b>HDB</b>_HDB<b>03</b> 2000: g_ip_<b>HDB</b>_HDB<b>03</b>:Started \ 
    msl_SAPHana_<b>HDB</b>_HDB<b>03</b>:Master  
order ord_SAPHana_<b>HDB</b>_HDB<b>03</b> 2000: cln_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> \ 
    msl_SAPHana_<b>HDB</b>_HDB<b>03</b>
</code>

# <a name="now-we-load-hello-file-toohello-cluster"></a>Теперь мы можем загрузить hello файл toohello кластера
sudo crm configure load update crm-saphana.txt
</pre>

### <a name="test-cluster-setup"></a>Проверка установки кластера
Hello следующие главы описывают, как можно проверить настройки программы установки. Каждый тест предполагается, что являются корнем и SAP HANA образец hello выполняется на виртуальной машине saphanavm1 hello.

#### <a name="fencing-test"></a>Тестирование ограждения

Можно проверить hello установки агента разграничения hello, отключив hello сетевого интерфейса на saphanavm1 узла.

<pre><code>
sudo ifdown eth0
</code></pre>

Теперь Hello виртуальной машины следует получить перезапуске или остановке в зависимости от конфигурации кластера.
Если задать toooff stonith действие hello hello виртуальной машины будет остановлена и ресурсы hello, перенесенных toohello выполняющаяся виртуальная машина.

После повторного запуска виртуальной машины hello hello SAP HANA ресурсов не удастся toostart дополнительный — при выборе AUTOMATED_REGISTER = «false». В этом случае необходимые tooconfigure hello HANA экземпляр в качестве получателя, выполнив следующую команду hello.

<pre><code>
su - <b>hdb</b>adm

# Stop hello HANA instance just in case it is running
sapcontrol -nr <b>03</b> -function StopWait 600 10
hdbnsutil -sr_register --remoteHost=<b>saphanavm2</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE1</b>

# switch back tooroot and cleanup hello failed state
exit
crm resource cleanup msl_SAPHana_<b>HDB</b>_HDB<b>03</b> <b>saphanavm1</b>
</code></pre>

#### <a name="testing-a-manual-failover"></a>Тестирование отработки отказа вручную

Отработка отказа вручную можно проверить, остановка службы pacemaker hello на saphanavm1 узла.
<pre><code>
service pacemaker stop
</code></pre>

После отработки отказа hello можно снова запустить службу hello. Hello ресурсов SAP HANA на saphanavm1 не удастся toostart дополнительный — при выборе AUTOMATED_REGISTER = «false». В этом случае необходимые tooconfigure hello HANA экземпляр в качестве получателя, выполнив следующую команду hello.

<pre><code>
service pacemaker start
su - <b>hdb</b>adm

# Stop hello HANA instance just in case it is running
sapcontrol -nr <b>03</b> -function StopWait 600 10
hdbnsutil -sr_register --remoteHost=<b>saphanavm2</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE1</b> 


# switch back tooroot and cleanup hello failed state
exit
crm resource cleanup msl_SAPHana_<b>HDB</b>_HDB<b>03</b> <b>saphanavm1</b>
</code></pre>

#### <a name="testing-a-migration"></a>Тестирование переноса

Можно перенести главного узла hello SAP HANA, выполнив следующую команду hello
<pre><code>
crm resource migrate msl_SAPHana_<b>HDB</b>_HDB<b>03</b> <b>saphanavm2</b>
crm resource migrate g_ip_<b>HDB</b>_HDB<b>03</b> <b>saphanavm2</b>
</code></pre>

Это необходимо перенести главного узла SAP HANA hello и hello группу, содержащую hello виртуальных IP адресов toosaphanavm2.
Hello ресурсов SAP HANA на saphanavm1 не удастся toostart дополнительный — при выборе AUTOMATED_REGISTER = «false». В этом случае необходимые tooconfigure hello HANA экземпляр в качестве получателя, выполнив следующую команду hello.

<pre><code>
su - <b>hdb</b>adm

# Stop hello HANA instance just in case it is running
sapcontrol -nr <b>03</b> -function StopWait 600 10
hdbnsutil -sr_register --remoteHost=<b>saphanavm2</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE1</b> 
</code></pre>

При миграции Hello создается расположение ограничений, которые должны toobe снова удалены.

<pre><code>
crm configure edited

# delete location contraints that are named like hello following contraint. You should have two contraints, one for hello SAP HANA resource and one for hello IP address group.
location cli-prefer-g_ip_<b>HDB</b>_HDB<b>03</b> g_ip_<b>HDB</b>_HDB<b>03</b> role=Started inf: <b>saphanavm2</b>
</code></pre>

Необходимо также toocleanup состояние hello hello дополнительного узла ресурса

<pre><code>
# switch back tooroot and cleanup hello failed state
exit
crm resource cleanup msl_SAPHana_<b>HDB</b>_HDB<b>03</b> <b>saphanavm1</b>
</code></pre>

## <a name="next-steps"></a>Дальнейшие действия
* [SAP NetWeaver на виртуальных машинах Windows. Руководство по планированию и внедрению][planning-guide]
* [Развертывание программного обеспечения SAP на виртуальных машинах Azure][deployment-guide]
* [SAP NetWeaver на виртуальных машинах Windows. Руководство по развертыванию СУБД][dbms-guide]
* tooestablish высокого уровня доступности и план аварийного восстановления из SAP HANA в Azure (большие экземпляры). в статье toolearn [SAP HANA (крупных экземпляров) высокой доступности и аварийного восстановления в Azure](hana-overview-high-availability-disaster-recovery.md). 
