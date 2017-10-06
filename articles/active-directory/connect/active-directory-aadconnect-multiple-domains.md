---
title: "Подключение нескольких доменов aaaAzure AD"
description: "В этом документе описываются процедуры установки и настройки нескольких доменов верхнего уровня в Office 365 и Azure AD."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: curtand
ms.assetid: 5595fb2f-2131-4304-8a31-c52559128ea4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 91d87875ceacee4e34f132938e4bb0294fb954e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="multiple-domain-support-for-federating-with-azure-ad"></a><span data-ttu-id="669d1-103">Поддержка нескольких доменов для федерации с Azure AD</span><span class="sxs-lookup"><span data-stu-id="669d1-103">Multiple Domain Support for Federating with Azure AD</span></span>
<span data-ttu-id="669d1-104">Hello следующей документации содержатся рекомендации о том, как toouse нескольких доменов верхнего уровня и поддоменам, при включении в федерацию с Office 365 или Azure AD доменов.</span><span class="sxs-lookup"><span data-stu-id="669d1-104">hello following documentation provides guidance on how toouse multiple top-level domains and sub-domains when federating with Office 365 or Azure AD domains.</span></span>

## <a name="multiple-top-level-domain-support"></a><span data-ttu-id="669d1-105">Поддержка нескольких доменов верхнего уровня</span><span class="sxs-lookup"><span data-stu-id="669d1-105">Multiple top-level domain support</span></span>
<span data-ttu-id="669d1-106">Для создания федерации нескольких доменов верхнего уровня с Azure AD необходимо выполнить некоторые дополнительные настройки, которые не требуются при создании федерации с одним доменом верхнего уровня.</span><span class="sxs-lookup"><span data-stu-id="669d1-106">Federating multiple, top-level domains with Azure AD requires some additional configuration that is not required when federating with one top-level domain.</span></span>

<span data-ttu-id="669d1-107">Если домен включена в федерацию с Azure AD, несколько свойств, задаются на hello домена в Azure.</span><span class="sxs-lookup"><span data-stu-id="669d1-107">When a domain is federated with Azure AD, several properties are set on hello domain in Azure.</span></span>  <span data-ttu-id="669d1-108">Важным свойством является IssuerUri.</span><span class="sxs-lookup"><span data-stu-id="669d1-108">One important one is IssuerUri.</span></span>  <span data-ttu-id="669d1-109">Это URI, который используется с Azure AD tooidentify домен hello, hello маркера связан с.</span><span class="sxs-lookup"><span data-stu-id="669d1-109">This is a URI that is used by Azure AD tooidentify hello domain that hello token is associated with.</span></span>  <span data-ttu-id="669d1-110">Hello URI не требует tooresolve tooanything, но он должен быть допустимым URI.</span><span class="sxs-lookup"><span data-stu-id="669d1-110">hello URI doesn’t need tooresolve tooanything but it must be a valid URI.</span></span>  <span data-ttu-id="669d1-111">По умолчанию Azure AD устанавливает значение toohello hello идентификатор службы федерации в вашей локальной AD FS конфигурации.</span><span class="sxs-lookup"><span data-stu-id="669d1-111">By default, Azure AD sets this toohello value of hello federation service identifier in your on-premises AD FS configuration.</span></span>

> [!NOTE]
> <span data-ttu-id="669d1-112">Идентификатор службы федерации Hello является URI, который уникально идентифицирует службы федерации.</span><span class="sxs-lookup"><span data-stu-id="669d1-112">hello federation service identifier is a URI that uniquely identifies a federation service.</span></span>  <span data-ttu-id="669d1-113">Служба федерации Hello является экземпляром AD FS, которые работают как службы маркеров безопасности hello.</span><span class="sxs-lookup"><span data-stu-id="669d1-113">hello federation service is an instance of AD FS that functions as hello security token service.</span></span> 
> 
> 

