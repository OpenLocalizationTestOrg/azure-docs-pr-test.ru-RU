---
title: "aaaFederating несколько Azure AD с помощью одной службы федерации Active Directory | Документы Microsoft"
description: "В этом документе вы узнаете, как toofederate несколько Azure AD с одной AD FS."
keywords: "федерация, ADFS, AD FS, несколько клиентов, один клиент AD FS, один экземпляр ADFS, федерация нескольких клиентов, федерация ADFS с несколькими лесами, AAD Сonnect, федерация, федерация между клиентами"
services: active-directory
documentationcenter: 
author: anandyadavmsft
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: anandy; billmath
ms.openlocfilehash: 442192896b3b13f7bf9388396cd3769e194329d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
#<a name="federate-multiple-instances-of-azure-ad-with-single-instance-of-ad-fs"></a><span data-ttu-id="66fc6-104">Федерация нескольких экземпляров Azure AD с одним экземпляром AD FS</span><span class="sxs-lookup"><span data-stu-id="66fc6-104">Federate multiple instances of Azure AD with single instance of AD FS</span></span>

<span data-ttu-id="66fc6-105">Одна высокодоступная ферма AD FS может объединять несколько лесов при наличии взаимного доверия между ними.</span><span class="sxs-lookup"><span data-stu-id="66fc6-105">A single high available AD FS farm can federate multiple forests if they have 2-way trust between them.</span></span> <span data-ttu-id="66fc6-106">Эти несколько лесов может или не может соответствовать toohello же Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="66fc6-106">These multiple forests may or may not correspond toohello same Azure Active Directory.</span></span> <span data-ttu-id="66fc6-107">В этой статье описано, как tooconfigure федерацию между одно развертывание AD FS и несколько лесов, toodifferent синхронизации Azure AD.</span><span class="sxs-lookup"><span data-stu-id="66fc6-107">This article provides instructions on how tooconfigure federation between a single AD FS deployment and more than one forests that sync toodifferent Azure AD.</span></span>

![Федерация нескольких клиентов с одним экземпляром AD FS](media/active-directory-aadconnectfed-single-adfs-multitenant-federation/concept.png)
 
> [!NOTE]
> <span data-ttu-id="66fc6-109">В этом сценарии не поддерживаются обратная запись устройств и автоматическое присоединение устройств.</span><span class="sxs-lookup"><span data-stu-id="66fc6-109">Device writeback and automatic device join are not supported in this scenario.</span></span>

> [!NOTE]
> <span data-ttu-id="66fc6-110">Azure AD Connect не может быть федерации tooconfigure используется в этом случае Azure AD Connect можно настроить федерации для доменов в одном Azure AD.</span><span class="sxs-lookup"><span data-stu-id="66fc6-110">Azure AD Connect cannot be used tooconfigure federation in this scenario as Azure AD Connect can configure federation for domains in a single Azure AD.</span></span>

##<a name="steps-for-federating-ad-fs-with-multiple-azure-ad"></a><span data-ttu-id="66fc6-111">Шаги для федерации AD FS и нескольких экземпляров Azure AD</span><span class="sxs-lookup"><span data-stu-id="66fc6-111">Steps for federating AD FS with multiple Azure AD</span></span>

<span data-ttu-id="66fc6-112">Рассмотрите возможность уже включена в федерацию с hello AD FS локально установленный в среде Active Directory contoso.com локального домена contoso.com в Azure Active Directory contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="66fc6-112">Consider a domain contoso.com in Azure Active Directory contoso.onmicrosoft.com is already federated with hello AD FS on-premises installed in contoso.com on-premises Active Directory environment.</span></span> <span data-ttu-id="66fc6-113">Fabrikam.com является доменом в fabrikam.onmicrosoft.com Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="66fc6-113">Fabrikam.com is a domain in fabrikam.onmicrosoft.com Azure Active Directory.</span></span>

##<a name="step-1-establish-a-two-way-trust"></a><span data-ttu-id="66fc6-114">Шаг 1. Установка взаимного доверия</span><span class="sxs-lookup"><span data-stu-id="66fc6-114">Step 1: Establish a two-way trust</span></span>
 
