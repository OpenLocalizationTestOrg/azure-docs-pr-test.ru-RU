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
ms.date: 07/05/2017
ms.author: sethm
ms.openlocfilehash: 1db00dc1f91e8976b622030450445babbe547ad8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="service-bus-management-libraries"></a><span data-ttu-id="0388f-103">Библиотеки управления служебной шины</span><span class="sxs-lookup"><span data-stu-id="0388f-103">Service Bus management libraries</span></span>

<span data-ttu-id="0388f-104">Библиотеки управления служебной шины Azure могут динамически подготавливать пространства имен и сущности служебной шины.</span><span class="sxs-lookup"><span data-stu-id="0388f-104">The Azure Service Bus management libraries can dynamically provision Service Bus namespaces and entities.</span></span> <span data-ttu-id="0388f-105">Это дает возможность реализовывать сложные развертывания и сценарии обмена сообщениями и позволяет программно определять, какие сущности следует подготовить.</span><span class="sxs-lookup"><span data-stu-id="0388f-105">This enables complex deployments and messaging scenarios, and makes it possible to programmatically determine what entities to provision.</span></span> <span data-ttu-id="0388f-106">В настоящее время эти библиотеки доступны для .NET.</span><span class="sxs-lookup"><span data-stu-id="0388f-106">These libraries are currently available for .NET.</span></span>

## <a name="supported-functionality"></a><span data-ttu-id="0388f-107">Поддерживаемые функции</span><span class="sxs-lookup"><span data-stu-id="0388f-107">Supported functionality</span></span>

* <span data-ttu-id="0388f-108">Создание, обновление, удаление пространства имен.</span><span class="sxs-lookup"><span data-stu-id="0388f-108">Namespace creation, update, deletion</span></span>
* <span data-ttu-id="0388f-109">Создание, обновление, удаление очереди.</span><span class="sxs-lookup"><span data-stu-id="0388f-109">Queue creation, update, deletion</span></span>
* <span data-ttu-id="0388f-110">Создание, обновление, удаление раздела.</span><span class="sxs-lookup"><span data-stu-id="0388f-110">Topic creation, update, deletion</span></span>
* <span data-ttu-id="0388f-111">Создание, обновление, удаление подписки.</span><span class="sxs-lookup"><span data-stu-id="0388f-111">Subscription creation, update, deletion</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0388f-112">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="0388f-112">Prerequisites</span></span>

<span data-ttu-id="0388f-113">Чтобы приступить к работе с библиотеками управления служебной шины, нужно пройти аутентификацию в службе Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="0388f-113">To get started using the Service Bus management libraries, you must authenticate with the Azure Active Directory (AAD) service.</span></span> <span data-ttu-id="0388f-114">AAD требует аутентификации в качестве субъекта-службы, предоставляющего доступ к вашим ресурсам Azure.</span><span class="sxs-lookup"><span data-stu-id="0388f-114">AAD requires that you authenticate as a service principal, which provides access to your Azure resources.</span></span> <span data-ttu-id="0388f-115">Сведения о создании субъекта-службы см. в одной из приведенных ниже статей:</span><span class="sxs-lookup"><span data-stu-id="0388f-115">For information about creating a service principal, see one of these articles:</span></span>  

* [<span data-ttu-id="0388f-116">Создание приложения Active Directory и субъекта-службы с доступом к ресурсам с помощью портала</span><span class="sxs-lookup"><span data-stu-id="0388f-116">Use the Azure portal to create Active Directory application and service principal that can access resources</span></span>](/azure/azure-resource-manager/resource-group-create-service-principal-portal)
* [<span data-ttu-id="0388f-117">Использование Azure PowerShell для создания субъекта-службы и доступа к ресурсам</span><span class="sxs-lookup"><span data-stu-id="0388f-117">Use Azure PowerShell to create a service principal to access resources</span></span>](/azure/azure-resource-manager/resource-group-authenticate-service-principal)
* [<span data-ttu-id="0388f-118">Использование интерфейса командной строки Azure для создания субъекта-службы и доступа к ресурсам</span><span class="sxs-lookup"><span data-stu-id="0388f-118">Use Azure CLI to create a service principal to access resources</span></span>](/azure/azure-resource-manager/resource-group-authenticate-service-principal-cli)

