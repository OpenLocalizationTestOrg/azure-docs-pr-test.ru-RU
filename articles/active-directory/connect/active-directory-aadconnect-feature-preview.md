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
ms.openlocfilehash: cbf8f729d0ebfb271bb0d8702ac043442b42c262
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="more-details-about-features-in-preview"></a><span data-ttu-id="e3029-103">Дополнительная информация о функциях в предварительной версии</span><span class="sxs-lookup"><span data-stu-id="e3029-103">More details about features in preview</span></span>
<span data-ttu-id="e3029-104">В этой статье описывается, как использовать функции, которые сейчас доступны в предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="e3029-104">This topic describes how to use features currently in preview.</span></span>

## <a name="group-writeback"></a><span data-ttu-id="e3029-105">Обратная запись групп</span><span class="sxs-lookup"><span data-stu-id="e3029-105">Group writeback</span></span>
<span data-ttu-id="e3029-106">Обратная запись группы в дополнительных функциях позволит вам выполнять обратную запись **групп Office 365** в лес с установленным Exchange.</span><span class="sxs-lookup"><span data-stu-id="e3029-106">The option for group writeback in optional features allows you to writeback **Office 365 Groups** to a forest with Exchange installed.</span></span> <span data-ttu-id="e3029-107">Это группа, управление которой всегда происходит в облаке.</span><span class="sxs-lookup"><span data-stu-id="e3029-107">This is a group that is always mastered in the cloud.</span></span> <span data-ttu-id="e3029-108">При наличии локальной службы Exchange вы можете записать эти группы обратно в локальную среду, чтобы пользователи с локальными почтовыми ящиками Exchange могли отправлять и получать электронные сообщения из этих групп.</span><span class="sxs-lookup"><span data-stu-id="e3029-108">If you have Exchange on-premises, then you can write back these groups to on-premises so users with an on-premises Exchange mailbox can send and receive emails from these groups.</span></span>

<span data-ttu-id="e3029-109">Дополнительные сведения о группах Office 365 и работе с ними см. [здесь](http://aka.ms/O365g).</span><span class="sxs-lookup"><span data-stu-id="e3029-109">More information about Office 365 Groups and how to use them can be found [here](http://aka.ms/O365g).</span></span>

<span data-ttu-id="e3029-110">Группа Office 365 представлена в виде группы рассылки в локальной среде AD DS.</span><span class="sxs-lookup"><span data-stu-id="e3029-110">An Office 365 group is represented as a distribution group in on-premises AD DS.</span></span> <span data-ttu-id="e3029-111">На локальном сервере Exchange должна быть установлена версия Exchange 2013 с накопительным пакетом обновления 8 (выпущен в марте 2015 года) или Exchange 2016, чтобы он мог распознавать этот новый тип группы.</span><span class="sxs-lookup"><span data-stu-id="e3029-111">Your on-premises Exchange server must be on Exchange 2013 cumulative update 8 (released in March 2015) or Exchange 2016 to recognize this new group type.</span></span>

<span data-ttu-id="e3029-112">**Примечания на период действия предварительной версии**</span><span class="sxs-lookup"><span data-stu-id="e3029-112">**Notes during the preview**</span></span>

* <span data-ttu-id="e3029-113">Сейчас, в предварительной версии, атрибут адресной книги не заполняется.</span><span class="sxs-lookup"><span data-stu-id="e3029-113">The address book attribute is currently not populated in the preview.</span></span> <span data-ttu-id="e3029-114">Без этого атрибута группа не отображается в глобальном списке адресов.</span><span class="sxs-lookup"><span data-stu-id="e3029-114">Without this attribute, the group is not visible in the GAL.</span></span> <span data-ttu-id="e3029-115">Для заполнения этого атрибута проще всего использовать командлет Exchange PowerShell `update-recipient`.</span><span class="sxs-lookup"><span data-stu-id="e3029-115">The easiest way to populate this attribute is to use the Exchange PowerShell cmdlet `update-recipient`.</span></span>
* <span data-ttu-id="e3029-116">Только леса со схемой Exchange являются допустимыми целевыми объектами для групп.</span><span class="sxs-lookup"><span data-stu-id="e3029-116">Only forests with the Exchange schema are valid targets for groups.</span></span> <span data-ttu-id="e3029-117">Если схема Exchange не будет обнаружена, обратную запись группы не удастся включить.</span><span class="sxs-lookup"><span data-stu-id="e3029-117">If no Exchange was detected, then group writeback is not possible to enable.</span></span>
* <span data-ttu-id="e3029-118">В настоящее время поддерживаются развертывания организаций Exchange только с одним лесом.</span><span class="sxs-lookup"><span data-stu-id="e3029-118">Only single-forest Exchange organization deployments are currently supported.</span></span> <span data-ttu-id="e3029-119">При наличии нескольких локальных организаций Exchange вам потребуется локальное решение GALSync, чтобы эти группы отображались в других лесах.</span><span class="sxs-lookup"><span data-stu-id="e3029-119">If you have more than one Exchange organization on-premises, then you need an on-premises GALSync solution for these groups to appear in your other forests.</span></span>
* <span data-ttu-id="e3029-120">Функция обратной записи группы не обрабатывает группы безопасности или группы рассылки.</span><span class="sxs-lookup"><span data-stu-id="e3029-120">The Group writeback feature does not handle security groups or distribution groups.</span></span>

> [!NOTE]
> <span data-ttu-id="e3029-121">Для обратной записи групп требуется подписка Azure AD Premium.</span><span class="sxs-lookup"><span data-stu-id="e3029-121">A subscription to Azure AD Premium is required for group writeback.</span></span>
> 
>

## <a name="user-writeback"></a><span data-ttu-id="e3029-122">Обратная запись пользователей</span><span class="sxs-lookup"><span data-stu-id="e3029-122">User writeback</span></span>
> [!IMPORTANT]
> <span data-ttu-id="e3029-123">Предварительная версия функции обратной записи пользователей была удалена в августовском обновлении (2015 г.) для Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="e3029-123">The user writeback preview feature was removed in the August 2015 update to Azure AD Connect.</span></span> <span data-ttu-id="e3029-124">Если вы включили ее, следует отключить эту функцию.</span><span class="sxs-lookup"><span data-stu-id="e3029-124">If you have enabled it, then you should disable this feature.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="e3029-125">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e3029-125">Next steps</span></span>
<span data-ttu-id="e3029-126">Продолжите [выборочную установку Azure AD Connect](active-directory-aadconnect-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="e3029-126">Continue your [Custom installation of Azure AD Connect](active-directory-aadconnect-get-started-custom.md).</span></span>

<span data-ttu-id="e3029-127">Узнайте больше об [интеграции локальных удостоверений с Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="e3029-127">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
