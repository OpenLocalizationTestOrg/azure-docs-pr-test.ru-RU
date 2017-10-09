---
title: "aaaCharacteristics из Azure Active Directory клиента intercaction | Документы Microsoft"
description: "Управление клиентами Azure Active Directory как полностью независимыми ресурсами."
services: active-tenant
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 2b862b75-14df-45f2-a8ab-2a3ff1e2eb08
ms.service: active-tenant
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/27/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017;it-pro
ms.reviewer: piotrci
ms.openlocfilehash: 57b677665c7cb4aee63f518c39d26754fe71a999
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="understand-how-multiple-azure-active-directory-tenants-interact"></a><span data-ttu-id="4007b-103">Сведения о взаимодействии нескольких клиентов Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4007b-103">Understand how multiple Azure Active Directory tenants interact</span></span>

<span data-ttu-id="4007b-104">В Azure Active Directory (Azure AD), для каждого клиента является полностью независимым ресурсом: Здравствуйте, однорангового узла, которая логически независима от других клиентов, которыми вы управляете.</span><span class="sxs-lookup"><span data-stu-id="4007b-104">In Azure Active Directory (Azure AD), each tenent is a fully independent resource: a peer that is logically independent from hello other tenants that you manage.</span></span> <span data-ttu-id="4007b-105">Между клиентами нет связи типа "родительский объект — дочерний объект".</span><span class="sxs-lookup"><span data-stu-id="4007b-105">There is no parent-child relationship between tenants.</span></span> <span data-ttu-id="4007b-106">Такая независимость клиентов подразумевает и независимость ресурсов, административную независимость и независимость синхронизации.</span><span class="sxs-lookup"><span data-stu-id="4007b-106">This independence between tenants includes resource independence, administrative independence, and synchronization independence.</span></span>

## <a name="resource-independence"></a><span data-ttu-id="4007b-107">Независимость ресурсов</span><span class="sxs-lookup"><span data-stu-id="4007b-107">Resource independence</span></span>
* <span data-ttu-id="4007b-108">Если создание или удаление ресурса в один клиент, он не оказывает влияния на любой ресурс другим клиентом, с единственным исключением hello внешних пользователей.</span><span class="sxs-lookup"><span data-stu-id="4007b-108">If you create or delete a resource in one tenant, it has no impact on any resource in another tenant, with hello partial exception of external users.</span></span> 
* <span data-ttu-id="4007b-109">Если какое-либо из доменных имен используется для одного клиента, то оно не может использоваться для любого другого клиента.</span><span class="sxs-lookup"><span data-stu-id="4007b-109">If you use one of your domain names with one tenant, it cannot be used with any other tenant.</span></span>

## <a name="administrative-independence"></a><span data-ttu-id="4007b-110">Административная независимость</span><span class="sxs-lookup"><span data-stu-id="4007b-110">Administrative independence</span></span>
<span data-ttu-id="4007b-111">Если пользователь без прав администратора клиента Contoso создает тестовый клиент Test, то:</span><span class="sxs-lookup"><span data-stu-id="4007b-111">If a non-administrative user of tenant 'Contoso' creates a test tenant 'Test,' then:</span></span>

* <span data-ttu-id="4007b-112">По умолчанию hello пользователь, создающий клиента добавляется как внешний пользователь в этот новый клиент и назначенный hello роли глобального администратора в этом клиенте.</span><span class="sxs-lookup"><span data-stu-id="4007b-112">By default, hello user who creates a tenant is added as an external user in that new tenant, and assigned hello global administrator role in that tenant.</span></span>
* <span data-ttu-id="4007b-113">Администраторы клиента «Contoso» Hello иметь нет прямых административных полномочий tootenant 'Test', если администратор 'Test' предоставит им явным образом эти права.</span><span class="sxs-lookup"><span data-stu-id="4007b-113">hello administrators of tenant 'Contoso' have no direct administrative privileges tootenant 'Test,' unless an administrator of 'Test' specifically grants them these privileges.</span></span> <span data-ttu-id="4007b-114">Тем не менее 'Contoso'-администраторы могут управлять доступом tootenant 'Test', если они управляют hello учетная запись пользователя, создавшего 'Test'.</span><span class="sxs-lookup"><span data-stu-id="4007b-114">However, administrators of 'Contoso' can control access tootenant 'Test' if they control hello user account that created 'Test.'</span></span>
* <span data-ttu-id="4007b-115">Если добавить или удалить роль администратора для пользователя в один клиент, не hello изменения не влияют на роли администратора hello, hello пользователем другим клиентом.</span><span class="sxs-lookup"><span data-stu-id="4007b-115">If you add/remove an administrator role for a user in one tenant, hello change does not affect hello administrator roles that hello user has in another tenant.</span></span>

