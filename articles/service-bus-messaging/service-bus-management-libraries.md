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
# <a name="service-bus-management-libraries"></a><span data-ttu-id="7a78f-103">Библиотеки управления служебной шины</span><span class="sxs-lookup"><span data-stu-id="7a78f-103">Service Bus management libraries</span></span>

<span data-ttu-id="7a78f-104">библиотеки управления Hello Azure Service Bus можно динамически подготавливать пространства имен служебной шины и сущностей.</span><span class="sxs-lookup"><span data-stu-id="7a78f-104">hello Azure Service Bus management libraries can dynamically provision Service Bus namespaces and entities.</span></span> <span data-ttu-id="7a78f-105">Это позволяет сложных развертываний и сценариев обмена сообщениями, а также позволяет определить, какие сущности tooprovision tooprogrammatically.</span><span class="sxs-lookup"><span data-stu-id="7a78f-105">This enables complex deployments and messaging scenarios, and makes it possible tooprogrammatically determine what entities tooprovision.</span></span> <span data-ttu-id="7a78f-106">В настоящее время эти библиотеки доступны для .NET.</span><span class="sxs-lookup"><span data-stu-id="7a78f-106">These libraries are currently available for .NET.</span></span>

## <a name="supported-functionality"></a><span data-ttu-id="7a78f-107">Поддерживаемые функции</span><span class="sxs-lookup"><span data-stu-id="7a78f-107">Supported functionality</span></span>

* <span data-ttu-id="7a78f-108">Создание, обновление, удаление пространства имен.</span><span class="sxs-lookup"><span data-stu-id="7a78f-108">Namespace creation, update, deletion</span></span>
* <span data-ttu-id="7a78f-109">Создание, обновление, удаление очереди.</span><span class="sxs-lookup"><span data-stu-id="7a78f-109">Queue creation, update, deletion</span></span>
* <span data-ttu-id="7a78f-110">Создание, обновление, удаление раздела.</span><span class="sxs-lookup"><span data-stu-id="7a78f-110">Topic creation, update, deletion</span></span>
* <span data-ttu-id="7a78f-111">Создание, обновление, удаление подписки.</span><span class="sxs-lookup"><span data-stu-id="7a78f-111">Subscription creation, update, deletion</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7a78f-112">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="7a78f-112">Prerequisites</span></span>

<span data-ttu-id="7a78f-113">tooget работы с использованием библиотеки управления Service Bus hello, вы должны проверить подлинность hello службы Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="7a78f-113">tooget started using hello Service Bus management libraries, you must authenticate with hello Azure Active Directory (AAD) service.</span></span> <span data-ttu-id="7a78f-114">AAD требует проверки подлинности как участника-службы, который предоставляет доступ tooyour ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="7a78f-114">AAD requires that you authenticate as a service principal, which provides access tooyour Azure resources.</span></span> <span data-ttu-id="7a78f-115">Сведения о создании субъекта-службы см. в одной из приведенных ниже статей:</span><span class="sxs-lookup"><span data-stu-id="7a78f-115">For information about creating a service principal, see one of these articles:</span></span>  

* [<span data-ttu-id="7a78f-116">Использовать приложение Active Directory Azure портала toocreate hello и участника-службы, могут обращаться к ресурсам</span><span class="sxs-lookup"><span data-stu-id="7a78f-116">Use hello Azure portal toocreate Active Directory application and service principal that can access resources</span></span>](/azure/azure-resource-manager/resource-group-create-service-principal-portal)
* [<span data-ttu-id="7a78f-117">Использование Azure PowerShell toocreate ресурсов tooaccess участника службы</span><span class="sxs-lookup"><span data-stu-id="7a78f-117">Use Azure PowerShell toocreate a service principal tooaccess resources</span></span>](/azure/azure-resource-manager/resource-group-authenticate-service-principal)
* [<span data-ttu-id="7a78f-118">Используйте основной tooaccess ресурсов службы toocreate Azure CLI</span><span class="sxs-lookup"><span data-stu-id="7a78f-118">Use Azure CLI toocreate a service principal tooaccess resources</span></span>](/azure/azure-resource-manager/resource-group-authenticate-service-principal-cli)

