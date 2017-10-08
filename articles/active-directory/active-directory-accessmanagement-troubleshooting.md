---
title: "aaaTroubleshooting динамическое членство для групп | Документы Microsoft"
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
ms.openlocfilehash: d792fc406288844e2c5dbe3702c2c9870d09473e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-dynamic-memberships-for-groups"></a><span data-ttu-id="08522-103">Устранение неполадок, связанных с динамическим членством в группах</span><span class="sxs-lookup"><span data-stu-id="08522-103">Troubleshooting dynamic memberships for groups</span></span>
<span data-ttu-id="08522-104">**Я настроил правило в группе, но обновления не членства в группе hello**</span><span class="sxs-lookup"><span data-stu-id="08522-104">**I configured a rule on a group but no memberships get updated in hello group**</span></span><br/><span data-ttu-id="08522-105">Убедитесь, что hello **делегированное управление группами** установлено слишком**Да** в hello **Настройка** вкладки. Вы увидите этот параметр только в том случае, если вы вошли как назначается toowhom пользователю лицензию Azure Active Directory Premium.</span><span class="sxs-lookup"><span data-stu-id="08522-105">Verify that hello **Enable delegated group management** setting is set too**Yes** in hello **Configure** tab. You will see this setting only if you are signed in as a user toowhom an Azure Active Directory Premium license is assigned.</span></span> <span data-ttu-id="08522-106">Проверка значений hello для атрибутов пользователей на правило hello: имеются пользователи, которые удовлетворяют правилу hello?</span><span class="sxs-lookup"><span data-stu-id="08522-106">Verify hello values for user attributes on hello rule: are there users that satisfy hello rule?</span></span>

<span data-ttu-id="08522-107">**Я настроил правило, но теперь будут удалены существующие члены правила hello hello**</span><span class="sxs-lookup"><span data-stu-id="08522-107">**I configured a rule, but now hello existing members of hello rule are removed**</span></span><br/><span data-ttu-id="08522-108">Это ожидаемое поведение.</span><span class="sxs-lookup"><span data-stu-id="08522-108">This is expected behavior.</span></span> <span data-ttu-id="08522-109">При изменении или включении правила, будут удалены существующие члены группы hello.</span><span class="sxs-lookup"><span data-stu-id="08522-109">Existing members of hello group are removed when a rule is enabled or changed.</span></span> <span data-ttu-id="08522-110">Hello пользователей, возвращаемых на основе оценки правила hello добавляются как члены группы toohello.</span><span class="sxs-lookup"><span data-stu-id="08522-110">hello users returned from evaluation of hello rule are added as members toohello group.</span></span>     

<span data-ttu-id="08522-111">**Я не вижу мгновенного изменения членства, когда добавляю или изменяю правило. Почему?**</span><span class="sxs-lookup"><span data-stu-id="08522-111">**I don’t see membership changes instantly when I add or change a rule, why not?**</span></span><br/><span data-ttu-id="08522-112">Специальная оценка членства выполняется периодически в асинхронном фоновом процессе.</span><span class="sxs-lookup"><span data-stu-id="08522-112">Dedicated membership evaluation is done periodically in an asynchronous background process.</span></span> <span data-ttu-id="08522-113">Как долго принимает hello процесса определяется hello число пользователей в группы hello, созданных в результате правило hello размер вашего каталога и hello.</span><span class="sxs-lookup"><span data-stu-id="08522-113">How long hello process takes is determined by hello number of users in your directory and hello size of hello group created as a result of hello rule.</span></span> <span data-ttu-id="08522-114">Как правило каталоги при небольшом количестве пользователей увидеть изменения членства в группе hello менее чем через несколько минут.</span><span class="sxs-lookup"><span data-stu-id="08522-114">Typically, directories with small numbers of users will see hello group membership changes in less than a few minutes.</span></span> <span data-ttu-id="08522-115">Каталоги с большим числом пользователей может занять 30 минут или дольше toopopulate.</span><span class="sxs-lookup"><span data-stu-id="08522-115">Directories with a large number of users can take 30 minutes or longer toopopulate.</span></span>

### <a name="next-steps"></a><span data-ttu-id="08522-116">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="08522-116">Next steps</span></span>
<span data-ttu-id="08522-117">В следующих статьях содержатся дополнительные сведения об Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="08522-117">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="08522-118">Управление tooresources доступ с помощью групп Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="08522-118">Managing access tooresources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="08522-119">Указатель статьей по управлению приложениями в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="08522-119">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="08522-120">Что такое Microsoft Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="08522-120">What is Azure Active Directory?</span></span>](active-directory-whatis.md)
* [<span data-ttu-id="08522-121">Интеграция локальных удостоверений с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="08522-121">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
