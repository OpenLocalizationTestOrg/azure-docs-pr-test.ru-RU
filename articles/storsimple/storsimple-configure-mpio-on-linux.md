---
title: "aaaConfigure MPIO на узле StorSimple Linux | Документы Microsoft"
description: "Настройка MPIO на узел Linux tooa StorSimple подключен, под управлением CentOS 6.6"
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: tysonn
ms.assetid: ca289eed-12b7-4e2e-9117-adf7e2034f2f
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/01/2016
ms.author: alkohli
ms.openlocfilehash: d9f7e02903243494c909313fb2c33ac690764274
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-mpio-on-a-storsimple-host-running-centos"></a>Настройка MPIO на узле StorSimple под управлением CentOS
В этой статье объясняется tooconfigure необходимые шаги hello несколько каналов ввода-ВЫВОДА (MPIO) на сервере узла Centos 6.6. сервер узла Hello-подключенных tooyour устройство Microsoft Azure StorSimple для обеспечения высокой доступности через инициаторы iSCSI. Описывает в автоматическое обнаружение сведений hello многоканального устройств и hello определенные настройки только для томов StorSimple.

Эта процедура является моделей hello применимо tooall устройств серии StorSimple 8000.

> [!NOTE]
> Эта процедура не подходит для виртуального устройства StorSimple. Дополнительные сведения см. в разделе как tooconfigure размещения серверов для виртуального устройства.
> 
> 

## <a name="about-multipathing"></a>Основные сведения о многоканальном вводе-выводе
Hello несколько каналов позволяет tooconfigure несколько путей ввода-вывода между сервером узла и устройством хранения. Эти каналы ввода-вывода являются физическими соединениями SAN, которые могут включать отдельные кабели, коммутаторы, сетевые интерфейсы и контроллеры. Несколько каналов объединяет пути ввода-вывода hello, tooconfigure новое устройство, связанный со всеми hello суммарный путей.

Hello несколько каналов предназначен двойную:

* **Высокий уровень доступности**: предоставляет альтернативный путь, если происходит сбой какой-либо элемент путь hello ввода-вывода (например, кабель, коммутатор, сетевого интерфейса или контроллера).
* **Балансировка нагрузки**: в зависимости от конфигурации hello устройство хранения, он может повысить производительность hello, обнаруживая нагрузках на пути ввода-вывода hello и динамически перераспределения этих нагрузок.

### <a name="about-multipathing-components"></a>Компоненты решения для многоканального ввода-вывода
Решение для многоканального ввода-вывода в ОС Linux состоит из компонентов ядра и компонентов пространства пользователя.

* **Ядра**: hello является основным компонентом hello *сопоставления устройств* , изменение пути ввода-вывода и поддерживает отработку отказа для пути и пути групп.

* **Пространство пользователя**: это *multipath средства* , управляющие многопутевых устройств, предписывая многоканального модуля сопоставления устройств hello какие toodo. Hello средства включают:
   
   * **Multipath**. Отображает многоканальные устройства и настраивает их.
   * **Multipathd**: управляющая программа, выполняющая пути hello multipath и мониторов.
   * **Имя Devmap**: обеспечивает devmaps значимые tooudev имя устройства.
   * **Kpartx**: сопоставляет линейной devmaps toodevice секций toomake многоканального схемы секционирования.
   * **Multipath.conf**: файл конфигурации для многоканального управляющей программы, используемые toooverwrite hello встроенной конфигурации таблицы.

### <a name="about-hello-multipathconf-configuration-file"></a>О файле конфигурации multipath.conf hello
файл конфигурации Hello `/etc/multipath.conf` вносит много hello функции несколько каналов настраивается пользователем. Hello `multipath` команда и hello управляющая программа ядра `multipathd` используйте сведения из этого файла. Hello файл был запрошен только во время настройки hello hello многоканального устройств. Убедитесь, что все изменения были сделаны перед запуском hello `multipath` команды. При изменении файла hello после этого может потребоваться toostop и запустите multipathd снова для эффекта tootake изменения hello.

