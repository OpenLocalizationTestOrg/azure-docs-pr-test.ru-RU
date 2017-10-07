---
title: "Управление toodevice aaaIntroduction в Azure Active Directory | Документы Microsoft"
description: "Узнайте, как управление устройствами можно управлять tooget hello устройств, которые обращаются к ресурсам в вашей среде."
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
ms.openlocfilehash: e2fc0a3e8d00dc69cf01db9074e34427e396cfcf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toodevice-management-in-azure-active-directory"></a><span data-ttu-id="d8466-103">Управление toodevice введение в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d8466-103">Introduction toodevice management in Azure Active Directory</span></span>

<span data-ttu-id="d8466-104">В мире mobile сначала, облачный Azure Active Directory (Azure AD) позволяет-toodevices приложений и служб из любого места.</span><span class="sxs-lookup"><span data-stu-id="d8466-104">In a mobile-first, cloud-first world, Azure Active Directory (Azure AD) enables single sign-on toodevices, apps, and services from anywhere.</span></span> <span data-ttu-id="d8466-105">С широким распространением устройств — Bring Your Own устройства (BYOD), включая hello ИТ-специалистов, сталкиваются с две — не дать цели:</span><span class="sxs-lookup"><span data-stu-id="d8466-105">With hello proliferation of devices - including Bring Your Own Device (BYOD), IT professionals are faced with two opposing goals:</span></span>

- <span data-ttu-id="d8466-106">Поддержать производительность toobe конечным пользователям hello везде, где каждый раз, когда</span><span class="sxs-lookup"><span data-stu-id="d8466-106">Empower hello end users toobe productive wherever and whenever</span></span>
- <span data-ttu-id="d8466-107">Защита корпоративных ресурсов hello в любое время</span><span class="sxs-lookup"><span data-stu-id="d8466-107">Protect hello corporate assets at any time</span></span>

<span data-ttu-id="d8466-108">Через устройства ваши пользователи получат доступ tooyour корпоративными ресурсами.</span><span class="sxs-lookup"><span data-stu-id="d8466-108">Through devices, your users are getting access tooyour corporate assets.</span></span> <span data-ttu-id="d8466-109">tooprotect корпоративным ресурсам, как ИТ-администратору необходимо toohave управление этими устройствами.</span><span class="sxs-lookup"><span data-stu-id="d8466-109">tooprotect your corporate assets, as an IT administrator, you want toohave control over these devices.</span></span> <span data-ttu-id="d8466-110">Это позволяет убедиться, что ваш пользователи получают доступ к ресурсам с устройств, которые стандартов безопасности и соответствия требованиям toomake.</span><span class="sxs-lookup"><span data-stu-id="d8466-110">This enables you toomake sure that your users are accessing your resources from devices that meet your standards for security and compliance.</span></span> 

<span data-ttu-id="d8466-111">Управление устройствами также является основой hello [условного доступа на основе устройств](active-directory-conditional-access-policy-connected-applications.md).</span><span class="sxs-lookup"><span data-stu-id="d8466-111">Device management is also hello foundation for [device-based conditional access](active-directory-conditional-access-policy-connected-applications.md).</span></span> <span data-ttu-id="d8466-112">С помощью условного доступа на основе устройств можно гарантировать, что доступа tooresources в вашей среде возможна только с помощью доверенного устройства.</span><span class="sxs-lookup"><span data-stu-id="d8466-112">With device-based conditional access, you can ensure that access tooresources in your environment is only possible with trusted devices.</span></span>   

<span data-ttu-id="d8466-113">В этом разделе описывается, как работает управление устройствами в Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d8466-113">This topic explains how device management in Azure Active Directory works.</span></span>

## <a name="getting-devices-under-hello-control-of-azure-ad"></a><span data-ttu-id="d8466-114">Получение устройств под управлением hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="d8466-114">Getting devices under hello control of Azure AD</span></span>

<span data-ttu-id="d8466-115">tooget устройства под управлением hello Azure AD, у вас есть два варианта:</span><span class="sxs-lookup"><span data-stu-id="d8466-115">tooget a device under hello control of Azure AD, you have two options:</span></span>

