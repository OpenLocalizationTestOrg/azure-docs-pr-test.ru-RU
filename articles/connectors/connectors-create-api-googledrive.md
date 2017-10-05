---
title: "Добавление соединителя Google Диска в приложения логики | Документация Майкрософт"
description: "Обзор соединителя Google-диска с параметрами интерфейса API REST"
services: 
suite: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: b2bcebc5-02d2-435b-b0da-ef53bc51c4b6
ms.service: multiple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/07/2016
ms.author: mandia; ladocs
ms.openlocfilehash: c066a10b33e172eb5f16eede43ec407794000c90
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-google-drive-connector"></a><span data-ttu-id="ee98f-103">Начало работы с соединителем Google-диска</span><span class="sxs-lookup"><span data-stu-id="ee98f-103">Get started with the Google Drive connector</span></span>
<span data-ttu-id="ee98f-104">Подключитесь к Google-диску, чтобы создавать файлы, получать строки и выполнять множество других действий.</span><span class="sxs-lookup"><span data-stu-id="ee98f-104">Connect to Google Drive to create files, get rows, and more.</span></span> <span data-ttu-id="ee98f-105">С помощью Google-диска вы можете:</span><span class="sxs-lookup"><span data-stu-id="ee98f-105">With Google Drive, you can:</span></span> 

* <span data-ttu-id="ee98f-106">формировать бизнес-процессы на основе данных, получаемых в результате поиска;</span><span class="sxs-lookup"><span data-stu-id="ee98f-106">Build your business flow based on the data you get from your search.</span></span> 
* <span data-ttu-id="ee98f-107">использовать действия для поиска изображений, новостей и многого другого.</span><span class="sxs-lookup"><span data-stu-id="ee98f-107">Use actions to search images, search the news, and more.</span></span> <span data-ttu-id="ee98f-108">Эти действия получают ответ и делают выходные данные доступными для использования другими действиями.</span><span class="sxs-lookup"><span data-stu-id="ee98f-108">These actions get a response, and then make the output available for other actions.</span></span> <span data-ttu-id="ee98f-109">Например, можно найти видеоролик, а затем с помощью Twitter опубликовать его в веб-канале Twitter.</span><span class="sxs-lookup"><span data-stu-id="ee98f-109">For example, you can search for a video, and then use Twitter to post that video to a Twitter feed.</span></span>

<span data-ttu-id="ee98f-110">Для начала можно создать приложение логики, как описано [здесь](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="ee98f-110">You can get started by creating a logic app now, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-the-connection-to-google-drive"></a><span data-ttu-id="ee98f-111">Создание подключения к Google-диску</span><span class="sxs-lookup"><span data-stu-id="ee98f-111">Create the connection to Google Drive</span></span>
<span data-ttu-id="ee98f-112">При добавлении соединителя в приложения логики эти приложения необходимо авторизовать для подключения к Google-диску.</span><span class="sxs-lookup"><span data-stu-id="ee98f-112">When you add this connector to your logic apps, you must authorize logic apps to connect to your Google Drive.</span></span>

> [!INCLUDE [Steps to create a connection to googledrive](../../includes/connectors-create-api-googledrive.md)]
> 
> 

<span data-ttu-id="ee98f-113">После создания подключения укажите свойства Google-диска, такие как путь к папке или имя файла.</span><span class="sxs-lookup"><span data-stu-id="ee98f-113">After you create the connection, you enter the Google Drive properties, like the folder path or file name.</span></span> 

## <a name="connector-specific-details"></a><span data-ttu-id="ee98f-114">Сведения о соединителях</span><span class="sxs-lookup"><span data-stu-id="ee98f-114">Connector-specific details</span></span>

<span data-ttu-id="ee98f-115">Информацию о существующих ограничениях, а также о триггерах и действиях, определенных в Swagger, см. в статье со [сведениями о соединителях](/connectors/googledrive/).</span><span class="sxs-lookup"><span data-stu-id="ee98f-115">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/googledrive/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="ee98f-116">Дополнительные сведения о соединителях</span><span class="sxs-lookup"><span data-stu-id="ee98f-116">More connectors</span></span>
<span data-ttu-id="ee98f-117">Вы можете вернуться к [списку интерфейсов API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="ee98f-117">Go back to the [APIs list](apis-list.md).</span></span>
