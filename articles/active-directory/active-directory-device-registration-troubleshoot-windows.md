---
title: "aaaTroubleshooting hello автоматической регистрации Azure AD домена компьютеров, присоединенных к для Windows 10 и Windows Server 2016 | Документы Microsoft"
description: "Устранение неполадок hello функции автоматической регистрации Azure AD домена компьютеров, присоединенных к для Windows 10 и Windows Server 2016."
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
ms.openlocfilehash: 3795323ce9392368b412b3e1208868431e59a74b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-auto-registration-of-domain-joined-computers-tooazure-ad--windows-10-and-windows-server-2016"></a><span data-ttu-id="5c52f-103">Устранение неполадок автоматической регистрации домена присоединены компьютеры tooAzure AD – Windows 10 и Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="5c52f-103">Troubleshooting auto-registration of domain joined computers tooAzure AD – Windows 10 and Windows Server 2016</span></span>

<span data-ttu-id="5c52f-104">Этот раздел является применимо toohello следующих клиентов:</span><span class="sxs-lookup"><span data-stu-id="5c52f-104">This topic is applicable toohello following clients:</span></span>

-   <span data-ttu-id="5c52f-105">Windows 10</span><span class="sxs-lookup"><span data-stu-id="5c52f-105">Windows 10</span></span>
-   <span data-ttu-id="5c52f-106">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="5c52f-106">Windows Server 2016</span></span>

<span data-ttu-id="5c52f-107">Для других клиентов Windows в разделе [Устранение неполадок автоматической регистрации домена присоединены компьютеры tooAzure AD для клиентов нижнего уровня Windows](active-directory-device-registration-troubleshoot-windows-legacy.md).</span><span class="sxs-lookup"><span data-stu-id="5c52f-107">For other Windows clients, see [Troubleshooting auto-registration of domain joined computers tooAzure AD for Windows down-level clients](active-directory-device-registration-troubleshoot-windows-legacy.md).</span></span>

<span data-ttu-id="5c52f-108">В этом разделе предполагается, что функции автоматической регистрации устройств, присоединенных к домену, перечисленные в описано в [как tooconfigure Автоматическая регистрация Windows, присоединенных к домену устройствами с помощью Azure Active Directory](active-directory-device-registration-get-started.md) toosupport hello следующие сценарии:</span><span class="sxs-lookup"><span data-stu-id="5c52f-108">This topic assumes that you have configured auto-registration of domain-joined devices as outlined in described in [How tooconfigure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-device-registration-get-started.md) toosupport hello following scenarios:</span></span>

- [<span data-ttu-id="5c52f-109">Условный доступ на основе устройств</span><span class="sxs-lookup"><span data-stu-id="5c52f-109">Device-based conditional access</span></span>](active-directory-conditional-access-automatic-device-registration-setup.md)

- [<span data-ttu-id="5c52f-110">Корпоративное перемещение параметров</span><span class="sxs-lookup"><span data-stu-id="5c52f-110">Enterprise roaming of settings</span></span>](active-directory-windows-enterprise-state-roaming-overview.md)

- [<span data-ttu-id="5c52f-111">Настройка Windows Hello для бизнеса</span><span class="sxs-lookup"><span data-stu-id="5c52f-111">Windows Hello for Business</span></span>](active-directory-azureadjoin-passport-deployment.md)


<span data-ttu-id="5c52f-112">В этом документе приведены инструкции по устранению как tooresolve потенциальные проблемы.</span><span class="sxs-lookup"><span data-stu-id="5c52f-112">This document provides troubleshooting guidance on how tooresolve potential issues.</span></span> 

<span data-ttu-id="5c52f-113">Hello регистрация поддерживается в hello Windows обновление 10 ноября 2015 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="5c52f-113">hello registration is supported in hello Windows 10 November 2015 Update and above.</span></span>  
<span data-ttu-id="5c52f-114">Рекомендуется использовать для включения выше сценариев hello hello окончания действия обновления.</span><span class="sxs-lookup"><span data-stu-id="5c52f-114">We recommend using hello Anniversary Update for enabling hello scenarios above.</span></span>

