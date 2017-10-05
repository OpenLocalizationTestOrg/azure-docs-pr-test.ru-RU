---
title: "Настройка устройства с Windows 10 для работы с Azure AD с помощью меню \"Параметры\" | Документация Майкрософт"
description: "Сведения о том, как пользователи могут присоединиться к Azure AD, используя меню \"Параметры\"."
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
ms.openlocfilehash: 5a3963f16b471ad1ca8681b22a1a027935400465
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-a-windows-10-device-with-azure-ad-from-settings"></a><span data-ttu-id="21055-103">Настройка устройства с Windows 10 для работы с Azure AD с помощью меню «Параметры»</span><span class="sxs-lookup"><span data-stu-id="21055-103">Set up a Windows 10 device with Azure AD from Settings</span></span>
<span data-ttu-id="21055-104">Если вы уже используете Windows 7 или Windows 8, и система на вашем компьютере или устройстве была обновлена до Windows 10, его можно присоединить к Azure Active Directory (Azure AD) через меню "Параметры".</span><span class="sxs-lookup"><span data-stu-id="21055-104">If you are already using Windows 7 or Windows 8, and your computer or device has been upgraded to Windows 10, you can join to Azure Active Directory (Azure AD) through the Settings menu.</span></span>

## <a name="to-join-to-azure-ad-from-the-settings-menu"></a><span data-ttu-id="21055-105">Присоединение к Azure AD с помощью меню "Параметры"</span><span class="sxs-lookup"><span data-stu-id="21055-105">To join to Azure AD from the Settings menu</span></span>
1. <span data-ttu-id="21055-106">В меню **Пуск** выберите пункт **Параметры**.</span><span class="sxs-lookup"><span data-stu-id="21055-106">From the **Start** menu, click the **Settings** charm.</span></span>
2. <span data-ttu-id="21055-107">В разделе **Параметры** выберите **Система**->**About** (О системе)->**Присоединиться к Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="21055-107">From **Settings**, select     **System**->**About**->**Join Azure AD**.</span></span>
   
   <span data-ttu-id="21055-108"><center>
   ![Присоединение к Azure AD с помощью меню "Параметры"](./media/active-directory-azureadjoin/active-directory-azureadjoin-settings.png) </center></span><span class="sxs-lookup"><span data-stu-id="21055-108"><center>
![Join Azure AD from the Settings menu](./media/active-directory-azureadjoin/active-directory-azureadjoin-settings.png) </center></span></span>
3. <span data-ttu-id="21055-109">В окне сообщения о присоединении к Azure AD нажмите кнопку **Продолжить** .</span><span class="sxs-lookup"><span data-stu-id="21055-109">Click **Continue** in the Azure AD Join message window.</span></span>
   
   <span data-ttu-id="21055-110"><center>
   ![Окно сообщения о присоединении к Azure AD](./media/active-directory-azureadjoin/active-directory-azureadjoin-message.png) </center></span><span class="sxs-lookup"><span data-stu-id="21055-110"><center>
![Join Azure AD message window](./media/active-directory-azureadjoin/active-directory-azureadjoin-message.png) </center></span></span>
4. <span data-ttu-id="21055-111">Введите учетные данные для входа.</span><span class="sxs-lookup"><span data-stu-id="21055-111">Provide your sign-in credentials.</span></span> <span data-ttu-id="21055-112">На этом этапе вы выполните все действия, необходимые для прохождения аутентификации.</span><span class="sxs-lookup"><span data-stu-id="21055-112">This sign-in experience will include all the steps that are required to complete authentication.</span></span> <span data-ttu-id="21055-113">Если вы входите в федеративный клиент, администратор вашей организации обеспечит возможность федеративного входа.</span><span class="sxs-lookup"><span data-stu-id="21055-113">If you are part of a federated tenant, your administrator will provide you with the federation experience that's hosted by your organization.</span></span>
   <span data-ttu-id="21055-114"><center>
   ![Ввод учетных данных для входа](./media/active-directory-azureadjoin/active-directory-azureadjoin-sign-in.png) </center></span><span class="sxs-lookup"><span data-stu-id="21055-114"><center>
![Provide sign-in credentials](./media/active-directory-azureadjoin/active-directory-azureadjoin-sign-in.png) </center></span></span>
5. <span data-ttu-id="21055-115">Если для присоединения к Azure AD в организации настроена Azure Multi-Factor Authentication, перед продолжением введите данные для второй части проверки.</span><span class="sxs-lookup"><span data-stu-id="21055-115">If your organization has configured Azure Multi-Factor Authentication for joining to Azure AD, provide the second factor before proceeding.</span></span>
6. <span data-ttu-id="21055-116">На экране с запросом **Allow this device to be managed** (Разрешить управление этим устройством?) нажмите кнопку **Принять**.</span><span class="sxs-lookup"><span data-stu-id="21055-116">Click **Accept** on the **Allow this device to be managed** screen.</span></span>
7. <span data-ttu-id="21055-117">Вы увидите сообщение "Теперь устройство присоединено к вашей организации в Azure AD".</span><span class="sxs-lookup"><span data-stu-id="21055-117">You should see the message "Your device is now joined to your organization in Azure AD".</span></span>

## <a name="additional-information"></a><span data-ttu-id="21055-118">Дополнительная информация</span><span class="sxs-lookup"><span data-stu-id="21055-118">Additional information</span></span>
* [<span data-ttu-id="21055-119">Сценарии использования для присоединения к Azure AD</span><span class="sxs-lookup"><span data-stu-id="21055-119">Learn about usage scenarios for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [<span data-ttu-id="21055-120">Подключение присоединенных к домену устройств к Azure AD для работы в Windows 10</span><span class="sxs-lookup"><span data-stu-id="21055-120">Connect domain-joined devices to Azure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="21055-121">Настройка присоединения к Azure AD</span><span class="sxs-lookup"><span data-stu-id="21055-121">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)
* [<span data-ttu-id="21055-122">Проверка подлинности удостоверений без использования паролей с помощью службы Microsoft Passport</span><span class="sxs-lookup"><span data-stu-id="21055-122">Authenticating identities without passwords through Microsoft Passport</span></span>](active-directory-azureadjoin-passport.md)

