---
title: "Azure AD Connect: предварительные версии компонентов | Документация Майкрософт"
description: "В этой статье более подробно описаны функции Azure AD Connect, находящиеся на этапе предварительной версии."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: c75cd8cf-3eff-4619-bbca-66276757cc07
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: bcfc710861b19d8f86f094ced0d1c691e0911f08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="more-details-about-features-in-preview"></a><span data-ttu-id="c4b51-103">Дополнительная информация о функциях в предварительной версии</span><span class="sxs-lookup"><span data-stu-id="c4b51-103">More details about features in preview</span></span>
<span data-ttu-id="c4b51-104">В этом разделе описывается, как toouse функции в настоящее время в предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="c4b51-104">This topic describes how toouse features currently in preview.</span></span>

## <a name="group-writeback"></a><span data-ttu-id="c4b51-105">Обратная запись групп</span><span class="sxs-lookup"><span data-stu-id="c4b51-105">Group writeback</span></span>
<span data-ttu-id="c4b51-106">параметр Hello для обратной записи групп в дополнительных компонентов позволяет toowriteback **группы Office 365** tooa леса с установленным Exchange.</span><span class="sxs-lookup"><span data-stu-id="c4b51-106">hello option for group writeback in optional features allows you toowriteback **Office 365 Groups** tooa forest with Exchange installed.</span></span> <span data-ttu-id="c4b51-107">Это группа, который управляется всегда в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="c4b51-107">This is a group that is always mastered in hello cloud.</span></span> <span data-ttu-id="c4b51-108">Если у вас есть локальные версии Exchange, затем можно написать обратно эти tooon локальные группы, пользователи, имеющие почтовый ящик в локальной среде Exchange можно отправлять и получать сообщения электронной почты из следующих групп.</span><span class="sxs-lookup"><span data-stu-id="c4b51-108">If you have Exchange on-premises, then you can write back these groups tooon-premises so users with an on-premises Exchange mailbox can send and receive emails from these groups.</span></span>

<span data-ttu-id="c4b51-109">Дополнительные сведения о группах Office 365 и как toouse их можно найти [здесь](http://aka.ms/O365g).</span><span class="sxs-lookup"><span data-stu-id="c4b51-109">More information about Office 365 Groups and how toouse them can be found [here](http://aka.ms/O365g).</span></span>

<span data-ttu-id="c4b51-110">Группа Office 365 представлена в виде группы рассылки в локальной среде AD DS.</span><span class="sxs-lookup"><span data-stu-id="c4b51-110">An Office 365 group is represented as a distribution group in on-premises AD DS.</span></span> <span data-ttu-id="c4b51-111">Ваш локальный сервер Exchange должен быть на Exchange 2013 с накопительным обновлением 8 (выпущенной в март 2015 г.) или Exchange 2016 toorecognize этот новый тип группы.</span><span class="sxs-lookup"><span data-stu-id="c4b51-111">Your on-premises Exchange server must be on Exchange 2013 cumulative update 8 (released in March 2015) or Exchange 2016 toorecognize this new group type.</span></span>

<span data-ttu-id="c4b51-112">**Заметки во время предварительного просмотра hello**</span><span class="sxs-lookup"><span data-stu-id="c4b51-112">**Notes during hello preview**</span></span>

* <span data-ttu-id="c4b51-113">в настоящее время атрибут книги адрес Hello не заполняется в режиме предварительного просмотра hello.</span><span class="sxs-lookup"><span data-stu-id="c4b51-113">hello address book attribute is currently not populated in hello preview.</span></span> <span data-ttu-id="c4b51-114">Без этого атрибута hello группы не отображается в глобальном списке адресов hello.</span><span class="sxs-lookup"><span data-stu-id="c4b51-114">Without this attribute, hello group is not visible in hello GAL.</span></span> <span data-ttu-id="c4b51-115">Здравствуйте, наиболее простым способом toopopulate этот атрибут является командлетом Exchange PowerShell hello toouse `update-recipient`.</span><span class="sxs-lookup"><span data-stu-id="c4b51-115">hello easiest way toopopulate this attribute is toouse hello Exchange PowerShell cmdlet `update-recipient`.</span></span>
* <span data-ttu-id="c4b51-116">Лес, схемы Exchange hello, допустимых целевых объектов для групп.</span><span class="sxs-lookup"><span data-stu-id="c4b51-116">Only forests with hello Exchange schema are valid targets for groups.</span></span> <span data-ttu-id="c4b51-117">Если Exchange не обнаружено, то обратной записи групп не возможных tooenable.</span><span class="sxs-lookup"><span data-stu-id="c4b51-117">If no Exchange was detected, then group writeback is not possible tooenable.</span></span>
* <span data-ttu-id="c4b51-118">В настоящее время поддерживаются развертывания организаций Exchange только с одним лесом.</span><span class="sxs-lookup"><span data-stu-id="c4b51-118">Only single-forest Exchange organization deployments are currently supported.</span></span> <span data-ttu-id="c4b51-119">При наличии более чем одной организации на локальной организации Exchange, необходимо локальное решение GALSync для этих групп tooappear в в других лесах.</span><span class="sxs-lookup"><span data-stu-id="c4b51-119">If you have more than one Exchange organization on-premises, then you need an on-premises GALSync solution for these groups tooappear in your other forests.</span></span>
* <span data-ttu-id="c4b51-120">функция обратной записи группы Hello не обрабатывает группы безопасности или группы рассылки.</span><span class="sxs-lookup"><span data-stu-id="c4b51-120">hello Group writeback feature does not handle security groups or distribution groups.</span></span>

> [!NOTE]
> <span data-ttu-id="c4b51-121">Подписки tooAzure AD Premium является обязательным для обратной записи групп.</span><span class="sxs-lookup"><span data-stu-id="c4b51-121">A subscription tooAzure AD Premium is required for group writeback.</span></span>
> 
>

## <a name="user-writeback"></a><span data-ttu-id="c4b51-122">Обратная запись пользователей</span><span class="sxs-lookup"><span data-stu-id="c4b51-122">User writeback</span></span>
> [!IMPORTANT]
> <span data-ttu-id="c4b51-123">Hello Предварительная версия функции обратной записи пользователя был удален в hello августа 2015 г. обновление tooAzure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="c4b51-123">hello user writeback preview feature was removed in hello August 2015 update tooAzure AD Connect.</span></span> <span data-ttu-id="c4b51-124">Если вы включили ее, следует отключить эту функцию.</span><span class="sxs-lookup"><span data-stu-id="c4b51-124">If you have enabled it, then you should disable this feature.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="c4b51-125">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c4b51-125">Next steps</span></span>
<span data-ttu-id="c4b51-126">Продолжите [выборочную установку Azure AD Connect](active-directory-aadconnect-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="c4b51-126">Continue your [Custom installation of Azure AD Connect](active-directory-aadconnect-get-started-custom.md).</span></span>

<span data-ttu-id="c4b51-127">Узнайте больше об [интеграции локальных удостоверений с Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="c4b51-127">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
