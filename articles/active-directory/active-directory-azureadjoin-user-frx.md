---
title: "aaaSet новые устройства в Azure AD во время установки | Документы Microsoft"
description: "В этом разделе объясняется, как пользователи могут настроить присоединение к Azure AD в процессе запуска при первом включении компьютера."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
tags: azure-classic-portal
ms.assetid: 06a149f7-4aa1-4fb9-a8ec-ac2633b031fb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: 6afce4be7f084f1956a6f9dbddaa8def0605956d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-new-device-with-azure-ad-during-setup"></a><span data-ttu-id="326db-103">Настройка нового устройства под управлением Windows 10 для работы с Azure AD</span><span class="sxs-lookup"><span data-stu-id="326db-103">Set up a new device with Azure AD during Setup</span></span>
<span data-ttu-id="326db-104">В Windows 10 пользователей можно соединить их устройства tooAzure Active Directory (Azure AD) в hello при первом запуске (FRX).</span><span class="sxs-lookup"><span data-stu-id="326db-104">In Windows 10, users can join their devices tooAzure Active Directory (Azure AD) in hello first-run experience (FRX).</span></span> <span data-ttu-id="326db-105">Это позволяет организациям toodistribute упакованной со сжатием устройств tootheir сотрудников или студентов или позволить им Выбор свои собственные устройства (CYOD).</span><span class="sxs-lookup"><span data-stu-id="326db-105">This allows organizations toodistribute shrink-wrapped devices tootheir employees or students, or let them choose their own devices (CYOD).</span></span>
<span data-ttu-id="326db-106">Если выпусков Windows 10 Профессиональная или Windows 10 Корпоративная установлено на устройстве, hello возникновение процесс установки toohello значения по умолчанию для устройств, принадлежащих компании.</span><span class="sxs-lookup"><span data-stu-id="326db-106">If either Windows 10 Professional or Windows 10 Enterprise editions is installed on a device, hello experience defaults toohello setup process for company-owned devices.</span></span>

## <a name="toojoin-a-device-tooazure-ad"></a><span data-ttu-id="326db-107">toojoin устройства tooAzure AD</span><span class="sxs-lookup"><span data-stu-id="326db-107">toojoin a device tooAzure AD</span></span>
1. <span data-ttu-id="326db-108">Если включить новое устройство и запустить процесс установки hello, вы увидите hello **Подготовка** сообщения.</span><span class="sxs-lookup"><span data-stu-id="326db-108">When you turn on your new device and start hello setup process, you should see hello  **Getting Ready** message.</span></span> <span data-ttu-id="326db-109">Выполните tooset приглашения hello вашего устройства.</span><span class="sxs-lookup"><span data-stu-id="326db-109">Follow hello prompts tooset up your device.</span></span>
2. <span data-ttu-id="326db-110">Для начала выберите свой регион и язык.</span><span class="sxs-lookup"><span data-stu-id="326db-110">Start by customizing your region and language.</span></span> <span data-ttu-id="326db-111">Затем примите условия лицензии программного обеспечения Microsoft hello.</span><span class="sxs-lookup"><span data-stu-id="326db-111">Then accept hello Microsoft Software License Terms.</span></span>
   <span data-ttu-id="326db-112">![Настройка для вашего региона](./media/active-directory-azureadjoin/active-directory-azureadjoin-customize-region.png)</span><span class="sxs-lookup"><span data-stu-id="326db-112">![Customize for your region](./media/active-directory-azureadjoin/active-directory-azureadjoin-customize-region.png)</span></span>
3. <span data-ttu-id="326db-113">Выберите сеть hello требуется toouse для подключения toohello Интернета.</span><span class="sxs-lookup"><span data-stu-id="326db-113">Select hello network you want toouse for connecting toohello Internet.</span></span>
4. <span data-ttu-id="326db-114">Укажите, является ли ваше устройство личным или корпоративным.</span><span class="sxs-lookup"><span data-stu-id="326db-114">Select whether you're using a personal device or a company-owned device.</span></span> <span data-ttu-id="326db-115">Если это принадлежащие компании, выберите **это устройство принадлежит организации toomy**.</span><span class="sxs-lookup"><span data-stu-id="326db-115">If it's company-owned, click **This device belongs toomy organization**.</span></span> <span data-ttu-id="326db-116">Это запускает процесс присоединения AD Azure hello.</span><span class="sxs-lookup"><span data-stu-id="326db-116">This starts hello Azure AD Join experience.</span></span> <span data-ttu-id="326db-117">В ОС Windows 10 Профессиональная экран будет выглядеть так:</span><span class="sxs-lookup"><span data-stu-id="326db-117">Following is a screen that you'll see if you're using Windows 10 Professional.</span></span>
   <span data-ttu-id="326db-118"><center>
   ![Владелец экрана ПК](./media/active-directory-azureadjoin/active-directory-azureadjoin-who-owns-pc.png)</span><span class="sxs-lookup"><span data-stu-id="326db-118"><center>
![Who owns this PC screen](./media/active-directory-azureadjoin/active-directory-azureadjoin-who-owns-pc.png)</span></span>
5. <span data-ttu-id="326db-119">Введите учетные данные hello, предоставленные tooyou вашей организацией.</span><span class="sxs-lookup"><span data-stu-id="326db-119">Enter hello credentials that were provided tooyou by your organization.</span></span>
   <span data-ttu-id="326db-120"><center>
   ![Экран входа](./media/active-directory-azureadjoin/active-directory-azureadjoin-sign-in.png)</span><span class="sxs-lookup"><span data-stu-id="326db-120"><center>
