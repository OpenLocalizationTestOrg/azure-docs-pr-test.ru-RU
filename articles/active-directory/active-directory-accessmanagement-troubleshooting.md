---
title: "Устранение неполадок динамического членства в группах | Документация Майкрософт"
description: "Советы по устранению неполадок динамического членства в группах в Azure AD."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 89bb04b6-a379-49c2-8465-fe386641816a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: curtand
ms.openlocfilehash: 32947e8cc69c9a48d9a285bf0a37ab3398571f86
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-dynamic-memberships-for-groups"></a><span data-ttu-id="78f50-103">Устранение неполадок, связанных с динамическим членством в группах</span><span class="sxs-lookup"><span data-stu-id="78f50-103">Troubleshooting dynamic memberships for groups</span></span>
<span data-ttu-id="78f50-104">**Мной было настроено правило для группы, но обновление членства в группе не произошло.**</span><span class="sxs-lookup"><span data-stu-id="78f50-104">**I configured a rule on a group but no memberships get updated in the group**</span></span><br/><span data-ttu-id="78f50-105">Убедитесь, что на вкладке **Настройка** параметр **Разрешить делегированное управление группой** имеет значение **Да**.</span><span class="sxs-lookup"><span data-stu-id="78f50-105">Verify that the **Enable delegated group management** setting is set to **Yes** in the **Configure** tab.</span></span> <span data-ttu-id="78f50-106">Этот параметр отображается только в том случае, если вы вошли в систему как пользователь, которому назначена лицензия Azure Active Directory Premium.</span><span class="sxs-lookup"><span data-stu-id="78f50-106">You will see this setting only if you are signed in as a user to whom an Azure Active Directory Premium license is assigned.</span></span> <span data-ttu-id="78f50-107">Проверьте значения атрибутов пользователей в правиле — существуют ли пользователи, удовлетворяющие правилу?</span><span class="sxs-lookup"><span data-stu-id="78f50-107">Verify the values for user attributes on the rule: are there users that satisfy the rule?</span></span>

<span data-ttu-id="78f50-108">**Мной было настроено правило, но теперь существующие участники правила удалены.**</span><span class="sxs-lookup"><span data-stu-id="78f50-108">**I configured a rule, but now the existing members of the rule are removed**</span></span><br/><span data-ttu-id="78f50-109">Это ожидаемое поведение.</span><span class="sxs-lookup"><span data-stu-id="78f50-109">This is expected behavior.</span></span> <span data-ttu-id="78f50-110">Существующие участники группы удаляются при включении или изменении правила.</span><span class="sxs-lookup"><span data-stu-id="78f50-110">Existing members of the group are removed when a rule is enabled or changed.</span></span> <span data-ttu-id="78f50-111">В группу добавляются пользователи, подобранные на основе оценки правила.</span><span class="sxs-lookup"><span data-stu-id="78f50-111">The users returned from evaluation of the rule are added as members to the group.</span></span>     

<span data-ttu-id="78f50-112">**Я не вижу мгновенного изменения членства, когда добавляю или изменяю правило. Почему?**</span><span class="sxs-lookup"><span data-stu-id="78f50-112">**I don’t see membership changes instantly when I add or change a rule, why not?**</span></span><br/><span data-ttu-id="78f50-113">Специальная оценка членства выполняется периодически в асинхронном фоновом процессе.</span><span class="sxs-lookup"><span data-stu-id="78f50-113">Dedicated membership evaluation is done periodically in an asynchronous background process.</span></span> <span data-ttu-id="78f50-114">На длительность процесса влияют количество пользователей в каталоге и размер группы, созданной в результате оценки правила.</span><span class="sxs-lookup"><span data-stu-id="78f50-114">How long the process takes is determined by the number of users in your directory and the size of the group created as a result of the rule.</span></span> <span data-ttu-id="78f50-115">Обычно каталоги с небольшим количеством пользователей выявят изменения членства в группах уже через несколько минут.</span><span class="sxs-lookup"><span data-stu-id="78f50-115">Typically, directories with small numbers of users will see the group membership changes in less than a few minutes.</span></span> <span data-ttu-id="78f50-116">В случае каталогов с большим числом пользователей заполнение может занять 30 минут или больше.</span><span class="sxs-lookup"><span data-stu-id="78f50-116">Directories with a large number of users can take 30 minutes or longer to populate.</span></span>

### <a name="next-steps"></a><span data-ttu-id="78f50-117">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="78f50-117">Next steps</span></span>
<span data-ttu-id="78f50-118">В следующих статьях содержатся дополнительные сведения об Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="78f50-118">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="78f50-119">Управление доступом к ресурсам с помощью групп Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="78f50-119">Managing access to resources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="78f50-120">Указатель статьей по управлению приложениями в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="78f50-120">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="78f50-121">Что такое Microsoft Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="78f50-121">What is Azure Active Directory?</span></span>](active-directory-whatis.md)
* [<span data-ttu-id="78f50-122">Интеграция локальных удостоверений с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="78f50-122">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
