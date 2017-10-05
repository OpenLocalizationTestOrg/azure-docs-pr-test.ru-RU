---
title: "Настройка нового устройства для работы с Azure AD во время настройки | Документация Майкрософт"
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
ms.openlocfilehash: 4367f453ef7c794653dfa9f305b137a168e0d207
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="set-up-a-new-device-with-azure-ad-during-setup"></a><span data-ttu-id="2033d-103">Настройка нового устройства под управлением Windows 10 для работы с Azure AD</span><span class="sxs-lookup"><span data-stu-id="2033d-103">Set up a new device with Azure AD during Setup</span></span>
<span data-ttu-id="2033d-104">Пользователи Windows 10 могут присоединить свои устройства к Azure Active Directory при первом запуске (FRX).</span><span class="sxs-lookup"><span data-stu-id="2033d-104">In Windows 10, users can join their devices to Azure Active Directory (Azure AD) in the first-run experience (FRX).</span></span> <span data-ttu-id="2033d-105">Это позволяет организациям предоставлять сотрудникам или студентам стандартные новые устройства или давать им возможность выбирать собственные (CYOD).</span><span class="sxs-lookup"><span data-stu-id="2033d-105">This allows organizations to distribute shrink-wrapped devices to their employees or students, or let them choose their own devices (CYOD).</span></span>
<span data-ttu-id="2033d-106">Если на устройстве установлена операционная система Windows 10 Профессиональная или Windows 10 Корпоративная, автоматически запускается процесс установки устройств, принадлежащих компании.</span><span class="sxs-lookup"><span data-stu-id="2033d-106">If either Windows 10 Professional or Windows 10 Enterprise editions is installed on a device, the experience defaults to the setup process for company-owned devices.</span></span>

## <a name="to-join-a-device-to-azure-ad"></a><span data-ttu-id="2033d-107">Присоединение устройства к Azure AD</span><span class="sxs-lookup"><span data-stu-id="2033d-107">To join a device to Azure AD</span></span>
1. <span data-ttu-id="2033d-108">При включении нового устройства и запуске установки появляется сообщение **Подготовка**.</span><span class="sxs-lookup"><span data-stu-id="2033d-108">When you turn on your new device and start the setup process, you should see the  **Getting Ready** message.</span></span> <span data-ttu-id="2033d-109">Настройте устройство согласно инструкциям на экране.</span><span class="sxs-lookup"><span data-stu-id="2033d-109">Follow the prompts to set up your device.</span></span>
2. <span data-ttu-id="2033d-110">Для начала выберите свой регион и язык.</span><span class="sxs-lookup"><span data-stu-id="2033d-110">Start by customizing your region and language.</span></span> <span data-ttu-id="2033d-111">Примите условия лицензионного соглашения об использовании программного обеспечения Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="2033d-111">Then accept the Microsoft Software License Terms.</span></span>
   <span data-ttu-id="2033d-112">![Настройка для вашего региона](./media/active-directory-azureadjoin/active-directory-azureadjoin-customize-region.png)</span><span class="sxs-lookup"><span data-stu-id="2033d-112">![Customize for your region](./media/active-directory-azureadjoin/active-directory-azureadjoin-customize-region.png)</span></span>
3. <span data-ttu-id="2033d-113">Выберите сеть для подключения к Интернету.</span><span class="sxs-lookup"><span data-stu-id="2033d-113">Select the network you want to use for connecting to the Internet.</span></span>
4. <span data-ttu-id="2033d-114">Укажите, является ли ваше устройство личным или корпоративным.</span><span class="sxs-lookup"><span data-stu-id="2033d-114">Select whether you're using a personal device or a company-owned device.</span></span> <span data-ttu-id="2033d-115">Если устройство корпоративное, щелкните **Это устройство принадлежит моей организации**.</span><span class="sxs-lookup"><span data-stu-id="2033d-115">If it's company-owned, click **This device belongs to my organization**.</span></span> <span data-ttu-id="2033d-116">После этого начнется процесс присоединения к Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2033d-116">This starts the Azure AD Join experience.</span></span> <span data-ttu-id="2033d-117">В ОС Windows 10 Профессиональная экран будет выглядеть так:</span><span class="sxs-lookup"><span data-stu-id="2033d-117">Following is a screen that you'll see if you're using Windows 10 Professional.</span></span>
   <span data-ttu-id="2033d-118"><center>
   ![Владелец экрана ПК](./media/active-directory-azureadjoin/active-directory-azureadjoin-who-owns-pc.png)</span><span class="sxs-lookup"><span data-stu-id="2033d-118"><center>
![Who owns this PC screen](./media/active-directory-azureadjoin/active-directory-azureadjoin-who-owns-pc.png)</span></span>
5. <span data-ttu-id="2033d-119">Введите учетные данные, предоставленные вашей организацией.</span><span class="sxs-lookup"><span data-stu-id="2033d-119">Enter the credentials that were provided to you by your organization.</span></span>
   <span data-ttu-id="2033d-120"><center>
   ![Экран входа](./media/active-directory-azureadjoin/active-directory-azureadjoin-sign-in.png)</span><span class="sxs-lookup"><span data-stu-id="2033d-120"><center>
