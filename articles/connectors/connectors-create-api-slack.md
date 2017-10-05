---
title: "Использование соединителя Slack в Azure Logic Apps | Документация Майкрософт"
description: "Из этой статьи вы узнаете, как в приложении логики подключиться к Slack."
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 234cad64-b13d-4494-ae78-18b17119ba24
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: fc5fc128efe01bd0727e3ff30d8938918e89ac3a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-slack-connector"></a><span data-ttu-id="16433-103">Начало работы с соединителем Slack</span><span class="sxs-lookup"><span data-stu-id="16433-103">Get started with the Slack connector</span></span>
<span data-ttu-id="16433-104">Slack — это средство для организации взаимодействия между группами пользователей, которое объединяет все сообщения в одном месте, поддерживает возможности мгновенного поиска и доступно в любом месте.</span><span class="sxs-lookup"><span data-stu-id="16433-104">Slack is a team communication tool, that brings together all of your team communications in one place, instantly searchable and available wherever you go.</span></span> 

<span data-ttu-id="16433-105">Для начала создайте приложение логики, как описано [здесь](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="16433-105">Get started by creating a logic app now; see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-to-slack"></a><span data-ttu-id="16433-106">Создание подключения к Slack</span><span class="sxs-lookup"><span data-stu-id="16433-106">Create a connection to Slack</span></span>
<span data-ttu-id="16433-107">Чтобы использовать соединитель Slack, сначала нужно создать **подключение** , а затем указать данные для приведенных ниже свойств.</span><span class="sxs-lookup"><span data-stu-id="16433-107">To use the Slack connector, you first create a **connection** then provide the details for these properties:</span></span> 

| <span data-ttu-id="16433-108">Свойство</span><span class="sxs-lookup"><span data-stu-id="16433-108">Property</span></span> | <span data-ttu-id="16433-109">Обязательно</span><span class="sxs-lookup"><span data-stu-id="16433-109">Required</span></span> | <span data-ttu-id="16433-110">Description (Описание)</span><span class="sxs-lookup"><span data-stu-id="16433-110">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="16433-111">Маркер</span><span class="sxs-lookup"><span data-stu-id="16433-111">Token</span></span> |<span data-ttu-id="16433-112">Да</span><span class="sxs-lookup"><span data-stu-id="16433-112">Yes</span></span> |<span data-ttu-id="16433-113">Указание учетных данных Slack</span><span class="sxs-lookup"><span data-stu-id="16433-113">Provide Slack Credentials</span></span> |

<span data-ttu-id="16433-114">Войдите в Slack и настройте в приложении логики **подключение** к Slack, выполнив следующие действия:</span><span class="sxs-lookup"><span data-stu-id="16433-114">Follow these steps to sign into Slack, and complete the configuration of the Slack **connection** in your logic app:</span></span>

1. <span data-ttu-id="16433-115">Выберите **Повторение**</span><span class="sxs-lookup"><span data-stu-id="16433-115">Select **Recurrence**</span></span>
2. <span data-ttu-id="16433-116">Выберите **частоту** и введите **интервал**.</span><span class="sxs-lookup"><span data-stu-id="16433-116">Select a **Frequency** and enter an **Interval**</span></span>
3. <span data-ttu-id="16433-117">Выберите **Добавить действие**.</span><span class="sxs-lookup"><span data-stu-id="16433-117">Select **Add an action**</span></span>  
   <span data-ttu-id="16433-118">![Настройка Slack][1]</span><span class="sxs-lookup"><span data-stu-id="16433-118">![Configure Slack][1]</span></span>  
4. <span data-ttu-id="16433-119">В поле поиска введите "Slack" и дождитесь возвращения всех записей с "Slack" в имени.</span><span class="sxs-lookup"><span data-stu-id="16433-119">Enter Slack in the search box and wait for the search to return all entries with Slack in the name</span></span>
5. <span data-ttu-id="16433-120">Выберите **Slack — опубликовать сообщение**</span><span class="sxs-lookup"><span data-stu-id="16433-120">Select **Slack - Post message**</span></span>
6. <span data-ttu-id="16433-121">Выберите **Вход в Slack**.</span><span class="sxs-lookup"><span data-stu-id="16433-121">Select **Sign in to Slack**:</span></span>  
   <span data-ttu-id="16433-122">![Настройка Slack][2]</span><span class="sxs-lookup"><span data-stu-id="16433-122">![Configure Slack][2]</span></span>
7. <span data-ttu-id="16433-123">Укажите учетные данные Slack, чтобы войти и авторизовать приложение.</span><span class="sxs-lookup"><span data-stu-id="16433-123">Provide your Slack credentials to sign in to authorize the  application</span></span>    
   ![Настройка Slack][3]  
8. <span data-ttu-id="16433-125">Вы будете перенаправлены на страницу входа своей организации.</span><span class="sxs-lookup"><span data-stu-id="16433-125">You'll be redirected to your organization's Log in page.</span></span> <span data-ttu-id="16433-126">**Разрешите** Slack взаимодействие с вашим приложением логики.</span><span class="sxs-lookup"><span data-stu-id="16433-126">**Authorize** Slack to interact with your logic app:</span></span>      
   <span data-ttu-id="16433-127">![Настройка Slack][5]</span><span class="sxs-lookup"><span data-stu-id="16433-127">![Configure Slack][5]</span></span> 
9. <span data-ttu-id="16433-128">После успешной аутентификации вы перейдете к своему приложению логики, чтобы завершить его, настроив параметры в разделе **Slack —получение всех сообщений** .</span><span class="sxs-lookup"><span data-stu-id="16433-128">After the authorization completes you'll be redirected to your logic app to complete it by configuring the **Slack - Get all messages** section.</span></span> <span data-ttu-id="16433-129">Добавьте другие необходимые вам триггеры и действия.</span><span class="sxs-lookup"><span data-stu-id="16433-129">Add other triggers and actions that you need.</span></span>  
   <span data-ttu-id="16433-130">![Настройка Slack][6]</span><span class="sxs-lookup"><span data-stu-id="16433-130">![Configure Slack][6]</span></span>
10. <span data-ttu-id="16433-131">Сохраните результаты работы, выбрав **Сохранить** в строке меню вверху.</span><span class="sxs-lookup"><span data-stu-id="16433-131">Save your work by selecting **Save** on the menu bar above.</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="16433-132">Сведения о соединителях</span><span class="sxs-lookup"><span data-stu-id="16433-132">Connector-specific details</span></span>

<span data-ttu-id="16433-133">Информацию о существующих ограничениях, а также о триггерах и действиях, определенных в Swagger, см. в статье со [сведениями о соединителях](/connectors/slack/).</span><span class="sxs-lookup"><span data-stu-id="16433-133">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/slack/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="16433-134">Дополнительные сведения о соединителях</span><span class="sxs-lookup"><span data-stu-id="16433-134">More connectors</span></span>
<span data-ttu-id="16433-135">Вы можете вернуться к [списку интерфейсов API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="16433-135">Go back to the [APIs list](apis-list.md).</span></span>

[1]: ./media/connectors-create-api-slack/connectionconfig1.png
[2]: ./media/connectors-create-api-slack/connectionconfig2.png 
[3]: ./media/connectors-create-api-slack/connectionconfig3.png
[4]: ./media/connectors-create-api-slack/connectionconfig4.png
[5]: ./media/connectors-create-api-slack/connectionconfig5.png
[6]: ./media/connectors-create-api-slack/connectionconfig6.png
