---
title: "Характеристики взаимодействия клиентов Azure Active Directory | Документация Майкрософт"
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
ms.openlocfilehash: d25d2c731034d0785bbd404ec693c4c41d913d01
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="understand-how-multiple-azure-active-directory-tenants-interact"></a><span data-ttu-id="d891c-103">Сведения о взаимодействии нескольких клиентов Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d891c-103">Understand how multiple Azure Active Directory tenants interact</span></span>

<span data-ttu-id="d891c-104">В Azure Active Directory (Azure AD) каждый клиент является полностью независимым ресурсом: равноправным, полнофункциональным и логически независимым от других клиентов, которыми вы управляете.</span><span class="sxs-lookup"><span data-stu-id="d891c-104">In Azure Active Directory (Azure AD), each tenent is a fully independent resource: a peer that is logically independent from the other tenants that you manage.</span></span> <span data-ttu-id="d891c-105">Между клиентами нет связи типа "родительский объект — дочерний объект".</span><span class="sxs-lookup"><span data-stu-id="d891c-105">There is no parent-child relationship between tenants.</span></span> <span data-ttu-id="d891c-106">Такая независимость клиентов подразумевает и независимость ресурсов, административную независимость и независимость синхронизации.</span><span class="sxs-lookup"><span data-stu-id="d891c-106">This independence between tenants includes resource independence, administrative independence, and synchronization independence.</span></span>

## <a name="resource-independence"></a><span data-ttu-id="d891c-107">Независимость ресурсов</span><span class="sxs-lookup"><span data-stu-id="d891c-107">Resource independence</span></span>
* <span data-ttu-id="d891c-108">Если создать или удалить ресурс в одном клиенте, это не повлияет на какой-либо ресурс в другом клиенте, за исключением внешних пользователей.</span><span class="sxs-lookup"><span data-stu-id="d891c-108">If you create or delete a resource in one tenant, it has no impact on any resource in another tenant, with the partial exception of external users.</span></span> 
* <span data-ttu-id="d891c-109">Если какое-либо из доменных имен используется для одного клиента, то оно не может использоваться для любого другого клиента.</span><span class="sxs-lookup"><span data-stu-id="d891c-109">If you use one of your domain names with one tenant, it cannot be used with any other tenant.</span></span>

## <a name="administrative-independence"></a><span data-ttu-id="d891c-110">Административная независимость</span><span class="sxs-lookup"><span data-stu-id="d891c-110">Administrative independence</span></span>
<span data-ttu-id="d891c-111">Если пользователь без прав администратора клиента Contoso создает тестовый клиент Test, то:</span><span class="sxs-lookup"><span data-stu-id="d891c-111">If a non-administrative user of tenant 'Contoso' creates a test tenant 'Test,' then:</span></span>

* <span data-ttu-id="d891c-112">По умолчанию пользователь, создающий новый клиент, добавляется в него в качестве внешнего пользователя, и ему назначается роль глобального администратора этого клиента.</span><span class="sxs-lookup"><span data-stu-id="d891c-112">By default, the user who creates a tenant is added as an external user in that new tenant, and assigned the global administrator role in that tenant.</span></span>
* <span data-ttu-id="d891c-113">У администраторов клиента Contoso нет прямых прав администратора для клиента Test, пока администратор Test явно не предоставит им эти привилегии.</span><span class="sxs-lookup"><span data-stu-id="d891c-113">The administrators of tenant 'Contoso' have no direct administrative privileges to tenant 'Test,' unless an administrator of 'Test' specifically grants them these privileges.</span></span> <span data-ttu-id="d891c-114">Тем не менее администраторы Contoso могут контролировать доступ к клиенту Test, если они управляют учетной записью пользователя, создавшего клиент Test.</span><span class="sxs-lookup"><span data-stu-id="d891c-114">However, administrators of 'Contoso' can control access to tenant 'Test' if they control the user account that created 'Test.'</span></span>
* <span data-ttu-id="d891c-115">Если добавить или удалить роль администратора для пользователя в одном клиенте, это изменение не повлияет на роли администратора, которые назначены пользователю в другом клиенте.</span><span class="sxs-lookup"><span data-stu-id="d891c-115">If you add/remove an administrator role for a user in one tenant, the change does not affect the administrator roles that the user has in another tenant.</span></span>

## <a name="synchronization-independence"></a><span data-ttu-id="d891c-116">Независимость синхронизации</span><span class="sxs-lookup"><span data-stu-id="d891c-116">Synchronization independence</span></span>
<span data-ttu-id="d891c-117">Вы можете настроить каждый клиент Azure AD независимо, чтобы синхронизировать данные из одного из следующих экземпляров:</span><span class="sxs-lookup"><span data-stu-id="d891c-117">You can configure each Azure AD tenant independently to get data synchronized from a single instance of either:</span></span>

* <span data-ttu-id="d891c-118">инструмент Azure AD Connect для синхронизации данных с одним лесом AD;</span><span class="sxs-lookup"><span data-stu-id="d891c-118">The Azure AD Connect tool, to synchronize data with a single AD forest.</span></span>
* <span data-ttu-id="d891c-119">соединитель Azure Active Directory для Forefront Identity Manager для синхронизации данных с одним или несколькими локальными лесами либо источниками данных за пределами Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d891c-119">The Azure Active tenant Connector for Forefront Identity Manager, to synchronize data with one or more on-premises forests, and/or non-Azure AD data sources.</span></span>

## <a name="add-an-azure-ad-tenant"></a><span data-ttu-id="d891c-120">Добавление клиента Azure AD</span><span class="sxs-lookup"><span data-stu-id="d891c-120">Add an Azure AD tenant</span></span>
<span data-ttu-id="d891c-121">Чтобы добавить клиент Azure AD на портале Azure, войдите на [портал Azure](https://portal.azure.com) под учетной записью глобального администратора Azure AD, а затем щелкните слева **Создать**.</span><span class="sxs-lookup"><span data-stu-id="d891c-121">To add an Azure AD tenant in the Azure portal, sign in to [the Azure portal](https://portal.azure.com) with an account that is an Azure AD global administrator, and, on the left, select **New**.</span></span>

> [!NOTE]
> <span data-ttu-id="d891c-122">В отличие от других ресурсов Azure, клиенты не являются дочерними ресурсами подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="d891c-122">Unlike other Azure resources, your tenants are not child resources of an Azure subscription.</span></span> <span data-ttu-id="d891c-123">Если подписка Azure будет отменена или срок ее действия истечет, вы по-прежнему сможете работать с данными клиента с помощью Azure PowerShell, API Azure Graph или Центра администрирования Office 365.</span><span class="sxs-lookup"><span data-stu-id="d891c-123">If your Azure subscription is canceled or expired, you can still access your tenant data using Azure PowerShell, the Azure Graph API, or the Office 365 Admin Center.</span></span> <span data-ttu-id="d891c-124">Можно также связать другую подписку с клиентом.</span><span class="sxs-lookup"><span data-stu-id="d891c-124">You can also associate another subscription with the tenant.</span></span>
>

## <a name="next-steps"></a><span data-ttu-id="d891c-125">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d891c-125">Next steps</span></span>
<span data-ttu-id="d891c-126">Общие сведения о лицензировании Azure AD и рекомендации по работе с этой службой см. в статье [Основы группового лицензирования в Azure Active Directory](active-directory-licensing-whatis-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d891c-126">For a broad overview of Azure AD licensing issues and best practices, see [What is Azure Active tenant licensing?](active-directory-licensing-whatis-azure-portal.md)</span></span>
