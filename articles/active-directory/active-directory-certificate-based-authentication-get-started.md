---
title: "Приступая к работе aaaAzure проверки подлинности на основе сертификатов Active Directory - | Документы Microsoft"
description: "Узнайте, как tooconfigure на основе сертификатов проверки подлинности в вашей среде"
author: MarkusVi
documentationcenter: na
manager: femila
ms.assetid: c6ad7640-8172-4541-9255-770f39ecce0e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/02/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 3c73bdf56018c0716085c923a61e9560dbe4004c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-certificate-based-authentication-in-azure-active-directory"></a><span data-ttu-id="f2c85-103">Приступая к работе с аутентификацией на основе сертификата в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f2c85-103">Get started with certificate-based authentication in Azure Active Directory</span></span>

<span data-ttu-id="f2c85-104">Проверка подлинности на основе сертификатов обеспечивает toobe проверку подлинности Azure Active Directory с помощью сертификата клиента на устройстве Windows, Android или iOS при подключении учетную Exchange online с:</span><span class="sxs-lookup"><span data-stu-id="f2c85-104">Certificate-based authentication enables you toobe authenticated by Azure Active Directory with a client certificate on a Windows, Android or iOS device when connecting your Exchange online account to:</span></span> 

- <span data-ttu-id="f2c85-105">мобильным приложениям Office, таким как Microsoft Outlook и Microsoft Word;</span><span class="sxs-lookup"><span data-stu-id="f2c85-105">Office mobile applications such as Microsoft Outlook and Microsoft Word</span></span>   

- <span data-ttu-id="f2c85-106">клиентам Exchange ActiveSync (EAS).</span><span class="sxs-lookup"><span data-stu-id="f2c85-106">Exchange ActiveSync (EAS) clients</span></span> 

<span data-ttu-id="f2c85-107">Эта настройка устраняет необходимость hello tooenter имя пользователя и пароль к нему в определенных почты и приложения Microsoft Office на мобильных устройствах.</span><span class="sxs-lookup"><span data-stu-id="f2c85-107">Configuring this feature eliminates hello need tooenter a username and password combination into certain mail and Microsoft Office applications on your mobile device.</span></span> 

<span data-ttu-id="f2c85-108">В этой статье:</span><span class="sxs-lookup"><span data-stu-id="f2c85-108">This topic:</span></span>

- <span data-ttu-id="f2c85-109">Предоставляет вам hello tooconfigure шаги, чтобы использовать на основе сертификатов проверки подлинности для пользователей клиентов в Office 365 Enterprise, Business, образовательных учреждений и планы правительства США.</span><span class="sxs-lookup"><span data-stu-id="f2c85-109">Provides you with hello steps tooconfigure and utilize certificate-based authentication for users of tenants in Office 365 Enterprise, Business, Education, and US Government plans.</span></span> <span data-ttu-id="f2c85-110">В тарифных планах Office 365 China, US Government Defense и US Government Federal доступна предварительная версия этой функции.</span><span class="sxs-lookup"><span data-stu-id="f2c85-110">This feature is available in preview in Office 365 China, US Government Defense, and US Government Federal plans.</span></span> 