<span data-ttu-id="669d1-114">Вы можете просмотреть IssuerUri с помощью команды PowerShell hello `Get-MsolDomainFederationSettings -DomainName <your domain>`.</span><span class="sxs-lookup"><span data-stu-id="669d1-114">You can vew IssuerUri by using hello PowerShell command `Get-MsolDomainFederationSettings -DomainName <your domain>`.</span></span>

![Get-MsolDomainFederationSettings](./media/active-directory-multiple-domains/MsolDomainFederationSettings.png)

<span data-ttu-id="669d1-116">Проблема возникает, когда мы хотим tooadd несколько доменов верхнего уровня.</span><span class="sxs-lookup"><span data-stu-id="669d1-116">A problem arises when we want tooadd more than one top-level domain.</span></span>  <span data-ttu-id="669d1-117">Например, предположим, что у вас настроена федерация между Azure AD и локальной средой.</span><span class="sxs-lookup"><span data-stu-id="669d1-117">For example, let's say you have setup federation between Azure AD and your on-premises environment.</span></span>  <span data-ttu-id="669d1-118">В данном документе я использую домен bmcontoso.com.  Теперь я добавил второй домен верхнего уровня bmfabrikam.com.</span><span class="sxs-lookup"><span data-stu-id="669d1-118">For this document I am using bmcontoso.com.  Now I have added a second, top-level domain, bmfabrikam.com.</span></span>

![Домены](./media/active-directory-multiple-domains/domains.png)

<span data-ttu-id="669d1-120">Если мы будем стараться федеративного домена нашей bmfabrikam.com toobe tooconvert, мы сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="669d1-120">When we attempt tooconvert our bmfabrikam.com domain toobe federated, we receive an error.</span></span>  <span data-ttu-id="669d1-121">Hello причиной этого является Azure AD имеет ограничение, которое не допускает hello IssuerUri свойство toohave hello одинаковое значение для более чем одного домена.</span><span class="sxs-lookup"><span data-stu-id="669d1-121">hello reason for this is, Azure AD has a constraint that does not allow hello IssuerUri property toohave hello same value for more than one domain.</span></span>  

![Ошибка федерации](./media/active-directory-multiple-domains/error.png)

### <a name="supportmultipledomain-parameter"></a><span data-ttu-id="669d1-123">Параметр SupportMultipleDomain</span><span class="sxs-lookup"><span data-stu-id="669d1-123">SupportMultipleDomain Parameter</span></span>
<span data-ttu-id="669d1-124">tooworkaround это, мы должны tooadd другой IssuerUri, это можно сделать с помощью hello `-SupportMultipleDomain` параметра.</span><span class="sxs-lookup"><span data-stu-id="669d1-124">tooworkaround this, we need tooadd a different IssuerUri which can be done by using hello `-SupportMultipleDomain` parameter.</span></span>  <span data-ttu-id="669d1-125">Этот параметр используется с hello следующие командлеты:</span><span class="sxs-lookup"><span data-stu-id="669d1-125">This parameter is used with hello following cmdlets:</span></span>

* `New-MsolFederatedDomain`
* `Convert-MsolDomaintoFederated`
* `Update-MsolFederatedDomain`

<span data-ttu-id="669d1-126">Этот параметр позволяет настроить hello IssuerUri таким образом, чтобы он основан на hello имя домена hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="669d1-126">This parameter makes Azure AD configure hello IssuerUri so that it is based on hello name of hello domain.</span></span>  <span data-ttu-id="669d1-127">Оно будет уникальным в различных каталогах в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="669d1-127">This will be unique across directories in Azure AD.</span></span>  <span data-ttu-id="669d1-128">Использование параметра hello успешно позволяет toocomplete команды PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="669d1-128">Using hello parameter allows hello PowerShell command toocomplete successfully.</span></span>

![Ошибка федерации](./media/active-directory-multiple-domains/convert.png)

<span data-ttu-id="669d1-130">Просмотрев параметры hello наш новый домен bmfabrikam.com можно увидеть hello следующее:</span><span class="sxs-lookup"><span data-stu-id="669d1-130">Looking at hello settings of our new bmfabrikam.com domain you can see hello following:</span></span>

