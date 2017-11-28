---
title: "aaaAccess приложений прокси приложения Azure AD в командах | Документы Microsoft"
description: "Используйте локальное приложение, через групп Майкрософт tooaccess прокси приложения Azure AD."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 13c36e43ae6349df09272e308ad4f40451cbbeb9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="access-your-on-premises-applications-through-microsoft-teams"></a><span data-ttu-id="1b94a-103">Доступ к приложениям в локальной среде через Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="1b94a-103">Access your on-premises applications through Microsoft Teams</span></span>

<span data-ttu-id="1b94a-104">Прокси приложения с Azure Active Directory позволяет единого входа tooon локальные приложения независимо от того, где вы находитесь и групп Майкрософт упрощает процесс совместной работы в одном месте.</span><span class="sxs-lookup"><span data-stu-id="1b94a-104">Azure Active Directory Application Proxy gives you single sign-on tooon-premises applications no matter where you are, and Microsoft Teams streamlines your collaborative efforts in one place.</span></span> <span data-ttu-id="1b94a-105">Интеграция hello два вместе означает, что пользователи могут эффективно с коллегами в любой ситуации.</span><span class="sxs-lookup"><span data-stu-id="1b94a-105">Integrating hello two together means that your users can be productive with their teammates in any situation.</span></span> 

