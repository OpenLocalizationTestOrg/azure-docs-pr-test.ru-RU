---
title: "Приступая к работе с аутентификацией на основе сертификата в Azure Active Directory | Документация Майкрософт"
description: "Узнайте, как настроить в своей среде аутентификацию на основе сертификата."
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
ms.openlocfilehash: 8ebc6f2dd7502fd75ffdd4d5d68338382cb1a46b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-certificate-based-authentication-in-azure-active-directory"></a><span data-ttu-id="21622-103">Приступая к работе с аутентификацией на основе сертификата в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="21622-103">Get started with certificate-based authentication in Azure Active Directory</span></span>

<span data-ttu-id="21622-104">Аутентификация на основе сертификата позволяет Azure Active Directory выполнять аутентификацию с помощью сертификата клиента на устройстве Windows, Android или iOS при подключении учетной записи Exchange Online к:</span><span class="sxs-lookup"><span data-stu-id="21622-104">Certificate-based authentication enables you to be authenticated by Azure Active Directory with a client certificate on a Windows, Android or iOS device when connecting your Exchange online account to:</span></span> 

- <span data-ttu-id="21622-105">мобильным приложениям Office, таким как Microsoft Outlook и Microsoft Word;</span><span class="sxs-lookup"><span data-stu-id="21622-105">Office mobile applications such as Microsoft Outlook and Microsoft Word</span></span>   

- <span data-ttu-id="21622-106">клиентам Exchange ActiveSync (EAS).</span><span class="sxs-lookup"><span data-stu-id="21622-106">Exchange ActiveSync (EAS) clients</span></span> 

<span data-ttu-id="21622-107">Настройка данной функции избавляет от необходимости ввода имени пользователя и пароля в определенных почтовых клиентах и приложениях Microsoft Office на мобильных устройствах.</span><span class="sxs-lookup"><span data-stu-id="21622-107">Configuring this feature eliminates the need to enter a username and password combination into certain mail and Microsoft Office applications on your mobile device.</span></span> 

<span data-ttu-id="21622-108">В этой статье:</span><span class="sxs-lookup"><span data-stu-id="21622-108">This topic:</span></span>

- <span data-ttu-id="21622-109">Показано, как настроить и использовать аутентификацию на основе сертификата для пользователей клиентов в тарифных планах Office 365 корпоративный, бизнес, для образования и для государственных организаций США.</span><span class="sxs-lookup"><span data-stu-id="21622-109">Provides you with the steps to configure and utilize certificate-based authentication for users of tenants in Office 365 Enterprise, Business, Education, and US Government plans.</span></span> <span data-ttu-id="21622-110">В тарифных планах Office 365 China, US Government Defense и US Government Federal доступна предварительная версия этой функции.</span><span class="sxs-lookup"><span data-stu-id="21622-110">This feature is available in preview in Office 365 China, US Government Defense, and US Government Federal plans.</span></span> 