![Ошибка федерации](./media/active-directory-multiple-domains/settings.png)

<span data-ttu-id="669d1-132">Обратите внимание, что `-SupportMultipleDomain` не изменяет hello других конечных точек, настроенных по-прежнему настроить службы федерации tooour toopoint на adfs.bmcontoso.com.</span><span class="sxs-lookup"><span data-stu-id="669d1-132">Note that `-SupportMultipleDomain` does not change hello other endpoints which are still configured toopoint tooour federation service on adfs.bmcontoso.com.</span></span>

<span data-ttu-id="669d1-133">Также, `-SupportMultipleDomain` does его применения, система hello AD FS включает hello правильное значение издателя в маркеры, выпущенные для Azure AD.</span><span class="sxs-lookup"><span data-stu-id="669d1-133">Another thing that `-SupportMultipleDomain` does is that it ensures that hello AD FS system includes hello proper Issuer value in tokens issued for Azure AD.</span></span> <span data-ttu-id="669d1-134">Это делается путем установки hello доменной части hello пользователей UPN и установка этого параметра hello в в качестве домена hello IssuerUri, т. е. суффикс https://{upn} / adfs/services/trust.</span><span class="sxs-lookup"><span data-stu-id="669d1-134">It does this by taking hello domain portion of hello users UPN and setting this as hello domain in hello IssuerUri, i.e. https://{upn suffix}/adfs/services/trust.</span></span> 

<span data-ttu-id="669d1-135">Таким образом во время проверки подлинности tooAzure AD или Office 365, элемент IssuerUri hello в токен пользователя hello — используется toolocate hello домена в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="669d1-135">Thus during authentication tooAzure AD or Office 365, hello IssuerUri element in hello user’s token is used toolocate hello domain in Azure AD.</span></span>  <span data-ttu-id="669d1-136">Если не удается найти совпадения, будут выполнены проверки подлинности hello.</span><span class="sxs-lookup"><span data-stu-id="669d1-136">If a match cannot be found hello authentication will fail.</span></span> 

<span data-ttu-id="669d1-137">Например, если имя участника-пользователя пользователь должен bsimon@bmcontoso.com, элемент IssuerUri hello проблемам hello токена службы федерации Active Directory будет иметь значение toohttp://bmcontoso.com/adfs/services/trust.</span><span class="sxs-lookup"><span data-stu-id="669d1-137">For example, if a user’s UPN is bsimon@bmcontoso.com, hello IssuerUri element in hello token AD FS issues will be set toohttp://bmcontoso.com/adfs/services/trust.</span></span> <span data-ttu-id="669d1-138">Это будет соответствовать конфигурации hello Azure AD, а проверка подлинности выполняется успешно.</span><span class="sxs-lookup"><span data-stu-id="669d1-138">This will match hello Azure AD configuration, and authentication will succeed.</span></span>

<span data-ttu-id="669d1-139">Hello Вот правила настраиваемые утверждения hello, реализующего следующую логику:</span><span class="sxs-lookup"><span data-stu-id="669d1-139">hello following is hello customized claim rule that implements this logic:</span></span>

    c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, ".+@(?<domain>.+)", "http://${domain}/adfs/services/trust/"));


> [!IMPORTANT]
> <span data-ttu-id="669d1-140">В порядке toouse hello - SupportMultipleDomain переключение при попытке tooadd новый или преобразовать уже добавленных доменов, вы должны toohave установки вашего toosupport федеративного отношения доверия их изначально.</span><span class="sxs-lookup"><span data-stu-id="669d1-140">In order toouse hello -SupportMultipleDomain switch when attempting tooadd new or convert already added domains, you need toohave setup your federated trust toosupport them originally.</span></span>  
> 
> 