- <span data-ttu-id="d8466-116">Регистрация</span><span class="sxs-lookup"><span data-stu-id="d8466-116">Registering</span></span> 
- <span data-ttu-id="d8466-117">Присоединение</span><span class="sxs-lookup"><span data-stu-id="d8466-117">Joining</span></span>

<span data-ttu-id="d8466-118">**Регистрация** устройства tooAzure AD позволяет вам toomanage удостоверения устройства.</span><span class="sxs-lookup"><span data-stu-id="d8466-118">**Registering** a device tooAzure AD enables you toomanage a device’s identity.</span></span> <span data-ttu-id="d8466-119">При регистрации устройства регистрации устройств Azure AD предоставляет hello устройств с удостоверением, которое является устройством hello tooauthenticate используется, когда пользователь выполняет вход tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="d8466-119">When a device is registered, Azure AD device registration provides hello device with an identity that is used tooauthenticate hello device when a user signs-in tooAzure AD.</span></span> <span data-ttu-id="d8466-120">Можно использовать удостоверение tooenable hello или отключить устройство.</span><span class="sxs-lookup"><span data-stu-id="d8466-120">You can use hello identity tooenable or disable a device.</span></span>

<span data-ttu-id="d8466-121">В сочетании с мобильными устройствами management(MDM) например Microsoft Intune, с дополнительными сведениями об устройстве hello обновляются hello атрибуты устройства в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d8466-121">When combined with a mobile device management(MDM) solution such as Microsoft Intune, hello device attributes in Azure AD are updated with additional information about hello device.</span></span> <span data-ttu-id="d8466-122">Это позволяет вам toocreate правила условного доступа, которые осуществляют доступ к устройствам toomeet стандартов безопасности и соответствия требованиям.</span><span class="sxs-lookup"><span data-stu-id="d8466-122">This allows you toocreate conditional access rules that enforce access from devices toomeet your standards for security and compliance.</span></span> <span data-ttu-id="d8466-123">Дополнительные сведения о регистрации устройств в Microsoft Intune см. в статье "Регистрация устройств для управления в Intune".</span><span class="sxs-lookup"><span data-stu-id="d8466-123">For more information on enrolling devices in Microsoft Intune, see Enroll devices for management in Intune .</span></span>

<span data-ttu-id="d8466-124">**Присоединение** устройство является расширение tooregistering устройства.</span><span class="sxs-lookup"><span data-stu-id="d8466-124">**Joining** a device is an extension tooregistering a device.</span></span> <span data-ttu-id="d8466-125">Это значит, он предоставляет все hello преимущества регистрации устройства, а в toothis сложения, он также изменяет hello локальное состояние устройства.</span><span class="sxs-lookup"><span data-stu-id="d8466-125">This means, it provides you with all hello benefits of registering a device and in addition toothis, it also changes hello local state of a device.</span></span> <span data-ttu-id="d8466-126">Изменение локального состояния hello позволяет устройства в toosign tooa пользователей вместо личную учетную запись организации рабочая учетная.</span><span class="sxs-lookup"><span data-stu-id="d8466-126">Changing hello local state enables your users toosign-in tooa device using an organizational work or school account instead of a personal account.</span></span>

## <a name="azure-ad-registered-devices"></a><span data-ttu-id="d8466-127">Устройства, зарегистрированные в Azure AD</span><span class="sxs-lookup"><span data-stu-id="d8466-127">Azure AD registered devices</span></span>   

<span data-ttu-id="d8466-128">Hello цель устройств Azure AD зарегистрирован — с поддерживаются hello tooprovide **Bring Your Own устройства (BYOD)** сценария.</span><span class="sxs-lookup"><span data-stu-id="d8466-128">hello goal of Azure AD registered devices is tooprovide you with support for hello **Bring Your Own Device (BYOD)** scenario.</span></span> <span data-ttu-id="d8466-129">В этом случае пользователь может обращаться к корпоративным ресурсам под контролем Azure Active Directory с помощью личного устройства.</span><span class="sxs-lookup"><span data-stu-id="d8466-129">In this scenario, a user can access your organization’s Azure Active Directory controlled resources using a personal device.</span></span>  