## <a name="step-1-retrieve-hello-registration-status"></a><span data-ttu-id="5c52f-115">Шаг 1: Получить состояние регистрации hello</span><span class="sxs-lookup"><span data-stu-id="5c52f-115">Step 1: Retrieve hello registration status</span></span> 

<span data-ttu-id="5c52f-116">**Состояние регистрации hello tooretrieve:**</span><span class="sxs-lookup"><span data-stu-id="5c52f-116">**tooretrieve hello registration status:**</span></span>

1. <span data-ttu-id="5c52f-117">Откройте командную строку hello с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="5c52f-117">Open hello command prompt as an administrator.</span></span>

2. <span data-ttu-id="5c52f-118">Введите **dsregcmd/status**.</span><span class="sxs-lookup"><span data-stu-id="5c52f-118">Type **dsregcmd /status**</span></span>



    <span data-ttu-id="5c52f-119">+----------------------------------------------------------------------+
    | Состояние устройства                                                         |  +----------------------------------------------------------------------+</span><span class="sxs-lookup"><span data-stu-id="5c52f-119">+----------------------------------------------------------------------+
    | Device State                                                         |  +----------------------------------------------------------------------+</span></span>
    
        AzureAdJoined : YES
     <span data-ttu-id="5c52f-120">EnterpriseJoined: Не DeviceId: 5820fbe9-60c8-43b0-bb11-44aee233e4e7 отпечаток: B753A6679CE720451921302CA873794D94C6204A KeyContainerId: bae6a60b-1d2f-4d2a-a298-33385f6d05e9 KeyProvider: TpmProtected поставщик криптографии Microsoft Platform: Да KeySignTest:: необходимо выполнить с повышенными привилегиями tootest.</span><span class="sxs-lookup"><span data-stu-id="5c52f-120">EnterpriseJoined : NO DeviceId : 5820fbe9-60c8-43b0-bb11-44aee233e4e7 Thumbprint : B753A6679CE720451921302CA873794D94C6204A KeyContainerId : bae6a60b-1d2f-4d2a-a298-33385f6d05e9 KeyProvider : Microsoft Platform Crypto Provider TpmProtected : YES KeySignTest: : MUST Run elevated tootest.</span></span>
                  <span data-ttu-id="5c52f-121">Idp : login.windows.net TenantId : 72b988bf-86f1-41af-91ab-2d7cd011db47 TenantName : Contoso AuthCodeUrl : https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/authorize AccessTokenUrl : https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/token MdmUrl : https://enrollment.manage-beta.microsoft.com/EnrollmentServer/Discovery.svc MdmTouUrl : https://portal.manage-beta.microsoft.com/TermsOfUse.aspx dmComplianceUrl : https://portal.manage-beta.microsoft.com/?portalAction=Compliance SettingsUrl : eyJVcmlzIjpbImh0dHBzOi8va2FpbGFuaS5vbmUubWljcm9zb2Z0LmNvbS8iLCJodHRwczovL2thaWxhbmkxLm9uZS5taWNyb3NvZnQuY29tLyJdfQ== JoinSrvVersion : 1.0 JoinSrvUrl : https://enterpriseregistration.windows.net/EnrollmentServer/device/ JoinSrvId : urn:ms-drs:enterpriseregistration.windows.net KeySrvVersion : 1.0 KeySrvUrl : https://enterpriseregistration.windows.net/EnrollmentServer/key/ KeySrvId : urn:ms-drs:enterpriseregistration.windows.net DomainJoined : YES DomainName : CONTOSO</span><span class="sxs-lookup"><span data-stu-id="5c52f-121">Idp : login.windows.net TenantId : 72b988bf-86f1-41af-91ab-2d7cd011db47 TenantName : Contoso AuthCodeUrl : https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/authorize AccessTokenUrl : https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/token MdmUrl : https://enrollment.manage-beta.microsoft.com/EnrollmentServer/Discovery.svc MdmTouUrl : https://portal.manage-beta.microsoft.com/TermsOfUse.aspx dmComplianceUrl : https://portal.manage-beta.microsoft.com/?portalAction=Compliance SettingsUrl : eyJVcmlzIjpbImh0dHBzOi8va2FpbGFuaS5vbmUubWljcm9zb2Z0LmNvbS8iLCJodHRwczovL2thaWxhbmkxLm9uZS5taWNyb3NvZnQuY29tLyJdfQ== JoinSrvVersion : 1.0 JoinSrvUrl : https://enterpriseregistration.windows.net/EnrollmentServer/device/ JoinSrvId : urn:ms-drs:enterpriseregistration.windows.net KeySrvVersion : 1.0 KeySrvUrl : https://enterpriseregistration.windows.net/EnrollmentServer/key/ KeySrvId : urn:ms-drs:enterpriseregistration.windows.net DomainJoined : YES DomainName : CONTOSO</span></span>
    
    <span data-ttu-id="5c52f-122">+----------------------------------------------------------------------+
    | Состояние пользователя                                                           |  +----------------------------------------------------------------------+</span><span class="sxs-lookup"><span data-stu-id="5c52f-122">+----------------------------------------------------------------------+
    | User State                                                           |  +----------------------------------------------------------------------+</span></span>
    
                 NgcSet : YES
               NgcKeyId : {C7A9AEDC-780E-4FDA-B200-1AE15561A46B}
        WorkplaceJoined : NO
          WamDefaultSet : YES
    <span data-ttu-id="5c52f-123">WamDefaultAuthority : organizations         WamDefaultId : https://login.microsoft.com       WamDefaultGUID : {B16898C6-A148-4967-9171-64D755DA8520} (AzureAd)           AzureAdPrt : YES</span><span class="sxs-lookup"><span data-stu-id="5c52f-123">WamDefaultAuthority : organizations         WamDefaultId : https://login.microsoft.com       WamDefaultGUID : {B16898C6-A148-4967-9171-64D755DA8520} (AzureAd)           AzureAdPrt : YES</span></span>