## <a name="how-tooupdate-hello-trust-between-ad-fs-and-azure-ad"></a><span data-ttu-id="669d1-141">Как tooupdate hello доверие между AD FS и Azure AD</span><span class="sxs-lookup"><span data-stu-id="669d1-141">How tooupdate hello trust between AD FS and Azure AD</span></span>
<span data-ttu-id="669d1-142">Если вы не настроили hello федеративного отношения доверия между AD FS и имеющимся экземпляром Azure AD, может потребоваться toore-создание этого отношения доверия.</span><span class="sxs-lookup"><span data-stu-id="669d1-142">If you did not setup hello federated trust between AD FS and your instance of Azure AD, you may need toore-create this trust.</span></span>  <span data-ttu-id="669d1-143">Это происходит потому, когда это изначально программу установки без hello `-SupportMultipleDomain` , hello IssuerUri имеет параметр со значением по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="669d1-143">This is because, when it is originally setup without hello `-SupportMultipleDomain` parameter, hello IssuerUri is set with hello default value.</span></span>  <span data-ttu-id="669d1-144">В hello снимке экрана ниже вы увидите набора toohttps://adfs.bmcontoso.com/adfs/services/trust hello IssuerUri.</span><span class="sxs-lookup"><span data-stu-id="669d1-144">In hello screenshot below you can see hello IssuerUri is set toohttps://adfs.bmcontoso.com/adfs/services/trust.</span></span>

<span data-ttu-id="669d1-145">Поэтому теперь, если мы добавлен новый домен в портале hello Azure AD, а затем tooconvert его с помощью `Convert-MsolDomaintoFederated -DomainName <your domain>`, мы получаем hello следующая ошибка.</span><span class="sxs-lookup"><span data-stu-id="669d1-145">So now, if we have successfully added an new domain in hello Azure AD portal and then attempt tooconvert it using `Convert-MsolDomaintoFederated -DomainName <your domain>`, we get hello following error.</span></span>

![Ошибка федерации](./media/active-directory-multiple-domains/trust1.png)

<span data-ttu-id="669d1-147">Если при попытке tooadd hello `-SupportMultipleDomain` коммутатора, мы получаем hello следующая ошибка:</span><span class="sxs-lookup"><span data-stu-id="669d1-147">If you try tooadd hello `-SupportMultipleDomain` switch we will receive hello following error:</span></span>

![Ошибка федерации](./media/active-directory-multiple-domains/trust2.png)

<span data-ttu-id="669d1-149">Просто попытки toorun `Update-MsolFederatedDomain -DomainName <your domain> -SupportMultipleDomain` на hello исходного домена приводит к ошибке.</span><span class="sxs-lookup"><span data-stu-id="669d1-149">Simply trying toorun `Update-MsolFederatedDomain -DomainName <your domain> -SupportMultipleDomain` on hello original domain will also result in an error.</span></span>

![Ошибка федерации](./media/active-directory-multiple-domains/trust3.png)

<span data-ttu-id="669d1-151">Выполните шаги hello ниже tooadd дополнительного домена верхнего уровня.</span><span class="sxs-lookup"><span data-stu-id="669d1-151">Use hello steps below tooadd an additional top-level domain.</span></span>  <span data-ttu-id="669d1-152">Если домен уже добавлен и не использовался hello `-SupportMultipleDomain` параметр start hello шагам для удаление и обновление вашего исходного домена.</span><span class="sxs-lookup"><span data-stu-id="669d1-152">If you have already added a domain and did not use hello `-SupportMultipleDomain` parameter start with hello steps for removing and updating your original domain.</span></span>  <span data-ttu-id="669d1-153">Если вы не добавили домен верхнего уровня еще можно начать с hello шаги для добавления домена, с помощью PowerShell Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="669d1-153">If you have not added a top-level domain yet you can start with hello steps for adding a domain using PowerShell of Azure AD Connect.</span></span>

<span data-ttu-id="669d1-154">Используйте следующие шаги tooremove hello Microsoft Online доверия hello и обновление вашего исходного домена.</span><span class="sxs-lookup"><span data-stu-id="669d1-154">Use hello following steps tooremove hello Microsoft Online trust and update your original domain.</span></span>