Hello multipath.conf состоит из пяти разделов.

- **Параметры системного уровня, используемые по умолчанию** *(defaults)*. Здесь можно изменять стандартные системные параметры.
- **Остальные устройства** *(черный список)*: можно указать hello список устройств, которые не должны контролироваться путем сопоставления устройств.
- **Защитить черным списком исключений** *(blacklist_exceptions)*: можно определить конкретные устройства toobe обрабатывается как многоканального устройства, даже если в черный список hello.
- **Определенные параметры хранения контроллера** *(устройства)*: можно указать параметры конфигурации, которые будут применяться toodevices у поставщика и продукта сведения.
- **Определенные параметры устройства** *(multipaths)*: можно использовать параметры конфигурации hello этот раздел toofine настраивать для отдельных логических устройств.

## <a name="configure-multipathing-on-storsimple-connected-toolinux-host"></a>Настроить несколько каналов на узле подключенных tooLinux StorSimple
Узел Linux tooa подключенное устройство StorSimple можно настроить для обеспечения высокой доступности и балансировки нагрузки. Например, если узел Linux hello имеет два интерфейса подключенных toohello устройство SAN и hello имеет два интерфейса подключение toohello SAN Здравствуйте, например, эти интерфейсы являются в одной подсети, а затем будут 4 пути. Однако если каждый интерфейс данных в интерфейс устройства и узла hello в другой подсети IP (и не маршрутизируемый), затем только 2 пути будут доступны. Можно настроить несколько каналов tooautomatically обнаружить все доступные пути hello, выберите алгоритм балансировки нагрузки для этих путей, применять определенные настройки для томов только для StorSimple и затем включить и проверить несколько каналов.

Hello следующая процедура описывает способ tooconfigure несколько каналов, когда устройство StorSimple с двумя сетевыми интерфейсами — узел подключенных tooa с двумя сетевыми интерфейсами.

## <a name="prerequisites"></a>Предварительные требования
В этом разделе описаны предварительные требования hello конфигурации для сервера CentOS и устройства StorSimple.

### <a name="on-centos-host"></a>Узел CentOS
1. Убедитесь, что у узла CentOS есть два активных сетевых интерфейса. Тип:
   
    `ifconfig`
   
    Hello примере показан вывод hello при двух сетевых интерфейсов (`eth0` и `eth1`) присутствуют на узле hello.
   
        [root@centosSS ~]# ifconfig
        eth0  Link encap:Ethernet  HWaddr 00:15:5D:A2:33:41  
          inet addr:10.126.162.65  Bcast:10.126.163.255  Mask:255.255.252.0
          inet6 addr: 2001:4898:4010:3012:215:5dff:fea2:3341/64 Scope:Global
          inet6 addr: fe80::215:5dff:fea2:3341/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
         RX packets:36536 errors:0 dropped:0 overruns:0 frame:0
          TX packets:6312 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
          RX bytes:13994127 (13.3 MiB)  TX bytes:645654 (630.5 KiB)
   
        eth1  Link encap:Ethernet  HWaddr 00:15:5D:A2:33:42  
          inet addr:10.126.162.66  Bcast:10.126.163.255  Mask:255.255.252.0
          inet6 addr: 2001:4898:4010:3012:215:5dff:fea2:3342/64 Scope:Global
          inet6 addr: fe80::215:5dff:fea2:3342/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:25962 errors:0 dropped:0 overruns:0 frame:0
          TX packets:11 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
          RX bytes:2597350 (2.4 MiB)  TX bytes:754 (754.0 b)
   
        loLink encap:Local Loopback  
          inet addr:127.0.0.1  Mask:255.0.0.0
          inet6 addr: ::1/128 Scope:Host
          UP LOOPBACK RUNNING  MTU:65536  Metric:1
          RX packets:12 errors:0 dropped:0 overruns:0 frame:0
          TX packets:12 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0
          RX bytes:720 (720.0 b)  TX bytes:720 (720.0 b)
