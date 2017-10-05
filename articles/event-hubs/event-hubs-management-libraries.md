---
title: "Библиотеки управления концентраторов событий Azure | Документация Майкрософт"
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
ms.openlocfilehash: 0d659cb860a6c98342b548212820efe046decfcc
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="event-hubs-management-libraries"></a><span data-ttu-id="ccd96-103">Библиотеки управления концентраторов событий</span><span class="sxs-lookup"><span data-stu-id="ccd96-103">Event Hubs management libraries</span></span>

<span data-ttu-id="ccd96-104">Библиотеки управления концентраторов событий могут динамически подготавливать пространства имен и сущности концентраторов событий.</span><span class="sxs-lookup"><span data-stu-id="ccd96-104">The Event Hubs management libraries can dynamically provision Event Hubs namespaces and entities.</span></span> <span data-ttu-id="ccd96-105">Это дает возможность реализовывать сложные развертывания и сценарии обмена сообщениями, позволяя программно определять, какие сущности следует подготовить.</span><span class="sxs-lookup"><span data-stu-id="ccd96-105">This enables complex deployments and messaging scenarios, so that you can programmatically determine what entities to provision.</span></span> <span data-ttu-id="ccd96-106">В настоящее время эти библиотеки доступны для .NET.</span><span class="sxs-lookup"><span data-stu-id="ccd96-106">These libraries are currently available for .NET.</span></span>

## <a name="supported-functionality"></a><span data-ttu-id="ccd96-107">Поддерживаемые функции</span><span class="sxs-lookup"><span data-stu-id="ccd96-107">Supported functionality</span></span>

* <span data-ttu-id="ccd96-108">Создание, обновление, удаление пространства имен.</span><span class="sxs-lookup"><span data-stu-id="ccd96-108">Namespace creation, update, deletion</span></span>
* <span data-ttu-id="ccd96-109">Создание, обновление, удаление концентраторов событий.</span><span class="sxs-lookup"><span data-stu-id="ccd96-109">Event Hubs creation, update, deletion</span></span>
* <span data-ttu-id="ccd96-110">Создание, обновление, удаление группы потребителей.</span><span class="sxs-lookup"><span data-stu-id="ccd96-110">Consumer Group creation, update, deletion</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ccd96-111">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="ccd96-111">Prerequisites</span></span>

<span data-ttu-id="ccd96-112">Чтобы приступить к работе с библиотеками управления концентраторов событий, нужно пройти аутентификацию в Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="ccd96-112">To get started using the Event Hubs management libraries, you must authenticate with Azure Active Directory (AAD).</span></span> <span data-ttu-id="ccd96-113">AAD требует аутентификации в качестве субъекта-службы, предоставляющего доступ к вашим ресурсам Azure.</span><span class="sxs-lookup"><span data-stu-id="ccd96-113">AAD requires that you authenticate as a service principal, which provides access to your Azure resources.</span></span> <span data-ttu-id="ccd96-114">Сведения о создании субъекта-службы см. в одной из приведенных ниже статей:</span><span class="sxs-lookup"><span data-stu-id="ccd96-114">For information about creating a service principal, see one of these articles:</span></span>  

* [<span data-ttu-id="ccd96-115">Создание приложения Active Directory и субъекта-службы с доступом к ресурсам с помощью портала</span><span class="sxs-lookup"><span data-stu-id="ccd96-115">Use the Azure portal to create Active Directory application and service principal that can access resources</span></span>](../azure-resource-manager/resource-group-create-service-principal-portal.md)
* [<span data-ttu-id="ccd96-116">Использование Azure PowerShell для создания субъекта-службы и доступа к ресурсам</span><span class="sxs-lookup"><span data-stu-id="ccd96-116">Use Azure PowerShell to create a service principal to access resources</span></span>](../azure-resource-manager/resource-group-authenticate-service-principal.md)
* [<span data-ttu-id="ccd96-117">Использование интерфейса командной строки Azure для создания субъекта-службы и доступа к ресурсам</span><span class="sxs-lookup"><span data-stu-id="ccd96-117">Use Azure CLI to create a service principal to access resources</span></span>](../azure-resource-manager/resource-group-authenticate-service-principal-cli.md)

