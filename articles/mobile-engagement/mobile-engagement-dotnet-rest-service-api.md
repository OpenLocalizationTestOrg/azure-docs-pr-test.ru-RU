---
title: "hello aaaUsing tooaccess API-интерфейса REST API службы Azure Mobile Engagement"
description: "Описывает, каким образом toouse hello API-интерфейс REST Mobile Engagement tooaccess API-интерфейсы службы Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: wesmc7777
manager: erikre
editor: 
ms.assetid: e8df4897-55ee-45df-b41e-ff187e3d9d12
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 10/05/2016
ms.author: wesmc;ricksal
ms.openlocfilehash: 315761299a42df6f65e81df20e632f9713844b0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="using-rest-tooaccess-azure-mobile-engagement-service-apis"></a><span data-ttu-id="df650-103">С помощью tooaccess REST API службы Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="df650-103">Using REST tooaccess Azure Mobile Engagement Service APIs</span></span>
<span data-ttu-id="df650-104">Azure Mobile Engagement предоставляет hello [Azure Mobile Engagement REST API](https://msdn.microsoft.com/library/azure/mt683754.aspx) автоматически устройств toomanage кампании Reach и Push-уведомлений и т. д.</span><span class="sxs-lookup"><span data-stu-id="df650-104">Azure Mobile Engagement provides hello [Azure Mobile Engagement REST API](https://msdn.microsoft.com/library/azure/mt683754.aspx) for you toomanage Devices, Reach/Push campaigns etc.</span></span>

> [!NOTE]
> <span data-ttu-id="df650-105">Служба Azure Mobile Engagement Hello будет прекращено 2018 марта и в настоящее время только доступные tooexisting клиентов.</span><span class="sxs-lookup"><span data-stu-id="df650-105">hello Azure Mobile Engagement service will be retired March 2018 and is currently only available tooexisting customers.</span></span> <span data-ttu-id="df650-106">Дополнительные сведения см. на странице [Службы мобильного взаимодействия](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span><span class="sxs-lookup"><span data-stu-id="df650-106">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

<span data-ttu-id="df650-107">Если не хотите toouse hello интерфейсы API REST напрямую, мы также предоставляем [файл Swagger](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-mobileengagement/2014-12-01/swagger/mobile-engagement.json) , можно использовать с средств toogenerate пакеты SDK для предпочитаемого языка.</span><span class="sxs-lookup"><span data-stu-id="df650-107">If you do not want toouse hello REST APIs directly, we also provide a [Swagger file](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-mobileengagement/2014-12-01/swagger/mobile-engagement.json) that you can use with tools toogenerate SDKs for your preferred language.</span></span> <span data-ttu-id="df650-108">Мы рекомендуем использовать hello [AutoRest](https://github.com/Azure/AutoRest) средства toogenerate SDK из нашего файла Swagger.</span><span class="sxs-lookup"><span data-stu-id="df650-108">We recommend using hello [AutoRest](https://github.com/Azure/AutoRest) tool toogenerate your SDK from our Swagger file.</span></span> <span data-ttu-id="df650-109">Мы создали таким же способом, что позволяет вам toointeract с этими интерфейсами API с помощью оболочки C# .NET SDK, и у вас нет toodo hello согласование маркера проверки подлинности и обновите самостоятельно.</span><span class="sxs-lookup"><span data-stu-id="df650-109">We have created a .NET SDK in a similar manner which allows you toointeract with these APIs using a C# wrapper and you don't have toodo hello authentication token negotiation and refresh yourself.</span></span> <span data-ttu-id="df650-110">В разделе [образца пакета SDK .NET API службы](mobile-engagement-dotnet-sdk-service-api.md) toolearn как toouse hello .net SDK для API</span><span class="sxs-lookup"><span data-stu-id="df650-110">See [Service API .NET SDK Sample](mobile-engagement-dotnet-sdk-service-api.md) toolearn how toouse hello .net SDK for API</span></span>
