---
title: "Как создать запрос в службу поддержки Azure | Документация Майкрософт"
description: "Создание запроса на поддержку Azure"
services: Azure Supportability
documentationcenter: 
author: ganganarayanan
manager: scotthit
editor: 
ms.assetid: fd6841ea-c1d5-4bb7-86bd-0c708d193b89
ms.service: azure-supportability
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/25/2016
ms.author: gangan
ms.openlocfilehash: 70a4762383d64dc8d568c628cf260ebd8f2d179d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-an-azure-support-request"></a><span data-ttu-id="ceceb-103">Создание запроса на поддержку Azure</span><span class="sxs-lookup"><span data-stu-id="ceceb-103">How to create an Azure support request</span></span>
## <a name="summary"></a><span data-ttu-id="ceceb-104">Сводка</span><span class="sxs-lookup"><span data-stu-id="ceceb-104">Summary</span></span>
<span data-ttu-id="ceceb-105">Клиенты Azure могут создавать запросы на поддержку и управлять ими на портале Azure [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ceceb-105">Azure customers can create and manage support requests in the Azure portal, [https://portal.azure.com](https://portal.azure.com).</span></span>

> [!NOTE]
> <span data-ttu-id="ceceb-106">Портал Azure для Германии: [https://portal.microsoftazure.de](https://portal.microsoftazure.de); портал Azure для государственных учреждений США: [https://portal.azure.us](https://portal.azure.us).</span><span class="sxs-lookup"><span data-stu-id="ceceb-106">Azure portal for Germany is [https://portal.microsoftazure.de](https://portal.microsoftazure.de) Azure portal for the United States government is [https://portal.azure.us](https://portal.azure.us).</span></span>
> 
> 

<span data-ttu-id="ceceb-107">Основываясь на отзывах клиентов, мы обновили процедуру работы с запросами на поддержку, чтобы сосредоточиться на трех основных целях:</span><span class="sxs-lookup"><span data-stu-id="ceceb-107">Based on customer feedback, we’ve updated the support request experience to focus on three main goals:</span></span>

* <span data-ttu-id="ceceb-108">**Рационализация**: уменьшение числа щелчков мышью и колонок, чтобы упростить процесс передачи запросов на поддержку.</span><span class="sxs-lookup"><span data-stu-id="ceceb-108">**Streamlined**: Reduce clicks and blades to make the process of submitting a support request simple.</span></span>
* <span data-ttu-id="ceceb-109">**Интеграция**: при устранении проблемы, связанной с ресурсом Azure, открытие запроса на поддержку должно быть простым и не требовать переключения контекста.</span><span class="sxs-lookup"><span data-stu-id="ceceb-109">**Integrated**: When you’re troubleshooting an issue with an Azure resource, it should be easy to open a support request for that resource without switching context.</span></span>
* <span data-ttu-id="ceceb-110">**Эффективность**: собирайте ключевую информацию, которая поможет сотруднику службы поддержки эффективно решить вашу проблему.</span><span class="sxs-lookup"><span data-stu-id="ceceb-110">**Efficient**: Gather the key information your support engineer will need to efficiently resolve your issue.</span></span>

## <a name="getting-started"></a><span data-ttu-id="ceceb-111">Приступая к работе</span><span class="sxs-lookup"><span data-stu-id="ceceb-111">Getting started</span></span>
<span data-ttu-id="ceceb-112">Запрос на поддержку можно создать в верхнем меню навигации или непосредственно из колонки ресурсов.</span><span class="sxs-lookup"><span data-stu-id="ceceb-112">You can create a support request from the top navigation menu or directly from a resource blade.</span></span>

<span data-ttu-id="ceceb-113">**Использование верхней панели навигации**</span><span class="sxs-lookup"><span data-stu-id="ceceb-113">**From the top navigation bar**</span></span>

![Новый запрос на поддержку](./media/how-to-create-azure-support-request/NewSupportRequest.png)

<span data-ttu-id="ceceb-115">**Использование колонки ресурсов**</span><span class="sxs-lookup"><span data-stu-id="ceceb-115">**From a resource blade**</span></span>

![Контекст](./media/how-to-create-azure-support-request/Incontext.png)

## <a name="basics"></a><span data-ttu-id="ceceb-117">Основы</span><span class="sxs-lookup"><span data-stu-id="ceceb-117">Basics</span></span>
<span data-ttu-id="ceceb-118">Первый шаг при отправке запроса на поддержку заключается в сборе сведений о возникшей проблеме и вашем плане поддержки.</span><span class="sxs-lookup"><span data-stu-id="ceceb-118">The first step of the support request process gathers basic information about your issue and your support plan.</span></span>

<span data-ttu-id="ceceb-119">Рассмотрим такой пример: возникли технические трудности с виртуальной машиной, и вы подозреваете наличие проблемы с сетевыми подключениями.</span><span class="sxs-lookup"><span data-stu-id="ceceb-119">Let’s take an example: You’re facing technical difficulties with your virtual machine and suspect a network connectivity issue.</span></span>
<span data-ttu-id="ceceb-120">После выбора службы ("виртуальная машина под управлением Windows") и ресурса (имя виртуальной машины) в первом шаге мастера начинается процедура оказания помощи.</span><span class="sxs-lookup"><span data-stu-id="ceceb-120">Selecting the service ("Virtual Machine running Windows") and the resource (the name of your virtual machine) in the first step of the wizard starts the process of getting help for this issue.</span></span>

![Колонка «Основные»](./media/how-to-create-azure-support-request/Basics.png)

> [!NOTE]
> <span data-ttu-id="ceceb-122">Azure предоставляет неограниченную поддержку для управления подписками (например, выставления счетов, корректировки квот и передачи учетных записей).</span><span class="sxs-lookup"><span data-stu-id="ceceb-122">Azure provides unlimited support for subscription management (things like billing, quota adjustments, and account transfers).</span></span> <span data-ttu-id="ceceb-123">Чтобы получить техническую поддержку, у вас должен быть план поддержки.</span><span class="sxs-lookup"><span data-stu-id="ceceb-123">For technical support, you need a support plan.</span></span> <span data-ttu-id="ceceb-124">[Дополнительные сведения о планах поддержки](https://azure.microsoft.com/support/plans).</span><span class="sxs-lookup"><span data-stu-id="ceceb-124">[Learn more about support plans](https://azure.microsoft.com/support/plans).</span></span>
> 
> 

## <a name="problem"></a><span data-ttu-id="ceceb-125">Проблема</span><span class="sxs-lookup"><span data-stu-id="ceceb-125">Problem</span></span>
<span data-ttu-id="ceceb-126">На втором шаге мастера собираются дополнительные сведения о проблеме.</span><span class="sxs-lookup"><span data-stu-id="ceceb-126">The second step of the wizard gathers additional details about the issue.</span></span> <span data-ttu-id="ceceb-127">Предоставление точных сведений позволяет перенаправить ваше обращение наиболее подходящему инженеру службы поддержки и оперативно приступить к диагностике проблемы.</span><span class="sxs-lookup"><span data-stu-id="ceceb-127">Providing accurate details in this step allows us to route your case to the best support engineer for the issue and to begin diagnosing the issue as soon as possible.</span></span>

![Колонка "Проблема"](./media/how-to-create-azure-support-request/Problem.png)

<span data-ttu-id="ceceb-129">В описанном выше примере с подключением виртуальных машин вам следует заполнить эту форму, чтобы указать проблему подключения к сети, а также предоставить дополнительные сведения о проблеме, включая приблизительное время ее возникновения.</span><span class="sxs-lookup"><span data-stu-id="ceceb-129">Continuing with the virtual machine connectivity example from above, you would fill out this form to indicate a network connectivity issue, and you would provide further details about the issue, including the approximate time when you experienced the issue.</span></span>

## <a name="related-help"></a><span data-ttu-id="ceceb-130">Связанные материалы</span><span class="sxs-lookup"><span data-stu-id="ceceb-130">Related Help</span></span>
<span data-ttu-id="ceceb-131">Для некоторых проблем мы предоставляем ссылки на материалы, помогающие устранить неполадки.</span><span class="sxs-lookup"><span data-stu-id="ceceb-131">For some problems, we provide related help links to troubleshoot the issue.</span></span> <span data-ttu-id="ceceb-132">Если инструкции в рекомендуемых документах не дают результата, можно продолжить создание запроса на поддержку.</span><span class="sxs-lookup"><span data-stu-id="ceceb-132">If the recommended documents do not help, you can continue through the process to create a support request.</span></span>
<span data-ttu-id="ceceb-133">![Связанные материалы](./media/how-to-create-azure-support-request/RelatedHelp.png)</span><span class="sxs-lookup"><span data-stu-id="ceceb-133">![Related help](./media/how-to-create-azure-support-request/RelatedHelp.png)</span></span>

## <a name="contact-information"></a><span data-ttu-id="ceceb-134">Контактные данные</span><span class="sxs-lookup"><span data-stu-id="ceceb-134">Contact Information</span></span>
<span data-ttu-id="ceceb-135">На последнем шаге мастера подтверждаются ваши контактные данные, чтобы мы могли связаться с вами.</span><span class="sxs-lookup"><span data-stu-id="ceceb-135">The last step of the wizard confirms your contact information so we know how to reach you.</span></span>
<span data-ttu-id="ceceb-136">![Контактные данные](./media/how-to-create-azure-support-request/ContactInformation.png)</span><span class="sxs-lookup"><span data-stu-id="ceceb-136">![Contact Information](./media/how-to-create-azure-support-request/ContactInformation.png)</span></span>

<span data-ttu-id="ceceb-137">В зависимости от серьезности проблемы вам может быть предложено указать, следует ли нам связаться с вами в рабочее время либо в любое время суток.</span><span class="sxs-lookup"><span data-stu-id="ceceb-137">Depending on the severity of your issue, you may be asked to indicate if you would like us to contact you during business hours or if you would prefer a 24x7 response, which means we may contact you at any time.</span></span>
<span data-ttu-id="ceceb-138">![Контактные данные для круглосуточной поддержки](./media/how-to-create-azure-support-request/ContactInformation-2.png)</span><span class="sxs-lookup"><span data-stu-id="ceceb-138">![Contact Information 24x7](./media/how-to-create-azure-support-request/ContactInformation-2.png)</span></span>

## <a name="manage-support-requests"></a><span data-ttu-id="ceceb-139">Управление запросами на поддержку</span><span class="sxs-lookup"><span data-stu-id="ceceb-139">Manage support requests</span></span>
<span data-ttu-id="ceceb-140">После создания запроса на поддержку сведения о нем можно просмотреть на странице **Управление запросами в службу поддержки** .</span><span class="sxs-lookup"><span data-stu-id="ceceb-140">After you create the support request, you can view the details from the **Manage Support Requests** page.</span></span>

<span data-ttu-id="ceceb-141">**Использование верхней панели навигации**</span><span class="sxs-lookup"><span data-stu-id="ceceb-141">**From the top navigation bar**</span></span>

![Ссылка на страницу "Управление запросом на поддержку"](./media/how-to-create-azure-support-request/ManageSupportRequest-link.png)

<span data-ttu-id="ceceb-143">На странице **Управление запросами в службу поддержки** можно просмотреть все запросы и их состояние.</span><span class="sxs-lookup"><span data-stu-id="ceceb-143">On the **Manage support requests** page, you can view all support requests and their status.</span></span>
<span data-ttu-id="ceceb-144">![Управление запросом на поддержку](./media/how-to-create-azure-support-request/ManageSupportRequest.png)</span><span class="sxs-lookup"><span data-stu-id="ceceb-144">![Manage Support Request](./media/how-to-create-azure-support-request/ManageSupportRequest.png)</span></span>

<span data-ttu-id="ceceb-145">Выберите запрос, чтобы просмотреть сведения, включая серьезность и ожидаемое время для ответа сотрудника службы поддержки.</span><span class="sxs-lookup"><span data-stu-id="ceceb-145">Select the support request to view details, including severity and the expected time it will take for a support engineer to respond.</span></span>
<span data-ttu-id="ceceb-146">![VID](./media/how-to-create-azure-support-request/VID.png)</span><span class="sxs-lookup"><span data-stu-id="ceceb-146">![VID](./media/how-to-create-azure-support-request/VID.png)</span></span>

<span data-ttu-id="ceceb-147">Если вы хотите изменить серьезность запроса, щелкните элемент **Влияние на бизнес** .</span><span class="sxs-lookup"><span data-stu-id="ceceb-147">If you want to change the severity of the request, click the **Business impact** tile.</span></span> <span data-ttu-id="ceceb-148">В предыдущем примере запросу присвоен уровень серьезности C.</span><span class="sxs-lookup"><span data-stu-id="ceceb-148">In the preceeding example, the request is currently set to Severity C.</span></span>

<span data-ttu-id="ceceb-149">При выборе элемента отображается список уровней серьезности, которые можно назначить открытому запросу.</span><span class="sxs-lookup"><span data-stu-id="ceceb-149">Clicking the tile shows you the list of severities you can assign to an open support request.</span></span>

> [!NOTE]
> <span data-ttu-id="ceceb-150">Максимальный уровень серьезности зависит от плана поддержки.</span><span class="sxs-lookup"><span data-stu-id="ceceb-150">The maximum severity level depends on your support plan.</span></span> <span data-ttu-id="ceceb-151">[Дополнительные сведения о планах поддержки](https://azure.microsoft.com/support/plans).</span><span class="sxs-lookup"><span data-stu-id="ceceb-151">[Learn more about support plans](https://azure.microsoft.com/support/plans).</span></span>
> 
> 

![VID-2](./media/how-to-create-azure-support-request/VID-2.png)

## <a name="feedback"></a><span data-ttu-id="ceceb-153">Отзыв</span><span class="sxs-lookup"><span data-stu-id="ceceb-153">Feedback</span></span>
<span data-ttu-id="ceceb-154">Мы всегда рады вашим отзывам и предложениям!</span><span class="sxs-lookup"><span data-stu-id="ceceb-154">We are always open to feedback and suggestions!</span></span> <span data-ttu-id="ceceb-155">Отправьте нам свои [предложения](https://feedback.azure.com/forums/266794-support-feedback).</span><span class="sxs-lookup"><span data-stu-id="ceceb-155">Please send us your [suggestions](https://feedback.azure.com/forums/266794-support-feedback).</span></span> <span data-ttu-id="ceceb-156">Кроме того, с нами можно связаться через [Twitter](https://twitter.com/azuresupport) или [форумы MSDN](https://social.msdn.microsoft.com/Forums/azure).</span><span class="sxs-lookup"><span data-stu-id="ceceb-156">Additionally, you can engage with us via [Twitter](https://twitter.com/azuresupport) or the [MSDN forums](https://social.msdn.microsoft.com/Forums/azure).</span></span>

## <a name="learn-more"></a><span data-ttu-id="ceceb-157">Подробнее</span><span class="sxs-lookup"><span data-stu-id="ceceb-157">Learn more</span></span>
[<span data-ttu-id="ceceb-158">Часто задаваемые вопросы о поддержке Azure</span><span class="sxs-lookup"><span data-stu-id="ceceb-158">Azure Support FAQ</span></span>](https://azure.microsoft.com/support/faq)