2. Установите *iSCSI-initiator-utils* на сервер CentOS. Выполните следующие шаги tooinstall hello *iSCSI инициатора utils*.
   
   1. Войдите на узел CentOS как `root` .
   2. Установка hello *iSCSI инициатора utils*. Тип:
      
       `yum install iscsi-initiator-utils`
   3. После hello *iSCSI инициатора utils* успешно установлен, запустить службу iSCSI hello. Тип:
      
       `service iscsid start`
      
       В случаях `iscsid` фактически не может начинаться и hello `--force` параметр будет требоваться
   4. Включение вашей инициатор iSCSI во время загрузки, используйте hello tooensure `chkconfig` команды tooenable hello службы.
      
       `chkconfig iscsi on`
   5. tooverify, что он был правильно программой установки, выполните команду hello.
      
       `chkconfig --list | grep iscsi`
      
       Результат выполнения команды показан ниже.
      
           iscsi   0:off   1:off   2:on3:on4:on5:on6:off
           iscsid  0:off   1:off   2:on3:on4:on5:on6:off
      
       Из hello выше примере видно, что среде iSCSI будет запускаться по времени загрузки на выполнения уровня 2, 3, 4 и 5.
3. Установите *device-mapper-multipath*. Тип:
   
    `yum install device-mapper-multipath`
   
    Hello Установка начнется. Тип **Y** toocontinue запрос на подтверждение.

### <a name="on-storsimple-device"></a>Устройство StorSimple
Устройство StorSimple должно удовлетворять следующим условиям.

* Наличие как минимум двух активных интерфейсов для iSCSI. tooverify, что два интерфейса iSCSI включен на устройстве StorSimple, выполните следующие шаги в классический портал Azure для устройства StorSimple hello hello.
  
  1. Войдите на классический портал hello для устройства StorSimple.
  2. Выберите службы диспетчера StorSimple, щелкните **устройств** и выберите hello конкретного устройства StorSimple. Нажмите кнопку **Настройка** и проверить параметры сетевого интерфейса hello. На снимке экрана ниже показаны два сетевых интерфейса с поддержкой iSCSI. Здесь оба интерфейса 10 GbE (DATA 2 и DATA 3) поддерживают iSCSI.
     
      ![Настройка MPIO на устройстве StorSimple, интерфейс DATA2](./media/storsimple-configure-mpio-on-linux/IC761347.png)
     
      ![Настройка MPIO на устройстве StorSimple, интерфейс DATA3](./media/storsimple-configure-mpio-on-linux/IC761348.png)
     
      В hello **Настройка** страницы
     
     1. Убедитесь, что оба сетевых интерфейса поддерживают iSCSI. Hello **iSCSI включен** должно быть задано слишком**Да**.
     2. Убедитесь, что сетевые интерфейсы hello hello такой же скоростью, должен иметь 1 GbE или 10 GbE.
     3. Обратите внимание, hello IPv4-адреса интерфейсы с включенным iSCSI hello и сохранить для последующего использования на узле hello.
* Hello iSCSI на устройстве StorSimple должны быть доступен с сервера CentOS hello.
      tooverify это, необходимо tooprovide hello IP-адреса интерфейсов StorSimple сеть с поддержкой iSCSI на хост-сервере. Здравствуйте, команды, используемые и соответствующий вывод с DATA2 hello (10.126.162.25) и DATA3 (10.126.162.26) показано ниже:
  
        [root@centosSS ~]# iscsiadm -m discovery -t sendtargets -p 10.126.162.25:3260
        10.126.162.25:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g44mt-target
        10.126.162.26:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g44mt-target

### <a name="hardware-configuration"></a>Конфигурация оборудования
Корпорация Майкрософт рекомендует подключении hello двух iSCSI сетевых интерфейсов для отдельных ветвей для обеспечения избыточности. на следующем рисунке Hello показывает hello рекомендуется следующая конфигурация оборудования для обеспечения высокой доступности и балансировки нагрузки несколько каналов для CentOS server и устройства StorSimple.

