---
title: "aaaSetting копирование присоединения Azure AD для пользователей | Документы Microsoft"
description: "В этой статье объясняется, как администраторы могут настроить присоединение к Azure AD для регистрации локальных каталогов и устройств."
services: active-directory
documentationcenter: 
author: femila
manager: swadhwa
editor: 
tags: azure-classic-portal
ms.assetid: bfc5d415-c918-4d8b-afee-b3f41cc28469
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: 60a5aeb11292cb6057ab1065c3ab77e5981d0cdb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="setting-up-azure-ad-join-in-your-organization"></a><span data-ttu-id="8dc91-103">Настройка присоединения к Azure AD в организации</span><span class="sxs-lookup"><span data-stu-id="8dc91-103">Setting up Azure AD Join in your organization</span></span>
<span data-ttu-id="8dc91-104">Перед настройкой присоединения Azure Active Directory (Azure AD соединения), вам требуется синхронизировать tooeither вверх вашего локального каталога пользователей toohello облака или вручную создать управляемых учетных записей в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8dc91-104">Before you set up Azure Active Directory Join (Azure AD Join), you need tooeither sync up your on-premises directory of users toohello cloud or manually create managed accounts in Azure AD.</span></span>

<span data-ttu-id="8dc91-105">Подробные инструкции для синхронизации вашей tooAzure пользователей в локальной среде AD рассматривается в [интеграция локальных удостоверений с Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="8dc91-105">Detailed instructions for syncing your on-premises users tooAzure AD is covered in [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>

<span data-ttu-id="8dc91-106">toomanually Создание и управление пользователями в Azure AD см. в слишком[Управление пользователями в Azure AD](https://msdn.microsoft.com/library/azure/hh967609.aspx).</span><span class="sxs-lookup"><span data-stu-id="8dc91-106">toomanually create and manage users in Azure AD, refer too[User management in Azure AD](https://msdn.microsoft.com/library/azure/hh967609.aspx).</span></span>

## <a name="set-up-device-registration"></a><span data-ttu-id="8dc91-107">Настройка регистрации устройств</span><span class="sxs-lookup"><span data-stu-id="8dc91-107">Set up device registration</span></span>
1. <span data-ttu-id="8dc91-108">Войдите на toohello портал Azure с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="8dc91-108">Log on toohello Azure portal as an administrator.</span></span>
2. <span data-ttu-id="8dc91-109">Выберите на левой панели hello **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8dc91-109">On hello left pane, select **Active Directory**.</span></span>
3. <span data-ttu-id="8dc91-110">На hello **каталога** вкладке, выберите свой каталог.</span><span class="sxs-lookup"><span data-stu-id="8dc91-110">On hello **Directory** tab, select your directory.</span></span>
4. <span data-ttu-id="8dc91-111">Выберите hello **Настройка** вкладки.</span><span class="sxs-lookup"><span data-stu-id="8dc91-111">Select hello **Configure** tab.</span></span>
5. <span data-ttu-id="8dc91-112">Go toohello **устройств** раздела.</span><span class="sxs-lookup"><span data-stu-id="8dc91-112">Go toohello **Devices** section.</span></span>
6. <span data-ttu-id="8dc91-113">На hello **устройств** установите hello следующее:</span><span class="sxs-lookup"><span data-stu-id="8dc91-113">On hello **devices** tab, set hello following:</span></span>  
   * <span data-ttu-id="8dc91-114">**МАКСИМАЛЬНОЕ число устройств на пользователя**: выберите hello максимальное число устройств, которые пользователь может располагать в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8dc91-114">**MAXIMUM NUMBER OF DEVICES PER USER**: Select hello maximum number of devices that a user can have in Azure AD.</span></span>  <span data-ttu-id="8dc91-115">Если пользователь достигает этой квоты, он не будет дополнительных устройств может tooadd только после удаления одного или нескольких существующих устройств из.</span><span class="sxs-lookup"><span data-stu-id="8dc91-115">If a user reaches this quota, they will not be able tooadd additional devices until one or more of their existing devices are removed.</span></span>
   * <span data-ttu-id="8dc91-116">**ТРЕБОВАНИЯ МНОГОФАКТОРНОЙ проверки Подлинности tooJOIN устройств**: пользователи могут быть обязательным tooprovide второй проверки подлинности коэффициент toojoin их устройства tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="8dc91-116">**REQUIRE MULTI-FACTOR AUTH tooJOIN DEVICES**: Set whether users are required tooprovide a second authentication factor toojoin their device tooAzure AD.</span></span> <span data-ttu-id="8dc91-117">Дополнительные сведения о многофакторной проверке подлинности Azure см. в разделе [Приступая к работе с многофакторной проверкой подлинности в Azure в облаке hello](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="8dc91-117">For more information on Azure Multi-Factor Authentication, see [Getting started with Azure Multi-Factor Authentication in hello cloud](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md).</span></span>
   * <span data-ttu-id="8dc91-118">**Пользователи могут устройств присоединения AZURE AD**: выберите hello пользователей и групп, которые допускаются tooAzure устройств toojoin AD.</span><span class="sxs-lookup"><span data-stu-id="8dc91-118">**USERS MAY AZURE AD JOIN DEVICES**: Select hello users and groups that are allowed toojoin devices tooAzure AD.</span></span>
   * <span data-ttu-id="8dc91-119">**Дополнительные АДМИНИСТРАТОРЫ ON AZURE AD к УСТРОЙСТВАМ, ПРИСОЕДИНЕННЫМ**: С Azure AD Premium или hello Enterprise Mobility Suite (EMS), можно выбрать пользователей, которым предоставляются права локального администратора toohello устройства.</span><span class="sxs-lookup"><span data-stu-id="8dc91-119">**ADDITIONAL ADMINISTRATORS ON AZURE AD JOINED DEVICES**: With Azure AD Premium or hello Enterprise Mobility Suite (EMS), you can choose which users are granted local administrator rights toohello device.</span></span> <span data-ttu-id="8dc91-120">По умолчанию права локального администратора предоставляются глобальным администраторам и владельцам устройств.</span><span class="sxs-lookup"><span data-stu-id="8dc91-120">Global administrators and device owners are granted local administrator rights by default.</span></span>

<span data-ttu-id="8dc91-121"><center>![Настройка регистрации устройств](./media/active-directory-azureadjoin/active-directory-aadjoin-configure-devices.png) </center></span><span class="sxs-lookup"><span data-stu-id="8dc91-121"><center>![Set up device regisration](./media/active-directory-azureadjoin/active-directory-aadjoin-configure-devices.png) </center></span></span>

<span data-ttu-id="8dc91-122">После настройки присоединения Azure AD для пользователей, они могут подключаться tooAzure AD через их корпоративных и личных устройств.</span><span class="sxs-lookup"><span data-stu-id="8dc91-122">After you set up Azure AD Join for your users, they can connect tooAzure AD through their corporate or personal devices.</span></span>

<span data-ttu-id="8dc91-123">Ниже приведены три сценария hello tooenable можно использовать ваш tooset пользователей копирование присоединения Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8dc91-123">Following are hello three scenarios you can use tooenable your users tooset up Azure AD Join:</span></span>

* <span data-ttu-id="8dc91-124">Пользователю о необходимости присоединиться устройства, принадлежащие компании непосредственно tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="8dc91-124">Users join a company-owned device directly tooAzure AD.</span></span>
* <span data-ttu-id="8dc91-125">Пользователей присоединения к домену принадлежащие компании устройства toohello локальной Active Directory и затем расширить tooAzure устройства hello AD.</span><span class="sxs-lookup"><span data-stu-id="8dc91-125">Users domain-join a company-owned device toohello on-premises Active Directory and then extend hello device tooAzure AD.</span></span>
* <span data-ttu-id="8dc91-126">Добавление пользователей работы или учебную учетные записи tooWindows на личных устройствах</span><span class="sxs-lookup"><span data-stu-id="8dc91-126">Users add work or school accounts tooWindows on a personal device</span></span>

## <a name="additional-information"></a><span data-ttu-id="8dc91-127">Дополнительная информация</span><span class="sxs-lookup"><span data-stu-id="8dc91-127">Additional information</span></span>
* [<span data-ttu-id="8dc91-128">Windows 10 для предприятия hello: способов toouse устройств для работы</span><span class="sxs-lookup"><span data-stu-id="8dc91-128">Windows 10 for hello enterprise: Ways toouse devices for work</span></span>](active-directory-azureadjoin-windows10-devices-overview.md)
* [<span data-ttu-id="8dc91-129">Расширение облака возможности tooWindows 10 устройствами с помощью присоединения Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8dc91-129">Extending cloud capabilities tooWindows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-user-upgrade.md)
* [<span data-ttu-id="8dc91-130">Сценарии использования для присоединения к Azure AD</span><span class="sxs-lookup"><span data-stu-id="8dc91-130">Learn about usage scenarios for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [<span data-ttu-id="8dc91-131">Подключитесь к домену устройства tooAzure AD для Windows 10</span><span class="sxs-lookup"><span data-stu-id="8dc91-131">Connect domain-joined devices tooAzure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="8dc91-132">Настройка присоединения к Azure AD</span><span class="sxs-lookup"><span data-stu-id="8dc91-132">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)

