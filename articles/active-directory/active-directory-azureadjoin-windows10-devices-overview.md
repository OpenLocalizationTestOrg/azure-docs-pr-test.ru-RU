---
title: "Windows 10 для предприятия hello: способов toouse устройств для работы | Документы Microsoft"
description: "Общие сведения о развертывании устройств Windows 10 для предприятий и как toointegrate с Azure Active Directory для hello Windows с облаком. Сравниваются различные способы hello устройства можно подготовить и использовать в организации через портал Azure hello."
keywords: "облако Windows, Windows в Azure Active Directory устройства Windows 10 в Azure, устройства Azure Windows"
services: active-directory
documentationcenter: 
author: femila
manager: femila
editor: 
tags: azure-classic-portal
ms.assetid: 2cb9ab6a-55b6-4658-b7f2-6e05ae015e1b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: 95b452bc5ba3937e16de769275a59c77cb821e23
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="windows-10-for-hello-enterprise-ways-toouse-devices-for-work"></a><span data-ttu-id="92dd1-105">Windows 10 для предприятия hello: способов toouse устройств для работы</span><span class="sxs-lookup"><span data-stu-id="92dd1-105">Windows 10 for hello enterprise: Ways toouse devices for work</span></span>
<span data-ttu-id="92dd1-106">Windows 10 предоставляет hello tooleverage возможности Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="92dd1-106">Windows 10 gives you hello ability tooleverage Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="92dd1-107">Можно подключить устройства Windows 10 tooAzure AD, чтобы пользователи могли войти в tooWindows с помощью учетных записей Azure AD, либо путем добавления их идентификаторы Azure toogain доступа toobusiness приложениям и ресурсам.</span><span class="sxs-lookup"><span data-stu-id="92dd1-107">You can connect Windows 10 devices tooAzure AD so that users can sign in tooWindows by using Azure AD accounts or by adding their Azure IDs toogain access toobusiness apps and resources.</span></span>

![Azure Active Directory с облаком Windows](./media/active-directory-azureadjoin/windows10-overview.png)

## <a name="integrating-windows-10-devices-with-azure-active-directory--a-content-map"></a><span data-ttu-id="92dd1-109">Интеграция устройств Windows 10 с Azure Active Directory: карта содержимого</span><span class="sxs-lookup"><span data-stu-id="92dd1-109">Integrating Windows 10 devices with Azure Active Directory--a content map</span></span>
<span data-ttu-id="92dd1-110">Hello следующие разделы предоставляют подробные сведения о различных возможностях устройств Windows 10 в вашей организации.</span><span class="sxs-lookup"><span data-stu-id="92dd1-110">hello following topics provide insights into different capabilities of Windows 10 devices in your organization.</span></span>

|  | <span data-ttu-id="92dd1-111">Разделы</span><span class="sxs-lookup"><span data-stu-id="92dd1-111">Topics</span></span> |
| --- | --- |
| <span data-ttu-id="92dd1-112">Приступая к работе</span><span class="sxs-lookup"><span data-stu-id="92dd1-112">Getting started</span></span> |[<span data-ttu-id="92dd1-113">Устройства под управлением Windows 10 в вашей рабочей области</span><span class="sxs-lookup"><span data-stu-id="92dd1-113">Using Windows 10 devices in your workplace</span></span>](active-directory-azureadjoin-windows10-devices.md) <br> <br> [<span data-ttu-id="92dd1-114">Расширение облака возможности tooWindows 10 устройствами с помощью присоединения Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="92dd1-114">Extending cloud capabilities tooWindows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-overview.md) <br> <br> [<span data-ttu-id="92dd1-115">Проверка подлинности удостоверений без использования паролей с помощью службы Microsoft Passport</span><span class="sxs-lookup"><span data-stu-id="92dd1-115">Authenticating identities without passwords through Microsoft Passport</span></span>](active-directory-azureadjoin-passport.md) |
| <span data-ttu-id="92dd1-116">Развертывание</span><span class="sxs-lookup"><span data-stu-id="92dd1-116">Deployment</span></span> |[<span data-ttu-id="92dd1-117">Сценарии использования и рекомендации по развертыванию для присоединения к Azure AD</span><span class="sxs-lookup"><span data-stu-id="92dd1-117">Usage scenarios and deployment considerations for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md) <br><br> [<span data-ttu-id="92dd1-118">Возникает подключении tooAzure устройств, присоединенных к домену AD, для Windows 10</span><span class="sxs-lookup"><span data-stu-id="92dd1-118">Connecting domain-joined devices tooAzure AD, for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)<br><br>[<span data-ttu-id="92dd1-119">Включение Microsoft Passport для работы в организации hello</span><span class="sxs-lookup"><span data-stu-id="92dd1-119">Enabling Microsoft Passport for work in hello organization</span></span>](active-directory-azureadjoin-passport-deployment.md)<br><br> [<span data-ttu-id="92dd1-120">Включение Enterprise State Roaming для Windows 10</span><span class="sxs-lookup"><span data-stu-id="92dd1-120">Enabling Enterprise State Roaming for Windows 10</span></span>](active-directory-windows-enterprise-state-roaming-overview.md)<br><br> |
| <span data-ttu-id="92dd1-121">Задачи пользователя</span><span class="sxs-lookup"><span data-stu-id="92dd1-121">User tasks</span></span> |[<span data-ttu-id="92dd1-122">Настройка нового устройства под управлением Windows 10 на работу с Azure AD</span><span class="sxs-lookup"><span data-stu-id="92dd1-122">Setting up a new Windows 10 device with Azure AD during setup</span></span>](active-directory-azureadjoin-user-frx.md) <br><br> [<span data-ttu-id="92dd1-123">Настройка устройства Windows 10 с Azure AD из меню параметров hello</span><span class="sxs-lookup"><span data-stu-id="92dd1-123">Setting up a Windows 10 device with Azure AD from hello settings menu</span></span>](active-directory-azureadjoin-user-upgrade.md) <br><br> [<span data-ttu-id="92dd1-124">Присоединение личных организации tooyour устройства Windows 10</span><span class="sxs-lookup"><span data-stu-id="92dd1-124">Joining a personal Windows 10 device tooyour organization</span></span>](active-directory-azureadjoin-personal-device.md) |