<span data-ttu-id="0388f-119">В этих руководствах вы получите `AppId` (идентификатор клиента), `TenantId` и `ClientSecret` (ключ аутентификации), которые используются библиотеками управления для аутентификации.</span><span class="sxs-lookup"><span data-stu-id="0388f-119">These tutorials provide you with an `AppId` (Client ID), `TenantId`, and `ClientSecret` (authentication key), all of which are used for authentication by the management libraries.</span></span> <span data-ttu-id="0388f-120">Необходимо иметь разрешения роли **Владелец** для группы ресурсов, которую вы хотите использовать.</span><span class="sxs-lookup"><span data-stu-id="0388f-120">You must have **Owner** permissions for the resource group on which you wish to run.</span></span>

## <a name="programming-pattern"></a><span data-ttu-id="0388f-121">Шаблон программирования</span><span class="sxs-lookup"><span data-stu-id="0388f-121">Programming pattern</span></span>

<span data-ttu-id="0388f-122">Шаблон обработки любого ресурса служебной шины соответствует общему протоколу.</span><span class="sxs-lookup"><span data-stu-id="0388f-122">The pattern to manipulate any Service Bus resource follows a common protocol:</span></span>

1. <span data-ttu-id="0388f-123">Получение маркера из Azure Active Directory с помощью библиотеки **Microsoft.IdentityModel.Clients.ActiveDirectory**.</span><span class="sxs-lookup"><span data-stu-id="0388f-123">Obtain a token from Azure Active Directory using the **Microsoft.IdentityModel.Clients.ActiveDirectory** library.</span></span>
   ```csharp
   var context = new AuthenticationContext($"https://login.microsoftonline.com/{tenantId}");

   var result = await context.AcquireTokenAsync("https://management.core.windows.net/", new ClientCredential(clientId, clientSecret));
   ```

1. <span data-ttu-id="0388f-124">Создание объекта `ServiceBusManagementClient`.</span><span class="sxs-lookup"><span data-stu-id="0388f-124">Create the `ServiceBusManagementClient` object.</span></span>

   ```csharp
   var creds = new TokenCredentials(token);
   var sbClient = new ServiceBusManagementClient(creds)
   {
       SubscriptionId = SettingsCache["SubscriptionId"]
   };
   ```

1. <span data-ttu-id="0388f-125">Присвоение параметрам `CreateOrUpdate` указанных значений.</span><span class="sxs-lookup"><span data-stu-id="0388f-125">Set the `CreateOrUpdate` parameters to your specified values.</span></span>

   ```csharp
   var queueParams = new QueueCreateOrUpdateParameters()
   {
       Location = SettingsCache["DataCenterLocation"],
       EnablePartitioning = true
   };
   ```

1. <span data-ttu-id="0388f-126">Выполнение вызова.</span><span class="sxs-lookup"><span data-stu-id="0388f-126">Execute the call.</span></span>

   ```csharp
   await sbClient.Queues.CreateOrUpdateAsync(resourceGroupName, namespaceName, QueueName, queueParams);
   ```

## <a name="next-steps"></a><span data-ttu-id="0388f-127">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0388f-127">Next steps</span></span>
* [<span data-ttu-id="0388f-128">Пример управления для .NET</span><span class="sxs-lookup"><span data-stu-id="0388f-128">.NET management sample</span></span>](https://github.com/Azure-Samples/service-bus-dotnet-management/)
* [<span data-ttu-id="0388f-129">Справочник по API Microsoft.Azure.Management.ServiceBus</span><span class="sxs-lookup"><span data-stu-id="0388f-129">Microsoft.Azure.Management.ServiceBus API reference</span></span>](/dotnet/api/Microsoft.Azure.Management.ServiceBus)