![Устройства, зарегистрированные в Azure AD](./media/device-management-introduction/03.png)

<span data-ttu-id="d8466-131">Hello доступ основан на рабочей или учебной учетной записи, которое было введено на устройстве hello.</span><span class="sxs-lookup"><span data-stu-id="d8466-131">hello access is based on a work or school account that has been entered on hello device.</span></span>  
<span data-ttu-id="d8466-132">Например Windows 10 позволяет пользователям tooadd работы или учебную учетную запись tooa персонального компьютера, планшета или телефона.</span><span class="sxs-lookup"><span data-stu-id="d8466-132">For example, Windows 10 enables users tooadd a work or school account tooa personal computer, tablet, or phone.</span></span>  
<span data-ttu-id="d8466-133">При добавлении пользователем рабочую или учебную учетную запись, hello устройство зарегистрировано в Azure AD и при необходимости зарегистрировано в системе управления (MDM) мобильных устройств hello, который настроен в вашей организации.</span><span class="sxs-lookup"><span data-stu-id="d8466-133">When a user has added a work or school account, hello device is registered with Azure AD and optionally enrolled in hello mobile device management (MDM) system that your organization has configured.</span></span> <span data-ttu-id="d8466-134">Пользователи в вашей организации можно добавить рабочий или удобно рабочей учетной записи tooa личного устройства:</span><span class="sxs-lookup"><span data-stu-id="d8466-134">Your organization’s users can add a work or school account tooa personal device conveniently:</span></span>

- <span data-ttu-id="d8466-135">При доступе к рабочих приложений для hello первый раз</span><span class="sxs-lookup"><span data-stu-id="d8466-135">When accessing a work application for hello first time</span></span>
- <span data-ttu-id="d8466-136">Вручную через hello **параметры** меню в случае hello Windows 10</span><span class="sxs-lookup"><span data-stu-id="d8466-136">Manually via hello **Settings** menu in hello case of Windows 10</span></span> 

<span data-ttu-id="d8466-137">Устройства, зарегистрированные в Azure AD, можно настроить для Windows 10, iOS, Android и macOS.</span><span class="sxs-lookup"><span data-stu-id="d8466-137">You can configure Azure AD registered devices for Windows 10, iOS, Android and macOS.</span></span>

## <a name="azure-ad-joined-devices"></a><span data-ttu-id="d8466-138">Устройства, присоединенные к Azure AD</span><span class="sxs-lookup"><span data-stu-id="d8466-138">Azure AD joined devices</span></span>

<span data-ttu-id="d8466-139">Задача Hello Azure AD объединить устройств — toosimplify:</span><span class="sxs-lookup"><span data-stu-id="d8466-139">hello goal of Azure AD joined devices is toosimplify:</span></span>

- <span data-ttu-id="d8466-140">развертывание Windows на корпоративных устройствах;</span><span class="sxs-lookup"><span data-stu-id="d8466-140">Windows deployments of work-owned devices</span></span> 
- <span data-ttu-id="d8466-141">Доступ tooorganizational приложениям и ресурсам с любого устройства Windows</span><span class="sxs-lookup"><span data-stu-id="d8466-141">Access tooorganizational apps and resources from any Windows device</span></span>

![Устройства, зарегистрированные в Azure AD](./media/device-management-introduction/02.png)


<span data-ttu-id="d8466-143">Эти задачи выполняются посредством предоставление пользователям возможности самообслуживания для получения работы устройства под управлением hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d8466-143">These goals are accomplished by providing your users with a self-service experience for getting work-owned devices under hello control of Azure AD.</span></span>  
<span data-ttu-id="d8466-144">**Присоединение к Azure AD** предназначено для организаций, в которых мобильные устройства и облачные технологии стоят на первом месте.</span><span class="sxs-lookup"><span data-stu-id="d8466-144">**Azure AD Join** is intended for organizations that are cloud-first / cloud-only.</span></span> <span data-ttu-id="d8466-145">Обычно это предприятия малого и среднего бизнеса, у которых нет локальной инфраструктуры Windows Server Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d8466-145">These are typically small- and medium-sized businesses that do not have an on-premises Windows Server Active Directory infrastructure.</span></span> 

