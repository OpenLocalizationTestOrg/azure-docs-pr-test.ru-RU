---
redirect_url: /azure/log-analytics/log-analytics-agent-linux
redirect_document_id: True
ROBOTS: NOINDEX
ms.openlocfilehash: 8b526144cd565f6750368e12970f008e66cc2023
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-linux-computers-toolog-analytics"></a>Подключение к tooLog компьютеров Linux аналитика
Log Analytics позволяет собирать и обрабатывать данные, созданные компьютерами Linux. Добавление данных, собранных из Linux tooOMS позволяет toomanage системами и контейнерными решениями, такими как Docker, независимо от того, где находятся компьютеры, — практически везде. Источники данных могут находятся в центре обработки данных в локальной как физические серверы, виртуальные компьютеры в службе, размещенной в облаке, например Amazon Web Services (AWS) или Microsoft Azure, или даже hello портативный компьютер в службу поддержки. Кроме того, OMS аналогичным образом собирает данные с компьютеров Windows. Так что это решение поддерживает гибридную ИТ-среду.

С помощью Log Analytics в OMS можно просматривать данные из всех этих источников и управлять ими на едином портале управления. Это уменьшает необходимость hello toomonitor его с помощью различных систем, позволяет легко tooconsume и позволяет экспортировать любые данные, например toowhatever бизнес-аналитика решения или системы, у вас уже есть.

