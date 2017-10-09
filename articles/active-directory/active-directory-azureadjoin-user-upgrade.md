---
title: "aaaSet устройства Windows 10 с Azure AD из параметров | Документы Microsoft"
description: "Объясняет, как пользователи могут присоединять tooAzure AD через меню \"настройки\" hello."
services: active-directory
documentationcenter: 
author: femila
manager: swadhwa
editor: 
tags: azure-classic-portal
ms.assetid: b844e1d9-ad43-4e4a-a398-5c4a43bf2f5c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: d6485228338db571cc01f913c99fbba49e0bb74a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-windows-10-device-with-azure-ad-from-settings"></a><span data-ttu-id="3d11b-103">Настройка устройства с Windows 10 для работы с Azure AD с помощью меню «Параметры»</span><span class="sxs-lookup"><span data-stu-id="3d11b-103">Set up a Windows 10 device with Azure AD from Settings</span></span>
<span data-ttu-id="3d11b-104">Если вы уже использование Windows 7 или Windows 8 и этот компьютер или устройство было обновленного tooWindows 10, вы можете присоединиться к tooAzure Active Directory (Azure AD) через меню "настройки" hello.</span><span class="sxs-lookup"><span data-stu-id="3d11b-104">If you are already using Windows 7 or Windows 8, and your computer or device has been upgraded tooWindows 10, you can join tooAzure Active Directory (Azure AD) through hello Settings menu.</span></span>

## <a name="toojoin-tooazure-ad-from-hello-settings-menu"></a><span data-ttu-id="3d11b-105">tooAzure toojoin AD из меню параметров hello</span><span class="sxs-lookup"><span data-stu-id="3d11b-105">toojoin tooAzure AD from hello Settings menu</span></span>
1. <span data-ttu-id="3d11b-106">Из hello **запустить** меню, щелкните hello **параметры** чудо-кнопку.</span><span class="sxs-lookup"><span data-stu-id="3d11b-106">From hello **Start** menu, click hello **Settings** charm.</span></span>
2. <span data-ttu-id="3d11b-107">В разделе **Параметры** выберите **Система**->**About** (О системе)->**Присоединиться к Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="3d11b-107">From **Settings**, select     **System**->**About**->**Join Azure AD**.</span></span>
   
   <span data-ttu-id="3d11b-108"><center>
   ![Присоединение Azure AD из меню параметров hello](./media/active-directory-azureadjoin/active-directory-azureadjoin-settings.png)</center></span><span class="sxs-lookup"><span data-stu-id="3d11b-108"><center>
![Join Azure AD from hello Settings menu](./media/active-directory-azureadjoin/active-directory-azureadjoin-settings.png) </center></span></span>
3. <span data-ttu-id="3d11b-109">Нажмите кнопку **Продолжить** в окне сообщения hello-присоединения Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3d11b-109">Click **Continue** in hello Azure AD Join message window.</span></span>
   
   <span data-ttu-id="3d11b-110"><center>
   ![Окно сообщения о присоединении к Azure AD](./media/active-directory-azureadjoin/active-directory-azureadjoin-message.png) </center></span><span class="sxs-lookup"><span data-stu-id="3d11b-110"><center>
![Join Azure AD message window](./media/active-directory-azureadjoin/active-directory-azureadjoin-message.png) </center></span></span>
4. <span data-ttu-id="3d11b-111">Введите учетные данные для входа.</span><span class="sxs-lookup"><span data-stu-id="3d11b-111">Provide your sign-in credentials.</span></span> <span data-ttu-id="3d11b-112">Это входа в систему будет включать все hello шаги, необходимые toocomplete проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="3d11b-112">This sign-in experience will include all hello steps that are required toocomplete authentication.</span></span> <span data-ttu-id="3d11b-113">Если вы являетесь частью федеративного клиента, администратору будет предоставления возможностей федерации hello, размещенному в вашей организации.</span><span class="sxs-lookup"><span data-stu-id="3d11b-113">If you are part of a federated tenant, your administrator will provide you with hello federation experience that's hosted by your organization.</span></span>
   <span data-ttu-id="3d11b-114"><center>
   ![Ввод учетных данных для входа](./media/active-directory-azureadjoin/active-directory-azureadjoin-sign-in.png) </center></span><span class="sxs-lookup"><span data-stu-id="3d11b-114"><center>
![Provide sign-in credentials](./media/active-directory-azureadjoin/active-directory-azureadjoin-sign-in.png) </center></span></span>
5. <span data-ttu-id="3d11b-115">Если ваша организация настроил многофакторной проверки подлинности Azure для присоединения tooAzure AD, предоставляют hello второй фактор, прежде чем продолжить.</span><span class="sxs-lookup"><span data-stu-id="3d11b-115">If your organization has configured Azure Multi-Factor Authentication for joining tooAzure AD, provide hello second factor before proceeding.</span></span>
6. <span data-ttu-id="3d11b-116">Нажмите кнопку **Accept** на hello **разрешить этот toobe устройства управляемых** экрана.</span><span class="sxs-lookup"><span data-stu-id="3d11b-116">Click **Accept** on hello **Allow this device toobe managed** screen.</span></span>
7. <span data-ttu-id="3d11b-117">Должно появиться сообщение hello, «устройство теперь не присоединены к домену tooyour организации в Azure AD».</span><span class="sxs-lookup"><span data-stu-id="3d11b-117">You should see hello message "Your device is now joined tooyour organization in Azure AD".</span></span>

## <a name="additional-information"></a><span data-ttu-id="3d11b-118">Дополнительная информация</span><span class="sxs-lookup"><span data-stu-id="3d11b-118">Additional information</span></span>
* [<span data-ttu-id="3d11b-119">Сценарии использования для присоединения к Azure AD</span><span class="sxs-lookup"><span data-stu-id="3d11b-119">Learn about usage scenarios for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [<span data-ttu-id="3d11b-120">Подключитесь к домену устройства tooAzure AD для Windows 10</span><span class="sxs-lookup"><span data-stu-id="3d11b-120">Connect domain-joined devices tooAzure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="3d11b-121">Настройка присоединения к Azure AD</span><span class="sxs-lookup"><span data-stu-id="3d11b-121">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)
* [<span data-ttu-id="3d11b-122">Проверка подлинности удостоверений без использования паролей с помощью службы Microsoft Passport</span><span class="sxs-lookup"><span data-stu-id="3d11b-122">Authenticating identities without passwords through Microsoft Passport</span></span>](active-directory-azureadjoin-passport.md)

