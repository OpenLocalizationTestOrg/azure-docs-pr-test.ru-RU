---
title: "aaaHow tooconfigure автоматической регистрации присоединенных к домену устройств Windows в Azure Active Directory | Документы Microsoft"
description: "Настройку вашей tooregister присоединенных к домену устройств Windows автоматически и без предупреждений с помощью Azure Active Directory."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 54e1b01b-03ee-4c46-bcf0-e01affc0419d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 1d736eba734418231f12e23a8fc1a93405f129c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-active-directory-device-registration"></a><span data-ttu-id="1db3a-103">Знакомство с регистрацией устройств в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1db3a-103">Get started with Azure Active Directory device registration</span></span>

<span data-ttu-id="1db3a-104">Регистрация устройств Azure Active Directory — hello основа для сценариев условного доступа на основе устройств.</span><span class="sxs-lookup"><span data-stu-id="1db3a-104">Azure Active Directory device registration is hello foundation for device-based conditional access scenarios.</span></span> <span data-ttu-id="1db3a-105">При регистрации устройства регистрации устройств Azure Active Directory предоставляет устройства hello удостоверение, которое является используется tooauthenticate hello устройства при входе пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="1db3a-105">When a device is registered, Azure Active Directory device registration provides hello device with an identity which is used tooauthenticate hello device when hello user signs in.</span></span> <span data-ttu-id="1db3a-106">Hello проверку подлинности устройства и атрибуты hello hello устройства, затем можно используется tooenforce политик условного доступа для приложений, размещенных в облаке hello и в локальной среде.</span><span class="sxs-lookup"><span data-stu-id="1db3a-106">hello authenticated device, and hello attributes of hello device, can then be used tooenforce conditional access policies for applications that are hosted in hello cloud and on-premises.</span></span>

<span data-ttu-id="1db3a-107">В сочетании с мобильными устройствами management(MDM) например Microsoft Intune, атрибуты устройства hello в Azure Active Directory обновляются с дополнительными сведениями об устройстве hello.</span><span class="sxs-lookup"><span data-stu-id="1db3a-107">When combined with a mobile device management(MDM) solution such as Microsoft Intune, hello device attributes in Azure Active Directory are updated with additional information about hello device.</span></span> <span data-ttu-id="1db3a-108">Это позволяет вам toocreate правила условного доступа, которые осуществляют доступ к устройствам toomeet стандартов безопасности и соответствия требованиям.</span><span class="sxs-lookup"><span data-stu-id="1db3a-108">This allows you toocreate conditional access rules that enforce access from devices toomeet your standards for security and compliance.</span></span> <span data-ttu-id="1db3a-109">Дополнительные сведения о регистрации устройств в Microsoft Intune см. в статье "Регистрация устройств для управления в Intune".</span><span class="sxs-lookup"><span data-stu-id="1db3a-109">For more information on enrolling devices in Microsoft Intune, see Enroll devices for management in Intune.</span></span>
<span data-ttu-id="1db3a-110">Сценарии, обеспечиваемые службой регистрации устройств Azure Active Directory. Регистрация устройств в Azure Active Directory предусматривает поддержку устройств Windows, iOS и Android.</span><span class="sxs-lookup"><span data-stu-id="1db3a-110">Scenarios enabled by Azure Active Directory Device Registration Azure Active Directory Device Registration includes support for iOS, Android, and Windows devices.</span></span> <span data-ttu-id="1db3a-111">Hello отдельных сценариях использования службы регистрации устройств Azure может иметь особые требования и поддерживаться другие платформы.</span><span class="sxs-lookup"><span data-stu-id="1db3a-111">hello individual scenarios that utilize Azure AD Device Registration may have more specific requirements and platform support.</span></span> 

<span data-ttu-id="1db3a-112">Эти сценарии выглядят так.</span><span class="sxs-lookup"><span data-stu-id="1db3a-112">These scenarios are as follows:</span></span>

