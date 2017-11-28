---
title: "Политики хранения отчетов Azure Active Directory | Документация Майкрософт"
description: "Политики хранения данных отчета в Azure Active Directory"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 183e53b0-0647-42e7-8abe-3e9ff424de12
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/05/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: ffeba8a6c32a21c75af21f948bbd6ea88dd9278c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-report-retention-policies"></a><span data-ttu-id="b7ce2-103">Политики хранения отчетов Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b7ce2-103">Azure Active Directory report retention policies</span></span>


<span data-ttu-id="b7ce2-104">Эта статья содержит ответы на часто задаваемые вопросы о хранении данных для разных отчетов о действиях в Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b7ce2-104">This topic provides you with answers to the most common questions in conjunction with the data retention for the different activity reports in Azure Active Directory.</span></span> 

<span data-ttu-id="b7ce2-105">**Вопрос. Как начать сбор данных о действиях?**</span><span class="sxs-lookup"><span data-stu-id="b7ce2-105">**Q: How can you get the collection of activity data started?**</span></span>

<span data-ttu-id="b7ce2-106">**Ответ.**</span><span class="sxs-lookup"><span data-stu-id="b7ce2-106">**A:**</span></span>

| <span data-ttu-id="b7ce2-107">Выпуск Azure AD</span><span class="sxs-lookup"><span data-stu-id="b7ce2-107">Azure AD Edition</span></span> | <span data-ttu-id="b7ce2-108">Начало сбора</span><span class="sxs-lookup"><span data-stu-id="b7ce2-108">Collection Start</span></span> |
| :--              | :--   |
| <span data-ttu-id="b7ce2-109">Azure AD Premium P1</span><span class="sxs-lookup"><span data-stu-id="b7ce2-109">Azure AD Premium P1</span></span> <br /> <span data-ttu-id="b7ce2-110">Azure AD Premium P2</span><span class="sxs-lookup"><span data-stu-id="b7ce2-110">Azure AD Premium P2</span></span> | <span data-ttu-id="b7ce2-111">При регистрации для подписки</span><span class="sxs-lookup"><span data-stu-id="b7ce2-111">When you sign-up for a subscription</span></span> |
| <span data-ttu-id="b7ce2-112">Azure AD уровня "Бесплатный"</span><span class="sxs-lookup"><span data-stu-id="b7ce2-112">Azure AD Free</span></span> | <span data-ttu-id="b7ce2-113">При первом открытии [колонки Azure Active Directory](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview) или использовании [API-интерфейсов отчетности](https://aka.ms/aadreports)</span><span class="sxs-lookup"><span data-stu-id="b7ce2-113">The first time you open the [Azure Active Directory blade](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview) or use the [reporting APIs](https://aka.ms/aadreports)</span></span>  |

---
<span data-ttu-id="b7ce2-114">**Вопрос. Когда данные о действиях становятся доступными на портале Azure?**</span><span class="sxs-lookup"><span data-stu-id="b7ce2-114">**Q: When is your activity data available in the Azure portal?**</span></span>

<span data-ttu-id="b7ce2-115">**Ответ.**</span><span class="sxs-lookup"><span data-stu-id="b7ce2-115">**A:**</span></span>

- <span data-ttu-id="b7ce2-116">**Немедленно** — если вы уже работали с отчетами на классическом портале Azure.</span><span class="sxs-lookup"><span data-stu-id="b7ce2-116">**Immediately** - If you have already been working with reports in the Azure classic portal</span></span>
- <span data-ttu-id="b7ce2-117">**В течение 2 часов** — если вы не включили функцию отчетности на классическом портале Azure.</span><span class="sxs-lookup"><span data-stu-id="b7ce2-117">**Within 2 hours** - If you haven’t turned reporting on  in the Azure classic portal</span></span>

---
<span data-ttu-id="b7ce2-118">**Вопрос. Как начать сбор сигналов системы безопасности?**</span><span class="sxs-lookup"><span data-stu-id="b7ce2-118">**Q: How can you get the collection of security signals started?**</span></span>  

<span data-ttu-id="b7ce2-119">**Ответ.** Процесс сбора сигналов системы безопасности начинается, когда вы соглашаетесь использовать центр защиты идентификации.</span><span class="sxs-lookup"><span data-stu-id="b7ce2-119">**A:** For security signals, the collection process starts when you opt-in to use the Identity Protection Center.</span></span> 


---
<span data-ttu-id="b7ce2-120">**Вопрос. Как долго хранятся собранные данные?**</span><span class="sxs-lookup"><span data-stu-id="b7ce2-120">**Q: For how long is the collected data stored?**</span></span>

<span data-ttu-id="b7ce2-121">**Ответ.**</span><span class="sxs-lookup"><span data-stu-id="b7ce2-121">**A:**</span></span>

<span data-ttu-id="b7ce2-122">**Отчеты о действиях**</span><span class="sxs-lookup"><span data-stu-id="b7ce2-122">**Activity reports**</span></span>    

| <span data-ttu-id="b7ce2-123">Отчет</span><span class="sxs-lookup"><span data-stu-id="b7ce2-123">Report</span></span>                 | <span data-ttu-id="b7ce2-124">Azure AD уровня "Бесплатный"</span><span class="sxs-lookup"><span data-stu-id="b7ce2-124">Azure AD Free</span></span> | <span data-ttu-id="b7ce2-125">Azure AD Premium P1</span><span class="sxs-lookup"><span data-stu-id="b7ce2-125">Azure AD Premium P1</span></span> | <span data-ttu-id="b7ce2-126">Azure AD Premium P2</span><span class="sxs-lookup"><span data-stu-id="b7ce2-126">Azure AD Premium P2</span></span> |
| :--                    | :--           | :--                 | :--                 |
| <span data-ttu-id="b7ce2-127">Аудит каталога</span><span class="sxs-lookup"><span data-stu-id="b7ce2-127">Directory Audit</span></span>        | <span data-ttu-id="b7ce2-128">7 дней</span><span class="sxs-lookup"><span data-stu-id="b7ce2-128">7 days</span></span>        | <span data-ttu-id="b7ce2-129">30 дней</span><span class="sxs-lookup"><span data-stu-id="b7ce2-129">30 days</span></span>             | <span data-ttu-id="b7ce2-130">30 дней</span><span class="sxs-lookup"><span data-stu-id="b7ce2-130">30 days</span></span>             |
| <span data-ttu-id="b7ce2-131">Действия при входе</span><span class="sxs-lookup"><span data-stu-id="b7ce2-131">Sign-in Activity</span></span>       | <span data-ttu-id="b7ce2-132">7 дней</span><span class="sxs-lookup"><span data-stu-id="b7ce2-132">7 days</span></span>        | <span data-ttu-id="b7ce2-133">30 дней</span><span class="sxs-lookup"><span data-stu-id="b7ce2-133">30 days</span></span>             | <span data-ttu-id="b7ce2-134">30 дней</span><span class="sxs-lookup"><span data-stu-id="b7ce2-134">30 days</span></span>             |

<span data-ttu-id="b7ce2-135">**Сигналы системы безопасности**</span><span class="sxs-lookup"><span data-stu-id="b7ce2-135">**Security Signals**</span></span>

| <span data-ttu-id="b7ce2-136">Отчет</span><span class="sxs-lookup"><span data-stu-id="b7ce2-136">Report</span></span>         | <span data-ttu-id="b7ce2-137">Azure AD уровня "Бесплатный"</span><span class="sxs-lookup"><span data-stu-id="b7ce2-137">Azure AD Free</span></span> | <span data-ttu-id="b7ce2-138">Azure AD Premium P1</span><span class="sxs-lookup"><span data-stu-id="b7ce2-138">Azure AD Premium P1</span></span> | <span data-ttu-id="b7ce2-139">Azure AD Premium P2</span><span class="sxs-lookup"><span data-stu-id="b7ce2-139">Azure AD Premium P2</span></span> |
| :--            | :--           | :--                 | :--                 |
| <span data-ttu-id="b7ce2-140">пользователи под угрозой;</span><span class="sxs-lookup"><span data-stu-id="b7ce2-140">Users at risk</span></span>  | <span data-ttu-id="b7ce2-141">7 дней</span><span class="sxs-lookup"><span data-stu-id="b7ce2-141">7 days</span></span>        | <span data-ttu-id="b7ce2-142">30 дней</span><span class="sxs-lookup"><span data-stu-id="b7ce2-142">30 days</span></span>             | <span data-ttu-id="b7ce2-143">90 дней</span><span class="sxs-lookup"><span data-stu-id="b7ce2-143">90 days</span></span>             |
| <span data-ttu-id="b7ce2-144">Вход, представляющий риск</span><span class="sxs-lookup"><span data-stu-id="b7ce2-144">Risky sign-ins</span></span> | <span data-ttu-id="b7ce2-145">7 дней</span><span class="sxs-lookup"><span data-stu-id="b7ce2-145">7 days</span></span>        | <span data-ttu-id="b7ce2-146">30 дней</span><span class="sxs-lookup"><span data-stu-id="b7ce2-146">30 days</span></span>             | <span data-ttu-id="b7ce2-147">90 дней</span><span class="sxs-lookup"><span data-stu-id="b7ce2-147">90 days</span></span>             |

---