![Конфигурация оборудования MPIO для StorSimple tooLinux узла](./media/storsimple-configure-mpio-on-linux/MPIOHardwareConfigurationStorSimpleToLinuxHost2M.png)

Как показано в предшествующих рисунок hello:

* Устройство StorSimple имеет активно-пассивную конфигурацию с двумя контроллерами.
* Два переключателя SAN, контроллеры tooyour подключенных устройств.
* На устройстве StorSimple активировано два инициатора iSCSI.
* На узле CentOS активировано два сетевых интерфейса.

Hello выше конфигурации является 4 отдельные пути между устройством и hello узла, если интерфейсы hello узле и данных доступны для маршрутизации.

> [!IMPORTANT]
> * При реализации многоканального ввода-вывода мы рекомендуем не смешивать сетевые интерфейсы 1 GbE и 10 GbE. При использовании двух сетевых интерфейсов оба интерфейса hello должны быть идентичными типа hello.
> * На устройстве StorSimple интерфейсы DATA0, DATA1, DATA4 и DATA5 относятся к типу 1 GbE, а DATA2 и DATA3 — к типу 10 GbE.
> 
> 

## <a name="configuration-steps"></a>Этапы настройки
этапы настройки Hello несколько каналов предусматривает настройку hello доступные пути для автоматического обнаружения, указав hello балансировки нагрузки алгоритм toouse, включение несколько каналов и наконец Проверка конфигурации hello. Каждое из этих действий подробно рассматривается в следующих разделах hello.

### <a name="step-1-configure-multipathing-for-automatic-discovery"></a>Этап 1. Настройка автоматического обнаружения доступных каналов
устройства multipath поддерживается Hello можно автоматически обнаружить и настроить.

1. Инициализируйте файл `/etc/multipath.conf` . Тип:
   
     `mpathconf --enable`
   
    Hello выше команда создаст `sample/etc/multipath.conf` файл.
2. Запустите службу многоканального ввода-вывода. Тип:
   
    `service multipathd start`
   
    Вы увидите hello следующие выходные данные:
   
    `Starting multipathd daemon:`
3. Включите автоматическое обнаружение каналов ввода-вывода. Тип:
   
    `mpathconf --find_multipaths y`
   
    Это будет изменен раздел значения по умолчанию hello вашей `multipath.conf` как показано ниже:
   
        defaults {
        find_multipaths yes
        user_friendly_names yes
        path_grouping_policy multibus
        }

### <a name="step-2-configure-multipathing-for-storsimple-volumes"></a>Этап 2. Настройка многоканального ввода-вывода для томов StorSimple
По умолчанию все устройства, черный указаны в файле multipath.conf hello и не выполняется. Вам потребуется несколько toocreate черный список исключений tooallow каналов для томов из устройства StorSimple.

1. Изменить hello `/etc/mulitpath.conf` файла. Тип:
   
    `vi /etc/multipath.conf`
2. Найдите раздел blacklist_exceptions hello в файле multipath.conf hello. Устройство StorSimple требует toobe среди черный список исключений в этом разделе. Вы можете Раскомментировать, что соответствующие строки в этот файл toomodify его как показано ниже (используйте только hello конкретной модели hello устройства, который вы используете):
   
        blacklist_exceptions {
            device {
                       vendor  "MSFT"
                       product "STORSIMPLE 8100*"
            }
            device {
                       vendor  "MSFT"
                       product "STORSIMPLE 8600*"
            }
           }

### <a name="step-3-configure-round-robin-multipathing"></a>Этап 3. Настройка циклического многоканального ввода-вывода
Этот алгоритм балансировки нагрузки использует все hello доступных multipaths toohello активного контроллера в сбалансированной, циклического перебора.

1. Изменить hello `/etc/multipath.conf` файла. Тип:
   
    `vi /etc/multipath.conf`
2. В разделе hello `defaults` раздел, набор hello `path_grouping_policy` слишком`multibus`. Hello `path_grouping_policy` указывает hello группирования путь по умолчанию политика multipaths toounspecified tooapply. раздел по умолчанию Hello будет выглядеть, как показано ниже.
   
        defaults {
                user_friendly_names yes
                path_grouping_policy multibus
        }

