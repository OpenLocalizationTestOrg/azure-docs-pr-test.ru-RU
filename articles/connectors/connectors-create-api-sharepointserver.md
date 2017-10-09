---
title: "hello aaaUse SharePoint Server Connector в приложениях для логики | Документы Microsoft"
description: "Начало работы с использованием hello hello SharePoint Server Connector в свои приложения логики"
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 0238a060-d592-4719-b7a2-26064c437a1a
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 3b814f42611e4971ff5c94ae3b021829217911dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-sharepoint-connector"></a><span data-ttu-id="e3be5-103">Приступая к работе с SharePoint соединителя hello</span><span class="sxs-lookup"><span data-stu-id="e3be5-103">Get started with hello SharePoint connector</span></span>
<span data-ttu-id="e3be5-104">Hello соединителя SharePoint предоставляет способ toowork со списками на сайте SharePoint.</span><span class="sxs-lookup"><span data-stu-id="e3be5-104">hello SharePoint Connector provides an way toowork with Lists on SharePoint.</span></span>

<span data-ttu-id="e3be5-105">Для начала создайте приложение логики, как описано [здесь](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="e3be5-105">Get started by creating a logic app; see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-toosharepoint"></a><span data-ttu-id="e3be5-106">Создание tooSharePoint подключения</span><span class="sxs-lookup"><span data-stu-id="e3be5-106">Create a connection tooSharePoint</span></span>
<span data-ttu-id="e3be5-107">toouse Здравствуйте соединителя SharePoint, сначала создайте **подключения** затем укажите подробности hello для этих свойств:</span><span class="sxs-lookup"><span data-stu-id="e3be5-107">toouse hello SharePoint Connector , you first create a **connection** then provide hello details for these properties:</span></span> 

| <span data-ttu-id="e3be5-108">Свойство</span><span class="sxs-lookup"><span data-stu-id="e3be5-108">Property</span></span> | <span data-ttu-id="e3be5-109">Обязательно</span><span class="sxs-lookup"><span data-stu-id="e3be5-109">Required</span></span> | <span data-ttu-id="e3be5-110">Description (Описание)</span><span class="sxs-lookup"><span data-stu-id="e3be5-110">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e3be5-111">Маркер</span><span class="sxs-lookup"><span data-stu-id="e3be5-111">Token</span></span> |<span data-ttu-id="e3be5-112">Да</span><span class="sxs-lookup"><span data-stu-id="e3be5-112">Yes</span></span> |<span data-ttu-id="e3be5-113">Указание учетных данных SharePoint</span><span class="sxs-lookup"><span data-stu-id="e3be5-113">Provide SharePoint Credentials</span></span> |

<span data-ttu-id="e3be5-114">tooconnect слишком**SharePoint**, введите ваш tooSharePoint удостоверение (имя пользователя и пароль, учетные данные смарт-карт и т. д.).</span><span class="sxs-lookup"><span data-stu-id="e3be5-114">tooconnect too**SharePoint**, enter your identity (username and password, smart card credentials, etc.) tooSharePoint.</span></span> <span data-ttu-id="e3be5-115">Вы прошел проверку подлинности, откройте соединитель SharePoint toouse hello в логике приложения.</span><span class="sxs-lookup"><span data-stu-id="e3be5-115">Once you've been authenticated, you can proceed toouse hello SharePoint connector  in your logic app.</span></span> 

<span data-ttu-id="e3be5-116">В конструкторе hello логики приложения, выполните эти шаги toosign в SharePoint toocreate hello соединение **подключения** для использования в приложении логики:</span><span class="sxs-lookup"><span data-stu-id="e3be5-116">While on hello designer of your logic app, follow these steps toosign into SharePoint toocreate hello connection **connection** for use in your logic app:</span></span>

1. <span data-ttu-id="e3be5-117">Введите в поле поиска hello SharePoint и дождитесь tooreturn hello поиск всех записей с SharePoint, в имени hello:</span><span class="sxs-lookup"><span data-stu-id="e3be5-117">Enter SharePoint in hello search box and wait for hello search tooreturn all entries with SharePoint in hello name:</span></span>   
   ![Настройка SharePoint][1]  
2. <span data-ttu-id="e3be5-119">Выберите **SharePoint - When a file is created** (SharePoint — при создании файла).</span><span class="sxs-lookup"><span data-stu-id="e3be5-119">Select **SharePoint - When a file is created**</span></span>   
3. <span data-ttu-id="e3be5-120">Выберите **входа tooSharePoint**:</span><span class="sxs-lookup"><span data-stu-id="e3be5-120">Select **Sign in tooSharePoint**:</span></span>   
   <span data-ttu-id="e3be5-121">![Настройка SharePoint][2]</span><span class="sxs-lookup"><span data-stu-id="e3be5-121">![Configure SharePoint][2]</span></span>    
4. <span data-ttu-id="e3be5-122">Укажите ваш toosign учетные данные SharePoint в tooauthenticate с SharePoint</span><span class="sxs-lookup"><span data-stu-id="e3be5-122">Provide your SharePoint credentials toosign in tooauthenticate with SharePoint</span></span>   
   ![Настройка SharePoint][3]     
5. <span data-ttu-id="e3be5-124">После завершения проверки подлинности hello вы будете перенаправленный tooyour логику приложения toocomplete его путем настройки SharePoint **при создании файла** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="e3be5-124">After hello authentication completes you'll be redirected tooyour logic app toocomplete it by configuring SharePoint's **When a file is created** dialog.</span></span>          
   <span data-ttu-id="e3be5-125">![Настройка SharePoint][4]</span><span class="sxs-lookup"><span data-stu-id="e3be5-125">![Configure SharePoint][4]</span></span>  
6. <span data-ttu-id="e3be5-126">Затем можно добавить другие триггеры и действия, необходимые toocomplete логику приложения.</span><span class="sxs-lookup"><span data-stu-id="e3be5-126">You can then add other triggers and actions that you need toocomplete your logic app.</span></span>   
7. <span data-ttu-id="e3be5-127">Сохранить результаты работы, выбрав **Сохранить** hello меню выше.</span><span class="sxs-lookup"><span data-stu-id="e3be5-127">Save your work by selecting **Save** on hello menu bar above.</span></span>  

## <a name="connector-specific-details"></a><span data-ttu-id="e3be5-128">Сведения о соединителях</span><span class="sxs-lookup"><span data-stu-id="e3be5-128">Connector-specific details</span></span>

<span data-ttu-id="e3be5-129">Просмотреть все триггеры и действия, определенные в hello swagger и любые пределы в hello см. также [сведений о соединителе](/connectors/sharepoint/).</span><span class="sxs-lookup"><span data-stu-id="e3be5-129">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/sharepoint/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="e3be5-130">Дополнительные сведения о соединителях</span><span class="sxs-lookup"><span data-stu-id="e3be5-130">More connectors</span></span>
<span data-ttu-id="e3be5-131">Вернитесь к предыдущему окну toohello [API-интерфейсы списка](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="e3be5-131">Go back toohello [APIs list](apis-list.md).</span></span>

[1]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig1.png  
[2]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig2.png 
[3]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig3.png
[4]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig4.png
[5]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig5.png
