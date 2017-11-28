---
title: "Синхронизация Azure AD Connect: включение корзины AD | Документация Майкрософт"
description: "В этом разделе приведены рекомендации по использованию функции корзины AD с Azure AD Connect."
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
ms.openlocfilehash: eb455477547f3db8245cf3601576eba9c6fdc56f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-sync-enable-ad-recycle-bin"></a><span data-ttu-id="4e80f-104">Синхронизация Azure AD Connect: включение корзины AD</span><span class="sxs-lookup"><span data-stu-id="4e80f-104">Azure AD Connect sync: Enable AD recycle bin</span></span>
<span data-ttu-id="4e80f-105">Для локальных каталогов Active Directory, которые синхронизируются с Azure AD, рекомендуется включить функцию корзины AD.</span><span class="sxs-lookup"><span data-stu-id="4e80f-105">It is recommended that you enable the AD Recycle Bin feature for your on-premises Active Directories, which are synchronized to Azure AD.</span></span> 

<span data-ttu-id="4e80f-106">Если вы случайно удалите объект пользователя в локальной службе AD, то при восстановлении с помощью этой функции Azure AD восстановит соответствующий объект пользователя Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4e80f-106">If you accidentally deleted an on-premises AD user object and restore it using the feature, Azure AD restores the corresponding Azure AD user object.</span></span>  <span data-ttu-id="4e80f-107">Сведения о функции корзины AD см. в статье [Scenario Overview for Restoring Deleted Active Directory Objects](https://technet.microsoft.com/library/dd379542.aspx) (Обзор сценария восстановления удаленных объектов Active Directory).</span><span class="sxs-lookup"><span data-stu-id="4e80f-107">For information about the AD Recycle Bin feature, refer to article [Scenario Overview for Restoring Deleted Active Directory Objects](https://technet.microsoft.com/library/dd379542.aspx).</span></span>

## <a name="benefits-of-enabling-the-ad-recycle-bin"></a><span data-ttu-id="4e80f-108">Преимущества включения корзины AD</span><span class="sxs-lookup"><span data-stu-id="4e80f-108">Benefits of enabling the AD recycle bin</span></span>
<span data-ttu-id="4e80f-109">Эта функция помогает восстановить объекты пользователей Azure AD следующим образом:</span><span class="sxs-lookup"><span data-stu-id="4e80f-109">This feature helps with restoring Azure AD user objects by doing the following:</span></span>

* <span data-ttu-id="4e80f-110">Если вы случайно удалите объект пользователя в локальной службе AD, то соответствующий объект пользователя Azure AD будет удален при следующем цикле синхронизации.</span><span class="sxs-lookup"><span data-stu-id="4e80f-110">If you accidentally deleted an on-premises AD user object, the corresponding Azure AD user object will be deleted in the next sync cycle.</span></span> <span data-ttu-id="4e80f-111">По умолчанию Azure AD хранит удаленный объект пользователя Azure AD в состоянии обратимого удаления в течение 30 дней.</span><span class="sxs-lookup"><span data-stu-id="4e80f-111">By default, Azure AD keeps the deleted Azure AD user object in soft-deleted state for 30 days.</span></span>

* <span data-ttu-id="4e80f-112">Если у вас включена функция корзины в локальной службе AD, то вы можете восстановить удаленный объект пользователя в локальной службе AD, не изменяя его значения привязки к источнику.</span><span class="sxs-lookup"><span data-stu-id="4e80f-112">If you have on-premises AD Recycle Bin feature enabled, you can restore the deleted on-premises AD user object without changing its Source Anchor value.</span></span> <span data-ttu-id="4e80f-113">Когда восстановленный объект пользователя в локальной службе AD синхронизируется с Azure AD, служба Azure AD восстановит соответствующий объект пользователя Azure AD, находящийся с состоянии обратимого удаления.</span><span class="sxs-lookup"><span data-stu-id="4e80f-113">When the recovered on-premises AD user object is synchronized to Azure AD, Azure AD will restore the corresponding soft-deleted Azure AD user object.</span></span> <span data-ttu-id="4e80f-114">Сведения об атрибуте привязки к источнику см. в статье [Azure AD Connect: принципы проектирования](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-design-concepts#sourceanchor).</span><span class="sxs-lookup"><span data-stu-id="4e80f-114">For information about Source Anchor attribute, refer to article [Azure AD Connect: Design concepts](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-design-concepts#sourceanchor).</span></span>

* <span data-ttu-id="4e80f-115">Если функция корзины в локальной службе AD не включена, то может потребоваться создать объект пользователя AD, чтобы заменить удаленный объект.</span><span class="sxs-lookup"><span data-stu-id="4e80f-115">If you do not have on-premises AD Recycle Bin feature enabled, you may be required to create an AD user object to replace the deleted object.</span></span> <span data-ttu-id="4e80f-116">Если в службе синхронизации Azure AD Connect для атрибута привязки к источнику настроено использование создаваемого системой атрибута AD (такого как ObjectGuid), то вновь создаваемый объект пользователя AD не будет иметь то же значение привязки к источнику, что и удаленный объект пользователя AD.</span><span class="sxs-lookup"><span data-stu-id="4e80f-116">If Azure AD Connect Synchronization Service is configured to use system-generated AD attribute (such as ObjectGuid) for the Source Anchor attribute, the newly created AD user object will not have the same Source Anchor value as the deleted AD user object.</span></span> <span data-ttu-id="4e80f-117">Когда вновь созданный объект пользователя AD синхронизируется с Azure AD, служба Azure AD создаст объект пользователя Azure AD, а не восстановит соответствующий объект, находящийся с состоянии обратимого удаления.</span><span class="sxs-lookup"><span data-stu-id="4e80f-117">When the newly created AD user object is synchronized to Azure AD, Azure AD creates a new Azure AD user object instead of restoring the soft-deleted Azure AD user object.</span></span>

> [!NOTE]
> <span data-ttu-id="4e80f-118">По умолчанию Azure AD хранит удаленные объекты пользователя Azure AD в состоянии обратимого удаления в течение 30 дней, прежде чем удалить их без возможности восстановления.</span><span class="sxs-lookup"><span data-stu-id="4e80f-118">By default, Azure AD keeps deleted Azure AD user objects in soft-deleted state for 30 days before they are permanently deleted.</span></span> <span data-ttu-id="4e80f-119">Тем не менее, администраторы могут ускорить удаление таких объектов.</span><span class="sxs-lookup"><span data-stu-id="4e80f-119">However, administrators can accelerate the deletion of such objects.</span></span> <span data-ttu-id="4e80f-120">После окончательного удаления объектов их больше невозможно восстановить, даже если в локальной службе AD включена функция корзины.</span><span class="sxs-lookup"><span data-stu-id="4e80f-120">Once the objects are permanently deleted, they can no longer be recovered, even if on-premises AD Recycle Bin feature is enabled.</span></span>



## <a name="next-steps"></a><span data-ttu-id="4e80f-121">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4e80f-121">Next steps</span></span>
<span data-ttu-id="4e80f-122">**Обзорные статьи**</span><span class="sxs-lookup"><span data-stu-id="4e80f-122">**Overview topics**</span></span>

* [<span data-ttu-id="4e80f-123">Службы синхронизации Azure AD Connect: общие сведений о синхронизации и ее настройка</span><span class="sxs-lookup"><span data-stu-id="4e80f-123">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)

* [<span data-ttu-id="4e80f-124">Интеграция локальных удостоверений с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4e80f-124">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