1. <span data-ttu-id="669d1-155">На сервере федерации AD FS откройте **Управление AD FS**</span><span class="sxs-lookup"><span data-stu-id="669d1-155">On your AD FS federation server open **AD FS Management.**</span></span> 
2. <span data-ttu-id="669d1-156">Hello левой части окна разверните **отношения доверия** и **доверия с проверяющей стороной**</span><span class="sxs-lookup"><span data-stu-id="669d1-156">On hello left, expand **Trust Relationships** and **Relying Party Trusts**</span></span>
3. <span data-ttu-id="669d1-157">На правом hello, удалите hello **Microsoft Office 365 Identity Platform** входа.</span><span class="sxs-lookup"><span data-stu-id="669d1-157">On hello right, delete hello **Microsoft Office 365 Identity Platform** entry.</span></span>
   <span data-ttu-id="669d1-158">![Удалить Microsoft Online](./media/active-directory-multiple-domains/trust4.png)</span><span class="sxs-lookup"><span data-stu-id="669d1-158">![Remove Microsoft Online](./media/active-directory-multiple-domains/trust4.png)</span></span>
4. <span data-ttu-id="669d1-159">На компьютере, где [Azure Active Directory модуля для Windows PowerShell](https://msdn.microsoft.com/library/azure/jj151815.aspx) на следующей hello: `$cred=Get-Credential`.</span><span class="sxs-lookup"><span data-stu-id="669d1-159">On a machine that has [Azure Active Directory Module for Windows PowerShell](https://msdn.microsoft.com/library/azure/jj151815.aspx) installed on it run hello following: `$cred=Get-Credential`.</span></span>  
5. <span data-ttu-id="669d1-160">Введите hello пользователя и пароль глобального администратора для домена Azure AD hello федеративные отношения с</span><span class="sxs-lookup"><span data-stu-id="669d1-160">Enter hello username and password of a global administrator for hello Azure AD domain you are federating with</span></span>
6. <span data-ttu-id="669d1-161">В PowerShell введите `Connect-MsolService -Credential $cred`</span><span class="sxs-lookup"><span data-stu-id="669d1-161">In PowerShell enter `Connect-MsolService -Credential $cred`</span></span>
7. <span data-ttu-id="669d1-162">В PowerShell введите `Update-MSOLFederatedDomain -DomainName <Federated Domain Name> -SupportMultipleDomain`.</span><span class="sxs-lookup"><span data-stu-id="669d1-162">In PowerShell enter `Update-MSOLFederatedDomain -DomainName <Federated Domain Name> -SupportMultipleDomain`.</span></span>  <span data-ttu-id="669d1-163">Это необходимо для hello исходного домена.</span><span class="sxs-lookup"><span data-stu-id="669d1-163">This is for hello original domain.</span></span>  <span data-ttu-id="669d1-164">Поэтому использование hello выше домены, которые было бы:`Update-MsolFederatedDomain -DomainName bmcontoso.com -SupportMultipleDomain`</span><span class="sxs-lookup"><span data-stu-id="669d1-164">So using hello above domains it would be:  `Update-MsolFederatedDomain -DomainName bmcontoso.com -SupportMultipleDomain`</span></span>

<span data-ttu-id="669d1-165">Используйте следующие шаги tooadd hello новый домен верхнего уровня с помощью PowerShell hello</span><span class="sxs-lookup"><span data-stu-id="669d1-165">Use hello following steps tooadd hello new top-level domain using PowerShell</span></span>

1. <span data-ttu-id="669d1-166">На компьютере, где [Azure Active Directory модуля для Windows PowerShell](https://msdn.microsoft.com/library/azure/jj151815.aspx) на следующей hello: `$cred=Get-Credential`.</span><span class="sxs-lookup"><span data-stu-id="669d1-166">On a machine that has [Azure Active Directory Module for Windows PowerShell](https://msdn.microsoft.com/library/azure/jj151815.aspx) installed on it run hello following: `$cred=Get-Credential`.</span></span>  
2. <span data-ttu-id="669d1-167">Введите hello пользователя и пароль глобального администратора для домена Azure AD hello федеративные отношения с</span><span class="sxs-lookup"><span data-stu-id="669d1-167">Enter hello username and password of a global administrator for hello Azure AD domain you are federating with</span></span>
3. <span data-ttu-id="669d1-168">В PowerShell введите `Connect-MsolService -Credential $cred`</span><span class="sxs-lookup"><span data-stu-id="669d1-168">In PowerShell enter `Connect-MsolService -Credential $cred`</span></span>
4. <span data-ttu-id="669d1-169">В PowerShell введите `New-MsolFederatedDomain –SupportMultipleDomain –DomainName`</span><span class="sxs-lookup"><span data-stu-id="669d1-169">In PowerShell enter `New-MsolFederatedDomain –SupportMultipleDomain –DomainName`</span></span>

<span data-ttu-id="669d1-170">Используйте следующие шаги tooadd hello новый домен верхнего уровня с помощью Azure AD Connect hello.</span><span class="sxs-lookup"><span data-stu-id="669d1-170">Use hello following steps tooadd hello new top-level domain using Azure AD Connect.</span></span>

1. <span data-ttu-id="669d1-171">Запустите Azure AD Connect с рабочего стола hello или меню «Пуск»</span><span class="sxs-lookup"><span data-stu-id="669d1-171">Launch Azure AD Connect from hello desktop or start menu</span></span>
2. <span data-ttu-id="669d1-172">Выберите "Добавить дополнительный домен Azure AD" ![Добавить дополнительный домен Azure AD](./media/active-directory-multiple-domains/add1.png).</span><span class="sxs-lookup"><span data-stu-id="669d1-172">Choose “Add an additional Azure AD Domain” ![Add an additional Azure AD domain](./media/active-directory-multiple-domains/add1.png)</span></span>
3. <span data-ttu-id="669d1-173">Введите учетные данные Azure AD и Active Directory.</span><span class="sxs-lookup"><span data-stu-id="669d1-173">Enter your Azure AD and Active Directory credentials</span></span>
4. <span data-ttu-id="669d1-174">Выберите второй домен hello нужно tooconfigure для федерации.</span><span class="sxs-lookup"><span data-stu-id="669d1-174">Select hello second domain you wish tooconfigure for federation.</span></span>
   <span data-ttu-id="669d1-175">![Добавить дополнительный домен Azure AD](./media/active-directory-multiple-domains/add2.png)</span><span class="sxs-lookup"><span data-stu-id="669d1-175">![Add an additional Azure AD domain](./media/active-directory-multiple-domains/add2.png)</span></span>
5. <span data-ttu-id="669d1-176">Нажмите "Установить".</span><span class="sxs-lookup"><span data-stu-id="669d1-176">Click Install</span></span>

### <a name="verify-hello-new-top-level-domain"></a><span data-ttu-id="669d1-177">Проверьте hello новый домен верхнего уровня</span><span class="sxs-lookup"><span data-stu-id="669d1-177">Verify hello new top-level domain</span></span>
<span data-ttu-id="669d1-178">С помощью команды PowerShell hello `Get-MsolDomainFederationSettings -DomainName <your domain>`можно просмотреть IssuerUri обновить hello.</span><span class="sxs-lookup"><span data-stu-id="669d1-178">By using hello PowerShell command `Get-MsolDomainFederationSettings -DomainName <your domain>`you can view hello updated IssuerUri.</span></span>  <span data-ttu-id="669d1-179">Hello снимке экрана показано hello параметры федерации были обновлены на нашем исходного домена http://bmcontoso.com/adfs/services/trust</span><span class="sxs-lookup"><span data-stu-id="669d1-179">hello screenshot below shows hello federation settings were updated on our original domain http://bmcontoso.com/adfs/services/trust</span></span>

![Get-MsolDomainFederationSettings](./media/active-directory-multiple-domains/MsolDomainFederationSettings.png)

<span data-ttu-id="669d1-181">И hello IssuerUri на нашем нового домена было установлено toohttps://bmfabrikam.com/adfs/services/trust</span><span class="sxs-lookup"><span data-stu-id="669d1-181">And hello IssuerUri on our new domain has been set toohttps://bmfabrikam.com/adfs/services/trust</span></span>

![Get-MsolDomainFederationSettings](./media/active-directory-multiple-domains/settings2.png)

## <a name="support-for-sub-domains"></a><span data-ttu-id="669d1-183">Поддержка поддоменов</span><span class="sxs-lookup"><span data-stu-id="669d1-183">Support for Sub-domains</span></span>
<span data-ttu-id="669d1-184">При добавлении дочерний домен, из-за hello, каким образом Azure AD обрабатывается доменов, он будет наследовать параметры hello hello родителя.</span><span class="sxs-lookup"><span data-stu-id="669d1-184">When you add a sub-domain, because of hello way Azure AD handled domains, it will inherit hello settings of hello parent.</span></span>  <span data-ttu-id="669d1-185">Это означает, что этой hello IssuerUri должен toomatch hello родителей.</span><span class="sxs-lookup"><span data-stu-id="669d1-185">This means that hello IssuerUri needs toomatch hello parents.</span></span>

<span data-ttu-id="669d1-186">Давайте предположим, что у меня был домен bmcontoso.com, а затем я добавил поддомен corp.bmcontoso.com.  Это означает, что hello IssuerUri для пользователя из corp.bmcontoso.com потребуется toobe **http://bmcontoso.com/adfs/services/trust.**</span><span class="sxs-lookup"><span data-stu-id="669d1-186">So lets say for example that I have bmcontoso.com and then add corp.bmcontoso.com.  This means that hello IssuerUri for a user from corp.bmcontoso.com will need toobe **http://bmcontoso.com/adfs/services/trust.**</span></span>  <span data-ttu-id="669d1-187">Однако реализации стандартных правил hello выше для Azure AD создает маркер с издателя, как **http://corp.bmcontoso.com/adfs/services/trust.**</span><span class="sxs-lookup"><span data-stu-id="669d1-187">However hello standard rule implemented above for Azure AD, will generate a token with an issuer as **http://corp.bmcontoso.com/adfs/services/trust.**</span></span> <span data-ttu-id="669d1-188">не соответствующая обязательное значение hello домена и не пройдет проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="669d1-188">which will not match hello domain's required value and authentication will fail.</span></span>

### <a name="how-tooenable-support-for-sub-domains"></a><span data-ttu-id="669d1-189">Как tooenable поддержка поддоменов</span><span class="sxs-lookup"><span data-stu-id="669d1-189">How tooenable support for sub-domains</span></span>
<span data-ttu-id="669d1-190">В порядке toowork вокруг этого hello AD FS с проверяющей стороной для Microsoft Online должен toobe обновлены.</span><span class="sxs-lookup"><span data-stu-id="669d1-190">In order toowork around this hello AD FS relying party trust for Microsoft Online needs toobe updated.</span></span>  <span data-ttu-id="669d1-191">toodo это, необходимо настроить настраиваемое правило для утверждений, чтобы он отсекает любой поддоменов из суффикс UPN пользователя hello, при создании пользовательского поставщика значения hello.</span><span class="sxs-lookup"><span data-stu-id="669d1-191">toodo this, you must configure a custom claim rule so that it strips off any sub-domains from hello user’s UPN suffix when constructing hello custom Issuer value.</span></span> 

<span data-ttu-id="669d1-192">После утверждения Hello для этого:</span><span class="sxs-lookup"><span data-stu-id="669d1-192">hello following claim will do this:</span></span>

    c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, "^.*@([^.]+\.)*?(?<domain>([^.]+\.?){2})$", "http://${domain}/adfs/services/trust/"));

