---
title: "aaaJoin tooyour личного устройства организации | Документы Microsoft"
description: "Объясняет, как пользователи могут регистрировать свои личные Windows 10 устройств tootheir корпоративной сети, а также шаги развертывания для сценария BYOD."
services: active-directory
documentationcenter: 
author: femila
manager: femila
editor: 
tags: azure-classic-portal
ms.assetid: 9f3d38f5-1cfd-43d4-97da-4fed1255a1ff
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: 979e2461dd9ad0438aa402a0a3223cc84c4c625c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="join-a-personal-device-tooyour-organization"></a><span data-ttu-id="9b7ef-103">Присоединиться к организации tooyour личного устройства</span><span class="sxs-lookup"><span data-stu-id="9b7ef-103">Join a personal device tooyour organization</span></span>
## <a name="toojoin-a-windows-10-device-tooyour-organization"></a><span data-ttu-id="9b7ef-104">Организация tooyour устройства toojoin Windows 10</span><span class="sxs-lookup"><span data-stu-id="9b7ef-104">toojoin a Windows 10 device tooyour organization</span></span>
1. <span data-ttu-id="9b7ef-105">Из hello **запустить** последовательно выберите пункты **параметры**.</span><span class="sxs-lookup"><span data-stu-id="9b7ef-105">From hello **Start** menu, select **Settings**.</span></span>
2. <span data-ttu-id="9b7ef-106">Выберите пункт **Учетные записи**, а затем нажмите кнопку **Ваша учетная запись**.</span><span class="sxs-lookup"><span data-stu-id="9b7ef-106">Select **Accounts**, and then click **Your account**.</span></span>
3. <span data-ttu-id="9b7ef-107">Выберите команду **Добавить рабочую или учебную учетную запись**и введите свою корпоративную учетную запись.</span><span class="sxs-lookup"><span data-stu-id="9b7ef-107">Click **Add Work or School account**, and then type in your organizational account.</span></span>
4. <span data-ttu-id="9b7ef-108">На приветствия на странице входа для вашей организации, введите имя пользователя и пароль и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="9b7ef-108">On hello sign-in page for your organization, enter your user name and password, and then click **OK**.</span></span>
5. <span data-ttu-id="9b7ef-109">Появится окно многофакторной проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="9b7ef-109">You will be prompted for a multi-factor authentication challenge.</span></span> <span data-ttu-id="9b7ef-110">(Этот запрос может настроить ИТ-администратор).</span><span class="sxs-lookup"><span data-stu-id="9b7ef-110">(This challenge is configurable by an IT administrator.)</span></span>
6. <span data-ttu-id="9b7ef-111">Azure Active Directory (Azure AD) проверяет, требует ли устройство hello регистрации управления мобильными устройствами.</span><span class="sxs-lookup"><span data-stu-id="9b7ef-111">Azure Active Directory (Azure AD) checks whether hello device requires mobile device management enrollment.</span></span>
7. <span data-ttu-id="9b7ef-112">Windows регистрирует hello устройства в каталоге организации hello в Azure AD и регистрирует в управление мобильными устройствами, если это необходимо.</span><span class="sxs-lookup"><span data-stu-id="9b7ef-112">Windows registers hello device in hello organization’s directory in Azure AD and enrolls it in mobile device management, if appropriate.</span></span>
8. <span data-ttu-id="9b7ef-113">Если управляемых пользователей Windows имеет toohello рабочего стола через hello автоматический вход.</span><span class="sxs-lookup"><span data-stu-id="9b7ef-113">If you are a managed user, Windows takes you toohello desktop through hello automatic sign-in.</span></span>
9. <span data-ttu-id="9b7ef-114">Если федеративные пользователи будут выполнены tooenter экрана tooa входа в Windows, учетные данные.</span><span class="sxs-lookup"><span data-stu-id="9b7ef-114">If you are a federated user, you will be taken tooa Windows sign-in screen tooenter your credentials.</span></span>

## <a name="additional-information"></a><span data-ttu-id="9b7ef-115">Дополнительная информация</span><span class="sxs-lookup"><span data-stu-id="9b7ef-115">Additional information</span></span>
* [<span data-ttu-id="9b7ef-116">Windows 10 для предприятия hello: способов toouse устройств для работы</span><span class="sxs-lookup"><span data-stu-id="9b7ef-116">Windows 10 for hello enterprise: Ways toouse devices for work</span></span>](active-directory-azureadjoin-windows10-devices-overview.md)
* [<span data-ttu-id="9b7ef-117">Расширение облака возможности tooWindows 10 устройствами с помощью присоединения Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9b7ef-117">Extending cloud capabilities tooWindows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-user-upgrade.md)
* [<span data-ttu-id="9b7ef-118">Проверка подлинности удостоверений без использования паролей с помощью службы Microsoft Passport</span><span class="sxs-lookup"><span data-stu-id="9b7ef-118">Authenticating identities without passwords through Microsoft Passport</span></span>](active-directory-azureadjoin-passport.md)
* [<span data-ttu-id="9b7ef-119">Сценарии использования для присоединения к Azure AD</span><span class="sxs-lookup"><span data-stu-id="9b7ef-119">Learn about usage scenarios for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [<span data-ttu-id="9b7ef-120">Подключитесь к домену устройства tooAzure AD для Windows 10</span><span class="sxs-lookup"><span data-stu-id="9b7ef-120">Connect domain-joined devices tooAzure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="9b7ef-121">Настройка присоединения к Azure AD</span><span class="sxs-lookup"><span data-stu-id="9b7ef-121">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)

