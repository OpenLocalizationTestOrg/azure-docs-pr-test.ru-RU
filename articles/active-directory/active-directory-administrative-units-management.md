---
title: "Управление административными единицами в Azure Active Directory (предварительная версия)"
description: "Использование административных единиц для делегирования разрешений в Azure Active Directory на фрагментарном уровне"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 8464cd6b-1d1a-470d-a4fb-ee29b8eab4c4
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/17/2017
ms.author: curtand
ms.reviewer: elkuzmen
ms.custom: oldportal;it-pro;
ms.openlocfilehash: e12a0aea8264b1ea67c26294ec5bbe9c404a171e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="administrative-units-management-in-azure-ad---public-preview"></a><span data-ttu-id="d3973-103">Управление административными единицами в Azure AD (общедоступная предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="d3973-103">Administrative units management in Azure AD - public preview</span></span>
<span data-ttu-id="d3973-104">В этой статье рассматриваются административные единицы — новые контейнеры ресурсов Azure Active Directory, которые можно использовать для делегирования административных разрешений и применения политик к подмножествам пользователей.</span><span class="sxs-lookup"><span data-stu-id="d3973-104">This article describes administrative units – a new Azure Active Directory container of resources that can be used for delegating administrative permissions over subsets of users and applying policies to a subset of users.</span></span> <span data-ttu-id="d3973-105">Административные единицы Azure Active Directory позволяют администраторам центра делегировать разрешения администраторам периферии или настраивать политики на детальном уровне.</span><span class="sxs-lookup"><span data-stu-id="d3973-105">In Azure Active Directory, administrative units enable central administrators to delegate permissions to regional administrators or to set policy at a granular level.</span></span>

<span data-ttu-id="d3973-106">Это полезно для организаций с независимыми подразделениями, например большого университета, состоящего из многочисленных автономных факультетов (бизнес-школы, инженерных и технических факультетов и пр.).</span><span class="sxs-lookup"><span data-stu-id="d3973-106">This is useful in organizations with independent divisions, for example, a large university that is made up of many autonomous schools (Business school, Engineering school, and so on) which are independent from each other.</span></span> <span data-ttu-id="d3973-107">В таких структурах есть собственные ИТ-администраторы, которые управляют доступом, пользователями и политиками на уровне своего подразделения.</span><span class="sxs-lookup"><span data-stu-id="d3973-107">Such divisions have their own IT administrators who control access, manage users, and set policies specifically for their division.</span></span> <span data-ttu-id="d3973-108">Администраторам центра хотят иметь возможность предоставлять администраторам подразделений разрешения в отношении пользователей из соответствующих подразделений.</span><span class="sxs-lookup"><span data-stu-id="d3973-108">Central administrators want to be able grant these divisional administrators permissions over the users in their particular divisions.</span></span> <span data-ttu-id="d3973-109">Например, администратор центра может создать административную единицу для конкретного факультета, например бизнес-школы, и заполнить ее только данными пользователей из этой бизнес-школы.</span><span class="sxs-lookup"><span data-stu-id="d3973-109">More specifically, using this example, a central administrator can, for instance, create an administrative unit for a particular school (Business school) and populate it with only the Business school users.</span></span> <span data-ttu-id="d3973-110">Затем администратор центра может назначить ИТ-сотрудникам школы специально подготовленную роль и предоставить им административные разрешения только в отношении пользователей в административной единице (бизнес-школе).</span><span class="sxs-lookup"><span data-stu-id="d3973-110">Then a central administrator can add the Business school IT staff to a scoped role, in other words, grant the IT staff of Business school administrative permissions only over the Business school administrative unit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d3973-111">Для назначения ролей для административных единиц вам необходима активная подписка Azure Active Directory Premium.</span><span class="sxs-lookup"><span data-stu-id="d3973-111">You can assign administrative unit-scoped admin roles only if you enable Azure Active Directory Premium.</span></span> <span data-ttu-id="d3973-112">Дополнительные сведения см. в разделе [Приступая к работе с Azure AD Premium](active-directory-get-started-premium.md).</span><span class="sxs-lookup"><span data-stu-id="d3973-112">For more information, see [Getting started with Azure AD Premium](active-directory-get-started-premium.md).</span></span>
>


<span data-ttu-id="d3973-113">С точки зрения администратора центра, административная единица является объектом каталога, который можно создать и заполнить ресурсами.</span><span class="sxs-lookup"><span data-stu-id="d3973-113">From the central administrator’s point of view, an administrative unit is a directory object that can be created and populated with resources.</span></span> <span data-ttu-id="d3973-114">**В этом выпуске предварительной версии ресурсами могут быть только пользователи.**</span><span class="sxs-lookup"><span data-stu-id="d3973-114">**In this preview release, these resources can be only users.**</span></span> <span data-ttu-id="d3973-115">Созданную и заполненную административную единицу можно использовать для предоставления разрешений, ограниченных содержащимися в ней ресурсами.</span><span class="sxs-lookup"><span data-stu-id="d3973-115">Once created and populated, the administrative unit can be used as a scope to restrict the granted permission only over resources contained in the administrative unit.</span></span>

## <a name="managing-administrative-units"></a><span data-ttu-id="d3973-116">Управление административными единицами</span><span class="sxs-lookup"><span data-stu-id="d3973-116">Managing administrative units</span></span>
<span data-ttu-id="d3973-117">В предварительной версии создание и управление административными единицами осуществляется с помощью модуля Azure Active Directory для Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d3973-117">In this preview release, you can create and manage administrative units using the Azure Active Directory Module for Windows PowerShell cmdlets.</span></span> <span data-ttu-id="d3973-118">См. дополнительные сведения об [использовании административных единиц](https://docs.microsoft.com/powershell/azure/active-directory/working-with-administrative-units?view=azureadps-2.0)</span><span class="sxs-lookup"><span data-stu-id="d3973-118">To learn more about how to do that, see [Working with Administrative Units](https://docs.microsoft.com/powershell/azure/active-directory/working-with-administrative-units?view=azureadps-2.0)</span></span>

<span data-ttu-id="d3973-119">Дополнительные сведения о требованиях к программному обеспечению и установке модуля Azure AD, а также информацию о командлетах управления административными единицами через модуль Azure AD, включая синтаксис, описание параметров и примеры, см. в разделе [Управление Azure AD с помощью Windows PowerShell](https://docs.microsoft.com/powershell/azure/active-directory/overview?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="d3973-119">For more information on software requirements and installing the Azure AD module, and for information on the Azure AD Module cmdlets for managing administrative units, including syntax, parameter descriptions, and examples, see [Azure Active Directory PowerShell](https://docs.microsoft.com/powershell/azure/active-directory/overview?view=azureadps-2.0).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d3973-120">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d3973-120">Next steps</span></span>
[<span data-ttu-id="d3973-121">Выпуски Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d3973-121">Azure Active Directory editions</span></span>](active-directory-editions.md)