- <span data-ttu-id="f2c85-111">Предполагается, что у вас уже настроены [инфраструктура открытых ключей (PKI)](https://go.microsoft.com/fwlink/?linkid=841737) и [AD FS](connect/active-directory-aadconnectfed-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f2c85-111">Assumes that you already have a [public key infrastructure (PKI)](https://go.microsoft.com/fwlink/?linkid=841737) and [AD FS](connect/active-directory-aadconnectfed-whatis.md) configured.</span></span>    


## <a name="requirements"></a><span data-ttu-id="f2c85-112">Требования</span><span class="sxs-lookup"><span data-stu-id="f2c85-112">Requirements</span></span>

<span data-ttu-id="f2c85-113">tooconfigure сертификат проверки подлинности на основе hello должны выполняться следующие условия:</span><span class="sxs-lookup"><span data-stu-id="f2c85-113">tooconfigure certificate-based authentication, hello following must be true:</span></span>  

- <span data-ttu-id="f2c85-114">Аутентификация на основе сертификата (CBA) поддерживается только для браузерных приложений и собственных клиентов в федеративных средах, использующих современную аутентификацию (ADAL).</span><span class="sxs-lookup"><span data-stu-id="f2c85-114">Certificate-based authentication (CBA) is only supported for Federated environments for browser applications or native clients using modern authentication (ADAL).</span></span> <span data-ttu-id="f2c85-115">Hello единственное исключение — Exchange Active Sync (EAS) для EXO, который может использоваться для учетных записей, федеративным и управляемым.</span><span class="sxs-lookup"><span data-stu-id="f2c85-115">hello one exception is Exchange Active Sync (EAS) for EXO which can be used for both, federated and managed accounts.</span></span> 

- <span data-ttu-id="f2c85-116">в Azure Active Directory необходимо включить Hello корневым центром сертификации и промежуточный центр сертификации.</span><span class="sxs-lookup"><span data-stu-id="f2c85-116">hello root certificate authority and any intermediate certificate authorities must be configured in Azure Active Directory.</span></span>  

- <span data-ttu-id="f2c85-117">Каждый центр сертификации должен иметь список отзыва сертификатов (CRL), на который можно сослаться с помощью URL-адреса для Интернета.</span><span class="sxs-lookup"><span data-stu-id="f2c85-117">Each certificate authority must have a certificate revocation list (CRL) that can be referenced via an Internet facing URL.</span></span>  

- <span data-ttu-id="f2c85-118">В Azure Active Directory должен быть настроен хотя бы один центр сертификации.</span><span class="sxs-lookup"><span data-stu-id="f2c85-118">You must have at least one certificate authority configured in Azure Active Directory.</span></span> <span data-ttu-id="f2c85-119">Связанные действия можно найти в hello [Настройка центров сертификации hello](#step-2-configure-the-certificate-authorities) раздела.</span><span class="sxs-lookup"><span data-stu-id="f2c85-119">You can find related steps in hello [Configure hello certificate authorities](#step-2-configure-the-certificate-authorities) section.</span></span>  

- <span data-ttu-id="f2c85-120">Для клиентов Exchange ActiveSync hello клиентский сертификат должен иметь hello маршрутизируемый адрес электронной почты пользователя адрес в Exchange online в любом hello имени участника-службы или hello имя RFC822 значение hello альтернативное имя субъекта.</span><span class="sxs-lookup"><span data-stu-id="f2c85-120">For Exchange ActiveSync clients, hello client certificate must have hello user’s routable email address in Exchange online in either hello Principal Name or hello RFC822 Name value of hello Subject Alternative Name field.</span></span> <span data-ttu-id="f2c85-121">Azure Active Directory сопоставляет атрибут hello RFC822 значения toohello адрес прокси-сервера в каталоге hello.</span><span class="sxs-lookup"><span data-stu-id="f2c85-121">Azure Active Directory maps hello RFC822 value toohello Proxy Address attribute in hello directory.</span></span>  

- <span data-ttu-id="f2c85-122">Устройство клиента должны иметь доступ по крайней мере одно tooat центр сертификации, выдающий сертификаты клиента.</span><span class="sxs-lookup"><span data-stu-id="f2c85-122">Your client device must have access tooat least one certificate authority that issues client certificates.</span></span>  

- <span data-ttu-id="f2c85-123">Сертификат клиента для проверки подлинности клиента должен быть выдан tooyour клиента.</span><span class="sxs-lookup"><span data-stu-id="f2c85-123">A client certificate for client authentication must have been issued tooyour client.</span></span>  




## <a name="step-1-select-your-device-platform"></a><span data-ttu-id="f2c85-124">Шаг 1. Выбор платформы устройства</span><span class="sxs-lookup"><span data-stu-id="f2c85-124">Step 1: Select your device platform</span></span>

<span data-ttu-id="f2c85-125">В качестве первого шага для hello платформы устройств, которые вас интересуют, необходимы следующие tooreview hello.</span><span class="sxs-lookup"><span data-stu-id="f2c85-125">As a first step, for hello device platform you care about, you need tooreview hello following:</span></span>

- <span data-ttu-id="f2c85-126">Поддержка мобильных приложений Office Hello</span><span class="sxs-lookup"><span data-stu-id="f2c85-126">hello Office mobile applications support</span></span> 
- <span data-ttu-id="f2c85-127">требования к реализации Hello</span><span class="sxs-lookup"><span data-stu-id="f2c85-127">hello specific implementation requirements</span></span>  

<span data-ttu-id="f2c85-128">Привет, связанные с существует сведения для следующих платформ устройств hello:</span><span class="sxs-lookup"><span data-stu-id="f2c85-128">hello related information exists for hello following device platforms:</span></span>

- [<span data-ttu-id="f2c85-129">Android</span><span class="sxs-lookup"><span data-stu-id="f2c85-129">Android</span></span>](active-directory-certificate-based-authentication-android.md)
- [<span data-ttu-id="f2c85-130">iOS</span><span class="sxs-lookup"><span data-stu-id="f2c85-130">iOS</span></span>](active-directory-certificate-based-authentication-ios.md)


## <a name="step-2-configure-hello-certificate-authorities"></a><span data-ttu-id="f2c85-131">Шаг 2: Настройка центров сертификации hello</span><span class="sxs-lookup"><span data-stu-id="f2c85-131">Step 2: Configure hello certificate authorities</span></span> 

<span data-ttu-id="f2c85-132">tooconfigure центров сертификации в Azure Active Directory для каждого центра сертификации передачи hello следующие:</span><span class="sxs-lookup"><span data-stu-id="f2c85-132">tooconfigure your certificate authorities in Azure Active Directory, for each certificate authority, upload hello following:</span></span> 

* <span data-ttu-id="f2c85-133">Hello открытую часть сертификата hello в *.cer* формат</span><span class="sxs-lookup"><span data-stu-id="f2c85-133">hello public portion of hello certificate, in *.cer* format</span></span> 
* <span data-ttu-id="f2c85-134">Hello в Интернете URL-адреса, где hello списков отзыва сертификатов (CRL) находятся</span><span class="sxs-lookup"><span data-stu-id="f2c85-134">hello Internet facing URLs where hello Certificate Revocation Lists (CRLs) reside</span></span>

<span data-ttu-id="f2c85-135">Схема Hello для сертификации выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="f2c85-135">hello schema for a certificate authority looks as follows:</span></span> 

    class TrustedCAsForPasswordlessAuth 
    { 
       CertificateAuthorityInformation[] certificateAuthorities;    
    } 

    class CertificateAuthorityInformation 

    { 
        CertAuthorityType authorityType; 
        X509Certificate trustedCertificate; 
        string crlDistributionPoint; 
        string deltaCrlDistributionPoint; 
        string trustedIssuer; 
        string trustedIssuerSKI; 
    }                

    enum CertAuthorityType 
    { 
        RootAuthority = 0, 
        IntermediateAuthority = 1 
    } 

<span data-ttu-id="f2c85-136">Для конфигурации hello, можно использовать hello [Azure Active Directory PowerShell версии 2](/powershell/azure/install-adv2?view=azureadps-2.0):</span><span class="sxs-lookup"><span data-stu-id="f2c85-136">For hello configuration, you can use hello [Azure Active Directory PowerShell Version 2](/powershell/azure/install-adv2?view=azureadps-2.0):</span></span>  

1. <span data-ttu-id="f2c85-137">Запустите Windows PowerShell с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="f2c85-137">Start Windows PowerShell with administrator privileges.</span></span> 
2. <span data-ttu-id="f2c85-138">Установите модуль hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f2c85-138">Install hello Azure AD module.</span></span> <span data-ttu-id="f2c85-139">Требуется версия tooinstall [2.0.0.33 ](https://www.powershellgallery.com/packages/AzureAD/2.0.0.33) или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="f2c85-139">You need tooinstall Version [2.0.0.33 ](https://www.powershellgallery.com/packages/AzureAD/2.0.0.33) or higher.</span></span>  
   
        Install-Module -Name AzureAD –RequiredVersion 2.0.0.33 

<span data-ttu-id="f2c85-140">В конфигурации, сначала должны tooestablish соединение с клиентом.</span><span class="sxs-lookup"><span data-stu-id="f2c85-140">As a first configuration step, you need tooestablish a connection with your tenant.</span></span> <span data-ttu-id="f2c85-141">Как только клиент tooyour подключение существует, можно просмотреть, добавить, удалить и изменить hello доверенных центров сертификации, которые определены в каталоге.</span><span class="sxs-lookup"><span data-stu-id="f2c85-141">As soon as a connection tooyour tenant exists, you can review, add, delete and modify hello trusted certificate authorities that are defined in your directory.</span></span> 

### <a name="connect"></a><span data-ttu-id="f2c85-142">Подключение</span><span class="sxs-lookup"><span data-stu-id="f2c85-142">Connect</span></span>

<span data-ttu-id="f2c85-143">соединение с клиентом, используйте hello tooestablish [Connect AzureAD](/powershell/module/azuread/connect-azuread?view=azureadps-2.0) командлета:</span><span class="sxs-lookup"><span data-stu-id="f2c85-143">tooestablish a connection with your tenant, use hello [Connect-AzureAD](/powershell/module/azuread/connect-azuread?view=azureadps-2.0) cmdlet:</span></span>

    Connect-AzureAD 


### <a name="retrieve"></a><span data-ttu-id="f2c85-144">Получение</span><span class="sxs-lookup"><span data-stu-id="f2c85-144">Retrieve</span></span> 

<span data-ttu-id="f2c85-145">tooretrieve hello доверенных центров сертификации, определенные в каталоге, использовать hello [Get AzureADTrustedCertificateAuthority](/powershell/module/azuread/get-azureadtrustedcertificateauthority?view=azureadps-2.0) командлета.</span><span class="sxs-lookup"><span data-stu-id="f2c85-145">tooretrieve hello trusted certificate authorities that are defined in your directory, use hello [Get-AzureADTrustedCertificateAuthority](/powershell/module/azuread/get-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet.</span></span> 

    Get-AzureADTrustedCertificateAuthority 
 

### <a name="add"></a><span data-ttu-id="f2c85-146">Добавить</span><span class="sxs-lookup"><span data-stu-id="f2c85-146">Add</span></span>

<span data-ttu-id="f2c85-147">toocreate доверенным центром сертификации, использовать hello [New AzureADTrustedCertificateAuthority](/powershell/module/azuread/new-azureadtrustedcertificateauthority?view=azureadps-2.0) командлета и набор hello **crlDistributionPoint** tooa правильное значение атрибута:</span><span class="sxs-lookup"><span data-stu-id="f2c85-147">toocreate a trusted certificate authority, use hello [New-AzureADTrustedCertificateAuthority](/powershell/module/azuread/new-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet and set hello **crlDistributionPoint** attribute tooa correct value:</span></span> 
   
    $cert=Get-Content -Encoding byte "[LOCATION OF hello CER FILE]" 
    $new_ca=New-Object -TypeName Microsoft.Open.AzureAD.Model.CertificateAuthorityInformation 
    $new_ca.AuthorityType=0 
    $new_ca.TrustedCertificate=$cert 
    $new_ca.crlDistributionPoint=”<CRL Distribution URL>”
    New-AzureADTrustedCertificateAuthority -CertificateAuthorityInformation $new_ca 


### <a name="remove"></a><span data-ttu-id="f2c85-148">Удалить</span><span class="sxs-lookup"><span data-stu-id="f2c85-148">Remove</span></span>

<span data-ttu-id="f2c85-149">tooremove доверенным центром сертификации, использовать hello [AzureADTrustedCertificateAuthority удаление](/powershell/module/azuread/remove-azureadtrustedcertificateauthority?view=azureadps-2.0) командлета:</span><span class="sxs-lookup"><span data-stu-id="f2c85-149">tooremove a trusted certificate authority, use hello [Remove-AzureADTrustedCertificateAuthority](/powershell/module/azuread/remove-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet:</span></span>
   
    $c=Get-AzureADTrustedCertificateAuthority 
    Remove-AzureADTrustedCertificateAuthority -CertificateAuthorityInformation $c[2] 


### <a name="modfiy"></a><span data-ttu-id="f2c85-150">Изменение</span><span class="sxs-lookup"><span data-stu-id="f2c85-150">Modfiy</span></span>

<span data-ttu-id="f2c85-151">toomodify доверенным центром сертификации, использовать hello [AzureADTrustedCertificateAuthority набор](/powershell/module/azuread/set-azureadtrustedcertificateauthority?view=azureadps-2.0) командлета:</span><span class="sxs-lookup"><span data-stu-id="f2c85-151">toomodify a trusted certificate authority, use hello [Set-AzureADTrustedCertificateAuthority](/powershell/module/azuread/set-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet:</span></span>

    $c=Get-AzureADTrustedCertificateAuthority 
    $c[0].AuthorityType=1 
    Set-AzureADTrustedCertificateAuthority -CertificateAuthorityInformation $c[0] 


## <a name="step-3-configure-revocation"></a><span data-ttu-id="f2c85-152">Шаг 3. Настройка отзыва</span><span class="sxs-lookup"><span data-stu-id="f2c85-152">Step 3: Configure revocation</span></span>

<span data-ttu-id="f2c85-153">toorevoke сертификат клиента Azure Active Directory выбирается сертификат hello список отзыва (CRL) из URL-адресов hello загружены как часть информации о центрах сертификации сертификат и кэширует его.</span><span class="sxs-lookup"><span data-stu-id="f2c85-153">toorevoke a client certificate, Azure Active Directory fetches hello certificate revocation list (CRL) from hello URLs uploaded as part of certificate authority information and caches it.</span></span> <span data-ttu-id="f2c85-154">Hello последней публикации отметки времени (**Дата вступления в силу** свойство) в список отзыва Сертификатов используется hello hello tooensure списка отзыва Сертификатов по-прежнему действителен.</span><span class="sxs-lookup"><span data-stu-id="f2c85-154">hello last publish timestamp (**Effective Date** property) in hello CRL is used tooensure hello CRL is still valid.</span></span> <span data-ttu-id="f2c85-155">Hello CRL — toocertificates периодически упоминаемого toorevoke доступа, входящих в состав списка hello.</span><span class="sxs-lookup"><span data-stu-id="f2c85-155">hello CRL is periodically referenced toorevoke access toocertificates that are a part of hello list.</span></span>

<span data-ttu-id="f2c85-156">При необходимости (например, в случае потери устройства) более быстрой отзыва, маркер авторизации hello hello пользователя может стать недействительным.</span><span class="sxs-lookup"><span data-stu-id="f2c85-156">If a more instant revocation is required (for example, if a user loses a device), hello authorization token of hello user can be invalidated.</span></span> <span data-ttu-id="f2c85-157">tooinvalidate hello авторизации маркеров, задайте hello **StsRefreshTokenValidFrom** для данного пользователя с помощью Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f2c85-157">tooinvalidate hello authorization token, set hello **StsRefreshTokenValidFrom** field for this particular user using Windows PowerShell.</span></span> <span data-ttu-id="f2c85-158">Необходимо обновить hello **StsRefreshTokenValidFrom** для каждого пользователя, который вы хотите получить доступ toorevoke для поля.</span><span class="sxs-lookup"><span data-stu-id="f2c85-158">You must update hello **StsRefreshTokenValidFrom** field for each user you want toorevoke access for.</span></span>

<span data-ttu-id="f2c85-159">tooensure отзыва hello сохраняется, необходимо задать hello **Дата вступления в силу** hello CRL tooa даты после hello значение, установленное **StsRefreshTokenValidFrom** и убедитесь в hello сертификата Hello списка отзыва Сертификатов.</span><span class="sxs-lookup"><span data-stu-id="f2c85-159">tooensure that hello revocation persists, you must set hello **Effective Date** of hello CRL tooa date after hello value set by **StsRefreshTokenValidFrom** and ensure hello certificate in question is in hello CRL.</span></span>

<span data-ttu-id="f2c85-160">Здравствуйте, следуйте процедуре hello структуры шаги для обновления и делает недействительными hello маркер авторизации, установка hello **StsRefreshTokenValidFrom** поля.</span><span class="sxs-lookup"><span data-stu-id="f2c85-160">hello following steps outline hello process for updating and invalidating hello authorization token by setting hello **StsRefreshTokenValidFrom** field.</span></span> 

<span data-ttu-id="f2c85-161">**tooconfigure отзыва:**</span><span class="sxs-lookup"><span data-stu-id="f2c85-161">**tooconfigure revocation:**</span></span> 

1. <span data-ttu-id="f2c85-162">Подключение со службой MSOL toohello учетные данные администратора:</span><span class="sxs-lookup"><span data-stu-id="f2c85-162">Connect with admin credentials toohello MSOL service:</span></span> 
   
        $msolcred = get-credential 
        connect-msolservice -credential $msolcred 

2. <span data-ttu-id="f2c85-163">Получить текущее значение StsRefreshTokensValidFrom hello для пользователя:</span><span class="sxs-lookup"><span data-stu-id="f2c85-163">Retrieve hello current StsRefreshTokensValidFrom value for a user:</span></span> 
   
        $user = Get-MsolUser -UserPrincipalName test@yourdomain.com` 
        $user.StsRefreshTokensValidFrom 

3. <span data-ttu-id="f2c85-164">Настройка нового значения StsRefreshTokensValidFrom для пользователя hello равно toohello Текущая отметка времени:</span><span class="sxs-lookup"><span data-stu-id="f2c85-164">Configure a new StsRefreshTokensValidFrom value for hello user equal toohello current timestamp:</span></span> 
   
        Set-MsolUser -UserPrincipalName test@yourdomain.com -StsRefreshTokensValidFrom ("03/05/2016")

<span data-ttu-id="f2c85-165">Дата Hello, задать должна быть в будущем hello.</span><span class="sxs-lookup"><span data-stu-id="f2c85-165">hello date you set must be in hello future.</span></span> <span data-ttu-id="f2c85-166">Если дата hello не будущих hello, hello **StsRefreshTokensValidFrom** свойство не задано.</span><span class="sxs-lookup"><span data-stu-id="f2c85-166">If hello date is not in hello future, hello **StsRefreshTokensValidFrom** property is not set.</span></span> <span data-ttu-id="f2c85-167">Если дата hello в будущем, hello **StsRefreshTokensValidFrom** задано toohello текущее время (не hello даты, указанной командой Set-MsolUser).</span><span class="sxs-lookup"><span data-stu-id="f2c85-167">If hello date is in hello future, **StsRefreshTokensValidFrom** is set toohello current time (not hello date indicated by Set-MsolUser command).</span></span> 


## <a name="step-4-test-your-configuration"></a><span data-ttu-id="f2c85-168">Шаг 4. Тестирование конфигурации</span><span class="sxs-lookup"><span data-stu-id="f2c85-168">Step 4: Test your configuration</span></span>

### <a name="testing-your-certificate"></a><span data-ttu-id="f2c85-169">Тестирование сертификата</span><span class="sxs-lookup"><span data-stu-id="f2c85-169">Testing your certificate</span></span>

<span data-ttu-id="f2c85-170">В качестве первой конфигурации теста, попробуйте toosign в слишком[Outlook Web Access](https://outlook.office365.com) или [SharePoint Online](https://microsoft.sharepoint.com) с помощью вашей **браузер на устройстве**.</span><span class="sxs-lookup"><span data-stu-id="f2c85-170">As a first configuration test, you should try toosign in too[Outlook Web Access](https://outlook.office365.com) or [SharePoint Online](https://microsoft.sharepoint.com) using your **on-device browser**.</span></span>

<span data-ttu-id="f2c85-171">Успешный вход подтверждает, что:</span><span class="sxs-lookup"><span data-stu-id="f2c85-171">If your sign-in is successful, then you know that:</span></span>

- <span data-ttu-id="f2c85-172">сертификат пользователя Hello был подготовленных tooyour тестовое устройство</span><span class="sxs-lookup"><span data-stu-id="f2c85-172">hello user certificate has been provisioned tooyour test device</span></span>
- <span data-ttu-id="f2c85-173">службы AD FS настроены правильно.</span><span class="sxs-lookup"><span data-stu-id="f2c85-173">AD FS is configured correctly</span></span>  


### <a name="testing-office-mobile-applications"></a><span data-ttu-id="f2c85-174">Тестирование мобильных приложений Office</span><span class="sxs-lookup"><span data-stu-id="f2c85-174">Testing Office mobile applications</span></span>

<span data-ttu-id="f2c85-175">**tootest сертификат проверки подлинности на основе мобильного приложения Office:**</span><span class="sxs-lookup"><span data-stu-id="f2c85-175">**tootest certificate-based authentication on your mobile Office application:**</span></span> 

1. <span data-ttu-id="f2c85-176">На тестируемом устройстве установите мобильное приложение Office (например, OneDrive).</span><span class="sxs-lookup"><span data-stu-id="f2c85-176">On your test device, install an Office mobile application (e.g., OneDrive).</span></span>
3. <span data-ttu-id="f2c85-177">Запуск приложения hello.</span><span class="sxs-lookup"><span data-stu-id="f2c85-177">Launch hello application.</span></span> 
4. <span data-ttu-id="f2c85-178">Введите имя пользователя и выберите сертификат пользователя hello, требуется toouse.</span><span class="sxs-lookup"><span data-stu-id="f2c85-178">Enter your user name, and then select hello user certificate you want toouse.</span></span> 

<span data-ttu-id="f2c85-179">Вы должны без проблем войти в систему.</span><span class="sxs-lookup"><span data-stu-id="f2c85-179">You should be successfully signed in.</span></span> 

### <a name="testing-exchange-activesync-client-applications"></a><span data-ttu-id="f2c85-180">Тестирование клиентских приложений Exchange ActiveSync</span><span class="sxs-lookup"><span data-stu-id="f2c85-180">Testing Exchange ActiveSync client applications</span></span>

<span data-ttu-id="f2c85-181">Доступные toohello приложения необходимо tooaccess Exchange ActiveSync (EAS) через сертификат проверки подлинности на основе профиля EAS, содержащий сертификат клиента hello.</span><span class="sxs-lookup"><span data-stu-id="f2c85-181">tooaccess Exchange ActiveSync (EAS) via certificate-based authentication, an EAS profile containing hello client certificate must be available toohello application.</span></span> 

<span data-ttu-id="f2c85-182">Hello профиля EAS должен содержать hello следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="f2c85-182">hello EAS profile must contain hello following information:</span></span>

- <span data-ttu-id="f2c85-183">Здравствуйте, toobe сертификат пользователя, используемый для проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="f2c85-183">hello user certificate toobe used for authentication</span></span> 

- <span data-ttu-id="f2c85-184">Конечная точка EAS Hello (например, outlook.office365.com)</span><span class="sxs-lookup"><span data-stu-id="f2c85-184">hello EAS endpoint (for example, outlook.office365.com)</span></span>

<span data-ttu-id="f2c85-185">Можно настроить и разместить на устройстве hello путем использования hello управления мобильными устройствами (MDM) как Intune, или установив сертификат hello вручную в hello профиля EAS на устройстве hello профиля EAS.</span><span class="sxs-lookup"><span data-stu-id="f2c85-185">An EAS profile can be configured and placed on hello device through hello utilization of Mobile device management (MDM) such as Intune or by manually placing hello certificate in hello EAS profile on hello device.</span></span>  

### <a name="testing-eas-client-applications-on-android"></a><span data-ttu-id="f2c85-186">Тестирование клиентских приложений EAS на Android</span><span class="sxs-lookup"><span data-stu-id="f2c85-186">Testing EAS client applications on Android</span></span>

<span data-ttu-id="f2c85-187">**Проверка подлинности сертификата tootest:**</span><span class="sxs-lookup"><span data-stu-id="f2c85-187">**tootest certificate authentication:**</span></span>  

1. <span data-ttu-id="f2c85-188">Настройка профиля EAS приложения hello, удовлетворяющее требованиям hello выше.</span><span class="sxs-lookup"><span data-stu-id="f2c85-188">Configure an EAS profile in hello application that satisfies hello requirements above.</span></span>  
2. <span data-ttu-id="f2c85-189">Откройте приложение hello и убедитесь, что почта синхронизируются.</span><span class="sxs-lookup"><span data-stu-id="f2c85-189">Open hello application, and verify that mail is synchronizing.</span></span> 