<span data-ttu-id="d8466-146">Реализация устройства присоединены Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="d8466-146">Implementing Azure AD joined devices provides you with hello following benefits:</span></span>

- <span data-ttu-id="d8466-147">**Единый вход (SSO)** tooyour Azure управляемых приложений SaaS и служб.</span><span class="sxs-lookup"><span data-stu-id="d8466-147">**Single-Sign-On (SSO)** tooyour Azure managed SaaS apps and services.</span></span> <span data-ttu-id="d8466-148">При доступе к рабочим ресурсам пользователи не видят запросов на дополнительную проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="d8466-148">Your users don’t see additional authentication prompts when accessing work resources.</span></span> <span data-ttu-id="d8466-149">Hello функциональные возможности единого входа — даже если они не являются подключенных toohello доменной сети доступны.</span><span class="sxs-lookup"><span data-stu-id="d8466-149">hello SSO functionality is even when they are not connected toohello domain network available.</span></span>

- <span data-ttu-id="d8466-150">**Перенос** пользовательских параметров между устройствами с поддержкой рабочих или учебных учетных записей (с соблюдением корпоративных требований).</span><span class="sxs-lookup"><span data-stu-id="d8466-150">**Enterprise compliant roaming** of user settings across joined devices.</span></span> <span data-ttu-id="d8466-151">Пользователи не должны tooconnect параметры toosee учетной записи (например, Hotmail) Microsoft на устройствах.</span><span class="sxs-lookup"><span data-stu-id="d8466-151">Users don’t need tooconnect a Microsoft account (for example, Hotmail) toosee settings across devices.</span></span>

- <span data-ttu-id="d8466-152">**Доступ tooWindows магазин для бизнеса** с помощью учетной записи AD.</span><span class="sxs-lookup"><span data-stu-id="d8466-152">**Access tooWindows Store for Business** using AD account.</span></span> <span data-ttu-id="d8466-153">Пользователи смогут выбирать из инвентаризацию организации hello предварительно выбранных приложений.</span><span class="sxs-lookup"><span data-stu-id="d8466-153">Your users can choose from an inventory of applications pre-selected by hello organization.</span></span>

- <span data-ttu-id="d8466-154">**Windows Hello** поддержка ресурсов toowork удобный и безопасный доступ.</span><span class="sxs-lookup"><span data-stu-id="d8466-154">**Windows Hello** support for secure and convenient access toowork resources.</span></span>

- <span data-ttu-id="d8466-155">**Ограничение доступа** tooapps только те устройства, которые соответствуют политике соответствия.</span><span class="sxs-lookup"><span data-stu-id="d8466-155">**Restriction of access** tooapps from only devices that meet compliance policy.</span></span>

<span data-ttu-id="d8466-156">Несмотря на то, что присоединение к Azure AD в первую очередь предназначено для организаций, у которых нет локальной инфраструктуры Windows Server Active Directory, его, безусловно, можно использовать в следующих сценариях:</span><span class="sxs-lookup"><span data-stu-id="d8466-156">While Azure AD join is primarily intended for organizations that do not have an on-premises Windows Server Active Directory infrastructure, you can certainly also use it in scenarios where:</span></span>

- <span data-ttu-id="d8466-157">Нельзя использовать присоединения к домену локального к примеру, если вам нужна tooget мобильных устройств, таких как планшеты и телефоны под управлением.</span><span class="sxs-lookup"><span data-stu-id="d8466-157">You can’t use an on-premises domain join, for example, if you need tooget mobile devices such as tablets and phones under control.</span></span>

- <span data-ttu-id="d8466-158">Вашим пользователям в первую очередь требуется tooaccess Office 365 или другими приложениями SaaS, интегрированных с Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d8466-158">Your users primarily need tooaccess Office 365 or other SaaS apps integrated with Azure AD.</span></span>