<span data-ttu-id="1b94a-106">Пользователи могут добавлять облачные приложения tootheir команды каналы [с помощью вкладок](https://support.office.com/article/Video-Using-Tabs-7350a03e-017a-4a00-a6ae-1c9fe8c497b3?ui=en-US&rs=en-US&ad=US), но что произойдет, если этот сайт SharePoint или средств планирования, то все они используют размещается локально?</span><span class="sxs-lookup"><span data-stu-id="1b94a-106">Your users can add cloud apps tootheir Teams channels [using tabs](https://support.office.com/article/Video-Using-Tabs-7350a03e-017a-4a00-a6ae-1c9fe8c497b3?ui=en-US&rs=en-US&ad=US), but what happens if that SharePoint site or planning tool they all use is hosted on-premises?</span></span> <span data-ttu-id="1b94a-107">Прокси приложения — решение hello.</span><span class="sxs-lookup"><span data-stu-id="1b94a-107">Application Proxy is hello solution.</span></span> <span data-ttu-id="1b94a-108">Они могут добавлять приложения hello опубликованных через прокси-сервер приложения tootheir каналы с использованием же внешние URL-адреса, всегда используют tooaccess приложений удаленно.</span><span class="sxs-lookup"><span data-stu-id="1b94a-108">They can add apps published through Application Proxy tootheir channels using hello same external URLs they always use tooaccess their apps remotely.</span></span> <span data-ttu-id="1b94a-109">И поскольку прокси-сервер приложения выполняет проверку подлинности через Azure Active Directory, hello, которое выполняется на одном один вход.</span><span class="sxs-lookup"><span data-stu-id="1b94a-109">And because Application Proxy authenticates through Azure Active Directory, hello same single sign-on experience carries through.</span></span>


## <a name="install-hello-application-proxy-connector-and-publish-your-app"></a><span data-ttu-id="1b94a-110">Установите соединитель прокси приложения hello и публикация приложения</span><span class="sxs-lookup"><span data-stu-id="1b94a-110">Install hello Application Proxy connector and publish your app</span></span>

<span data-ttu-id="1b94a-111">Если это еще не сделано, [настройки прокси-сервера приложений для вашего клиента и установить соединитель hello](active-directory-application-proxy-enable.md).</span><span class="sxs-lookup"><span data-stu-id="1b94a-111">If you haven't already, [configure Application Proxy for your tenant and install hello connector](active-directory-application-proxy-enable.md).</span></span> <span data-ttu-id="1b94a-112">Затем [опубликуйте свое локальное приложение](application-proxy-publish-azure-portal.md) для удаленного доступа.</span><span class="sxs-lookup"><span data-stu-id="1b94a-112">Then, [publish your on-premises application](application-proxy-publish-azure-portal.md) for remote access.</span></span> <span data-ttu-id="1b94a-113">Если вы публикуете приложение hello, запишите hello внешний URL-адрес, так как к конечным пользователям необходимы эти сведения при добавлении tooTeams приложения hello.</span><span class="sxs-lookup"><span data-stu-id="1b94a-113">When you're publishing hello app, make note of hello external URL because your end users need that information when they add hello app tooTeams.</span></span>

<span data-ttu-id="1b94a-114">Если уже имеется опубликованных приложений, но не помните их внешние URL-адреса, находить их в hello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1b94a-114">If you already have your apps published but don't remember their external URLs, look them up in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="1b94a-115">Вход, затем перейдите слишком**Azure Active Directory** > **корпоративных приложений** > **всех приложений** > Выбор приложения > **Прокси приложения**.</span><span class="sxs-lookup"><span data-stu-id="1b94a-115">Sign in, then navigate too**Azure Active Directory** > **Enterprise applications** > **All applications** > select your app > **Application proxy**.</span></span>

## <a name="add-your-app-tooteams"></a><span data-ttu-id="1b94a-116">Добавить tooTeams вашего приложения</span><span class="sxs-lookup"><span data-stu-id="1b94a-116">Add your app tooTeams</span></span>

<span data-ttu-id="1b94a-117">После публикации приложения hello через прокси-сервер приложения Проинформируйте пользователей о том, что их можно добавить непосредственно в связанные с командами каналы в виде вкладки.</span><span class="sxs-lookup"><span data-stu-id="1b94a-117">Once you publish hello app through Application Proxy, let your users know that they can add it as a tab directly in their Teams channels.</span></span> <span data-ttu-id="1b94a-118">Для этого им потребуется выполнить следующие три шага:</span><span class="sxs-lookup"><span data-stu-id="1b94a-118">Have them follow these three steps:</span></span>

1. <span data-ttu-id="1b94a-119">Перейдите toohello команды каналов место tooadd этого приложения и выберите  **+**  tooadd вкладки.</span><span class="sxs-lookup"><span data-stu-id="1b94a-119">Navigate toohello Teams channel where you want tooadd this app and select **+** tooadd a tab.</span></span>

   ![Выберите "Добавить вкладку"](./media/application-proxy-teams/add-tab.png)

2. <span data-ttu-id="1b94a-121">Выберите **веб-сайт** из параметры вкладки «hello».</span><span class="sxs-lookup"><span data-stu-id="1b94a-121">Select **Website** from hello tab options.</span></span>

   ![Добавление веб-сайта](./media/application-proxy-teams/website.png)

3. <span data-ttu-id="1b94a-123">Присвойте имя вкладке hello и задайте hello toohello прокси приложения внешний URL-АДРЕСЕ.</span><span class="sxs-lookup"><span data-stu-id="1b94a-123">Give hello tab a name and set hello URL toohello Application Proxy external URL.</span></span> 

   ![Настройка имени вкладки и URL-адреса](./media/application-proxy-teams/tab-name-url.png)

<span data-ttu-id="1b94a-125">Как только один член команды добавляет вкладку hello, оно отображается для всех пользователей в канале hello.</span><span class="sxs-lookup"><span data-stu-id="1b94a-125">Once one member of a team adds hello tab, it shows up for everyone in hello channel.</span></span> <span data-ttu-id="1b94a-126">Все пользователи, имеющие доступ toohello приложения получить единого входа с учетными данными hello, которые они используют для групп Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="1b94a-126">Any users who have access toohello app get single sign-on access with hello credentials they use for Microsoft Teams.</span></span> <span data-ttu-id="1b94a-127">Все пользователи, у которых нет доступа приложения toohello увидите вкладку hello в группах, но заблокированы, пока не предоставить им разрешения toohello локальных приложений и hello Azure портала опубликованной версии приложение hello.</span><span class="sxs-lookup"><span data-stu-id="1b94a-127">Any users who don't have access toohello app will see hello tab in Teams, but are blocked until you give them permissions toohello on-premises app and hello Azure portal published version of hello app.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="1b94a-128">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1b94a-128">Next steps</span></span>

- <span data-ttu-id="1b94a-129">Узнайте, каким образом слишком[публикации локальных сайтов SharePoint](application-proxy-enable-remote-access-sharepoint.md) с помощью прокси приложения.</span><span class="sxs-lookup"><span data-stu-id="1b94a-129">Learn how too[publish on-premises SharePoint sites](application-proxy-enable-remote-access-sharepoint.md) with Application Proxy.</span></span>
- <span data-ttu-id="1b94a-130">Настройка вашего приложения toouse [пользовательских доменов](active-directory-application-proxy-custom-domains.md) для их внешний URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="1b94a-130">Configure your apps toouse [custom domains](active-directory-application-proxy-custom-domains.md) for their external URL.</span></span> 
