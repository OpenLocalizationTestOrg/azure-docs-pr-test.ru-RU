---
title: "aaaCollect и проанализировать сообщения системного журнала в аналитику журнала OMS | Документы Microsoft"
description: "Syslog — это протокол ведения журнала событий, общие tooLinux. В этой статье описывается tooconfigure сбора сообщений Syslog в службе анализа журналов и подробные сведения о записи hello их создания в репозитории OMS hello."
services: log-analytics
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: f1d5bde4-6b86-4b8e-b5c1-3ecbaba76198
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/12/2017
ms.author: magoedte;bwren
ms.openlocfilehash: 8bfa0bca3f2f18287d1352c98bbaa2a70e41e276
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="syslog-data-sources-in-log-analytics"></a>Источники данных системного журнала в Log Analytics
Syslog — это протокол ведения журнала событий, общие tooLinux.  Приложения будет отправлять сообщения, хранящиеся на локальном компьютере hello или доставить tooa системного журнала сборщика.  При установке агента OMS для Linux hello настраивает hello локального системного журнала управляющей программы tooforward сообщения toohello агента.  Hello агент отправляет сообщение hello tooLog Analytics которых создается соответствующая запись в репозиторий OMS hello.  

> [!NOTE]
> Служба аналитики журналов поддерживает набор сообщений, отправленных rsyslog или syslog-ng, где rsyslog — управляющая программа по умолчанию hello. управляющая программа syslog по умолчанию Hello в версии 5 Red Hat Enterprise Linux, CentOS и Oracle Linux (sysklog) версии не поддерживается для сбора событий syslog. Здравствуйте, toocollect данных syslog из этой версии данных дистрибутивов [управляющую программу rsyslog](http://rsyslog.com) должен быть установлен и настроен tooreplace sysklog.
>
>

![Сбор сообщений системного журнала](media/log-analytics-data-sources-syslog/overview.png)

## <a name="configuring-syslog"></a>Настройка системного журнала
Hello агента OMS для Linux собираются только события с помощью средства hello и степени серьезности, которые указаны в его конфигурации.  Syslog можно настроить с помощью портала OMS hello или управление файлами конфигурации на агенты Linux.

### <a name="configure-syslog-in-hello-oms-portal"></a>Настройка системного журнала на портале OMS hello
Настроить Syslog из hello [меню данные в параметры журнала аналитика](log-analytics-data-sources.md#configuring-data-sources).  Эта конфигурация будет доставлено toohello файл конфигурации на каждом агенте Linux.

Можно добавить новое устройство, введя его имя и нажав кнопку **+**.  Для каждой территории будут собираться только сообщения с уровнем серьезности hello выбран.  Проверьте hello степени серьезности для определенной территории hello, которые должны toocollect.  Любые дополнительные критерии не может предоставить toofilter сообщений.

![Настройка системного журнала](media/log-analytics-data-sources-syslog/configure.png)

По умолчанию все изменения конфигурации автоматически размещаемых tooall агентов.  Если вы хотите tooconfigure Syslog вручную на каждом агенте Linux, затем снимите флажок hello *применить указанную ниже компьютеры Linux toomy конфигурации*.

### <a name="configure-syslog-on-linux-agent"></a>Настройка системного журнала на агенте Linux
Здравствуйте, когда [агент OMS установлен на клиентском компьютере Linux](log-analytics-linux-agents.md), он устанавливает файл конфигурации по умолчанию syslog, определяющий помещение hello и серьезность hello сообщения, которые будут собраны.  Можно изменить эту конфигурацию файла toochange hello.  файл конфигурации Hello отличается в зависимости от hello управляющей программы, hello клиент установил системного журнала.

> [!NOTE]
> При изменении конфигурации syslog hello, необходимо перезапустить управляющая программа syslog hello для эффекта tootake изменения hello.
>
>

#### <a name="rsyslog"></a>rsyslog
Hello rsyslog файл конфигурации расположен в **/etc/rsyslog.d/95-omsagent.conf**.  Его содержимое по умолчанию приведено ниже.  В этом разделе собраны syslog-сообщения, отправленные hello локального агента для всех средств с уровнем «предупреждение» или более поздней версии.

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

Это средство управления можно удалить, удалив его разделе файла конфигурации hello.  Можно ограничить hello степени серьезности, которые собираются для определенной территории, изменив запись этого средства.  Например toomessages toolimit hello пользователя территории с уровнем серьезности ошибки или более поздней версии необходимо изменить эту строку hello конфигурации файла toohello следующие:

    user.error    @127.0.0.1:25224


#### <a name="syslog-ng"></a>syslog-ng
файл конфигурации Hello для syslog-ng — место, в **/etc/syslog-ng/syslog-ng.conf**.  Его содержимое по умолчанию приведено ниже.  В этом разделе собраны syslog-сообщения, отправленные hello локального агента для всех средств и все уровни.   

    #
    # Warnings (except iptables) in one file:
    #
    destination warn { file("/var/log/warn" fsync(yes)); };
    log { source(src); filter(f_warn); destination(warn); };

    #OMS_Destination
    destination d_oms { udp("127.0.0.1" port(25224)); };

    #OMS_facility = auth
    filter f_auth_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(auth); };
    log { source(src); filter(f_auth_oms); destination(d_oms); };

    #OMS_facility = authpriv
    filter f_authpriv_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(authpriv); };
    log { source(src); filter(f_authpriv_oms); destination(d_oms); };

    #OMS_facility = cron
    filter f_cron_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(cron); };
    log { source(src); filter(f_cron_oms); destination(d_oms); };

    #OMS_facility = daemon
    filter f_daemon_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(daemon); };
    log { source(src); filter(f_daemon_oms); destination(d_oms); };

    #OMS_facility = kern
    filter f_kern_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(kern); };
    log { source(src); filter(f_kern_oms); destination(d_oms); };

    #OMS_facility = local0
    filter f_local0_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(local0); };
    log { source(src); filter(f_local0_oms); destination(d_oms); };

    #OMS_facility = local1
    filter f_local1_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(local1); };
    log { source(src); filter(f_local1_oms); destination(d_oms); };

    #OMS_facility = mail
    filter f_mail_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(mail); };
    log { source(src); filter(f_mail_oms); destination(d_oms); };

    #OMS_facility = syslog
    filter f_syslog_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(syslog); };
    log { source(src); filter(f_syslog_oms); destination(d_oms); };

    #OMS_facility = user
    filter f_user_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(user); };
    log { source(src); filter(f_user_oms); destination(d_oms); };