- <span data-ttu-id="d8466-159">Требуется toomanage группы пользователей в Azure AD, а не в Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d8466-159">You want toomanage a group of users in Azure AD instead of in Active Directory.</span></span> <span data-ttu-id="d8466-160">Они могут применяться, например, tooseasonal сотрудников, подрядчиков или учащихся.</span><span class="sxs-lookup"><span data-stu-id="d8466-160">This can apply, for example, tooseasonal workers, contractors, or students.</span></span>

- <span data-ttu-id="d8466-161">Вы хотите tooprovide присоединяемый tooworkers возможности в удаленных офисах филиалов с ограниченной локальной инфраструктуры.</span><span class="sxs-lookup"><span data-stu-id="d8466-161">You want tooprovide joining capabilities tooworkers in remote branch offices with limited on-premises infrastructure.</span></span>

<span data-ttu-id="d8466-162">Можно настроить устройства, присоединенные к Azure AD, для устройств Windows 10.</span><span class="sxs-lookup"><span data-stu-id="d8466-162">You can configure Azure AD joined devices for Windows 10 devices.</span></span>


## <a name="hybrid-azure-ad-joined-devices"></a><span data-ttu-id="d8466-163">Гибридные устройства, присоединенные к Azure AD</span><span class="sxs-lookup"><span data-stu-id="d8466-163">Hybrid Azure AD joined devices</span></span>

<span data-ttu-id="d8466-164">Для более десяти лет во многих организациях использовали hello домена соединения tootheir в локальной среде Active Directory tooenable:</span><span class="sxs-lookup"><span data-stu-id="d8466-164">For more than a decade, many organizations have used hello domain join tootheir on-premises Active Directory tooenable:</span></span>

- <span data-ttu-id="d8466-165">ИТ отделы toomanage работы устройства из центрального расположения.</span><span class="sxs-lookup"><span data-stu-id="d8466-165">IT departments toomanage work-owned devices from a central location.</span></span>

- <span data-ttu-id="d8466-166">Пользователи toosign tootheir устройств с их Active Directory рабочая или учебная учетные записи.</span><span class="sxs-lookup"><span data-stu-id="d8466-166">Users toosign in tootheir devices with their Active Directory work or school accounts.</span></span> 

<span data-ttu-id="d8466-167">Как правило, организации с локально занимаемое место рассчитывать на устройства tooprovision методы обработки изображений и часто используют **System Center Configuration Manager (SCCM)** или **Групповая политика (GP)** toomanage их.</span><span class="sxs-lookup"><span data-stu-id="d8466-167">Typically, organizations with an on-premises footprint rely on imaging methods tooprovision devices, and they often use **System Center Configuration Manager (SCCM)** or **group policy (GP)** toomanage them.</span></span>

<span data-ttu-id="d8466-168">Если в локальной среде AD занимаемое место и также выгода от hello возможности, предоставляемые Azure Active Directory, можно реализовать гибридных устройств объединить Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d8466-168">If your environment has an on-premises AD footprint and you also want benefit from hello capabilities provided by Azure Active Directory, you can implement hybrid Azure AD joined devices.</span></span> <span data-ttu-id="d8466-169">Это устройства, которые также присутствуют, соединенных tooyour локальную Active Directory и Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d8466-169">These are devices that are both, joined tooyour on-premises Active Directory and your Azure Active Directory.</span></span>

![Устройства, зарегистрированные в Azure AD](./media/device-management-introduction/01.png)


<span data-ttu-id="d8466-171">Гибридные устройства, присоединенные к Azure AD, следует использовать в указанных далее случаях.</span><span class="sxs-lookup"><span data-stu-id="d8466-171">You should use Azure AD hybrid joined devices if:</span></span>

- <span data-ttu-id="d8466-172">У вас устройств развернутой toothese приложений Win32, использующими NTLM или Kerberos.</span><span class="sxs-lookup"><span data-stu-id="d8466-172">You have Win32 apps deployed toothese devices that use NTLM / Kerberos.</span></span>

- <span data-ttu-id="d8466-173">Требуется групповой Политики или SCCM / DCM toomanage устройств.</span><span class="sxs-lookup"><span data-stu-id="d8466-173">You require GP or SCCM / DCM toomanage devices.</span></span>