- <span data-ttu-id="1db3a-113">**Условный доступ для приложений Office 365 с помощью Microsoft Intune:** ИТ-администраторы могут создавать условного доступа устройств политики toosecure корпоративным ресурсам, пока в hello же время позволяя информационных работников на совместимых устройствах службы tooaccess hello.</span><span class="sxs-lookup"><span data-stu-id="1db3a-113">**Conditional access for Office 365 applications with Microsoft Intune:** IT admins can provision conditional access device policies toosecure corporate resources, while at hello same time allowing information workers on compliant devices tooaccess hello services.</span></span> <span data-ttu-id="1db3a-114">Дополнительные сведения см. в статье о политиках условного доступа к Office 365 с устройств.</span><span class="sxs-lookup"><span data-stu-id="1db3a-114">For more information, see Conditional Access Device Policies for Office 365 services.</span></span>

- <span data-ttu-id="1db3a-115">**Tooapplications условного доступа, которые размещается локально:** зарегистрированные устройства можно использовать с политиками доступа для приложений, которые будут настроены toouse AD FS Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="1db3a-115">**Conditional access tooapplications that are hosted on-premises:** You can use registered devices with access policies for applications that are configured toouse AD FS with Windows Server 2012 R2.</span></span> <span data-ttu-id="1db3a-116">Узнать больше о настройке условного доступа для локальной среды можно в разделе [Настройка локального условного доступа с помощью регистрации устройств в Azure Active Directory](active-directory-device-registration-on-premises-setup.md).</span><span class="sxs-lookup"><span data-stu-id="1db3a-116">For more information about setting up conditional access for on-premises, see [Setting up On-premises Conditional Access using Azure Active Directory device registration](active-directory-device-registration-on-premises-setup.md).</span></span>

## <a name="setting-up-azure-active-directory-device-registration"></a><span data-ttu-id="1db3a-117">Настройка регистрации устройств в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1db3a-117">Setting up Azure Active Directory Device Registration</span></span>

<span data-ttu-id="1db3a-118">toosetup регистрацию устройств, у вас есть несколько вариантов:</span><span class="sxs-lookup"><span data-stu-id="1db3a-118">toosetup device registration, you have multiple options:</span></span>

- <span data-ttu-id="1db3a-119">Устройства можно регистрировать при tooAzure присоединены к домену AD домена.</span><span class="sxs-lookup"><span data-stu-id="1db3a-119">Devices can register when joined tooAzure AD domain.</span></span> <span data-ttu-id="1db3a-120">Для получения дополнительных сведений об этом разделе можно узнать больше о присоединении к Azure AD и hello параметры, необходимые для пользователей домена toojoin Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1db3a-120">For more on this topic, you can Learn more about Azure AD Join and hello settings required for users toojoin Azure AD domain.</span></span>

- <span data-ttu-id="1db3a-121">Устройства могут быть зарегистрированы при пользователей добавление работы или учебную учетные записи tooWindows на личных устройствах или при подключении ресурсов рабочих tooa требуется регистрация мобильного устройства.</span><span class="sxs-lookup"><span data-stu-id="1db3a-121">Devices can be registered when users add work or school accounts tooWindows on a personal device or when mobile devices connect tooa work resources requiring registration.</span></span> <span data-ttu-id="1db3a-122">tooensure это, необходимо включить регистрацию устройств в Azure AD в hello портала Azure.</span><span class="sxs-lookup"><span data-stu-id="1db3a-122">tooensure this, you must enable Azure AD Device Registration in hello Azure Portal.</span></span> 

- <span data-ttu-id="1db3a-123">Устройства можно зарегистрировать с помощью автоматической регистрации устройств для традиционных компьютеров, присоединенных к домену.</span><span class="sxs-lookup"><span data-stu-id="1db3a-123">Devices can be registered using automatic device registration for traditional domain-joined machines.</span></span> <span data-ttu-id="1db3a-124">tooensure это, необходимо первой установки Azure AD Connect, прежде чем продолжить автоматической регистрации устройств.</span><span class="sxs-lookup"><span data-stu-id="1db3a-124">tooensure this, you must first Setup Azure AD Connect before you continue with automatic device registration.</span></span>

<span data-ttu-id="1db3a-125">Последней инструкции в разделе [как tooconfigure Автоматическая регистрация Windows, присоединенных к домену устройствами с помощью Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md).</span><span class="sxs-lookup"><span data-stu-id="1db3a-125">For latest instructions, see [How tooconfigure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md).</span></span>  
<span data-ttu-id="1db3a-126">Также можно просмотреть и включить или отключить зарегистрированных устройств с помощью портала администрирования hello в Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1db3a-126">You can also review and enable or disable registered devices using hello Administrator Portal in Azure Active Directory.</span></span>

