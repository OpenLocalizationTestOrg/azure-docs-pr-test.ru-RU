---
title: "Как настроить автоматическую регистрацию присоединенных к домену устройств Windows в Azure Active Directory | Документация Майкрософт"
description: "Настройте автоматическую регистрацию устройств Windows, присоединенных к домену, без предупреждений с помощью Azure Active Directory."
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
ms.openlocfilehash: 38750050e8525272079e1f3a5509da1e8f0a557b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="get-started-with-azure-active-directory-device-registration"></a><span data-ttu-id="dab3a-103">Знакомство с регистрацией устройств в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="dab3a-103">Get started with Azure Active Directory device registration</span></span>

<span data-ttu-id="dab3a-104">Регистрация устройств в Azure Active Directory лежит в основе всех сценариев условного доступа с устройств.</span><span class="sxs-lookup"><span data-stu-id="dab3a-104">Azure Active Directory device registration is the foundation for device-based conditional access scenarios.</span></span> <span data-ttu-id="dab3a-105">Служба регистрации устройств Azure Active Directory назначает регистрируемому устройству идентификатор, который позволяет аутентифицировать его при входе пользователя.</span><span class="sxs-lookup"><span data-stu-id="dab3a-105">When a device is registered, Azure Active Directory device registration provides the device with an identity which is used to authenticate the device when the user signs in.</span></span> <span data-ttu-id="dab3a-106">Аутентифицированное устройство и его атрибуты затем можно использовать для принудительного соблюдения политик условного доступа в приложениях, размещенных в облаке и локально.</span><span class="sxs-lookup"><span data-stu-id="dab3a-106">The authenticated device, and the attributes of the device, can then be used to enforce conditional access policies for applications that are hosted in the cloud and on-premises.</span></span>

<span data-ttu-id="dab3a-107">При использовании таких решений MDM (управление мобильными устройствами), как Microsoft Intune, в атрибуты устройства в Azure Active Directory добавляются дополнительные данные о нем.</span><span class="sxs-lookup"><span data-stu-id="dab3a-107">When combined with a mobile device management(MDM) solution such as Microsoft Intune, the device attributes in Azure Active Directory are updated with additional information about the device.</span></span> <span data-ttu-id="dab3a-108">Это позволяет создавать правила условного доступа, которые обеспечивают доступ с устройств в соответствии с вашими стандартами безопасности и соблюдения нормативных требований.</span><span class="sxs-lookup"><span data-stu-id="dab3a-108">This allows you to create conditional access rules that enforce access from devices to meet your standards for security and compliance.</span></span> <span data-ttu-id="dab3a-109">Дополнительные сведения о регистрации устройств в Microsoft Intune см. в статье "Регистрация устройств для управления в Intune".</span><span class="sxs-lookup"><span data-stu-id="dab3a-109">For more information on enrolling devices in Microsoft Intune, see Enroll devices for management in Intune.</span></span>
<span data-ttu-id="dab3a-110">Сценарии, обеспечиваемые службой регистрации устройств Azure Active Directory. Регистрация устройств в Azure Active Directory предусматривает поддержку устройств Windows, iOS и Android.</span><span class="sxs-lookup"><span data-stu-id="dab3a-110">Scenarios enabled by Azure Active Directory Device Registration Azure Active Directory Device Registration includes support for iOS, Android, and Windows devices.</span></span> <span data-ttu-id="dab3a-111">В отдельных сценариях использования службы регистрации устройств Azure AD могут действовать особые требования и поддерживаться другие платформы.</span><span class="sxs-lookup"><span data-stu-id="dab3a-111">The individual scenarios that utilize Azure AD Device Registration may have more specific requirements and platform support.</span></span> 

<span data-ttu-id="dab3a-112">Эти сценарии выглядят так.</span><span class="sxs-lookup"><span data-stu-id="dab3a-112">These scenarios are as follows:</span></span>

