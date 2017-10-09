---
title: "aaaPublish-WebApplicationVM | Документы Microsoft"
description: "Узнайте, как toodeploy виртуальная машина web tooa приложения. Этот скрипт создает hello необходимые ресурсы в подписке Azure, если они не существуют."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: de4cec95-f73f-44d9-babd-9f47f2633cdb
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: e4b52b620bebf44b87ddfc3b19c155bb65111814
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="publish-webapplicationvm-windows-powershell-script"></a>Publish-WebApplicationVM (сценарий Windows PowerShell)
Развертывание виртуальной машины web tooa приложений. Hello скрипт создает hello необходимые ресурсы в подписке Azure, если они не существуют.

```
Publish-WebApplicationVM
–Configuration <configuration>
-SubscriptionName <subscriptionName>
-WebDeployPackage <packageName>
-VMPassword @{Name = "name"; Password = "password")
-DatabaseServerPassword @{Name = "name"; Password = "password"}
-SendHostMessagesToOutput
-Verbose
```

### <a name="configuration"></a>Конфигурация
Hello путь toohello файл конфигурации JSON, описывающий сведения hello hello развертывания.

| Псевдонимы | Нет |
| --- | --- |
| Обязательный? |Да |
| Позиция |именованная |
| Значение по умолчанию |Нет |
| Принимает входные данные конвейера? |нет |
| Принимает подстановочные знаки? |нет |

### <a name="subscriptionname"></a>Параметр SubscriptionName
Имя Hello hello подписки Azure, в котором нужно toocreate hello виртуальной машины.

| Псевдонимы | Нет |
| --- | --- |
| Обязательный? |нет |
| Позиция |именованная |
| Значение по умолчанию |Использует первую подписку hello в файле подписки hello |
| Принимает входные данные конвейера? |нет |
| Принимает подстановочные знаки? |нет |

### <a name="webdeploypackage"></a>Параметр WebDeployPackage
Hello путь toohello развертывания пакета toopublish toohello виртуальная машина web. Этот пакет можно создать с помощью мастера публикации веб-сайта hello в Visual Studio. Ознакомьтесь со статьей [Как создать пакет веб-развертывания в Visual Studio](https://msdn.microsoft.com/library/dd465323.aspx).

| Псевдонимы | Нет |
| --- | --- |
| Обязательный? |нет |
| Позиция |именованная |
| Значение по умолчанию |Нет |
| Принимает входные данные конвейера? |нет |
| Принимает подстановочные знаки? |нет |

### <a name="allowuntrusted"></a>AllowUntrusted
Если значение равно true, разрешить использование hello сертификаты, которые не были подписаны доверенным корневым центром сертификации.

| Псевдонимы | Нет |
| --- | --- |
| Обязательный? |нет |
| Позиция |именованная |
| Значение по умолчанию |нет |
| Принимает входные данные конвейера? |нет |
| Принимает подстановочные знаки? |нет |

### <a name="vmpassword"></a>VMPassword
Hello учетные данные для учетной записи виртуальной машины hello. Пример: - VMPassword @{Name = «admin»; Пароль = «password»}

| Псевдонимы | Нет |
| --- | --- |
| Обязательный? |нет |
| Позиция |именованная |
| Значение по умолчанию |Нет |
| Принимает входные данные конвейера? |нет |
| Принимает подстановочные знаки? |нет |

### <a name="databaseserverpassword"></a>Параметр DatabaseServerPassword
Hello учетные данные для hello базы данных SQL Azure. Пример: - DatabaseServerPassword @{Name = «admin»; Пароль = «password»}

| Псевдонимы | Нет |
| --- | --- |
| Обязательный? |нет |
| Позиция |именованная |
| Значение по умолчанию |Нет |
| Принимает входные данные конвейера? |нет |
| Принимает подстановочные знаки? |нет |

### <a name="sendhostmessagestooutput"></a>Параметр SendHostMessagesToOutput
Значение true, если поток вывода для печати сообщения из скрипта toohello hello.

| Псевдонимы | Нет |
| --- | --- |
| Обязательный? |нет |
| Позиция |именованная |
| Значение по умолчанию |нет |
| Принимает входные данные конвейера? |нет |
| Принимает подстановочные знаки? |нет |

## <a name="remarks"></a>Примечания
Полное описание toouse hello сценария toocreate разработки и тестовой среде. в статье [tooDev tooPublish с помощью сценариев Windows PowerShell и тестовых средах](vs-azure-tools-publishing-using-powershell-scripts.md).

файл конфигурации JSON Hello указывает hello сведения о том, что будет toobe развертывания. Он включает сведения hello, указанный при создании проекта hello, такие как имя hello, территориальная группа, образ виртуального жесткого диска и размер виртуальной машины hello. Также включает hello конечных точек на виртуальной машине hello, tooprovision hello баз данных, если таковые имеются и параметры веб-развертываний. После кода Hello показан пример файла конфигурации JSON:

```
{
    "environmentSettings": {
        "cloudService": {
            "name": "myvmname",
            "affinityGroup": "",
            "location": "West US",
            "virtualNetwork": "",
            "subnet": "",
            "availabilitySet": "",
            "virtualMachine": {
                "name": "myvmname",
                "vhdImage": "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-201404.01-en.us-127GB.vhd",
                "size": "Small",
                "user": "vmuser1",
                "password": "",
                "enableWebDeployExtension": true,
                "endpoints": [
                    {
                        "name": "Http",
                        "protocol": "TCP",
                        "publicPort": "80",
                        "privatePort": "80"
                    },
                    {
                        "name": "Https",
                        "protocol": "TCP",
                        "publicPort": "443",
                        "privatePort": "443"
                    },
                    {
                        "name": "WebDeploy",
                        "protocol": "TCP",
                        "publicPort": "8172",
                        "privatePort": "8172"
                    },
                    {
                        "name": "Remote Desktop",
                        "protocol": "TCP",
                        "publicPort": "3389",
                        "privatePort": "3389"
                    },
                    {
                        "name": "Powershell",
                        "protocol": "TCP",
                        "publicPort": "5986",
                        "privatePort": "5986"
                    }
                ]
            }
        },
        "databases": [
            {
                "connectionStringName": "",
                "databaseName": "",
                "serverName": "",
                "user": "",
                "password": ""
            }
        ],
        "webDeployParameters": {
            "iisWebApplicationName": "Default Web Site"
        }
    }
}
```

Вы можете изменить состав подготовки файла toochange hello JSON конфигурации. Виртуальная машина и облачная служба обязательны, но hello раздел базы данных является необязательным.

