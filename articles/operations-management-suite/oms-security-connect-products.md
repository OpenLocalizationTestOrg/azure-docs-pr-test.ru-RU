---
title: "aaaConnecting вашего решения аудита и безопасности продуктов toohello безопасности Operations Management Suite (OMS) | Документы Microsoft"
description: "В этом документе помогает вам tooconnect вашей безопасности продуктов tooOperations Management Suite безопасности и аудита решения, с помощью общего формата событий."
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: 46eee484-e078-4bad-8c89-c88a3508f6aa
ms.service: operations-management-suite
ms.custom: oms-security
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2017
ms.author: yurid
ms.openlocfilehash: 0f4b372d0379987c4e249628a3c8d52733be65c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connecting-your-security-products-toohello-operations-management-suite-oms-security-and-audit-solution"></a>Подключение вашего решения аудита и безопасности продуктов toohello безопасности Operations Management Suite (OMS) 
В этом документе помогает подключить продуктов безопасности в hello OMS безопасности и аудита решения. поддерживаются следующие источники Hello:

- события CEF;
- события Cisco ASA.


## <a name="what-is-cef"></a>Что такое CEF?
Общий формат событий (CEF) является стандартизированный формат на основе сообщения системного журнала, используемые многие поставщики tooallow событий взаимодействие с безопасностью между разными платформами. OMS поддержка безопасности и аудита решения с помощью CEF, позволяющий tooconnect продуктов безопасности OMS безопасности приема данных. 

Подключившись к tooOMS источника данных, являются может tootake преимуществами hello следующие возможности, которые являются частью этой платформе:

- поиск и корреляция;
- Аудит
- Предупреждение
- Аналитика угроз
- Важные проблемы

## <a name="collection-of-security-solution-logs"></a>сбор журналов решения для защиты.

Решение для защиты OMS поддерживает сбор журналов с использованием CEF в системных журналах и журналах [Cisco ASA](https://blogs.technet.microsoft.com/msoms/2016/08/25/add-your-cisco-asa-logs-to-oms-security/). В этом примере hello источник (компьютер, который создает журналы hello) — управляющая программа syslog-ng компьютере Linux и hello целевой объект — безопасность OMS. компьютер Linux tooprepare hello, вам потребуется hello tooperform следующие задачи:

- Загрузите hello агента OMS для Linux, версии 1.2.0-25 или более поздней версии.
- Выполните раздел hello **краткое руководство по установке** из [в этой статье](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#steps-to-install-the-oms-agent-for-linux) tooinstall и рабочая область tooyour встроенного hello агента.

Как правило hello агент установлен на компьютере, отличном от hello, на какие журналы hello создаются. Компьютер агента toohello журналы hello пересылки обычно требуют hello следующие шаги:

- Настройка ведения журнала продукта/machine tooforward hello необходимые события toohello управляющая программа syslog (rsyslog или syslog-ng) hello на компьютере агента hello.
- Включите управляющая программа syslog hello в сообщений hello агента машины tooreceive из удаленной системы.

На компьютере агента hello hello события должны toobe, отправленных из системного журнала управляющей программы hello toolocal UDP-порт 25226. агент Здравствуй прослушивает входящие события для этого порта. Hello ниже приведен пример конфигурации для отправки всех событий из hello локальной системы toohello агента (можно изменить конфигурации toofit hello локальные параметры).

1. Hello откройте окно терминала и перейдите toohello directory */etc/syslog-ng /* 
2. Создайте новый файл *безопасности конфигурации omsagent.conf* и добавьте следующие содержимое hello: OMS_facility = local4
    
    filter f_local4_oms { facility(local4); };

    destination security_oms { tcp("127.0.0.1" port(25226)); };

    log { source(src); filter(f_local4_oms); destination(security_oms); };
    
3. Загрузите файл hello *security_events.conf* и поместите его в */etc/opt/microsoft/omsagent/conf/omsagent.d/* на компьютере агента OMS hello.
4. Введите команду hello ниже управляющая программа syslog hello toorestart: *для запуска syslog-ng:*
    
    ```
    sudo service rsyslog restart
    ```

    *Для rsyslog выполните следующую команду:*
    
    ```
    /etc/init.d/syslog-ng restart
    ```
5. Введите команду hello ниже toorestart hello агента OMS.

    *Для syslog-ng выполните следующую команду:*
    
    ```
    sudo service omsagent restart
    ```

    *Для rsyslog выполните следующую команду:*
    
    ```
    systemctl restart omsagent
    ```
6. Введите следующую команду hello и просмотрите tooconfirm результат hello, отсутствии ошибок в журнале агента OMS hello:

    ``` 
    tail /var/opt/microsoft/omsagent/log/omsagent.log
    ```

## <a name="reviewing-collected-security-events"></a>Просмотр собранных событий безопасности

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

После hello конфигурации находится над, событий безопасности hello запустится toobe, полученный системой безопасности OMS. toovisualize эти события, откройте hello поиска журналов, введите команду hello *тип = CommonSecurityLog* в hello поле поиска и нажмите клавишу ВВОД. Hello примере показан результат hello этой команды Обратите внимание на то что в этом случае OMS безопасности уже полученный журналы безопасности от разных поставщиков:
   
![Оценка базовых показателей в решении OMS "Безопасность и аудит"](./media/oms-security-connect-products/oms-security-connect-products-fig1.png)

Можно уточнить поиск для одного поставщика, например, журналы документации Cisco toovisualize, тип: *тип = CommonSecurityLog DeviceVendor = Cisco*. Hello «CommonSecurityLog» стандартные поля для любой заголовок CEF, включая основные extensios hello, во время любого другого расширения, является ли она «Пользовательского модуля», будет вставлен в поле «AdditionalExtensions». Можно использовать поля tooget выделенной функции hello настраиваемые поля из него. 

### <a name="accessing-computers-missing-baseline-assessment"></a>Просмотр сведений о компьютерах с отсутствующей базовой оценкой
OMS поддерживает профиль базового члена домена hello в Windows Server 2008 R2 до tooWindows Server 2012 R2. Эта возможность для Windows Server 2016 находится на этапе разработки и будет добавлена после публикации. Все другие операционные системы, проверенных через базовые оценки OMS безопасность и аудит отображаются под hello **компьютеры с недостающими базовых показателей оценки** раздела.

## <a name="see-also"></a>См. также
В этом документе вы узнали, каким образом tooconnect вашей tooOMS CEF решения. toolearn Дополнительные сведения о безопасности OMS см. следующие статьи hello.

* [Общие сведения об Operations Management Suite (OMS)](operations-management-suite-overview.md)
* [Мониторинг и реагирование tooSecurity оповещения в Operations Management Suite безопасности и аудита решения](oms-security-responding-alerts.md)
* [Мониторинг ресурсов в решении "Безопасность и аудит" Operations Management Suite](oms-security-monitoring-resources.md)

