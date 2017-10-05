---
title: "Устранение неполадок автоматической регистрации присоединенных к домену Azure AD компьютеров для Windows 10 и Windows Server 2016 | Документация Майкрософт"
description: "Устранение неполадок автоматической регистрации присоединенных к домену Azure AD компьютеров для Windows 10 и Windows Server 2016."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: cdc25576-37f2-4afb-a786-f59ba4c284c2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 5b7f95f302f716d9221b5fae59aa2df5c956a524
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshooting-auto-registration-of-domain-joined-computers-to-azure-ad--windows-10-and-windows-server-2016"></a><span data-ttu-id="2e016-103">Устранение неполадок автоматической регистрации присоединенных к домену Azure AD компьютеров для Windows 10 и Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="2e016-103">Troubleshooting auto-registration of domain joined computers to Azure AD – Windows 10 and Windows Server 2016</span></span>

<span data-ttu-id="2e016-104">Это руководство касается следующих клиентов:</span><span class="sxs-lookup"><span data-stu-id="2e016-104">This topic is applicable to the following clients:</span></span>

-   <span data-ttu-id="2e016-105">Windows 10</span><span class="sxs-lookup"><span data-stu-id="2e016-105">Windows 10</span></span>
-   <span data-ttu-id="2e016-106">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="2e016-106">Windows Server 2016</span></span>

<span data-ttu-id="2e016-107">Сведения о других клиентах Windows см. в статье [Устранение неполадок автоматической регистрации присоединенных к домену Azure AD компьютеров для клиентов Windows нижнего уровня](active-directory-device-registration-troubleshoot-windows-legacy.md).</span><span class="sxs-lookup"><span data-stu-id="2e016-107">For other Windows clients, see [Troubleshooting auto-registration of domain joined computers to Azure AD for Windows down-level clients](active-directory-device-registration-troubleshoot-windows-legacy.md).</span></span>

<span data-ttu-id="2e016-108">В этом руководстве предполагается, что вы [настроили автоматическую регистрацию присоединенных к домену устройств Windows в Azure Active Directory](active-directory-device-registration-get-started.md) для выполнения следующих сценариев:</span><span class="sxs-lookup"><span data-stu-id="2e016-108">This topic assumes that you have configured auto-registration of domain-joined devices as outlined in described in [How to configure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-device-registration-get-started.md) to support the following scenarios:</span></span>

- [<span data-ttu-id="2e016-109">Условный доступ на основе устройств</span><span class="sxs-lookup"><span data-stu-id="2e016-109">Device-based conditional access</span></span>](active-directory-conditional-access-automatic-device-registration-setup.md)

- [<span data-ttu-id="2e016-110">Корпоративное перемещение параметров</span><span class="sxs-lookup"><span data-stu-id="2e016-110">Enterprise roaming of settings</span></span>](active-directory-windows-enterprise-state-roaming-overview.md)

- [<span data-ttu-id="2e016-111">Настройка Windows Hello для бизнеса</span><span class="sxs-lookup"><span data-stu-id="2e016-111">Windows Hello for Business</span></span>](active-directory-azureadjoin-passport-deployment.md)


<span data-ttu-id="2e016-112">Этот документ содержит рекомендации по устранению неполадок для устранения потенциальных проблем.</span><span class="sxs-lookup"><span data-stu-id="2e016-112">This document provides troubleshooting guidance on how to resolve potential issues.</span></span> 

<span data-ttu-id="2e016-113">Регистрация поддерживается в обновлении Windows 10 от ноября 2015 г. и в более поздних обновлениях.</span><span class="sxs-lookup"><span data-stu-id="2e016-113">The registration is supported in the Windows 10 November 2015 Update and above.</span></span>  
<span data-ttu-id="2e016-114">Чтобы выполнить приведенные выше сценарии, мы рекомендуем использовать юбилейное обновление.</span><span class="sxs-lookup"><span data-stu-id="2e016-114">We recommend using the Anniversary Update for enabling the scenarios above.</span></span>

## <a name="step-1-retrieve-the-registration-status"></a><span data-ttu-id="2e016-115">Шаг 1. Получение сведений о состоянии регистрации</span><span class="sxs-lookup"><span data-stu-id="2e016-115">Step 1: Retrieve the registration status</span></span> 

<span data-ttu-id="2e016-116">**Чтобы получить сведения о состоянии регистрации, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="2e016-116">**To retrieve the registration status:**</span></span>

1. <span data-ttu-id="2e016-117">Запустите командную строку от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="2e016-117">Open the command prompt as an administrator.</span></span>

