---
title: "Общие сведения об управлении устройствами в Azure Active Directory | Документация Майкрософт"
description: "Узнайте, как с помощью управления устройствами можно контролировать устройства, получающие доступ к ресурсам в вашей среде."
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
ms.date: 08/24/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: bebbdddf6b591ea7e36cbac38b568bce614bb335
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="introduction-to-device-management-in-azure-active-directory"></a><span data-ttu-id="0857a-103">Общие сведения об управлении устройствами в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0857a-103">Introduction to device management in Azure Active Directory</span></span>

<span data-ttu-id="0857a-104">В эпоху мобильных и облачных технологий Azure Active Directory (Azure AD) обеспечивает единый вход для устройств, приложений и служб из любого расположения.</span><span class="sxs-lookup"><span data-stu-id="0857a-104">In a mobile-first, cloud-first world, Azure Active Directory (Azure AD) enables single sign-on to devices, apps, and services from anywhere.</span></span> <span data-ttu-id="0857a-105">В связи с увеличением количества устройств (включая BYOD) ИТ-специалисты все чаще сталкиваются с двумя противоположными задачами:</span><span class="sxs-lookup"><span data-stu-id="0857a-105">With the proliferation of devices - including Bring Your Own Device (BYOD), IT professionals are faced with two opposing goals:</span></span>

- <span data-ttu-id="0857a-106">продуктивная работа пользователей в любом месте и в любое время;</span><span class="sxs-lookup"><span data-stu-id="0857a-106">Empower the end users to be productive wherever and whenever</span></span>
- <span data-ttu-id="0857a-107">постоянная защита корпоративных ресурсов.</span><span class="sxs-lookup"><span data-stu-id="0857a-107">Protect the corporate assets at any time</span></span>

<span data-ttu-id="0857a-108">С помощью устройств пользователи получают доступ к корпоративным ресурсам.</span><span class="sxs-lookup"><span data-stu-id="0857a-108">Through devices, your users are getting access to your corporate assets.</span></span> <span data-ttu-id="0857a-109">В целях защиты корпоративных ресурсов ИТ-администраторам требуются возможности управления этими устройствами.</span><span class="sxs-lookup"><span data-stu-id="0857a-109">To protect your corporate assets, as an IT administrator, you want to have control over these devices.</span></span> <span data-ttu-id="0857a-110">Это позволит предоставлять пользователям доступ к ресурсам с устройств, которые соответствуют стандартам безопасности и нормативным требованиям.</span><span class="sxs-lookup"><span data-stu-id="0857a-110">This enables you to make sure that your users are accessing your resources from devices that meet your standards for security and compliance.</span></span> 

<span data-ttu-id="0857a-111">Управление устройствами также лежит в основе [условного доступа с устройств](active-directory-conditional-access-policy-connected-applications.md).</span><span class="sxs-lookup"><span data-stu-id="0857a-111">Device management is also the foundation for [device-based conditional access](active-directory-conditional-access-policy-connected-applications.md).</span></span> <span data-ttu-id="0857a-112">Используя условный доступ с устройств, можно разрешать доступ к ресурсам в своей среде только доверенным устройствам.</span><span class="sxs-lookup"><span data-stu-id="0857a-112">With device-based conditional access, you can ensure that access to resources in your environment is only possible with trusted devices.</span></span>   

<span data-ttu-id="0857a-113">В этом разделе описывается, как работает управление устройствами в Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0857a-113">This topic explains how device management in Azure Active Directory works.</span></span>

## <a name="getting-devices-under-the-control-of-azure-ad"></a><span data-ttu-id="0857a-114">Ввод устройств под контроль Azure AD</span><span class="sxs-lookup"><span data-stu-id="0857a-114">Getting devices under the control of Azure AD</span></span>

<span data-ttu-id="0857a-115">Существует два варианта ввода устройств под контроль Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0857a-115">To get a device under the control of Azure AD, you have two options:</span></span>

