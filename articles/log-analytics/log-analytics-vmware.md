---
title: "aaaVMware решений мониторинга в службе анализа журналов | Документы Microsoft"
description: "Узнайте, как hello решения отслеживания VMware помогают управлять журналами и отслеживать узлах ESXi."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: 16516639-cc1e-465c-a22f-022f3be297f1
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: banders
ms.openlocfilehash: 959d5c2201fc5c7947f8b8870d055cdf9eea8e01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="vmware-monitoring-preview-solution-in-log-analytics"></a>Решение для мониторинга VMware (предварительная версия) в Log Analytics | Microsoft Azure

![Символ VMware](./media/log-analytics-vmware/vmware-symbol.png)

Hello решение для наблюдения за VMware в службе анализа журналов — это решение, поможет вам создать централизованное ведение журналов и подход к наблюдению для больших журналов VMware. В этой статье описывается, как устранение неполадок, отслеживания и управления узлами ESXi hello в одном месте с помощью решения hello. Решение для hello вы увидите подробные данные для всех своих узлах ESXi в одном месте. Вы увидите счетчики событий top, состоянии и тенденциях виртуальной Машины и ESXi узлов, предоставленные с помощью журналов узла ESXi hello. Вы также можете устранять неполадки, просматривая централизованные журналы узлов ESXi и выполняя поиск в них. И наоборот, можно создавать оповещения на основе поисковых запросов по журналам.

Hello решение использует функциональные возможности собственного syslog hello ESXi узла toopush tooa целевой объект данных виртуальную Машину, которая имеет агента OMS. Однако решение hello не записи файлов в системный журнал в пределах целевого hello виртуальной Машины. агент OMS Hello открывает порт 1514 и прослушивает toothis. При получении данных hello, hello агента OMS передает данные hello в OMS.

## <a name="installing-and-configuring-hello-solution"></a>Установка и настройка решения hello
Используйте следующие сведения tooinstall hello и настроить решение hello.

* Добавить tooyour мониторинг VMware решения hello, рабочую область OMS hello процесс описывается в [решений добавьте анализа журналов из коллекции решений hello](log-analytics-add-solutions.md).

#### <a name="supported-vmware-esxi-hosts"></a>Поддерживаемые узлы VMware ESXi
vSphere ESXi Host версий 5.5 и 6.0.

#### <a name="prepare-a-linux-server"></a>Подготовка сервера под управлением Linux
Создайте все данные системного журнала Linux операционной системы виртуальной Машины tooreceive из узлах ESXi hello. Hello [агента OMS для Linux](log-analytics-linux-agents.md) точка hello коллекции для всех данных системного журнала узла ESXi. Можно использовать несколько ESXi узлов tooforward журналы tooa Linux односерверной, как следующий пример hello.  

   ![Поток данных системных журналов](./media/log-analytics-vmware/diagram.png)

