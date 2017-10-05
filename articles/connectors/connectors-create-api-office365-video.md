---
title: "Использование соединителя Office 365 Видео в приложениях логики | Документация Майкрософт"
description: "Начало использования соединителя Office 365 Видео в приложениях логики службы приложений Microsoft Azure"
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 738e5aa7-2523-4116-8b65-211b9063852d
ms.service: multiple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: f0e3613d4a3fd5478787c0365eb7a0bcde886c81
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-office365-video-connector"></a><span data-ttu-id="904ca-103">Начало работы с соединителем Office 365 Видео</span><span class="sxs-lookup"><span data-stu-id="904ca-103">Get started with the Office365 Video connector</span></span>
<span data-ttu-id="904ca-104">Подключившись к Office 365 Видео, вы сможете получать информацию об Office 365 Видео, список видео и многое другое.</span><span class="sxs-lookup"><span data-stu-id="904ca-104">Connect to Office 365 Video to get information about an Office 365 video, get a list of videos, and more.</span></span> <span data-ttu-id="904ca-105">С помощью Office 365 Видео вы можете:</span><span class="sxs-lookup"><span data-stu-id="904ca-105">With Office 365 Video, you can:</span></span>

* <span data-ttu-id="904ca-106">формировать бизнес-процессы на основе данных, получаемых из Office 365 Видео;</span><span class="sxs-lookup"><span data-stu-id="904ca-106">Build your business flow based on the data you get from Office 365 Video.</span></span> 
* <span data-ttu-id="904ca-107">использовать действия для проверки состояния видеопортала, получения списка всех видео, имеющихся в канале, и т. д.</span><span class="sxs-lookup"><span data-stu-id="904ca-107">Use actions that check the video portal status, get a list of all video in a channel, and more.</span></span> <span data-ttu-id="904ca-108">Эти действия получают ответ и делают выходные данные доступными для использования другими действиями.</span><span class="sxs-lookup"><span data-stu-id="904ca-108">These actions get a response, and then make the output available for other actions.</span></span> <span data-ttu-id="904ca-109">Например, можно воспользоваться соединителем Поиска Bing для поиска видео в Office 365, а затем соединителем Office 365 Видео для получения сведений об этом видео.</span><span class="sxs-lookup"><span data-stu-id="904ca-109">For example, you can use the Bing Search connector to search for Office 365 videos, and then use the Office 365 video connector to get information about that video.</span></span> <span data-ttu-id="904ca-110">Если видео соответствует вашим требованиям, его можно опубликовать в Facebook.</span><span class="sxs-lookup"><span data-stu-id="904ca-110">If the video meets your requirements, you can post this video on Facebook.</span></span> 

<span data-ttu-id="904ca-111">Для начала можно создать приложение логики, как описано [здесь](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="904ca-111">You can get started by creating a logic app now, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-to-office365-video-connector"></a><span data-ttu-id="904ca-112">Создание подключения к соединителю Office 365 Видео</span><span class="sxs-lookup"><span data-stu-id="904ca-112">Create a connection to Office365 Video connector</span></span>
<span data-ttu-id="904ca-113">При добавлении этого соединителя в приложения логики необходимо войти в учетную запись Office 365 Видео и разрешить приложениям логики подключаться к вашей учетной записи.</span><span class="sxs-lookup"><span data-stu-id="904ca-113">When you add this connector to your logic apps, you must sign-in to your Office 365 Video account and allow logic apps to connect to your account.</span></span>

> [!INCLUDE [Steps to create a connection to Office 365 Video](../../includes/connectors-create-api-office365video.md)]
> 
> 

<span data-ttu-id="904ca-114">После создания подключения укажите свойства Office 365 Видео, такие как имя клиента или идентификатор канала.</span><span class="sxs-lookup"><span data-stu-id="904ca-114">After you create the connection, you enter the Office 365 video properties, like the tenant name or channel ID.</span></span> 


## <a name="connector-specific-details"></a><span data-ttu-id="904ca-115">Сведения о соединителях</span><span class="sxs-lookup"><span data-stu-id="904ca-115">Connector-specific details</span></span>

<span data-ttu-id="904ca-116">Информацию о существующих ограничениях, а также о триггерах и действиях, определенных в Swagger, см. в статье со [сведениями о соединителях](/connectors/office365videoconnector/).</span><span class="sxs-lookup"><span data-stu-id="904ca-116">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/office365videoconnector/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="904ca-117">Дополнительные сведения о соединителях</span><span class="sxs-lookup"><span data-stu-id="904ca-117">More connectors</span></span>
<span data-ttu-id="904ca-118">Вы можете вернуться к [списку интерфейсов API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="904ca-118">Go back to the [APIs list](apis-list.md).</span></span>