- <span data-ttu-id="21622-111">Предполагается, что у вас уже настроены [инфраструктура открытых ключей (PKI)](https://go.microsoft.com/fwlink/?linkid=841737) и [AD FS](connect/active-directory-aadconnectfed-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="21622-111">Assumes that you already have a [public key infrastructure (PKI)](https://go.microsoft.com/fwlink/?linkid=841737) and [AD FS](connect/active-directory-aadconnectfed-whatis.md) configured.</span></span>    


## <a name="requirements"></a><span data-ttu-id="21622-112">Требования</span><span class="sxs-lookup"><span data-stu-id="21622-112">Requirements</span></span>

<span data-ttu-id="21622-113">Для настройки аутентификации на основе сертификата должны выполняться следующие условия:</span><span class="sxs-lookup"><span data-stu-id="21622-113">To configure certificate-based authentication, the following must be true:</span></span>  

- <span data-ttu-id="21622-114">Аутентификация на основе сертификата (CBA) поддерживается только для браузерных приложений и собственных клиентов в федеративных средах, использующих современную аутентификацию (ADAL).</span><span class="sxs-lookup"><span data-stu-id="21622-114">Certificate-based authentication (CBA) is only supported for Federated environments for browser applications or native clients using modern authentication (ADAL).</span></span> <span data-ttu-id="21622-115">Единственным исключением является решение Exchange Active (EAS) для EXO, которое можно использовать для федеративных и управляемых учетных записей.</span><span class="sxs-lookup"><span data-stu-id="21622-115">The one exception is Exchange Active Sync (EAS) for EXO which can be used for both, federated and managed accounts.</span></span> 

- <span data-ttu-id="21622-116">Корневой центр сертификации и все промежуточные центры сертификации должны быть настроены в Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="21622-116">The root certificate authority and any intermediate certificate authorities must be configured in Azure Active Directory.</span></span>  

- <span data-ttu-id="21622-117">Каждый центр сертификации должен иметь список отзыва сертификатов (CRL), на который можно сослаться с помощью URL-адреса для Интернета.</span><span class="sxs-lookup"><span data-stu-id="21622-117">Each certificate authority must have a certificate revocation list (CRL) that can be referenced via an Internet facing URL.</span></span>  

- <span data-ttu-id="21622-118">В Azure Active Directory должен быть настроен хотя бы один центр сертификации.</span><span class="sxs-lookup"><span data-stu-id="21622-118">You must have at least one certificate authority configured in Azure Active Directory.</span></span> <span data-ttu-id="21622-119">Соответствующие действия описаны в разделе [Настройка центров сертификации](#step-2-configure-the-certificate-authorities).</span><span class="sxs-lookup"><span data-stu-id="21622-119">You can find related steps in the [Configure the certificate authorities](#step-2-configure-the-certificate-authorities) section.</span></span>  

- <span data-ttu-id="21622-120">Для клиентов Exchange ActiveSync: в сертификате клиента в поле "Альтернативное имя субъекта" в качестве значения имени субъекта или имени RFC822 должен быть указан маршрутизируемый адрес электронной почты пользователя в Exchange Online.</span><span class="sxs-lookup"><span data-stu-id="21622-120">For Exchange ActiveSync clients, the client certificate must have the user’s routable email address in Exchange online in either the Principal Name or the RFC822 Name value of the Subject Alternative Name field.</span></span> <span data-ttu-id="21622-121">Azure Active Directory сопоставляет значение RFC822 с атрибутом прокси-адреса в каталоге.</span><span class="sxs-lookup"><span data-stu-id="21622-121">Azure Active Directory maps the RFC822 value to the Proxy Address attribute in the directory.</span></span>  

- <span data-ttu-id="21622-122">Устройство клиента должно иметь доступ хотя бы к одному центру сертификации, выдающему сертификаты клиента.</span><span class="sxs-lookup"><span data-stu-id="21622-122">Your client device must have access to at least one certificate authority that issues client certificates.</span></span>  

- <span data-ttu-id="21622-123">Для аутентификации вашего клиента должен быть выдан сертификат клиента.</span><span class="sxs-lookup"><span data-stu-id="21622-123">A client certificate for client authentication must have been issued to your client.</span></span>  




## <a name="step-1-select-your-device-platform"></a><span data-ttu-id="21622-124">Шаг 1. Выбор платформы устройства</span><span class="sxs-lookup"><span data-stu-id="21622-124">Step 1: Select your device platform</span></span>

<span data-ttu-id="21622-125">При выборе платформы устройства для начала необходимо ознакомиться со следующими сведениями:</span><span class="sxs-lookup"><span data-stu-id="21622-125">As a first step, for the device platform you care about, you need to review the following:</span></span>

- <span data-ttu-id="21622-126">Поддержка мобильных приложений Office</span><span class="sxs-lookup"><span data-stu-id="21622-126">The Office mobile applications support</span></span> 
- <span data-ttu-id="21622-127">Особые требования к реализации</span><span class="sxs-lookup"><span data-stu-id="21622-127">The specific implementation requirements</span></span>  

<span data-ttu-id="21622-128">Эта информация доступна для следующих платформ устройств:</span><span class="sxs-lookup"><span data-stu-id="21622-128">The related information exists for the following device platforms:</span></span>

- [<span data-ttu-id="21622-129">Android</span><span class="sxs-lookup"><span data-stu-id="21622-129">Android</span></span>](active-directory-certificate-based-authentication-android.md)
- [<span data-ttu-id="21622-130">iOS</span><span class="sxs-lookup"><span data-stu-id="21622-130">iOS</span></span>](active-directory-certificate-based-authentication-ios.md)


## <a name="step-2-configure-the-certificate-authorities"></a><span data-ttu-id="21622-131">Шаг 2. Настройка центров сертификации</span><span class="sxs-lookup"><span data-stu-id="21622-131">Step 2: Configure the certificate authorities</span></span> 

<span data-ttu-id="21622-132">Чтобы настроить в Azure Active Directory центры сертификации, для каждого центра сертификации отправьте следующие данные:</span><span class="sxs-lookup"><span data-stu-id="21622-132">To configure your certificate authorities in Azure Active Directory, for each certificate authority, upload the following:</span></span> 

* <span data-ttu-id="21622-133">открытую часть сертификата в формате *CER* ;</span><span class="sxs-lookup"><span data-stu-id="21622-133">The public portion of the certificate, in *.cer* format</span></span> 
* <span data-ttu-id="21622-134">URL-адреса для Интернета, где находятся списки отзыва сертификатов (CRL).</span><span class="sxs-lookup"><span data-stu-id="21622-134">The Internet facing URLs where the Certificate Revocation Lists (CRLs) reside</span></span>

<span data-ttu-id="21622-135">Схема для центра сертификации выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="21622-135">The schema for a certificate authority looks as follows:</span></span> 

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

<span data-ttu-id="21622-136">Для настройки можно использовать [Azure Active Directory PowerShell версии 2](/powershell/azure/install-adv2?view=azureadps-2.0):</span><span class="sxs-lookup"><span data-stu-id="21622-136">For the configuration, you can use the [Azure Active Directory PowerShell Version 2](/powershell/azure/install-adv2?view=azureadps-2.0):</span></span>  

1. <span data-ttu-id="21622-137">Запустите Windows PowerShell с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="21622-137">Start Windows PowerShell with administrator privileges.</span></span> 
2. <span data-ttu-id="21622-138">Установите модуль Azure AD.</span><span class="sxs-lookup"><span data-stu-id="21622-138">Install the Azure AD module.</span></span> <span data-ttu-id="21622-139">Необходимо установить версию [2.0.0.33](https://www.powershellgallery.com/packages/AzureAD/2.0.0.33) или более позднюю.</span><span class="sxs-lookup"><span data-stu-id="21622-139">You need to install Version [2.0.0.33 ](https://www.powershellgallery.com/packages/AzureAD/2.0.0.33) or higher.</span></span>  
   
        Install-Module -Name AzureAD –RequiredVersion 2.0.0.33 

<span data-ttu-id="21622-140">В качестве первого шага настройки необходимо установить подключение к клиенту.</span><span class="sxs-lookup"><span data-stu-id="21622-140">As a first configuration step, you need to establish a connection with your tenant.</span></span> <span data-ttu-id="21622-141">Как только установлено подключение к клиенту, вы можете просмотреть, добавить, удалить или изменить доверенные центры сертификации, определенные в каталоге.</span><span class="sxs-lookup"><span data-stu-id="21622-141">As soon as a connection to your tenant exists, you can review, add, delete and modify the trusted certificate authorities that are defined in your directory.</span></span> 

### <a name="connect"></a><span data-ttu-id="21622-142">Подключение</span><span class="sxs-lookup"><span data-stu-id="21622-142">Connect</span></span>

<span data-ttu-id="21622-143">Чтобы установить подключение к клиенту, используйте командлет [Connect-AzureAD](/powershell/module/azuread/connect-azuread?view=azureadps-2.0):</span><span class="sxs-lookup"><span data-stu-id="21622-143">To establish a connection with your tenant, use the [Connect-AzureAD](/powershell/module/azuread/connect-azuread?view=azureadps-2.0) cmdlet:</span></span>

    Connect-AzureAD 


### <a name="retrieve"></a><span data-ttu-id="21622-144">Получение</span><span class="sxs-lookup"><span data-stu-id="21622-144">Retrieve</span></span> 

<span data-ttu-id="21622-145">Чтобы получить доверенные центры сертификации, определенные в каталоге, используйте командлет [Get-AzureADTrustedCertificateAuthority](/powershell/module/azuread/get-azureadtrustedcertificateauthority?view=azureadps-2.0):</span><span class="sxs-lookup"><span data-stu-id="21622-145">To retrieve the trusted certificate authorities that are defined in your directory, use the [Get-AzureADTrustedCertificateAuthority](/powershell/module/azuread/get-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet.</span></span> 

    Get-AzureADTrustedCertificateAuthority 
 

### <a name="add"></a><span data-ttu-id="21622-146">Добавить</span><span class="sxs-lookup"><span data-stu-id="21622-146">Add</span></span>

<span data-ttu-id="21622-147">Чтобы создать доверенный центр сертификации, используйте командлет [New-AzureADTrustedCertificateAuthority](/powershell/module/azuread/new-azureadtrustedcertificateauthority?view=azureadps-2.0) и задайте правильное значение атрибута **crlDistributionPoint**.</span><span class="sxs-lookup"><span data-stu-id="21622-147">To create a trusted certificate authority, use the [New-AzureADTrustedCertificateAuthority](/powershell/module/azuread/new-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet and set the **crlDistributionPoint** attribute to a correct value:</span></span> 
   
    $cert=Get-Content -Encoding byte "[LOCATION OF THE CER FILE]" 
    $new_ca=New-Object -TypeName Microsoft.Open.AzureAD.Model.CertificateAuthorityInformation 
    $new_ca.AuthorityType=0 
    $new_ca.TrustedCertificate=$cert 
    $new_ca.crlDistributionPoint=”<CRL Distribution URL>”
    New-AzureADTrustedCertificateAuthority -CertificateAuthorityInformation $new_ca 


### <a name="remove"></a><span data-ttu-id="21622-148">Удалить</span><span class="sxs-lookup"><span data-stu-id="21622-148">Remove</span></span>

<span data-ttu-id="21622-149">Чтобы удалить доверенный центр сертификации, используйте командлет [Remove-AzureADTrustedCertificateAuthority](/powershell/module/azuread/remove-azureadtrustedcertificateauthority?view=azureadps-2.0):</span><span class="sxs-lookup"><span data-stu-id="21622-149">To remove a trusted certificate authority, use the [Remove-AzureADTrustedCertificateAuthority](/powershell/module/azuread/remove-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet:</span></span>
   
    $c=Get-AzureADTrustedCertificateAuthority 
    Remove-AzureADTrustedCertificateAuthority -CertificateAuthorityInformation $c[2] 


### <a name="modfiy"></a><span data-ttu-id="21622-150">Изменение</span><span class="sxs-lookup"><span data-stu-id="21622-150">Modfiy</span></span>

<span data-ttu-id="21622-151">Чтобы изменить доверенный центр сертификации, используйте командлет [Set-AzureADTrustedCertificateAuthority](/powershell/module/azuread/set-azureadtrustedcertificateauthority?view=azureadps-2.0):</span><span class="sxs-lookup"><span data-stu-id="21622-151">To modify a trusted certificate authority, use the [Set-AzureADTrustedCertificateAuthority](/powershell/module/azuread/set-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet:</span></span>

    $c=Get-AzureADTrustedCertificateAuthority 
    $c[0].AuthorityType=1 
    Set-AzureADTrustedCertificateAuthority -CertificateAuthorityInformation $c[0] 


## <a name="step-3-configure-revocation"></a><span data-ttu-id="21622-152">Шаг 3. Настройка отзыва</span><span class="sxs-lookup"><span data-stu-id="21622-152">Step 3: Configure revocation</span></span>

<span data-ttu-id="21622-153">Чтобы отозвать сертификат клиента, Azure Active Directory извлекает список отзыва сертификатов (CRL) из URL-адресов, переданных вместе с информацией центра сертификации, и кэширует его.</span><span class="sxs-lookup"><span data-stu-id="21622-153">To revoke a client certificate, Azure Active Directory fetches the certificate revocation list (CRL) from the URLs uploaded as part of certificate authority information and caches it.</span></span> <span data-ttu-id="21622-154">Метка времени последней публикации (свойство**Дата вступления в силу** ) в списке отзыва сертификатов обеспечивает допустимость этого списка.</span><span class="sxs-lookup"><span data-stu-id="21622-154">The last publish timestamp (**Effective Date** property) in the CRL is used to ensure the CRL is still valid.</span></span> <span data-ttu-id="21622-155">Список отзыва сертификатов периодически опрашивается для отзыва доступа к сертификатам, которые числятся в этом списке.</span><span class="sxs-lookup"><span data-stu-id="21622-155">The CRL is periodically referenced to revoke access to certificates that are a part of the list.</span></span>

<span data-ttu-id="21622-156">Если требуется более быстрый отзыв (например, если пользователь потерял устройство), то маркер авторизации пользователя можно сделать недействительным.</span><span class="sxs-lookup"><span data-stu-id="21622-156">If a more instant revocation is required (for example, if a user loses a device), the authorization token of the user can be invalidated.</span></span> <span data-ttu-id="21622-157">Чтобы сделать маркер авторизации недействительным, с помощью Windows PowerShell определите поле **StsRefreshTokenValidFrom** для этого пользователя.</span><span class="sxs-lookup"><span data-stu-id="21622-157">To invalidate the authorization token, set the **StsRefreshTokenValidFrom** field for this particular user using Windows PowerShell.</span></span> <span data-ttu-id="21622-158">Поле **StsRefreshTokenValidFrom** необходимо обновить для каждого пользователя, доступ для которого будет отозван.</span><span class="sxs-lookup"><span data-stu-id="21622-158">You must update the **StsRefreshTokenValidFrom** field for each user you want to revoke access for.</span></span>

<span data-ttu-id="21622-159">Чтобы отзыв оставался в силе, для свойства **Дата вступления в силу** списка отзыва сертификатов необходимо указать дату, которая наступит после даты, заданной в поле **StsRefreshTokenValidFrom**, а также убедиться, что этот сертификат есть в списке отзыва сертификатов.</span><span class="sxs-lookup"><span data-stu-id="21622-159">To ensure that the revocation persists, you must set the **Effective Date** of the CRL to a date after the value set by **StsRefreshTokenValidFrom** and ensure the certificate in question is in the CRL.</span></span>

<span data-ttu-id="21622-160">Ниже описан процесс обновления и аннулирования маркера авторизации с помощью поля **StsRefreshTokenValidFrom** .</span><span class="sxs-lookup"><span data-stu-id="21622-160">The following steps outline the process for updating and invalidating the authorization token by setting the **StsRefreshTokenValidFrom** field.</span></span> 

<span data-ttu-id="21622-161">**Чтобы настроить отзыв сертификата, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="21622-161">**To configure revocation:**</span></span> 

1. <span data-ttu-id="21622-162">Используя учетные данные администратора, подключитесь к службе MSOL:</span><span class="sxs-lookup"><span data-stu-id="21622-162">Connect with admin credentials to the MSOL service:</span></span> 
   
        $msolcred = get-credential 
        connect-msolservice -credential $msolcred 

2. <span data-ttu-id="21622-163">Получите текущее значение StsRefreshTokensValidFrom для пользователя:</span><span class="sxs-lookup"><span data-stu-id="21622-163">Retrieve the current StsRefreshTokensValidFrom value for a user:</span></span> 
   
        $user = Get-MsolUser -UserPrincipalName test@yourdomain.com` 
        $user.StsRefreshTokensValidFrom 

3. <span data-ttu-id="21622-164">Настройте новое значение StsRefreshTokensValidFrom для пользователя, равное текущей метке времени:</span><span class="sxs-lookup"><span data-stu-id="21622-164">Configure a new StsRefreshTokensValidFrom value for the user equal to the current timestamp:</span></span> 
   
        Set-MsolUser -UserPrincipalName test@yourdomain.com -StsRefreshTokensValidFrom ("03/05/2016")

<span data-ttu-id="21622-165">Задаваемая дата должна быть в будущем.</span><span class="sxs-lookup"><span data-stu-id="21622-165">The date you set must be in the future.</span></span> <span data-ttu-id="21622-166">Если дата не в будущем, свойство **StsRefreshTokensValidFrom** не будет задано.</span><span class="sxs-lookup"><span data-stu-id="21622-166">If the date is not in the future, the **StsRefreshTokensValidFrom** property is not set.</span></span> <span data-ttu-id="21622-167">Если дата в будущем, для **StsRefreshTokensValidFrom** задается актуальное время (не дата, указанная командой Set-MsolUser).</span><span class="sxs-lookup"><span data-stu-id="21622-167">If the date is in the future, **StsRefreshTokensValidFrom** is set to the current time (not the date indicated by Set-MsolUser command).</span></span> 


## <a name="step-4-test-your-configuration"></a><span data-ttu-id="21622-168">Шаг 4. Тестирование конфигурации</span><span class="sxs-lookup"><span data-stu-id="21622-168">Step 4: Test your configuration</span></span>

### <a name="testing-your-certificate"></a><span data-ttu-id="21622-169">Тестирование сертификата</span><span class="sxs-lookup"><span data-stu-id="21622-169">Testing your certificate</span></span>

<span data-ttu-id="21622-170">В качестве первой проверки конфигурации попытайтесь войти в [Outlook Web Access](https://outlook.office365.com) или [SharePoint Online](https://microsoft.sharepoint.com), используя **браузер на устройстве**.</span><span class="sxs-lookup"><span data-stu-id="21622-170">As a first configuration test, you should try to sign in to [Outlook Web Access](https://outlook.office365.com) or [SharePoint Online](https://microsoft.sharepoint.com) using your **on-device browser**.</span></span>

<span data-ttu-id="21622-171">Успешный вход подтверждает, что:</span><span class="sxs-lookup"><span data-stu-id="21622-171">If your sign-in is successful, then you know that:</span></span>

- <span data-ttu-id="21622-172">для тестируемого устройства подготовлен сертификат пользователя;</span><span class="sxs-lookup"><span data-stu-id="21622-172">The user certificate has been provisioned to your test device</span></span>
- <span data-ttu-id="21622-173">службы AD FS настроены правильно.</span><span class="sxs-lookup"><span data-stu-id="21622-173">AD FS is configured correctly</span></span>  


### <a name="testing-office-mobile-applications"></a><span data-ttu-id="21622-174">Тестирование мобильных приложений Office</span><span class="sxs-lookup"><span data-stu-id="21622-174">Testing Office mobile applications</span></span>

<span data-ttu-id="21622-175">**Чтобы протестировать аутентификацию на основе сертификата в мобильном приложении Office, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="21622-175">**To test certificate-based authentication on your mobile Office application:**</span></span> 

1. <span data-ttu-id="21622-176">На тестируемом устройстве установите мобильное приложение Office (например, OneDrive).</span><span class="sxs-lookup"><span data-stu-id="21622-176">On your test device, install an Office mobile application (e.g., OneDrive).</span></span>
3. <span data-ttu-id="21622-177">Запустите приложение.</span><span class="sxs-lookup"><span data-stu-id="21622-177">Launch the application.</span></span> 
4. <span data-ttu-id="21622-178">Введите имя пользователя, а затем выберите сертификат пользователя, который хотите использовать.</span><span class="sxs-lookup"><span data-stu-id="21622-178">Enter your user name, and then select the user certificate you want to use.</span></span> 

<span data-ttu-id="21622-179">Вы должны без проблем войти в систему.</span><span class="sxs-lookup"><span data-stu-id="21622-179">You should be successfully signed in.</span></span> 

### <a name="testing-exchange-activesync-client-applications"></a><span data-ttu-id="21622-180">Тестирование клиентских приложений Exchange ActiveSync</span><span class="sxs-lookup"><span data-stu-id="21622-180">Testing Exchange ActiveSync client applications</span></span>

<span data-ttu-id="21622-181">Для доступа к Exchange ActiveSync (EAS) с использованием аутентификации на основе сертификата приложению должен быть доступен профиль EAS, содержащий сертификат клиента.</span><span class="sxs-lookup"><span data-stu-id="21622-181">To access Exchange ActiveSync (EAS) via certificate-based authentication, an EAS profile containing the client certificate must be available to the application.</span></span> 

<span data-ttu-id="21622-182">В профиле EAS должны содержаться следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="21622-182">The EAS profile must contain the following information:</span></span>

- <span data-ttu-id="21622-183">сертификат пользователя, который будет использоваться для аутентификации;</span><span class="sxs-lookup"><span data-stu-id="21622-183">The user certificate to be used for authentication</span></span> 

- <span data-ttu-id="21622-184">конечная точка EAS (например, outlook.office365.com).</span><span class="sxs-lookup"><span data-stu-id="21622-184">The EAS endpoint (for example, outlook.office365.com)</span></span>

<span data-ttu-id="21622-185">Профиль EAS можно настроить и поместить на устройство с помощью системы управления мобильными устройствами (MDM), такой как Intune, либо вручную поместить сертификат в профиль EAS на устройстве.</span><span class="sxs-lookup"><span data-stu-id="21622-185">An EAS profile can be configured and placed on the device through the utilization of Mobile device management (MDM) such as Intune or by manually placing the certificate in the EAS profile on the device.</span></span>  

### <a name="testing-eas-client-applications-on-android"></a><span data-ttu-id="21622-186">Тестирование клиентских приложений EAS на Android</span><span class="sxs-lookup"><span data-stu-id="21622-186">Testing EAS client applications on Android</span></span>

<span data-ttu-id="21622-187">**Чтобы протестировать аутентификацию на основе сертификата, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="21622-187">**To test certificate authentication:**</span></span>  

1. <span data-ttu-id="21622-188">Настройте профиль EAS в приложении, удовлетворяющем изложенным выше требованиям.</span><span class="sxs-lookup"><span data-stu-id="21622-188">Configure an EAS profile in the application that satisfies the requirements above.</span></span>  
2. <span data-ttu-id="21622-189">Откройте приложение и убедитесь, что почта синхронизируется.</span><span class="sxs-lookup"><span data-stu-id="21622-189">Open the application, and verify that mail is synchronizing.</span></span> 