- <span data-ttu-id="0857a-116">Регистрация</span><span class="sxs-lookup"><span data-stu-id="0857a-116">Registering</span></span> 
- <span data-ttu-id="0857a-117">Присоединение</span><span class="sxs-lookup"><span data-stu-id="0857a-117">Joining</span></span>

<span data-ttu-id="0857a-118">**Регистрация** устройства в Azure AD позволяет управлять идентификатором устройства.</span><span class="sxs-lookup"><span data-stu-id="0857a-118">**Registering** a device to Azure AD enables you to manage a device’s identity.</span></span> <span data-ttu-id="0857a-119">В ходе регистрации служба регистрации устройств Azure Active Directory назначает устройству идентификатор, который используется для проверки подлинности устройства при входе пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0857a-119">When a device is registered, Azure AD device registration provides the device with an identity that is used to authenticate the device when a user signs-in to Azure AD.</span></span> <span data-ttu-id="0857a-120">Идентификатор можно использовать для включения или отключения устройства.</span><span class="sxs-lookup"><span data-stu-id="0857a-120">You can use the identity to enable or disable a device.</span></span>

<span data-ttu-id="0857a-121">При применении вместе с таким решением MDM (управление мобильными устройствами), как Microsoft Intune, в атрибуты устройства в Azure Active Directory добавляются дополнительные данные о нем.</span><span class="sxs-lookup"><span data-stu-id="0857a-121">When combined with a mobile device management(MDM) solution such as Microsoft Intune, the device attributes in Azure AD are updated with additional information about the device.</span></span> <span data-ttu-id="0857a-122">Это позволяет создавать правила условного доступа, которые обеспечивают доступ с устройств в соответствии с вашими стандартами безопасности и соблюдения нормативных требований.</span><span class="sxs-lookup"><span data-stu-id="0857a-122">This allows you to create conditional access rules that enforce access from devices to meet your standards for security and compliance.</span></span> <span data-ttu-id="0857a-123">Дополнительные сведения о регистрации устройств в Microsoft Intune см. в статье "Регистрация устройств для управления в Intune".</span><span class="sxs-lookup"><span data-stu-id="0857a-123">For more information on enrolling devices in Microsoft Intune, see Enroll devices for management in Intune .</span></span>

<span data-ttu-id="0857a-124">**Присоединение** устройства является расширением для регистрации устройства.</span><span class="sxs-lookup"><span data-stu-id="0857a-124">**Joining** a device is an extension to registering a device.</span></span> <span data-ttu-id="0857a-125">Это означает, что оно предоставляет все преимущества регистрации устройства и дополнительно изменяет локальное состояние устройства.</span><span class="sxs-lookup"><span data-stu-id="0857a-125">This means, it provides you with all the benefits of registering a device and in addition to this, it also changes the local state of a device.</span></span> <span data-ttu-id="0857a-126">За счет изменения локального состояния пользователи могут входить на устройство с помощью рабочей или учебной учетной записи организации вместо личной учетной записи.</span><span class="sxs-lookup"><span data-stu-id="0857a-126">Changing the local state enables your users to sign-in to a device using an organizational work or school account instead of a personal account.</span></span>

## <a name="azure-ad-registered-devices"></a><span data-ttu-id="0857a-127">Устройства, зарегистрированные в Azure AD</span><span class="sxs-lookup"><span data-stu-id="0857a-127">Azure AD registered devices</span></span>   

<span data-ttu-id="0857a-128">Устройства, зарегистрированные в Azure AD, обеспечивают поддержку в сценарии **Принеси свое устройство (BYOD)**.</span><span class="sxs-lookup"><span data-stu-id="0857a-128">The goal of Azure AD registered devices is to provide you with support for the **Bring Your Own Device (BYOD)** scenario.</span></span> <span data-ttu-id="0857a-129">В этом случае пользователь может обращаться к корпоративным ресурсам под контролем Azure Active Directory с помощью личного устройства.</span><span class="sxs-lookup"><span data-stu-id="0857a-129">In this scenario, a user can access your organization’s Azure Active Directory controlled resources using a personal device.</span></span>  