## <a name="synchronization-independence"></a><span data-ttu-id="4007b-116">Независимость синхронизации</span><span class="sxs-lookup"><span data-stu-id="4007b-116">Synchronization independence</span></span>
<span data-ttu-id="4007b-117">Можно настроить каждый Azure AD независимо друг от друга клиента tooget синхронизации данных от одного экземпляра либо:</span><span class="sxs-lookup"><span data-stu-id="4007b-117">You can configure each Azure AD tenant independently tooget data synchronized from a single instance of either:</span></span>

* <span data-ttu-id="4007b-118">средства Hello Azure AD Connect toosynchronize данных с одним лесом AD.</span><span class="sxs-lookup"><span data-stu-id="4007b-118">hello Azure AD Connect tool, toosynchronize data with a single AD forest.</span></span>
* <span data-ttu-id="4007b-119">Здравствуйте клиента Azure Active соединитель для Forefront Identity Manager, toosynchronize данных одного или нескольких локальных лесов и/или источников данных без использования Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4007b-119">hello Azure Active tenant Connector for Forefront Identity Manager, toosynchronize data with one or more on-premises forests, and/or non-Azure AD data sources.</span></span>

## <a name="add-an-azure-ad-tenant"></a><span data-ttu-id="4007b-120">Добавление клиента Azure AD</span><span class="sxs-lookup"><span data-stu-id="4007b-120">Add an Azure AD tenant</span></span>
<span data-ttu-id="4007b-121">tooadd клиент Azure AD в hello портал Azure вход слишком[hello портал Azure](https://portal.azure.com) с учетной записью глобального администратора Azure AD, а hello слева, выберите **New**.</span><span class="sxs-lookup"><span data-stu-id="4007b-121">tooadd an Azure AD tenant in hello Azure portal, sign in too[hello Azure portal](https://portal.azure.com) with an account that is an Azure AD global administrator, and, on hello left, select **New**.</span></span>

> [!NOTE]
> <span data-ttu-id="4007b-122">В отличие от других ресурсов Azure, клиенты не являются дочерними ресурсами подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="4007b-122">Unlike other Azure resources, your tenants are not child resources of an Azure subscription.</span></span> <span data-ttu-id="4007b-123">Если отмены или истек срок действия подписки Azure, можно получить доступ с помощью Azure PowerShell, hello Azure Graph API или Центр администрирования Office 365 hello данных клиента.</span><span class="sxs-lookup"><span data-stu-id="4007b-123">If your Azure subscription is canceled or expired, you can still access your tenant data using Azure PowerShell, hello Azure Graph API, or hello Office 365 Admin Center.</span></span> <span data-ttu-id="4007b-124">Можно также связать другую подписку с клиентом hello.</span><span class="sxs-lookup"><span data-stu-id="4007b-124">You can also associate another subscription with hello tenant.</span></span>
>

## <a name="next-steps"></a><span data-ttu-id="4007b-125">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4007b-125">Next steps</span></span>
<span data-ttu-id="4007b-126">Общие сведения о лицензировании Azure AD и рекомендации по работе с этой службой см. в статье [Основы группового лицензирования в Azure Active Directory](active-directory-licensing-whatis-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="4007b-126">For a broad overview of Azure AD licensing issues and best practices, see [What is Azure Active tenant licensing?](active-directory-licensing-whatis-azure-portal.md)</span></span>
