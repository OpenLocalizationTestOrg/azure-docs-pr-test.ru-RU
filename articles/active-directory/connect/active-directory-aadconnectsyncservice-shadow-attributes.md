---
title: "Теневые атрибуты службы синхронизации Azure AD Connect | Документация Майкрософт"
description: "Описание работы теневых атрибутов в службе синхронизации Azure AD Connect."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 0b6a7f22d744480a40a878c979986cdd7667109c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-sync-service-shadow-attributes"></a><span data-ttu-id="d0a03-103">Теневые атрибуты службы синхронизации Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="d0a03-103">Azure AD Connect sync service shadow attributes</span></span>
<span data-ttu-id="d0a03-104">Большинство атрибутов представляется в Azure AD так же, как и в локальной службе Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d0a03-104">Most attributes are represented the same way in Azure AD as they are in your on-premises Active Directory.</span></span> <span data-ttu-id="d0a03-105">Однако некоторые атрибуты требуют особого обращения, их значение в Azure AD может отличаться от того, что синхронизирует Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="d0a03-105">But some attributes have some special handling and the attribute value in Azure AD might be different than what Azure AD Connect synchronizes.</span></span>

## <a name="introducing-shadow-attributes"></a><span data-ttu-id="d0a03-106">Общие сведения о теневых атрибутах</span><span class="sxs-lookup"><span data-stu-id="d0a03-106">Introducing shadow attributes</span></span>
<span data-ttu-id="d0a03-107">Для некоторых атрибутов в Azure AD используются два представления.</span><span class="sxs-lookup"><span data-stu-id="d0a03-107">Some attributes have two representations in Azure AD.</span></span> <span data-ttu-id="d0a03-108">Для них сохраняются локальное и вычисляемое значения.</span><span class="sxs-lookup"><span data-stu-id="d0a03-108">Both the on-premises value and a calculated value are stored.</span></span> <span data-ttu-id="d0a03-109">Эти дополнительные атрибуты называются теневыми.</span><span class="sxs-lookup"><span data-stu-id="d0a03-109">These extra attributes are called shadow attributes.</span></span> <span data-ttu-id="d0a03-110">Двумя наиболее распространенными атрибутами из этой категории являются **userPrincipalName** и **proxyAddress**.</span><span class="sxs-lookup"><span data-stu-id="d0a03-110">The two most common attributes where you see this behavior are **userPrincipalName** and **proxyAddress**.</span></span> <span data-ttu-id="d0a03-111">Изменение значений атрибутов происходит, они представляют непроверенные домены.</span><span class="sxs-lookup"><span data-stu-id="d0a03-111">The change in attribute values happens when there are values in these attributes representing non-verified domains.</span></span> <span data-ttu-id="d0a03-112">Но модуль синхронизации в Connect считывает значение в теневом атрибуте, поэтому с его точки зрения атрибут подтвержден Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d0a03-112">But the sync engine in Connect reads the value in the shadow attribute so from its perspective, the attribute has been confirmed by Azure AD.</span></span>

<span data-ttu-id="d0a03-113">Теневые атрибуты невозможно просмотреть, используя портал Azure или PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d0a03-113">You cannot see the shadow attributes using the Azure portal or with PowerShell.</span></span> <span data-ttu-id="d0a03-114">Но понимание принципа помогает при устранении неполадок в определенных сценариях, когда атрибут имеет разные значения в локальной среде и в облаке.</span><span class="sxs-lookup"><span data-stu-id="d0a03-114">But understanding the concept helps you to troubleshoot certain scenarios where the attribute has different values on-premises and in the cloud.</span></span>

<span data-ttu-id="d0a03-115">Чтобы лучше понять, как это работает, рассмотрим следующий пример от компании Fabrikam.</span><span class="sxs-lookup"><span data-stu-id="d0a03-115">To better understand the behavior, look at this example from Fabrikam:</span></span>  
![Домены](./media/active-directory-aadconnectsyncservice-shadow-attributes/domains.png)  
<span data-ttu-id="d0a03-117">Они используют несколько суффиксов имени участника-пользователя в своей локальной службе Active Directory, но проверен только один из них.</span><span class="sxs-lookup"><span data-stu-id="d0a03-117">They have multiple UPN suffixes in their on-premises Active Directory, but they have only verified one.</span></span>

### <a name="userprincipalname"></a><span data-ttu-id="d0a03-118">userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="d0a03-118">userPrincipalName</span></span>
<span data-ttu-id="d0a03-119">У пользователя имеются следующие значения атрибутов в непроверенном домене.</span><span class="sxs-lookup"><span data-stu-id="d0a03-119">A user has the following attribute values in a non-verified domain:</span></span>

