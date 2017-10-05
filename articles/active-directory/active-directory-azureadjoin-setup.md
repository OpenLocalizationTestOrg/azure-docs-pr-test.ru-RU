---
title: "Настройка присоединения Azure AD для ваших пользователей | Документация Майкрософт"
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
ms.openlocfilehash: c37adc2654f7e931fdda22627e4a6ece2789fd86
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="setting-up-azure-ad-join-in-your-organization"></a><span data-ttu-id="ba93a-103">Настройка присоединения к Azure AD в организации</span><span class="sxs-lookup"><span data-stu-id="ba93a-103">Setting up Azure AD Join in your organization</span></span>
<span data-ttu-id="ba93a-104">Прежде чем приступить к настройке присоединения к Azure Active Directory, необходимо синхронизировать локальный каталог пользователей с облаком или вручную создать управляемые учетные записи в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ba93a-104">Before you set up Azure Active Directory Join (Azure AD Join), you need to either sync up your on-premises directory of users to the cloud or manually create managed accounts in Azure AD.</span></span>

<span data-ttu-id="ba93a-105">Подробные инструкции по синхронизации локальных пользователей с Azure AD представлены в разделе [Интеграция локальных удостоверений с Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="ba93a-105">Detailed instructions for syncing your on-premises users to Azure AD is covered in [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>

<span data-ttu-id="ba93a-106">Сведения о том, как вручную создать пользователей и управлять ими в Azure AD, содержатся в статье [Управление пользователями в Azure AD](https://msdn.microsoft.com/library/azure/hh967609.aspx).</span><span class="sxs-lookup"><span data-stu-id="ba93a-106">To manually create and manage users in Azure AD, refer to [User management in Azure AD](https://msdn.microsoft.com/library/azure/hh967609.aspx).</span></span>

## <a name="set-up-device-registration"></a><span data-ttu-id="ba93a-107">Настройка регистрации устройств</span><span class="sxs-lookup"><span data-stu-id="ba93a-107">Set up device registration</span></span>
1. <span data-ttu-id="ba93a-108">Войдите на портал Azure с учетной записью администратора.</span><span class="sxs-lookup"><span data-stu-id="ba93a-108">Log on to the Azure portal as an administrator.</span></span>
2. <span data-ttu-id="ba93a-109">На панели слева выберите **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ba93a-109">On the left pane, select **Active Directory**.</span></span>
3. <span data-ttu-id="ba93a-110">На вкладке **Каталог** выберите требуемый каталог.</span><span class="sxs-lookup"><span data-stu-id="ba93a-110">On the **Directory** tab, select your directory.</span></span>
4. <span data-ttu-id="ba93a-111">Перейдите на вкладку **Настройка** .</span><span class="sxs-lookup"><span data-stu-id="ba93a-111">Select the **Configure** tab.</span></span>
5. <span data-ttu-id="ba93a-112">Откройте раздел **Устройства** .</span><span class="sxs-lookup"><span data-stu-id="ba93a-112">Go to the **Devices** section.</span></span>
6. <span data-ttu-id="ba93a-113">На вкладке **устройства** задайте указанные ниже настройки.</span><span class="sxs-lookup"><span data-stu-id="ba93a-113">On the **devices** tab, set the following:</span></span>  
   * <span data-ttu-id="ba93a-114">**Максимальное количество устройств на пользователя**: выберите максимальное количество устройств, которое пользователь может иметь в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ba93a-114">**MAXIMUM NUMBER OF DEVICES PER USER**: Select the maximum number of devices that a user can have in Azure AD.</span></span>  <span data-ttu-id="ba93a-115">По достижении этой квоты пользователь больше не сможет добавлять дополнительные устройства до тех пор, пока не будут удалены одно или несколько существующих устройств.</span><span class="sxs-lookup"><span data-stu-id="ba93a-115">If a user reaches this quota, they will not be able to add additional devices until one or more of their existing devices are removed.</span></span>
   * <span data-ttu-id="ba93a-116">**Чтобы присоединить устройства, требуется Multi-factor Auth**: укажите, следует ли пользователям предоставлять второй фактор проверки подлинности для присоединения устройства к Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ba93a-116">**REQUIRE MULTI-FACTOR AUTH TO JOIN DEVICES**: Set whether users are required to provide a second authentication factor to join their device to Azure AD.</span></span> <span data-ttu-id="ba93a-117">Дополнительные сведения о многофакторной идентификации в Azure см. в статье [Приступая к работе с Многофакторной идентификацией Azure в облаке](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="ba93a-117">For more information on Azure Multi-Factor Authentication, see [Getting started with Azure Multi-Factor Authentication in the cloud](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md).</span></span>
   * <span data-ttu-id="ba93a-118">**Пользователи, которые могут присоединять устройства к Azure AD**: выберите пользователей и группы, которым разрешено присоединять устройства к Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ba93a-118">**USERS MAY AZURE AD JOIN DEVICES**: Select the users and groups that are allowed to join devices to Azure AD.</span></span>
   * <span data-ttu-id="ba93a-119">**Дополнительные администраторы присоединенных к Azure AD устройств**: в Azure AD Premium или Enterprise Mobility Suite (EMS) можно выбрать, каким пользователям предоставляются права локального администратора на устройстве.</span><span class="sxs-lookup"><span data-stu-id="ba93a-119">**ADDITIONAL ADMINISTRATORS ON AZURE AD JOINED DEVICES**: With Azure AD Premium or the Enterprise Mobility Suite (EMS), you can choose which users are granted local administrator rights to the device.</span></span> <span data-ttu-id="ba93a-120">По умолчанию права локального администратора предоставляются глобальным администраторам и владельцам устройств.</span><span class="sxs-lookup"><span data-stu-id="ba93a-120">Global administrators and device owners are granted local administrator rights by default.</span></span>

<span data-ttu-id="ba93a-121"><center>![Настройка регистрации устройств](./media/active-directory-azureadjoin/active-directory-aadjoin-configure-devices.png) </center></span><span class="sxs-lookup"><span data-stu-id="ba93a-121"><center>![Set up device regisration](./media/active-directory-azureadjoin/active-directory-aadjoin-configure-devices.png) </center></span></span>

<span data-ttu-id="ba93a-122">После настройки подключения к Azure AD для пользователей они могут подключаться к Azure AD, используя свои корпоративные или личные устройства.</span><span class="sxs-lookup"><span data-stu-id="ba93a-122">After you set up Azure AD Join for your users, they can connect to Azure AD through their corporate or personal devices.</span></span>

<span data-ttu-id="ba93a-123">Ниже приведены три сценария предоставления пользователям возможности настроить присоединения к Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ba93a-123">Following are the three scenarios you can use to enable your users to set up Azure AD Join:</span></span>

* <span data-ttu-id="ba93a-124">Присоединение пользователями устройств, принадлежащих компании, напрямую к Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ba93a-124">Users join a company-owned device directly to Azure AD.</span></span>
* <span data-ttu-id="ba93a-125">Присоединение пользователями подключенных к домену устройств, принадлежащих компании, к локальной службе Active Directory и расширение устройства до Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ba93a-125">Users domain-join a company-owned device to the on-premises Active Directory and then extend the device to Azure AD.</span></span>
* <span data-ttu-id="ba93a-126">Добавление пользователями рабочих или учебных учетных записей Windows на личные устройства.</span><span class="sxs-lookup"><span data-stu-id="ba93a-126">Users add work or school accounts to Windows on a personal device</span></span>

## <a name="additional-information"></a><span data-ttu-id="ba93a-127">Дополнительная информация</span><span class="sxs-lookup"><span data-stu-id="ba93a-127">Additional information</span></span>
* [<span data-ttu-id="ba93a-128">Windows 10 для предприятия: использование устройств для работы</span><span class="sxs-lookup"><span data-stu-id="ba93a-128">Windows 10 for the enterprise: Ways to use devices for work</span></span>](active-directory-azureadjoin-windows10-devices-overview.md)
* [<span data-ttu-id="ba93a-129">Использование возможностей облачных служб на устройствах с Windows 10 с помощью присоединения к Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ba93a-129">Extending cloud capabilities to Windows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-user-upgrade.md)
* [<span data-ttu-id="ba93a-130">Сценарии использования для присоединения к Azure AD</span><span class="sxs-lookup"><span data-stu-id="ba93a-130">Learn about usage scenarios for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [<span data-ttu-id="ba93a-131">Подключение присоединенных к домену устройств к Azure AD для работы в Windows 10</span><span class="sxs-lookup"><span data-stu-id="ba93a-131">Connect domain-joined devices to Azure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="ba93a-132">Настройка присоединения к Azure AD</span><span class="sxs-lookup"><span data-stu-id="ba93a-132">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)