> [!NOTE]
> Здравствуйте, наиболее часто встречающихся значений из `path_grouping_policy` включают:
> 
> * failover — один канал для каждой группы приоритетов;
> * multibus — все допустимые каналы в одной группе приоритетов.
> 
> 

### <a name="step-4-enable-multipathing"></a>Этап 4. Активация многоканального ввода-вывода
1. Перезапустите hello `multipathd` управляющей программы. Тип:
   
    `service multipathd restart`
2. Hello выходные данные будут, как показано ниже:
   
        [root@centosSS ~]# service multipathd start
        Starting multipathd daemon:  [OK]

### <a name="step-5-verify-multipathing"></a>Этап 5. Проверка работы многоканального ввода-вывода
1. Сначала убедитесь, что iSCSI соединения с устройством StorSimple hello следующим образом:
   
   а. Обнаружьте устройство StorSimple. Тип:
      
    ```
    iscsiadm -m discovery -t sendtargets -p  <IP address of network interface on hello device>:<iSCSI port on StorSimple device>
    ```
    
    Hello IP-адрес DATA0 10.126.162.25 и открыть порт 3260 на устройстве StorSimple hello для трафика iSCSI исходящих при выводится как показано ниже:
    
    ```
    10.126.162.25:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target
    10.126.162.26:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target
    ```

    Копировать hello IQN устройства StorSimple `iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target`, из hello предшествующих выходных данных.

   b. Подключиться с помощью целевой IQN устройства toohello. устройство StorSimple Hello находится здесь hello цели iSCSI. Тип:

    ```
    iscsiadm -m node --login -T <IQN of iSCSI target>
    ```

    Hello следующем примере показаны выходные данные с целевой IQN из `iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target`. выходные данные Hello указывает, успешно подключились toohello двух интерфейсов сети с поддержкой iSCSI на устройстве.

    ```
    Logging in too[iface: eth0, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.25,3260] (multiple)
    Logging in too[iface: eth1, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.25,3260] (multiple)
    Logging in too[iface: eth0, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.26,3260] (multiple)
    Logging in too[iface: eth1, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.26,3260] (multiple)
    Login too[iface: eth0, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.25,3260] successful.
    Login too[iface: eth1, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.25,3260] successful.
    Login too[iface: eth0, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.26,3260] successful.
    Login too[iface: eth1, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.26,3260] successful.
    ```

    Если вы видите только один хост-интерфейс и здесь два пути, необходимо tooenable обоих интерфейсов "hello" на узле для iSCSI. Можно выполнить hello [подробные инструкции в документации Linux](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/5/html/Online_Storage_Reconfiguration_Guide/iscsioffloadmain.html).

