---
title: "Добавление соединителя Пользователи Office 365 в приложения логики | Документация Майкрософт"
description: "Обзор соединителя Office 365 Пользователи с параметрами интерфейса API REST"
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: b2146481-9105-4f56-b4c2-7ae340cb922f
ms.service: multiple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 08/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 330f733440932a769eb0fe6031cd0d947a820080
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-office-365-users-connector"></a><span data-ttu-id="c1bd7-103">Начало работы с соединителем Office 365 Пользователи</span><span class="sxs-lookup"><span data-stu-id="c1bd7-103">Get started with the Office 365 Users connector</span></span>
<span data-ttu-id="c1bd7-104">Подключившись к Office 365 Пользователи, вы сможете получать профили, искать пользователей и выполнять многие другие действия.</span><span class="sxs-lookup"><span data-stu-id="c1bd7-104">Connect to Office 365 Users to get profiles, search users, and more.</span></span> <span data-ttu-id="c1bd7-105">С помощью Office 365 Пользователи вы можете:</span><span class="sxs-lookup"><span data-stu-id="c1bd7-105">With Office 365 Users, you can:</span></span>

* <span data-ttu-id="c1bd7-106">формировать бизнес-процессы на основе данных, получаемых из Office 365 Пользователи;</span><span class="sxs-lookup"><span data-stu-id="c1bd7-106">Build your business flow based on the data you get from Office 365 Users.</span></span> 
* <span data-ttu-id="c1bd7-107">использовать действия для получения непосредственных подчиненных, профиля пользователя для менеджера и т. д.</span><span class="sxs-lookup"><span data-stu-id="c1bd7-107">Use actions that get direct reports, get a manager's user profile, and more.</span></span> <span data-ttu-id="c1bd7-108">Эти действия получают ответ и делают выходные данные доступными для использования другими действиями.</span><span class="sxs-lookup"><span data-stu-id="c1bd7-108">These actions get a response, and then make the output available for other actions.</span></span> <span data-ttu-id="c1bd7-109">Например, можно получить список непосредственных подчиненных того или иного лица и внести соответствующие изменения в базу данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="c1bd7-109">For example, get a person's direct reports, and then take this information and update a SQL Azure database.</span></span> 

<span data-ttu-id="c1bd7-110">Для начала можно создать приложение логики, как описано [здесь](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="c1bd7-110">You can get started by creating a logic app now, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-to-office-365-users"></a><span data-ttu-id="c1bd7-111">Создание подключения к Office 365 Пользователи</span><span class="sxs-lookup"><span data-stu-id="c1bd7-111">Create a connection to Office 365 Users</span></span>
<span data-ttu-id="c1bd7-112">При добавлении этого соединителя в приложения логики необходимо войти в учетную запись Office 365 Пользователи и разрешить приложениям логики подключаться к вашей учетной записи.</span><span class="sxs-lookup"><span data-stu-id="c1bd7-112">When you add this connector to your logic apps, you must sign-in to your Office 365 Users account and allow logic apps to connect to your account.</span></span>

> [!INCLUDE [Steps to create a connection to Office 365 Users](../../includes/connectors-create-api-office365users.md)]
> 
> 

<span data-ttu-id="c1bd7-113">После создания подключения укажите свойства Office 365 Пользователи, такие как идентификатор пользователя.</span><span class="sxs-lookup"><span data-stu-id="c1bd7-113">After you create the connection, you enter the Office 365 Users properties, like the user ID.</span></span> <span data-ttu-id="c1bd7-114">Эти свойства описаны далее в **справочнике по REST API** .</span><span class="sxs-lookup"><span data-stu-id="c1bd7-114">The **REST API reference** in this topic describes these properties.</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="c1bd7-115">Сведения о соединителях</span><span class="sxs-lookup"><span data-stu-id="c1bd7-115">Connector-specific details</span></span>

<span data-ttu-id="c1bd7-116">Информацию о существующих ограничениях, а также о триггерах и действиях, определенных в Swagger, см. в статье со [сведениями о соединителях](/connectors/officeusers/).</span><span class="sxs-lookup"><span data-stu-id="c1bd7-116">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/officeusers/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="c1bd7-117">Дополнительные сведения о соединителях</span><span class="sxs-lookup"><span data-stu-id="c1bd7-117">More connectors</span></span>
<span data-ttu-id="c1bd7-118">Вы можете вернуться к [списку интерфейсов API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="c1bd7-118">Go back to the [APIs list](apis-list.md).</span></span>