- <span data-ttu-id="dab3a-113">**Условный доступ к приложениям Office 365 с использованием Microsoft Intune**. ИТ-администраторы могут подготавливать политики условного доступа устройств для защиты корпоративных ресурсов, при этом разрешая информационным работникам обращаться к службам на совместимых устройствах.</span><span class="sxs-lookup"><span data-stu-id="dab3a-113">**Conditional access for Office 365 applications with Microsoft Intune:** IT admins can provision conditional access device policies to secure corporate resources, while at the same time allowing information workers on compliant devices to access the services.</span></span> <span data-ttu-id="dab3a-114">Дополнительные сведения см. в статье о политиках условного доступа к Office 365 с устройств.</span><span class="sxs-lookup"><span data-stu-id="dab3a-114">For more information, see Conditional Access Device Policies for Office 365 services.</span></span>

- <span data-ttu-id="dab3a-115">**Условный доступ к приложениям, размещенным локально**. Для зарегистрированных устройств можно применять политики доступа к приложениям, настройки которых позволяют использовать службы федерации Active Directory в Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="dab3a-115">**Conditional access to applications that are hosted on-premises:** You can use registered devices with access policies for applications that are configured to use AD FS with Windows Server 2012 R2.</span></span> <span data-ttu-id="dab3a-116">Узнать больше о настройке условного доступа для локальной среды можно в разделе [Настройка локального условного доступа с помощью регистрации устройств в Azure Active Directory](active-directory-device-registration-on-premises-setup.md).</span><span class="sxs-lookup"><span data-stu-id="dab3a-116">For more information about setting up conditional access for on-premises, see [Setting up On-premises Conditional Access using Azure Active Directory device registration](active-directory-device-registration-on-premises-setup.md).</span></span>

## <a name="setting-up-azure-active-directory-device-registration"></a><span data-ttu-id="dab3a-117">Настройка регистрации устройств в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="dab3a-117">Setting up Azure Active Directory Device Registration</span></span>

<span data-ttu-id="dab3a-118">Есть несколько вариантов настройки регистрации устройств:</span><span class="sxs-lookup"><span data-stu-id="dab3a-118">To setup device registration, you have multiple options:</span></span>

- <span data-ttu-id="dab3a-119">Устройства можно зарегистрировать, когда выполняется присоединение к домену Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dab3a-119">Devices can register when joined to Azure AD domain.</span></span> <span data-ttu-id="dab3a-120">Ознакомьтесь с дополнительными сведениями о присоединении к Azure AD, а также с параметрами, необходимыми для пользователей при присоединении к домену Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dab3a-120">For more on this topic, you can Learn more about Azure AD Join and the settings required for users to join Azure AD domain.</span></span>

- <span data-ttu-id="dab3a-121">Устройства можно зарегистрировать при добавлении пользователями рабочих или учебных учетных записей Windows на личные устройства или при подключении мобильных устройств к рабочим ресурсам, требующим регистрации.</span><span class="sxs-lookup"><span data-stu-id="dab3a-121">Devices can be registered when users add work or school accounts to Windows on a personal device or when mobile devices connect to a work resources requiring registration.</span></span> <span data-ttu-id="dab3a-122">Для этого необходимо включить регистрацию устройств в Azure AD на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="dab3a-122">To ensure this, you must enable Azure AD Device Registration in the Azure Portal.</span></span> 

- <span data-ttu-id="dab3a-123">Устройства можно зарегистрировать с помощью автоматической регистрации устройств для традиционных компьютеров, присоединенных к домену.</span><span class="sxs-lookup"><span data-stu-id="dab3a-123">Devices can be registered using automatic device registration for traditional domain-joined machines.</span></span> <span data-ttu-id="dab3a-124">Для этого сначала необходимо настроить Azure AD Connect, а затем выполнить автоматическую регистрацию устройств.</span><span class="sxs-lookup"><span data-stu-id="dab3a-124">To ensure this, you must first Setup Azure AD Connect before you continue with automatic device registration.</span></span>

<span data-ttu-id="dab3a-125">Дополнительные сведения см. в статье [Настройка автоматической регистрации присоединенных к домену устройств Windows в Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md).</span><span class="sxs-lookup"><span data-stu-id="dab3a-125">For latest instructions, see [How to configure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md).</span></span>  
<span data-ttu-id="dab3a-126">Вы можете также просмотреть и включить или выключить зарегистрированные устройства с помощью портала администрирования в Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="dab3a-126">You can also review and enable or disable registered devices using the Administrator Portal in Azure Active Directory.</span></span>