| <span data-ttu-id="d0a03-120">Атрибут</span><span class="sxs-lookup"><span data-stu-id="d0a03-120">Attribute</span></span> | <span data-ttu-id="d0a03-121">Значение</span><span class="sxs-lookup"><span data-stu-id="d0a03-121">Value</span></span> |
| --- | --- |
| <span data-ttu-id="d0a03-122">userPrincipalName для локальной среды</span><span class="sxs-lookup"><span data-stu-id="d0a03-122">on-premises userPrincipalName</span></span> | lee.sperry@fabrikam.com |
| <span data-ttu-id="d0a03-123">shadowUserPrincipalName для Azure AD</span><span class="sxs-lookup"><span data-stu-id="d0a03-123">Azure AD shadowUserPrincipalName</span></span> | lee.sperry@fabrikam.com |
| <span data-ttu-id="d0a03-124">userPrincipalName для Azure AD</span><span class="sxs-lookup"><span data-stu-id="d0a03-124">Azure AD userPrincipalName</span></span> | lee.sperry@fabrikam.onmicrosoft.com |

<span data-ttu-id="d0a03-125">Атрибут userPrincipalName — это значение, отображаемое при использовании PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d0a03-125">The userPrincipalName attribute is the value you see when using PowerShell.</span></span>

<span data-ttu-id="d0a03-126">Так как реальное локальное значение атрибута хранится в Azure AD, после проверки домена fabrikam.com служба Azure AD обновляет атрибут userPrincipalName значением из shadowUserPrincipalName.</span><span class="sxs-lookup"><span data-stu-id="d0a03-126">Since the real on-premises attribute value is stored in Azure AD, when you verify the fabrikam.com domain, Azure AD updates the userPrincipalName attribute with the value from the shadowUserPrincipalName.</span></span> <span data-ttu-id="d0a03-127">Нет необходимости синхронизировать все изменения из Azure AD Connect, чтобы обновлять эти значения.</span><span class="sxs-lookup"><span data-stu-id="d0a03-127">You do not have to synchronize any changes from Azure AD Connect for these values to be updated.</span></span>

### <a name="proxyaddresses"></a><span data-ttu-id="d0a03-128">proxyAddresses</span><span class="sxs-lookup"><span data-stu-id="d0a03-128">proxyAddresses</span></span>
<span data-ttu-id="d0a03-129">То же самое, только с учетом проверенных доменов, происходит с proxyAddresses, но с добавлением некоторой логики.</span><span class="sxs-lookup"><span data-stu-id="d0a03-129">The same process for only including verified domains also occurs for proxyAddresses, but with some additional logic.</span></span> <span data-ttu-id="d0a03-130">Проверка проверенных доменов происходит только для пользователей почтовых ящиков.</span><span class="sxs-lookup"><span data-stu-id="d0a03-130">The check for verified domains only happens for mailbox users.</span></span> <span data-ttu-id="d0a03-131">Пользователь, поддерживающий почту, или контакт представляет пользователя в другой организации Exchange, и вы можете добавить в эти объекты любые значения в proxyAddresses.</span><span class="sxs-lookup"><span data-stu-id="d0a03-131">A mail-enabled user or contact represent a user in another Exchange organization and you can add any values in proxyAddresses to these objects.</span></span>

<span data-ttu-id="d0a03-132">Для пользователя почтового ящика, размещенного в локальной среде или Exchange Online, отображаются только значения для проверенных доменов.</span><span class="sxs-lookup"><span data-stu-id="d0a03-132">For a mailbox user, either on-premises or in Exchange Online, only values for verified domains appear.</span></span> <span data-ttu-id="d0a03-133">Это выглядит следующим образом.</span><span class="sxs-lookup"><span data-stu-id="d0a03-133">It could look like this:</span></span>

| <span data-ttu-id="d0a03-134">Атрибут</span><span class="sxs-lookup"><span data-stu-id="d0a03-134">Attribute</span></span> | <span data-ttu-id="d0a03-135">Значение</span><span class="sxs-lookup"><span data-stu-id="d0a03-135">Value</span></span> |
| --- | --- |
| <span data-ttu-id="d0a03-136">proxyAddresses для локальной среды</span><span class="sxs-lookup"><span data-stu-id="d0a03-136">on-premises proxyAddresses</span></span> | SMTP:abbie.spencer@fabrikamonline.com</br>smtp:abbie.spencer@fabrikam.com</br>smtp:abbie@fabrikamonline.com |
| <span data-ttu-id="d0a03-137">proxyAddresses для Exchange Online</span><span class="sxs-lookup"><span data-stu-id="d0a03-137">Exchange Online proxyAddresses</span></span> | SMTP:abbie.spencer@fabrikamonline.com</br>smtp:abbie@fabrikamonline.com</br>SIP:abbie.spencer@fabrikamonline.com |

