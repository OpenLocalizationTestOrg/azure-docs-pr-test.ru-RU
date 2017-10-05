---
title: "Настройка схемы услуги в Operations Management Suite | Документы Майкрософт"
description: "Схема услуги — это решение Operations Management Suite, которое автоматически обнаруживает компоненты приложений в системах Windows и Linux и сопоставляет взаимодействие между службами. В этой статье содержатся подробные сведения о развертывании схемы услуги в вашей среде и приведены разнообразные сценарии ее использования."
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
ms.openlocfilehash: 0da0231f1a6c01ddd95ce7872e0e4aa47dc61f1b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="configure-service-map-in-operations-management-suite"></a>Настройка схемы услуги в Operations Management Suite
Служба схемы услуги автоматически обнаруживает компоненты приложений в системах Windows и Linux и сопоставляет взаимодействие между службами. Она позволяет рассматривать серверы как взаимосвязанные системы, предоставляющие важные службы. Схема услуги отображает сведения о подключениях между серверами, процессами и портами в любой подключенной по протоколу TCP архитектуре без дополнительной настройки. Пользователям требуется только установить агент.

В этой статье подробно описывается настройка схемы услуги и подключение агентов. Сведения об использовании схемы услуги см. в статье [Использование решения схемы услуги в Operations Management Suite](operations-management-suite-service-map.md).