[!NOTE]
<span data-ttu-id="669d1-193">Номер последней Hello в регулярном выражении hello задать hello сколько родительских доменов в корневой домен.</span><span class="sxs-lookup"><span data-stu-id="669d1-193">hello last number in hello regular expression set hello how many parent domains there is in your root domain.</span></span> <span data-ttu-id="669d1-194">Так как здесь используется bmcontoso.com, необходимы два родительских домена.</span><span class="sxs-lookup"><span data-stu-id="669d1-194">Here i have bmcontoso.com so two parent domains are necessary.</span></span> <span data-ttu-id="669d1-195">Если три родительских доменов были сохранены toobe (т. е.: corp.bmcontoso.com), то номер hello было бы три.</span><span class="sxs-lookup"><span data-stu-id="669d1-195">If three parent domains were toobe kept (i.e.: corp.bmcontoso.com), then hello number would have been three.</span></span> <span data-ttu-id="669d1-196">Eventualy диапазон может быть указан, совпадения hello всегда станет более hello toomatch доменов.</span><span class="sxs-lookup"><span data-stu-id="669d1-196">Eventualy a range can be indicated, hello match will always be made toomatch hello maximum of domains.</span></span> <span data-ttu-id="669d1-197">«{2,3}» будет соответствовать двумя доменами toothree (т. е.: bmfabrikam.com и corp.bmcontoso.com).</span><span class="sxs-lookup"><span data-stu-id="669d1-197">"{2,3}" will match two toothree domains (i.e.: bmfabrikam.com and corp.bmcontoso.com).</span></span>