2. Том является сервер CentOS предоставляется toohello из устройства StorSimple hello. Дополнительные сведения см. в разделе [шаг 6: Создание тома](storsimple-deployment-walkthrough.md#step-6-create-a-volume) через hello классический портал Azure на устройстве StorSimple.

3. Проверьте hello доступные пути. Тип:

      ```
      multipath –l
      ```

      Привет, в следующем примере показаны выходные данные hello для двух сетевых интерфейсов на интерфейсе StorSimple устройство подключенных tooa один узел сети с двумя доступные пути.

        ```
        mpathb (36486fd20cc081f8dcd3fccb992d45a68) dm-3 MSFT,STORSIMPLE 8100
        size=100G features='0' hwhandler='0' wp=rw
        `-+- policy='round-robin 0' prio=0 status=active
        |- 7:0:0:1 sdc 8:32 active undef running
        `- 6:0:0:1 sdd 8:48 active undef running
        ```

        hello following example shows hello output for two network interfaces on a StorSimple device connected tootwo host network interfaces with four available paths.

        ```
        mpathb (36486fd27a23feba1b096226f11420f6b) dm-2 MSFT,STORSIMPLE 8100
        size=100G features='0' hwhandler='0' wp=rw
        `-+- policy='round-robin 0' prio=0 status=active
        |- 17:0:0:0 sdb 8:16 active undef running
        |- 15:0:0:0 sdd 8:48 active undef running
        |- 14:0:0:0 sdc 8:32 active undef running
        `- 16:0:0:0 sde 8:64 active undef running
        ```

        After hello paths are configured, refer toohello specific instructions on your host operating system (Centos 6.6) toomount and format this volume.

## <a name="troubleshoot-multipathing"></a>Устранение неполадок многоканального ввода-вывода
В этом разделе приведены некоторые полезные советы, которые помогут вам при возникновении проблем во время настройки многоканального ввода-вывода.

В. Я не вижу hello изменения в `multipath.conf` файл вступают в силу.

О. При внесении любого изменения toohello `multipath.conf` файл, необходимо будет toorestart hello несколько каналов службы. Введите следующую команду hello:

    service multipathd restart

В. Включена, две сетевые интерфейсы на устройстве StorSimple hello и двух сетевых интерфейсов на узле hello. Перечень доступных путей hello, виден только двух ветвей. Ожидалось toosee четыре доступные пути.

О. Убедитесь, что на hello hello два пути одной подсети, поддерживают маршрутизацию. Если сетевые интерфейсы hello находятся на разных виртуальных локальных сетей, не поддерживают маршрутизацию, вы увидите только двух ветвей. Одним из способов tooverify это toomake том, что можно получить доступ к оба интерфейса hello узла из сетевого интерфейса на устройстве StorSimple hello. Необходимо будет слишком[обратитесь в службу поддержки корпорации Майкрософт](storsimple-contact-microsoft-support.md) как такая проверка может выполняться только через сеанса поддержки.

В. Когда я пытаюсь вывести список доступных каналов, ничего не происходит.

О. Как правило, не отображаются все пути многопутевых предлагает проблема с управляющей программы hello несколько каналов, и это скорее всего, здесь все проблемы заключается в hello `multipath.conf` файла.

Было бы также стоит проверки, что можно увидеть некоторые диски после подключения целевой toohello как нет ответа из списков многоканального hello может также означать, что у вас нет все диски.

* Используйте следующие шины SCSI hello toorescan команда hello.
  
    `$ rescan-scsi-bus.sh `(часть пакета sg3_utils)
* Введите следующие команды hello:
  
    `$ dmesg | grep sd*`
     
     Или
  
    `$ fdisk –l`
  
    В результате будут возвращены сведения о недавно добавленных дисках.
* toodetermine ли это StorSimple диск, используйте hello, следующие команды:
  
    `cat /sys/block/<DISK>/device/model`
  
    В результате будет возвращена строка, которая определит, принадлежит ли диск устройству StorSimple.

Менее вероятной, но также возможной причиной может быть устаревший идентификатор процесса iscsid. Используйте следующую команду toolog off из сеансов iSCSI hello hello.

    iscsiadm -m node --logout -p <Target_IP>

Повторите эту команду для всех сетевых интерфейсов hello подключен на цели iSCSI hello, который является устройства StorSimple. После входа от всех сеансов iSCSI hello, используйте hello цели iSCSI IQN, tooreestablish hello сеанса iSCSI. Введите следующую команду hello:

    iscsiadm -m node --login -T <TARGET_IQN>


В. Я не уверен, включено ли мое устройство в список разрешенных устройств.

О. tooverify ли устройство не входят, используйте следующую команду по устранению неполадок интерактивных hello:

    multipathd –k
    multipathd> show devices
    available block devices:
    ram0 devnode blacklisted, unmonitored
    ram1 devnode blacklisted, unmonitored
    ram2 devnode blacklisted, unmonitored
    ram3 devnode blacklisted, unmonitored
    ram4 devnode blacklisted, unmonitored
    ram5 devnode blacklisted, unmonitored
    ram6 devnode blacklisted, unmonitored
    ram7 devnode blacklisted, unmonitored
    ram8 devnode blacklisted, unmonitored
    ram9 devnode blacklisted, unmonitored
    ram10 devnode blacklisted, unmonitored
    ram11 devnode blacklisted, unmonitored
    ram12 devnode blacklisted, unmonitored
    ram13 devnode blacklisted, unmonitored
    ram14 devnode blacklisted, unmonitored
    ram15 devnode blacklisted, unmonitored
    loop0 devnode blacklisted, unmonitored
    loop1 devnode blacklisted, unmonitored
    loop2 devnode blacklisted, unmonitored
    loop3 devnode blacklisted, unmonitored
    loop4 devnode blacklisted, unmonitored
    loop5 devnode blacklisted, unmonitored
    loop6 devnode blacklisted, unmonitored
    loop7 devnode blacklisted, unmonitored
    sr0 devnode blacklisted, unmonitored
    sda devnode whitelisted, monitored
    dm-0 devnode blacklisted, unmonitored
    dm-1 devnode blacklisted, unmonitored
    dm-2 devnode blacklisted, unmonitored
    sdb devnode whitelisted, monitored
    sdc devnode whitelisted, monitored
    dm-3 devnode blacklisted, unmonitored


Дополнительные сведения см. слишком[воспользуйтесь неполадок интерактивную команду для несколько каналов](http://www.centos.org/docs/5/html/5.1/DM_Multipath/multipath_config_confirm.html).

## <a name="list-of-useful-commands"></a>Список полезных команд
| При появлении запроса на подтверждение нажмите клавишу  | Команда | Описание |
| --- | --- | --- |
| **iSCSI** |`service iscsid start` |Запуск службы iSCSI |
| &nbsp; |`service iscsid stop` |Остановка службы iSCSI |
| &nbsp; |`service iscsid restart` |Перезапуск службы iSCSI |
| &nbsp; |`iscsiadm -m discovery -t sendtargets -p <TARGET_IP>` |Обнаружение доступных целевых объектов на hello указан адрес |
| &nbsp; |`iscsiadm -m node --login -T <TARGET_IQN>` |Войдите в toohello цели iSCSI |
| &nbsp; |`iscsiadm -m node --logout -p <Target_IP>` |Выйдите из цели iSCSI hello |
| &nbsp; |`cat /etc/iscsi/initiatorname.iscsi` |Вывод имени инициатора iSCSI |
| &nbsp; |`iscsiadm –m session –s <sessionid> -P 3` |Проверьте состояние hello сеанса iSCSI hello и тома, обнаруженные на узле hello |
| &nbsp; |`iscsi –m session` |Показывает все сеансы iSCSI hello, установленных между hello узле и устройстве StorSimple hello |
|  | | |
| **Поддержка нескольких каналов ввода-вывода** |`service multipathd start` |Запуск управляющей программы многоканального ввода-вывода |
| &nbsp; |`service multipathd stop` |Остановка управляющей программы многоканального ввода-вывода |
| &nbsp; |`service multipathd restart` |Перезапуск управляющей программы многоканального ввода-вывода |
| &nbsp; |`chkconfig multipathd on` </br> ИЛИ </br> `mpathconf –with_chkconfig y` |Включить toostart многоканального управляющей программы во время загрузки |
| &nbsp; |`multipathd –k` |Запуск интерактивной консоли hello для устранения неполадок |
| &nbsp; |`multipath –l` |Вывод списка подключений и устройств с многоканальным вводом-выводом |
| &nbsp; |`mpathconf --enable` |Создание примера файла mulitpath.conf в `/etc/mulitpath.conf` |
|  | | |

## <a name="next-steps"></a>Дальнейшие действия
При настройке MPIO на узле Linux, может также потребоваться следующие документы CentoS 6.6 toohello toorefer:

* [Настройка MPIO на CentOS](http://www.centos.org/docs/5/html/5.1/DM_Multipath/setup_procedure.html)
* [Учебное руководство Linux](http://linux-training.be/files/books/LinuxAdm.pdf)

