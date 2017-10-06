---
title: "Схемы услуг в Operations Management Suite aaaConfigure | Документы Microsoft"
description: "Схемы услуг — это решение Operations Management Suite, который автоматически обнаруживает компонентов приложений в Windows и системами Linux и карты hello обмен данными между службами. В этой статье содержатся подробные сведения о развертывании схемы услуги в вашей среде и приведены разнообразные сценарии ее использования."
services: operations-management-suite
documentationcenter: 
author: daveirwin1
manager: jwhit
editor: tysonn
ms.assetid: d3d66b45-9874-4aad-9c00-124734944b2e
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/18/2016
ms.author: daseidma;bwren;dairwin
ms.openlocfilehash: 3127f4440f2886370f8ff617c405c6d70a926eb8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-service-map-in-operations-management-suite"></a>Настройка схемы услуги в Operations Management Suite
Схемы услуг автоматически обнаруживает компонентов приложений в системах Windows и Linux и maps hello обмен данными между службами. Его можно использовать tooview серверов как можно считать их--взаимосвязанных систем, доставляющих критически важных служб. Схема услуги отображает сведения о подключениях между серверами, процессами и портами в любой подключенной по протоколу TCP архитектуре без дополнительной настройки. Пользователям требуется только установить агент.

В этой статье приводятся сведения hello настройки агентов схемы услуг и адаптации. Сведения об использовании схемы услуг см. в разделе [использовать решение схемы услуг hello в Operations Management Suite](operations-management-suite-service-map.md).

