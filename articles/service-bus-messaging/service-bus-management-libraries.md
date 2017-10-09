---
title: "библиотеки управления Service Bus aaaAzure | Документы Microsoft"
description: "Управление пространствами имен служебной шины и сущностями обмена сообщениями из .NET."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/05/2017
ms.author: sethm
ms.openlocfilehash: 9e4ad91f22815ca0838e6e4647a3606109b2b441
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-management-libraries"></a>Библиотеки управления служебной шины

библиотеки управления Hello Azure Service Bus можно динамически подготавливать пространства имен служебной шины и сущностей. Это позволяет сложных развертываний и сценариев обмена сообщениями, а также позволяет определить, какие сущности tooprovision tooprogrammatically. В настоящее время эти библиотеки доступны для .NET.

## <a name="supported-functionality"></a>Поддерживаемые функции

* Создание, обновление, удаление пространства имен.
* Создание, обновление, удаление очереди.
* Создание, обновление, удаление раздела.
* Создание, обновление, удаление подписки.

## <a name="prerequisites"></a>Предварительные требования

tooget работы с использованием библиотеки управления Service Bus hello, вы должны проверить подлинность hello службы Azure Active Directory (AAD). AAD требует проверки подлинности как участника-службы, который предоставляет доступ tooyour ресурсов Azure. Сведения о создании субъекта-службы см. в одной из приведенных ниже статей:  

* [Использовать приложение Active Directory Azure портала toocreate hello и участника-службы, могут обращаться к ресурсам](/azure/azure-resource-manager/resource-group-create-service-principal-portal)
* [Использование Azure PowerShell toocreate ресурсов tooaccess участника службы](/azure/azure-resource-manager/resource-group-authenticate-service-principal)
* [Используйте основной tooaccess ресурсов службы toocreate Azure CLI](/azure/azure-resource-manager/resource-group-authenticate-service-principal-cli)

Эти учебники предоставляют `AppId` (идентификатор клиента), `TenantId`, и `ClientSecret` (ключ проверки подлинности), каждый из которых используются для проверки подлинности управления библиотеками hello. Необходимо иметь **владельца** разрешения для группы ресурсов hello, над которым необходимо toorun.

## <a name="programming-pattern"></a>Шаблон программирования

Здравствуйте, toomanipulate шаблон общего протокола соответствует любой ресурс служебной шины:

1. Получение токена от Azure Active Directory с помощью hello **Microsoft.IdentityModel.Clients.ActiveDirectory** библиотеки.
   ```csharp
   var context = new AuthenticationContext($"https://login.microsoftonline.com/{tenantId}");

   var result = await context.AcquireTokenAsync("https://management.core.windows.net/", new ClientCredential(clientId, clientSecret));
   ```

1. Создать hello `ServiceBusManagementClient` объекта.

   ```csharp
   var creds = new TokenCredentials(token);
   var sbClient = new ServiceBusManagementClient(creds)
   {
       SubscriptionId = SettingsCache["SubscriptionId"]
   };
   ```

1. Набор hello `CreateOrUpdate` tooyour параметры указанные значения.

   ```csharp
   var queueParams = new QueueCreateOrUpdateParameters()
   {
       Location = SettingsCache["DataCenterLocation"],
       EnablePartitioning = true
   };
   ```

1. Hello вызова Execute.

   ```csharp
   await sbClient.Queues.CreateOrUpdateAsync(resourceGroupName, namespaceName, QueueName, queueParams);
   ```

## <a name="next-steps"></a>Дальнейшие действия
* [Пример управления для .NET](https://github.com/Azure-Samples/service-bus-dotnet-management/)
* [Справочник по API Microsoft.Azure.Management.ServiceBus](/dotnet/api/Microsoft.Azure.Management.ServiceBus)