![Устройства, зарегистрированные в Azure AD](./media/device-management-introduction/03.png)

<span data-ttu-id="0857a-131">Доступ основан на рабочей или учебной учетной записи, которая была введена на устройстве.</span><span class="sxs-lookup"><span data-stu-id="0857a-131">The access is based on a work or school account that has been entered on the device.</span></span>  
<span data-ttu-id="0857a-132">Например, Windows 10 позволяет добавлять рабочую или учебную учетную запись на ПК, планшет или телефон.</span><span class="sxs-lookup"><span data-stu-id="0857a-132">For example, Windows 10 enables users to add a work or school account to a personal computer, tablet, or phone.</span></span>  
<span data-ttu-id="0857a-133">После того как пользователь добавит рабочую или учебную учетную запись, устройство регистрируется в Azure AD, а при необходимости — также в системе управления мобильными устройствами (MDM), настроенной в организации.</span><span class="sxs-lookup"><span data-stu-id="0857a-133">When a user has added a work or school account, the device is registered with Azure AD and optionally enrolled in the mobile device management (MDM) system that your organization has configured.</span></span> <span data-ttu-id="0857a-134">Пользователи организации могут удобно добавлять рабочие или учебные учетные записи на свои личные устройства:</span><span class="sxs-lookup"><span data-stu-id="0857a-134">Your organization’s users can add a work or school account to a personal device conveniently:</span></span>

- <span data-ttu-id="0857a-135">при первом доступе к рабочему приложению;</span><span class="sxs-lookup"><span data-stu-id="0857a-135">When accessing a work application for the first time</span></span>
- <span data-ttu-id="0857a-136">вручную через меню **Параметры** (при использовании Windows 10).</span><span class="sxs-lookup"><span data-stu-id="0857a-136">Manually via the **Settings** menu in the case of Windows 10</span></span> 

<span data-ttu-id="0857a-137">Устройства, зарегистрированные в Azure AD, можно настроить для Windows 10, iOS, Android и macOS.</span><span class="sxs-lookup"><span data-stu-id="0857a-137">You can configure Azure AD registered devices for Windows 10, iOS, Android and macOS.</span></span>

## <a name="azure-ad-joined-devices"></a><span data-ttu-id="0857a-138">Устройства, присоединенные к Azure AD</span><span class="sxs-lookup"><span data-stu-id="0857a-138">Azure AD joined devices</span></span>

<span data-ttu-id="0857a-139">Устройства, присоединенные к Azure AD, упрощают выполнение следующих задач:</span><span class="sxs-lookup"><span data-stu-id="0857a-139">The goal of Azure AD joined devices is to simplify:</span></span>

- <span data-ttu-id="0857a-140">развертывание Windows на корпоративных устройствах;</span><span class="sxs-lookup"><span data-stu-id="0857a-140">Windows deployments of work-owned devices</span></span> 
- <span data-ttu-id="0857a-141">доступ к корпоративным приложениям и ресурсам с любого устройства Windows.</span><span class="sxs-lookup"><span data-stu-id="0857a-141">Access to organizational apps and resources from any Windows device</span></span>

![Устройства, зарегистрированные в Azure AD](./media/device-management-introduction/02.png)


<span data-ttu-id="0857a-143">Для достижения этих целей пользователям предоставляются возможности самостоятельного ввода корпоративных устройств под управление Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0857a-143">These goals are accomplished by providing your users with a self-service experience for getting work-owned devices under the control of Azure AD.</span></span>  
<span data-ttu-id="0857a-144">**Присоединение к Azure AD** предназначено для организаций, в которых мобильные устройства и облачные технологии стоят на первом месте.</span><span class="sxs-lookup"><span data-stu-id="0857a-144">**Azure AD Join** is intended for organizations that are cloud-first / cloud-only.</span></span> <span data-ttu-id="0857a-145">Обычно это предприятия малого и среднего бизнеса, у которых нет локальной инфраструктуры Windows Server Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0857a-145">These are typically small- and medium-sized businesses that do not have an on-premises Windows Server Active Directory infrastructure.</span></span> 