## <a name="dependency-agent-downloads"></a>Скачиваемые файлы агента зависимостей
| Файл | ОС | Version (версия) | SHA-256 |
|:--|:--|:--|:--|
| [InstallDependencyAgent-Windows.exe](https://aka.ms/dependencyagentwindows) | Windows | 9.0.5 | 73B3F6A2A76A08D58F72A550947FF839B588591C48E6EDDD6DDF73AA3FD82B43 |
| [InstallDependencyAgent-Linux64.bin](https://aka.ms/dependencyagentlinux) | Linux | 9.0.5 | A1BAD0B36EBF79F2B69113A07FCF48C68D90BD169C722689F9C83C69FC032371 |


## <a name="connected-sources"></a>Подключенные источники
Схемы услуг получает данные из hello агента Microsoft зависимостей. Hello агент зависимостей зависит от hello агента OMS для ее подключения tooOperations Management Suite. Это означает, что сервер должен иметь hello агента OMS, установить и настроить первыми, а затем можно установить агент зависимостей приветствия. Hello следующей таблице приведены источники hello подключен, поддерживаемых hello карту службы решения.

| Подключенный источник | Поддерживаются | Описание |
|:--|:--|:--|
| Агенты Windows | Да | Служба схемы услуги анализирует и собирает данные с компьютеров с агентами Windows. <br><br>В дополнение toohello [агента OMS](../log-analytics/log-analytics-windows-agents.md), агентов Windows требуют hello агента Microsoft зависимостей. В разделе hello [поддерживаемые операционные системы](#supported-operating-systems) полный список версий операционной системы. |
| Агенты Linux | Да | Служба схемы услуги анализирует и собирает данные с компьютеров с агентами Linux. <br><br>В дополнение toohello [агента OMS](../log-analytics/log-analytics-linux-agents.md), агенты Linux требуется hello агента Microsoft зависимостей. В разделе hello [поддерживаемые операционные системы](#supported-operating-systems) полный список версий операционной системы. |
| Группа управления System Center Operations Manager | Да | Служба схемы услуги анализирует и собирает данные из агентов Windows и Linux в подключенной [группе управления System Center Operations Manager](../log-analytics/log-analytics-om-agents.md). <br><br>Прямое подключение от tooOperations компьютера агента System Center Operations Manager hello Management Suite является обязательным. Данные будут отправлены из hello управления группы toohello Operations Management Suite репозитория.|
| Учетная запись хранения Azure. | Нет | Схемы услуг собирает данные с компьютеров агентов, поэтому нет данных от него toocollect из хранилища Azure. |

Схема услуги поддерживает только 64-разрядные платформы.

В Windows hello агента наблюдения Майкрософт (MMA) используется toogather System Center Operations Manager и Operations Management Suite и отправки данных мониторинга. (Этот агент называется hello агента System Center Operations Manager, агент OMS, аналитика агента журнала, MMA или Direct Agent, в зависимости от контекста hello.) System Center Operations Manager и Operations Management Suite предоставляет различные поля out из hello версии hello MMA. Каждый эти версии можно отчет tooSystem Center Operations Manager, tooOperations Management Suite или tooboth.  

В Linux hello агента OMS для Linux собирает и отправляет мониторинга данных tooOperations Management Suite. Схемы услуг можно использовать на серверах с установленными агентами OMS прямой или на серверах, подключенных tooOperations Management Suite через группы управления System Center Operations Manager.  

В этой статье мы будете ссылаться агенты tooall--ли Linux или Windows, является ли подключается tooa группы управления System Center Operations Manager или напрямую tooOperations Management Suite — как hello «Агент OMS». Мы будем использовать имя конкретного развертывания hello агента hello только в том случае, если он необходим для контекста.

Hello схемы услуг агента не передает сами все данные и не требует изменения toofirewalls ни порты. данные Hello в схемы услуг всегда передается hello агента OMS tooOperations Management Suite, напрямую или через шлюз OMS hello.

![Агенты схемы услуги](media/oms-service-map/agents.png)

Если вы являетесь клиентом System Center Operations Manager с tooOperations подключено групп управления Management Suite:

- Если агенты System Center Operations Manager можно получить доступ к hello Internet tooconnect tooOperations Management Suite, никаких дополнительных настроек не требуется.  
- Если агенты System Center Operations Manager не удается получить доступ к Operations Management Suite через Интернет hello, необходимо toowork шлюза OMS hello tooconfigure с System Center Operations Manager.
  
При использовании hello OMS Direct Agent необходим tooconfigure hello самого агента OMS tooconnect tooOperations Management Suite tooyour OMS шлюза. Hello OMS шлюза можно загрузить из hello [центра загрузки Майкрософт](https://www.microsoft.com/download/details.aspx?id=52666).

### <a name="management-packs"></a>Пакеты управления
При активации схемы услуг в рабочую область Operations Management Suite пакета управления 300 КБ отправляется серверов Windows hello tooall в этой рабочей области. Если вы используете System Center Operations Manager агентов в [подключенной группе управления](../log-analytics/log-analytics-om-agents.md), hello схемы услуг пакет управления, развернутых из System Center Operations Manager. Если непосредственно подключенные агенты hello, Operations Management Suite доставляет hello пакета управления.

пакет управления Hello называется Microsoft.IntelligencePacks.ApplicationDependencyMonitor. Он является письменного too%Programfiles%\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs\. Hello источника данных с использованием пакета управления hello — % Program files%\Microsoft Monitoring Agent\Agent\Health Service State\Resources\<AutoGeneratedID > \ Microsoft.EnterpriseManagement.Advisor.ApplicationDependencyMonitorDataSource.dll.

## <a name="installation"></a>Установка
### <a name="install-hello-dependency-agent-on-microsoft-windows"></a>Установить агент зависимостей hello в Microsoft Windows
Права администратора не требуется tooinstall или удалите агент hello.

Hello зависимостей агент устанавливается на компьютерах Windows с помощью InstallDependencyAgent Windows.exe. Если запустить этот исполняемый файл без параметров, запускается мастер интерактивно выполните tooinstall.  

Используйте следующие шаги tooinstall hello зависимостей агента на каждом компьютере Windows hello:

1.  Установка агента OMS hello с помощью инструкций hello в [toohello компьютеров Windows подключения службы анализа журналов в Azure](../log-analytics/log-analytics-windows-agents.md).
2.  Скачать агент для Windows hello и запустите его с помощью hello следующую команду: <br>`InstallDependencyAgent-Windows.exe`
3.  Выполните приветствия мастера tooinstall hello агента.
4.  При сбое toostart hello агент зависимостей в журнале hello подробные сведения об ошибке. Для агентов Windows hello каталог журнала находится в %Programfiles%\Microsoft Agent\logs зависимостей. 

#### <a name="windows-command-line"></a>Командная строка Windows
Используйте параметры из hello следующую таблицу tooinstall из командной строки. Список флагов установки hello, запустите установщик hello с помощью hello toosee /? /? следующим образом.

    InstallDependencyAgent-Windows.exe /?

| Параметр | Описание |
|:--|:--|
| /? | Получение списка параметров командной строки hello. |
| /S | Выполняет автоматическую установку без вывода сообщений для пользователя. |

Файлы для агента зависимостей Windows hello, помещаются в C:\Program Files\Microsoft зависимостей агента по умолчанию.

### <a name="install-hello-dependency-agent-on-linux"></a>Установить агент зависимостей hello в Linux
Корневой доступ является обязательным tooinstall или настройки агента hello.

Hello зависимостей агент устанавливается на компьютеров Linux с помощью InstallDependencyAgent Linux64.bin, сценарий оболочки с самораспаковывающийся двоичный файл. Можно выполнить с помощью sh hello файл или добавить выполнение сам файл toohello разрешения.
 
Используйте следующие шаги tooinstall hello зависимостей агента на каждом компьютере Linux hello.

1.  Установка агента OMS hello с помощью инструкций hello в [сбора данных и управления ими с компьютеров Linux](https://technet.microsoft.com/library/mt622052.aspx).
2.  Установка агента Linux зависимостей hello корневым каталогом с помощью hello следующую команду:<br>`sh InstallDependencyAgent-Linux64.bin`
3.  При сбое toostart hello агент зависимостей в журнале hello подробные сведения об ошибке. Каталог журнала hello является /var/opt/microsoft/dependency-agent/log агенты Linux.

Список флагов установки hello, запустите программу установки hello с toosee hello - справки флаг следующим образом.

    InstallDependencyAgent-Linux64.bin -help

| Параметр | Описание |
|:--|:--|
| -help | Получение списка параметров командной строки hello. |
| -s | Выполняет автоматическую установку без вывода сообщений для пользователя. |
| --check | Проверьте разрешения и hello операционной системы, но не устанавливать агент hello. |

Файлы для hello агент зависимостей помещаются в hello следующие каталоги:

| Файлы | Расположение |
|:--|:--|
| Основные файлы | /opt/microsoft/dependency-agent |
| Файлы журналов | /var/opt/microsoft/dependency-agent/log |
| Файлы конфигурации | /etc/opt/microsoft/dependency-agent/config |
| Исполняемые файлы службы | /opt/microsoft/dependency-agent/bin/microsoft-dependency-agent<br>/opt/microsoft/dependency-agent/bin/microsoft-dependency-agent-manager |
| Двоичные файлы хранилища | /var/opt/microsoft/dependency-agent/storage |

## <a name="installation-script-examples"></a>Примеры скриптов установки
tooeasily развертывание hello зависимостей агент на нескольких серверах одновременно, он помогает toouse сценария. Можно использовать следующие примеры toodownload сценария hello и установить агент зависимостей hello на Windows или Linux.

### <a name="powershell-script-for-windows"></a>Скрипт PowerShell для Windows
```PowerShell
Invoke-WebRequest "https://aka.ms/dependencyagentwindows" -OutFile InstallDependencyAgent-Windows.exe

.\InstallDependencyAgent-Windows.exe /S
```

### <a name="shell-script-for-linux"></a>Скрипт оболочки для Linux
```
wget --content-disposition https://aka.ms/dependencyagentlinux -O InstallDependencyAgent-Linux64.bin
sh InstallDependencyAgent-Linux64.bin -s
```

## <a name="desired-state-configuration"></a>Настройка требуемого состояния
hello toodeploy агент зависимостей посредством настройки требуемого состояния можно использовать модуль xPSDesiredStateConfiguration hello и большой объем кода hello следующим образом:
```
configuration ServiceMap {

Import-DscResource -ModuleName xPSDesiredStateConfiguration

$DAPackageLocalPath = "C:\InstallDependencyAgent-Windows.exe"

Node localhost
{ 
    # Download and install hello Dependency Agent
    xRemoteFile DAPackage 
    {
        Uri = "https://aka.ms/dependencyagentwindows"
        DestinationPath = $DAPackageLocalPath
    }

    xPackage DA
    {
        Ensure="Present"
        Name = "Dependency Agent"
        Path = $DAPackageLocalPath
        Arguments = '/S'
        ProductId = ""
        InstalledCheckRegKey = "HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Windows\CurrentVersion\Uninstall\DependencyAgent"
        InstalledCheckRegValueName = "DisplayName"
        InstalledCheckRegValueData = "Dependency Agent"
        DependsOn = "[xRemoteFile]DAPackage"
    }
  }
}
```

## <a name="uninstallation"></a>Удаление
### <a name="uninstall-hello-dependency-agent-on-windows"></a>Удаление агента зависимостей в ОС Windows hello
Администратор может удалить hello зависимостей агент для Windows с панели управления.

Администратор также можно запустить %Programfiles%\Microsoft Agent\Uninstall.exe зависимостей toouninstall hello агент зависимостей.

### <a name="uninstall-hello-dependency-agent-on-linux"></a>Удаление hello агент зависимостей в Linux
Удаление toocompletely Здравствуйте агент зависимостей от Linux, необходимо удалить самого агента hello и hello соединитель, который автоматически устанавливается вместе с агентом hello. Можно удалить с помощью hello, выполнив одну команду:

    rpm -e dependency-agent dependency-agent-connector

## <a name="troubleshooting"></a>Устранение неполадок
Если при установке или запуске схемы услуги возникли проблемы, в этом разделе приводятся сведения, которые могут помочь вам. Если по-прежнему не удается устранить проблему, обратитесь в службу поддержки Майкрософт.

### <a name="dependency-agent-installation-problems"></a>Проблемы при установке агента зависимостей
#### <a name="installer-asks-for-a-reboot"></a>Установщик запрашивает перезагрузку
Hello агент зависимостей *обычно* не требует перезагрузки после установки или удаления. Однако в некоторых редких случаях, Windows Server требует toocontinue перезагрузки при установке. Это происходит, когда зависимость, обычно hello Microsoft распространяемый пакет Visual C++, требующее перезагрузки из-за заблокированный файл.

#### <a name="message-unable-tooinstall-dependency-agent-visual-studio-runtime-libraries-failed-tooinstall-code--codenumber-appears"></a>Сообщение «не удается tooinstall агент зависимостей: библиотеки среды выполнения Visual Studio не удалось выполнить tooinstall (код = [Номер_кода])» отображается

Hello зависимостей агента Microsoft основана на hello библиотек времени выполнения Microsoft Visual Studio. Вы получите сообщение, если во время установки библиотек hello проблема. 

установщики библиотеки среды выполнения Hello создавать журналы в папке %LOCALAPPDATA%\temp hello. файл Hello является dd_vcredist_arch_yyyymmddhhmmss.log, где *arch* «x86» или «amd64» и *ггггммддччммсс* hello Дата и время (в 24-часовом формате) создания журнала hello. Hello журнал предоставляет подробные сведения о проблеме hello, блокирующего установку.

Он может быть полезным tooinstall hello [последние библиотеки среды выполнения](https://support.microsoft.com/help/2977003/the-latest-supported-visual-c-downloads) самостоятельно первой.

Hello следующей таблице перечислены коды и рекомендуемые решения.

| Код | Описание | Способы устранения: |
|:--|:--|:--|
| 0x17 | Установщик библиотеки Hello требует обновления Windows, который не был установлен. | Просмотрите hello последнего журнала установщика библиотеки.<br><br>Ли ссылка слишком «Windows8.1-установлено KB2999226-x64.msu» следуют строки «ошибка 0x80240017: сбой tooexecute пакета MSU,» нет необходимых компонентов hello tooinstall установлено KB2999226. Следуйте инструкциям hello в разделе предварительных требований hello в [универсальная среда выполнения C в Windows](https://support.microsoft.com/kb/2999226). Может требуется toorun центра обновления Windows и перезагружаться несколько раз в предварительных требованиях hello tooinstall заказа.<br><br>Снова запустите установщик агента Microsoft зависимостей hello. |

### <a name="post-installation-issues"></a>Проблемы после установки
#### <a name="server-doesnt-appear-in-service-map"></a>Сервер не отображается в службе схемы услуги
Если зависимость агент установлен, но вы не видите нужного сервера hello карту службы решения:
* Успешная установка hello зависимостей агента? Это можно проверить путем проверки toosee hello служба установлена и запущена.<br><br>
**Windows**: поиске hello службы с именем «Агент зависимостей Microsoft».<br>
**Linux**: поиск hello выполнения процесса «microsoft зависимостей агент».

* Включены hello [бесплатной ценовой категории Operations Management Suite или журнала аналитики](https://docs.microsoft.com/azure/log-analytics/log-analytics-add-solutions#offers-and-pricing-tiers)? план Free hello позволяет toofive уникальный схемы услуг серверов. Все последующие серверы, не отображаются в схемы услуг, даже если hello пяти предыдущих больше не отправляют данные.

* — Это сервер отправки журнала и данных производительности tooOperations Management Suite? Перейдите tooLog поиска и запустите hello в следующем запросе для компьютера: 

        * Computer="<your computer name here>" | measure count() by Type
        
  Можно попасть на ряд событий в результатах hello? — Это последние данные hello? В этом случае агент OMS функционировании и взаимодействия с hello службы Operations Management Suite. Если нет, проверьте hello агент OMS на сервере: [Устранение неполадок Windows для агента OMS](https://support.microsoft.com/help/3126513/how-to-troubleshoot-operations-management-suite-onboarding-issues) или [агента OMS для Linux, устранение неполадок](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/Troubleshooting.md).

#### <a name="server-appears-in-service-map-but-has-no-processes"></a>Сервер отображается в решении "Схема услуги", но для него нет процессов
Если вы видите сервером для схемы услуг, но нет процесса или подключения данных, которое указывает, что hello зависимостей агента установлена и запущена, но не удалось загрузить драйвер ядра hello. 

Проверьте файл C:\Program Files\Microsoft зависимостей Agent\logs\wrapper.log hello (Windows) или /var/opt/microsoft/dependency-agent/log/service.log (Linux). Hello последней строки файла hello должно быть указано, почему не удалось загрузить hello ядра. Например hello ядра может не поддерживаться в Linux при обновлении ядро.

## <a name="data-collection"></a>Сбор данных
Можно ожидать, что каждый агент tootransmit приблизительно 25 МБ в день, в зависимости от сложности зависимостей системы. Каждый агент отправляет данные зависимостей схемы услуги каждые 15 секунд.  

Hello агент зависимостей обычно занимают 0,1% системной памяти и 0,1% ЦП системы.

## <a name="supported-azure-regions"></a>Поддерживаемые регионы Azure
Карта службы в настоящее время доступна в следующих регионах Azure hello:
- Восток США
- Западная Европа
- Западно-центральная часть США


## <a name="supported-operating-systems"></a>Поддерживаемые операционные системы
Hello следующих разделах перечислены hello поддерживаемые операционные системы для hello агент зависимостей. Схема услуги не поддерживает 32-разрядные архитектуры операционных систем.

### <a name="windows-server"></a>Windows Server
- Windows Server 2016
- Windows Server 2012 R2
- Windows Server 2012
- Windows Server 2008 R2 с пакетом обновления 1

### <a name="windows-desktop"></a>Классические приложения Windows
- Windows 10
- Windows 8.1
- Windows 8
- Windows 7

### <a name="red-hat-enterprise-linux-centos-linux-and-oracle-linux-with-rhel-kernel"></a>Red Hat Enterprise Linux, CentOS Linux и Oracle Linux (с ядром RHEL)
- Поддерживаются только версии ядра по умолчанию и SMP для Linux.
- Нестандартные версии ядра, такие как PAE и Xen, не поддерживаются ни в одном дистрибутиве Linux. Например в системе с строку hello выпуска «2.6.16.21-0.8-xen» не поддерживается.
- Пользовательские ядра, включая повторные компиляции стандартных ядер, не поддерживаются.
- Ядро CentOSPlus не поддерживается.
- Oracle Unbreakable Enterprise Kernel (UEK) рассматривается в разделе ниже.


#### <a name="red-hat-linux-7"></a>Red Hat Linux 7
| Версия ОС | Версия ядра |
|:--|:--|
| 7.0 | 3.10.0-123 |
| 7.1. | 3.10.0-229 |
| 7,2 | 3.10.0-327 |
| 7.3 | 3.10.0–514 |

#### <a name="red-hat-linux-6"></a>Red Hat Linux 6
| Версия ОС | Версия ядра |
|:--|:--|
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
| Версия ОС | Версия ядра |
|:--|:--|
| 5.8 | 2.6.18-308 |
| 5.9 | 2.6.18-348 |
| 5.10 | 2.6.18-371 |
| 5.11 | 2.6.18-398<br>2.6.18-400<br>2.6.18-402<br>2.6.18-404<br>2.6.18-406<br>2.6.18-407<br>2.6.18-408<br>2.6.18-409<br>2.6.18-410<br>2.6.18-411<br>2.6.18-412<br>2.6.18-416<br>2.6.18–417<br>2.6.18-419 |

#### <a name="oracle-enterprise-linux-with-unbreakable-enterprise-kernel"></a>Oracle Enterprise Linux с Unbreakable Enterprise Kernel

#### <a name="oracle-linux-6"></a>Oracle Linux 6
| Версия ОС | Версия ядра
|:--|:--|
| 6.2 | Oracle 2.6.32-300 (UEK R1) |
| 6.3 | Oracle 2.6.39-200 (UEK R2) |
| 6.4 | Oracle 2.6.39-400 (UEK R2) |
| 6,5 | Oracle 2.6.39-400 (UEK R2 i386) |
| 6.6 | Oracle 2.6.39-400 (UEK R2 i386) |

#### <a name="oracle-linux-5"></a>Oracle Linux 5

| Версия ОС | Версия ядра
|:--|:--|
| 5.8 | Oracle 2.6.32-300 (UEK R1) |
| 5.9 | Oracle 2.6.39-300 (UEK R2) |
| 5.10 | Oracle 2.6.39-400 (UEK R2) |
| 5.11 | Oracle 2.6.39-400 (UEK R2) |

#### <a name="suse-linux-enterprise-server"></a>SUSE Linux Enterprise Server

#### <a name="suse-linux-11"></a>SUSE Linux 11
| Версия ОС | Версия ядра
|:--|:--|
| 11 | 2.6.27 |
| 11 SP1 | 2.6.32 |
| 11 SP2 | 3.0.13 |
| 11 SP3 | 3.0.76 |
| 11 SP4 | 3.0.101 |

#### <a name="suse-linux-10"></a>SUSE Linux 10
| Версия ОС | Версия ядра
|:--|:--|
| 10 SP4 | 2.6.16.60 |

## <a name="diagnostic-and-usage-data"></a>Данные диагностики и использования
Корпорация Майкрософт автоматически собирает данные об использовании и производительности посредством использования hello схемы услуг службы. Корпорация Майкрософт использует этот tooprovide данных и повышения качества hello, безопасности и целостности hello схемы услуг службы. Данные включают сведения о конфигурации программного обеспечения, такие как версия операционной системы и hello. Также включает IP-адрес, DNS-имя и имя рабочей станции в порядке tooprovide точные и эффективный возможности по устранению неполадок. Корпорация Майкрософт не собирает сведения об именах, адресах и другую контактную информацию.

Дополнительные сведения о сборе и использовании данных см. в разделе hello [заявления о конфиденциальности Microsoft Online Services](https://go.microsoft.com/fwlink/?LinkId=512132).



## <a name="next-steps"></a>Дальнейшие действия
- Узнайте, каким образом слишком[использовать схемы услуг](operations-management-suite-service-map.md) после развертывания и настройки.