## <a name="step-2-evaluate-hello-registration-status"></a><span data-ttu-id="5c52f-124">Шаг 2: Оценка hello состояние регистрации</span><span class="sxs-lookup"><span data-stu-id="5c52f-124">Step 2: Evaluate hello registration status</span></span> 

<span data-ttu-id="5c52f-125">Просмотрите следующие поля hello и убедитесь в том, что они имеют hello ожидаемые значения:</span><span class="sxs-lookup"><span data-stu-id="5c52f-125">Review hello following fields and make sure that they have hello expected values:</span></span>

### <a name="azureadjoined--yes"></a><span data-ttu-id="5c52f-126">AzureAdJoined: YES</span><span class="sxs-lookup"><span data-stu-id="5c52f-126">AzureAdJoined : YES</span></span>  

<span data-ttu-id="5c52f-127">В этом поле показан, зарегистрировано ли устройство hello в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5c52f-127">This field shows whether hello device is registered with Azure AD.</span></span> <span data-ttu-id="5c52f-128">Если значение hello показывает, как «Нет», регистрации не завершена.</span><span class="sxs-lookup"><span data-stu-id="5c52f-128">If hello value shows as ‘NO’, registration has not completed.</span></span> 

<span data-ttu-id="5c52f-129">**Возможные причины:**</span><span class="sxs-lookup"><span data-stu-id="5c52f-129">**Possible causes:**</span></span>

- <span data-ttu-id="5c52f-130">Не удалось выполнить проверку подлинности компьютера hello для регистрации.</span><span class="sxs-lookup"><span data-stu-id="5c52f-130">Authentication of hello computer for registration failed.</span></span>