<span data-ttu-id="0857a-146">Интеграция устройств, присоединенных к Azure AD, обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="0857a-146">Implementing Azure AD joined devices provides you with the following benefits:</span></span>

- <span data-ttu-id="0857a-147">**Единый вход (SSO)** в управляемые Azure приложения и службы SaaS.</span><span class="sxs-lookup"><span data-stu-id="0857a-147">**Single-Sign-On (SSO)** to your Azure managed SaaS apps and services.</span></span> <span data-ttu-id="0857a-148">При доступе к рабочим ресурсам пользователи не видят запросов на дополнительную проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="0857a-148">Your users don’t see additional authentication prompts when accessing work resources.</span></span> <span data-ttu-id="0857a-149">Функциональные возможности единого входа действуют даже при отсутствии подключения к доступной доменной сети.</span><span class="sxs-lookup"><span data-stu-id="0857a-149">The SSO functionality is even when they are not connected to the domain network available.</span></span>

- <span data-ttu-id="0857a-150">**Перенос** пользовательских параметров между устройствами с поддержкой рабочих или учебных учетных записей (с соблюдением корпоративных требований).</span><span class="sxs-lookup"><span data-stu-id="0857a-150">**Enterprise compliant roaming** of user settings across joined devices.</span></span> <span data-ttu-id="0857a-151">Для просмотра параметров на устройствах пользователям не нужно подключать учетную запись Майкрософт (например, Hotmail).</span><span class="sxs-lookup"><span data-stu-id="0857a-151">Users don’t need to connect a Microsoft account (for example, Hotmail) to see settings across devices.</span></span>

- <span data-ttu-id="0857a-152">**Доступ к Магазину Windows для бизнеса** с использованием учетной записи AD.</span><span class="sxs-lookup"><span data-stu-id="0857a-152">**Access to Windows Store for Business** using AD account.</span></span> <span data-ttu-id="0857a-153">Пользователи могут выбирать из коллекции предварительно определенных приложений в организации.</span><span class="sxs-lookup"><span data-stu-id="0857a-153">Your users can choose from an inventory of applications pre-selected by the organization.</span></span>

- <span data-ttu-id="0857a-154">Поддержка **Windows Hello** для удобного и безопасного доступа к ресурсам.</span><span class="sxs-lookup"><span data-stu-id="0857a-154">**Windows Hello** support for secure and convenient access to work resources.</span></span>

- <span data-ttu-id="0857a-155">**Ограничение доступа** к приложениям только с тех устройств, которые отвечают политике соответствия.</span><span class="sxs-lookup"><span data-stu-id="0857a-155">**Restriction of access** to apps from only devices that meet compliance policy.</span></span>

<span data-ttu-id="0857a-156">Несмотря на то, что присоединение к Azure AD в первую очередь предназначено для организаций, у которых нет локальной инфраструктуры Windows Server Active Directory, его, безусловно, можно использовать в следующих сценариях:</span><span class="sxs-lookup"><span data-stu-id="0857a-156">While Azure AD join is primarily intended for organizations that do not have an on-premises Windows Server Active Directory infrastructure, you can certainly also use it in scenarios where:</span></span>

- <span data-ttu-id="0857a-157">вы не можете использовать присоединение к домену в локальной среде, например если требуется управлять мобильными устройствами, такими как планшеты и телефоны;</span><span class="sxs-lookup"><span data-stu-id="0857a-157">You can’t use an on-premises domain join, for example, if you need to get mobile devices such as tablets and phones under control.</span></span>

- <span data-ttu-id="0857a-158">вашим пользователям в основном нужен доступ к Office 365 или другим приложения SaaS, интегрированным с Azure AD;</span><span class="sxs-lookup"><span data-stu-id="0857a-158">Your users primarily need to access Office 365 or other SaaS apps integrated with Azure AD.</span></span>

