---
title: "aaaWire решение данных в службе анализа журналов | Документы Microsoft"
description: "Данные передачи — это объединенные сетевые данные и данные производительности, передаваемые с компьютеров с установленными агентами OMS, включая агенты Operations Manager и агенты, подключенные к Windows. Сетевые данные вместе с данным вашего журнала toohelp корреляцию данных."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: fc3d7127-0baa-4772-858a-5ba995d1519b
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: banders
ms.openlocfilehash: adafdf98dfbda9d87759643a1a606a84eafd1348
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="wire-data-20-preview-solution-in-log-analytics"></a>Решение Wire Data 2.0 (предварительная версия) в Log Analytics

![Символ Wire Data](./media/log-analytics-wire-data/wire-data2-symbol.png)

Данные передачи — это объединенные сетевые данные и данные производительности, передаваемые с компьютеров с установленными агентами OMS, включая агенты Operations Manager и агенты, подключенные к Windows, а также агенты Linux. Сетевые данные вместе с вашей toohelp данные журнала корреляцию данных.

Кроме агентов tooOMS hello решение для данных передачи использует агенты Microsoft зависимостей, устанавливаемого на компьютерах в ИТ-инфраструктуре. Tooand зависимостей агенты монитора сети данных, отправляемых с компьютеров сети уровней 2 – 3 в hello [модели OSI](https://en.wikipedia.org/wiki/OSI_model), включая hello различные используемые протоколы и порты. Затем данные отправляются tooLog аналитика с помощью агентов.

> [!NOTE]
> Не удается добавить hello предыдущей версии решения toonew hello данные передачи областей. Если исходные данные передачи решение hello включена, можно продолжить toouse его. Однако toouse 2.0 передачи данных, необходимо сначала удалить исходную версию hello.

По умолчанию Log Analytics собирает зарегистрированные в журналах данные производительности ЦП, памяти, дисков и сети на основе показателей счетчиков, встроенных в Windows. Сбора сетевых и других данных выполняется режиме реального времени для каждого агента, включая протоколы подсетей и протоколы уровня приложений, используемого компьютера hello. На странице параметров hello вкладка "журналы" hello, можно добавить другие счетчики производительности.

Если вы использовали [sFlow](http://www.sflow.org/) или другое программное обеспечение с [протоколом NetFlow от Cisco](http://www.cisco.com/c/en/us/products/collateral/ios-nx-os-software/ios-netflow/prod_white_paper0900aecd80406232.html), затем hello статистику и данные, вы видите из данных передачи будут знакомы tooyou.

Ниже перечислены некоторые типы встроенных запросов поиска журналов hello.

- агенты,предоставляющие данные передачи;
- IP-адреса агентов, предоставляющих данные передачи;
- исходящие подключения по IP-адресам;
- количество байт, отправленных протоколами приложений;
- количество байт, отправленных службой приложений;
- количество байт, полученных различными протоколами;
- общее количество отправленных и полученных байт по версии IP;
- среднее время задержки для подключений, которые оценивались как надежные;
- компьютерные процессы, которые инициировали или получали сетевой трафик;
- объем сетевого трафика для процесса.

При поиске с помощью данных передачи, можно фильтровать и hello группы данных tooview сведения об основных агентах и основных протоколах. Кроме того, можно узнать, когда определенные компьютеры (IP-адреса или MAC-адреса) взаимодействовали друг с другом, как долго длился процесс и сколько данных было отправлено. По сути вы просматриваете метаданные о сетевом трафике на основе поиска.

Однако просмотр метаданных не всегда полезен для проведения глубокой диагностики. Данные передачи в Log Analytics не являются полным отражением сетевых данных. Поэтому они не предназначены для расширенного устранения неполадок на уровне пакетов. Здравствуйте, преимуществом использования агента hello, по сравнению с tooother методов сбора, не имеют tooinstall устройств, перенастройки коммутаторов сети или выполнения сложных конфигураций. Данные передачи — это просто на основе агентов — hello агент устанавливается на компьютере, и он будет отслеживать свой собственный сетевой трафик. Еще одним преимуществом использования удобно, если нужно toomonitor рабочие нагрузки, выполняющиеся у поставщиков облачных служб или поставщика услуг размещения Microsoft Azure, где пользователь hello не является владельцем уровня структуры hello.

## <a name="connected-sources"></a>Подключенные источники

Данные передачи получает данные из hello агента Microsoft зависимостей. Hello агент зависимостей зависит от hello агента OMS для ее подключения tooLog Analytics. Это означает, что сервер должен иметь hello OMS агент установлен и настроен первый, и затем установить агент зависимостей hello. Hello следующей таблице описаны hello подключенных источников, которые поддерживает решение для данных передачи hello.

| **Подключенный источник** | **Поддерживаются** | **Описание** |
| --- | --- | --- |
| Агенты Windows | Да | Решение "Данные передачи" анализирует и собирает данные из компьютеров агентов Windows. <br><br> В дополнение toohello [агента OMS](log-analytics-windows-agents.md), агентов Windows требуют hello агента Microsoft зависимостей. В разделе hello [поддерживаемые операционные системы](../operations-management-suite/operations-management-suite-service-map-configure.md#supported-operating-systems) полный список версий операционной системы. |
| Агенты Linux | Да | Решение "Данные передачи" анализирует и собирает данные из компьютеров агентов Linux.<br><br> В дополнение toohello [агента OMS](log-analytics-linux-agents.md), агенты Linux требуется hello агента Microsoft зависимостей. В разделе hello [поддерживаемые операционные системы](../operations-management-suite/operations-management-suite-service-map-configure.md#supported-operating-systems) полный список версий операционной системы. |
| Группа управления System Center Operations Manager | Да | Решение "Данные передачи" анализирует и собирает данные из агентов Windows и Linux в подключенной [группе управления System Center Operations Manager](log-analytics-om-agents.md). <br><br> Прямое подключение от tooLog компьютера агента System Center Operations Manager hello аналитика является обязательным. Данные будут отправлены из tooLog группы управления hello Analytics. |
| Учетная запись хранения Azure. | Нет | Данные передачи собирает данные от компьютеров агентов, поэтому нет данных от него toocollect из хранилища Azure. |

В Windows hello агента наблюдения Майкрософт (MMA) используется как System Center Operations Manager, так и служба аналитики журналов toogather и отправлять данные. В зависимости от контекста hello агента hello называется hello агента System Center Operations Manager, агент OMS, аналитика агента журнала, MMA или Direct Agent. System Center Operations Manager и анализа журналов предоставляют несколько разных версий hello MMA. Каждый эти версии можно отчет tooSystem Center Operations Manager, tooLog Analytics или tooboth.

В Linux hello агента OMS для Linux собирает и отправляет данные tooLog Analytics. Данные передачи можно использовать на серверах с установленными агентами OMS прямой или на серверах, подключенных tooLog Analytics через группы управления System Center Operations Manager.

В этой статье, ссылается на агенты tooall ли Linux или Windows, ли tooa подключенной группы управления System Center Operations Manager или напрямую tooLog аналитика называется hello _агента OMS_. Мы будем использовать имя конкретного развертывания hello агента hello только в том случае, если он необходим для контекста.

Hello агент зависимостей не передает сами все данные и не требует изменения toofirewalls ни порты. Hello в данных передачи всегда передачи данных по tooLog агента OMS hello аналитики, либо непосредственно или с помощью OMS шлюза "hello".

![Схема передачи данных агентами](./media/log-analytics-wire-data/agents.png)

Если вы являетесь пользователем System Center Operations Manager с tooLog подключено групп управления аналитика:

- Без дополнительных настроек не требуется, когда агенты System Center Operations Manager можно получить доступ к hello Internet tooconnect tooLog Analytics.
- Необходимо toowork шлюза OMS hello tooconfigure с System Center Operations Manager агентов System Center Operations Manager нет доступа к службе анализа журналов через Интернет hello.

При использовании hello Direct Agent необходим tooconfigure hello OMS самого агента tooconnect tooLog Analytics tooyour OMS шлюза. Можно загрузить hello шлюза OMS hello [центра загрузки Майкрософт](https://www.microsoft.com/download/details.aspx?id=52666).

## <a name="prerequisites"></a>Предварительные требования

- Требуется hello [аналитика](https://www.microsoft.com/cloud-platform/operations-management-suite-pricing) предложение решения.
- Если вы используете предыдущую версию hello hello решение для данных передачи, необходимо сначала удалить его. Тем не менее все данные, полученные через hello исходное решение для передачи данных по-прежнему доступна в 2.0 передачи данных и поиска журналов.
- Права администратора, необходимые tooinstall или удалите hello агент зависимостей.
- Hello зависимостей агент должен устанавливаться на компьютер с 64-разрядной операционной системе.

### <a name="operating-systems"></a>Операционные системы

Hello следующих разделах перечислены hello поддерживаемые операционные системы для hello агент зависимостей. Решение "Данные передачи" не поддерживает 32-разрядные архитектуры операционных систем.

#### <a name="windows-server"></a>Windows Server

- Windows Server 2016
- Windows Server 2012 R2
- Windows Server 2012
- Windows Server 2008 R2 с пакетом обновления 1

#### <a name="windows-desktop"></a>Классические приложения Windows

- Windows 10
- Windows 8.1
- Windows 8
- Windows 7

#### <a name="red-hat-enterprise-linux-centos-linux-and-oracle-linux-with-rhel-kernel"></a>Red Hat Enterprise Linux, CentOS Linux и Oracle Linux (с ядром RHEL)

- Поддерживаются только версии ядра по умолчанию и SMP для Linux.
- Нестандартные версии ядра, такие как PAE и Xen, не поддерживаются ни в одном дистрибутиве Linux. Например, в системе с выпуска строку hello _2.6.16.21-0.8-xen_ не поддерживается.
- Пользовательские ядра, включая повторные компиляции стандартных ядер, не поддерживаются.
- Ядро CentOSPlus не поддерживается.
- Oracle Unbreakable Enterprise Kernel (UEK) рассматривается в разделе ниже.

#### <a name="red-hat-linux-7"></a>Red Hat Linux 7

| **Версия ОС** | **Версия ядра** |
| --- | --- |
| 7.0 | 3.10.0-123 |
| 7.1. | 3.10.0-229 |
| 7,2 | 3.10.0-327 |
| 7.3 | 3.10.0–514 |

#### <a name="red-hat-linux-6"></a>Red Hat Linux 6

| **Версия ОС** | **Версия ядра** |
| --- | --- |
| 6,0 | 2.6.32-71 |
| 6.1 | 2.6.32-131 |
| 6.2 | 2.6.32-220 |
| 6.3 | 2.6.32-279 |
| 6.4 | 2.6.32-358 |
| 6,5 | 2.6.32-431 |
| 6.6 | 2.6.32-504 |
| 6.7 | 2.6.32-573 |
| 6,8 | 2.6.32-642 |

#### <a name="red-hat-linux-5"></a>Red Hat Linux 5

| **Версия ОС** | **Версия ядра** |
| --- | --- |
| 5.8 | 2.6.18-308 |
| 5.9 | 2.6.18-348 |
| 5.10 | 2.6.18-371 |
| 5.11 | 2.6.18-398 <br> 2.6.18-400 <br>2.6.18-402 <br>2.6.18-404 <br>2.6.18-406 <br> 2.6.18-407 <br> 2.6.18-408 <br> 2.6.18-409 <br> 2.6.18-410 <br> 2.6.18-411 <br> 2.6.18-412 <br> 2.6.18-416 <br> 2.6.18–417 <br> 2.6.18-419 |

#### <a name="oracle-enterprise-linux-with-unbreakable-enterprise-kernel"></a>Oracle Enterprise Linux с Unbreakable Enterprise Kernel

#### <a name="oracle-linux-6"></a>Oracle Linux 6

| **Версия ОС** | **Версия ядра** |
| --- | --- |
| 6.2 | Oracle 2.6.32-300 (UEK R1) |
| 6.3 | Oracle 2.6.39-200 (UEK R2) |
| 6.4 | Oracle 2.6.39-400 (UEK R2) |
| 6,5 | Oracle 2.6.39-400 (UEK R2 i386) |
| 6.6 | Oracle 2.6.39-400 (UEK R2 i386) |

#### <a name="oracle-linux-5"></a>Oracle Linux 5

| **Версия ОС** | **Версия ядра** |
| --- | --- |
| 5.8 | Oracle 2.6.32-300 (UEK R1) |
| 5.9 | Oracle 2.6.39-300 (UEK R2) |
| 5.10 | Oracle 2.6.39-400 (UEK R2) |
| 5.11 | Oracle 2.6.39-400 (UEK R2) |

#### <a name="suse-linux-enterprise-server"></a>SUSE Linux Enterprise Server

#### <a name="suse-linux-11"></a>SUSE Linux 11

| **Версия ОС** | **Версия ядра** |
| --- | --- |
| 11 | 2.6.27 |
| 11 SP1 | 2.6.32 |
| 11 SP2 | 3.0.13 |
| 11 SP3 | 3.0.76 |
| 11 SP4 | 3.0.101 |

#### <a name="suse-linux-10"></a>SUSE Linux 10

| **Версия ОС** | **Версия ядра** |
| --- | --- |
| 10 SP4 | 2.6.16.60 |

#### <a name="dependency-agent-downloads"></a>Скачиваемые файлы агента зависимостей

| **File** | **ОС** | **Версия** | **SHA-256** |
| --- | --- | --- | --- |
| [InstallDependencyAgent-Windows.exe](https://aka.ms/dependencyagentwindows) | Windows | 9.0.5 | 73B3F6A2A76A08D58F72A550947FF839B588591C48E6EDDD6DDF73AA3FD82B43 |
| [InstallDependencyAgent-Linux64.bin](https://aka.ms/dependencyagentlinux) | Linux | 9.0.5 | A1BAD0B36EBF79F2B69113A07FCF48C68D90BD169C722689F9C83C69FC032371 |



## <a name="configuration"></a>Конфигурация

Выполните следующие шаги tooconfigure hello данные передачи решения для рабочих областей hello.

1. Включить решение hello анализа журналов действий из hello [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.WireData2OMS?tab=Overview) или с помощью hello процесс, описанный в [решений добавьте анализа журналов из коллекции решений hello](log-analytics-add-solutions.md).
2. Установите агент зависимостей hello на каждом компьютере, где вы хотите tooget данные. Hello агент зависимостей можно отслеживать соседей tooimmediate соединения, поэтому может не требоваться агента на каждом компьютере.

### <a name="install-hello-dependency-agent-on-windows"></a>Установка агента зависимостей hello в Windows

Права администратора не требуется tooinstall или удалите агент hello.

Hello зависимостей агент устанавливается на компьютерах под управлением Windows через InstallDependencyAgent Windows.exe. Если запустить этот исполняемый файл без параметров, запускается мастер интерактивно выполните tooinstall.

Используйте следующие шаги tooinstall hello зависимостей агента на каждом компьютере под управлением Windows hello:

1. Установка агента OMS hello с помощью инструкций hello в [toohello компьютеров Windows подключения службы анализа журналов в Azure](log-analytics-windows-agents.md).
2. Скачать агент Windows hello, с помощью ссылки hello в предыдущем разделе hello и запустите его с помощью hello следующую команду: InstallDependencyAgent Windows.exe
3. Выполните приветствия мастера tooinstall hello агента.
4. При сбое toostart hello агент зависимостей в журнале hello подробные сведения об ошибке. Для агентов Windows hello каталог журнала находится в %Programfiles%\Microsoft Agent\logs зависимостей.

#### <a name="windows-command-line"></a>Командная строка Windows

Используйте параметры из hello следующую таблицу tooinstall из командной строки. Список флагов установки hello, запустите установщик hello с помощью hello toosee /? /? следующим образом.

InstallDependencyAgent-Windows.exe /?

| **Параметр** | **Описание** |
| --- | --- |
| <code>/?</code> | Получение списка параметров командной строки hello. |
| <code>/S</code> | Выполняет автоматическую установку без вывода сообщений для пользователя. |

Файлы для агента зависимостей Windows hello, помещаются в C:\Program Files\Microsoft зависимостей агента по умолчанию.

### <a name="install-hello-dependency-agent-on-linux"></a>Установить агент зависимостей hello в Linux

Корневой доступ является обязательным tooinstall или настройки агента hello.

Hello зависимостей агент устанавливается на компьютеров Linux с помощью InstallDependencyAgent Linux64.bin, сценарий оболочки с самораспаковывающийся двоичный файл. Можно выполнять с помощью файла hello _sh_ или добавьте выполнение сам файл toohello разрешения.

Используйте следующие шаги tooinstall hello зависимостей агента на каждом компьютере Linux hello.

1. Установка агента OMS hello с помощью инструкций hello в [сбора данных и управления ими с компьютеров Linux](log-analytics-agent-linux.md).
2. Скачать агент Linux зависимостей hello, с помощью ссылки hello в предыдущем разделе hello и затем установить его как корневой элемент с помощью hello следующую команду: sh InstallDependencyAgent Linux64.bin
3. При сбое toostart hello агент зависимостей в журнале hello подробные сведения об ошибке. На агентах Linux — каталог журнала hello: /var/opt/microsoft/dependency-agent/log.

Список флагов установки hello, запустите программу установки hello с hello toosee `-help` флаг следующим образом.

```
InstallDependencyAgent-Linux64.bin -help
```

| **Параметр** | **Описание** |
| --- | --- |
| <code>-help</code> | Получение списка параметров командной строки hello. |
| <code>-s</code> | Выполняет автоматическую установку без вывода сообщений для пользователя. |
| <code>--check</code> | Проверьте разрешения и hello операционной системы, но не устанавливать агент hello. |

Файлы для hello агент зависимостей помещаются в hello следующие каталоги:

| **Файлы** | **Расположение** |
| --- | --- |
| Основные файлы | /opt/microsoft/dependency-agent |
| Файлы журналов | /var/opt/microsoft/dependency-agent/log |
| Файлы конфигурации | /etc/opt/microsoft/dependency-agent/config |
| Исполняемые файлы службы | /opt/microsoft/dependency-agent/bin/microsoft-dependency-agent<br><br>/opt/microsoft/dependency-agent/bin/microsoft-dependency-agent-manager |
| Двоичные файлы хранилища | /var/opt/microsoft/dependency-agent/storage |

### <a name="installation-script-examples"></a>Примеры скриптов установки

tooeasily развертывание hello зависимостей агент на нескольких серверах одновременно, он помогает toouse сценария. Можно использовать следующие примеры toodownload сценария hello и установить агент зависимостей hello на Windows или Linux.

#### <a name="powershell-script-for-windows"></a>Скрипт PowerShell для Windows

```PowerShell

Invoke-WebRequest &quot;https://aka.ms/dependencyagentwindows&quot; -OutFile InstallDependencyAgent-Windows.exe

.\InstallDependencyAgent-Windows.exe /S

```

#### <a name="shell-script-for-linux"></a>Скрипт оболочки для Linux

```
wget --content-disposition https://aka.ms/dependencyagentlinux -O InstallDependencyAgent-Linux64.bin
```

```
sh InstallDependencyAgent-Linux64.bin -s
```

### <a name="desired-state-configuration"></a>Настройка требуемого состояния

hello toodeploy агент зависимостей посредством настройки требуемого состояния можно использовать модуль xPSDesiredStateConfiguration hello и большой объем кода hello следующим образом:

```
Import-DscResource -ModuleName xPSDesiredStateConfiguration

$DAPackageLocalPath = &quot;C:\InstallDependencyAgent-Windows.exe&quot;



Node $NodeName

{

    # Download and install hello Dependency Agent

    xRemoteFile DAPackage

    {

        Uri = &quot;https://aka.ms/dependencyagentwindows&quot;

        DestinationPath = $DAPackageLocalPath

        DependsOn = &quot;[Package]OI&quot;

    }

    xPackage DA

    {

        Ensure=&quot;Present&quot;

        Name = &quot;Dependency Agent&quot;

        Path = $DAPackageLocalPath

        Arguments = '/S'

        ProductId = &quot;&quot;

        InstalledCheckRegKey = &quot;HKEY\_LOCAL\_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Windows\CurrentVersion\Uninstall\DependencyAgent&quot;

        InstalledCheckRegValueName = &quot;DisplayName&quot;

        InstalledCheckRegValueData = &quot;Dependency Agent&quot;

    }

}

```
### <a name="uninstall-hello-dependency-agent"></a>Удаление hello агенту зависимостей

Используйте следующие разделы toohelp, удалите агент зависимостей hello hello.

#### <a name="uninstall-hello-dependency-agent-on-windows"></a>Удаление агента зависимостей в ОС Windows hello

Администратор может удалить hello зависимостей агент для Windows с панели управления.

Администратор также можно запустить %Programfiles%\Microsoft Agent\Uninstall.exe зависимостей toouninstall hello агент зависимостей.

#### <a name="uninstall-hello-dependency-agent-on-linux"></a>Удаление hello агент зависимостей в Linux

Удаление toocompletely Здравствуйте агент зависимостей от Linux, необходимо удалить самого агента hello и hello соединитель, который автоматически устанавливается вместе с агентом hello. Можно удалить с помощью hello, выполнив одну команду:

```
rpm -e dependency-agent dependency-agent-connector
```

## <a name="management-packs"></a>Пакеты управления

При активации в рабочей области аналитики журналов данных передачи пакета управления 300 КБ отправляется tooall серверов Windows hello в этой рабочей области. Если вы используете System Center Operations Manager агентов в [подключенной группе управления](log-analytics-om-agents.md), hello монитор зависимостей пакета управления, развернутых из System Center Operations Manager. Если непосредственно подключенные агенты hello, аналитика журналов доставляет hello пакета управления.

пакет управления Hello называется Microsoft.IntelligencePacks.ApplicationDependencyMonitor. Он записывается в папку %Programfiles%\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs. — Hello источника данных, который использует пакет управления hello: % Program files%\Microsoft Monitoring Agent\Agent\Health Service State\Resources&lt;AutoGeneratedID&gt;\ Microsoft.EnterpriseManagement.Advisor.ApplicationDependencyMonitorDataSource.dll.

## <a name="using-hello-solution"></a>С помощью решения hello

**Установка и настройка решения hello**

Используйте следующие сведения tooinstall hello и настроить решение hello.

- решение для данных передачи Hello получает данные с компьютеров под управлением Windows Server 2012 R2, Windows 8.1 и более поздних операционных системах.
- На компьютеры, где требуется tooacquire передачи данных из требуется Microsoft .NET Framework 4.0 или более поздней версии.
- Добавление hello данные передачи решения tooyour анализа журналов рабочей области с помощью hello процесс, описанный в [решений добавьте анализа журналов из коллекции решений hello](log-analytics-add-solutions.md). Дополнительная настройка не требуется.
- Tooview передачи данных для конкретного решения, вы должны toohave hello решение уже добавлен tooyour рабочей области.

После установлены агенты и установке решения hello, Плитка hello 2.0 передачи данных отображается в рабочей области.

> [!NOTE]
> В настоящее время необходимо использовать данные передачи tooview портала OMS hello. Нельзя использовать hello Azure портала tooview передачи данных.

![Плитка "Данные передачи"](./media/log-analytics-wire-data/wire-data-tile.png)

## <a name="using-hello-wire-data-20-solution"></a>С помощью решения hello 2.0 передачи данных

На портале OMS hello щелкните hello **передачи данных 2.0** плитки tooopen hello передачи данных мониторинга. панель мониторинга Hello включает hello колонок в hello в следующей таблице. Каждой колонки перечислены вверх too10 сузьте указан, в колонке критерий hello области и временной диапазон. Можно выполнить поиск журнала, который возвращает все записи, нажав кнопку **все** hello нижней части колонки hello или щелкнув заголовок колонки hello.

| **Колонка** | **Описание** |
| --- | --- |
| Агенты, записывающие сетевой трафик | Показывает количество hello агенты, которые записи сетевого трафика и перечисляет hello top 10 компьютеров, которые захватываемых трафика. Щелкните номер toorun hello поиска журналов для <code>Type:WireData &#124; measure Sum(TotalBytes) by Computer &#124; top 500000</code>. Выберите компьютер в списке toorun hello поиска журналов, возвращая hello общее число записанных байтов. |
| Локальные подсети | Показывает количество hello в локальной подсети, которые обнаружены агенты.  Щелкните номер toorun hello поиска журналов для <code>Type:WireData &#124; Measure Sum(TotalBytes) by LocalSubnet</code> , в которой перечислены все подсети с hello количеством байтов, отправленных в каждый из них. Выберите подсеть в списке toorun hello поиска журналов, возвращая hello общее число байтов, отправленных в подсети hello. |
| Протоколы уровня приложений | Показывает номер hello протоколы уровня приложений используется, как обнаруженный агентами. Щелкните номер toorun hello поиска журналов для <code>Type:WireData &#124; Measure Sum(TotalBytes) by ApplicationProtocol</code>. Щелкните toorun протокола поиска журналов, возвращая hello общее число байтов, отправленных по протоколу hello. |

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

![Панель мониторинга "Данные передачи"](./media/log-analytics-wire-data/wire-data-dash.png)

Можно использовать hello **агенты, записывающие сетевой трафик** toodetermine колонки, какую часть пропускной способности сети, потребляемый компьютеров. Эта колонка позволяет легко найти hello _chattiest_ компьютера в среде. Такие компьютеры могут быть перегружены, работать со сбоями либо использовать больше сетевых ресурсов, чем обычно.

![Пример поиска по журналам](./media/log-analytics-wire-data/log-search-example01.png)

Аналогичным образом можно использовать hello **в локальных подсетях** toodetermine колонки, объем сетевого трафика, перемещение по подсетей. Пользователи часто создают подсети для важных областей своих приложений. Эта колонка позволяет просматривать такие области.

![Пример поиска по журналам](./media/log-analytics-wire-data/log-search-example02.png)

Hello **протоколы уровня приложений** колонке полезно потому, что бывает полезно знать протоколы используется. Например можно предположить, настоящий SSH toonot в сетевой среде. Просмотр данных, доступных в колонке hello быстро подтвердить или не опровергает ваши ожидания.

![Пример поиска по журналам](./media/log-analytics-wire-data/log-search-example03.png)

В этом примере можно было бы глубже изучить SSH сведения toosee компьютеры, на которых используется SSH и множество других сведений о связи.

![результаты поиска SSH](./media/log-analytics-wire-data/ssh-details.png)

Это также полезно tooknow Если трафик протокола увеличивается или уменьшается во времени. Например если возрастает hello объем данных, передаваемых приложением, могут быть то, что следует обратить внимание, или, может оказаться внимания.

## <a name="input-data"></a>Входные данные

Метаданные о сетевом трафике, с помощью hello агенты, которые вы включили собирает данные передачи. Каждый агент передает данные примерно каждые 15 секунд.

## <a name="output-data"></a>Выходные данные

Для каждого типа входных данных создается запись с данными о типе _WireData_. Данные передачи записи имеют свойства, показанные в следующей таблице hello:

| Свойство | Описание |
|---|---|
| Компьютер | Имя компьютера, на котором были собраны данные |
| TimeGenerated | Время записи hello |
| LocalIP | IP-адрес локального компьютера hello |
| SessionState | Подключен или отключен |
| ReceivedBytes | Число полученных байт |
| ProtocolName | Имя hello сетевой протокол, используемый |
| IPVersion | Версия IP |
| Направление | Входящий или исходящий |
| MaliciousIP | IP-адрес известного вредоносного источника |
| Severity | Опасность потенциально вредоносной программы |
| RemoteIPCountry | Страна hello удаленный IP-адрес |
| ManagementGroupName | Имя группы управления Operations Manager hello |
| SourceSystem | Источник, на котором были собраны данные |
| SessionStartTime | Время начала сеанса |
| SessionEndTime | Время окончания сеанса |
| LocalSubnet | Подсеть, в которой были собраны данные |
| LocalPortNumber | Номер локального порта |
| RemoteIP | Удаленный IP-адрес, используемый hello удаленного компьютера |
| RemotePortNumber | Номер порта, используемый hello удаленный IP-адрес |
| SessionID | Уникальное значение, которое идентифицирует сеанс связи между двумя IP-адресами |
| SentBytes | Число отправленных байт |
| TotalBytes | Общее число байтов, отправленных в течение сеанса |
| ApplicationProtocol | Тип используемого сетевого протокола   |
| ProcessID | Идентификатор процесса Windows |
| ProcessName | Путь и имя файла процесса hello |
| RemoteIPLongitude | Значение долготы IP |
| RemoteIPLatitude | Значение широты IP |


## <a name="next-steps"></a>Дальнейшие действия

- [Выполнять поиск в журналах](log-analytics-log-searches.md) tooview подробные записи поиска передачи данных.