<span data-ttu-id="d0a03-138">В этом случае **smtp:abbie.spencer@fabrikam.com** был удален, так как этот домен не проверен.</span><span class="sxs-lookup"><span data-stu-id="d0a03-138">In this case **smtp:abbie.spencer@fabrikam.com** was removed since that domain has not been verified.</span></span> <span data-ttu-id="d0a03-139">Но служба Exchange также добавила **SIP:abbie.spencer@fabrikamonline.com**.</span><span class="sxs-lookup"><span data-stu-id="d0a03-139">But Exchange also added **SIP:abbie.spencer@fabrikamonline.com**.</span></span> <span data-ttu-id="d0a03-140">Fabrikam не использовал Lync или Skype локально, но Azure AD и Exchange Online готовы к этому.</span><span class="sxs-lookup"><span data-stu-id="d0a03-140">Fabrikam has not used Lync/Skype on-premises, but Azure AD and Exchange Online prepare for it.</span></span>

<span data-ttu-id="d0a03-141">Эта логика proxyAddresses называется **ProxyCalc**.</span><span class="sxs-lookup"><span data-stu-id="d0a03-141">This logic for proxyAddresses is referred to as **ProxyCalc**.</span></span> <span data-ttu-id="d0a03-142">ProxyCalc вызывается при каждом изменении пользователя, когда:</span><span class="sxs-lookup"><span data-stu-id="d0a03-142">ProxyCalc is invoked with every change on a user when:</span></span>

- <span data-ttu-id="d0a03-143">Пользователь назначил план обслуживания, который включает в себя Exchange Online, даже если у пользователя отсутствует лицензия на Exchange.</span><span class="sxs-lookup"><span data-stu-id="d0a03-143">The user has been assigned a service plan that includes Exchange Online even if the user was not licensed for Exchange.</span></span> <span data-ttu-id="d0a03-144">Например, если пользователь назначил номер SKU Office E3, но ему был назначен только номер SKU SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="d0a03-144">For example, if the user is assigned the Office E3 SKU, but only was assigned SharePoint Online.</span></span> <span data-ttu-id="d0a03-145">Это верно, даже если ваш почтовый ящик является локальным.</span><span class="sxs-lookup"><span data-stu-id="d0a03-145">This is true even if your mailbox is still on-premises.</span></span>
- <span data-ttu-id="d0a03-146">Атрибут msExchRecipientTypeDetails имеет значение.</span><span class="sxs-lookup"><span data-stu-id="d0a03-146">The attribute msExchRecipientTypeDetails has a value.</span></span>
- <span data-ttu-id="d0a03-147">Пользователь изменил proxyAddresses или userPrincipalName.</span><span class="sxs-lookup"><span data-stu-id="d0a03-147">You make a change to proxyAddresses or userPrincipalName.</span></span>

<span data-ttu-id="d0a03-148">ProxyCalc может потратить некоторое время на обработку изменения пользователя, не синхронизируясь с процессом экспорта Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="d0a03-148">ProxyCalc might take some time to process a change on a user and is not synchronous with the Azure AD Connect export process.</span></span>

> [!NOTE]
> <span data-ttu-id="d0a03-149">Логика ProxyCalc содержит дополнительные режимы для более сложных сценариев, которые не описаны в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="d0a03-149">The ProxyCalc logic has some additional behaviors for advanced scenarios not documented in this topic.</span></span> <span data-ttu-id="d0a03-150">Этот раздел предоставлен для понимания поведения и не содержит описания всей внутренней логики.</span><span class="sxs-lookup"><span data-stu-id="d0a03-150">This topic is provided for you to understand the behavior and not document all internal logic.</span></span>

### <a name="quarantined-attribute-values"></a><span data-ttu-id="d0a03-151">Значения атрибутов, помещенных в карантин</span><span class="sxs-lookup"><span data-stu-id="d0a03-151">Quarantined attribute values</span></span>
<span data-ttu-id="d0a03-152">Теневые атрибуты также используются при наличии повторяющихся значений атрибутов.</span><span class="sxs-lookup"><span data-stu-id="d0a03-152">Shadow attributes are also used when there are duplicate attribute values.</span></span> <span data-ttu-id="d0a03-153">Дополнительные сведения см. в разделе [Синхронизация удостоверений и устойчивость повторяющихся атрибутов](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md).</span><span class="sxs-lookup"><span data-stu-id="d0a03-153">For more information, see [duplicate attribute resiliency](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="d0a03-154">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="d0a03-154">See also</span></span>
* [<span data-ttu-id="d0a03-155">Службы синхронизации Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="d0a03-155">Azure AD Connect sync</span></span>](active-directory-aadconnectsync-whatis.md)
* <span data-ttu-id="d0a03-156">[Интеграция локальных удостоверений с Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="d0a03-156">[Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
