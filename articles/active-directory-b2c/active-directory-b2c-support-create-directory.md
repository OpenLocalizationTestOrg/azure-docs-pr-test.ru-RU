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
ms.openlocfilehash: 4bb7ec6ec67d3368a0e36c098f290f582510714a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-creating-an-azure-active-directory-or-azure-active-directory-b2c-tenant"></a><span data-ttu-id="d1574-103">Устранение неполадок при создании клиентов Azure Active Directory или Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="d1574-103">Troubleshoot creating an Azure Active Directory or Azure Active Directory B2C tenant</span></span> 

## <a name="create-an-azure-ad-tenant"></a><span data-ttu-id="d1574-104">Создание клиента Azure AD</span><span class="sxs-lookup"><span data-stu-id="d1574-104">Create an Azure AD tenant</span></span>
<span data-ttu-id="d1574-105">Если при первой попытке hello не удается создать клиент Azure Active Directory (Azure AD), повторите попытку.</span><span class="sxs-lookup"><span data-stu-id="d1574-105">If you can't create an Azure Active Directory (Azure AD) tenant on hello first attempt, try again.</span></span> <span data-ttu-id="d1574-106">Если hello проблема будет повторяться, обратитесь в службу поддержки Azure.</span><span class="sxs-lookup"><span data-stu-id="d1574-106">If hello problem persists, contact Azure Support.</span></span>

## <a name="create-an-azure-ad-b2c-tenant"></a><span data-ttu-id="d1574-107">Создание клиента Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="d1574-107">Create an Azure AD B2C tenant</span></span>
<span data-ttu-id="d1574-108">При возникновении проблем при вы [Создание Azure Active Directory B2C клиента (Azure AD B2C)](active-directory-b2c-get-started.md), попробуйте hello следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="d1574-108">If you encounter issues when you [create an Azure Active Directory B2C (Azure AD B2C) tenant](active-directory-b2c-get-started.md), try hello following options:</span></span>

* <span data-ttu-id="d1574-109">Если клиент Azure AD B2C hello не отображается в списке клиентов, повторите попытку toocreate hello клиента.</span><span class="sxs-lookup"><span data-stu-id="d1574-109">If hello Azure AD B2C tenant doesn't show up in your list of tenants, try again toocreate hello tenant.</span></span>
* <span data-ttu-id="d1574-110">Если вы видите сообщение об ошибке после hello hello Azure AD B2C клиента отображаются в списке клиентов, удалите hello клиента и создайте его заново:</span><span class="sxs-lookup"><span data-stu-id="d1574-110">If hello Azure AD B2C tenant does show up in your list of tenants and you see hello following  error message, delete hello tenant and create it again:</span></span>

    <span data-ttu-id="d1574-111">«Не удалось завершить создание клиента B2C hello «contosob2c» hello.</span><span class="sxs-lookup"><span data-stu-id="d1574-111">"Could not complete hello creation of hello B2C tenant 'contosob2c'.</span></span> <span data-ttu-id="d1574-112">Please visit this [link](http://go.microsoft.com/fwlink/?LinkID=624192&clcid=0x409) for more guidance." (Не удалось завершить создание клиента B2C contosob2c. Щелкните ссылку, чтобы получить дополнительные рекомендации).</span><span class="sxs-lookup"><span data-stu-id="d1574-112">Please visit this [link](http://go.microsoft.com/fwlink/?LinkID=624192&clcid=0x409) for more guidance."</span></span>
* <span data-ttu-id="d1574-113">Существуют известные проблемы при удалении существующей Azure AD B2C клиента и создать его повторно с помощью hello таким же именем домена.</span><span class="sxs-lookup"><span data-stu-id="d1574-113">There are known issues when you delete an existing Azure AD B2C tenant and re-create it by using hello same domain name.</span></span> <span data-ttu-id="d1574-114">При создании клиента Azure AD B2C необходимо использовать другое доменное имя.</span><span class="sxs-lookup"><span data-stu-id="d1574-114">When you create a new Azure AD B2C tenant, you must use a different domain name.</span></span>
* <span data-ttu-id="d1574-115">Если ни одно из приведенных решений не помогло, обратитесь в службу поддержки Azure.</span><span class="sxs-lookup"><span data-stu-id="d1574-115">If these resolutions don't work, contact Azure Support.</span></span> <span data-ttu-id="d1574-116">Дополнительные сведения см. в статье [Azure Active Directory B2C: регистрация запросов в службу поддержки](active-directory-b2c-support.md).</span><span class="sxs-lookup"><span data-stu-id="d1574-116">For more information, see [File support requests for Azure AD B2C](active-directory-b2c-support.md).</span></span>