Это средство управления можно удалить, удалив его разделе файла конфигурации hello.  Можно ограничить hello степени серьезности, которые собираются для определенной территории, удалив их из списка.  Например, toolimit hello пользователя средство toojust сообщения, предупреждения и критической ситуации, необходимо изменить этот раздел hello конфигурации файла toohello следующие:

    #OMS_facility = user
    filter f_user_oms { level(alert,crit) and facility(user); };
    log { source(src); filter(f_user_oms); destination(d_oms); };


### <a name="collecting-data-from-additional-syslog-ports"></a>Сбор данных из дополнительных портов системного журнала
агент OMS Здравствуй прослушивает сообщения системного журнала на локальном клиенте hello через порт 25224.  При установке агента hello, применяется конфигурация syslog по умолчанию и найти в следующие расположения hello:

* rsyslog: `/etc/rsyslog.d/95-omsagent.conf`;
* syslog-ng: `/etc/syslog-ng/syslog-ng.conf`.

Можно изменить номер порта hello, создав два файла конфигурации: FluentD config rsyslog или syslog-ng файл, в зависимости от установки управляющей программы Syslog hello.  

* файл конфигурации FluentD Hello должен быть новый файл, расположенный в: `/etc/opt/microsoft/omsagent/conf/omsagent.d` и замените значение hello hello **порт** запись с вашей другой номер порта.

        <source>
          type syslog
          port %SYSLOG_PORT%
          bind 127.0.0.1
          protocol_type udp
          tag oms.syslog
        </source>
        <filter oms.syslog.**>
          type filter_syslog
        </filter>