<span data-ttu-id="7a78f-119">Эти учебники предоставляют `AppId` (идентификатор клиента), `TenantId`, и `ClientSecret` (ключ проверки подлинности), каждый из которых используются для проверки подлинности управления библиотеками hello.</span><span class="sxs-lookup"><span data-stu-id="7a78f-119">These tutorials provide you with an `AppId` (Client ID), `TenantId`, and `ClientSecret` (authentication key), all of which are used for authentication by hello management libraries.</span></span> <span data-ttu-id="7a78f-120">Необходимо иметь **владельца** разрешения для группы ресурсов hello, над которым необходимо toorun.</span><span class="sxs-lookup"><span data-stu-id="7a78f-120">You must have **Owner** permissions for hello resource group on which you wish toorun.</span></span>

## <a name="programming-pattern"></a><span data-ttu-id="7a78f-121">Шаблон программирования</span><span class="sxs-lookup"><span data-stu-id="7a78f-121">Programming pattern</span></span>

<span data-ttu-id="7a78f-122">Здравствуйте, toomanipulate шаблон общего протокола соответствует любой ресурс служебной шины:</span><span class="sxs-lookup"><span data-stu-id="7a78f-122">hello pattern toomanipulate any Service Bus resource follows a common protocol:</span></span>

1. <span data-ttu-id="7a78f-123">Получение токена от Azure Active Directory с помощью hello **Microsoft.IdentityModel.Clients.ActiveDirectory** библиотеки.</span><span class="sxs-lookup"><span data-stu-id="7a78f-123">Obtain a token from Azure Active Directory using hello **Microsoft.IdentityModel.Clients.ActiveDirectory** library.</span></span>
   ```csharp
   var context = new AuthenticationContext($"https://login.microsoftonline.com/{tenantId}");

   var result = await context.AcquireTokenAsync("https://management.core.windows.net/", new ClientCredential(clientId, clientSecret));
   ```

1. <span data-ttu-id="7a78f-124">Создать hello `ServiceBusManagementClient` объекта.</span><span class="sxs-lookup"><span data-stu-id="7a78f-124">Create hello `ServiceBusManagementClient` object.</span></span>

   ```csharp
   var creds = new TokenCredentials(token);
   var sbClient = new ServiceBusManagementClient(creds)
   {
       SubscriptionId = SettingsCache["SubscriptionId"]
   };
   ```

1. <span data-ttu-id="7a78f-125">Набор hello `CreateOrUpdate` tooyour параметры указанные значения.</span><span class="sxs-lookup"><span data-stu-id="7a78f-125">Set hello `CreateOrUpdate` parameters tooyour specified values.</span></span>

   ```csharp
   var queueParams = new QueueCreateOrUpdateParameters()
   {
       Location = SettingsCache["DataCenterLocation"],
       EnablePartitioning = true
   };
   ```

1. <span data-ttu-id="7a78f-126">Hello вызова Execute.</span><span class="sxs-lookup"><span data-stu-id="7a78f-126">Execute hello call.</span></span>

   ```csharp
   await sbClient.Queues.CreateOrUpdateAsync(resourceGroupName, namespaceName, QueueName, queueParams);
   ```

## <a name="next-steps"></a><span data-ttu-id="7a78f-127">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7a78f-127">Next steps</span></span>
* [<span data-ttu-id="7a78f-128">Пример управления для .NET</span><span class="sxs-lookup"><span data-stu-id="7a78f-128">.NET management sample</span></span>](https://github.com/Azure-Samples/service-bus-dotnet-management/)
* [<span data-ttu-id="7a78f-129">Справочник по API Microsoft.Azure.Management.ServiceBus</span><span class="sxs-lookup"><span data-stu-id="7a78f-129">Microsoft.Azure.Management.ServiceBus API reference</span></span>](/dotnet/api/Microsoft.Azure.Management.ServiceBus)