## <a name="enable-the-azure-active-directory-device-registration-service"></a><span data-ttu-id="dab3a-127">Включение службы регистрации устройств Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="dab3a-127">Enable the Azure Active Directory device registration service</span></span>

<span data-ttu-id="dab3a-128">**Чтобы включить службу регистрации устройств Azure Active Directory, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="dab3a-128">**To enable the Azure Active Directory device registration service:**</span></span>

1.  <span data-ttu-id="dab3a-129">Войдите на портал Microsoft Azure как администратор.</span><span class="sxs-lookup"><span data-stu-id="dab3a-129">Sign in to the Microsoft Azure portal as administrator.</span></span>

2.  <span data-ttu-id="dab3a-130">На панели слева выберите **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="dab3a-130">On the left pane, select **Active Directory**.</span></span>

3.  <span data-ttu-id="dab3a-131">На вкладке «Каталог» выберите требуемый каталог.</span><span class="sxs-lookup"><span data-stu-id="dab3a-131">On the Directory tab, select your directory.</span></span>

4.  <span data-ttu-id="dab3a-132">Нажмите **Настроить**.</span><span class="sxs-lookup"><span data-stu-id="dab3a-132">Click **Configure**.</span></span>

5.  <span data-ttu-id="dab3a-133">Прокрутите страницу до раздела **Устройства**.</span><span class="sxs-lookup"><span data-stu-id="dab3a-133">Scroll to **Devices**.</span></span>

6.  <span data-ttu-id="dab3a-134">Для параметра "Пользователи могут регистрировать устройства в Azure AD" выберите значение "Все".</span><span class="sxs-lookup"><span data-stu-id="dab3a-134">Select ALL for USERS MAY REGISTER THEIR DEVICES WITH AZURE AD.</span></span>

7.  <span data-ttu-id="dab3a-135">Выберите максимальное число устройств, которое требуется авторизовать для одного пользователя.</span><span class="sxs-lookup"><span data-stu-id="dab3a-135">Select the maximum number of devices you want to authorize per user.</span></span>

<span data-ttu-id="dab3a-136">Для регистрации в Microsoft Intune или службе управления мобильными устройствами для Office 365 требуется регистрация устройств.</span><span class="sxs-lookup"><span data-stu-id="dab3a-136">The enrollment with Microsoft Intune or Mobile Device Management for Office 365 requires device registration.</span></span> <span data-ttu-id="dab3a-137">Если вы настроили одну из этих служб, то будет выбран пункт **ВСЕ**, а кнопка **НЕТ** будет отключена.</span><span class="sxs-lookup"><span data-stu-id="dab3a-137">If you have configured either of these services, **ALL** is selected and **NONE** is disabled.</span></span> <span data-ttu-id="dab3a-138">Убедитесь, что все настроено правильно и имеются соответствующие лицензии.</span><span class="sxs-lookup"><span data-stu-id="dab3a-138">Please ensure that they are configured correctly and have the appropriate licensing.</span></span>

<span data-ttu-id="dab3a-139">По умолчанию двухфакторная проверка подлинности для службы не включена.</span><span class="sxs-lookup"><span data-stu-id="dab3a-139">By default, two-factor authentication is not enabled for the service.</span></span> <span data-ttu-id="dab3a-140">Однако ее рекомендуется использовать при регистрации устройства.</span><span class="sxs-lookup"><span data-stu-id="dab3a-140">However, two-factor authentication is recommended when registering a device.</span></span>

- <span data-ttu-id="dab3a-141">Прежде чем делать обязательной двухфакторную проверку подлинности для службы, необходимо настроить поставщик двухфакторной проверки подлинности в Azure Active Directory, а также настроить учетные записи пользователей для работы с Multi-Factor Authentication. См. раздел «Использование Multi-Factor Authentication со службами федерации Active Directory».</span><span class="sxs-lookup"><span data-stu-id="dab3a-141">Before requiring two-factor authentication for this service, you must configure a two-factor authentication provider in Azure Active Directory and configure your user accounts for Multi-Factor Authentication, see Adding Multi-Factor Authentication to Azure Active Directory</span></span>