![Sign-in screen](./media/active-directory-azureadjoin/active-directory-azureadjoin-sign-in.png)</span></span>
6. <span data-ttu-id="2033d-121">После ввода имени пользователя в Azure AD выполняется поиск соответствующего клиента.</span><span class="sxs-lookup"><span data-stu-id="2033d-121">After you have entered your user name, a matching tenant is located in Azure AD.</span></span> <span data-ttu-id="2033d-122">Если вы находитесь в федеративном домене, то будете перенаправлены на локальный сервер службы токенов безопасности, например в службы федерации Active Directory (AD FS).</span><span class="sxs-lookup"><span data-stu-id="2033d-122">If you are in a federated domain, you will be redirected to your on-premises Secure Token Service (STS) server--for example, Active Directory Federation Services (AD FS).</span></span>
7. <span data-ttu-id="2033d-123">В доменах, отличных от федеративных, необходимо ввести учетные данные непосредственно на размещенной в Azure AD странице.</span><span class="sxs-lookup"><span data-stu-id="2033d-123">If you are a user in a non-federated domain, enter your credentials directly on the Azure AD-hosted page.</span></span> <span data-ttu-id="2033d-124">Если была настроена фирменная символика, вы также увидите логотип компании и сопроводительный текст.</span><span class="sxs-lookup"><span data-stu-id="2033d-124">If company branding was configured, you will also see your organization’s logo and support text.</span></span>
8. <span data-ttu-id="2033d-125">Появится окно многофакторной проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="2033d-125">You're prompted for a multi-factor authentication challenge.</span></span> <span data-ttu-id="2033d-126">Его настраивает ИТ-администратор.</span><span class="sxs-lookup"><span data-stu-id="2033d-126">This challenge is configurable by an IT administrator.</span></span>
9. <span data-ttu-id="2033d-127">Azure AD проверит, требуется ли регистрация пользователя или устройства в рамках политики управления мобильными устройствами.</span><span class="sxs-lookup"><span data-stu-id="2033d-127">Azure AD checks whether this user/device requires enrollment in mobile device management.</span></span>
10. <span data-ttu-id="2033d-128">Windows регистрирует устройство в каталоге организации в Azure AD и в службе управления мобильными устройствами, если это уместно.</span><span class="sxs-lookup"><span data-stu-id="2033d-128">Windows registers the device in the organization’s directory in Azure AD and enrolls it in mobile device management, if appropriate.</span></span>
11. <span data-ttu-id="2033d-129">Если вы являетесь управляемым пользователем, Windows осуществляет переход на рабочий стол с помощью автоматического входа.</span><span class="sxs-lookup"><span data-stu-id="2033d-129">If you are a managed user, Windows takes you to the desktop through the automatic sign-in process.</span></span>
12. <span data-ttu-id="2033d-130">Если вы являетесь федеративным пользователем, то появится экран входа в Windows, где нужно будет ввести учетные данные.</span><span class="sxs-lookup"><span data-stu-id="2033d-130">If you are a federated user, you are directed to the Windows sign-in screen to enter your credentials.</span></span>

> [!NOTE]
> <span data-ttu-id="2033d-131">Присоединение к локальному домену Active Directory Windows Server при первом запуске Windows не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="2033d-131">Joining an on-premises Windows Server Active Directory domain in the Windows out-of-box experience is not supported.</span></span> <span data-ttu-id="2033d-132">Если вы планируете присоединить компьютер к домену, перейдите по ссылке **Настроить Windows с локальной учетной записью** .</span><span class="sxs-lookup"><span data-stu-id="2033d-132">Therefore, if you plan to join a computer to a domain, you should select the link **Set up Windows with a local account** instead.</span></span> <span data-ttu-id="2033d-133">Затем вы сможете присоединиться к домену из меню параметров компьютера, как это делали раньше.</span><span class="sxs-lookup"><span data-stu-id="2033d-133">You can then join the domain from the settings on your computer as you’ve done before.</span></span>
> 
> 

## <a name="additional-information"></a><span data-ttu-id="2033d-134">Дополнительная информация</span><span class="sxs-lookup"><span data-stu-id="2033d-134">Additional information</span></span>
* [<span data-ttu-id="2033d-135">Windows 10 для предприятия: использование устройств для работы</span><span class="sxs-lookup"><span data-stu-id="2033d-135">Windows 10 for the enterprise: Ways to use devices for work</span></span>](active-directory-azureadjoin-windows10-devices-overview.md)
* [<span data-ttu-id="2033d-136">Использование возможностей облачных служб на устройствах с Windows 10 с помощью присоединения к Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2033d-136">Extending cloud capabilities to Windows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-user-upgrade.md)
* [<span data-ttu-id="2033d-137">Проверка подлинности удостоверений без использования паролей с помощью службы Microsoft Passport</span><span class="sxs-lookup"><span data-stu-id="2033d-137">Authenticating identities without passwords through Microsoft Passport</span></span>](active-directory-azureadjoin-passport.md)
* [<span data-ttu-id="2033d-138">Сценарии использования для присоединения к Azure AD</span><span class="sxs-lookup"><span data-stu-id="2033d-138">Learn about usage scenarios for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [<span data-ttu-id="2033d-139">Подключение присоединенных к домену устройств к Azure AD для работы в Windows 10</span><span class="sxs-lookup"><span data-stu-id="2033d-139">Connect domain-joined devices to Azure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="2033d-140">Настройка присоединения к Azure AD</span><span class="sxs-lookup"><span data-stu-id="2033d-140">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)