- <span data-ttu-id="0857a-159">вы хотите управлять группой пользователей в Azure AD, а не в Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0857a-159">You want to manage a group of users in Azure AD instead of in Active Directory.</span></span> <span data-ttu-id="0857a-160">Это может действовать, например, для сезонных сотрудников, подрядчиков или учащихся.</span><span class="sxs-lookup"><span data-stu-id="0857a-160">This can apply, for example, to seasonal workers, contractors, or students.</span></span>

- <span data-ttu-id="0857a-161">вы хотите, чтобы работники удаленных филиалов с ограниченной локальной инфраструктурой могли подключаться к основной сети;</span><span class="sxs-lookup"><span data-stu-id="0857a-161">You want to provide joining capabilities to workers in remote branch offices with limited on-premises infrastructure.</span></span>

<span data-ttu-id="0857a-162">Можно настроить устройства, присоединенные к Azure AD, для устройств Windows 10.</span><span class="sxs-lookup"><span data-stu-id="0857a-162">You can configure Azure AD joined devices for Windows 10 devices.</span></span>


## <a name="hybrid-azure-ad-joined-devices"></a><span data-ttu-id="0857a-163">Гибридные устройства, присоединенные к Azure AD</span><span class="sxs-lookup"><span data-stu-id="0857a-163">Hybrid Azure AD joined devices</span></span>

<span data-ttu-id="0857a-164">На протяжении более десяти лет многие организации использовали присоединение к доменам в своей локальной среде Active Directory для предоставления возможностей:</span><span class="sxs-lookup"><span data-stu-id="0857a-164">For more than a decade, many organizations have used the domain join to their on-premises Active Directory to enable:</span></span>

- <span data-ttu-id="0857a-165">ИТ-отделам для управления корпоративными устройствами центрального расположения;</span><span class="sxs-lookup"><span data-stu-id="0857a-165">IT departments to manage work-owned devices from a central location.</span></span>

- <span data-ttu-id="0857a-166">пользователям для входа на устройства с помощью рабочих или учебных учетных записей Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0857a-166">Users to sign in to their devices with their Active Directory work or school accounts.</span></span> 

<span data-ttu-id="0857a-167">Как правило, организации с локальной службой создают для подготовки устройств системные образы, а для управления устройствами часто применяют **System Center Configuration Manager (SCCM)** или **групповые политики**.</span><span class="sxs-lookup"><span data-stu-id="0857a-167">Typically, organizations with an on-premises footprint rely on imaging methods to provision devices, and they often use **System Center Configuration Manager (SCCM)** or **group policy (GP)** to manage them.</span></span>

<span data-ttu-id="0857a-168">Если в вашей среде действует локальная служба AD и вы также хотите получить выгоду от возможностей, предоставляемых Azure Active Directory, можно использовать гибридные устройства, присоединенные к Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0857a-168">If your environment has an on-premises AD footprint and you also want benefit from the capabilities provided by Azure Active Directory, you can implement hybrid Azure AD joined devices.</span></span> <span data-ttu-id="0857a-169">Это устройства, которые присоединены и к локальной среде Active Directory, и к Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0857a-169">These are devices that are both, joined to your on-premises Active Directory and your Azure Active Directory.</span></span>

![Устройства, зарегистрированные в Azure AD](./media/device-management-introduction/01.png)


<span data-ttu-id="0857a-171">Гибридные устройства, присоединенные к Azure AD, следует использовать в указанных далее случаях.</span><span class="sxs-lookup"><span data-stu-id="0857a-171">You should use Azure AD hybrid joined devices if:</span></span>

- <span data-ttu-id="0857a-172">У вас есть развернутые на мобильных устройствах приложения Win32, которые используют NTLM или Kerberos.</span><span class="sxs-lookup"><span data-stu-id="0857a-172">You have Win32 apps deployed to these devices that use NTLM / Kerberos.</span></span>

- <span data-ttu-id="0857a-173">Для управления устройствами вам нужны групповые политики или SCCM/DCM.</span><span class="sxs-lookup"><span data-stu-id="0857a-173">You require GP or SCCM / DCM to manage devices.</span></span>

