---
title: "Windows 10 и Windows Server 2016 устройств, присоединенных к aaaTroubleshooting гибридной Azure Active Directory | Документы Microsoft"
description: "Устранение неполадок на устройствах под управлением Windows 10 и Windows Server 2016 с гибридным присоединением к Azure Active Directory ."
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
ms.date: 08/17/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: cc252d1d0684d6632694afc8a367327794228c19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-hybrid-azure-active-directory-joined-windows-10-and-windows-server-2016-devices"></a><span data-ttu-id="71a66-103">Устранение неполадок на устройствах под управлением Windows 10 и Windows Server 2016 с гибридным присоединением к Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="71a66-103">Troubleshooting hybrid Azure Active Directory joined Windows 10 and Windows Server 2016 devices</span></span> 

<span data-ttu-id="71a66-104">Этот раздел является применимо toohello следующих клиентов:</span><span class="sxs-lookup"><span data-stu-id="71a66-104">This topic is applicable toohello following clients:</span></span>

-   <span data-ttu-id="71a66-105">Windows 10</span><span class="sxs-lookup"><span data-stu-id="71a66-105">Windows 10</span></span>
-   <span data-ttu-id="71a66-106">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="71a66-106">Windows Server 2016</span></span>

<span data-ttu-id="71a66-107">Сведения о других клиентах Windows см. в статье [Troubleshooting hybrid Azure Active Directory joined down-level devices](device-management-troubleshoot-hybrid-join-windows-legacy.md) (Устранение неполадок на устройствах нижнего уровня с гибридным присоединением к Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="71a66-107">For other Windows clients, see [Troubleshooting hybrid Azure Active Directory joined down-level devices](device-management-troubleshoot-hybrid-join-windows-legacy.md).</span></span>

<span data-ttu-id="71a66-108">В этом разделе предполагается, что [устройств, присоединенных к настроенным гибридной Azure Active Directory](device-management-hybrid-azuread-joined-devices-setup.md) toosupport hello следующие сценарии:</span><span class="sxs-lookup"><span data-stu-id="71a66-108">This topic assumes that you have [configured hybrid Azure Active Directory joined devices](device-management-hybrid-azuread-joined-devices-setup.md) toosupport hello following scenarios:</span></span>

- <span data-ttu-id="71a66-109">Условный доступ на основе устройств</span><span class="sxs-lookup"><span data-stu-id="71a66-109">Device-based conditional access</span></span>

- [<span data-ttu-id="71a66-110">Корпоративное перемещение параметров</span><span class="sxs-lookup"><span data-stu-id="71a66-110">Enterprise roaming of settings</span></span>](active-directory-windows-enterprise-state-roaming-overview.md)

- [<span data-ttu-id="71a66-111">Настройка Windows Hello для бизнеса</span><span class="sxs-lookup"><span data-stu-id="71a66-111">Windows Hello for Business</span></span>](active-directory-azureadjoin-passport-deployment.md)


<span data-ttu-id="71a66-112">В этом документе приведены инструкции по устранению как tooresolve потенциальные проблемы.</span><span class="sxs-lookup"><span data-stu-id="71a66-112">This document provides troubleshooting guidance on how tooresolve potential issues.</span></span> 


<span data-ttu-id="71a66-113">Для Windows 10 и Windows Server 2016, с помощью гибридного hello поддерживает соединения Azure Active Directory Windows 10 ноября 2015 г. обновление и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="71a66-113">For Windows 10 and Windows Server 2016, hybrid Azure Active Directory join supports hello Windows 10 November 2015 Update and above.</span></span> <span data-ttu-id="71a66-114">Мы рекомендуем использовать hello окончания действия обновления.</span><span class="sxs-lookup"><span data-stu-id="71a66-114">We recommend using hello Anniversary update.</span></span>

## <a name="step-1-retrieve-hello-join-status"></a><span data-ttu-id="71a66-115">Шаг 1: Получить состояние соединения hello</span><span class="sxs-lookup"><span data-stu-id="71a66-115">Step 1: Retrieve hello join status</span></span> 

<span data-ttu-id="71a66-116">**состояние соединения hello tooretrieve:**</span><span class="sxs-lookup"><span data-stu-id="71a66-116">**tooretrieve hello join status:**</span></span>

1. <span data-ttu-id="71a66-117">Привет открыть командную строку с правами администратора</span><span class="sxs-lookup"><span data-stu-id="71a66-117">Open hello command prompt as an administrator</span></span>

2. <span data-ttu-id="71a66-118">Введите **dsregcmd/status**.</span><span class="sxs-lookup"><span data-stu-id="71a66-118">Type **dsregcmd /status**</span></span>



    <span data-ttu-id="71a66-119">+----------------------------------------------------------------------+
    | Состояние устройства                                                         |  +----------------------------------------------------------------------+</span><span class="sxs-lookup"><span data-stu-id="71a66-119">+----------------------------------------------------------------------+
    | Device State                                                         |  +----------------------------------------------------------------------+</span></span>
    
        AzureAdJoined: YES
     <span data-ttu-id="71a66-120">EnterpriseJoined: Не DeviceId: 5820fbe9-60c8-43b0-bb11-44aee233e4e7 отпечаток: B753A6679CE720451921302CA873794D94C6204A KeyContainerId: bae6a60b-1d2f-4d2a-a298-33385f6d05e9 KeyProvider: TpmProtected поставщик криптографии Microsoft Platform: Да KeySignTest:: необходимо выполнить с повышенными привилегиями tootest.</span><span class="sxs-lookup"><span data-stu-id="71a66-120">EnterpriseJoined: NO DeviceId: 5820fbe9-60c8-43b0-bb11-44aee233e4e7 Thumbprint: B753A6679CE720451921302CA873794D94C6204A KeyContainerId: bae6a60b-1d2f-4d2a-a298-33385f6d05e9 KeyProvider: Microsoft Platform Crypto Provider TpmProtected: YES KeySignTest: : MUST Run elevated tootest.</span></span>
                  <span data-ttu-id="71a66-121">Idp: login.windows.net TenantId: 72b988bf-86f1-41af-91ab-2d7cd011db47 TenantName: Contoso AuthCodeUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/authorize AccessTokenUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/token MdmUrl: https://enrollment.manage-beta.microsoft.com/EnrollmentServer/Discovery.svc MdmTouUrl: https://portal.manage-beta.microsoft.com/TermsOfUse.aspx dmComplianceUrl: https://portal.manage-beta.microsoft.com/?portalAction=Compliance SettingsUrl: eyJVcmlzIjpbImh0dHBzOi8va2FpbGFuaS5vbmUubWljcm9zb2Z0LmNvbS8iLCJodHRwczovL2thaWxhbmkxLm9uZS5taWNyb3NvZnQuY29tLyJdfQ== JoinSrvVersion: 1.0 JoinSrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/device/ JoinSrvId: urn:ms-drs:enterpriseregistration.windows.net KeySrvVersion: 1.0 KeySrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/key/ KeySrvId: urn:ms-drs:enterpriseregistration.windows.net DomainJoined: YES DomainName: CONTOSO</span><span class="sxs-lookup"><span data-stu-id="71a66-121">Idp: login.windows.net TenantId: 72b988bf-86f1-41af-91ab-2d7cd011db47 TenantName: Contoso AuthCodeUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/authorize AccessTokenUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/token MdmUrl: https://enrollment.manage-beta.microsoft.com/EnrollmentServer/Discovery.svc MdmTouUrl: https://portal.manage-beta.microsoft.com/TermsOfUse.aspx dmComplianceUrl: https://portal.manage-beta.microsoft.com/?portalAction=Compliance SettingsUrl: eyJVcmlzIjpbImh0dHBzOi8va2FpbGFuaS5vbmUubWljcm9zb2Z0LmNvbS8iLCJodHRwczovL2thaWxhbmkxLm9uZS5taWNyb3NvZnQuY29tLyJdfQ== JoinSrvVersion: 1.0 JoinSrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/device/ JoinSrvId: urn:ms-drs:enterpriseregistration.windows.net KeySrvVersion: 1.0 KeySrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/key/ KeySrvId: urn:ms-drs:enterpriseregistration.windows.net DomainJoined: YES DomainName: CONTOSO</span></span>
    
    <span data-ttu-id="71a66-122">+----------------------------------------------------------------------+
    | Состояние пользователя                                                           |  +----------------------------------------------------------------------+</span><span class="sxs-lookup"><span data-stu-id="71a66-122">+----------------------------------------------------------------------+
    | User State                                                           |  +----------------------------------------------------------------------+</span></span>
    
                 NgcSet: YES
               NgcKeyId: {C7A9AEDC-780E-4FDA-B200-1AE15561A46B}
        WorkplaceJoined: NO
          WamDefaultSet: YES
    <span data-ttu-id="71a66-123">WamDefaultAuthority: organizations         WamDefaultId: https://login.microsoft.com       WamDefaultGUID: {B16898C6-A148-4967-9171-64D755DA8520} (AzureAd)           AzureAdPrt: YES</span><span class="sxs-lookup"><span data-stu-id="71a66-123">WamDefaultAuthority: organizations         WamDefaultId: https://login.microsoft.com       WamDefaultGUID: {B16898C6-A148-4967-9171-64D755DA8520} (AzureAd)           AzureAdPrt: YES</span></span>



## <a name="step-2-evaluate-hello-join-status"></a><span data-ttu-id="71a66-124">Шаг 2: Оценка hello состояние соединения</span><span class="sxs-lookup"><span data-stu-id="71a66-124">Step 2: Evaluate hello join status</span></span> 

<span data-ttu-id="71a66-125">Просмотрите следующие поля hello и убедитесь в том, что они имеют hello ожидаемые значения:</span><span class="sxs-lookup"><span data-stu-id="71a66-125">Review hello following fields and make sure that they have hello expected values:</span></span>

### <a name="azureadjoined--yes"></a><span data-ttu-id="71a66-126">AzureAdJoined: YES</span><span class="sxs-lookup"><span data-stu-id="71a66-126">AzureAdJoined : YES</span></span>  

<span data-ttu-id="71a66-127">Это поле указывает, присоединен ли hello устройства в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="71a66-127">This field indicates whether hello device is joined with Azure AD.</span></span> <span data-ttu-id="71a66-128">Если значение hello **нет**, hello tooAzure соединения AD еще не завершен.</span><span class="sxs-lookup"><span data-stu-id="71a66-128">If hello value is **NO**, hello join tooAzure AD has not completed yet.</span></span> 

<span data-ttu-id="71a66-129">**Возможные причины:**</span><span class="sxs-lookup"><span data-stu-id="71a66-129">**Possible causes:**</span></span>

- <span data-ttu-id="71a66-130">Ошибка проверки подлинности компьютера hello для соединения.</span><span class="sxs-lookup"><span data-stu-id="71a66-130">Authentication of hello computer for a join failed.</span></span>

- <span data-ttu-id="71a66-131">Есть прокси-сервер HTTP hello организации, которые не могут быть обнаружены на компьютере hello</span><span class="sxs-lookup"><span data-stu-id="71a66-131">There is an HTTP proxy in hello organization that cannot be discovered by hello computer</span></span>

- <span data-ttu-id="71a66-132">для регистрации компьютера Hello не могут достичь tooauthenticate Azure AD или Azure DRS</span><span class="sxs-lookup"><span data-stu-id="71a66-132">hello computer cannot reach Azure AD tooauthenticate or Azure DRS for registration</span></span>

- <span data-ttu-id="71a66-133">Hello компьютер может быть hello внутренней сети организации или VPN с tooan прямая линия видимости локального контроллера домена AD.</span><span class="sxs-lookup"><span data-stu-id="71a66-133">hello computer may not be on hello organization’s internal network or on VPN with direct line of sight tooan on-premises AD domain controller.</span></span>

- <span data-ttu-id="71a66-134">Если hello компьютера доверенным платформенным Модулем, он может быть в неверном состоянии.</span><span class="sxs-lookup"><span data-stu-id="71a66-134">If hello computer has a TPM, it can be in a bad state.</span></span>

- <span data-ttu-id="71a66-135">Может быть неправильной конфигурации в службах hello отмечалось в документе hello, которые понадобятся tooverify еще раз.</span><span class="sxs-lookup"><span data-stu-id="71a66-135">There might be a misconfiguration in hello services noted in hello document earlier that you will need tooverify again.</span></span> <span data-ttu-id="71a66-136">Ниже приведены распространенные примеры.</span><span class="sxs-lookup"><span data-stu-id="71a66-136">Common examples are:</span></span>

    - <span data-ttu-id="71a66-137">На сервере федерации нет включенных конечных точек WS-Trust.</span><span class="sxs-lookup"><span data-stu-id="71a66-137">Your federation server does not have WS-Trust endpoints enabled</span></span>

    - <span data-ttu-id="71a66-138">На сервере федерации может быть запрещена входящая аутентификация компьютеров в сети с использованием встроенной проверки подлинности Windows.</span><span class="sxs-lookup"><span data-stu-id="71a66-138">Your federation server does not allow inbound authentication from computers in your network using Integrated Windows Authentication.</span></span>

    - <span data-ttu-id="71a66-139">Нет объекта точки подключения службы, указывающий tooyour проверенное имя домена в Azure AD в лесу hello AD, которой принадлежит компьютер hello</span><span class="sxs-lookup"><span data-stu-id="71a66-139">There is no Service Connection Point object that points tooyour verified domain name in Azure AD in hello AD forest where hello computer belongs to</span></span>

---

### <a name="domainjoined--yes"></a><span data-ttu-id="71a66-140">DomainJoined: YES</span><span class="sxs-lookup"><span data-stu-id="71a66-140">DomainJoined : YES</span></span>  

<span data-ttu-id="71a66-141">Это поле указывает ли hello устройство присоединено tooan локальной Active Directory или нет.</span><span class="sxs-lookup"><span data-stu-id="71a66-141">This field indicates whether hello device is joined tooan on-premises Active Directory or not.</span></span> <span data-ttu-id="71a66-142">Если значение hello **нет**, hello устройства не может выполнить соединение гибридной Azure AD.</span><span class="sxs-lookup"><span data-stu-id="71a66-142">If hello value is **NO**, hello device cannot perform a hybrid Azure AD join.</span></span>  

---

### <a name="workplacejoined--no"></a><span data-ttu-id="71a66-143">WorkplaceJoined: NO</span><span class="sxs-lookup"><span data-stu-id="71a66-143">WorkplaceJoined : NO</span></span>  

<span data-ttu-id="71a66-144">Это поле указывает, зарегистрировано ли устройство hello в Azure AD в качестве персонального устройства (помечен как *присоединено к рабочему месту*).</span><span class="sxs-lookup"><span data-stu-id="71a66-144">This field indicates whether hello device is registered with Azure AD as a personal device (marked as *Workplace Joined*).</span></span> <span data-ttu-id="71a66-145">Этот параметр должен иметь значение **NO** для присоединенных к домену компьютеров, на которых также настроено гибридное присоединение к Azure AD.</span><span class="sxs-lookup"><span data-stu-id="71a66-145">This value should be **NO** for a domain-joined computer that is also hybrid Azure AD joined.</span></span> <span data-ttu-id="71a66-146">Если значение hello **Да**, рабочей или учебной учетной записи был добавлен завершения предыдущего toohello соединения hello гибридной Azure AD.</span><span class="sxs-lookup"><span data-stu-id="71a66-146">If hello value is **YES**, a work or school account was added prior toohello completion of hello hybrid Azure AD join.</span></span> <span data-ttu-id="71a66-147">В этом случае hello учетной записи учитывается при использовании версии hello Юбилейного обновления Windows 10 (1607).</span><span class="sxs-lookup"><span data-stu-id="71a66-147">In this case, hello account is ignored when using hello Anniversary Update version of Windows 10 (1607).</span></span>

---

### <a name="wamdefaultset--yes-and-azureadprt--yes"></a><span data-ttu-id="71a66-148">WamDefaultSet: YES и AzureADPrt: YES</span><span class="sxs-lookup"><span data-stu-id="71a66-148">WamDefaultSet : YES and AzureADPrt : YES</span></span>
  
<span data-ttu-id="71a66-149">Эти поля указывают, является ли пользователь hello успешно проверку подлинности tooAzure AD при входе в toohello устройства.</span><span class="sxs-lookup"><span data-stu-id="71a66-149">These fields indicate whether hello user has successfully authenticated tooAzure AD when signing in toohello device.</span></span> <span data-ttu-id="71a66-150">Если значения hello **нет**, может быть вызвано:</span><span class="sxs-lookup"><span data-stu-id="71a66-150">If hello values are **NO**, it could be due:</span></span>

- <span data-ttu-id="71a66-151">Ключ хранилища неправильный (STK) в доверенный платформенный модуль, связанный с hello устройства при регистрации (hello проверка KeySignTest во время работы с повышенными правами).</span><span class="sxs-lookup"><span data-stu-id="71a66-151">Bad storage key (STK) in TPM associated with hello device upon registration (check hello KeySignTest while running elevated).</span></span>

- <span data-ttu-id="71a66-152">Наличие альтернативного имени пользователя.</span><span class="sxs-lookup"><span data-stu-id="71a66-152">Alternate Login ID</span></span>

- <span data-ttu-id="71a66-153">Прокси-сервер HTTP не найден.</span><span class="sxs-lookup"><span data-stu-id="71a66-153">HTTP Proxy not found</span></span>

## <a name="next-steps"></a><span data-ttu-id="71a66-154">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="71a66-154">Next steps</span></span>

<span data-ttu-id="71a66-155">Ответы на вопросы см hello [управление устройствами вопросы и ответы](device-management-faq.md)</span><span class="sxs-lookup"><span data-stu-id="71a66-155">For questions, see hello [device management FAQ](device-management-faq.md)</span></span> 
