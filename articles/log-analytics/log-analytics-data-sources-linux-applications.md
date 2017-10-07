---
title: "производительность приложения Linux в аналитику журнала OMS aaaCollect | Документы Microsoft"
description: "Эта статья содержит сведения по настройке hello агента OMS для счетчиков производительности Linux toocollect для MySQL и HTTP-сервера Apache."
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
ms.date: 05/04/2017
ms.author: magoedte
ms.openlocfilehash: 51105c6add5c7941a004570a76a4d94c02fc8a71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="collect-performance-counters-for-linux-applications-in-log-analytics"></a>Сбор данных производительности приложений Linux в Log Analytics 
Эта статья содержит сведения по настройке hello [агента OMS для Linux](https://github.com/Microsoft/OMS-Agent-for-Linux) toocollect счетчики производительности для конкретных приложений.  в данной статье приложения Hello является:  

- [MySQL](#MySQL)
- [HTTP-сервер Apache](#apache-http-server)

## <a name="mysql"></a>MySQL
Если сервер MySQL или MariaDB Server обнаруживается hello компьютера при установке агента OMS hello, поставщик для сервера MySQL наблюдения за производительностью устанавливается автоматически. Этот поставщик подключается toohello локального MySQL или MariaDB tooexpose статистики производительности сервера. Необходимо настроить учетные данные пользователя MySQL, чтобы hello поставщик можно получить доступ к MySQL Server hello.

### <a name="configure-mysql-credentials"></a>Настройка учетных данных MySQL
Hello поставщик MySQL OMI требуется предварительно настроенный пользователь MySQL и установленные клиентские библиотеки MySQL в порядке tooquery hello производительности и сведения о работоспособности из экземпляра MySQL hello.  Эти учетные данные хранятся в файле проверки подлинности, который хранится на агенте Linux hello.  файл проверки подлинности Hello указывает адреса привязки и выполняет прослушивание экземпляр MySQL порт hello и новые учетные данные toouse toogather метрики.  

Во время установки hello агента OMS для Linux hello MySQL OMI поставщика будет проверять файлы конфигурации my.cnf MySQL (расположения по умолчанию) для адреса привязки и порта и частично набор hello файл проверки подлинности MySQL OMI.

файл проверки подлинности MySQL Hello хранится по `/var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth`.


### <a name="authentication-file-format"></a>Формат файла аутентификации
Ниже приведен формат hello hello файл проверки подлинности MySQL OMI

    [Port]=[Bind-Address], [username], [Base64 encoded Password]
    (Port)=(Bind-Address), (username), (Base64 encoded Password)
    (Port)=(Bind-Address), (username), (Base64 encoded Password)
    AutoUpdate=[true|false]

в hello в следующей таблице описываются записи Hello в файле проверки подлинности hello.

| Свойство | Описание |
|:--|:--|
| Порт | Представляет hello текущий порт hello выполняет прослушивание экземпляр MySQL. Порт 0 указывает, что для экземпляра по умолчанию используются следующие свойства hello. |
| адрес привязки;| Текущий адрес привязки MySQL. |
| Имя пользователя| Пользователь MySQL использовать экземпляр сервера MySQL hello toomonitor toouse. |
| пароль в кодировке Base64.| Пароль hello пользователя MySQL, закодированный в Base64. |
| Автоматическое обновление| Указывает, является ли toorescan для изменения в файле my.cnf hello и перезаписать файл проверки подлинности OMI MySQL hello в том случае, когда hello поставщик OMI MySQL обновляется. |

### <a name="default-instance"></a>Экземпляр по умолчанию
файл проверки подлинности MySQL OMI Hello можно определить экземпляр по умолчанию и toomake номеров портов, управление несколькими экземплярами MySQL на одном узле Linux проще.  экземпляр по умолчанию Hello обозначается экземпляром с портом 0. Все дополнительные экземпляры наследуют свойства от экземпляра по умолчанию hello если они не заданы разные значения. Например при добавлении экземпляра MySQL, прослушивает порт «3308», адрес привязки, имя пользователя и пароль в кодировке Base64 экземпляра по умолчанию hello достигается используется tootry и отслеживать экземпляр hello прослушивание на порту 3308. Если hello экземпляр в порту 3308 является адресом привязанного tooanother и использует hello же имя пользователя MySQL требуется пароль пары только hello адреса привязки и hello другие свойства будут унаследованы.

в следующей таблице Hello имеет пример настройки экземпляра 

| Описание | Файл |
|:--|:--|
| Экземпляр по умолчанию и экземпляр с портом 3308. | `0=127.0.0.1, myuser, cnBwdA==`<br>`3308=, ,`<br>`AutoUpdate=true` |
| Экземпляр по умолчанию и экземпляр с портом 3308 и другими именем пользователя и паролем. | `0=127.0.0.1, myuser, cnBwdA==`<br>`3308=127.0.1.1, myuser2,cGluaGVhZA==`<br>`AutoUpdate=true` |


### <a name="mysql-omi-authentication-file-program"></a>Программа для изменения файла проверки подлинности OMI MySQL
Поставщик, включенных hello установку hello MySQL OMI является программы файла проверки подлинности MySQL OMI, который может быть файл проверки подлинности OMI MySQL используется tooedit hello. Hello программы файла проверки подлинности можно найти в следующие расположения hello.

    /opt/microsoft/mysql-cimprov/bin/mycimprovauth

> [!NOTE]
> Hello учетных данных файл должен быть доступен для чтения для учетной записи omsagent hello. Выполнение hello выполнить команду mycimprovauth от имени omsgent рекомендуется.

Hello следующей таблице приведены сведения о синтаксисе hello использования mycimprovauth.

| Операция | Пример | Описание
|:--|:--|:--|
| autoupdate *false\|true* | mycimprovauth autoupdate false | Задает ли hello файл проверки подлинности будут автоматически обновляться на перезапуск или обновить. |
| default *bind-address username password* | mycimprovauth default 127.0.0.1 root pwd | Задает hello экземпляр по умолчанию в hello файл проверки подлинности MySQL OMI.<br>поле пароля Hello следует вводить в формате обычного текста - пароль hello в hello файл проверки подлинности MySQL OMI будет использоваться в кодировке Base 64. |
| delete *default\|port_num* | mycimprovauth 3308 | Удаляет указанный экземпляр hello, либо по умолчанию или номер порта. |
| help | mycimprov help | Печать списка toouse команд. |
| print | mycimprov print | Печать легко tooread файл проверки подлинности MySQL OMI. |
| update port_num *bind-address username password* | mycimprov update 3307 127.0.0.1 root pwd | Обновляет указанный экземпляр hello или добавляет hello экземпляр в том случае, если он не существует. |

Hello следующие примеры команд определить учетную запись пользователя по умолчанию hello MySQL server в localhost.  поле пароля Hello следует вводить в формате обычного текста — пароль hello в hello файл проверки подлинности MySQL OMI будет использоваться в кодировке Base 64

    sudo su omsagent -c '/opt/microsoft/mysql-cimprov/bin/mycimprovauth default 127.0.0.1 <username> <password>'
    sudo /opt/omi/bin/service_control restart

### <a name="database-permissions-required-for-mysql-performance-counters"></a>Разрешения базы данных, необходимые для счетчиков производительности MySQL
Hello пользователю MySQL требуется доступ toohello следующие запросы toocollect данных производительности MySQL Server. 

    SHOW GLOBAL STATUS;
    SHOW GLOBAL VARIABLES:


пользователь MySQL Hello также требует доступ SELECT toohello следующие таблицы по умолчанию.

- information_schema;
- mysql. 

Эти права можно предоставить, запустив hello следующих команд grant.

    GRANT SELECT ON information_schema.* too‘monuser’@’localhost’;
    GRANT SELECT ON mysql.* too‘monuser’@’localhost’;


> [!NOTE]
> tooa toogrant разрешения мониторинга пользователя hello, давая пользователю MySQL требуется hello привилегию «предоставление», а также hello предоставляемое право.

### <a name="define-performance-counters"></a>Определение счетчиков производительности

После настройки hello агента OMS для Linux toosend данных tooLog аналитики, необходимо настроить toocollect счетчики производительности hello.  Используйте процедуру hello в [Windows и Linux источников данных производительности в службе анализа журналов](log-analytics-data-sources-windows-events.md) со счетчиками hello в hello в следующей таблице.

| Имя объекта | Имя счетчика |
|:--|:--|
| База данных MySQL | Дисковое пространство в байтах |
| База данных MySQL | Таблицы |
| MySQL Server | Счетчик производительности "Прерванные подключения" |
| MySQL Server | Счетчик производительности "Использование подключения" |
| MySQL Server | Используемое дисковое пространство в байтах |
| MySQL Server | Счетчик производительности "Сканирование всей таблицы" |
| MySQL Server | Счетчик производительности "Попадания в буферный пул InnoDB" |
| MySQL Server | Счетчик производительности "Использование буферного пула InnoDB" |
| MySQL Server | Счетчик производительности "Использование буферного пула InnoDB" |
| MySQL Server | Счетчик производительности "Попадания в кэш ключей" |
| MySQL Server | Счетчик производительности "Использование кэша ключей" |
| MySQL Server | Счетчик производительности "Запись в кэш ключей" |
| MySQL Server | Счетчик производительности "Попадания в кэш запросов" |
| MySQL Server | Счетчик производительности "Очистка кэша запросов" |
| MySQL Server | Счетчик производительности "Использование кэша запросов" |
| MySQL Server | Счетчик производительности "Попадания в кэш таблиц" |
| MySQL Server | Счетчик производительности "Использование кэша таблиц" |
| MySQL Server | Счетчик производительности "Блокировка подключения к таблице" |

## <a name="apache-http-server"></a>HTTP-сервер Apache 
Если при установке пакета omsagent hello HTTP-сервера Apache обнаружен на компьютере hello, будет автоматически устанавливается поставщик для HTTP-сервера Apache наблюдения за производительностью. Этот поставщик использует модуль Apache, который должен быть загружен в hello HTTP-сервера Apache в порядке tooaccess данных о производительности. может быть загружен модуль Hello hello следующую команду:
```
sudo /opt/microsoft/apache-cimprov/bin/apache_config.sh -c
```

toounload hello Apache модуль мониторинга, запустите hello следующую команду:
```
sudo /opt/microsoft/apache-cimprov/bin/apache_config.sh -u
```

### <a name="define-performance-counters"></a>Определение счетчиков производительности

После настройки hello агента OMS для Linux toosend данных tooLog аналитики, необходимо настроить toocollect счетчики производительности hello.  Используйте процедуру hello в [Windows и Linux источников данных производительности в службе анализа журналов](log-analytics-data-sources-windows-events.md) со счетчиками hello в hello в следующей таблице.

| Имя объекта | Имя счетчика |
|:--|:--|
| HTTP-сервер Apache | Занятые рабочие роли |
| HTTP-сервер Apache | Бездействующие рабочие роли |
| HTTP-сервер Apache | Счетчик производительности "Занятые рабочие роли" |
| HTTP-сервер Apache | Счетчик производительности "Общее использование ЦП" |
| Виртуальный узел Apache | Ошибок в минуту (клиент) |
| Виртуальный узел Apache | Ошибок в минуту (сервер) |
| Виртуальный узел Apache | КБ на запрос |
| Виртуальный узел Apache | КБ в запросах в секунду |
| Виртуальный узел Apache | Запросов в секунду |



## <a name="next-steps"></a>Дальнейшие действия
* [Сбор счетчиков производительности](log-analytics-data-sources-performance-counters.md) с агентов Linux.
* Дополнительные сведения о [входа выполняет](log-analytics-log-searches.md) tooanalyze hello данные, собранные из источников данных и решений. 
