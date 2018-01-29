---
title: "Publish-WebApplicationVM | Документация Майкрософт"
description: "Узнайте, как развернуть веб-приложение на виртуальной машине. Этот сценарий создает необходимые ресурсы в подписке Azure, если они еще не созданы."
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
ms.openlocfilehash: 2738fc1dff50a177a227ae2c7719bd9a192d82ad
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/11/2017
---
# <a name="publish-webapplicationvm-windows-powershell-script"></a>Publish-WebApplicationVM (сценарий Windows PowerShell)
Развертывание веб-приложения на виртуальной машине. и создает необходимые ресурсы в подписке Azure, если они еще не созданы.

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

### <a name="configuration"></a>Параметр Configuration
Путь к файлу конфигурации JSON, содержащему подробные сведения о развертывании.

| Псевдонимы | Нет |
| --- | --- |
| Обязательный? |Да |
| Позиция |именованная |
| Значение по умолчанию |Нет |
| Принимает входные данные конвейера? |нет |
| Принимает подстановочные знаки? |нет |

### <a name="subscriptionname"></a>Параметр SubscriptionName
Имя подписки Azure, в которой необходимо создать виртуальную машину.

| Псевдонимы | Нет |
| --- | --- |
| Обязательный? |нет |
| Позиция |именованная |
| Значение по умолчанию |Используется первая подписка в файле подписок |
| Принимает входные данные конвейера? |нет |
| Принимает подстановочные знаки? |нет |

### <a name="webdeploypackage"></a>Параметр WebDeployPackage
Путь к пакету веб-развертывания для публикации на виртуальной машине. Этот пакет можно создать с помощью мастера «Публикация веб-сайта» в Visual Studio. Ознакомьтесь со статьей [Как создать пакет веб-развертывания в Visual Studio](https://msdn.microsoft.com/library/dd465323.aspx).

| Псевдонимы | Нет |
| --- | --- |
| Обязательный? |нет |
| Позиция |именованная |
| Значение по умолчанию |Нет |
| Принимает входные данные конвейера? |нет |
| Принимает подстановочные знаки? |нет |

### <a name="allowuntrusted"></a>AllowUntrusted
Значение true позволяет использовать сертификаты, не подписанные надежным корневым центром сертификации.

| Псевдонимы | Нет |
| --- | --- |
| Обязательный? |нет |
| Позиция |именованная |
| Значение по умолчанию |нет |
| Принимает входные данные конвейера? |нет |
| Принимает подстановочные знаки? |нет |

### <a name="vmpassword"></a>VMPassword
Данные учетной записи виртуальной машины. Пример: -VMPassword @{Name = admin; Password = password}

| Псевдонимы | Нет |
| --- | --- |
| Обязательный? |нет |
| Позиция |именованная |
| Значение по умолчанию |Нет |
| Принимает входные данные конвейера? |нет |
| Принимает подстановочные знаки? |нет |

### <a name="databaseserverpassword"></a>Параметр DatabaseServerPassword
Учетные данные для базы данных SQL в Azure. Пример: -DatabaseServerPassword @{Name = admin; Password = password}

| Псевдонимы | Нет |
| --- | --- |
| Обязательный? |нет |
| Позиция |именованная |
| Значение по умолчанию |Нет |
| Принимает входные данные конвейера? |нет |
| Принимает подстановочные знаки? |нет |

### <a name="sendhostmessagestooutput"></a>Параметр SendHostMessagesToOutput
Если установлено значение true, оправляет сообщения из сценария в поток вывода.

| Псевдонимы | Нет |
| --- | --- |
| Обязательный? |нет |
| Позиция |именованная |
| Значение по умолчанию |нет |
| Принимает входные данные конвейера? |нет |
| Принимает подстановочные знаки? |нет |

## <a name="remarks"></a>Примечания
Подробное описание того, как использовать сценарий для создания сред разработки и тестирования, см. в статье [Использование скриптов Windows PowerShell для публикации в среды разработки и тестирования](vs-azure-tools-publishing-using-powershell-scripts.md).

В файле конфигурации JSON указаны данные объектов, которые необходимо развернуть. Он содержит сведения, указанные при создании проекта, например имя, группу сходства, образ виртуального жесткого диска и размер виртуальной машины. Он также включает конечные точки виртуальной машины, подготавливаемые базы данных (если они есть) и параметры веб-развертывания. В следующем коде показан пример файла конфигурации JSON.

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

В файле конфигурации JSON можно изменить объекты, которые подлежат подготовке. Виртуальная машина и облачная служба необходимы, но раздел баз данных является необязательным.