## <a name="dependency-agent-downloads"></a>Скачиваемые файлы агента зависимостей
| Файл | ОС | Version (версия) | SHA-256 |
|:--|:--|:--|:--|
| [InstallDependencyAgent-Windows.exe](https://aka.ms/dependencyagentwindows) | Windows | 9.0.5 | 73B3F6A2A76A08D58F72A550947FF839B588591C48E6EDDD6DDF73AA3FD82B43 |
| [InstallDependencyAgent-Linux64.bin](https://aka.ms/dependencyagentlinux) | Linux | 9.0.5 | A1BAD0B36EBF79F2B69113A07FCF48C68D90BD169C722689F9C83C69FC032371 |


## <a name="connected-sources"></a>Подключенные источники
Схема услуги получает данные от агента зависимостей Майкрософт. Агент зависимостей является зависимым от агента OMS в плане подключений к Operations Management Suite. Это означает, что сначала на сервере нужно установить и настроить агент OMS, после чего можно будет установить агент зависимостей. В приведенной ниже таблице описаны подключенные источники, которые поддерживаются решением схемы услуги.

| Подключенный источник | Поддерживаются | Описание |
|:--|:--|:--|
| Агенты Windows | Да | Служба схемы услуги анализирует и собирает данные с компьютеров с агентами Windows. <br><br>Помимо [агента OMS](../log-analytics/log-analytics-windows-agents.md) для агентов Windows необходим агент зависимостей Майкрософт. Полный список версий операционных систем см. в разделе [Поддерживаемые операционные системы](#supported-operating-systems). |
| Агенты Linux | Да | Служба схемы услуги анализирует и собирает данные с компьютеров с агентами Linux. <br><br>Помимо [агента OMS](../log-analytics/log-analytics-linux-agents.md) для агентов Linux необходим агент зависимостей Майкрософт. Полный список версий операционных систем см. в разделе [Поддерживаемые операционные системы](#supported-operating-systems). |
| Группа управления System Center Operations Manager | Да | Служба схемы услуги анализирует и собирает данные из агентов Windows и Linux в подключенной [группе управления System Center Operations Manager](../log-analytics/log-analytics-om-agents.md). <br><br>Требуется прямое подключение из агента System Center Operations Manager к Operations Management Suite. Данные пересылаются из группы управления в репозиторий Operations Management Suite.|
| Учетная запись хранения Azure. | Нет | Служба схемы услуги собирает данные с компьютеров с агентом, поэтому данные из службы хранилища Azure не собираются. |

Схема услуги поддерживает только 64-разрядные платформы.

В ОС Windows System Center Operations Manager и Operations Management Suite используют Microsoft Monitoring Agent (MMA) для сбора и отправки данных мониторинга. (В зависимости от контекста этот агент называется агентом System Center Operations Manager, агентом OMS, агентом Log Analytics, MMA или прямым агентом.) System Center Operations Manager и Operations Management Suite предоставляют различные готовые к использованию версии MMA. В каждой из этих версий предусмотрена возможность отправлять отчеты в System Center Operations Manager, Operations Management Suite или в оба решения.  

В ОС Linux агент OMS для Linux собирает и отправляет данные мониторинга в Operations Management Suite. Схему услуги можно использовать на серверах с прямыми агентами OMS или на серверах, подключенных к Operations Management Suite через группы управления System Center Operations Manager.  

В этой статье мы будем называть все эти агенты — как в Linux, так и в Windows, подключенные к группе управления System Center Operations Manager или непосредственно к Operations Management Suite — агентами OMS. Имя конкретного развернутого агента будет использоваться, только если оно требуется в контексте.

Агент схемы услуги самостоятельно не передает данные и не требует внесения изменений в брандмауэры или порты. Данные схемы услуги всегда передаются агентом OMS в Operations Management Suite напрямую или через шлюз OMS.

![Агенты схемы услуги](media/oms-service-map/agents.png)

Если вы являетесь пользователем System Center Operations Manager с группой управления, подключенной к Operations Management Suite:

- Если у ваших агентов System Center Operations Manager есть доступ к Operations Management Suite через Интернет, никаких дополнительных настроек не требуется.  
- Если у агентов System Center Operations Manager нет доступа к Operations Management Suite через Интернет, необходимо настроить шлюз OMS для работы с System Center Operations Manager.
  
При использовании прямого агента OMS необходимо настроить агент OMS для подключения к Operations Management Suite или шлюзу OMS. Шлюз OMS можно скачать в [Центре загрузки Майкрософт](https://www.microsoft.com/download/details.aspx?id=52666).

### <a name="management-packs"></a>Пакеты управления
Если схема услуги активирована в рабочей области Operations Management Suite, то на все серверы в этой рабочей области отправляется пакет управления размером 300 КБ. Если агенты System Center Operations Manager используются в [подключенной группе управления](../log-analytics/log-analytics-om-agents.md), то пакет управления схемы услуги развертывается из System Center Operations Manager. Если агенты подключены напрямую, пакет управления доставляется с помощью Operations Management Suite.

Пакет управления называется Microsoft.IntelligencePacks.ApplicationDependencyMonitor. Он записывается в папку %Programfiles%\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs\. Источник данных, используемый пакетом управления, — %Program files%\Microsoft Monitoring Agent\Agent\Health Service State\Resources\<Автоматически_созданный_идентификатор>\Microsoft.EnterpriseManagement.Advisor.ApplicationDependencyMonitorDataSource.dll.

## <a name="installation"></a>Установка
### <a name="install-the-dependency-agent-on-microsoft-windows"></a>Установка агента зависимостей в Microsoft Windows
Для установки или удаления агента требуются права администратора.

Агент зависимостей устанавливается на компьютерах Windows с помощью файла InstallDependencyAgent-Windows.exe. Если запустить этот исполняемый файл без параметров, запустится мастер для установки в интерактивном режиме.  

Выполните приведение шаги, чтобы установить агент зависимостей на каждом компьютере Windows.

1.  Установите агент OMS, выполнив инструкции в разделе [Подключение компьютеров Windows к службе Log Analytics в Azure](../log-analytics/log-analytics-windows-agents.md).
2.  Скачайте агент Windows и запустите его с помощью следующей команды. <br>`InstallDependencyAgent-Windows.exe`
3.  Следуйте инструкциям мастера для установки агента.
4.  Если агент зависимостей не запускается, просмотрите подробные сведения об ошибке в записях журналов. В агентах Windows каталогом журналов является %Programfiles%\Microsoft Dependency Agent\logs. 

#### <a name="windows-command-line"></a>Командная строка Windows
Используйте параметры из следующей таблицы для установки из командной строки. Чтобы просмотреть список параметров установки, запустите установщик с параметром /? /? следующим образом.

    InstallDependencyAgent-Windows.exe /?

| Параметр | Описание |
|:--|:--|
| /? | Получение списка параметров командной строки. |
| /S | Выполняет автоматическую установку без вывода сообщений для пользователя. |

Файлы для агента зависимостей Windows по умолчанию размещаются в папке C:\Program Files\Microsoft Dependency Agent.

### <a name="install-the-dependency-agent-on-linux"></a>Установка агента зависимостей в Linux
Для установки или настройки агента требуется доступ с правами привилегированного пользователя.

Агент зависимостей устанавливается на компьютерах Linux с помощью файла InstallDependencyAgent-Linux64.bin. Это скрипт оболочки с самоизвлекающимся двоичным файлом. Вы можете запустить этот файл с помощью sh или добавить разрешения на выполнение в сам файл.
 
Выполните приведение шаги, чтобы установить агент зависимостей на каждом компьютере Linux.

1.  Установите агент OMS, выполнив инструкции, приведенные в статье [Подключение компьютеров Linux к Operations Management Suite (OMS)](https://technet.microsoft.com/library/mt622052.aspx).
2.  Установите агент зависимостей Linux с правами привилегированного пользователя, используя следующую команду:<br>`sh InstallDependencyAgent-Linux64.bin`
3.  Если агент зависимостей не запускается, просмотрите подробные сведения об ошибке в записях журналов. В агентах Linux каталог журналов находится в расположении /var/opt/microsoft/dependency-agent/log.

Чтобы просмотреть список параметров установки, запустите программу установки с параметров -help указанным ниже образом.

    InstallDependencyAgent-Linux64.bin -help

| Параметр | Описание |
|:--|:--|
| -help | Получение списка параметров командной строки. |
| -s | Выполняет автоматическую установку без вывода сообщений для пользователя. |
| --check | Проверяет разрешения и операционную систему, но не устанавливает агент. |

Файлы для агента зависимостей размещаются в следующих каталогах.

| Файлы | Расположение |
|:--|:--|
| Основные файлы | /opt/microsoft/dependency-agent |
| Файлы журналов | /var/opt/microsoft/dependency-agent/log |
| Файлы конфигурации | /etc/opt/microsoft/dependency-agent/config |
| Исполняемые файлы службы | /opt/microsoft/dependency-agent/bin/microsoft-dependency-agent<br>/opt/microsoft/dependency-agent/bin/microsoft-dependency-agent-manager |
| Двоичные файлы хранилища | /var/opt/microsoft/dependency-agent/storage |

## <a name="installation-script-examples"></a>Примеры скриптов установки
Чтобы легко развернуть агент зависимостей сразу на нескольких серверах, можно использовать скрипт. Для скачивания и установки агента зависимостей в Windows или Linux можно использовать приведенные ниже примеры скриптов.

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
Чтобы развернуть агент зависимостей посредством Desired State Configuration, можно использовать модуль xPSDesiredStateConfiguration и небольшой фрагмент кода, как показано ниже.
```
configuration ServiceMap {

Import-DscResource -ModuleName xPSDesiredStateConfiguration

$DAPackageLocalPath = "C:\InstallDependencyAgent-Windows.exe"

Node localhost
{ 
    # Download and install the Dependency Agent
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
### <a name="uninstall-the-dependency-agent-on-windows"></a>Удаление агента зависимостей в Windows
Администратор может удалить агент зависимостей для Windows через панель управления.

Для удаления агента зависимостей администратор может также запустить файл %Programfiles%\Microsoft Dependency Agent\Uninstall.exe.

### <a name="uninstall-the-dependency-agent-on-linux"></a>Удаление агента зависимостей в Linux
Чтобы полностью удалить агент зависимостей в Linux, необходимо удалить сам агент и соединитель, который автоматически устанавливается с агентом. Удалить и то, и другое одновременно можно с помощью одной команды.

    rpm -e dependency-agent dependency-agent-connector

## <a name="troubleshooting"></a>Устранение неполадок
Если при установке или запуске схемы услуги возникли проблемы, в этом разделе приводятся сведения, которые могут помочь вам. Если по-прежнему не удается устранить проблему, обратитесь в службу поддержки Майкрософт.

### <a name="dependency-agent-installation-problems"></a>Проблемы при установке агента зависимостей
#### <a name="installer-asks-for-a-reboot"></a>Установщик запрашивает перезагрузку
При установке или удалении агент зависимостей *обычно* не требует перезагрузки. Однако в некоторых редких случаях для продолжения установки Windows Server требуется перезагрузить. Это происходит, когда зависимость (как правило, распространяемые компоненты Microsoft VC ++) требует перезагрузки из-за заблокированного файла.

#### <a name="message-unable-to-install-dependency-agent-visual-studio-runtime-libraries-failed-to-install-code--codenumber-appears"></a>Сообщение "Не удалось установить агент зависимостей: сбой установки библиотек среды выполнения Visual Studio (код = [номер_кода])"

Агент зависимостей Майкрософт создан на основе библиотек среды выполнения Microsoft Visual Studio. Если во время установки этих библиотек возникла проблема, вы получите сообщение. 

Установщики библиотек среды выполнения создают журналы в папке %LOCALAPPDATA%\temp. Файл будет иметь вид dd_vcredist_arch_yyyymmddhhmmss.log, где вместо *arch* будет указано x86 или amd64, а вместо *yyyymmddhhmmss* — дата и время создания журнала (в 24-часовом формате). В журнале содержатся подробные сведения о проблеме, из-за которой блокируется установка.

Сначала лучше всего установить [последнюю версию библиотек среды выполнения](https://support.microsoft.com/help/2977003/the-latest-supported-visual-c-downloads).

В таблице ниже приведены некоторые номера кодов и рекомендации по устранению проблем.

| Код | Описание | Способы устранения: |
|:--|:--|:--|
| 0x17 | Установщику библиотек требуется обновление Windows, которое не было установлено. | Проверьте сведения в последнем журнале установщика библиотек.<br><br>Если после ссылки на Windows8.1-KB2999226-x64.msu следует строка "Ошибка 0x80240017: не удалось выполнить пакет MSU", значит, не установлены необходимые компоненты для установки обновления KB2999226. Следуйте инструкциям в разделе предварительных требований статьи [Обновление для универсальной среды выполнения C в Windows](https://support.microsoft.com/kb/2999226). Может потребоваться запустить Центр обновления Windows и несколько раз выполнить перезагрузку, чтобы установить необходимые компоненты.<br><br>Запустите установщик агента зависимостей Microsoft. |

### <a name="post-installation-issues"></a>Проблемы после установки
#### <a name="server-doesnt-appear-in-service-map"></a>Сервер не отображается в службе схемы услуги
Если агент зависимостей успешно установлен, но в решении "Схема услуги" не отображается сервер, ответьте на следующие вопросы:
* Успешно ли установлен агент зависимостей? Для этого проверьте, установлена и запущена ли служба.<br><br>
**Windows**: найдите службу с именем "Агент зависимостей (Майкрософт)".<br>
**Linux**: найдите выполняющийся процесс microsoft-dependency-agent.

* Используете ли вы [ценовую категорию "Бесплатный" Operations Management Suite и Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-add-solutions#offers-and-pricing-tiers)? План "Бесплатный" предусматривает использование пяти уникальных серверов решения "Схема услуги". Все последующие серверы не будут отображаться в решении "Схема услуги", даже если предыдущие пять больше не отправляют данные.

* Отправляет ли сервер данные журналов и данные по производительности в Operations Management Suite? Перейдите к поиску по журналам и выполните следующий запрос для своего компьютера: 

        * Computer="<your computer name here>" | measure count() by Type
        
  Вы получили множество событий в результатах? Это последние данные? В этом случае агент OMS работает правильно и обменивается данными со службой Operations Management Suite. В противном случае проверьте агент OMS на сервере. См. статью [Устранение неполадок агента OMS для Windows](https://support.microsoft.com/help/3126513/how-to-troubleshoot-operations-management-suite-onboarding-issues) или [Устранение неполадок агента OMS для Linux](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/Troubleshooting.md).

#### <a name="server-appears-in-service-map-but-has-no-processes"></a>Сервер отображается в решении "Схема услуги", но для него нет процессов
Если сервер отображается в решении "Схема услуги", но для него нет процессов или данных о подключении, это означает, что агент зависимостей установлен и запущен, но не удалось загрузить драйвер ядра. 

Проверьте файл C:\Program Files\Microsoft Dependency Agent\logs\wrapper.log (Windows) или /var/opt/microsoft/dependency-agent/log/service.log (Linux). В последних строках файла должно быть указано, почему не удалось загрузить ядро. Например, если вы обновили ядро, оно может не поддерживаться в Linux.

## <a name="data-collection"></a>Сбор данных
Каждый агент передает примерно 25 МБ данных в день в зависимости от сложности зависимостей системы. Каждый агент отправляет данные зависимостей схемы услуги каждые 15 секунд.  

Агент зависимостей обычно потребляет 0,1 % системной памяти и 0,1 % ресурсов ЦП системы.

## <a name="supported-azure-regions"></a>Поддерживаемые регионы Azure
Схема услуги в настоящее время доступна в следующих регионах Azure:
- Восток США
- Западная Европа
- Западно-центральная часть США


## <a name="supported-operating-systems"></a>Поддерживаемые операционные системы
В следующих разделах представлены поддерживаемые операционные системы для агента зависимостей. Схема услуги не поддерживает 32-разрядные архитектуры операционных систем.

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
- Нестандартные версии ядра, такие как PAE и Xen, не поддерживаются ни в одном дистрибутиве Linux. Например, система со строкой версии "2.6.16.21-0.8-xen" не поддерживается.
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
Корпорация Майкрософт автоматически собирает данные об использовании и производительности с помощью службы схемы услуги. Эти данные используются, чтобы улучшить качество, повысить безопасность и целостность службы схемы услуги. Они включают в себя сведения о конфигурации программного обеспечения, такие как версия операционной системы. Они также включают в себя IP-адрес, DNS-имя и имя рабочей станции с целью предоставления возможностей для точного и эффективного устранения неполадок. Корпорация Майкрософт не собирает сведения об именах, адресах и другую контактную информацию.

Дополнительные сведения о сборе и использовании данных см. в [заявлении о конфиденциальности служб Microsoft Online Services](https://go.microsoft.com/fwlink/?LinkId=512132).



## <a name="next-steps"></a>Дальнейшие действия
- Узнайте, как [использовать схему услуги](operations-management-suite-service-map.md) после ее развертывания и настройки.
