---
title: "Использование соединителя SharePoint Server в приложениях логики | Документация Майкрософт"
description: "Как приступить к использованию соединителя SharePoint Server в приложениях логики."
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
ms.openlocfilehash: 0f3274816e279a1aa57febaa2f8294914900799a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-sharepoint-connector"></a><span data-ttu-id="6f347-103">Приступая к работе с соединителем SharePoint</span><span class="sxs-lookup"><span data-stu-id="6f347-103">Get started with the SharePoint connector</span></span>
<span data-ttu-id="6f347-104">Подключение SharePoint позволяет работать со списками в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="6f347-104">The SharePoint Connector provides an way to work with Lists on SharePoint.</span></span>

<span data-ttu-id="6f347-105">Для начала создайте приложение логики, как описано [здесь](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="6f347-105">Get started by creating a logic app; see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-to-sharepoint"></a><span data-ttu-id="6f347-106">Создание подключения к SharePoint</span><span class="sxs-lookup"><span data-stu-id="6f347-106">Create a connection to SharePoint</span></span>
<span data-ttu-id="6f347-107">Чтобы использовать соединитель SharePoint, сначала нужно создать **подключение** , а затем указать данные для следующих свойств:</span><span class="sxs-lookup"><span data-stu-id="6f347-107">To use the SharePoint Connector , you first create a **connection** then provide the details for these properties:</span></span> 

| <span data-ttu-id="6f347-108">Свойство</span><span class="sxs-lookup"><span data-stu-id="6f347-108">Property</span></span> | <span data-ttu-id="6f347-109">Обязательно</span><span class="sxs-lookup"><span data-stu-id="6f347-109">Required</span></span> | <span data-ttu-id="6f347-110">Description (Описание)</span><span class="sxs-lookup"><span data-stu-id="6f347-110">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6f347-111">Маркер</span><span class="sxs-lookup"><span data-stu-id="6f347-111">Token</span></span> |<span data-ttu-id="6f347-112">Да</span><span class="sxs-lookup"><span data-stu-id="6f347-112">Yes</span></span> |<span data-ttu-id="6f347-113">Указание учетных данных SharePoint</span><span class="sxs-lookup"><span data-stu-id="6f347-113">Provide SharePoint Credentials</span></span> |

<span data-ttu-id="6f347-114">Для подключения к **SharePoint** необходимо предоставить свое удостоверение (имя пользователя и пароль, учетные данные смарт-карты и т. п.).</span><span class="sxs-lookup"><span data-stu-id="6f347-114">To connect to **SharePoint**, enter your identity (username and password, smart card credentials, etc.) to SharePoint.</span></span> <span data-ttu-id="6f347-115">После прохождения проверки подлинности вы сможете использовать соединитель SharePoint в приложении логики.</span><span class="sxs-lookup"><span data-stu-id="6f347-115">Once you've been authenticated, you can proceed to use the SharePoint connector  in your logic app.</span></span> 

<span data-ttu-id="6f347-116">В конструкторе приложения логики выполните следующие действия, чтобы войти в SharePoint для создания подключения **connection** , которое будет использоваться в приложении логики.</span><span class="sxs-lookup"><span data-stu-id="6f347-116">While on the designer of your logic app, follow these steps to sign into SharePoint to create the connection **connection** for use in your logic app:</span></span>

1. <span data-ttu-id="6f347-117">В поле поиска введите SharePoint и дождитесь возвращения всех записей с текстом SharePoint в имени.</span><span class="sxs-lookup"><span data-stu-id="6f347-117">Enter SharePoint in the search box and wait for the search to return all entries with SharePoint in the name:</span></span>   
   ![Настройка SharePoint][1]  
2. <span data-ttu-id="6f347-119">Выберите **SharePoint - When a file is created** (SharePoint — при создании файла).</span><span class="sxs-lookup"><span data-stu-id="6f347-119">Select **SharePoint - When a file is created**</span></span>   
3. <span data-ttu-id="6f347-120">Выберите **Sign in to SharePoint** (Вход в SharePoint).</span><span class="sxs-lookup"><span data-stu-id="6f347-120">Select **Sign in to SharePoint**:</span></span>   
   <span data-ttu-id="6f347-121">![Настройка SharePoint][2]</span><span class="sxs-lookup"><span data-stu-id="6f347-121">![Configure SharePoint][2]</span></span>    
4. <span data-ttu-id="6f347-122">Укажите учетные данные SharePoint, чтобы войти и пройти аутентификацию в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="6f347-122">Provide your SharePoint credentials to sign in to authenticate with SharePoint</span></span>   
   ![Настройка SharePoint][3]     
5. <span data-ttu-id="6f347-124">После успешной аутентификации вы перейдете к своему приложению логики, чтобы завершить его, настроив параметры в диалоговом окне **При создании файла** SharePoint.</span><span class="sxs-lookup"><span data-stu-id="6f347-124">After the authentication completes you'll be redirected to your logic app to complete it by configuring SharePoint's **When a file is created** dialog.</span></span>          
   <span data-ttu-id="6f347-125">![Настройка SharePoint][4]</span><span class="sxs-lookup"><span data-stu-id="6f347-125">![Configure SharePoint][4]</span></span>  
6. <span data-ttu-id="6f347-126">Затем можно будет добавить другие триггеры и действия, необходимые для завершения приложения логики.</span><span class="sxs-lookup"><span data-stu-id="6f347-126">You can then add other triggers and actions that you need to complete your logic app.</span></span>   
7. <span data-ttu-id="6f347-127">Сохраните результаты работы, выбрав **Сохранить** в строке меню вверху.</span><span class="sxs-lookup"><span data-stu-id="6f347-127">Save your work by selecting **Save** on the menu bar above.</span></span>  

## <a name="connector-specific-details"></a><span data-ttu-id="6f347-128">Сведения о соединителях</span><span class="sxs-lookup"><span data-stu-id="6f347-128">Connector-specific details</span></span>

<span data-ttu-id="6f347-129">Информацию о существующих ограничениях, а также о триггерах и действиях, определенных в Swagger, см. в статье со [сведениями о соединителях](/connectors/sharepoint/).</span><span class="sxs-lookup"><span data-stu-id="6f347-129">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/sharepoint/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="6f347-130">Дополнительные сведения о соединителях</span><span class="sxs-lookup"><span data-stu-id="6f347-130">More connectors</span></span>
<span data-ttu-id="6f347-131">Вы можете вернуться к [списку интерфейсов API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="6f347-131">Go back to the [APIs list](apis-list.md).</span></span>

[1]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig1.png  
[2]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig2.png 
[3]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig3.png
[4]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig4.png
[5]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig5.png
