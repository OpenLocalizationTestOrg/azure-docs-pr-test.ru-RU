---
title: "aaaConnect на компьютерах Linux tooOperations Management Suite (OMS) | Документы Microsoft"
description: "В этой статье описывается, как tooconnect компьютеров Linux, размещенные в Azure, другие облачной или локальной tooOMS использование hello агента OMS для Linux."
services: log-analytics
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/21/2017
ms.author: magoedte
ms.openlocfilehash: cb4fc671d0678f9fadc689c6ba7d719213aa61b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-linux-computers-toooperations-management-suite-oms"></a>Подключения на компьютерах Linux tooOperations Management Suite (OMS) 

С помощью Microsoft Operations Management Suite (OMS) можно собирать и использовать данные, созданные на компьютерах под управлением Linux и в контейнерах (например, Docker), расположенных в локальном центре обработки данных как физические серверы или виртуальные машины либо виртуальные машины в облачной службе (например, Amazon Web Services (AWS) или Microsoft Azure). Можно также использовать решений управления, доступных в OMS, такие как отслеживание изменений, изменения в конфигурации tooidentify, и tooproactively обновлений программного обеспечения для управления обновлениями toomanage управление жизненным циклом hello виртуальных машин Linux. 

Hello агента OMS для Linux взаимодействует исходящие с hello службой OMS через TCP-порт 443, а также если hello компьютер подключается toocommunicate tooa брандмауэр или прокси-сервера через Интернет, hello просмотрите [Настройка hello агент для использования с HTTP-прокси сервер или шлюз OMS](#configuring-the-agent-for-use-with-an-http-proxy-server-or-oms-gateway) toounderstand изменения конфигурации, которые необходимо применить toobe.  При наблюдении за hello компьютер с System Center 2016 — Operations Manager или Operations Manager 2012 R2, она может быть многосетевой данных toocollect службы OMS hello и прямой toohello службы; по-прежнему контролироваться с помощью Operations Manager  Компьютеры Linux, отслеживаемые группой управления Operations Manager, интегрированного с OMS, не будут получать конфигурацию для источников данных и пересылать собранные данные через группы управления hello.  агент OMS Hello не может быть настроенный tooreport toomore чем одной рабочей области.  

Если политики безопасности ИТ запретить компьютеры toohello tooconnect вашей сети Интернет, агент hello быть сведения о конфигурации настроенного tooconnect toohello шлюза OMS tooreceive и отправки собранных данных в зависимости от решения hello вами включена. Дополнительные сведения и инструкции по tooconfigure вашего агента OMS для Linux toocommunicate через службу OMS toohello шлюза OMS. в статье [подключения tooOMS компьютеров с помощью шлюза OMS hello](log-analytics-oms-gateway.md).  

Hello следующая диаграмма изображает hello подключению hello управляемыми агентом компьютерами Linux OMS, включая направление hello и порты.

![Схема взаимодействия прямого агента с OMS](./media/log-analytics-agent-linux/log-analytics-agent-linux-communication.png)

## <a name="system-requirements"></a>Требования к системе
Прежде чем начать, просмотрите следующие сведения о tooverify требованиям hello hello.

### <a name="supported-linux-operating-systems"></a>Поддерживаемые операционные системы Linux
официально поддерживаются следующие версии ОС Linux Hello.  Однако hello агента OMS для Linux также можно запустить на других дистрибутивах, которых нет в списке.

* Amazon Linux 2012.09 too2015.09 (x86/x64)
* CentOS Linux 5, 6 и 7 (x86/x64)
* Oracle Linux 5, 6 и 7 (x86/x64)
* Red Hat Enterprise Linux Server 5, 6 и 7 (x86/x64)
* Debian GNU/Linux 6, 7 и 8 (x86/x64)
* Ubuntu 12.04 LTS, 14.04 LTS, 15.04, 15.10, 16.04 LTS (x86/x64)
* SUSE Linux Enterprise Server 11 и 12 (x86/x64)

### <a name="network"></a>Сеть
Hello информацию ниже списке hello прокси-сервера и сведения о конфигурации брандмауэра является обязательным для hello toocommunicate агент Linux в OMS. — Исходящим из службы OMS toohello сети. 

|Ресурс агента| порты; |  
|------|---------|  
|*.ods.opinsights.azure.com | Порт 443|   
|*.oms.opinsights.azure.com | Порт 443|   
|*.blob.core.windows.net/ | Порт 443|   
|*.azure-automation.net | Порт 443|  

### <a name="package-requirements"></a>Требования к пакетам

 **Требуемый пакет**   | **Описание**   | **Минимальная версия**
--------------------- | --------------------- | -------------------
Glibc | Библиотека C GNU   | 2.5-12 
Openssl | Библиотеки OpenSSL | 0.9.8e или 1.0
Curl | Веб-клиент cURL | 7.15.5
Python-ctypes | | 
PAM | Подключаемые модули аутентификации | 

> [!NOTE]
>  Rsyslog или syslog-ng, требуется toocollect syslog-сообщения. управляющая программа syslog по умолчанию Hello в версии 5 Red Hat Enterprise Linux, CentOS и Oracle Linux (sysklog) версии не поддерживается для сбора событий syslog. toocollect данных syslog из этой версии данных дистрибутивов hello rsyslog управляющая программа должна быть установлена и настроена tooreplace sysklog 

Привет agent включает несколько пакетов. Hello файл версии содержит следующие пакеты, работающей hello оболочку пакета с hello `--extract`:

**Package** | **Версия** | **Описание**
----------- | ----------- | --------------
omsagent | 1.4.0 | Hello агент Operations Management Suite для Linux
omsconfig | 1.1.1 | Агент конфигурации для агента OMS hello
omi | 1.2.0 | OMI (Open Management Infrastructure) — облегченная версия сервера CIM
scx | 1.6.3 | Поставщики OMI CIM для метрик производительности операционной системы
apache-cimprov | 1.0.1 | Поставщик мониторинга производительности сервера Apache HTTP Server для OMI. Устанавливается при обнаружении сервера Apache HTTP Server.
mysql-cimprov | 1.0.1 | Поставщик мониторинга производительности сервера MySQL для OMI. Устанавливается при обнаружении сервера MySQL или MariaDB.
docker-cimprov | 1.0.0 | Поставщик Docker для OMI. Устанавливается при обнаружении Docker.

### <a name="compatibility-with-system-center-operations-manager"></a>Совместимость с System Center Operations Manager
Hello агента OMS для Linux использует двоичные файлы агента совместно с System Center Operations Manager агент hello. Если установить hello агента OMS для Linux в системе под управлением Operations Manager, он hello пакеты OMI и SCX на hello компьютера tooa новой версии. В этом выпуске hello OMS и System Center 2016 — совместимы агенты Operations Manager, Operations Manager 2012 R2 для Linux. 

> [!NOTE]
> System Center 2012 SP1 и более ранних версий не в настоящее время несовместимы или не поддерживаются с hello агента OMS для Linux.<br>
> Если hello агента OMS для Linux — установленных tooa компьютера, который в настоящее время не отслеживаются Operations Manager, и затем toomonitor hello компьютер с Operations Manager, необходимо изменить hello [конфигурацию OMI](#enable-the-oms-agent-for-linux-to-report-to-system-center-operations-manager) предыдущего компьютер toodiscovering hello. **Этот шаг является *не* требуется, если агент Operations Manager hello установлен до hello агента OMS для Linux.**

### <a name="system-configuration-changes"></a>Изменения конфигурации системы
После установки hello агента OMS для пакетов Linux, hello следующие дополнительные системные применяются изменения конфигурации. Эти артефакты удаляются при удалении пакета omsagent hello.

* Создается непривилегированный пользователь с именем `omsagent` . Это hello hello omsagent управляющая программа выполняется как.
* В каталоге /etc/sudoers.d/omsagent создается файл sudoers с директивами include. Это разрешает omsagent toorestart hello syslog и omsagent управляющие программы. Если директивы «include» sudo не поддерживаются в версии hello установки sudo, эти записи записываются слишком/д/sudoers.
* Конфигурация syslog Hello — измененные tooforward подмножество событий toohello агента. Дополнительные сведения см. в разделе hello **Настройка сбора данных** ниже

### <a name="upgrade-from-a-previous-release"></a>Обновление предыдущей версии
В этом выпуске поддерживаются обновления версий ниже 1.0.0-47. Выполнение установки hello при hello `--upgrade` команда обновляет все компоненты hello агента toohello последнюю версию.

## <a name="installing-hello-agent"></a>Установка агента hello

В этом разделе описывается, как пакеты tooinstall hello агента OMS для Linux с помощью bunndle, который содержит Debian и об/мин для каждого из компонентов агента hello.  Его можно установить непосредственно или извлечении tooretrieve hello отдельных пакетов.  

Во-первых, требуется свой идентификатор рабочей области OMS и ключ, который можно найти с помощью переключения toohello [классический портал OMS](https://mms.microsoft.com).  На hello **Обзор** страницы в верхнем меню выберите hello **параметры**, после чего перейти слишком**соединенными серверами Sources\Linux**.  Вы видите hello значение toohello справа от **идентификатор рабочей области** и **первичный ключ**.  Скопируйте их и вставьте в любой удобный для вас редактор.    

1. Последняя версия hello загрузки [агента OMS для Linux (x64)](https://github.com/Microsoft/OMS-Agent-for-Linux/releases/download/OMSAgent_GA_v1.4.0-45/omsagent-1.4.0-45.universal.x64.sh) или [агента OMS для Linux x86](https://github.com/Microsoft/OMS-Agent-for-Linux/releases/download/OMSAgent_GA_v1.4.0-45/omsagent-1.4.0-45.universal.x86.sh) из GitHub.  
2. Перенос hello соответствующий пакет (x86 или x64) tooyour компьютера Linux с использованием scp или sftp.
3. Установка hello пакета с помощью hello `--install` или `--upgrade` аргумент. 

    > [!NOTE]
    > Если все существующие пакеты установлены, например, если уже установлен агент hello System Center Operations Manager для Linux, используйте hello `--upgrade` аргумент. tooOperations tooconnect Management Suite во время установки, укажите hello `-w <WorkspaceID>` и `-s <Shared Key>` параметров.


#### <a name="tooinstall-and-onboard-directly"></a>tooinstall и подключать напрямую
```
sudo sh ./omsagent-<version>.universal.x64.sh --upgrade -w <workspace id> -s <shared key>
```

#### <a name="tooupgrade-hello-agent-package"></a>пакет агента tooupgrade hello
```
sudo sh ./omsagent-<version>.universal.x64.sh --upgrade
```

#### <a name="tooinstall-and-onboard-tooa-workspace-in-us-government-cloud"></a>tooinstall и встроенного tooa рабочей области в государственных облака
```
sudo sh ./omsagent-<version>.universal.x64.sh --upgrade -w <workspace id> -s <shared key> -d opinsights.azure.us
```

## <a name="configuring-hello-agent-for-use-with-an-http-proxy-server-or-oms-gateway"></a>Настройка агента hello для использования с OMS шлюза или прокси-сервера HTTP
Hello агента OMS для Linux поддерживает взаимодействие через прокси-сервер HTTP или HTTPS, или служба OMS toohello OMS шлюза.  Поддерживается анонимная и базовая аутентификация (с именем пользователя и паролем).  

### <a name="proxy-configuration"></a>Конфигурация прокси-сервера
значение конфигурации прокси-сервера Hello имеет hello, используя синтаксис:

`[protocol://][user:password@]proxyhost[:port]`

Свойство|Описание
-|-
Протокол|HTTP или HTTPS
user|Необязательное имя пользователя для аутентификации прокси-сервера
пароль|Необязательный пароль для аутентификации прокси-сервера
proxyhost|Адрес или полное доменное имя сервера прокси-сервера hello и OMS шлюза
порт|Номер порта, необязательно для hello прокси сервера и OMS шлюза

Например: `http://user01:password@proxy01.contoso.com:8080`

Hello прокси-сервер можно указать во время установки или путем изменения файла конфигурации proxy.conf hello после установки.   

### <a name="specify-proxy-configuration-during-installation"></a>Определение конфигурации прокси-сервера во время установки
Hello `-p` или `--proxy` аргумент для установки пакета hello omsagent задает toouse конфигурации прокси-сервера hello. 

```
sudo sh ./omsagent-<version>.universal.x64.sh --upgrade -p http://<proxy user>:<proxy password>@<proxy address>:<proxy port> -w <workspace id> -s <shared key>
```

### <a name="define-hello-proxy-configuration-in-a-file"></a>Определения в файле конфигурации прокси-сервера hello
Hello конфигурацию прокси-сервера можно задать в файлах hello `/etc/opt/microsoft/omsagent/proxy.conf` и `/etc/opt/microsoft/omsagent/conf/proxy.conf `. непосредственно создать или изменить файлы Hello, но их разрешения должны быть обновленные toogrant hello omiuser пользователя разрешения на чтение файлов hello. Например:
```
proxyconf="https://proxyuser:proxypassword@proxyserver01:8080"
sudo echo $proxyconf >>/etc/opt/microsoft/omsagent/proxy.conf
sudo chown omsagent:omiusers /etc/opt/microsoft/omsagent/proxy.conf
sudo chmod 600 /etc/opt/microsoft/omsagent/proxy.conf /etc/opt/microsoft/omsagent/conf/proxy.conf  
sudo /opt/microsoft/omsagent/bin/service_control restart [<workspace id>]
```

### <a name="removing-hello-proxy-configuration"></a>Удаление конфигурации прокси-сервера hello
tooremove ранее определенного прокси-конфигурацию и восстановить подключение toodirect, удалите файл proxy.conf hello:
```
sudo rm /etc/opt/microsoft/omsagent/proxy.conf /etc/opt/microsoft/omsagent/conf/proxy.conf
sudo /opt/microsoft/omsagent/bin/service_control restart 
```

## <a name="onboarding-with-operations-management-suite"></a>Подключение к Operations Management Suite
Если идентификатор рабочей области и ключ не был предоставлен во время установки пакета hello, hello агент должен быть впоследствии зарегистрирован Operations Management Suite.

### <a name="onboarding-using-hello-command-line"></a>С помощью командной строки hello адаптации
Выполните команду omsadmin.sh hello, указав идентификатор hello рабочей области и ключа для рабочей области. Эту команду должен выполнять привилегированный пользователь (sudo):
```
cd /opt/microsoft/omsagent/bin
sudo ./omsadmin.sh -w <WorkspaceID> -s <Shared Key>
```

### <a name="onboarding-using-a-file"></a>Подключение с помощью файла
1.  Создайте файл hello `/etc/omsagent-onboard.conf`. Hello файл должен быть для чтения и записи для корня.
`sudo vi /etc/omsagent-onboard.conf`
2.  Вставьте следующие строки в файле hello, указав идентификатор рабочей области и общим ключом hello:

        WORKSPACE_ID=<WorkspaceID>  
        SHARED_KEY=<Shared Key>  
   
3.  Выполните следующие команды tooOnboard tooOMS hello.`sudo /opt/microsoft/omsagent/bin/omsadmin.sh`
4.  для успешного освоения удаляется файл Hello.

## <a name="enable-hello-oms-agent-for-linux-tooreport-toosystem-center-operations-manager"></a>Включить hello агента OMS для Linux tooreport tooSystem Center Operations Manager
Выполните следующие шаги tooconfigure hello агента OMS для группы управления System Center Operations Manager tooa tooreport Linux hello.  

1. Измените файл hello`/etc/opt/omi/conf/omiserver.conf`
2. Убедитесь, что hello строки, начинающиеся с **httpsport =** hello порт 1270. Например: `httpsport=1270`.
3. Перезапустите сервер OMI hello:`sudo /opt/omi/bin/service_control restart`

## <a name="agent-logs"></a>Журналы агента
Здравствуйте журналы для hello агента OMS для Linux можно найти в: `/var/opt/microsoft/omsagent/<workspace id>/log/` hello журналы для hello omsconfig (конфигурация агента) можно найти в: `/var/opt/microsoft/omsconfig/log/` журналы для компонентов OMI и SCX hello (которые предоставляют данные метрик производительности) можно найти в:`/var/opt/omi/log/ and /var/opt/microsoft/scx/log`

### <a name="log-rotation-configuration"></a>Конфигурация чередования журналов##
Поворот конфигурации Hello журналов для omsagent можно найти в:`/etc/logrotate.d/omsagent-<workspace id>`

Ниже перечислены параметры по умолчанию Hello 
```
/var/opt/microsoft/omsagent/<workspace id>/log/omsagent.log {
    rotate 5
    missingok
    notifempty
    compress
    size 50k
    copytruncate
}
```

## <a name="uninstalling-hello-oms-agent-for-linux"></a>При удалении hello агента OMS для Linux
Hello пакетов агента можно удалить с запущенной hello sh-файла пакета с hello `--purge` аргументом, который полностью удаляет с компьютера hello hello агента и его конфигурации.   

```
> sudo rpm -e omsconfig
> sudo rpm -e omsagent
> sudo /opt/microsoft/scx/bin/uninstall
```

## <a name="troubleshooting"></a>Устранение неполадок

### <a name="issue-unable-tooconnect-through-proxy-toooms"></a>Проблема: Не удается tooconnect через tooOMS прокси-сервера

#### <a name="probable-causes"></a>Возможные причины
* неверно указано во время адаптации прокси Hello
* Hello конечных точек службы OMS не являются whitelistested в центре обработки данных 

#### <a name="resolutions"></a>Способы устранения
1. Toohello Reonboard службой OMS с hello агента OMS для Linux, используя следующую команду с параметром hello hello `-v` включена. Это позволяет подробные выходные данные агента hello подключение через прокси-сервера hello toohello службой OMS. 
`/opt/microsoft/omsagent/bin/omsadmin.sh -w <OMS Workspace ID> -s <OMS Workspace Key> -p <Proxy Conf> -v`

2. Просмотрите раздел hello [Настройка hello агент для использования с прокси-сервер HTTP server(#configuring the-agent-for-use-with-a-http-proxy-server) tooverify правильно настроены hello toocommunicate агента через прокси-сервер.    
* Проверьте, hello следующих конечных точек службы OMS, входят:

    |Ресурс агента| порты; |  
    |------|---------|  
    |*.ods.opinsights.azure.com | Порт 443|   
    |*.oms.opinsights.azure.com | Порт 443|   
    |ods.systemcenteradvisor.com | Порт 443|   
    |*.blob.core.windows.net/ | Порт 443|   

### <a name="issue-you-receive-a-403-error-when-trying-tooonboard"></a>Проблема: Появляется ошибка 403 при попытке tooonboard

#### <a name="probable-causes"></a>Возможные причины
* На сервере Linux установлены неправильные время и дата. 
* Используется недопустимый идентификатор или ключ рабочей области.

#### <a name="resolution"></a>Способы устранения:

1. Проверьте время hello на сервер Linux с датой команда hello. Если время hello +/-15 минут от текущего времени, адаптации завершается ошибкой. toocorrect этой обновления hello и часовой пояс сервера Linux. 
2. Убедитесь, что вы установили последнюю версию hello hello агента OMS для Linux.  Новейшая версия Hello теперь отображается уведомление, если отклонение во времени является причиной сбоя адаптации hello.
3. Reonboard, используя правильный идентификатор рабочей области и ключ рабочей области, следующие инструкции по установке hello ранее в этом разделе.

### <a name="issue-you-see-a-500-and-404-error-in-hello-log-file-right-after-onboarding"></a>Проблема: Появится 500 и 404 об ошибке в файле журнала hello сразу же после адаптации
Это известная проблема, которая возникает при первой передаче данных Linux в рабочую область OMS. Это не влияет на отправляемые данные и не мешает работе службы.

### <a name="issue--you-are-not-seeing-any-data-in-hello-oms-portal"></a>Проблема: Не отображаются все данные на портале OMS hello

#### <a name="probable-causes"></a>Возможные причины

- Не удалось выполнить toohello адаптации службой OMS
- Заблокированные соединения toohello службой OMS
- Создана резервная копия данных агента OMS для Linux.

#### <a name="resolutions"></a>Способы устранения
1. Проверьте адаптации hello службой OMS успешность путем проверки существования hello следующий файл:`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf`
2. С помощью hello Reonboard `omsadmin.sh` инструкции командной строки
3. Если используется прокси-сервер, см. инструкции по разрешению прокси toohello ранее указанного.
4. В некоторых случаях если hello агента OMS для Linux не может взаимодействовать со службой OMS hello данных в агенте hello — в очереди toohello полный буфер размером, равным 50 МБ. Hello агента OMS для Linux необходимо перезапустить, выполнив следующую команду hello: `/opt/microsoft/omsagent/bin/service_control restart [<workspace id>]`. 

    >[!NOTE]
    >Эта проблема исправлена в агенте версии 1.1.0-28 и выше.
> 