* Для rsyslog, необходимо создать новый файл конфигурации, расположенных в: `/etc/rsyslog.d/` и замените hello значение % SYSLOG_PORT % ваш собственный номер порта.  

    > [!NOTE]
    > Если изменить это значение в файле конфигурации hello `95-omsagent.conf`, она будет перезаписана при hello агент применяет конфигурацию по умолчанию.
    >

        # OMS Syslog collection for workspace %WORKSPACE_ID%
        kern.warning              @127.0.0.1:%SYSLOG_PORT%
        user.warning              @127.0.0.1:%SYSLOG_PORT%
        daemon.warning            @127.0.0.1:%SYSLOG_PORT%
        auth.warning              @127.0.0.1:%SYSLOG_PORT%

* Hello syslog-ng конфигурации должен быть изменен путем копирования hello пример конфигурации показан ниже и добавление toohello настраиваемые параметры, измененные hello конец файла конфигурации syslog ng.conf hello расположен в `/etc/syslog-ng/`.  Сделать **не** использовать метки по умолчанию hello **% WORKSPACE_ID % _oms** или **% WORKSPACE_ID_OMS**, определить пользовательские метки toohelp отличить изменения.  

    > [!NOTE]
    > При изменении значения по умолчанию hello в файле конфигурации hello, они будут перезаписаны при hello агент применяет конфигурацию по умолчанию.
    >

        filter f_custom_filter { level(warning) and facility(auth; };
        destination d_custom_dest { udp("127.0.0.1" port(%SYSLOG_PORT%)); };
        log { source(s_src); filter(f_custom_filter); destination(d_custom_dest); };

После завершения изменения hello, hello системного журнала и hello служба агента OMS должен перезапустить toobe tooensure hello конфигурацию изменения вступят в силу.   

## <a name="syslog-record-properties"></a>Свойства записей системного журнала
Системный журнал записей имеют тип **Syslog** и имеющих свойства hello в hello в следующей таблице.

| Свойство | Описание |
|:--- |:--- |
| Компьютер |Компьютер, hello события, собранные из. |
| Facility |Определяет часть hello hello системы, создавшей приветственное сообщение. |
| HostIP |IP-адрес hello компьютер, отправляющий сообщение hello. |
| HostName |Имя системы hello отправляет сообщение hello. |
| SeverityLevel |Уровень серьезности события hello. |
| SyslogMessage |Текст сообщения hello. |
| ProcessID |Идентификатор процесса hello, создавшего сообщение hello. |
| EventTime |Дата и время hello событий был создан. |

## <a name="log-queries-with-syslog-records"></a>Запросы к журналу для получения записей системного журнала
Hello следующей таблице приведены примеры различных журнала запросов, получающих записи Syslog.

| Запрос | Описание |
|:--- |:--- |
| Type=Syslog |Все записи системного журнала. |
| Type=Syslog SeverityLevel=error |Все записи системного журнала с уровнем серьезности "ошибка". |
| Type=Syslog &#124; measure count() by Computer |Число записей системного журнала по компьютеру. |
| Type=Syslog &#124; measure count() by Facility |Число записей системного журнала по устройству. |

>[!NOTE]
> Если рабочую область был обновленного toohello [языка запросов новый журнал аналитики](log-analytics-log-search-upgrade.md), то hello выше запросы будут изменены следующие toohello.

> | Запрос | Описание |
|:--- |:--- |
| syslog |Все записи системного журнала. |
| Syslog &#124; where SeverityLevel == "error" |Все записи системного журнала с уровнем серьезности "ошибка". |
| Syslog &#124; summarize AggregatedValue = count() by Computer |Число записей системного журнала по компьютеру. |
| Syslog &#124; summarize AggregatedValue = count() by Facility |Число записей системного журнала по устройству. |

## <a name="next-steps"></a>Дальнейшие действия
* Дополнительные сведения о [входа выполняет](log-analytics-log-searches.md) tooanalyze hello данные, собранные из источников данных и решений.
* Используйте [настраиваемые поля](log-analytics-custom-fields.md) tooparse данных из системного журнала записей в отдельные поля.
* [Настройка агентов Linux](log-analytics-linux-agents.md) toocollect других типов данных.
