---
title: "hello aaaUse соединитель Slack в свои приложения логики Azure | Документы Microsoft"
description: "Подключение tooSlack в свои приложения логики"
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
ms.openlocfilehash: 6599d7b69d2147425c9fab978c5d0f93e5605f19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-slack-connector"></a><span data-ttu-id="d9de8-103">Начало работы с соединителем резерв hello</span><span class="sxs-lookup"><span data-stu-id="d9de8-103">Get started with hello Slack connector</span></span>
<span data-ttu-id="d9de8-104">Slack — это средство для организации взаимодействия между группами пользователей, которое объединяет все сообщения в одном месте, поддерживает возможности мгновенного поиска и доступно в любом месте.</span><span class="sxs-lookup"><span data-stu-id="d9de8-104">Slack is a team communication tool, that brings together all of your team communications in one place, instantly searchable and available wherever you go.</span></span> 

<span data-ttu-id="d9de8-105">Для начала создайте приложение логики, как описано [здесь](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="d9de8-105">Get started by creating a logic app now; see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-tooslack"></a><span data-ttu-id="d9de8-106">Создание tooSlack подключения</span><span class="sxs-lookup"><span data-stu-id="d9de8-106">Create a connection tooSlack</span></span>
<span data-ttu-id="d9de8-107">Резерв соединителя toouse hello, сначала создать **подключения** затем укажите подробности hello для этих свойств:</span><span class="sxs-lookup"><span data-stu-id="d9de8-107">toouse hello Slack connector, you first create a **connection** then provide hello details for these properties:</span></span> 

| <span data-ttu-id="d9de8-108">Свойство</span><span class="sxs-lookup"><span data-stu-id="d9de8-108">Property</span></span> | <span data-ttu-id="d9de8-109">Обязательно</span><span class="sxs-lookup"><span data-stu-id="d9de8-109">Required</span></span> | <span data-ttu-id="d9de8-110">Description (Описание)</span><span class="sxs-lookup"><span data-stu-id="d9de8-110">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d9de8-111">Маркер</span><span class="sxs-lookup"><span data-stu-id="d9de8-111">Token</span></span> |<span data-ttu-id="d9de8-112">Да</span><span class="sxs-lookup"><span data-stu-id="d9de8-112">Yes</span></span> |<span data-ttu-id="d9de8-113">Указание учетных данных Slack</span><span class="sxs-lookup"><span data-stu-id="d9de8-113">Provide Slack Credentials</span></span> |

<span data-ttu-id="d9de8-114">Выполните эти действия toosign в Slack, а полный hello конфигурация hello Slack **подключения** в приложении логики:</span><span class="sxs-lookup"><span data-stu-id="d9de8-114">Follow these steps toosign into Slack, and complete hello configuration of hello Slack **connection** in your logic app:</span></span>

1. <span data-ttu-id="d9de8-115">Выберите **Повторение**</span><span class="sxs-lookup"><span data-stu-id="d9de8-115">Select **Recurrence**</span></span>
2. <span data-ttu-id="d9de8-116">Выберите **частоту** и введите **интервал**.</span><span class="sxs-lookup"><span data-stu-id="d9de8-116">Select a **Frequency** and enter an **Interval**</span></span>
3. <span data-ttu-id="d9de8-117">Выберите **Добавить действие**.</span><span class="sxs-lookup"><span data-stu-id="d9de8-117">Select **Add an action**</span></span>  
   <span data-ttu-id="d9de8-118">![Настройка Slack][1]</span><span class="sxs-lookup"><span data-stu-id="d9de8-118">![Configure Slack][1]</span></span>  
4. <span data-ttu-id="d9de8-119">Введите в поле поиска hello резерв и дождитесь hello поиска tooreturn все записи со Slack в имени hello</span><span class="sxs-lookup"><span data-stu-id="d9de8-119">Enter Slack in hello search box and wait for hello search tooreturn all entries with Slack in hello name</span></span>
5. <span data-ttu-id="d9de8-120">Выберите **Slack — опубликовать сообщение**</span><span class="sxs-lookup"><span data-stu-id="d9de8-120">Select **Slack - Post message**</span></span>
6. <span data-ttu-id="d9de8-121">Выберите **входа tooSlack**:</span><span class="sxs-lookup"><span data-stu-id="d9de8-121">Select **Sign in tooSlack**:</span></span>  
   <span data-ttu-id="d9de8-122">![Настройка Slack][2]</span><span class="sxs-lookup"><span data-stu-id="d9de8-122">![Configure Slack][2]</span></span>
7. <span data-ttu-id="d9de8-123">Укажите ваш toosign резерв учетные данные в приложении tooauthorize hello</span><span class="sxs-lookup"><span data-stu-id="d9de8-123">Provide your Slack credentials toosign in tooauthorize hello  application</span></span>    
   ![Настройка Slack][3]  
8. <span data-ttu-id="d9de8-125">Вы будете страница входа на перенаправленном tooyour организации.</span><span class="sxs-lookup"><span data-stu-id="d9de8-125">You'll be redirected tooyour organization's Log in page.</span></span> <span data-ttu-id="d9de8-126">**Авторизовать** резерв toointeract с логикой приложения:</span><span class="sxs-lookup"><span data-stu-id="d9de8-126">**Authorize** Slack toointeract with your logic app:</span></span>      
   <span data-ttu-id="d9de8-127">![Настройка Slack][5]</span><span class="sxs-lookup"><span data-stu-id="d9de8-127">![Configure Slack][5]</span></span> 
9. <span data-ttu-id="d9de8-128">После завершения авторизации hello вы будете перенаправленный tooyour логику приложения toocomplete его путем настройки hello **временных резервов - получение всех сообщений** раздела.</span><span class="sxs-lookup"><span data-stu-id="d9de8-128">After hello authorization completes you'll be redirected tooyour logic app toocomplete it by configuring hello **Slack - Get all messages** section.</span></span> <span data-ttu-id="d9de8-129">Добавьте другие необходимые вам триггеры и действия.</span><span class="sxs-lookup"><span data-stu-id="d9de8-129">Add other triggers and actions that you need.</span></span>  
   <span data-ttu-id="d9de8-130">![Настройка Slack][6]</span><span class="sxs-lookup"><span data-stu-id="d9de8-130">![Configure Slack][6]</span></span>
10. <span data-ttu-id="d9de8-131">Сохранить результаты работы, выбрав **Сохранить** hello меню выше.</span><span class="sxs-lookup"><span data-stu-id="d9de8-131">Save your work by selecting **Save** on hello menu bar above.</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="d9de8-132">Сведения о соединителях</span><span class="sxs-lookup"><span data-stu-id="d9de8-132">Connector-specific details</span></span>

<span data-ttu-id="d9de8-133">Просмотреть все триггеры и действия, определенные в hello swagger и любые пределы в hello см. также [сведений о соединителе](/connectors/slack/).</span><span class="sxs-lookup"><span data-stu-id="d9de8-133">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/slack/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="d9de8-134">Дополнительные сведения о соединителях</span><span class="sxs-lookup"><span data-stu-id="d9de8-134">More connectors</span></span>
<span data-ttu-id="d9de8-135">Вернитесь к предыдущему окну toohello [API-интерфейсы списка](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="d9de8-135">Go back toohello [APIs list](apis-list.md).</span></span>

[1]: ./media/connectors-create-api-slack/connectionconfig1.png
[2]: ./media/connectors-create-api-slack/connectionconfig2.png 
[3]: ./media/connectors-create-api-slack/connectionconfig3.png
[4]: ./media/connectors-create-api-slack/connectionconfig4.png
[5]: ./media/connectors-create-api-slack/connectionconfig5.png
[6]: ./media/connectors-create-api-slack/connectionconfig6.png