![Sign-in screen](./media/active-directory-azureadjoin/active-directory-azureadjoin-sign-in.png)</span></span>
6. <span data-ttu-id="326db-121">После ввода имени пользователя в Azure AD выполняется поиск соответствующего клиента.</span><span class="sxs-lookup"><span data-stu-id="326db-121">After you have entered your user name, a matching tenant is located in Azure AD.</span></span> <span data-ttu-id="326db-122">Если вы находитесь в федеративный домен, можно перенаправленный tooyour локального сервера службы маркеров безопасности (STS) — например, Active Directory службы федерации (AD FS).</span><span class="sxs-lookup"><span data-stu-id="326db-122">If you are in a federated domain, you will be redirected tooyour on-premises Secure Token Service (STS) server--for example, Active Directory Federation Services (AD FS).</span></span>
7. <span data-ttu-id="326db-123">Если вы являетесь пользователем в домене, не относящихся к федерации, введите свои учетные данные непосредственно в Azure AD размещенной страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="326db-123">If you are a user in a non-federated domain, enter your credentials directly on hello Azure AD-hosted page.</span></span> <span data-ttu-id="326db-124">Если была настроена фирменная символика, вы также увидите логотип компании и сопроводительный текст.</span><span class="sxs-lookup"><span data-stu-id="326db-124">If company branding was configured, you will also see your organization’s logo and support text.</span></span>
8. <span data-ttu-id="326db-125">Появится окно многофакторной проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="326db-125">You're prompted for a multi-factor authentication challenge.</span></span> <span data-ttu-id="326db-126">Его настраивает ИТ-администратор.</span><span class="sxs-lookup"><span data-stu-id="326db-126">This challenge is configurable by an IT administrator.</span></span>
9. <span data-ttu-id="326db-127">Azure AD проверит, требуется ли регистрация пользователя или устройства в рамках политики управления мобильными устройствами.</span><span class="sxs-lookup"><span data-stu-id="326db-127">Azure AD checks whether this user/device requires enrollment in mobile device management.</span></span>
10. <span data-ttu-id="326db-128">Windows регистрирует hello устройства в каталоге организации hello в Azure AD и регистрирует в управление мобильными устройствами, если это необходимо.</span><span class="sxs-lookup"><span data-stu-id="326db-128">Windows registers hello device in hello organization’s directory in Azure AD and enrolls it in mobile device management, if appropriate.</span></span>
11. <span data-ttu-id="326db-129">Если управляемых пользователей Windows имеет desktop toohello hello автоматического входа в процессе.</span><span class="sxs-lookup"><span data-stu-id="326db-129">If you are a managed user, Windows takes you toohello desktop through hello automatic sign-in process.</span></span>
12. <span data-ttu-id="326db-130">Если федеративные пользователи направляются toohello входа в Windows экране tooenter учетные данные.</span><span class="sxs-lookup"><span data-stu-id="326db-130">If you are a federated user, you are directed toohello Windows sign-in screen tooenter your credentials.</span></span>

> [!NOTE]
> <span data-ttu-id="326db-131">Присоединением к домену Windows Server Active Directory в локальной среде в hello Windows out-of-box experience не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="326db-131">Joining an on-premises Windows Server Active Directory domain in hello Windows out-of-box experience is not supported.</span></span> <span data-ttu-id="326db-132">Таким образом, если планируется toojoin tooa домен компьютера, следует выбрать ссылку hello **настроить Windows с учетной записью** вместо него.</span><span class="sxs-lookup"><span data-stu-id="326db-132">Therefore, if you plan toojoin a computer tooa domain, you should select hello link **Set up Windows with a local account** instead.</span></span> <span data-ttu-id="326db-133">Затем можно соединить hello домена из параметров hello на компьютере, как вы сделали перед.</span><span class="sxs-lookup"><span data-stu-id="326db-133">You can then join hello domain from hello settings on your computer as you’ve done before.</span></span>
> 
> 

## <a name="additional-information"></a><span data-ttu-id="326db-134">Дополнительная информация</span><span class="sxs-lookup"><span data-stu-id="326db-134">Additional information</span></span>
* [<span data-ttu-id="326db-135">Windows 10 для предприятия hello: способов toouse устройств для работы</span><span class="sxs-lookup"><span data-stu-id="326db-135">Windows 10 for hello enterprise: Ways toouse devices for work</span></span>](active-directory-azureadjoin-windows10-devices-overview.md)
* [<span data-ttu-id="326db-136">Расширение облака возможности tooWindows 10 устройствами с помощью присоединения Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="326db-136">Extending cloud capabilities tooWindows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-user-upgrade.md)
* [<span data-ttu-id="326db-137">Проверка подлинности удостоверений без использования паролей с помощью службы Microsoft Passport</span><span class="sxs-lookup"><span data-stu-id="326db-137">Authenticating identities without passwords through Microsoft Passport</span></span>](active-directory-azureadjoin-passport.md)
* [<span data-ttu-id="326db-138">Сценарии использования для присоединения к Azure AD</span><span class="sxs-lookup"><span data-stu-id="326db-138">Learn about usage scenarios for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [<span data-ttu-id="326db-139">Подключитесь к домену устройства tooAzure AD для Windows 10</span><span class="sxs-lookup"><span data-stu-id="326db-139">Connect domain-joined devices tooAzure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="326db-140">Настройка присоединения к Azure AD</span><span class="sxs-lookup"><span data-stu-id="326db-140">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)