- <span data-ttu-id="d8466-174">Требуется toocontinue toouse обработки изображений решения tooconfigure устройств для ваших сотрудников.</span><span class="sxs-lookup"><span data-stu-id="d8466-174">You want toocontinue toouse imaging solutions tooconfigure devices for your employees.</span></span>

<span data-ttu-id="d8466-175">Можно настроить гибридные устройства, присоединенные к Azure AD, для устройств Windows 10 низкого уровня, например Windows 8 и Windows 7.</span><span class="sxs-lookup"><span data-stu-id="d8466-175">You can configure Hybrid Azure AD joined devices for Windows 10 and down-level devices such as Windows 8 and Windows 7.</span></span>

## <a name="summary"></a><span data-ttu-id="d8466-176">Сводка</span><span class="sxs-lookup"><span data-stu-id="d8466-176">Summary</span></span>

<span data-ttu-id="d8466-177">Управление устройствами в Azure AD позволяет:</span><span class="sxs-lookup"><span data-stu-id="d8466-177">With device management in Azure AD, you can:</span></span> 

- <span data-ttu-id="d8466-178">Упростить процесс hello объединения устройств под управлением hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="d8466-178">Simplify hello process of bringing devices under hello control of Azure AD</span></span>

- <span data-ttu-id="d8466-179">Предоставлять пользователям организации легко toouse доступа tooyour облачные ресурсы</span><span class="sxs-lookup"><span data-stu-id="d8466-179">Provide your users with an easy toouse access tooyour organization’s cloud-based resources</span></span>

<span data-ttu-id="d8466-180">Как показывает опыт, необходимо использовать следующие устройства:</span><span class="sxs-lookup"><span data-stu-id="d8466-180">As a rule of a thumb, you should use:</span></span>

- <span data-ttu-id="d8466-181">устройства, зарегистрированные в Azure AD, для личных устройств;</span><span class="sxs-lookup"><span data-stu-id="d8466-181">Azure AD registered devices for personal devices</span></span>

- <span data-ttu-id="d8466-182">Устройств, присоединенных к Azure AD, для устройств, не присоединенных к tooan локальной AD</span><span class="sxs-lookup"><span data-stu-id="d8466-182">Azure AD joined devices for devices that are not joined tooan on-premises AD</span></span> 

- <span data-ttu-id="d8466-183">Устройств, присоединенных к гибридной Azure AD, для устройств, присоединенных к tooan локальной AD</span><span class="sxs-lookup"><span data-stu-id="d8466-183">Hybrid Azure AD joined devices for devices that are joined tooan on-premises AD</span></span>     




## <a name="next-steps"></a><span data-ttu-id="d8466-184">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d8466-184">Next steps</span></span>

- <span data-ttu-id="d8466-185">Общие сведения о том, как устройство toomanage в hello Azure портала, см. в разделе tooget [управление устройствами с помощью портала Azure hello](device-management-azure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="d8466-185">tooget an overview of how toomanage device in hello Azure portal, see [managing devices using hello Azure portal](device-management-azure-portal.md)</span></span>

- <span data-ttu-id="d8466-186">toolearn Дополнительные сведения о условного доступа на основе устройств, в разделе [настройки политик условного доступа на основе устройств Azure Active Directory](active-directory-conditional-access-policy-connected-applications.md).</span><span class="sxs-lookup"><span data-stu-id="d8466-186">toolearn more about device-based conditional access, see [configure Azure Active Directory device-based conditional access policies](active-directory-conditional-access-policy-connected-applications.md).</span></span>

- <span data-ttu-id="d8466-187">toosetup гибридных Azure AD объединить устройства, см. [как tooconfigure гибридной Azure Active Directory устройств, присоединенных к](device-management-hybrid-azuread-joined-devices-setup.md).</span><span class="sxs-lookup"><span data-stu-id="d8466-187">toosetup hybrid Azure AD joined devices, see [how tooconfigure hybrid Azure Active Directory joined devices](device-management-hybrid-azuread-joined-devices-setup.md).</span></span>


