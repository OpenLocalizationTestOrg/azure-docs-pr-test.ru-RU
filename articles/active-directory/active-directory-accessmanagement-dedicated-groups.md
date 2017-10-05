---
title: "Выделенные группы в Azure Active Directory | Документация Майкрософт"
description: "Обзор работы выделенных групп в Azure Active Directory и способов их создания."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 86158909-083a-41fe-8090-955e96ad1865
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: curtand
ms.openlocfilehash: d9decd5de6a5bafc525edc5b04c82701185088ff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="dedicated-groups-in-azure-active-directory"></a><span data-ttu-id="f0f17-103">Выделенные группы в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f0f17-103">Dedicated groups in Azure Active Directory</span></span>
<span data-ttu-id="f0f17-104">В Azure Active Directory (Azure AD) функция выделенных групп автоматически создает и заполняет предварительно определенные группы Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f0f17-104">In Azure Active Directory (Azure AD), the dedicated groups feature automatically creates and populates membership for Azure AD predefined groups.</span></span> <span data-ttu-id="f0f17-105">Нельзя добавлять или удалять участников выделенных групп с помощью классического портала Azure, командлетов Windows PowerShell или программно.</span><span class="sxs-lookup"><span data-stu-id="f0f17-105">Members of dedicated groups cannot be added or removed using the Azure classic portal, Windows PowerShell cmdlets, or programmatically.</span></span>

> [!NOTE]
> <span data-ttu-id="f0f17-106">Выделенные группы требуют назначения лицензии Azure AD Premium:</span><span class="sxs-lookup"><span data-stu-id="f0f17-106">Dedicated groups require that an Azure AD Premium license is assigned to</span></span>
>
> * <span data-ttu-id="f0f17-107">администратору, который управляет правилом в группе;</span><span class="sxs-lookup"><span data-stu-id="f0f17-107">the administrator who manages the rule on a group</span></span>
> * <span data-ttu-id="f0f17-108">всем пользователям, которых правило выбрало в качестве участников группы.</span><span class="sxs-lookup"><span data-stu-id="f0f17-108">all users who are selected by the rule to be a member of the group</span></span>
>
>

<span data-ttu-id="f0f17-109">**Включение выделенных групп**</span><span class="sxs-lookup"><span data-stu-id="f0f17-109">**To enable dedicated groups**</span></span>

1. <span data-ttu-id="f0f17-110">На [классическом портале Azure](https://manage.windowsazure.com)щелкните **Active Directory**, а затем откройте каталог своей организации.</span><span class="sxs-lookup"><span data-stu-id="f0f17-110">In the [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then open your organization’s directory.</span></span>
2. <span data-ttu-id="f0f17-111">Перейдите на вкладку **Группы** , а затем откройте группу, которую нужно изменить.</span><span class="sxs-lookup"><span data-stu-id="f0f17-111">Select the **Groups** tab, and then open the group you want to edit.</span></span>
3. <span data-ttu-id="f0f17-112">Выберите вкладку **Настройка**, а затем для параметра **Включить выделенные группы** выберите значение **Да**.</span><span class="sxs-lookup"><span data-stu-id="f0f17-112">Select the **Configure** tab, and then set **Enable Dedicated Groups** to **Yes**.</span></span>

<span data-ttu-id="f0f17-113">После включения выделенных групп, т. е. выбора значения **Да**, можно дополнительно включить автоматическое создание выделенной группы "Все пользователи" в каталоге, задав для параметра **Включить группу "Все пользователи"** значение **Да**.</span><span class="sxs-lookup"><span data-stu-id="f0f17-113">Once the Enable Dedicated Groups switch is set to **Yes**, you can further enable the directory to automatically create the All Users dedicated group by setting the **Enable “All Users” Group** switch to **Yes**.</span></span> <span data-ttu-id="f0f17-114">Затем можно также изменить имя этой выделенной группы, введя его в поле **Отображаемое имя для группы "Все пользователи"**.</span><span class="sxs-lookup"><span data-stu-id="f0f17-114">You can then also edit the name of this dedicated group by typing it in the **Display Name for “All Users” Group** field.</span></span>

<span data-ttu-id="f0f17-115">Группу "Все пользователи" можно использовать для назначения одинаковых разрешений всем пользователям в каталоге.</span><span class="sxs-lookup"><span data-stu-id="f0f17-115">The All Users group can be used to assign the same permissions to all the users in your directory.</span></span> <span data-ttu-id="f0f17-116">Например, можно предоставить всем пользователям в каталоге доступ к приложению SaaS, назначив выделенной группе «Все пользователи» доступ к этому приложению.</span><span class="sxs-lookup"><span data-stu-id="f0f17-116">For example, you can grant all users in your directory access to a SaaS application by assigning access for the All Users dedicated group to this application.</span></span>

<span data-ttu-id="f0f17-117">Выделенная группа "Все пользователи" включает в себя всех пользователей в каталоге, в том числе гостей и внешних пользователей.</span><span class="sxs-lookup"><span data-stu-id="f0f17-117">The dedicated All Users group includes all users in the directory, including guests and external users.</span></span> <span data-ttu-id="f0f17-118">Если требуется группа без внешних пользователей, вы можете создать группу с помощью динамического правила на основе атрибутов, например:</span><span class="sxs-lookup"><span data-stu-id="f0f17-118">If you need a group that excludes external users, then you can accomplish this by creating a group with an attribute-based dynamic rule such as the following:</span></span>

                (user.userPrincipalName -notContains "#EXT#@")

<span data-ttu-id="f0f17-119">Для группы, не включающей в себя гостей, используйте такое правило:</span><span class="sxs-lookup"><span data-stu-id="f0f17-119">For a group that excludes all Guests, use a rule such as the following:</span></span>

                (user.userType -ne "Guest")

<span data-ttu-id="f0f17-120">Сведения о том, как создавать *более сложные* правила (которые содержат несколько сравнений), регулирующие членство в динамических группах, см. в статье [Использование атрибутов для создания расширенных правил](active-directory-accessmanagement-groups-with-advanced-rules.md).</span><span class="sxs-lookup"><span data-stu-id="f0f17-120">To learn about how to create *advanced* rules (rules that can contain multiple comparisons) for dynamic group membership, see [Using attributes to create advanced rules](active-directory-accessmanagement-groups-with-advanced-rules.md).</span></span>

### <a name="next-steps"></a><span data-ttu-id="f0f17-121">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f0f17-121">Next steps</span></span>
<span data-ttu-id="f0f17-122">В следующих статьях содержатся дополнительные сведения об Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f0f17-122">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="f0f17-123">Управление доступом к ресурсам с помощью групп Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f0f17-123">Managing access to resources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="f0f17-124">Указатель статьей по управлению приложениями в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f0f17-124">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="f0f17-125">Что такое Microsoft Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f0f17-125">What is Azure Active Directory?</span></span>](active-directory-whatis.md)
* [<span data-ttu-id="f0f17-126">Интеграция локальных удостоверений с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f0f17-126">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
