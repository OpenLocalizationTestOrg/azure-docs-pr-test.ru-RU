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
# <a name="event-hubs-management-libraries"></a><span data-ttu-id="82720-103">Библиотеки управления концентраторов событий</span><span class="sxs-lookup"><span data-stu-id="82720-103">Event Hubs management libraries</span></span>

<span data-ttu-id="82720-104">библиотеки управления Hello концентраторов событий можно динамически подготавливать концентраторов событий пространств имен и сущностей.</span><span class="sxs-lookup"><span data-stu-id="82720-104">hello Event Hubs management libraries can dynamically provision Event Hubs namespaces and entities.</span></span> <span data-ttu-id="82720-105">Благодаря этому сложных развертываний и сценариев обмена сообщениями, чтобы программно определить, какие tooprovision сущностей.</span><span class="sxs-lookup"><span data-stu-id="82720-105">This enables complex deployments and messaging scenarios, so that you can programmatically determine what entities tooprovision.</span></span> <span data-ttu-id="82720-106">В настоящее время эти библиотеки доступны для .NET.</span><span class="sxs-lookup"><span data-stu-id="82720-106">These libraries are currently available for .NET.</span></span>

## <a name="supported-functionality"></a><span data-ttu-id="82720-107">Поддерживаемые функции</span><span class="sxs-lookup"><span data-stu-id="82720-107">Supported functionality</span></span>

* <span data-ttu-id="82720-108">Создание, обновление, удаление пространства имен.</span><span class="sxs-lookup"><span data-stu-id="82720-108">Namespace creation, update, deletion</span></span>
* <span data-ttu-id="82720-109">Создание, обновление, удаление концентраторов событий.</span><span class="sxs-lookup"><span data-stu-id="82720-109">Event Hubs creation, update, deletion</span></span>
* <span data-ttu-id="82720-110">Создание, обновление, удаление группы потребителей.</span><span class="sxs-lookup"><span data-stu-id="82720-110">Consumer Group creation, update, deletion</span></span>

## <a name="prerequisites"></a><span data-ttu-id="82720-111">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="82720-111">Prerequisites</span></span>

<span data-ttu-id="82720-112">tooget работы с использованием библиотеки управления hello концентраторов событий, необходимо проверить подлинность с помощью Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="82720-112">tooget started using hello Event Hubs management libraries, you must authenticate with Azure Active Directory (AAD).</span></span> <span data-ttu-id="82720-113">AAD требует проверки подлинности как участника-службы, который предоставляет доступ tooyour ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="82720-113">AAD requires that you authenticate as a service principal, which provides access tooyour Azure resources.</span></span> <span data-ttu-id="82720-114">Сведения о создании субъекта-службы см. в одной из приведенных ниже статей:</span><span class="sxs-lookup"><span data-stu-id="82720-114">For information about creating a service principal, see one of these articles:</span></span>  

* [<span data-ttu-id="82720-115">Использовать приложение Active Directory Azure портала toocreate hello и участника-службы, могут обращаться к ресурсам</span><span class="sxs-lookup"><span data-stu-id="82720-115">Use hello Azure portal toocreate Active Directory application and service principal that can access resources</span></span>](../azure-resource-manager/resource-group-create-service-principal-portal.md)
* [<span data-ttu-id="82720-116">Использование Azure PowerShell toocreate ресурсов tooaccess участника службы</span><span class="sxs-lookup"><span data-stu-id="82720-116">Use Azure PowerShell toocreate a service principal tooaccess resources</span></span>](../azure-resource-manager/resource-group-authenticate-service-principal.md)
* [<span data-ttu-id="82720-117">Используйте основной tooaccess ресурсов службы toocreate Azure CLI</span><span class="sxs-lookup"><span data-stu-id="82720-117">Use Azure CLI toocreate a service principal tooaccess resources</span></span>](../azure-resource-manager/resource-group-authenticate-service-principal-cli.md)

<span data-ttu-id="82720-118">Эти учебники предоставляют `AppId` (идентификатор клиента), `TenantId`, и `ClientSecret` (ключ проверки подлинности), каждый из которых используются для проверки подлинности управления библиотеками hello.</span><span class="sxs-lookup"><span data-stu-id="82720-118">These tutorials provide you with an `AppId` (Client ID), `TenantId`, and `ClientSecret` (authentication key), all of which are used for authentication by hello management libraries.</span></span> <span data-ttu-id="82720-119">Необходимо иметь **владельца** разрешения для группы ресурсов hello, на котором будет toorun.</span><span class="sxs-lookup"><span data-stu-id="82720-119">You must have **Owner** permissions for hello resource group on which you want toorun.</span></span>

## <a name="programming-pattern"></a><span data-ttu-id="82720-120">Шаблон программирования</span><span class="sxs-lookup"><span data-stu-id="82720-120">Programming pattern</span></span>

<span data-ttu-id="82720-121">Здравствуйте, шаблон toomanipulate любой ресурс концентраторов событий соответствует общего протокола:</span><span class="sxs-lookup"><span data-stu-id="82720-121">hello pattern toomanipulate any Event Hubs resource follows a common protocol:</span></span>

1. <span data-ttu-id="82720-122">Получение токена от AAD с помощью hello `Microsoft.IdentityModel.Clients.ActiveDirectory` библиотеки.</span><span class="sxs-lookup"><span data-stu-id="82720-122">Obtain a token from AAD using hello `Microsoft.IdentityModel.Clients.ActiveDirectory` library.</span></span>
    ```csharp
    var context = new AuthenticationContext($"https://login.microsoftonline.com/{tenantId}");

    var result = await context.AcquireTokenAsync(
        "https://management.core.windows.net/",
        new ClientCredential(clientId, clientSecret)
    );
    ```

1. <span data-ttu-id="82720-123">Создать hello `EventHubManagementClient` объекта.</span><span class="sxs-lookup"><span data-stu-id="82720-123">Create hello `EventHubManagementClient` object.</span></span>
    ```csharp
    var creds = new TokenCredentials(token);
    var ehClient = new EventHubManagementClient(creds)
    {
        SubscriptionId = SettingsCache["SubscriptionId"]
    };
    ```

1. <span data-ttu-id="82720-124">Набор hello `CreateOrUpdate` tooyour параметры указанные значения.</span><span class="sxs-lookup"><span data-stu-id="82720-124">Set hello `CreateOrUpdate` parameters tooyour specified values.</span></span>
    ```csharp
    var ehParams = new EventHubCreateOrUpdateParameters()
    {
        Location = SettingsCache["DataCenterLocation"]
    };
    ```

1. <span data-ttu-id="82720-125">Hello вызова Execute.</span><span class="sxs-lookup"><span data-stu-id="82720-125">Execute hello call.</span></span>
    ```csharp
    await ehClient.EventHubs.CreateOrUpdateAsync(resourceGroupName, namespaceName, EventHubName, ehParams);
    ```

## <a name="next-steps"></a><span data-ttu-id="82720-126">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="82720-126">Next steps</span></span>
* [<span data-ttu-id="82720-127">Пример управления для .NET</span><span class="sxs-lookup"><span data-stu-id="82720-127">.NET Management sample</span></span>](https://github.com/Azure-Samples/event-hubs-dotnet-management/)
* [<span data-ttu-id="82720-128">Справочник по Microsoft.Azure.Management.EventHub</span><span class="sxs-lookup"><span data-stu-id="82720-128">Microsoft.Azure.Management.EventHub Reference</span></span>](/dotnet/api/Microsoft.Azure.Management.EventHub) 