<span data-ttu-id="ccd96-118">В этих руководствах вы получите `AppId` (идентификатор клиента), `TenantId` и `ClientSecret` (ключ аутентификации), которые используются библиотеками управления для аутентификации.</span><span class="sxs-lookup"><span data-stu-id="ccd96-118">These tutorials provide you with an `AppId` (Client ID), `TenantId`, and `ClientSecret` (authentication key), all of which are used for authentication by the management libraries.</span></span> <span data-ttu-id="ccd96-119">Необходимо иметь разрешения роли **Владелец** для группы ресурсов, которую вы хотите использовать.</span><span class="sxs-lookup"><span data-stu-id="ccd96-119">You must have **Owner** permissions for the resource group on which you want to run.</span></span>

## <a name="programming-pattern"></a><span data-ttu-id="ccd96-120">Шаблон программирования</span><span class="sxs-lookup"><span data-stu-id="ccd96-120">Programming pattern</span></span>

<span data-ttu-id="ccd96-121">Шаблон обработки любого ресурса концентраторов событий придерживается общего протокола.</span><span class="sxs-lookup"><span data-stu-id="ccd96-121">The pattern to manipulate any Event Hubs resource follows a common protocol:</span></span>

1. <span data-ttu-id="ccd96-122">Получение токена из AAD с использованием библиотеки `Microsoft.IdentityModel.Clients.ActiveDirectory`.</span><span class="sxs-lookup"><span data-stu-id="ccd96-122">Obtain a token from AAD using the `Microsoft.IdentityModel.Clients.ActiveDirectory` library.</span></span>
    ```csharp
    var context = new AuthenticationContext($"https://login.microsoftonline.com/{tenantId}");

    var result = await context.AcquireTokenAsync(
        "https://management.core.windows.net/",
        new ClientCredential(clientId, clientSecret)
    );
    ```

1. <span data-ttu-id="ccd96-123">Создание объекта `EventHubManagementClient`.</span><span class="sxs-lookup"><span data-stu-id="ccd96-123">Create the `EventHubManagementClient` object.</span></span>
    ```csharp
    var creds = new TokenCredentials(token);
    var ehClient = new EventHubManagementClient(creds)
    {
        SubscriptionId = SettingsCache["SubscriptionId"]
    };
    ```

1. <span data-ttu-id="ccd96-124">Присвоение параметрам `CreateOrUpdate` указанных значений.</span><span class="sxs-lookup"><span data-stu-id="ccd96-124">Set the `CreateOrUpdate` parameters to your specified values.</span></span>
    ```csharp
    var ehParams = new EventHubCreateOrUpdateParameters()
    {
        Location = SettingsCache["DataCenterLocation"]
    };
    ```

1. <span data-ttu-id="ccd96-125">Выполнение вызова.</span><span class="sxs-lookup"><span data-stu-id="ccd96-125">Execute the call.</span></span>
    ```csharp
    await ehClient.EventHubs.CreateOrUpdateAsync(resourceGroupName, namespaceName, EventHubName, ehParams);
    ```

## <a name="next-steps"></a><span data-ttu-id="ccd96-126">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ccd96-126">Next steps</span></span>
* [<span data-ttu-id="ccd96-127">Пример управления для .NET</span><span class="sxs-lookup"><span data-stu-id="ccd96-127">.NET Management sample</span></span>](https://github.com/Azure-Samples/event-hubs-dotnet-management/)
* [<span data-ttu-id="ccd96-128">Справочник по Microsoft.Azure.Management.EventHub</span><span class="sxs-lookup"><span data-stu-id="ccd96-128">Microsoft.Azure.Management.EventHub Reference</span></span>](/dotnet/api/Microsoft.Azure.Management.EventHub) 