2. <span data-ttu-id="2e016-118">Введите **dsregcmd/status**.</span><span class="sxs-lookup"><span data-stu-id="2e016-118">Type **dsregcmd /status**</span></span>



    <span data-ttu-id="2e016-119">+----------------------------------------------------------------------+
    | Состояние устройства                                                         |  +----------------------------------------------------------------------+</span><span class="sxs-lookup"><span data-stu-id="2e016-119">+----------------------------------------------------------------------+
    | Device State                                                         |  +----------------------------------------------------------------------+</span></span>
    
        AzureAdJoined : YES
     <span data-ttu-id="2e016-120">EnterpriseJoined : NO DeviceId : 5820fbe9-60c8-43b0-bb11-44aee233e4e7 Thumbprint : B753A6679CE720451921302CA873794D94C6204A KeyContainerId : bae6a60b-1d2f-4d2a-a298-33385f6d05e9 KeyProvider : Microsoft Platform Crypto Provider TpmProtected : YES KeySignTest: : MUST Run elevated to test.</span><span class="sxs-lookup"><span data-stu-id="2e016-120">EnterpriseJoined : NO DeviceId : 5820fbe9-60c8-43b0-bb11-44aee233e4e7 Thumbprint : B753A6679CE720451921302CA873794D94C6204A KeyContainerId : bae6a60b-1d2f-4d2a-a298-33385f6d05e9 KeyProvider : Microsoft Platform Crypto Provider TpmProtected : YES KeySignTest: : MUST Run elevated to test.</span></span>
                  <span data-ttu-id="2e016-121">Idp : login.windows.net TenantId : 72b988bf-86f1-41af-91ab-2d7cd011db47 TenantName : Contoso AuthCodeUrl : https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/authorize AccessTokenUrl : https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/token MdmUrl : https://enrollment.manage-beta.microsoft.com/EnrollmentServer/Discovery.svc MdmTouUrl : https://portal.manage-beta.microsoft.com/TermsOfUse.aspx dmComplianceUrl : https://portal.manage-beta.microsoft.com/?portalAction=Compliance SettingsUrl : eyJVcmlzIjpbImh0dHBzOi8va2FpbGFuaS5vbmUubWljcm9zb2Z0LmNvbS8iLCJodHRwczovL2thaWxhbmkxLm9uZS5taWNyb3NvZnQuY29tLyJdfQ== JoinSrvVersion : 1.0 JoinSrvUrl : https://enterpriseregistration.windows.net/EnrollmentServer/device/ JoinSrvId : urn:ms-drs:enterpriseregistration.windows.net KeySrvVersion : 1.0 KeySrvUrl : https://enterpriseregistration.windows.net/EnrollmentServer/key/ KeySrvId : urn:ms-drs:enterpriseregistration.windows.net DomainJoined : YES DomainName : CONTOSO</span><span class="sxs-lookup"><span data-stu-id="2e016-121">Idp : login.windows.net TenantId : 72b988bf-86f1-41af-91ab-2d7cd011db47 TenantName : Contoso AuthCodeUrl : https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/authorize AccessTokenUrl : https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/token MdmUrl : https://enrollment.manage-beta.microsoft.com/EnrollmentServer/Discovery.svc MdmTouUrl : https://portal.manage-beta.microsoft.com/TermsOfUse.aspx dmComplianceUrl : https://portal.manage-beta.microsoft.com/?portalAction=Compliance SettingsUrl : eyJVcmlzIjpbImh0dHBzOi8va2FpbGFuaS5vbmUubWljcm9zb2Z0LmNvbS8iLCJodHRwczovL2thaWxhbmkxLm9uZS5taWNyb3NvZnQuY29tLyJdfQ== JoinSrvVersion : 1.0 JoinSrvUrl : https://enterpriseregistration.windows.net/EnrollmentServer/device/ JoinSrvId : urn:ms-drs:enterpriseregistration.windows.net KeySrvVersion : 1.0 KeySrvUrl : https://enterpriseregistration.windows.net/EnrollmentServer/key/ KeySrvId : urn:ms-drs:enterpriseregistration.windows.net DomainJoined : YES DomainName : CONTOSO</span></span>
    
    <span data-ttu-id="2e016-122">+----------------------------------------------------------------------+
    | Состояние пользователя                                                           |  +----------------------------------------------------------------------+</span><span class="sxs-lookup"><span data-stu-id="2e016-122">+----------------------------------------------------------------------+
    | User State                                                           |  +----------------------------------------------------------------------+</span></span>
    
                 NgcSet : YES
               NgcKeyId : {C7A9AEDC-780E-4FDA-B200-1AE15561A46B}
        WorkplaceJoined : NO
          WamDefaultSet : YES
    <span data-ttu-id="2e016-123">WamDefaultAuthority : organizations         WamDefaultId : https://login.microsoft.com       WamDefaultGUID : {B16898C6-A148-4967-9171-64D755DA8520} (AzureAd)           AzureAdPrt : YES</span><span class="sxs-lookup"><span data-stu-id="2e016-123">WamDefaultAuthority : organizations         WamDefaultId : https://login.microsoft.com       WamDefaultGUID : {B16898C6-A148-4967-9171-64D755DA8520} (AzureAd)           AzureAdPrt : YES</span></span>



