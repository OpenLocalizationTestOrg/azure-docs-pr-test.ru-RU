---
title: "Оценка базовых показателей в Интернете с помощью решения \"Безопасность и аудит\" в Operations Management Suite | Документация Майкрософт"
description: "В этом документе объясняется, как выполнить оценку базовых показателей в Интернете всех отслеживаемых веб-серверов с помощью решения \"Безопасность и аудит\" Operations Management Suite в целях обеспечения безопасности и соответствия требованиям."
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ROBOTS: NOINDEX
redirect_url: https://www.microsoft.com/cloud-platform/security-and-compliance
ms.assetid: 17837c8b-3e79-47c0-9b83-a51c6ca44ca6
ms.service: operations-management-suite
ms.custom: oms-security
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/27/2017
ms.author: yurid
ms.openlocfilehash: 0d4707dc0c0ffbf40d0d10a6d12b9709a9655258
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="web-baseline-assessment-in-operations-management-suite-security-and-audit-solution"></a><span data-ttu-id="efcf0-103">Оценка базовых показателей в Интернете в решении "Безопасность и аудит" Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="efcf0-103">Web Baseline Assessment in Operations Management Suite Security and Audit Solution</span></span>
<span data-ttu-id="efcf0-104">В этом документе показано, как использовать возможности оценки базовых показателей в Интернете [решения "Безопасность и аудит" Operations Management Suite (OMS)](operations-management-suite-overview.md), чтобы оценить безопасное состояние отслеживаемых ресурсов.</span><span class="sxs-lookup"><span data-stu-id="efcf0-104">This document helps you to use [Operations Management Suite (OMS) Security and Audit Solution](operations-management-suite-overview.md) web baseline assessment capabilities to access the secure state of your monitored resources.</span></span>

## <a name="what-is-web-baseline-assessment"></a><span data-ttu-id="efcf0-105">Что такое оценка базовых показателей в Интернете?</span><span class="sxs-lookup"><span data-stu-id="efcf0-105">What is Web Baseline Assessment?</span></span>
<span data-ttu-id="efcf0-106">В настоящее время система безопасности OMS предоставляет оценку базовых показателей безопасности для операционных систем.</span><span class="sxs-lookup"><span data-stu-id="efcf0-106">Currently OMS Security provides security baseline assessment for operating systems.</span></span> <span data-ttu-id="efcf0-107">Она проверяет параметры операционной системы серверов каждые 24 часа и позволяет получить представление о потенциально уязвимых параметрах.</span><span class="sxs-lookup"><span data-stu-id="efcf0-107">It scans the operating system settings of your servers every 24 hours and provides a view into potentially vulnerable settings.</span></span> <span data-ttu-id="efcf0-108">Дополнительные сведения об этой возможности см. в статье [Оценка базовых показателей в решении "Безопасность и аудит" Operations Management Suite](oms-security-baseline.md).</span><span class="sxs-lookup"><span data-stu-id="efcf0-108">Read [Baseline Assessment in Operations Management Suite Security and Audit Solution](oms-security-baseline.md) for more information on this.</span></span>

<span data-ttu-id="efcf0-109">Цель оценки базовых показателей в Интернете — найти потенциально уязвимые параметры веб-сервера.</span><span class="sxs-lookup"><span data-stu-id="efcf0-109">The goal of the web baseline assessment is to find potentially vulnerable web server settings.</span></span> <span data-ttu-id="efcf0-110">К трем основным источникам конфигураций базовых показателей в Интернете относятся: .NET, ASP.NET и IIS.</span><span class="sxs-lookup"><span data-stu-id="efcf0-110">The three primary sources for the web baseline configurations are: .NET, ASP.NET, and IIS configuration.</span></span>  <span data-ttu-id="efcf0-111">Аналогично оценке базовых показателей операционной системы система безопасности OMS также проверяет веб-серверы каждые 24 часа и позволяет получить представление о состоянии их безопасности.</span><span class="sxs-lookup"><span data-stu-id="efcf0-111">Just like the operating system baseline assessment, OMS Security is going to scan your web servers every 24hrs and provide a view into security state of them.</span></span>  <span data-ttu-id="efcf0-112">В службе IIS конфигурации имеют широкие возможности настройки, позволяющие переопределить различные уровни сайтов и приложений.</span><span class="sxs-lookup"><span data-stu-id="efcf0-112">In Internet Information Service (IIS), configurations are highly customizable, which allows various site and application levels to be overridden.</span></span> <span data-ttu-id="efcf0-113">Помимо корневого уровня по умолчанию, параметры также проверяются на каждом уровне приложения или сайта.</span><span class="sxs-lookup"><span data-stu-id="efcf0-113">The scanner checks the settings at each application/site level in addition to the default root level.</span></span> <span data-ttu-id="efcf0-114">Это позволяет определить расположения потенциально уязвимых параметров и быстро применить меры по устранению.</span><span class="sxs-lookup"><span data-stu-id="efcf0-114">This helps you to identify potential vulnerability settings locations and quickly remediate.</span></span>


