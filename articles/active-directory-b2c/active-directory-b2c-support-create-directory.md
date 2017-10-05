---
title: "Устранение неполадок при создании клиентов Azure Active Directory B2C | Документация Майкрософт"
description: "В этой статье описаны проблемы и их решения при создании клиента Azure Active Directory или клиента Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 7ba4c6b2-161b-45b5-b3bd-ccb662f5d7a0
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: 81af4536fc223319369aff262d42149cfbf1a1e9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-creating-an-azure-active-directory-or-azure-active-directory-b2c-tenant"></a><span data-ttu-id="45b01-103">Устранение неполадок при создании клиентов Azure Active Directory или Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="45b01-103">Troubleshoot creating an Azure Active Directory or Azure Active Directory B2C tenant</span></span> 

## <a name="create-an-azure-ad-tenant"></a><span data-ttu-id="45b01-104">Создание клиента Azure AD</span><span class="sxs-lookup"><span data-stu-id="45b01-104">Create an Azure AD tenant</span></span>
<span data-ttu-id="45b01-105">Если вам не удается создать клиент Azure Active Directory (Azure AD) с первого раза, попробуйте сделать это еще раз.</span><span class="sxs-lookup"><span data-stu-id="45b01-105">If you can't create an Azure Active Directory (Azure AD) tenant on the first attempt, try again.</span></span> <span data-ttu-id="45b01-106">Если проблема не исчезла, обратитесь в службу поддержки Azure.</span><span class="sxs-lookup"><span data-stu-id="45b01-106">If the problem persists, contact Azure Support.</span></span>

## <a name="create-an-azure-ad-b2c-tenant"></a><span data-ttu-id="45b01-107">Создание клиента Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="45b01-107">Create an Azure AD B2C tenant</span></span>
<span data-ttu-id="45b01-108">При возникновении проблем во время [создания клиента Azure Active Directory B2C](active-directory-b2c-get-started.md) попробуйте сделать следующее.</span><span class="sxs-lookup"><span data-stu-id="45b01-108">If you encounter issues when you [create an Azure Active Directory B2C (Azure AD B2C) tenant](active-directory-b2c-get-started.md), try the following options:</span></span>

* <span data-ttu-id="45b01-109">Если клиент Azure AD B2C не отображается в списке клиентов, повторите попытку создания клиента.</span><span class="sxs-lookup"><span data-stu-id="45b01-109">If the Azure AD B2C tenant doesn't show up in your list of tenants, try again to create the tenant.</span></span>
* <span data-ttu-id="45b01-110">Если клиент Azure AD B2C не отображается в списке клиентов и появляется указанное ниже сообщение об ошибке, удалите клиента и создайте его заново.</span><span class="sxs-lookup"><span data-stu-id="45b01-110">If the Azure AD B2C tenant does show up in your list of tenants and you see the following  error message, delete the tenant and create it again:</span></span>

    <span data-ttu-id="45b01-111">"Could not complete the creation of the B2C tenant 'contosob2c'.</span><span class="sxs-lookup"><span data-stu-id="45b01-111">"Could not complete the creation of the B2C tenant 'contosob2c'.</span></span> <span data-ttu-id="45b01-112">Please visit this [link](http://go.microsoft.com/fwlink/?LinkID=624192&clcid=0x409) for more guidance." (Не удалось завершить создание клиента B2C contosob2c. Щелкните ссылку, чтобы получить дополнительные рекомендации).</span><span class="sxs-lookup"><span data-stu-id="45b01-112">Please visit this [link](http://go.microsoft.com/fwlink/?LinkID=624192&clcid=0x409) for more guidance."</span></span>
* <span data-ttu-id="45b01-113">При удалении существующего клиента Azure AD B2C и его повторном создании с тем же доменным именем могут возникнуть известные проблемы.</span><span class="sxs-lookup"><span data-stu-id="45b01-113">There are known issues when you delete an existing Azure AD B2C tenant and re-create it by using the same domain name.</span></span> <span data-ttu-id="45b01-114">При создании клиента Azure AD B2C необходимо использовать другое доменное имя.</span><span class="sxs-lookup"><span data-stu-id="45b01-114">When you create a new Azure AD B2C tenant, you must use a different domain name.</span></span>
* <span data-ttu-id="45b01-115">Если ни одно из приведенных решений не помогло, обратитесь в службу поддержки Azure.</span><span class="sxs-lookup"><span data-stu-id="45b01-115">If these resolutions don't work, contact Azure Support.</span></span> <span data-ttu-id="45b01-116">Дополнительные сведения см. в статье [Azure Active Directory B2C: регистрация запросов в службу поддержки](active-directory-b2c-support.md).</span><span class="sxs-lookup"><span data-stu-id="45b01-116">For more information, see [File support requests for Azure AD B2C](active-directory-b2c-support.md).</span></span>