### <a name="configure-syslog-collection"></a>Настройка сбора системных журналов
1. Настройте пересылку системных журналов для VSphere. Подробные сведения toohelp настроить перенаправление системного журнала, в разделе [настройке syslog в ESXi 5.x и 6.0 (2003322)](https://kb.vmware.com/selfservice/microsites/search.do?language=en_US&cmd=displayKC&externalId=2003322). Go слишком**конфигурации узла ESXi** > **программного обеспечения** > **Дополнительные параметры** > **Syslog**.
   ![vsphereconfig](./media/log-analytics-vmware/vsphere1.png)  
2. В hello *Syslog.global.logHost* поля, добавьте номер порта сервера и hello вашей Linux *1514*. Например, `tcp://hostname:1514` или `tcp://123.456.789.101:1514`.
3. Откройте брандмауэр узла ESXi hello для системного журнала. Последовательно выберите **ESXi Host Configuration** > **Software** > **Security Profile** > **Firewall** и **Properties** (Конфигурация узла ESXi > Программное обеспечение > Профиль безопасности > Брандмауэр > Свойства).  

    ![vspherefw](./media/log-analytics-vmware/vsphere2.png)  

    ![vspherefwproperties](./media/log-analytics-vmware/vsphere3.png)  
4. Проверьте tooverify консоли vSphere hello, что syslog правильно настроены. Подтвердите в hello ESXI узел, порт **1514** настроен.
5. Загрузите и установите hello агента OMS для Linux на сервере Linux hello. Дополнительные сведения см. в разделе hello [документации для агента OMS для Linux](https://github.com/Microsoft/OMS-Agent-for-Linux).
6. После установки агента OMS для Linux hello go toohello /etc/opt/microsoft/omsagent/sysconf/omsagent.d и копирования hello vmware_esxi.conf файл toohello /etc/opt/microsoft/omsagent/conf/omsagent.d каталогов и hello hello изменения владельца или группы и разрешения файла hello. Например:

    ```
    sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.d/vmware_esxi.conf /etc/opt/microsoft/omsagent/conf/omsagent.d
   sudo chown omsagent:omiusers /etc/opt/microsoft/omsagent/conf/omsagent.d/vmware_esxi.conf
    ```
7. Перезапустите hello агента OMS для Linux с помощью `sudo /opt/microsoft/omsagent/bin/service_control restart`.
8. Проверить hello подключение между сервером Linux hello и узел ESXi hello с помощью hello `nc` на узел ESXi hello. Например:

    ```
    [root@ESXiHost:~] nc -z 123.456.789.101 1514
    Connection too123.456.789.101 1514 port [tcp/*] succeeded!
    ```

9. В hello портал OMS, выполняют поиск журнала `Type=VMware_CL`. Если OMS собирает данные системного журнала hello, она сохраняет формат syslog hello. На портале hello захватываются некоторые определенные поля, такие как *Hostname* и *ProcessName*.  

    ![type](./media/log-analytics-vmware/type.png)  

    Представление результаты поиска, аналогичные выше рисунке toohello настроек мониторинга OMS VMware мониторинга решения toouse hello.  

## <a name="vmware-data-collection-details"></a>Сведения о сборе данных VMware
Hello решения отслеживания VMware сбор данных метрики и журнала для различных производительности узлах ESXi, с помощью hello агенты OMS для Linux, включен.

Hello следующей таблице приведены методы сбора данных и другие сведения о сборе данных.

| платформа | Агент OMS для Linux | Агент SCOM | Хранилище Azure | Нужен ли SCOM? | Отправка данных агента SCOM через группу управления | частота сбора |
| --- | --- | --- | --- | --- | --- | --- |
| Linux |&#8226; |  |  |  |  |Каждые 3 минуты |

Привет, в следующей таблице содержатся примеры полей данных, собираемых hello решения отслеживания VMware.

| Имя поля | Описание |
| --- | --- |
| Device_s |Запоминающие устройства VMware |
| ESXIFailure_s |Типы сбоев |
| EventTime_t |Время возникновения события |
| HostName_s |Имя узла ESXi |
| Operation_s |Создание или удаление ВМ |
| ProcessName_s |Имя события |
| ResourceId_s |Имя узла VMware hello |
| ResourceLocation_s |VMware |
| ResourceName_s |VMware |
| ResourceType_s |Hyper-V. |
| SCSIStatus_s |Состояние VMware SCSI |
| SyslogMessage_s |Данные системного журнала |
| UserName_s |Пользователь, создавший или удаливший ВМ |
| VMName_s |имя виртуальной машины; |
| Компьютер |Главный компьютер |
| TimeGenerated |были созданы данные hello времени |
| DataCenter_s |Центр обработки данных VMware |
| StorageLatency_s |Задержка хранилища (мс) |

## <a name="vmware-monitoring-solution-overview"></a>Обзор решения для мониторинга VMware
Hello VMware отображается на портале OMS hello. Решение отображает обобщенное представление ошибок. При выборе плитки приветствия, чем перейти в представление панели мониторинга.

![Плитка](./media/log-analytics-vmware/tile.png)

#### <a name="navigate-hello-dashboard-view"></a>Перейдите в представление панели мониторинга hello
В hello **VMware** представление панели мониторинга колонках упорядочены по:

* число состояний сбоя;
* основной узел по счетчикам событий;
* счетчики основных событий;
* действия виртуальной машины;
* события диска узла ESXi.

![Решение 1](./media/log-analytics-vmware/solutionview1-1.png)

![Решение 2](./media/log-analytics-vmware/solutionview1-2.png)

Щелкните любой колонке tooopen панель поиска аналитики журналов, содержатся подробные сведения для hello колонку.

Здесь можно изменить запрос toomodify hello поиска для определенного. Учебник по hello основы поиска OMS, извлечь hello [учебника поиска журналов OMS.](log-analytics-log-searches.md)

#### <a name="find-esxi-host-events"></a>Поиск событий узлов ESXi
Для одного узла ESXi создается несколько журналов на основе выполняющихся процессов. Hello решения отслеживания VMware централизует их, а также указано hello счетчиков событий. Это централизованное представление помогает понять, на каком узле ESXi происходит больше всего событий и какие именно события происходят в вашей среде чаще всего.

![event](./media/log-analytics-vmware/events.png)

Чтобы просмотреть дополнительные сведения, щелкните узел ESXi или тип события.

Щелкнув имя узла ESXi, вы сможете просмотреть сведения, связанные с этим узлом ESXi. Если вы хотите toonarrow результатов с типом события hello, добавьте `“ProcessName_s=EVENT TYPE”` в запросе поиска. Можно выбрать **ProcessName** в фильтре поиска hello. Ограничивающего hello сведения для вас.

![Детализация](./media/log-analytics-vmware/eventhostdrilldown.png)

#### <a name="find-high-vm-activities"></a>Поиск активных действий ВМ
Виртуальные машины могут создаваться и удаляться на любом узле ESXi. Это полезно для tooidentify администратор создает узел ESXi сколько виртуальных машин. В свою очередь, помогает toounderstand производительности и планирования производительности. При управлении средой очень важно отслеживать события действий ВМ.

![Детализация](./media/log-analytics-vmware/vmactivities1.png)

Если требуется дополнительный узел ESXi toosee данные для создания виртуальной Машины, щелкните имя узла ESXi.

![Детализация](./media/log-analytics-vmware/createvm.png)

#### <a name="common-search-queries"></a>Распространенные поисковые запросы
Hello решение включает в себя другие полезные запросы, которые помогут вам управлять узлах ESXi высокой дисковое пространство, памятью и обработка отказов пути.

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

![Запросы](./media/log-analytics-vmware/queries.png)


#### <a name="save-queries"></a>Сохранение запросов
Сохранение запросов поиска — это стандартная функция OMS, которая помогает сохранять запросы, которые оказались полезными для вас. После создания запроса, который вам пригодиться, сохраните его, выбрав hello **Избранное**. Сохраненный запрос позволяет легко использовать его повторно с hello [Моя панель мониторинга](log-analytics-dashboards.md) страницы, где можно создать собственные настраиваемые панели мониторинга.

![DockerDashboardView](./media/log-analytics-vmware/dockerdashboardview.png)

#### <a name="create-alerts-from-queries"></a>Создание оповещений из запросов
После создания запросов, может потребоваться tooalert запросы hello toouse вы когда происходят определенные события. В разделе [предупреждения в службе анализа журналов](log-analytics-alerts.md) сведения о том, как toocreate предупреждения. Примеры предупреждений запросов и другие примеры запросов см. в разделе hello [монитор VMware с помощью аналитики журналов OMS](https://blogs.technet.microsoft.com/msoms/2016/06/15/monitor-vmware-using-oms-log-analytics) записи блога.

## <a name="frequently-asked-questions"></a>Часто задаваемые вопросы
### <a name="what-do-i-need-toodo-on-hello-esxi-host-setting-what-impact-will-it-have-on-my-current-environment"></a>Что нужно сделать toodo на параметр узла ESXi hello? Какое влияние это окажет на мою текущую среду?
Hello решение использует hello собственного Syslog узла ESXi пересылки механизм. Не требуется никаких дополнительных программ Microsoft hello узел ESXi toocapture hello журналов. Возможно только в существующей среде tooyour слабо влияет. Однако следует соблюдать tooset syslog отправку ESXI функциональность.

### <a name="do-i-need-toorestart-my-esxi-host"></a>Зачем мне toorestart Мой узел ESXi?
Нет. Для этого процесса перезапуск не требуется. В некоторых случаях vSphere не обновляется должным образом hello syslog. В таком случае вход узла ESXi toohello и перезагрузить hello syslog. Опять же у вас нет узла toorestart hello, поэтому этот процесс не нарушают работу tooyour среды.

### <a name="can-i-increase-or-decrease-hello-volume-of-log-data-sent-toooms"></a>Можно увеличить или уменьшить hello объем данных журнала, отправленных tooOMS?
Да, можно. Можно использовать параметры уровень ведения журнала узла ESXi hello в vSphere. Сбор журналов зависит от hello *сведения* уровне. Таким образом, если требуется создание виртуальной Машины tooaudit или удаления, необходимо tookeep hello *сведения* уровня на Hostd. Дополнительные сведения см. в разделе hello [VMware базы знаний](https://kb.vmware.com/selfservice/microsites/search.do?&cmd=displayKC&externalId=1017658).

### <a name="why-is-hostd-not-providing-data-toooms-my-log-setting-is-set-tooinfo"></a>Почему Hostd не обеспечивает tooOMS данных? Мои журнала установлено tooinfo.
Произошла ошибка узла ESXi для отметки времени syslog hello. Дополнительные сведения см. в разделе hello [VMware базы знаний](https://kb.vmware.com/selfservice/microsites/search.do?language=en_US&cmd=displayKC&externalId=2111202). После применения метода hello, Hostd должны работать нормально.

### <a name="can-i-have-multiple-esxi-hosts-forwarding-syslog-data-tooa-single-vm-with-omsagent"></a>Можно ли использовать несколько ESXi узлов пересылки данных tooa syslog одной виртуальной Машины с omsagent?
Да. У вас есть несколько ESXi узлов пересылки tooa одной виртуальной Машины с omsagent.

### <a name="why-dont-i-see-data-flowing-into-oms"></a>Почему не отображается поступление данных в OMS?
Это может быть вызвано несколькими причинами.

* узел ESXi Hello не является правильно нажать omsagent работающей виртуальной Машины toohello данных. tootest, выполните следующие шаги hello:

  1. tooconfirm, войдите в узел ESXi toohello с помощью ssh и запустите hello следующую команду:`nc -z ipaddressofVM 1514`

      Если это не удалось, параметры vSphere в hello Расширенная настройка, вероятно, являются неправильно. В разделе [настройки сбора данных системного журнала](#configure-syslog-collection) сведения о как tooset копирование hello ESXi размещения для пересылки системного журнала.
  2. Если подключение к порту syslog прошла успешно, но данные не отображаются, перезагрузите syslog hello в узел ESXi hello с помощью ssh hello toorun следующую команду:` esxcli system syslog reload`
* неверно задан Hello виртуальной Машины с агентом OMS. tootest это, выполните следующие шаги hello:

  1. OMS прослушивает порт toohello 1514 и отправляет данные в OMS. tooverify, что он открыт, выполните следующую команду hello.`netstat -a | grep 1514`
  2. Вы увидите, что порт `1514/tcp` открыт. Если этого не сделать, убедитесь, что правильно установлен, omsagent hello. Если сведения о порте hello не отображается, порт syslog hello не открыт на hello виртуальной Машины.

     1. Убедитесь, что hello агент OMS выполняется с помощью `ps -ef | grep oms`. Если она не запущена, запустите процесс hello, выполнив команду hello` sudo /opt/microsoft/omsagent/bin/service_control start`
     2. Откройте hello `/etc/opt/microsoft/omsagent/conf/omsagent.d/vmware_esxi.conf` файла.

         Убедитесь, что пользователь правильную hello и параметра групповой допустимым, как:`-rw-r--r-- 1 omsagent omiusers 677 Sep 20 16:46 vmware_esxi.conf`

         Если hello файл не существует, или hello пользователя и установлена неверная настройка группы, предпринять корректирующие действия по [Подготовка сервера Linux](#prepare-a-linux-server).

## <a name="next-steps"></a>Дальнейшие действия
* Используйте [запросов поиска журналов](log-analytics-log-searches.md) в службе анализа журналов tooview подробные данные узла VMware.
* [Создавайте собственные панели мониторинга](log-analytics-dashboards.md), отображающие данные об узле VMware.
* [Создавайте оповещения](log-analytics-alerts.md), информирующие о возникновении определенных событий узла VMware.