## <a name="web-security-baseline-assessment"></a><span data-ttu-id="efcf0-115">Оценка базовых показателей безопасности в Интернете</span><span class="sxs-lookup"><span data-stu-id="efcf0-115">Web Security Baseline Assessment</span></span>
<span data-ttu-id="efcf0-116">Для этой предварительной версии доступ к данной функции будет осуществляться с помощью параметра поиска OMS.</span><span class="sxs-lookup"><span data-stu-id="efcf0-116">For this preview this feature is going to be accessed using the OMS Search option.</span></span> <span data-ttu-id="efcf0-117">Чтобы выполнить соответствующий запрос, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="efcf0-117">Follow the steps below to perform the appropriated query:</span></span>

1. <span data-ttu-id="efcf0-118">На главной панели мониторинга **Microsoft Operations Management Suite** щелкните элемент **Безопасность и аудит**.</span><span class="sxs-lookup"><span data-stu-id="efcf0-118">In the **Microsoft Operations Management Suite** main dashboard click **Security and Audit** tile.</span></span>
2. <span data-ttu-id="efcf0-119">На панели мониторинга **Безопасность и аудит** нажмите кнопку **Поиск по журналу**.</span><span class="sxs-lookup"><span data-stu-id="efcf0-119">In the **Security and Audit** dashboard, click **Log Search** button.</span></span>
3. <span data-ttu-id="efcf0-120">Первым можно использовать запрос **сводка по оценке базовых показателей в Интернете**.</span><span class="sxs-lookup"><span data-stu-id="efcf0-120">The first query that you can use is the **Web Baseline Assessment Summary**.</span></span> <span data-ttu-id="efcf0-121">В поле **Begin search here** (Начать поиск здесь) введите этот запрос: Type*=SecurityBaselineSummary BaselineType=web*.</span><span class="sxs-lookup"><span data-stu-id="efcf0-121">In the **Begin search here** field, type this query: Type*=SecurityBaselineSummary BaselineType=web*.</span></span> <span data-ttu-id="efcf0-122">Ниже приведен пример выходных данных.</span><span class="sxs-lookup"><span data-stu-id="efcf0-122">The following screen has an output sample:</span></span>

![Сводка по оценке базовых показателей в Интернете](./media/oms-security-web-baseline/oms-security-web-baseline-fig1-new.png)

> [!NOTE]
> <span data-ttu-id="efcf0-124">В этом запросе каждая запись указывает сводку оценки на одном сервере.</span><span class="sxs-lookup"><span data-stu-id="efcf0-124">In this query, each record indicates assessment summary on a single server.</span></span>

<span data-ttu-id="efcf0-125">После входа в службу **поиска журналов** можно ввести разные запросы, чтобы получить дополнительные сведения об оценке базовых показателей в Интернете.</span><span class="sxs-lookup"><span data-stu-id="efcf0-125">Once you are in the **Log Search**, you can type different queries to obtain more information about the web baseline assessment.</span></span> <span data-ttu-id="efcf0-126">Помимо предыдущего запроса в этой предварительной версии также можно использовать приведенные ниже запросы.</span><span class="sxs-lookup"><span data-stu-id="efcf0-126">In addition to the previous query, you can also use the following ones in this preview.</span></span>

<span data-ttu-id="efcf0-127">**Web Baseline Rule Assessment** (Оценка правила базовых показателей в Интернете). Каждая запись представляет оценку правила базовых показателей в Интернете на одном сервере.</span><span class="sxs-lookup"><span data-stu-id="efcf0-127">**Web Baseline Rule Assessment**: Each record represents a single web baseline rule evaluation on a single server.</span></span> <span data-ttu-id="efcf0-128">Она содержит все сведения о правиле, расположении, ожидаемый и фактический результаты.</span><span class="sxs-lookup"><span data-stu-id="efcf0-128">It includes all data for the rule, location, the expected result, and the actual result.</span></span>

<span data-ttu-id="efcf0-129">**Запрос**: Type*=SecurityBaseline BaselineType=web*</span><span class="sxs-lookup"><span data-stu-id="efcf0-129">**Query**: Type*=SecurityBaseline BaselineType=web*</span></span>