<span data-ttu-id="669d1-198">Используйте следующие шаги tooadd hello в поддоменов toosupport пользовательского утверждения.</span><span class="sxs-lookup"><span data-stu-id="669d1-198">Use hello following steps tooadd a custom claim toosupport sub-domains.</span></span>

1. <span data-ttu-id="669d1-199">Откройте оснастку управления AD FS.</span><span class="sxs-lookup"><span data-stu-id="669d1-199">Open AD FS Management</span></span>
2. <span data-ttu-id="669d1-200">Щелкните правой кнопкой мыши доверие Microsoft Online RP hello и выберите правила для утверждений, изменение</span><span class="sxs-lookup"><span data-stu-id="669d1-200">Right click hello Microsoft Online RP trust and choose Edit Claim rules</span></span>
3. <span data-ttu-id="669d1-201">Выберите третий правила утверждения hello и замените ![изменить утверждения](./media/active-directory-multiple-domains/sub1.png)</span><span class="sxs-lookup"><span data-stu-id="669d1-201">Select hello third claim rule, and replace ![Edit claim](./media/active-directory-multiple-domains/sub1.png)</span></span>
4. <span data-ttu-id="669d1-202">Замените hello текущего утверждения:</span><span class="sxs-lookup"><span data-stu-id="669d1-202">Replace hello current claim:</span></span>
   
        c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, ".+@(?<domain>.+)","http://${domain}/adfs/services/trust/"));
   
       with
   
        c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, "^.*@([^.]+\.)*?(?<domain>([^.]+\.?){2})$", "http://${domain}/adfs/services/trust/"));

    ![Заменить утверждение](./media/active-directory-multiple-domains/sub2.png)

5. <span data-ttu-id="669d1-204">Нажмите кнопку "ОК".</span><span class="sxs-lookup"><span data-stu-id="669d1-204">Click Ok.</span></span>  <span data-ttu-id="669d1-205">Нажмите кнопку "Применить".</span><span class="sxs-lookup"><span data-stu-id="669d1-205">Click Apply.</span></span>  <span data-ttu-id="669d1-206">Нажмите кнопку "ОК".</span><span class="sxs-lookup"><span data-stu-id="669d1-206">Click Ok.</span></span>  <span data-ttu-id="669d1-207">Откройте оснастку управления AD FS.</span><span class="sxs-lookup"><span data-stu-id="669d1-207">Close AD FS Management.</span></span>

