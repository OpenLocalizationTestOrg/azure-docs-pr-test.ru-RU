---
title: "Библиотеки управления служебной шины Azure | Документация Майкрософт"
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
ms.date: 10/18/2017
ms.author: sethm
ms.openlocfilehash: 3b7096a073b509217a6ed29b53f88f912e6613f6
ms.sourcegitcommit: d6ad3203ecc54ab267f40649d3903584ac4db60b
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/19/2017
---
# <a name="service-bus-management-libraries"></a>Библиотеки управления служебной шины

Библиотеки управления служебной шины Azure могут динамически подготавливать пространства имен и сущности служебной шины. Это дает возможность реализовывать сложные развертывания и сценарии обмена сообщениями и позволяет программно определять, какие сущности следует подготовить. В настоящее время эти библиотеки доступны для .NET.

## <a name="supported-functionality"></a>Поддерживаемые функции

* Создание, обновление, удаление пространства имен.
* Создание, обновление, удаление очереди.
* Создание, обновление, удаление раздела.
* Создание, обновление, удаление подписки.

## <a name="prerequisites"></a>Предварительные требования

Чтобы приступить к работе с библиотеками управления служебной шины, нужно пройти аутентификацию в службе Azure Active Directory (AAD). AAD требует аутентификации в качестве субъекта-службы, предоставляющего доступ к вашим ресурсам Azure. Сведения о создании субъекта-службы см. в одной из приведенных ниже статей:  

* [Создание приложения Active Directory и субъекта-службы с доступом к ресурсам с помощью портала](/azure/azure-resource-manager/resource-group-create-service-principal-portal)
* [Использование Azure PowerShell для создания субъекта-службы и доступа к ресурсам](/azure/azure-resource-manager/resource-group-authenticate-service-principal)
* [Использование интерфейса командной строки Azure для создания субъекта-службы и доступа к ресурсам](/azure/azure-resource-manager/resource-group-authenticate-service-principal-cli)

В этих руководствах вы получите `AppId` (идентификатор клиента), `TenantId` и `ClientSecret` (ключ аутентификации), которые используются библиотеками управления для аутентификации. Необходимо иметь разрешения роли **Владелец** для группы ресурсов, которую вы хотите использовать.

## <a name="programming-pattern"></a>Шаблон программирования

Шаблон обработки любого ресурса служебной шины соответствует общему протоколу.

1. Получение маркера из Azure Active Directory с помощью библиотеки **Microsoft.IdentityModel.Clients.ActiveDirectory**.
   ```csharp
   var context = new AuthenticationContext($"https://login.microsoftonline.com/{tenantId}");

   var result = await context.AcquireTokenAsync("https://management.core.windows.net/", new ClientCredential(clientId, clientSecret));
   ```
2. Создание объекта `ServiceBusManagementClient`.

   ```csharp
   var creds = new TokenCredentials(token);
   var sbClient = new ServiceBusManagementClient(creds)
   {
       SubscriptionId = SettingsCache["SubscriptionId"]
   };
   ```
3. Присвоение параметрам `CreateOrUpdate` указанных значений.

   ```csharp
   var queueParams = new QueueCreateOrUpdateParameters()
   {
       Location = SettingsCache["DataCenterLocation"],
       EnablePartitioning = true
   };
   ```
4. Выполнение вызова.

   ```csharp
   await sbClient.Queues.CreateOrUpdateAsync(resourceGroupName, namespaceName, QueueName, queueParams);
   ```

## <a name="next-steps"></a>Дальнейшие действия
* [Пример управления для .NET](https://github.com/Azure-Samples/service-bus-dotnet-management/)
* [Справочник по API Microsoft.Azure.Management.ServiceBus](/dotnet/api/Microsoft.Azure.Management.ServiceBus)