## <a name="enable-hello-azure-active-directory-device-registration-service"></a><span data-ttu-id="1db3a-127">Включение службы регистрации устройств Azure Active Directory hello</span><span class="sxs-lookup"><span data-stu-id="1db3a-127">Enable hello Azure Active Directory device registration service</span></span>

<span data-ttu-id="1db3a-128">**hello tooenable службы регистрации устройств Azure Active Directory:**</span><span class="sxs-lookup"><span data-stu-id="1db3a-128">**tooenable hello Azure Active Directory device registration service:**</span></span>

1.  <span data-ttu-id="1db3a-129">Войдите в toohello портал Microsoft Azure от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="1db3a-129">Sign in toohello Microsoft Azure portal as administrator.</span></span>

2.  <span data-ttu-id="1db3a-130">Выберите на левой панели hello **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1db3a-130">On hello left pane, select **Active Directory**.</span></span>

3.  <span data-ttu-id="1db3a-131">На вкладке каталог hello выберите свой каталог.</span><span class="sxs-lookup"><span data-stu-id="1db3a-131">On hello Directory tab, select your directory.</span></span>

4.  <span data-ttu-id="1db3a-132">Нажмите **Настроить**.</span><span class="sxs-lookup"><span data-stu-id="1db3a-132">Click **Configure**.</span></span>

5.  <span data-ttu-id="1db3a-133">Прокрутите слишком**устройств**.</span><span class="sxs-lookup"><span data-stu-id="1db3a-133">Scroll too**Devices**.</span></span>

6.  <span data-ttu-id="1db3a-134">Для параметра "Пользователи могут регистрировать устройства в Azure AD" выберите значение "Все".</span><span class="sxs-lookup"><span data-stu-id="1db3a-134">Select ALL for USERS MAY REGISTER THEIR DEVICES WITH AZURE AD.</span></span>

7.  <span data-ttu-id="1db3a-135">Выберите максимальное число hello устройств требуется tooauthorize на пользователя.</span><span class="sxs-lookup"><span data-stu-id="1db3a-135">Select hello maximum number of devices you want tooauthorize per user.</span></span>

<span data-ttu-id="1db3a-136">Hello регистрации с Microsoft Intune или управление мобильными устройствами для Office 365 требуется регистрация устройства.</span><span class="sxs-lookup"><span data-stu-id="1db3a-136">hello enrollment with Microsoft Intune or Mobile Device Management for Office 365 requires device registration.</span></span> <span data-ttu-id="1db3a-137">Если вы настроили одну из этих служб, то будет выбран пункт **ВСЕ**, а кнопка **НЕТ** будет отключена.</span><span class="sxs-lookup"><span data-stu-id="1db3a-137">If you have configured either of these services, **ALL** is selected and **NONE** is disabled.</span></span> <span data-ttu-id="1db3a-138">Убедитесь, что они настроены правильно и иметь соответствующие лицензии hello.</span><span class="sxs-lookup"><span data-stu-id="1db3a-138">Please ensure that they are configured correctly and have hello appropriate licensing.</span></span>

<span data-ttu-id="1db3a-139">По умолчанию двухфакторная проверка подлинности не включена для службы hello.</span><span class="sxs-lookup"><span data-stu-id="1db3a-139">By default, two-factor authentication is not enabled for hello service.</span></span> <span data-ttu-id="1db3a-140">Однако ее рекомендуется использовать при регистрации устройства.</span><span class="sxs-lookup"><span data-stu-id="1db3a-140">However, two-factor authentication is recommended when registering a device.</span></span>

- <span data-ttu-id="1db3a-141">Прежде чем делать обязательной двухфакторную проверку подлинности для этой службы, вы должны настроить поставщик двухфакторной проверки подлинности в Azure Active Directory и настроить учетные записи пользователей для многофакторной проверки подлинности см. в разделе Добавление многофакторной проверки подлинности tooAzure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1db3a-141">Before requiring two-factor authentication for this service, you must configure a two-factor authentication provider in Azure Active Directory and configure your user accounts for Multi-Factor Authentication, see Adding Multi-Factor Authentication tooAzure Active Directory</span></span>

