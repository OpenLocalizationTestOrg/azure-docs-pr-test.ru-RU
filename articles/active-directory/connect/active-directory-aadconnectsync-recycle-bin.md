---
title: "Синхронизация Azure AD Connect: включение корзины AD | Документация Майкрософт"
description: "В этом разделе рекомендует использование hello AD корзиной с Azure AD Connect."
services: active-directory
keywords: "корзина AD, случайное удаление, привязка к источнику"
documentationcenter: 
author: cychua
manager: femila
editor: 
ms.assetid: afec4207-74f7-4cdd-b13a-574af5223a90
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 2bb4827d677ccecfd8d2861f2a2fcf73b8cc2d95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-enable-ad-recycle-bin"></a><span data-ttu-id="e89a3-104">Синхронизация Azure AD Connect: включение корзины AD</span><span class="sxs-lookup"><span data-stu-id="e89a3-104">Azure AD Connect sync: Enable AD recycle bin</span></span>
<span data-ttu-id="e89a3-105">Рекомендуется включить hello AD Корзина для вашей локальной каталогов Active Directory, которые синхронизированные tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="e89a3-105">It is recommended that you enable hello AD Recycle Bin feature for your on-premises Active Directories, which are synchronized tooAzure AD.</span></span> 

<span data-ttu-id="e89a3-106">Если вы случайно удалены из локальной объектом пользователя AD и восстановить его с помощью функции hello Azure AD восстанавливает hello соответствующего объекта пользователя Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e89a3-106">If you accidentally deleted an on-premises AD user object and restore it using hello feature, Azure AD restores hello corresponding Azure AD user object.</span></span>  <span data-ttu-id="e89a3-107">Дополнительную информацию о hello AD корзиной tooarticle [Обзор сценария для восстановления удаленных объектов Active Directory](https://technet.microsoft.com/library/dd379542.aspx).</span><span class="sxs-lookup"><span data-stu-id="e89a3-107">For information about hello AD Recycle Bin feature, refer tooarticle [Scenario Overview for Restoring Deleted Active Directory Objects](https://technet.microsoft.com/library/dd379542.aspx).</span></span>

## <a name="benefits-of-enabling-hello-ad-recycle-bin"></a><span data-ttu-id="e89a3-108">Преимущества использования hello AD корзины.</span><span class="sxs-lookup"><span data-stu-id="e89a3-108">Benefits of enabling hello AD recycle bin</span></span>
<span data-ttu-id="e89a3-109">Эта функция позволяет с восстановлением объекты пользователя Azure AD, выполнив hello ниже:</span><span class="sxs-lookup"><span data-stu-id="e89a3-109">This feature helps with restoring Azure AD user objects by doing hello following:</span></span>

* <span data-ttu-id="e89a3-110">Если вы случайно удалены из локальной объекта пользователя AD, hello соответствующего объекта пользователя Azure AD будет удалено в hello следующего цикла синхронизации.</span><span class="sxs-lookup"><span data-stu-id="e89a3-110">If you accidentally deleted an on-premises AD user object, hello corresponding Azure AD user object will be deleted in hello next sync cycle.</span></span> <span data-ttu-id="e89a3-111">По умолчанию Azure AD хранит удалены hello объекта-пользователя Azure AD обратимо удаленные состояние в течение 30 дней.</span><span class="sxs-lookup"><span data-stu-id="e89a3-111">By default, Azure AD keeps hello deleted Azure AD user object in soft-deleted state for 30 days.</span></span>

