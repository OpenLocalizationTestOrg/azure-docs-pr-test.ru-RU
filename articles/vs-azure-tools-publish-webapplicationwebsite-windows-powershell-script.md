---
title: "aaaPublish-WebApplicationWebSite (скрипт Windows PowerShell) | Документы Microsoft"
description: "Узнайте, как toopublish веб-узел проекта tooan веб-сайте Azure. Этот скрипт создает hello необходимые ресурсы в подписке Azure, если они не существуют."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 63cfaa2d-f04d-40dc-8677-345385c278d5
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: d46904e30e3c2e040e57888fa31543e8e366527f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="publish-webapplicationwebsite-windows-powershell-script"></a>Publish-WebApplicationWebSite (сценарий Windows PowerShell)
## <a name="syntax"></a>Синтаксис
Публикует tooan проект web веб-сайте Azure. Hello скрипт создает hello необходимые ресурсы в подписке Azure, если они не существуют.

    Publish-WebApplicationWebSite
    –Configuration <configuration>
    -SubscriptionName <subscriptionName>
    -WebDeployPackage <packageName>
    -DatabaseServerPassword @{Name = "name"; Password = "password"}
    -SendHostMessagesToOutput
    -Verbose


## <a name="configuration"></a>Конфигурация
Hello путь toohello файл конфигурации JSON, описывающий сведения hello hello развертывания.

| Параметр | Значение по умолчанию |
| --- | --- |
| Псевдонимы |Нет |
| Обязательный? |Да |
| Позиция |именованная |
| Значение по умолчанию |Нет |
| Принимает входные данные конвейера? |нет |
| Принимает подстановочные знаки? |нет |

## <a name="subscriptionname"></a>Параметр SubscriptionName
Имя Hello hello подписки Azure, вы должны быть toocreate hello веб-сайта.

| Параметр | Значение по умолчанию |
| --- | --- |
| Псевдонимы |Нет |
| Обязательный? |нет |
| Позиция |именованная |
| Значение по умолчанию |Нет |
| Принимает входные данные конвейера? |нет |
| Принимает подстановочные знаки? |нет |

## <a name="webdeploypackage"></a>Параметр WebDeployPackage
Hello путь toohello web развертывания пакета toopublish toohello веб-сайта. Этот пакет можно создать с помощью мастера публикации веб-сайта hello в Visual Studio. Дополнительные сведения можно найти в статье [Начало работы с облачными службами Azure и ASP.NET](http://go.microsoft.com/fwlink/p/?LinkID=623089).

| Параметр | Значение по умолчанию |
| --- | --- |
| Псевдонимы |Нет |
| Обязательный? |нет |
| Позиция |именованная |
| Значение по умолчанию |Нет |
| Принимает входные данные конвейера? |нет |
| Принимает подстановочные знаки? |нет |

## <a name="databaseserverpassword"></a>Параметр DatabaseServerPassword
Hello имя пользователя и пароль для hello базы данных SQL Azure.

| Параметр | Значение по умолчанию |
| --- | --- |
| Псевдонимы |Нет |
| Обязательный? |нет |
| Позиция |именованная |
| Значение по умолчанию |Нет |
| Принимает входные данные конвейера? |нет |
| Принимает подстановочные знаки? |нет |

## <a name="sendhostmessagestooutput"></a>Параметр SendHostMessagesToOutput
Значение true, если поток вывода для печати сообщения из скрипта toohello hello.

| Параметр | Значение по умолчанию |
| --- | --- |
| Псевдонимы |Нет |
| Обязательный? |нет |
| Позиция |именованная |
| Значение по умолчанию |нет |
| Принимает входные данные конвейера? |нет |
| Принимает подстановочные знаки? |нет |

## <a name="remarks"></a>Примечания
Полное описание toouse hello сценария toocreate разработки и тестовой среде. в статье [tooDev tooPublish с помощью сценариев Windows PowerShell и тестовых средах](vs-azure-tools-publishing-using-powershell-scripts.md).

файл конфигурации JSON Hello указывает hello сведения о том, что будет toobe развертывания. Он включает сведения hello, указанный при создании проекта hello, такие как имя hello и имя пользователя для веб-сайта hello. Он также включает tooprovision hello базы данных, если таковые имеются. После кода Hello показан пример файла конфигурации JSON:

    {
        "environmentSettings": {
            "webSite": {
                "name": "WebApplication10554",
                "location": "West US"
            },
            "databases": [
                {
                    "connectionStringName": "DefaultConnection",
                    "databaseName": "WebApplication10554_db",
                    "serverName": "iss00brc88",
                    "user": "sqluser2",
                    "password": "",
                    "edition": "",
                    "size": "",
                    "collation": "",
                    "location": "West US"
                }
            ]
        }
    }

Вы можете изменить состав развертывания файла toochange hello JSON конфигурации. Раздел веб-сайта является обязательным, но hello раздел базы данных является необязательным.

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения см. в статье [Publish-WebApplicationVM (сценарий Windows PowerShell)](vs-azure-tools-publish-webapplicationvm.md)

