---
title: "библиотеки управления концентраторов событий aaaAzure | Документы Microsoft"
description: "Управление пространствами имен и сущностями концентраторов событий из .NET"
services: event-hubs
cloud: na
documentationcenter: na
author: sethmanheim
manager: timlt
ms.assetid: 
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: b7db0077f6f31397ae46e926c3c28630a157824c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-management-libraries"></a>Библиотеки управления концентраторов событий

библиотеки управления Hello концентраторов событий можно динамически подготавливать концентраторов событий пространств имен и сущностей. Благодаря этому сложных развертываний и сценариев обмена сообщениями, чтобы программно определить, какие tooprovision сущностей. В настоящее время эти библиотеки доступны для .NET.

## <a name="supported-functionality"></a>Поддерживаемые функции

* Создание, обновление, удаление пространства имен.
* Создание, обновление, удаление концентраторов событий.
* Создание, обновление, удаление группы потребителей.

## <a name="prerequisites"></a>Предварительные требования

tooget работы с использованием библиотеки управления hello концентраторов событий, необходимо проверить подлинность с помощью Azure Active Directory (AAD). AAD требует проверки подлинности как участника-службы, который предоставляет доступ tooyour ресурсов Azure. Сведения о создании субъекта-службы см. в одной из приведенных ниже статей:  

* [Использовать приложение Active Directory Azure портала toocreate hello и участника-службы, могут обращаться к ресурсам](../azure-resource-manager/resource-group-create-service-principal-portal.md)
* [Использование Azure PowerShell toocreate ресурсов tooaccess участника службы](../azure-resource-manager/resource-group-authenticate-service-principal.md)
* [Используйте основной tooaccess ресурсов службы toocreate Azure CLI](../azure-resource-manager/resource-group-authenticate-service-principal-cli.md)

Эти учебники предоставляют `AppId` (идентификатор клиента), `TenantId`, и `ClientSecret` (ключ проверки подлинности), каждый из которых используются для проверки подлинности управления библиотеками hello. Необходимо иметь **владельца** разрешения для группы ресурсов hello, на котором будет toorun.

## <a name="programming-pattern"></a>Шаблон программирования

Здравствуйте, шаблон toomanipulate любой ресурс концентраторов событий соответствует общего протокола:

1. Получение токена от AAD с помощью hello `Microsoft.IdentityModel.Clients.ActiveDirectory` библиотеки.
    ```csharp
    var context = new AuthenticationContext($"https://login.microsoftonline.com/{tenantId}");

    var result = await context.AcquireTokenAsync(
        "https://management.core.windows.net/",
        new ClientCredential(clientId, clientSecret)
    );
    ```

1. Создать hello `EventHubManagementClient` объекта.
    ```csharp
    var creds = new TokenCredentials(token);
    var ehClient = new EventHubManagementClient(creds)
    {
        SubscriptionId = SettingsCache["SubscriptionId"]
    };
    ```

1. Набор hello `CreateOrUpdate` tooyour параметры указанные значения.
    ```csharp
    var ehParams = new EventHubCreateOrUpdateParameters()
    {
        Location = SettingsCache["DataCenterLocation"]
    };
    ```

1. Hello вызова Execute.
    ```csharp
    await ehClient.EventHubs.CreateOrUpdateAsync(resourceGroupName, namespaceName, EventHubName, ehParams);
    ```

## <a name="next-steps"></a>Дальнейшие действия
* [Пример управления для .NET](https://github.com/Azure-Samples/event-hubs-dotnet-management/)
* [Справочник по Microsoft.Azure.Management.EventHub](/dotnet/api/Microsoft.Azure.Management.EventHub) 