![Оценка правила базовых показателей в Интернете](./media/oms-security-web-baseline/oms-security-web-baseline-fig2.png)

<span data-ttu-id="efcf0-131">**Show all results for a specific server** (Показать все результаты для конкретного сервера). Этот запрос показывает, как просмотреть результаты определенного сервера.</span><span class="sxs-lookup"><span data-stu-id="efcf0-131">**Show all results for a specific server**: This query shows how to see results of a specific server.</span></span>

<span data-ttu-id="efcf0-132">**Запрос**: *Type=SecurityBaseline BaselineType=web Computer=BaselineTestVM1*</span><span class="sxs-lookup"><span data-stu-id="efcf0-132">**Query**: *Type=SecurityBaseline BaselineType=web Computer=BaselineTestVM1*</span></span>

![Все результаты](./media/oms-security-web-baseline/oms-security-web-baseline-fig3.png)

<span data-ttu-id="efcf0-134">Записи и запросы также можно использовать для создания панелей мониторинга, отчетов или оповещений.</span><span class="sxs-lookup"><span data-stu-id="efcf0-134">You can also use these records/queries to create your own dashboards, reports, or alerts.</span></span> <span data-ttu-id="efcf0-135">Ниже приведен пример элемента управления пользовательского интерфейса, который можно добавить на панель мониторинга.</span><span class="sxs-lookup"><span data-stu-id="efcf0-135">The screen below has a sample UI control that you can add to your dashboard.</span></span> <span data-ttu-id="efcf0-136">Дополнительные сведения о визуализации данных с помощью конструктора представлений OMS см. [здесь](https://blogs.technet.microsoft.com/msoms/2016/06/30/oms-view-designer-visualize-your-data-your-way/).</span><span class="sxs-lookup"><span data-stu-id="efcf0-136">You can learn how to visualize your data using OMS View Designer [here](https://blogs.technet.microsoft.com/msoms/2016/06/30/oms-view-designer-visualize-your-data-your-way/).</span></span> <span data-ttu-id="efcf0-137">Ниже приведен пример того, как будет выглядеть плитка после такой настройки.</span><span class="sxs-lookup"><span data-stu-id="efcf0-137">The screen below is an example of how the tile will look like once you make this customization.</span></span>

![Пример пользовательского интерфейса](./media/oms-security-web-baseline/oms-security-web-baseline-fig4.png)

> [!NOTE]
> <span data-ttu-id="efcf0-139">Если вы хотите узнать о параметрах, которые проверяются для оценки базовых показателей, скачайте [эту электронную таблицу Excel](https://gallery.technet.microsoft.com/OMS-Web-Baseline-1e811690).</span><span class="sxs-lookup"><span data-stu-id="efcf0-139">If you would like to know the settings that are checked for the baseline assessment, you can download [this Excel spreadsheet](https://gallery.technet.microsoft.com/OMS-Web-Baseline-1e811690) that contains these settings.</span></span>

## <a name="see-also"></a><span data-ttu-id="efcf0-140">См. также</span><span class="sxs-lookup"><span data-stu-id="efcf0-140">See also</span></span>
<span data-ttu-id="efcf0-141">В этом документе вы узнали о процедуре оценки базовых показателей в Интернете в решении OMS "Безопасность и аудит".</span><span class="sxs-lookup"><span data-stu-id="efcf0-141">In this document, you learned about OMS Security and Audit web baseline assessment.</span></span> <span data-ttu-id="efcf0-142">Дополнительные сведения о функциях безопасности OMS см. в следующих статьях.</span><span class="sxs-lookup"><span data-stu-id="efcf0-142">To learn more about OMS Security, see the following articles:</span></span>

* [<span data-ttu-id="efcf0-143">Общие сведения об Operations Management Suite (OMS)</span><span class="sxs-lookup"><span data-stu-id="efcf0-143">Operations Management Suite (OMS) overview</span></span>](operations-management-suite-overview.md)
* [<span data-ttu-id="efcf0-144">Мониторинг и реагирование на оповещения безопасности в решении "Безопасность и аудит" Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="efcf0-144">Monitoring and Responding to Security Alerts in Operations Management Suite Security and Audit Solution</span></span>](oms-security-responding-alerts.md)
* [<span data-ttu-id="efcf0-145">Мониторинг ресурсов в решении "Безопасность и аудит" Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="efcf0-145">Monitoring Resources in Operations Management Suite Security and Audit Solution</span></span>](oms-security-monitoring-resources.md)