## <a name="step-2-evaluate-the-registration-status"></a><span data-ttu-id="2e016-124">Шаг 2. Анализ сведений о состоянии регистрации</span><span class="sxs-lookup"><span data-stu-id="2e016-124">Step 2: Evaluate the registration status</span></span> 

<span data-ttu-id="2e016-125">Просмотрите следующие поля и убедитесь, что для них заданы ожидаемые значения.</span><span class="sxs-lookup"><span data-stu-id="2e016-125">Review the following fields and make sure that they have the expected values:</span></span>

### <a name="azureadjoined--yes"></a><span data-ttu-id="2e016-126">AzureAdJoined: YES</span><span class="sxs-lookup"><span data-stu-id="2e016-126">AzureAdJoined : YES</span></span>  

<span data-ttu-id="2e016-127">Это поле показывает, зарегистрировано ли устройство в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2e016-127">This field shows whether the device is registered with Azure AD.</span></span> <span data-ttu-id="2e016-128">Если в поле отображается значение NO, то регистрация не завершена.</span><span class="sxs-lookup"><span data-stu-id="2e016-128">If the value shows as ‘NO’, registration has not completed.</span></span> 

<span data-ttu-id="2e016-129">**Возможные причины:**</span><span class="sxs-lookup"><span data-stu-id="2e016-129">**Possible causes:**</span></span>

- <span data-ttu-id="2e016-130">Произошла ошибка аутентификации для регистрации компьютера.</span><span class="sxs-lookup"><span data-stu-id="2e016-130">Authentication of the computer for registration failed.</span></span>

- <span data-ttu-id="2e016-131">Компьютер не может обнаружить прокси-сервер HTTP в организации.</span><span class="sxs-lookup"><span data-stu-id="2e016-131">There is an HTTP proxy in the organization that cannot be discovered by the computer</span></span>

- <span data-ttu-id="2e016-132">Компьютеру не удается получить доступ к Azure AD, чтобы пройти аутентификацию, или Azure DRS, чтобы пройти регистрацию.</span><span class="sxs-lookup"><span data-stu-id="2e016-132">The computer cannot reach Azure AD for authentication or Azure DRS for registration</span></span>

- <span data-ttu-id="2e016-133">Компьютер может быть не подключен к внутренней сети организации или к VPN в пределах "прямой видимости" локального контроллера домена AD.</span><span class="sxs-lookup"><span data-stu-id="2e016-133">The computer may not be on the organization’s internal network or on VPN with direct line of sight to an on-premises AD domain controller.</span></span>

- <span data-ttu-id="2e016-134">Доверенный платформенный модуль на компьютере может быть неисправен.</span><span class="sxs-lookup"><span data-stu-id="2e016-134">If the computer has a TPM, it may be in a bad state.</span></span>

- <span data-ttu-id="2e016-135">Службы, упомянутые в документе выше, могут быть неправильно настроены. Это понадобится перепроверить.</span><span class="sxs-lookup"><span data-stu-id="2e016-135">There may be a misconfiguration in services noted in the document earlier that you will need to verify again.</span></span> <span data-ttu-id="2e016-136">Ниже приведены распространенные примеры.</span><span class="sxs-lookup"><span data-stu-id="2e016-136">Common examples are:</span></span>

    - <span data-ttu-id="2e016-137">На сервере федерации нет включенных конечных точек WS-Trust.</span><span class="sxs-lookup"><span data-stu-id="2e016-137">Your federation server does not have WS-Trust endpoints enabled</span></span>

    - <span data-ttu-id="2e016-138">На сервере федерации может быть запрещена входящая аутентификация компьютеров в сети с использованием встроенной проверки подлинности Windows.</span><span class="sxs-lookup"><span data-stu-id="2e016-138">Your federation server may not allow inbound authentication from computers in your network using Integrated Windows Authentication.</span></span>

    - <span data-ttu-id="2e016-139">Нет объекта точки подключения службы, указывающего на имя проверенного домена в Azure AD в лесу AD, к которому относится компьютер.</span><span class="sxs-lookup"><span data-stu-id="2e016-139">There is no Service Connection Point object that points to your verified domain name in Azure AD in the AD forest where the computer belongs to</span></span>

---

### <a name="domainjoined--yes"></a><span data-ttu-id="2e016-140">DomainJoined: YES</span><span class="sxs-lookup"><span data-stu-id="2e016-140">DomainJoined : YES</span></span>  