- <span data-ttu-id="1db3a-142">Если вы используете службы федерации Active Directory с Windows Server 2012 R2, то для них необходимо настроить модуль двухфакторной проверки подлинности. Ознакомьтесь со статьей "Использование Многофакторной идентификации со службами федерации Active Directory".</span><span class="sxs-lookup"><span data-stu-id="1db3a-142">If you are using AD FS with Windows Server 2012 R2, you must configure a two-factor authentication module in AD FS, see Using Multi-Factor Authentication with Active Directory Federation Services.</span></span>

## <a name="view-and-manage-device-objects-in-azure-active-directory"></a><span data-ttu-id="1db3a-143">Просмотр объектов устройств в Azure Active Directory и управление ими</span><span class="sxs-lookup"><span data-stu-id="1db3a-143">View and manage device objects in Azure Active Directory</span></span>

<span data-ttu-id="1db3a-144">Из портала администратора Azure hello можно просматривать, блокировать и разблокировать устройства.</span><span class="sxs-lookup"><span data-stu-id="1db3a-144">From hello Azure Administrator portal, you can view, block, and unblock devices.</span></span> <span data-ttu-id="1db3a-145">Заблокированное устройство больше не будут иметь доступ tooapplications, которые настроенное tooallow только зарегистрированные устройства.</span><span class="sxs-lookup"><span data-stu-id="1db3a-145">A device that is blocked will no longer have access tooapplications that are configured tooallow only registered devices.</span></span>

<span data-ttu-id="1db3a-146">**tooview объектов устройств в Azure Active Directory и управления ими:**</span><span class="sxs-lookup"><span data-stu-id="1db3a-146">**tooview and manage device objects in Azure Active Directory:**</span></span>
 
1.  <span data-ttu-id="1db3a-147">Войдите на toohello портал Microsoft Azure от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="1db3a-147">Log on toohello Microsoft Azure portal as administrator.</span></span>

2.  <span data-ttu-id="1db3a-148">Выберите на левой панели hello **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1db3a-148">On hello left pane, select **Active Directory**.</span></span>

3.  <span data-ttu-id="1db3a-149">Выберите свой каталог.</span><span class="sxs-lookup"><span data-stu-id="1db3a-149">Select your directory.</span></span>

4.  <span data-ttu-id="1db3a-150">Выберите **Пользователи**.</span><span class="sxs-lookup"><span data-stu-id="1db3a-150">Select **Users**.</span></span> 

5.  <span data-ttu-id="1db3a-151">Нажмите кнопку hello пользователя, для которого требуется toosee hello устройств.</span><span class="sxs-lookup"><span data-stu-id="1db3a-151">Click hello user for which you want toosee hello devices.</span></span>

6.  <span data-ttu-id="1db3a-152">Выберите **Устройства**.</span><span class="sxs-lookup"><span data-stu-id="1db3a-152">Select **Devices**.</span></span>

7.  <span data-ttu-id="1db3a-153">Выберите **Зарегистрированные устройства**.</span><span class="sxs-lookup"><span data-stu-id="1db3a-153">Select **Registered Devices**.</span></span>

<span data-ttu-id="1db3a-154">Теперь можно просмотреть, заблокировать или разблокировать зарегистрированные устройства пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="1db3a-154">Now, you can review, block, or unblock hello user's registered devices.</span></span>
<span data-ttu-id="1db3a-155">Устройств Windows 10, которые являются локальными присоединенных к домену и автоматически зарегистрирует не отображаются на вкладке пользователи hello. Используйте toofind команду PowerShell Get-MsolDevice hello все устройства на предприятии.</span><span class="sxs-lookup"><span data-stu-id="1db3a-155">Windows 10 devices that are on-premises domain-joined and automatically registered do not appear under hello Users tab. Please use hello Get-MsolDevice PowerShell command toofind all your enterprise devices.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="1db3a-156">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1db3a-156">Next steps</span></span>

<span data-ttu-id="1db3a-157">toosetup автоматической регистрации устройств в разделе [как tooconfigure Автоматическая регистрация Windows, присоединенных к домену устройствами с помощью Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md).</span><span class="sxs-lookup"><span data-stu-id="1db3a-157">toosetup automated device registration, see [How tooconfigure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md).</span></span>