- <span data-ttu-id="dab3a-142">Если вы используете службы федерации Active Directory с Windows Server 2012 R2, то для них необходимо настроить модуль двухфакторной проверки подлинности. Ознакомьтесь со статьей "Использование Многофакторной идентификации со службами федерации Active Directory".</span><span class="sxs-lookup"><span data-stu-id="dab3a-142">If you are using AD FS with Windows Server 2012 R2, you must configure a two-factor authentication module in AD FS, see Using Multi-Factor Authentication with Active Directory Federation Services.</span></span>

## <a name="view-and-manage-device-objects-in-azure-active-directory"></a><span data-ttu-id="dab3a-143">Просмотр объектов устройств в Azure Active Directory и управление ими</span><span class="sxs-lookup"><span data-stu-id="dab3a-143">View and manage device objects in Azure Active Directory</span></span>

<span data-ttu-id="dab3a-144">На портале администрирования Azure можно просматривать, блокировать и разблокировать устройства.</span><span class="sxs-lookup"><span data-stu-id="dab3a-144">From the Azure Administrator portal, you can view, block, and unblock devices.</span></span> <span data-ttu-id="dab3a-145">Заблокированное устройство лишается доступа к приложениям, которые настроены для доступа только с зарегистрированных устройств.</span><span class="sxs-lookup"><span data-stu-id="dab3a-145">A device that is blocked will no longer have access to applications that are configured to allow only registered devices.</span></span>

<span data-ttu-id="dab3a-146">**Для просмотра объектов устройств в Azure Active Directory и управления ими выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="dab3a-146">**To view and manage device objects in Azure Active Directory:**</span></span>
 
1.  <span data-ttu-id="dab3a-147">Войдите на портал Microsoft Azure как администратор.</span><span class="sxs-lookup"><span data-stu-id="dab3a-147">Log on to the Microsoft Azure portal as administrator.</span></span>

2.  <span data-ttu-id="dab3a-148">На панели слева выберите **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="dab3a-148">On the left pane, select **Active Directory**.</span></span>

3.  <span data-ttu-id="dab3a-149">Выберите свой каталог.</span><span class="sxs-lookup"><span data-stu-id="dab3a-149">Select your directory.</span></span>

4.  <span data-ttu-id="dab3a-150">Выберите **Пользователи**.</span><span class="sxs-lookup"><span data-stu-id="dab3a-150">Select **Users**.</span></span> 

5.  <span data-ttu-id="dab3a-151">Щелкните пользователя, для которого требуется просмотреть устройства.</span><span class="sxs-lookup"><span data-stu-id="dab3a-151">Click the user for which you want to see the devices.</span></span>

6.  <span data-ttu-id="dab3a-152">Выберите **Устройства**.</span><span class="sxs-lookup"><span data-stu-id="dab3a-152">Select **Devices**.</span></span>

7.  <span data-ttu-id="dab3a-153">Выберите **Зарегистрированные устройства**.</span><span class="sxs-lookup"><span data-stu-id="dab3a-153">Select **Registered Devices**.</span></span>

<span data-ttu-id="dab3a-154">Теперь вы можете просмотреть, заблокировать или разблокировать зарегистрированные устройства пользователя.</span><span class="sxs-lookup"><span data-stu-id="dab3a-154">Now, you can review, block, or unblock the user's registered devices.</span></span>
<span data-ttu-id="dab3a-155">На вкладке "Пользователи" не отображаются устройства Windows 10, которые присоединены к локальному домену и автоматически зарегистрированы.</span><span class="sxs-lookup"><span data-stu-id="dab3a-155">Windows 10 devices that are on-premises domain-joined and automatically registered do not appear under the Users tab.</span></span> <span data-ttu-id="dab3a-156">Используйте команду PowerShell Get-MsolDevice, чтобы найти все корпоративные устройства.</span><span class="sxs-lookup"><span data-stu-id="dab3a-156">Please use the Get-MsolDevice PowerShell command to find all your enterprise devices.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="dab3a-157">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="dab3a-157">Next steps</span></span>

<span data-ttu-id="dab3a-158">Чтобы настроить автоматическую регистрацию устройств, см. статью [Настройка автоматической регистрации присоединенных к домену устройств Windows в Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md).</span><span class="sxs-lookup"><span data-stu-id="dab3a-158">To setup automated device registration, see [How to configure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md).</span></span>