<span data-ttu-id="2e016-141">Это поле показывает, присоединено ли устройство к локальному каталогу Active Directory или нет.</span><span class="sxs-lookup"><span data-stu-id="2e016-141">This field shows whether the device is joined to an on-premises Active Directory or not.</span></span> <span data-ttu-id="2e016-142">Устройство не сможет автоматически зарегистрироваться в Azure AD, если отображается значение **NO**.</span><span class="sxs-lookup"><span data-stu-id="2e016-142">If the value shows as **NO**, the device cannot auto-register with Azure AD.</span></span> <span data-ttu-id="2e016-143">Сначала проверьте, может ли устройство присоединиться к локальному каталогу Active Directory перед регистрацией в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2e016-143">Check first that the device joins to the on-premises Active Directory before it can register with Azure AD.</span></span> <span data-ttu-id="2e016-144">Узнайте о возможностях присоединения Azure Active Directory, если вы хотите присоединить компьютер к Azure AD напрямую.</span><span class="sxs-lookup"><span data-stu-id="2e016-144">If you are looking for joining the computer to Azure AD directly, please go to Learn about capabilities of Azure Active Directory Join.</span></span>

---

### <a name="workplacejoined--no"></a><span data-ttu-id="2e016-145">WorkplaceJoined: NO</span><span class="sxs-lookup"><span data-stu-id="2e016-145">WorkplaceJoined : NO</span></span>  

<span data-ttu-id="2e016-146">Это поле показывает, зарегистрировано ли устройство в Azure AD в качестве личного устройства (с пометкой "Присоединено к рабочей области").</span><span class="sxs-lookup"><span data-stu-id="2e016-146">This field shows whether the device is registered with Azure AD but as a personal device (marked as ‘Workplace Joined’).</span></span> <span data-ttu-id="2e016-147">Для присоединенного к домену компьютера, зарегистрированного в Azure AD, значение этого поля должно быть NO. Однако если отображается значение YES, это означает, что до выполнения регистрации компьютера была добавлена рабочая или учебная учетная запись.</span><span class="sxs-lookup"><span data-stu-id="2e016-147">If this value should show as ‘NO’ for a domain joined computer registered with Azure AD, however if it shows as YES it means that a work or school account was added prior to the computer completing registration.</span></span> <span data-ttu-id="2e016-148">В таком случае при использовании версии юбилейного обновления Windows 10 учетная запись будет игнорироваться (версия 1607 при выполнении команды WinVer в окне "Запуск" или в окне командной строки).</span><span class="sxs-lookup"><span data-stu-id="2e016-148">In this case the account will be ignored if using the Anniversary Update version of Windows 10 (1607 when running the WinVer command in the ‘Run’ window or a command prompt window).</span></span>

---

### <a name="wamdefaultset--yes-and-azureadprt--yes"></a><span data-ttu-id="2e016-149">WamDefaultSet: YES и AzureADPrt: YES</span><span class="sxs-lookup"><span data-stu-id="2e016-149">WamDefaultSet : YES and AzureADPrt : YES</span></span>
  
<span data-ttu-id="2e016-150">Эти поля показывают, что при входе в систему устройства пользователь успешно прошел аутентификацию в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2e016-150">These fields show that the user has successfully authenticated to Azure AD upon signing in to the device.</span></span> <span data-ttu-id="2e016-151">Ниже приведены возможные причины, по которым может отображаться значение NO.</span><span class="sxs-lookup"><span data-stu-id="2e016-151">If they show ‘NO’ the following are possible causes:</span></span>

- <span data-ttu-id="2e016-152">С устройством при регистрации был связан недопустимый ключ к хранилищу данных в доверенном платформенном модуле (проверьте KeySignTest во время работы с повышенными привилегиями).</span><span class="sxs-lookup"><span data-stu-id="2e016-152">Bad storage key (STK) in TPM associated with the device upon registration (check the KeySignTest while running elevated).</span></span>

- <span data-ttu-id="2e016-153">Наличие альтернативного имени пользователя.</span><span class="sxs-lookup"><span data-stu-id="2e016-153">Alternate Login ID</span></span>

- <span data-ttu-id="2e016-154">Прокси-сервер HTTP не найден.</span><span class="sxs-lookup"><span data-stu-id="2e016-154">HTTP Proxy not found</span></span>

## <a name="next-steps"></a><span data-ttu-id="2e016-155">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2e016-155">Next steps</span></span>

<span data-ttu-id="2e016-156">Дополнительные сведения см. в статье [Automatic device registration FAQ](active-directory-device-registration-faq.md) (Часто задаваемые вопросы об автоматической регистрации устройств)</span><span class="sxs-lookup"><span data-stu-id="2e016-156">For more information, see the [Automatic device registration FAQ](active-directory-device-registration-faq.md)</span></span> 