Эта статья содержит краткое руководство, которое поможет сбора и управления данными для компьютеров Linux с помощью hello агента OMS для Linux. Дополнительные технические сведения, такие как конфигурация прокси-сервера, сведения о метриках CollectD и пользовательских источниках данных JSON, см. в [обзоре агента OMS для Linux](https://github.com/Microsoft/OMS-Agent-for-Linux) и [полной документации по агенту OMS для Linux](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md) на сайте GitHub.

В настоящее время можно собирать следующие типы данных с компьютеров Linux hello:

* Метрики производительности
* события системного журнала;
* оповещения Nagios и Zabbix;
* метрики производительности, данные инвентаризации и журналов контейнера Docker.

## <a name="supported-linux-versions"></a>Поддерживаемые версии Linux
x86 и x64 являются официально поддерживаемыми версиями в различных дистрибутивах Linux. Однако hello агента OMS для Linux также можно запустить на других дистрибутивах, которых нет в списке.

* выпуски Amazon Linux 2012.09–2015.09;
* CentOS Linux 5, 6 и 7;
* Oracle Linux 5, 6 и 7;
* сервер Red Hat Enterprise Linux 5, 6 и 7;
* Debian GNU/Linux 6, 7 и 8;
* Ubuntu 12.04 LTS, 14.04 LTS, 15.04, 15.10;
* SUSE Linux Enterprise Server 11 и 12.

## <a name="oms-agent-for-linux"></a>Агент OMS для Linux
Hello агент Operations Management Suite для Linux состоит из нескольких пакетов. Hello файл версии содержит следующие пакеты, работающей hello оболочку пакета с hello `--extract`.

| **Package** | **Версия** | **Описание** |
| --- | --- | --- |
| omsagent |1.1.0 |Hello агент Operations Management Suite для Linux |
| omsconfig |1.1.1 |Агент конфигурации для агента OMS hello |
| omi |1.0.8.3 |OMI (Open Management Infrastructure) — упрощенная версия сервера CIM |
| scx |1.6.2 |Поставщики OMI CIM для метрик производительности операционной системы |
| apache-cimprov |1.0.0 |Поставщик мониторинга производительности сервера Apache HTTP Server для OMI. Устанавливается только при обнаружении сервера Apache HTTP Server |
| mysql-cimprov |1.0.0 |Поставщик мониторинга производительности сервера MySQL для OMI. Устанавливается только при обнаружении сервера MySQL или MariaDB |
| docker-cimprov |0.1.0 |Поставщик Docker для OMI. Устанавливается только при обнаружении Docker |

### <a name="additional-installation-artifacts"></a>Дополнительные артефакты установки
После установки агента OMS hello для пакетов Linux, hello следующие дополнительные системные применяются изменения конфигурации. Эти артефакты удаляются при удалении пакета omsagent hello.

* Создается непривилегированный пользователь с именем `omsagent` . Это hello hello omsagent управляющая программа выполняется как
* Создается файл «include» sudoers в /etc/sudoers.d/omsagent это разрешает omsagent toorestart hello syslog и omsagent управляющие программы. Если директивы «include» sudo не поддерживаются в версии hello установки sudo, эти операции будут записаны слишком/д/sudoers.
* Конфигурация syslog Hello — измененные tooforward подмножество событий toohello агента. Дополнительные сведения см. в разделе hello **Настройка сбора данных** ниже

### <a name="linux-data-collection-details"></a>Сведения о сборе данных Linux
Hello следующей таблице приведены методы сбора данных и другие сведения о сборе данных.

| источник | Direct Agent | Агент SCOM | Хранилище Azure | Нужен ли SCOM? | Отправка данных агента SCOM через группу управления | Частота сбора |
| --- | --- | --- | --- | --- | --- | --- |
| Zabbix |![Да](./media/log-analytics-linux-agents/oms-bullet-green.png) |![Нет](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Нет](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Нет](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Нет](./media/log-analytics-linux-agents/oms-bullet-red.png) |1 минута |
| Nagios |![Да](./media/log-analytics-linux-agents/oms-bullet-green.png) |![Нет](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Нет](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Нет](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Нет](./media/log-analytics-linux-agents/oms-bullet-red.png) |При получении |
| syslog |![Да](./media/log-analytics-linux-agents/oms-bullet-green.png) |![Нет](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Нет](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Нет](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Нет](./media/log-analytics-linux-agents/oms-bullet-red.png) |Из хранилища Azure — 10 минут, из агента — при получении |
| Счетчики производительности Linux |![Да](./media/log-analytics-linux-agents/oms-bullet-green.png) |![Нет](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Нет](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Нет](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Нет](./media/log-analytics-linux-agents/oms-bullet-red.png) |По расписанию, не менее 10 секунд |
| Отслеживание изменений |![Да](./media/log-analytics-linux-agents/oms-bullet-green.png) |![Нет](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Нет](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Нет](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Нет](./media/log-analytics-linux-agents/oms-bullet-red.png) |Ежечасно |

### <a name="package-requirements"></a>Требования к пакетам
| **Требуемый пакет** | **Описание** | **Минимальная версия** |
| --- | --- | --- |
| Glibc |Библиотека C GNU |2.5-12 |
| Openssl |Библиотеки OpenSSL |0.9.8e или 1.0 |
| Curl |Веб-клиент cURL |7.15.5 |
| Python-ctypes |Библиотеки функций |Недоступно |
| PAM |Подключаемые модули аутентификации |Недоступно |

> [!NOTE]
> Rsyslog или syslog-ng, требуется toocollect syslog-сообщения. управляющая программа syslog по умолчанию Hello в версии 5 Red Hat Enterprise Linux, CentOS и Oracle Linux (sysklog) версии не поддерживается для сбора событий syslog. toocollect данных syslog из этой версии данных дистрибутивов hello rsyslog управляющая программа должна быть установлена и настроена tooreplace sysklog.
>
>

## <a name="quick-install"></a>Быстрая установка
Запустите следующие команды toodownload hello omsagent hello, проверки контрольной суммы hello, а затем Установка и встроенного hello агента. Команды предназначены для 64-разрядных систем. Hello идентификатор рабочей области и первичный ключ можно найти на портале OMS hello под **параметры** на hello **подключенные источники** вкладки.

![сведения о рабочей области](./media/log-analytics-linux-agents/oms-direct-agent-primary-key.png)

```
wget https://raw.githubusercontent.com/Microsoft/OMS-Agent-for-Linux/master/installer/scripts/onboard_agent.sh && sh onboard_agent.sh -w <YOUR OMS WORKSPACE ID> -s <YOUR OMS WORKSPACE PRIMARY KEY>
```

Существует множество других методов tooinstall hello агента и его обновления. Вы можете прочитать больше о них на [hello tooinstall действия агента OMS для Linux](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#steps-to-install-the-oms-agent-for-linux).

Вы также можете просмотреть hello [Azure видеоруководство](https://www.youtube.com/watch?v=mF1wtHPEzT0).

## <a name="choose-your-linux-data-collection-method"></a>Выбор метода сбора данных Linux
Выбор hello типов данных, которые бы как toocollect зависит от того, нужно ли портал OMS toouse hello, или если необходимо изменение различных конфигурационных файлов непосредственно на клиентах Linux. При выборе toouse hello портала конфигурации hello автоматически отправляется tooall клиентские компьютеры Linux. Если необходимы различные конфигурации для разных клиентов Linux будет необходима tooedit клиентских файлов по отдельности или использовать альтернативу, например PowerShell DSC, Chef или Puppet.

Можно указать события syslog hello и счетчики производительности, которые должны toocollect с помощью файлов конфигурации на компьютерах Linux hello. *Если выбрана tooconfigure сбора данных путем изменения файлов конфигурации агента, следует отключить централизованную конфигурацию hello.*  Инструкции приведены ниже tooconfigure сбора данных в агент hello файлы конфигурации, а также toodisable централизованной конфигурации для всех агентов OMS для Linux или отдельных компьютеров.

### <a name="disable-oms-management-for-an-individual-linux-computer"></a>Отключение управления OMS для отдельного компьютера Linux
Централизованный сбор данных для данных конфигурации для отдельного компьютера Linux с помощью сценария OMS_MetaConfigHelper.py hello будет отключена. Это может быть полезно, если подмножеству компьютеров требуется специальная конфигурация.

toodisable централизованной конфигурации:

```
sudo /opt/microsoft/omsconfig/Scripts/OMS_MetaConfigHelper.py --disable
```

toore Включение централизованной конфигурации:

```
sudo /opt/microsoft/omsconfig/Scripts/OMS_MetaConfigHelper.py –enable
```

## <a name="linux-performance-counters"></a>Счетчики производительности Linux
Счетчики производительности Linux, похожие счетчики производительности tooWindows — оба работают одинаково. Можно использовать следующие процедуры tooadd hello и их настройки. После добавления tooOMS, данные собираются для них каждые 30 секунд.

### <a name="tooadd-a-linux-performance-counter-in-oms"></a>tooadd счетчика производительности Linux в OMS
1. tooconfigure агенты OMS для Linux с помощью портала OMS hello, добавьте счетчики производительности Linux на странице "Параметры" hello щелкните **данные**.  
2. На hello **параметры** в разделе **данные** , нажмите кнопку **счетчики производительности Linux** и затем выберите или введите имя hello hello счетчика требуется tooadd.  
    ![Данные](./media/log-analytics-linux-agents/oms-settings-data01.png)
3. Если вы не знаете полное имя счетчика hello hello, можно начать вводить часть имени, и появится список доступных счетчиков. Когда счетчик hello вы tooadd, выберите имя hello hello списка и нажмите кнопку hello, а также значок tooadd hello счетчика.
4. После добавления счетчиков hello, он отображается в списке hello счетчиков и будет выделен цветной линией.
5. По умолчанию hello **применить указанную ниже конфигурацию toomy машины** выбран параметр. Toodisable отправку данных конфигурации, снимите выделение hello.
6. Закончив изменение счетчиков производительности, hello нижней части страницы приветствия щелкните **Сохранить** toofinalize изменения. изменения конфигурации Hello внесенные отправляются hello tooall агенты OMS для Linux, которые зарегистрированы в OMS, обычно это занимает 5 минут.

### <a name="configure-linux-performance-counters-in-oms"></a>Настройка счетчиков производительности Linux в OMS
Для каждого счетчика производительности Windows можно выбрать конкретный экземпляр. Однако любой экземпляр счетчика, выбранный для счетчиков производительности Linux, применяется tooall дочерним счетчикам родительского счетчика hello. Hello следующей таблице показаны распространенные экземпляров hello tooboth доступные счетчики производительности Linux и Windows.

| **Имя экземпляра** | **Значение** |
| --- | --- |
| \_Total |Общее количество всех экземпляров hello |
| \* |Все экземпляры |
| (/&#124;/var) |Сопоставление экземпляров с именем / или/var |

Аналогичным образом hello интервал выборки, выбранный для родительского счетчика, применяется tooall его дочерним счетчикам. Другими словами интервалы выборки счетчика дочерних hello и экземпляры всех связаны друг с другом.

### <a name="add-and-configure-performance-metrics-with-linux"></a>Добавление и настройка метрик производительности в Linux
Toocollect метрики производительности определяются hello конфигурации в каталоге/и т. д/opt/microsoft/omsagent/&lt;идентификатор рабочей области&gt;/conf/omsagent.conf. В разделе [доступные метрики производительности](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#appendix-available-performance-metrics) доступные классы и метрики для агента OMS для Linux hello.

Каждый объект или категория toocollect метрик производительности должен быть определен в файле конфигурации hello как один `<source>` элемента. следующий синтаксис Hello hello шаблону ниже.

```
<source>
  type oms_omi  
  object_name "Processor"
  instance_regex ".*"
  counter_name_regex ".*"
  interval 30s
</source>

```

используются следующие настраиваемые параметры Hello этого элемента:

* **Объект\_имя**: hello имя объекта для коллекции hello.
* **Экземпляр\_regex**: *регулярное выражение* определение какие toocollect экземпляров. Здравствуйте, значение: `.*` указывает все экземпляры. toocollect метрик процессора только hello \_общий экземпляр можно указать `_Total`. только toocollect метрик процесса для hello экземпляров crond или sshd, можно указать: `(crond|sshd)`.
* **Счетчик\_имя\_regex**: *регулярное выражение* определение toocollect какие счетчики (hello объекта). Укажите все счетчики объекта hello toocollect: `.*`. toocollect только данные счетчиков пространства подкачки hello объекта памяти, можно указать:`.+Swap.+`
* **Интервал:**: hello частоту, с которой hello собираются данные счетчиков объекта.

— Конфигурация по умолчанию Hello для метрики производительности:

```
<source>
  type oms_omi
  object_name "Physical Disk"
  instance_regex ".*"
  counter_name_regex ".*"
  interval 5m
</source>

<source>
  type oms_omi
  object_name "Logical Disk"
  instance_regex ".*
  counter_name_regex ".*"
  interval 5m
</source>

<source>
  type oms_omi
  object_name "Processor"
  instance_regex ".*
  counter_name_regex ".*"
  interval 30s
</source>

<source>
  type oms_omi
  object_name "Memory"
  instance_regex ".*"
  counter_name_regex ".*"
  interval 30s
</source>

```

### <a name="enable-mysql-performance-counters-using-linux-commands"></a>Включение счетчиков производительности MySQL с помощью команд Linux
Если сервер MySQL или MariaDB Server обнаруживается hello компьютера при установке пакета omsagent hello, поставщик для сервера MySQL наблюдения за производительностью автоматически устанавливается. Этот поставщик подключается toohello локального MySQL или MariaDB tooexpose статистики производительности сервера. Необходимо tooconfigure учетные данные пользователя MySQL hello поставщик можно получить доступ к MySQL Server hello.

toodefine пользователя по умолчанию учетная запись для hello MySQL server в localhost, hello используйте следующий пример команды.

> [!NOTE]
> Hello учетных данных файл должен быть доступен для чтения для учетной записи omsagent hello. Выполнение hello выполнить команду mycimprovauth от имени omsgent рекомендуется.
>
>

```
sudo su omsagent -c '/opt/microsoft/mysql-cimprov/bin/mycimprovauth default 127.0.0.1 <username> <password>

sudo /opt/omi/bin/service_control restart
```


Кроме того, можно указать hello необходимые учетные данные MySQL в файле, создав файл hello: /var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth. Дополнительные сведения об управлении учетными данными MySQL для отслеживания с помощью файла mysql-auth hello см. в разделе [мониторинга учетные данные в файле проверки подлинности hello управление MySQL](#manage-mysql-monitoring-credentials-in-the-authentication-file).

В разделе [базы данных разрешения, необходимые для счетчиков производительности MySQL](#database-permissions-required-for-mysql-performance-counters) подробные сведения о разрешениях объекта, предусмотренного toocollect пользователя MySQL hello данных производительности MySQL Server.

### <a name="enable-apache-http-server-performance-counters-using-linux-commands"></a>Включение счетчиков производительности сервера Apache HTTP Server с помощью команд Linux
Если при установке пакета omsagent hello на компьютере hello обнаружен HTTP-сервера Apache, автоматически устанавливается поставщик для HTTP-сервера Apache наблюдения за производительностью. Этот поставщик использует «модуль», должны быть загружены в hello HTTP-сервера Apache в данные производительности о заказах tooaccess Apache.

Можно загрузить модуль hello с hello следующую команду:

```
sudo /opt/microsoft/apache-cimprov/bin/apache_config.sh -c
```

toounload hello Apache модуль мониторинга, запустите hello следующую команду:

```
sudo /opt/microsoft/apache-cimprov/bin/apache_config.sh -u
```
### <a name="tooview-performance-data-with-log-analytics"></a>tooview данные о производительности с помощью аналитики журналов
1. На портале Operations Management Suite hello щелкните плитку hello поиска журналов.
2. Введите в строке поиска hello `* (Type=Perf)` tooview всех счетчиков производительности.

Поскольку OMS также собирает данные счетчика производительности Windows, вы должны ограничить hello tooLinux данных поиска. Таким образом hello примере будут отображаться производительности данных конкретного tooan сервера Linux с именем Chorizo21.

```
Type=Perf Computer=chorizo*
```

![пример сервера, отображающийся на странице результатов поиска](./media/log-analytics-linux-agents/oms-perfsearch01.png)

В результатах hello, можно щелкнуть **метрики** tooview hello счетчики, которые были собраны данные. Данные в реальном времени отображаются в виде графиков для каждого счетчика.

![Метрики](./media/log-analytics-linux-agents/oms-perfmetrics01.png)

## <a name="syslog"></a>syslog
Syslog — это событие, ведение журнала протокола аналогичные tooWindows журналы событий — оба работают одинаково в OMS.

### <a name="tooadd-a-new-linux-syslog-facility-in-oms"></a>tooadd нового средства syslog Linux в OMS
1. На hello **параметры** в разделе **данные** , нажмите кнопку **Syslog** и toohello слева hello и значок, введите имя средства syslog hello, которое следует tooadd hello.
    ![Системный журнал Linux](./media/log-analytics-linux-agents/oms-linuxsyslog01.png)
2. Если вы не знаете полное имя hello hello подсистемы, можно начать вводить часть имени, и появится список доступных средств syslog. При обнаружении hello средства syslog, что вы tooadd, выберите имя hello hello списка и нажмите кнопку hello, а также значок tooadd hello средства syslog.
3. После добавления hello услуги, он отображается в списке hello будет выделено цветной линией. Затем выберите hello степени серьезности (категорий сведений средства syslog), которые должны toocollect.
4. Hello нижней части страницы приветствия щелкните **Сохранить** toofinalize изменения. изменения конфигурации Hello внесенные отправляются hello tooall агенты OMS для Linux, которые зарегистрированы в OMS, обычно это занимает 5 минут.

### <a name="configure-linux-syslog-facilities-in-linux"></a>Настройка устройств системного журнала Linux в Linux
События syslog отправляются из управляющей программы syslog hello, например rsyslog или syslog-ng, tooa локальный порт, агентом Здравствуй прослушивает. Порт по умолчанию — 25224. При установке агента hello, применяется конфигурация syslog по умолчанию. Ее можно найти в следующих каталогах:

rsyslog — /etc/rsyslog.d/rsyslog-oms.conf;

syslog-ng — /etc/syslog-ng/syslog-ng.conf.

по умолчанию Hello: Конфигурация syslog агента OMS передает события syslog из всех средств с уровнем серьезности «предупреждение» или более поздней версии.

> [!NOTE]
> При изменении конфигурации syslog hello, необходимо перезапустить управляющая программа syslog hello для эффекта tootake изменения hello.
>
>

Hello конфигурация syslog по умолчанию для hello агента OMS для Linux для OMS является:

#### <a name="rsyslog"></a>При использовании rsyslog:
```
kern.warning       @127.0.0.1:25224
user.warning       @127.0.0.1:25224
daemon.warning     @127.0.0.1:25224
auth.warning       @127.0.0.1:25224
syslog.warning     @127.0.0.1:25224
uucp.warning       @127.0.0.1:25224
authpriv.warning   @127.0.0.1:25224
ftp.warning        @127.0.0.1:25224
cron.warning       @127.0.0.1:25224
local0.warning     @127.0.0.1:25224
local1.warning     @127.0.0.1:25224
local2.warning     @127.0.0.1:25224
local3.warning     @127.0.0.1:25224
local4.warning     @127.0.0.1:25224
local5.warning     @127.0.0.1:25224
local6.warning     @127.0.0.1:25224
local7.warning     @127.0.0.1:25224
```

#### <a name="syslog-ng"></a>При использовании syslog-ng:
```
#OMS_facility = all
filter f_warning_oms { level(warning); };
destination warning_oms { tcp("127.0.0.1" port(25224)); };
log { source(src); filter(f_warning_oms); destination(warning_oms); };
```

### <a name="tooview-all-syslog-events-with-log-analytics"></a>tooview все события системного журнала с помощью аналитики журналов
1. На портале Operations Management Suite hello щелкните hello **поиска журналов** плитки.
2. В hello **управление журналом** группирование, выберите поиска стандартных системного журнала, а затем выберите один toorun его.

В этом примере представлены все события системного журнала.

![события системного журнала, отображаемые на странице поиска по журналам](./media/log-analytics-linux-agents/oms-linux-syslog.png)

Теперь вы можете подробно рассмотреть результаты поиска.

## <a name="linux-alerts"></a>Оповещения Linux
При использовании Nagios или Zabbix toomanage компьютеры Linux, то OMS может получать hello предупреждения, созданные с помощью этих средств. Тем не менее — в настоящее время нет метода tooconfigure входящих данных предупреждений с помощью портала OMS hello. Вместо этого необходим tooedit конфигурации файла toostart отправку оповещений tooOMS.

### <a name="collect-alerts-from-nagios"></a>Сбор оповещений из Nagios
toocollect предупреждения с сервера Nagios, необходимо toomake hello после изменения конфигурации.

1. Предоставление пользовательских hello **omsagent** toohello доступ на чтение для файла журнала Nagios (т. е. /var/log/nagios/nagios.log). При условии, что файл nagios.log hello принадлежит группе hello **nagios** , можно добавить пользователя hello **omsagent** toohello **nagios** группы.

    ```
    sudo usermod –a -G nagios omsagent
    ```
2. Измените файл omsagent.confconfiguration hello (/ и т. д/opt/microsoft/omsagent/&lt;идентификатор рабочей области&gt;/conf/omsagent.conf). Убедитесь, что присутствуют и не закомментированы следующие записи hello:

    ```
    <source>
    type tail
    #Update path toopoint tooyour nagios.log
    path /var/log/nagios/nagios.log
    format none
    tag oms.nagios
    </source>

    <filter oms.nagios>
    type filter_nagios_log
    </filter>
    ```
3. Перезапустите управляющую программу omsagent hello:

    ```
    sudo /opt/microsoft/omsagent/bin/service_control restart
    ```

### <a name="collect-alerts-from-zabbix"></a>Сбор оповещений из Zabbix
toocollect предупреждений с сервера Zabbix выполните toothose аналогичные шаги для Nagios выше, за исключением того, потребуется toospecify пользователя и пароль в *открытый текст*. Это не очень удобно, но в скором времени это требование может измениться. tooaddress эту проблему, рекомендуется создать пользователя hello и предоставить ему разрешение toomonitor только.

Раздел примера файла конфигурации omsagent.conf hello (/ и т. д/opt/microsoft/omsagent/&lt;идентификатор рабочей области&gt;/conf/omsagent.conf) для Zabbix должен выглядеть hello следующее:

```
<source>
  type zabbix_alerts
  run_interval 1m
  tag oms.zabbix
  zabbix_url http://localhost/zabbix/api_jsonrpc.php
  zabbix_username Admin
  zabbix_password zabbix
</source>

```

### <a name="view-alerts-in-log-analytics-search"></a>Просмотр оповещений с использованием поиска Log Analytics
После настройки вашей tooOMS оповещения toosend компьютеров Linux, можно использовать несколько простых поиска запросов tooview hello предупреждения журнала. Hello следующем примере запрос поиска возвращает все записанные hello оповещения, которые были созданы. Например если в ИТ-инфраструктуре возникает какая-либо проблемы, затем результаты для hello в следующем примере, что запрос может указывать на источник проблемы hello. Кроме того, вы можете легко просмотреть toohello оповещения по исходной системе toohelp узких расследования. Hello преимущество заключается в отсутствии обязательно систем управления toovarious toogo от начала hello — при условии, что оповещения отправляются tooOMS, можно начать прямо отсюда.

```
Type=Alert
```

#### <a name="tooview-all-nagios-alerts-with-log-analytics"></a>tooview Nagios все оповещения с помощью аналитики журналов
1. На портале Operations Management Suite hello щелкните hello **поиска журналов** плитки.
2. В строке запроса hello введите следующий запрос поиска hello

    ```
    Type=Alert SourceSystem=Nagios
    ```
   ![оповещения Nagios, отображаемые на странице поиска по журналам](./media/log-analytics-linux-agents/oms-linux-nagios-alerts.png)

После появления результатов поиска hello, можно просмотреть дополнительные сведения о таких как *AlertState*.

### <a name="tooview-all-zabbix-alerts-with-log-analytics"></a>tooview всех оповещений Zabbix с помощью аналитики журналов
1. На портале Operations Management Suite hello щелкните hello **поиска журналов** плитки.
2. В строке запроса hello введите следующий запрос поиска hello

    ```
    Type=Alert SourceSystem=Zabbix
    ```
   ![оповещения Zabbix, отображаемые на странице поиска по журналам](./media/log-analytics-linux-agents/oms-linux-zabbix-alerts.png)

После появления результатов поиска hello, можно просмотреть дополнительные сведения о таких как *AlertName*.

## <a name="compatibility-with-system-center-operations-manager"></a>Совместимость с System Center Operations Manager
Hello агента OMS для Linux использует двоичные файлы агента совместно с System Center Operations Manager агент hello. Установка hello агента OMS для Linux в системе под управлением Operations Manager обновления hello пакеты OMI и SCX на hello компьютера tooa новой версии. Hello агента OMS для Linux и System Center 2012 R2 являются совместимыми. Однако **System Center 2012 SP1 и более ранних версий не в настоящее время несовместимы или не поддерживаются с hello агента OMS для Linux.**

> [!NOTE]
> Если hello агента OMS для Linux — установленных tooa компьютера, который в настоящее время не находится под управлением Operations Manager и более поздней версии требуется компьютер hello toomanage с Operations Manager, необходимо изменить конфигурацию OMI hello перед обнаружением компьютера hello. **Этот шаг не требуется, если до hello агента OMS для Linux установлен агент Operations Manager hello.**
>
>

### <a name="tooenable-hello-oms-agent-for-linux-toocommunicate-with-operations-manager"></a>hello tooenable агента OMS для Linux toocommunicate с Operations Manager
1. Изменение файла /etc/opt/omi/conf/omiserver.conf hello
2. Убедитесь, что hello строки, начинающиеся с **httpsport =** hello порт 1270. Таким образом — `httpsport=1270`
3. Перезапустите сервер OMI hello:

    ```
    sudo /opt/omi/bin/service_control restart
    ```

## <a name="database-permissions-required-for-mysql-performance-counters"></a>Разрешения базы данных, необходимые для счетчиков производительности MySQL
toogrant разрешения tooa пользователя MySQL, hello пользователю необходимо иметь hello привилегию «предоставление», а также hello предоставляемое право.

Чтобы пользователь MySQL hello tooreturn производительности данных hello пользователь должен иметь доступа toohello следующие запросы:

```
SHOW GLOBAL STATUS;
SHOW GLOBAL VARIABLES:
```

В дополнение к этому toothese запросы hello MySQL пользователю требуется доступ SELECT toohello следующие таблицы по умолчанию:

* information_schema;
* mysql

Эти права можно предоставить, запустив hello следующих команд grant.

```
GRANT SELECT ON information_schema.* too‘monuser’@’localhost’;
GRANT SELECT ON mysql.* too‘monuser’@’localhost’;
```

## <a name="manage-mysql-monitoring-credentials-in-hello-authentication-file"></a>Управление учетными данными в файле проверки подлинности hello мониторинга MySQL
Hello следующие разделы помогут управлять учетными данными MySQL.

### <a name="configure-hello-mysql-omi-provider"></a>Настройка поставщика MySQL OMI hello
Hello поставщик MySQL OMI требуется предварительно настроенный пользователь MySQL и установленные клиентские библиотеки MySQL порядок сведений о производительности и работоспособности tooquery hello из экземпляра MySQL hello.

### <a name="mysql-omi-authentication-file"></a>Файл аутентификации OMI MySQL
Поставщик MySQL OMI использует toodetermine файла проверки подлинности выполняет прослушивание экземпляр MySQL hello какие адреса привязки и порта, и что учетные данные toouse toogather метрики. Во время установки hello MySQL OMI поставщика будет проверять файлы конфигурации my.cnf MySQL (расположения по умолчанию) для адреса привязки и порта и частично набор hello файл проверки подлинности MySQL OMI.

Отслеживание toocomplete экземпляра сервера MySQL добавьте предварительно созданный файл проверки подлинности MySQL OMI в правильный каталог hello.

### <a name="authentication-file-format"></a>Формат файла аутентификации
Hello файл проверки подлинности MySQL OMI является текстовый файл, содержащий сведения о:

* Порт
* адрес привязки;
* имя пользователя MySQL;
* пароль в кодировке Base64.

только Hello файл проверки подлинности MySQL OMI предоставляет права доступа для пользователей Linux toohello чтения и записи, который его создал.

```
[Port]=[Bind-Address], [username], [Base64 encoded Password]
(Port)=(Bind-Address), (username), (Base64 encoded Password)
(Port)=(Bind-Address), (username), (Base64 encoded Password)
AutoUpdate=[true|false]
```

Файл проверки подлинности MySQL OMI по умолчанию содержит экземпляр по умолчанию и номер порта в зависимости от того, какие сведения доступны и проанализированы из hello найден файл конфигурации MySQL.

экземпляр по умолчанию Hello означает toomake, управление несколькими экземплярами MySQL на одном узле Linux проще и обозначается экземпляром hello с портом 0. Все добавленные экземпляры наследуют свойства от экземпляра по умолчанию hello. Например при добавлении экземпляра MySQL, прослушивает порт «3308», адрес привязки, имя пользователя и пароль в кодировке Base64 экземпляра по умолчанию hello достигается используется tootry и отслеживать экземпляр hello прослушивание на порту 3308. Если hello экземпляр в порту 3308 привязан tooanother адрес и использует hello же имя пользователя MySQL и пары пароль только hello необходимо заново указать hello необходимые адреса привязки и hello другие свойства будут унаследованы.

Примеры файла проверки подлинности hello напоминать следующий hello.

Экземпляр по умолчанию и экземпляр с портом 3308:

```
0=127.0.0.1, myuser, cnBwdA==3308=, ,AutoUpdate=true
```

Экземпляр по умолчанию и экземпляр с портом 3308 и другим паролем в кодировке Base 64:

```
0=127.0.0.1, myuser, cnBwdA==3308=127.0.1.1, , AutoUpdate=true
```


| **Свойство** | **Описание** |
| --- | --- |
| Порт |Порт представляет hello текущий порт hello выполняет прослушивание экземпляр MySQL.  Hello порт 0 означает, что для экземпляра по умолчанию используются следующие свойства hello. |
| адрес привязки; |Hello адрес привязки — hello текущий адрес привязки MySQL. |
| Имя пользователя |Это имя пользователя hello hello пользователя MySQL, который следует экземпляра сервера MySQL hello toomonitor toouse. |
| пароль в кодировке Base64. |Это пароль hello hello пользователя MySQL, закодированный в Base64. |
| Автоматическое обновление |После обновления поставщик OMI MySQL hello поставщика hello повторить сканирование на наличие изменений в файле my.cnf hello и перезаписывает файл проверки подлинности OMI MySQL hello. Установите этот флаг tootrue или false в зависимости от необходимых обновлений toohello MySQL OMI файл проверки подлинности. |

#### <a name="authentication-file-location"></a>Расположение файла аутентификации
Hello файл проверки подлинности OMI MySQL должен находится в следующие расположения hello и имя «mysql-auth»:

/var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth

файл Hello (и каталог проверки auth/omsagent) должен принадлежать пользователю omsagent hello.

## <a name="agent-logs"></a>Журналы агента
журналы Hello hello агента OMS для Linux находятся в:

/var/opt/microsoft/omsagent/&lt;ИД_рабочей_области&gt;/log/

Hello журналы hello агента OMS для Linux для omsconfig (конфигурация агента) находятся в:

/var/opt/microsoft/omsconfig/log/

Журналы для компонентов OMI и SCX hello (которые предоставляют данные метрик производительности) находятся в следующем:

/var/opt/omi/log/ и /var/opt/microsoft/scx/log

## <a name="troubleshooting-hello-oms-agent-for-linux"></a>Устранение неполадок hello агента OMS для Linux
Используйте следующие сведения toodiagnose hello и устранение общих проблем.

Если ни один из hello, устранение неполадок в этом разделе поможет также можно hello следующие ресурсы toohelp устранить проблему.

* Клиенты с поддержкой Premier могут обратиться в службу поддержки [здесь](https://premier.microsoft.com/).
* Клиентам с соглашений для поддержки Azure можно зарегистрироваться поддержки по поводу hello [портал Azure](https://manage.windowsazure.com/?getsupport=true)
* Можно [сообщить о проблеме в GitHub](https://github.com/Microsoft/OMS-Agent-for-Linux/issues).
* Форум, посвященный обратной связи идеи и отчет об ошибках toocreate [http://aka.ms/opinsightsfeedback](http://aka.ms/opinsightsfeedback)

### <a name="important-log-locations"></a>Важные расположения журналов
| Файл | Путь |
| --- | --- |
| Файл журнала агента OMS для Linux |`/var/opt/microsoft/omsagent/<workspace id>/log/omsagent.log ` |
| Файл журнала конфигурации агента OMS |`/var/opt/microsoft/omsconfig/omsconfig.log` |

### <a name="important-configuration-files"></a>Важные файлы конфигурации
| Категория | Расположение файла |
| --- | --- |
| syslog |`/etc/syslog-ng/syslog-ng.conf`, `/etc/rsyslog.conf` или `/etc/rsyslog.d/95-omsagent.conf` |
| Данные производительности, Nagios, Zabbix, выходные данные OMS и общая конфигурация агента |`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` |
| Дополнительные конфигурации |`/etc/opt/microsoft/omsagent/<workspace id>/omsagent.d/*.conf` |

> [!NOTE]
> Если конфигурация портала OMS включена, при редактировании файлы конфигурации счетчиков производительности и системных журналов переопределяются. Вы можете отключить конфигурацию в hello портал OMS (для всех узлов) или для отдельных узлов, выполнив следующие hello:
>
>

```
sudo su omsagent -c /opt/microsoft/omsconfig/Scripts/OMS_MetaConfigHelper.py --disable
```


### <a name="enable-debug-logging"></a>Включение ведения журнала отладки
Отладка tooenable ведения журнала, можно использовать подключаемый модуль вывода OMS hello и подробный вывод.

#### <a name="oms-output-plugin"></a>Подключаемый модуль выходных данных OMS
FluentD позволяет hello подключаемого модуля toospecify уровни ведения журнала для различных журнала уровней для входов и выходов. toospecify другая степень журнал для вывода OMS, изменение конфигурации агента общие hello в hello `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` файла.

Hello внизу hello файл конфигурации, измените hello `log_level` свойство из `info` слишком`debug`.

 ```
 <match oms.** docker.**>
  type out_oms
  log_level debug
  num_threads 5
  buffer_chunk_limit 5m
  buffer_type file
  buffer_path /var/opt/microsoft/omsagent/<workspace id>/state/out_oms*.buffer
  buffer_queue_limit 10
  flush_interval 20s
  retry_limit 10
  retry_wait 30s
</match>
 ```

Ведение журнала отладки позволяет службой OMS, разделенных тип, число элементов данных и время, затраченное toosend toohello передачи toosee в пакетном режиме.

*Пример включенного журнала отладки.*

```
Success sending oms.nagios x 1 in 0.14s
Success sending oms.omi x 4 in 0.52s
Success sending oms.syslog.authpriv.info x 1 in 0.91s
```

#### <a name="verbose-output"></a>Подробные выходные данные
Вместо того чтобы использовать подключаемый модуль вывода OMS hello, можно также вывести элементов данных непосредственно слишком`stdout`, которое отображается в hello агента OMS для Linux файла журнала.

В файле конфигурации общего агента OMS hello в `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`, hello OMS вывода подключаемого модуля, добавив комментарий горизонтального `#` перед каждой строки.

```
#<match oms.** docker.**>
#  type out_oms
#  log_level info
#  num_threads 5
#  buffer_chunk_limit 5m
#  buffer_type file
#  buffer_path /var/opt/microsoft/omsagent/<workspace id>/state/out_oms*.buffer
#  buffer_queue_limit 10
#  flush_interval 20s
#  retry_limit 10
#  retry_wait 30s
#</match>
```

Ниже Здравствуйте подключаемого модуля выходные данные, удалить комментарий hello в следующем разделе, удалив hello hello `#` символ в начале каждой строки hello.

```
<match **>
  type stdout
</match>
```

### <a name="forwarded-syslog-messages-do-not-appear-in-hello-log"></a>Перенаправленных сообщений системного журнала не отображаются в журнале hello
#### <a name="probable-causes"></a>Возможные причины
* Hello применения toohello Linux сервер конфигурации не разрешает сбор средства отправки hello и/или уровня ведения журнала
* Syslog не пересылается правильно toohello сервера Linux
* Hello количество сообщений, направляются в секунду слишком велики для базовой конфигурации hello агента OMS для Linux toohandle hello

#### <a name="resolutions"></a>Способы устранения
* Проверка конфигурации hello в hello портал OMS для системного журнала имеет все возможности hello и уровни журнала hello
  * **OMS Portal (Портал OMS) > Параметры > Данные > Системный журнал**.
* Убедитесь, что собственный syslog, управляющие программы обмена сообщениями (`rsyslog`, `syslog-ng`), может tooreceive hello перенаправленных сообщений
* Проверьте параметры брандмауэра на tooensure сервера системного журнала hello, что сообщений не блокируются
* Имитации tooOMS сообщения системного журнала, с помощью hello `logger` команды — например:
  * `logger -p local0.err "This is my test message"`

### <a name="problems-connecting-toooms-when-using-a-proxy"></a>Проблемы с подключением tooOMS при использовании прокси-сервера
#### <a name="probable-causes"></a>Возможные причины
* Hello прокси-сервера указан неверный при установке и настройке агента hello
* конечные точки службы OMS Hello не whitelistested в центре обработки данных

#### <a name="resolutions"></a>Способы устранения
* Переустановите hello агента OMS для Linux, используя следующую команду с параметром hello hello `-v` включена. Это позволяет подробные выходные данные агента hello подключение через прокси-сервера hello toohello службой OMS.
  * `/opt/microsoft/omsagent/bin/omsadmin.sh -w <OMS Workspace ID> -s <OMS Workspace Key> -p <Proxy Conf> -v`
  * Ознакомьтесь с документацией hello для OMS прокси-сервера в [Настройка hello агент для использования с прокси-сервера HTTP](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#configuring-the-agent-for-use-with-an-http-proxy-server)
* Убедитесь, что hello следующих конечных точек службы OMS входят

| Ресурс агента | порты; |
| --- | --- |
| &#42;.ods.opinsights.azure.com |Порт 443 |
| &#42;.oms.opinsights.azure.com |Порт 443 |
| ods.systemcenteradvisor.com |Порт 443 |
| &#42;.blob.core.windows.net/ |Порт 443 |

### <a name="a-403-error-is-displayed-when-onboarding"></a>При подключении отобразилась ошибка с кодом 403
#### <a name="probable-causes"></a>Возможные причины
* Hello Дата и время неверны на сервере Linux
* Hello идентификатор рабочей области и ключ рабочей области, используемый неверны

#### <a name="resolution"></a>Способы устранения:
* Проверьте время hello на сервер Linux с hello `date` команды. Если приветствия данные больше или меньше, чем 15 минут с момента hello текущее время, адаптации завершается ошибкой. toocorrect, Обновить дату hello и часовой пояс сервера Linux.
* последнюю версию агента OMS для Linux hello Hello уведомляет пользователя, если разница во времени является причиной сбоя адаптации
* RE регистрации с помощью hello правильный идентификатор рабочей области и ключ рабочей области. В разделе [адаптации, с помощью командной строки hello](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) для получения дополнительной информации.

### <a name="a-500-error-or-404-error-appears-in-hello-log-file-after-onboarding"></a>Ошибка 500 или сообщение об ошибке 404 указывается в файле журнала hello после адаптации
Это известная проблема, возникающая во время первой передачи данных Linux в рабочей области OMS hello. Это не влияет на отправляемые данные и не вызывает другие проблемы. Можно проигнорировать ошибки hello при первоначальном адаптации.

### <a name="nagios-data-does-not-appear-in-hello-oms-portal"></a>Nagios данных не отображается в hello портал OMS.
#### <a name="probable-causes"></a>Возможные причины
* Hello omsagent пользователь не имеет разрешения tooread из файла журнала Nagios hello
* Hello Nagios источника и фильтр разделы по-прежнему закомментированы в файле omsagent.conf hello

#### <a name="resolutions"></a>Способы устранения
* Добавьте пользователя omsagent hello в порядке tooread из файла Nagios hello. Дополнительные сведения см. в разделе об [оповещениях Nagios](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#nagios-alerts).
* В hello агента OMS для Linux файла общие конфигурации на `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`, убедитесь, что **оба** hello Nagios источника и фильтровать раздела имеют примечания удалены, аналогичные toohello следующий пример.

```
<source>
  type tail
  path /var/log/nagios/nagios.log
  format none
  tag oms.nagios
</source>

<filter oms.nagios>
  type filter_nagios_log
</filter>
```


### <a name="linux-data-doesnt-appear-in-hello-oms-portal"></a>Не обновляются данные Linux hello портал OMS.
#### <a name="probable-causes"></a>Возможные причины
* Не удалось выполнить toohello адаптации службой OMS
* Заблокированные соединения toohello службой OMS
* Hello агента OMS для Linux данных резервных копий

#### <a name="resolutions"></a>Способы устранения
* Убедитесь, что toohello адаптации службой OMS, проверяя, hello успешно `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf` существует.
* RE регистрации с помощью hello omsadmin.sh командной строки. В разделе [адаптации, с помощью командной строки hello](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) для получения дополнительной информации.
* При использовании прокси-сервера используйте hello прокси действия по устранению неполадок выше
* В некоторых случаях если hello агента OMS для Linux не может взаимодействовать со службой OMS hello данные на hello агента — размер полный буфер toohello резервную копию 50 МБ. Перезапустите hello агента OMS для Linux с помощью hello `/opt/microsoft/omsagent/bin/service_control restart` команды.
  >[AZURE.NOTE] Эта проблема исправлена в агенте версии 1.1.0-28 и выше.

### <a name="syslog-linux-performance-counter-configuration-is-not-applied-in-hello-oms-portal"></a>Конфигурация счетчиков производительности syslog Linux не применяется на портале OMS hello
#### <a name="probable-causes"></a>Возможные причины
* агент конфигурации Hello в hello агента OMS для Linux не получен hello последнюю конфигурацию из портала OMS hello.
* Hello измененные параметры портала hello не были применены

#### <a name="resolutions"></a>Способы устранения
`omsconfig`— агент конфигурации hello в hello агента OMS для Linux, который получает изменения конфигурации портала OMS каждые 5 минут. Эта конфигурация будет применен toohello агента OMS для Linux файлов конфигурации, расположенный `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf`.

* В некоторых случаях hello агента OMS для Linux конфигурации агента может оказаться может toocommunicate со службой настройки портала hello приведет к последней конфигурации не применяются.
* Убедитесь, что hello `omsconfig` агент установлен hello следующее:

  * `dpkg --list omsconfig` или `rpm -qi omsconfig`
  * Если не установлен, установите последнюю версию hello hello агента OMS для Linux
* Убедитесь, что hello `omsconfig` агент может взаимодействовать со службой OMS hello

  * Запустите hello `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/GetDscConfiguration.py'` команды
    * Hello выше команда возвращает hello конфигурацию, агент получает из портала hello, включая параметры Syslog, счетчики производительности Linux и пользовательских журналов
    * Если команда hello выше не выполняется, запустите hello `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/PerformRequiredConfigurationChecks.py` команды. Эта команда принудительно выполняет toocommunicate агента omsconfig hello с последней конфигурацией hello OMS службы tooretrieve hello.

### <a name="custom-linux-log-data-does-not-appear-in-hello-oms-portal"></a>Пользовательские данные журнала Linux не отображается в hello портал OMS.
#### <a name="probable-causes"></a>Возможные причины
* Сбой службы адаптации tooOMS
* Hello **hello применить следующие конфигурации toomy серверы Linux** параметр не выбран
* omsconfig не подбираются hello последнюю пользовательский журнал с портала hello
* Hello `omsagent` используется пользовательский журнал hello tooaccess не удается из-за проблемы разрешения tooa или `omsagent` не найден. В этом случае вы увидите hello следующие выходные данные:
  * `[DATETIME] [warn]: file not found. Continuing without tailing it.`
  * `[DATETIME] [error]: file not accessible by omsagent.`
* Это известная проблема с hello гонки, которая была исправлена в hello агента OMS для Linux версии 1.1.0-217

#### <a name="resolutions"></a>Способы устранения
* Убедитесь, что вы успешно встроен, определяя, является ли hello `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf` файл существует.
  * При необходимости, регистрации снова с помощью командной строки omsadmin.sh hello. В разделе [адаптации, с помощью командной строки hello](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) для получения дополнительной информации.
* В hello портал OMS. в разделе **параметры** на hello **данные** убедитесь, что hello **hello применить следующие конфигурации toomy серверы Linux** выбран параметр  
  ![Применить конфигурацию](./media/log-analytics-linux-agents/customloglinuxenabled.png)
* Убедитесь, что hello `omsconfig` агент может взаимодействовать со службой OMS hello

  * Запустите hello `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/GetDscConfiguration.py'` команды
  * Hello выше команда возвращает hello конфигурацию, агент получает из hello портал, включая параметры Syslog, счетчики производительности Linux и пользовательских журналов
  * Если команда hello выше не выполняется, запустите hello `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/PerformRequiredConfigurationChecks.py` команды. Эта команда принудительно toocommunicate агента omsconfig hello со службой OMS и получить последнюю конфигурацию hello.

Вместо hello агента OMS для работы в качестве пользователя с правами доступа пользователя Linux `root`, hello агента OMS для Linux, выполняется как hello `omsagent` пользователя. В большинстве случаев явное разрешение должно быть предоставлено toohello пользователя в порядке tooread некоторые файлы.

разрешение toogrant слишком`omsagent` пользователя, запустите hello, следующие команды:

1. Добавить hello `omsagent` определенной группе пользователей tooa с`sudo usermod -a -G <GROUPNAME> <USERNAME>`
2. Предоставьте необходимый файл toohello универсальный доступ на чтение с`sudo chmod -R ugo+rw <FILE DIRECTORY>`

Имеется известная проблема с hello гонки, которая была исправлена в hello агента OMS для Linux 1.1.0-217 версии. После обновления toohello последнюю версию агента, выполните hello, следующая команда tooget hello последнюю версию подключаемого модуля hello выходные данные:

```
sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.conf /etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf
```

## <a name="known-limitations"></a>Известные ограничения
Просмотрите следующие разделы toolearn о текущих ограничений hello агента OMS для Linux hello.

### <a name="azure-diagnostics"></a>Диагностика Azure
Для виртуальных машин Linux, работающих в Azure дополнительные действия могут быть tooallow требуется сбор данных диагностики Azure и Operations Management Suite. **Версии 2.2** hello диагностическое расширение является обязательным для совместимости с hello агента OMS для Linux.

Дополнительные сведения об установке и настройке hello диагностического расширения для Linux см. в разделе [использовать hello Azure CLI команда tooenable диагностического расширения для Linux](../virtual-machines/linux/classic/diagnostic-extension-v2.md#use-the-azure-cli-command-to-enable-the-linux-diagnostic-extension).

**Обновление 2.0 too2.2 интерфейсе командной строки Azure ASM hello диагностического расширения для Linux:**

```
azure vm extension set -u <vm_name> LinuxDiagnostic Microsoft.OSTCExtensions 2.0
azure vm extension set <vm_name> LinuxDiagnostic Microsoft.OSTCExtensions 2.2 --private-config-path PrivateConfig.json
```

**ARM**

```
azure vm extension set -u <resource-group> <vm-name> Microsoft.Insights.VMDiagnosticsSettings Microsoft.OSTCExtensions 2.0
azure vm extension set <resource-group> <vm-name> LinuxDiagnostic Microsoft.OSTCExtensions 2.2 --private-config-path PrivateConfig.json
```

В этих примерах команд указан файл PrivateConfig.json. Hello формат этого файла должен быть похож на следующий образец hello.

```
    {
    "storageAccountName":"hello storage account tooreceive data",
    "storageAccountKey":"hello key of hello account"
    }
```

### <a name="sysklog-is-not-supported"></a>sysklog не поддерживается
Rsyslog или syslog-ng, требуется toocollect syslog-сообщения. управляющая программа syslog по умолчанию Hello в версии 5 Red Hat Enterprise Linux, CentOS и Oracle Linux (sysklog) версии не поддерживается для сбора событий syslog. toocollect данных syslog из этой версии данных дистрибутивов hello rsyslog управляющая программа должна быть установлена и настроена tooreplace sysklog. Дополнительные сведения о замене sysklog на rsyslog см. в разделе [Установка hello вновь созданного пакета RPM rsyslog](http://wiki.rsyslog.com/index.php/Rsyslog_on_CentOS_success_story#Install_the_newly_built_rsyslog_RPM).

## <a name="next-steps"></a>Дальнейшие действия
* [Добавление решений анализа журналов из коллекции решений hello](log-analytics-add-solutions.md) tooadd функциональные возможности и сбора данных.
* Ознакомьтесь с [входа выполняет](log-analytics-log-searches.md) tooview подробные данные, собранные решения.
* Используйте [панелей мониторинга](log-analytics-dashboards.md) toosave и отображения выполняет собственную.
