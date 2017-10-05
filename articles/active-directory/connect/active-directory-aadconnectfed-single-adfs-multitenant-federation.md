---
title: "Федерация нескольких экземпляров Azure AD с одним экземпляром AD FS | Документация Майкрософт"
description: "Из этого документа вы узнаете, как создать федерацию нескольких экземпляров Azure AD с одним экземпляром AD FS."
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
ms.openlocfilehash: 436bf5905d2b203dc4cceea97f4fb90593df7111
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
#<a name="federate-multiple-instances-of-azure-ad-with-single-instance-of-ad-fs"></a><span data-ttu-id="68394-104">Федерация нескольких экземпляров Azure AD с одним экземпляром AD FS</span><span class="sxs-lookup"><span data-stu-id="68394-104">Federate multiple instances of Azure AD with single instance of AD FS</span></span>

<span data-ttu-id="68394-105">Одна высокодоступная ферма AD FS может объединять несколько лесов при наличии взаимного доверия между ними.</span><span class="sxs-lookup"><span data-stu-id="68394-105">A single high available AD FS farm can federate multiple forests if they have 2-way trust between them.</span></span> <span data-ttu-id="68394-106">Эти несколько лесов могут соответствовать или не соответствовать одной службе Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="68394-106">These multiple forests may or may not correspond to the same Azure Active Directory.</span></span> <span data-ttu-id="68394-107">Эта статья содержит инструкции по настройке федерации между одним экземпляром AD FS и несколькими лесами, которые синхронизируются с другим экземпляром Azure AD.</span><span class="sxs-lookup"><span data-stu-id="68394-107">This article provides instructions on how to configure federation between a single AD FS deployment and more than one forests that sync to different Azure AD.</span></span>

![Федерация нескольких клиентов с одним экземпляром AD FS](media/active-directory-aadconnectfed-single-adfs-multitenant-federation/concept.png)
 
> [!NOTE]
> <span data-ttu-id="68394-109">В этом сценарии не поддерживаются обратная запись устройств и автоматическое присоединение устройств.</span><span class="sxs-lookup"><span data-stu-id="68394-109">Device writeback and automatic device join are not supported in this scenario.</span></span>

> [!NOTE]
> <span data-ttu-id="68394-110">Azure AD Connect нельзя использовать для настройки федерации в этом сценарии, так как Azure AD Connect может настраивать федерацию для доменов в одном экземпляре Azure AD.</span><span class="sxs-lookup"><span data-stu-id="68394-110">Azure AD Connect cannot be used to configure federation in this scenario as Azure AD Connect can configure federation for domains in a single Azure AD.</span></span>

##<a name="steps-for-federating-ad-fs-with-multiple-azure-ad"></a><span data-ttu-id="68394-111">Шаги для федерации AD FS и нескольких экземпляров Azure AD</span><span class="sxs-lookup"><span data-stu-id="68394-111">Steps for federating AD FS with multiple Azure AD</span></span>

<span data-ttu-id="68394-112">Представьте, что домен contoso.com в Azure Active Directory (contoso.onmicrosoft.com) включен в федерацию локального экземпляра AD FS, установленного в локальной среде Active Directory contoso.com.</span><span class="sxs-lookup"><span data-stu-id="68394-112">Consider a domain contoso.com in Azure Active Directory contoso.onmicrosoft.com is already federated with the AD FS on-premises installed in contoso.com on-premises Active Directory environment.</span></span> <span data-ttu-id="68394-113">Fabrikam.com является доменом в fabrikam.onmicrosoft.com Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="68394-113">Fabrikam.com is a domain in fabrikam.onmicrosoft.com Azure Active Directory.</span></span>

##<a name="step-1-establish-a-two-way-trust"></a><span data-ttu-id="68394-114">Шаг 1. Установка взаимного доверия</span><span class="sxs-lookup"><span data-stu-id="68394-114">Step 1: Establish a two-way trust</span></span>
 