* <span data-ttu-id="e89a3-112">При наличии в локальной среде AD корзины функция включена, можно восстановить hello удалены локального объекта пользователя AD без изменения его значения источника привязки.</span><span class="sxs-lookup"><span data-stu-id="e89a3-112">If you have on-premises AD Recycle Bin feature enabled, you can restore hello deleted on-premises AD user object without changing its Source Anchor value.</span></span> <span data-ttu-id="e89a3-113">Когда hello восстановить в локальной синхронизированным объектом пользователя AD tooAzure AD Azure AD будет восстановлена hello соответствующий обратимо удаленные объектом-пользователем Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e89a3-113">When hello recovered on-premises AD user object is synchronized tooAzure AD, Azure AD will restore hello corresponding soft-deleted Azure AD user object.</span></span> <span data-ttu-id="e89a3-114">Дополнительную информацию об атрибуте источника привязки tooarticle [Azure AD Connect: основные понятия разработки](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-design-concepts#sourceanchor).</span><span class="sxs-lookup"><span data-stu-id="e89a3-114">For information about Source Anchor attribute, refer tooarticle [Azure AD Connect: Design concepts](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-design-concepts#sourceanchor).</span></span>

* <span data-ttu-id="e89a3-115">Если у вас в локальной среде AD включена функция Bin управления, может быть обязательным toocreate AD пользователя tooreplace hello удаленного объекта.</span><span class="sxs-lookup"><span data-stu-id="e89a3-115">If you do not have on-premises AD Recycle Bin feature enabled, you may be required toocreate an AD user object tooreplace hello deleted object.</span></span> <span data-ttu-id="e89a3-116">Если служба синхронизации Azure AD Connect является настроенным toouse созданные системой AD (например, ObjectGuid) для атрибута источника привязки hello, hello вновь созданный объект пользователя AD будет не имеют hello одинаковые значения источника привязки как hello удаленный объект пользователя AD.</span><span class="sxs-lookup"><span data-stu-id="e89a3-116">If Azure AD Connect Synchronization Service is configured toouse system-generated AD attribute (such as ObjectGuid) for hello Source Anchor attribute, hello newly created AD user object will not have hello same Source Anchor value as hello deleted AD user object.</span></span> <span data-ttu-id="e89a3-117">Если hello вновь созданный объект пользователя AD синхронизированные tooAzure AD, Azure AD создает новый объект пользователя Azure AD, вместо восстановления обратимо удаленные hello объекта-пользователя Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e89a3-117">When hello newly created AD user object is synchronized tooAzure AD, Azure AD creates a new Azure AD user object instead of restoring hello soft-deleted Azure AD user object.</span></span>

> [!NOTE]
> <span data-ttu-id="e89a3-118">По умолчанию Azure AD хранит удаленные объекты пользователя Azure AD в состоянии обратимого удаления в течение 30 дней, прежде чем удалить их без возможности восстановления.</span><span class="sxs-lookup"><span data-stu-id="e89a3-118">By default, Azure AD keeps deleted Azure AD user objects in soft-deleted state for 30 days before they are permanently deleted.</span></span> <span data-ttu-id="e89a3-119">Однако администраторы могут ускорить hello удаления таких объектов.</span><span class="sxs-lookup"><span data-stu-id="e89a3-119">However, administrators can accelerate hello deletion of such objects.</span></span> <span data-ttu-id="e89a3-120">После hello объекты удаляются без возможности восстановления, они больше не может быть восстановлен, даже если в локальном AD корзиной включен.</span><span class="sxs-lookup"><span data-stu-id="e89a3-120">Once hello objects are permanently deleted, they can no longer be recovered, even if on-premises AD Recycle Bin feature is enabled.</span></span>



## <a name="next-steps"></a><span data-ttu-id="e89a3-121">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e89a3-121">Next steps</span></span>
<span data-ttu-id="e89a3-122">**Обзорные статьи**</span><span class="sxs-lookup"><span data-stu-id="e89a3-122">**Overview topics**</span></span>

* [<span data-ttu-id="e89a3-123">Службы синхронизации Azure AD Connect: общие сведений о синхронизации и ее настройка</span><span class="sxs-lookup"><span data-stu-id="e89a3-123">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)

* [<span data-ttu-id="e89a3-124">Интеграция локальных удостоверений с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e89a3-124">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