- <span data-ttu-id="5c52f-131">Есть прокси-сервер HTTP hello организации, которые не могут быть обнаружены на компьютере hello</span><span class="sxs-lookup"><span data-stu-id="5c52f-131">There is an HTTP proxy in hello organization that cannot be discovered by hello computer</span></span>

- <span data-ttu-id="5c52f-132">Hello недоступность Azure AD для проверки подлинности или DRS Azure для регистрации</span><span class="sxs-lookup"><span data-stu-id="5c52f-132">hello computer cannot reach Azure AD for authentication or Azure DRS for registration</span></span>

- <span data-ttu-id="5c52f-133">Hello компьютер может быть hello внутренней сети организации или VPN с tooan прямая линия видимости локального контроллера домена AD.</span><span class="sxs-lookup"><span data-stu-id="5c52f-133">hello computer may not be on hello organization’s internal network or on VPN with direct line of sight tooan on-premises AD domain controller.</span></span>

- <span data-ttu-id="5c52f-134">Если компьютер hello доверенного платформенного МОДУЛЯ, возможно, в неверном состоянии.</span><span class="sxs-lookup"><span data-stu-id="5c52f-134">If hello computer has a TPM, it may be in a bad state.</span></span>

- <span data-ttu-id="5c52f-135">Может быть неправильной конфигурации в службах отмечалось в документе hello, которые понадобятся tooverify еще раз.</span><span class="sxs-lookup"><span data-stu-id="5c52f-135">There may be a misconfiguration in services noted in hello document earlier that you will need tooverify again.</span></span> <span data-ttu-id="5c52f-136">Ниже приведены распространенные примеры.</span><span class="sxs-lookup"><span data-stu-id="5c52f-136">Common examples are:</span></span>

    - <span data-ttu-id="5c52f-137">На сервере федерации нет включенных конечных точек WS-Trust.</span><span class="sxs-lookup"><span data-stu-id="5c52f-137">Your federation server does not have WS-Trust endpoints enabled</span></span>

    - <span data-ttu-id="5c52f-138">На сервере федерации может быть запрещена входящая аутентификация компьютеров в сети с использованием встроенной проверки подлинности Windows.</span><span class="sxs-lookup"><span data-stu-id="5c52f-138">Your federation server may not allow inbound authentication from computers in your network using Integrated Windows Authentication.</span></span>

    - <span data-ttu-id="5c52f-139">Нет объекта точки подключения службы, указывающий tooyour проверенное имя домена в Azure AD в лесу hello AD, которой принадлежит компьютер hello</span><span class="sxs-lookup"><span data-stu-id="5c52f-139">There is no Service Connection Point object that points tooyour verified domain name in Azure AD in hello AD forest where hello computer belongs to</span></span>

---

### <a name="domainjoined--yes"></a><span data-ttu-id="5c52f-140">DomainJoined: YES</span><span class="sxs-lookup"><span data-stu-id="5c52f-140">DomainJoined : YES</span></span>  

<span data-ttu-id="5c52f-141">Это поле показывает, является hello устройства присоединены к домену tooan локальной Active Directory, или нет.</span><span class="sxs-lookup"><span data-stu-id="5c52f-141">This field shows whether hello device is joined tooan on-premises Active Directory or not.</span></span> <span data-ttu-id="5c52f-142">Если отображается значение hello, что **нет**, hello устройства не может автоматически регистрируются в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5c52f-142">If hello value shows as **NO**, hello device cannot auto-register with Azure AD.</span></span> <span data-ttu-id="5c52f-143">Сначала проверьте, toohello соединения hello устройства в локальной Active Directory, прежде чем он может зарегистрироваться в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5c52f-143">Check first that hello device joins toohello on-premises Active Directory before it can register with Azure AD.</span></span> <span data-ttu-id="5c52f-144">Если вы ищете присоединение hello tooAzure компьютера AD напрямую, перейдите в tooLearn о возможности присоединения Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5c52f-144">If you are looking for joining hello computer tooAzure AD directly, please go tooLearn about capabilities of Azure Active Directory Join.</span></span>