<span data-ttu-id="68394-115">Чтобы служба AD FS в contoso.com могла проверять подлинность пользователей в fabrikam.com, требуется взаимное доверие между contoso.com и fabrikam.com.</span><span class="sxs-lookup"><span data-stu-id="68394-115">For AD FS in contoso.com to be able to authenticate users in fabrikam.com, a two-way trust is needed between contoso.com and fabrikam.com.</span></span> <span data-ttu-id="68394-116">Следуйте рекомендациям, приведенным в этой [статье](https://technet.microsoft.com/library/cc816590.aspx), чтобы создать отношения взаимного доверия.</span><span class="sxs-lookup"><span data-stu-id="68394-116">Follow the guideline in this [article](https://technet.microsoft.com/library/cc816590.aspx) to create the two-way trust.</span></span>
 
##<a name="step-2-modify-contosocom-federation-settings"></a><span data-ttu-id="68394-117">Шаг 2. Изменение параметров федерации contoso.com</span><span class="sxs-lookup"><span data-stu-id="68394-117">Step 2: Modify contoso.com federation settings</span></span> 
 
<span data-ttu-id="68394-118">Издателем отдельного домена, включенного в федерацию AD FS, по умолчанию является http://ADFSServiceFQDN/adfs/services/trust, например http://fs.contoso.com/adfs/services/trust.</span><span class="sxs-lookup"><span data-stu-id="68394-118">The default issuer set for a single domain federated to AD FS is "http://ADFSServiceFQDN/adfs/services/trust", for example, “http://fs.contoso.com/adfs/services/trust”.</span></span> <span data-ttu-id="68394-119">Служба Azure Active Directory требует отдельного издателя для каждого федеративного домена.</span><span class="sxs-lookup"><span data-stu-id="68394-119">Azure Active Directory requires unique issuer for each federated domain.</span></span> <span data-ttu-id="68394-120">Так как один и тот же экземпляр AD FS будет включать в федерацию два домена, значение издателя должно быть изменено, чтобы оно было уникальным для каждого домена AD FS, которое входит в федерацию с Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="68394-120">Since the same AD FS is going to federate two domains, the issuer value needs to be modified so that it is unique for each domain AD FS federates with Azure Active Directory.</span></span> 
 
<span data-ttu-id="68394-121">На сервере AD FS откройте Azure AD PowerShell и выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="68394-121">On the AD FS server, open Azure AD PowerShell and perform the following steps:</span></span>
 
<span data-ttu-id="68394-122">Подключитесь к службе Azure Active Directory, которая содержит домен contoso.com (Connect-MsolService). Обновите параметры федерации для contoso.com (Update-MsolFederatedDomain - DomainName contoso.com — SupportMultipleDomain).</span><span class="sxs-lookup"><span data-stu-id="68394-122">Connect to the Azure Active Directory that contains the domain contoso.com Connect-MsolService Update the federation settings for contoso.com Update-MsolFederatedDomain -DomainName contoso.com –SupportMultipleDomain</span></span>
 
<span data-ttu-id="68394-123">Издатель в параметре федерации домена будет изменен на http://contoso.com/adfs/services/trust, и для проверяющей стороны Azure AD будет добавлено правило утверждения выдачи, чтобы она выдавала правильный идентификатор издателя на основе суффикса имени участника-пользователя.</span><span class="sxs-lookup"><span data-stu-id="68394-123">Issuer in the domain federation setting will be changed to "http://contoso.com/adfs/services/trust" and an issuance claim rule will be added for the Azure AD Relying Party Trust to issue the correct issuerId value based on the UPN suffix.</span></span>
 
##<a name="step-3-federate-fabrikamcom-with-ad-fs"></a><span data-ttu-id="68394-124">Шаг 3. Федерация fabrikam.com с AD FS</span><span class="sxs-lookup"><span data-stu-id="68394-124">Step 3: Federate fabrikam.com with AD FS</span></span>
 
<span data-ttu-id="68394-125">В сеансе Azure AD PowerShell подключитесь к службе Azure Active Directory, которая содержит домен fabrikam.com.</span><span class="sxs-lookup"><span data-stu-id="68394-125">In Azure AD powershell session perform the following steps: Connect to Azure Active Directory that contains the domain fabrikam.com</span></span>

    Connect-MsolService
<span data-ttu-id="68394-126">Преобразуйте управляемый домен fabrikam.com в федеративный:</span><span class="sxs-lookup"><span data-stu-id="68394-126">Convert the fabrikam.com managed domain to federated:</span></span>

    Convert-MsolDomainToFederated -DomainName anandmsft.com -Verbose -SupportMultipleDomain
 
<span data-ttu-id="68394-127">Вышеуказанная операция добавит домен fabrikam.com в федерацию с тем же экземпляром AD FS.</span><span class="sxs-lookup"><span data-stu-id="68394-127">The above operation will federate the domain fabrikam.com with the same AD FS.</span></span> <span data-ttu-id="68394-128">Параметры обоих доменов можно проверить с помощью командлета Get-MsolDomainFederationSettings.</span><span class="sxs-lookup"><span data-stu-id="68394-128">You can verify the domain settings by using Get-MsolDomainFederationSettings for both domains.</span></span>

## <a name="next-steps"></a><span data-ttu-id="68394-129">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="68394-129">Next steps</span></span>
[<span data-ttu-id="68394-130">Подключение Active Directory к Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="68394-130">Connect Active Directory with Azure Active Directory</span></span>](active-directory-aadconnect.md)