- <span data-ttu-id="0857a-174">Вы хотите и дальше использовать системные образы для настройки устройств сотрудников.</span><span class="sxs-lookup"><span data-stu-id="0857a-174">You want to continue to use imaging solutions to configure devices for your employees.</span></span>

<span data-ttu-id="0857a-175">Можно настроить гибридные устройства, присоединенные к Azure AD, для устройств Windows 10 низкого уровня, например Windows 8 и Windows 7.</span><span class="sxs-lookup"><span data-stu-id="0857a-175">You can configure Hybrid Azure AD joined devices for Windows 10 and down-level devices such as Windows 8 and Windows 7.</span></span>

## <a name="summary"></a><span data-ttu-id="0857a-176">Сводка</span><span class="sxs-lookup"><span data-stu-id="0857a-176">Summary</span></span>

<span data-ttu-id="0857a-177">Управление устройствами в Azure AD позволяет:</span><span class="sxs-lookup"><span data-stu-id="0857a-177">With device management in Azure AD, you can:</span></span> 

- <span data-ttu-id="0857a-178">упростить процесс ввода устройств под управление Azure AD;</span><span class="sxs-lookup"><span data-stu-id="0857a-178">Simplify the process of bringing devices under the control of Azure AD</span></span>

- <span data-ttu-id="0857a-179">предоставить пользователям простой доступ к облачным ресурсам организации.</span><span class="sxs-lookup"><span data-stu-id="0857a-179">Provide your users with an easy to use access to your organization’s cloud-based resources</span></span>

<span data-ttu-id="0857a-180">Как показывает опыт, необходимо использовать следующие устройства:</span><span class="sxs-lookup"><span data-stu-id="0857a-180">As a rule of a thumb, you should use:</span></span>

- <span data-ttu-id="0857a-181">устройства, зарегистрированные в Azure AD, для личных устройств;</span><span class="sxs-lookup"><span data-stu-id="0857a-181">Azure AD registered devices for personal devices</span></span>

- <span data-ttu-id="0857a-182">устройства, присоединенные к Azure AD, для устройств, которые не присоединены к локальной службе Azure AD;</span><span class="sxs-lookup"><span data-stu-id="0857a-182">Azure AD joined devices for devices that are not joined to an on-premises AD</span></span> 

- <span data-ttu-id="0857a-183">гибридные устройства, присоединенные к Azure AD, для устройств, которые присоединены к локальной службе AD.</span><span class="sxs-lookup"><span data-stu-id="0857a-183">Hybrid Azure AD joined devices for devices that are joined to an on-premises AD</span></span>     




## <a name="next-steps"></a><span data-ttu-id="0857a-184">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0857a-184">Next steps</span></span>

- <span data-ttu-id="0857a-185">Чтобы получить общие сведения о том, как управлять устройствами на портале Azure, см. раздел [Управление устройствами с помощью портала Azure (предварительная версия)](device-management-azure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="0857a-185">To get an overview of how to manage device in the Azure portal, see [managing devices using the Azure portal](device-management-azure-portal.md)</span></span>

- <span data-ttu-id="0857a-186">Дополнительные сведения об условном доступе на основе устройств см. в статье [Настройка политики условного доступа на основе устройств для подключенных к Azure Active Directory приложений](active-directory-conditional-access-policy-connected-applications.md).</span><span class="sxs-lookup"><span data-stu-id="0857a-186">To learn more about device-based conditional access, see [configure Azure Active Directory device-based conditional access policies](active-directory-conditional-access-policy-connected-applications.md).</span></span>

- <span data-ttu-id="0857a-187">Сведения о настройке гибридных устройств, присоединенных к Azure AD, см. в статье [о том, как настроить гибридные устройства, присоединенные к Azure Active Directory](device-management-hybrid-azuread-joined-devices-setup.md).</span><span class="sxs-lookup"><span data-stu-id="0857a-187">To setup hybrid Azure AD joined devices, see [how to configure hybrid Azure Active Directory joined devices](device-management-hybrid-azuread-joined-devices-setup.md).</span></span>