<span data-ttu-id="66fc6-115">Для AD FS в contoso.com пользователи могут tooauthenticate toobe в fabrikam.com требуется двустороннее отношение доверия между contoso.com и fabrikam.com. Выполните рекомендации hello в этом [статьи](https://technet.microsoft.com/library/cc816590.aspx) toocreate hello двустороннее отношение доверия.</span><span class="sxs-lookup"><span data-stu-id="66fc6-115">For AD FS in contoso.com toobe able tooauthenticate users in fabrikam.com, a two-way trust is needed between contoso.com and fabrikam.com. Follow hello guideline in this [article](https://technet.microsoft.com/library/cc816590.aspx) toocreate hello two-way trust.</span></span>
 
##<a name="step-2-modify-contosocom-federation-settings"></a><span data-ttu-id="66fc6-116">Шаг 2. Изменение параметров федерации contoso.com</span><span class="sxs-lookup"><span data-stu-id="66fc6-116">Step 2: Modify contoso.com federation settings</span></span> 
 
<span data-ttu-id="66fc6-117">Издатель по умолчанию Hello, заданное для одного домена федеративной tooAD FS является «http://ADFSServiceFQDN/adfs/services/trust», например, «http://fs.contoso.com/adfs/services/trust».</span><span class="sxs-lookup"><span data-stu-id="66fc6-117">hello default issuer set for a single domain federated tooAD FS is "http://ADFSServiceFQDN/adfs/services/trust", for example, “http://fs.contoso.com/adfs/services/trust”.</span></span> <span data-ttu-id="66fc6-118">Служба Azure Active Directory требует отдельного издателя для каждого федеративного домена.</span><span class="sxs-lookup"><span data-stu-id="66fc6-118">Azure Active Directory requires unique issuer for each federated domain.</span></span> <span data-ttu-id="66fc6-119">Поскольку hello же AD FS будут toofederate два домена, значение издателя hello должен toobe изменены таким образом, чтобы он уникален для каждого домена AD FS создает федерацию с Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="66fc6-119">Since hello same AD FS is going toofederate two domains, hello issuer value needs toobe modified so that it is unique for each domain AD FS federates with Azure Active Directory.</span></span> 
 
<span data-ttu-id="66fc6-120">На сервере AD FS hello откройте Azure AD PowerShell и выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="66fc6-120">On hello AD FS server, open Azure AD PowerShell and perform hello following steps:</span></span>
 
<span data-ttu-id="66fc6-121">Подключение Azure Active Directory, содержащий hello домена contoso.com Connect-MsolService обновления hello параметры федерации для contoso.com Update-MsolFederatedDomain - DomainName contoso.com toohello – SupportMultipleDomain</span><span class="sxs-lookup"><span data-stu-id="66fc6-121">Connect toohello Azure Active Directory that contains hello domain contoso.com Connect-MsolService Update hello federation settings for contoso.com Update-MsolFederatedDomain -DomainName contoso.com –SupportMultipleDomain</span></span>
 
<span data-ttu-id="66fc6-122">Будет изменено издателя в параметра федерации доменов hello слишком «http://contoso.com/adfs/services/trust» и выдачи утверждений, правило будет добавлено для hello Azure AD доверия с проверяющей стороной tooissue hello правильное значение issuerId на основании hello суффикс UPN.</span><span class="sxs-lookup"><span data-stu-id="66fc6-122">Issuer in hello domain federation setting will be changed too"http://contoso.com/adfs/services/trust" and an issuance claim rule will be added for hello Azure AD Relying Party Trust tooissue hello correct issuerId value based on hello UPN suffix.</span></span>
 
##<a name="step-3-federate-fabrikamcom-with-ad-fs"></a><span data-ttu-id="66fc6-123">Шаг 3. Федерация fabrikam.com с AD FS</span><span class="sxs-lookup"><span data-stu-id="66fc6-123">Step 3: Federate fabrikam.com with AD FS</span></span>
 
<span data-ttu-id="66fc6-124">В Azure AD powershell сеанс выполнять следующие шаги hello: подключение tooAzure Active Directory, содержащую hello домена fabrikam.com</span><span class="sxs-lookup"><span data-stu-id="66fc6-124">In Azure AD powershell session perform hello following steps: Connect tooAzure Active Directory that contains hello domain fabrikam.com</span></span>

    Connect-MsolService
<span data-ttu-id="66fc6-125">Преобразуйте toofederated домена fabrikam.com управляемых hello:</span><span class="sxs-lookup"><span data-stu-id="66fc6-125">Convert hello fabrikam.com managed domain toofederated:</span></span>

    Convert-MsolDomainToFederated -DomainName anandmsft.com -Verbose -SupportMultipleDomain
 
<span data-ttu-id="66fc6-126">Hello выше операции будет федерацию hello домена fabrikam.com с hello же AD FS.</span><span class="sxs-lookup"><span data-stu-id="66fc6-126">hello above operation will federate hello domain fabrikam.com with hello same AD FS.</span></span> <span data-ttu-id="66fc6-127">Параметры домена hello можно проверить с помощью Get-MsolDomainFederationSettings для обоих доменов.</span><span class="sxs-lookup"><span data-stu-id="66fc6-127">You can verify hello domain settings by using Get-MsolDomainFederationSettings for both domains.</span></span>

## <a name="next-steps"></a><span data-ttu-id="66fc6-128">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="66fc6-128">Next steps</span></span>
[<span data-ttu-id="66fc6-129">Подключение Active Directory к Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="66fc6-129">Connect Active Directory with Azure Active Directory</span></span>](active-directory-aadconnect.md)
