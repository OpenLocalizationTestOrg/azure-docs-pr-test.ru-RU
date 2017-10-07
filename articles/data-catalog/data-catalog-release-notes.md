---
title: "заметки о выпуске aaaAzure данных каталога | Документы Microsoft"
description: "Заметки о выпуске каталога данных Azure."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 3aca9c49-45a4-4352-92e6-bd25ee3eacf7
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 661826f66020ba72a885c6b14522b53c8b469d20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-catalog-release-notes"></a>Заметки о выпуске каталога данных Azure
## <a name="notes-for-hello-november-20-2015-release-of-azure-data-catalog"></a>Заметки о выпуске 20 ноября 2015 г. hello каталога данных Azure
### <a name="opening-data-sources-in-power-bi-desktop"></a>Открытие источников данных в Power BI Desktop
При использовании параметра «Открыть в Power BI Desktop» hello из hello **каталога данных Azure** портала, пользователей может возникнуть одна из двух проблем в hello приложения Power BI Desktop:

* Откроется диалоговое окно с заголовком hello «Не удается tooOpen документа»
* Открывает Hello приложения Power BI Desktop, но файл hello появится пустой toobe

В каждом случае hello проблему можно устранить, загрузив и установив последнюю версию Power BI Desktop из hello [PowerBI.com](https://powerbi.com).

## <a name="notes-for-hello-november-13-2015-release-of-azure-data-catalog"></a>Заметки о выпуске 13 ноября 2015 г. hello каталога данных Azure
### <a name="registering-and-connecting-tooteradata"></a>Регистрация и подключении tooTeradata
При подключении tooTeradata источники данных пользователям необходимо установить правильный драйвер Teradata ODBC hello, соответствующих hello разрядности (32-разрядной или 64-разрядной) используемого программного hello.

На момент написания этой ADC Дата выпуска, hello последней [Teradata ODBC-драйвер для windows (версия 15.10)](http://downloads.teradata.com/download/connectivity/odbc-driver/windows) совместим с Office 2013, но не с Office 2016.

## <a name="notes-for-hello-july-13-2015-release-of-azure-data-catalog"></a>Заметки о выпуске 13 июля 2015 г. hello каталога данных Azure
### <a name="registering-and-connecting-toooracle-database"></a>Регистрация и подключении tooOracle базы данных
При подключении пользователей источников данных tooOracle базы данных необходимо установить hello правильный Oracle драйверы, которые соответствуют hello разрядности (32-разрядной или 64-разрядной) hello программном обеспечении, используемом.

* При регистрации источников данных Oracle на компьютере под управлением 32-разрядной версии Windows, будет использоваться hello 32-разрядные драйверы Oracle
* При регистрации источников данных Oracle на компьютере под управлением 64-разрядной версии Windows, будет использоваться hello 64-разрядные драйверы Oracle
* При подключении tooOracle источники данных, с помощью Excel на компьютере под управлением hello 32-разрядной версии Microsoft Office, включая на 64-разрядной Windows hello 32-разрядные драйверы Oracle будет использоваться
* При подключении tooOracle источники данных, с помощью Excel на компьютере под управлением hello 64-разрядная версия Microsoft Office, будут использоваться hello 64-разрядные драйверы Oracle

### <a name="registering-and-connecting-toosql-server-reporting-services"></a>Регистрация и подключении tooSQL Server Reporting Services
Для источников данных службы SQL Server Reporting Services (SSRS) поддерживается только в настоящее время составляет tooNative режиме серверы. Поддержка служб SSRS в режиме интеграции с SharePoint будет добавлена в более поздней версии.

### <a name="opening-data-assets-in-excel"></a>Открытие ресурсов данных в Excel
При открытии ресурсов данных в Microsoft Excel из hello **каталога данных Azure** портала, пользователям может предлагаться с **уведомление безопасности Microsoft Excel** диалоговое окно. Это стандартный, ожидаемое поведение и пользователи могут выбирать **включить** toocontinue.

Подробнее об этом см. в статье [Включение или отключение предупреждений системы безопасности о ссылках и файлах с подозрительных веб-сайтов](https://support.office.com/article/Enable-or-disable-security-alerts-about-links-and-files-from-suspicious-websites-A1AC6AE9-5C4A-4EB3-B3F8-143336039BBE).

### <a name="proxy-and-policy-configuration-and-data-source-registration"></a>Конфигурация прокси-сервера и политики, а также регистрация источника данных
Пользователи могут столкнуться с ситуацией, где они могут войти на портал toohello каталога данных Azure, но при попытке toolog на точках сообщение об ошибке, которая запрещает вход в систему регистрации инструмента toohello данных источника.

Существуют две возможные причины такого проблемного поведения.

**Причина 1: Конфигурации служб федерации Active Directory** средство регистрации источника данных hello использует проверку подлинности форм toovalidate входа пользователей в систему с данными Active Directory. Для успешного входа в систему необходимо включить проверку подлинности форм в hello глобальной политики проверки подлинности администратором Active Directory.

В некоторых ситуациях это ошибка может происходить только в том случае, если пользователь hello находится в сети компании hello, или только при подключении пользователя hello с hello вне корпоративной сети. Hello глобальной политики проверки подлинности позволяет toobe методы проверки подлинности включен отдельно для интрасети и экстрасети. Ошибки входа может возникнуть, если для сети hello, из какой hello подключении не включена проверка подлинности форм.

Подробнее: [Настройка политик проверки подлинности](https://technet.microsoft.com/library/dn486781.aspx).

**Причина 2: Конфигурация прокси-сервера сети** Если hello корпоративной сети используются прокси-сервера, средство регистрации hello может оказаться tooAzure может tooconnect Active Directory через прокси-сервер hello. Пользователи гарантирует этого инструмента регистрации hello, изменив файл конфигурации средства hello, добавление файла toohello этого раздела:

      <system.net>
        <defaultProxy useDefaultCredentials="true" enabled="true">
          <proxy usesystemdefault="True"
                          proxyaddress="http://<your corporate network proxy url>"
                          bypassonlocal="True"/>
        </defaultProxy>
      </system.net>


файл RegistrationTool.exe.config toolocate hello, запустите средство регистрации hello, а затем откройте диспетчер задач Windows программа hello. На вкладке сведения hello в диспетчере задач щелкните правой кнопкой мыши на RegistrationTool.exe и выберите Открыть расположение файла hello во всплывающем меню.