---

### <a name="workplacejoined--no"></a><span data-ttu-id="5c52f-145">WorkplaceJoined: NO</span><span class="sxs-lookup"><span data-stu-id="5c52f-145">WorkplaceJoined : NO</span></span>  

<span data-ttu-id="5c52f-146">В этом поле показан, зарегистрировано ли устройство hello в Azure AD, а также как личного устройства (помеченные как «Присоединено к рабочему месту»).</span><span class="sxs-lookup"><span data-stu-id="5c52f-146">This field shows whether hello device is registered with Azure AD but as a personal device (marked as ‘Workplace Joined’).</span></span> <span data-ttu-id="5c52f-147">Если это значение должно отображаться как «Нет» для присоединенных к домену компьютера, зарегистрированных в Azure AD, однако если показано значение "Да" означает, что рабочей или учебной учетной записи был Завершение регистрации добавлены предыдущих toohello компьютера.</span><span class="sxs-lookup"><span data-stu-id="5c52f-147">If this value should show as ‘NO’ for a domain joined computer registered with Azure AD, however if it shows as YES it means that a work or school account was added prior toohello computer completing registration.</span></span> <span data-ttu-id="5c52f-148">В этом случае hello учетной записи будет игнорироваться при использовании версии hello Юбилейного обновления Windows 10 (1607 при выполнении команды WinVer hello hello окна «Выполнить» или окно командной строки).</span><span class="sxs-lookup"><span data-stu-id="5c52f-148">In this case hello account will be ignored if using hello Anniversary Update version of Windows 10 (1607 when running hello WinVer command in hello ‘Run’ window or a command prompt window).</span></span>

---

### <a name="wamdefaultset--yes-and-azureadprt--yes"></a><span data-ttu-id="5c52f-149">WamDefaultSet: YES и AzureADPrt: YES</span><span class="sxs-lookup"><span data-stu-id="5c52f-149">WamDefaultSet : YES and AzureADPrt : YES</span></span>
  
<span data-ttu-id="5c52f-150">Эти поля видно, что этот пользователь hello еще успешно прошел проверку подлинности tooAzure AD после входа в устройство toohello.</span><span class="sxs-lookup"><span data-stu-id="5c52f-150">These fields show that hello user has successfully authenticated tooAzure AD upon signing in toohello device.</span></span> <span data-ttu-id="5c52f-151">Если они показывают «Нет» hello ниже приведены возможные причины ее возникновения.</span><span class="sxs-lookup"><span data-stu-id="5c52f-151">If they show ‘NO’ hello following are possible causes:</span></span>

- <span data-ttu-id="5c52f-152">Ключ хранилища неправильный (STK) в доверенный платформенный модуль, связанный с hello устройства при регистрации (hello проверка KeySignTest во время работы с повышенными правами).</span><span class="sxs-lookup"><span data-stu-id="5c52f-152">Bad storage key (STK) in TPM associated with hello device upon registration (check hello KeySignTest while running elevated).</span></span>

- <span data-ttu-id="5c52f-153">Наличие альтернативного имени пользователя.</span><span class="sxs-lookup"><span data-stu-id="5c52f-153">Alternate Login ID</span></span>

- <span data-ttu-id="5c52f-154">Прокси-сервер HTTP не найден.</span><span class="sxs-lookup"><span data-stu-id="5c52f-154">HTTP Proxy not found</span></span>

## <a name="next-steps"></a><span data-ttu-id="5c52f-155">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5c52f-155">Next steps</span></span>

<span data-ttu-id="5c52f-156">Дополнительные сведения см. в разделе hello [автоматической регистрации устройств вопросы и ответы](active-directory-device-registration-faq.md)</span><span class="sxs-lookup"><span data-stu-id="5c52f-156">For more information, see hello [Automatic device registration FAQ](active-directory-device-registration-faq.md)</span></span> 
