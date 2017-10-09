---
title: "aaaOperations Management Suite безопасности и аудита решения Web базовых | Документы Microsoft"
description: "В этом документе объясняется, как toouse OMS безопасность и аудит решения tooperform оценку базовые web всех отслеживаемых веб-серверов в целях обеспечения соответствия и безопасности."
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
ms.openlocfilehash: 8aa87fa404ff97ab549dda3f9bebb75766055963
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="web-baseline-assessment-in-operations-management-suite-security-and-audit-solution"></a><span data-ttu-id="d3bf1-103">Оценка базовых показателей в Интернете в решении "Безопасность и аудит" Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="d3bf1-103">Web Baseline Assessment in Operations Management Suite Security and Audit Solution</span></span>
<span data-ttu-id="d3bf1-104">Этот документ поможет вам toouse [решение аудита и безопасности Operations Management Suite (OMS)](operations-management-suite-overview.md) веб-оценки базовые возможности tooaccess hello безопасном состоянии отслеживаемых ресурсов.</span><span class="sxs-lookup"><span data-stu-id="d3bf1-104">This document helps you toouse [Operations Management Suite (OMS) Security and Audit Solution](operations-management-suite-overview.md) web baseline assessment capabilities tooaccess hello secure state of your monitored resources.</span></span>

## <a name="what-is-web-baseline-assessment"></a><span data-ttu-id="d3bf1-105">Что такое оценка базовых показателей в Интернете?</span><span class="sxs-lookup"><span data-stu-id="d3bf1-105">What is Web Baseline Assessment?</span></span>
<span data-ttu-id="d3bf1-106">В настоящее время система безопасности OMS предоставляет оценку базовых показателей безопасности для операционных систем.</span><span class="sxs-lookup"><span data-stu-id="d3bf1-106">Currently OMS Security provides security baseline assessment for operating systems.</span></span> <span data-ttu-id="d3bf1-107">Он проверяет параметры операционной системы hello серверов каждые 24 часа и дает представление об потенциально уязвимой параметры.</span><span class="sxs-lookup"><span data-stu-id="d3bf1-107">It scans hello operating system settings of your servers every 24 hours and provides a view into potentially vulnerable settings.</span></span> <span data-ttu-id="d3bf1-108">Дополнительные сведения об этой возможности см. в статье [Оценка базовых показателей в решении "Безопасность и аудит" Operations Management Suite](oms-security-baseline.md).</span><span class="sxs-lookup"><span data-stu-id="d3bf1-108">Read [Baseline Assessment in Operations Management Suite Security and Audit Solution](oms-security-baseline.md) for more information on this.</span></span>

<span data-ttu-id="d3bf1-109">Цель Hello hello web базовых показателей оценки — toofind потенциально уязвимой веб-сервере параметров.</span><span class="sxs-lookup"><span data-stu-id="d3bf1-109">hello goal of hello web baseline assessment is toofind potentially vulnerable web server settings.</span></span> <span data-ttu-id="d3bf1-110">Здравствуйте три основных источника для являются базовой конфигурации hello веб-: конфигурации .NET, ASP.NET и IIS.</span><span class="sxs-lookup"><span data-stu-id="d3bf1-110">hello three primary sources for hello web baseline configurations are: .NET, ASP.NET, and IIS configuration.</span></span>  <span data-ttu-id="d3bf1-111">Так же, как hello оценки базовой операционной системы, безопасность OMS будет tooscan вашего веб-серверах каждые 24-часовом и предоставляет доступ к состояние безопасности из них.</span><span class="sxs-lookup"><span data-stu-id="d3bf1-111">Just like hello operating system baseline assessment, OMS Security is going tooscan your web servers every 24hrs and provide a view into security state of them.</span></span>  <span data-ttu-id="d3bf1-112">В Internet Information Service (IIS), конфигурации являются широкие возможности настройки, позволяющее различные toobe уровни сайт и приложение переопределен.</span><span class="sxs-lookup"><span data-stu-id="d3bf1-112">In Internet Information Service (IIS), configurations are highly customizable, which allows various site and application levels toobe overridden.</span></span> <span data-ttu-id="d3bf1-113">сканер Hello проверяет параметры hello на каждом уровне приложения или на сайте, в добавление toohello по умолчанию корневого уровня.</span><span class="sxs-lookup"><span data-stu-id="d3bf1-113">hello scanner checks hello settings at each application/site level in addition toohello default root level.</span></span> <span data-ttu-id="d3bf1-114">Это помогает tooidentify потенциальной уязвимости параметры расположения и быстро устранять.</span><span class="sxs-lookup"><span data-stu-id="d3bf1-114">This helps you tooidentify potential vulnerability settings locations and quickly remediate.</span></span>


## <a name="web-security-baseline-assessment"></a><span data-ttu-id="d3bf1-115">Оценка базовых показателей безопасности в Интернете</span><span class="sxs-lookup"><span data-stu-id="d3bf1-115">Web Security Baseline Assessment</span></span>
<span data-ttu-id="d3bf1-116">Для этой предварительной версии этой функции будет toobe, получить доступ с помощью параметра поиска OMS hello.</span><span class="sxs-lookup"><span data-stu-id="d3bf1-116">For this preview this feature is going toobe accessed using hello OMS Search option.</span></span> <span data-ttu-id="d3bf1-117">Выполните действия hello под запросом tooperform hello appropriated.</span><span class="sxs-lookup"><span data-stu-id="d3bf1-117">Follow hello steps below tooperform hello appropriated query:</span></span>

1. <span data-ttu-id="d3bf1-118">В hello **Microsoft Operations Management Suite** основной панели мониторинга щелкните **безопасность и аудит** плитки.</span><span class="sxs-lookup"><span data-stu-id="d3bf1-118">In hello **Microsoft Operations Management Suite** main dashboard click **Security and Audit** tile.</span></span>
2. <span data-ttu-id="d3bf1-119">В hello **безопасность и аудит** панели мониторинга, щелкните **поиска журналов** кнопки.</span><span class="sxs-lookup"><span data-stu-id="d3bf1-119">In hello **Security and Audit** dashboard, click **Log Search** button.</span></span>
3. <span data-ttu-id="d3bf1-120">Hello первый запрос, который можно использовать — hello **Сводка по оценке базовые Web**.</span><span class="sxs-lookup"><span data-stu-id="d3bf1-120">hello first query that you can use is hello **Web Baseline Assessment Summary**.</span></span> <span data-ttu-id="d3bf1-121">В hello **начинает поиск здесь** введите этот запрос: тип*= SecurityBaselineSummary BaselineType = web*.</span><span class="sxs-lookup"><span data-stu-id="d3bf1-121">In hello **Begin search here** field, type this query: Type*=SecurityBaselineSummary BaselineType=web*.</span></span> <span data-ttu-id="d3bf1-122">Следующий экран приветствия имеет образец вывода:</span><span class="sxs-lookup"><span data-stu-id="d3bf1-122">hello following screen has an output sample:</span></span>

![Сводка по оценке базовых показателей в Интернете](./media/oms-security-web-baseline/oms-security-web-baseline-fig1-new.png)

> [!NOTE]
> <span data-ttu-id="d3bf1-124">В этом запросе каждая запись указывает сводку оценки на одном сервере.</span><span class="sxs-lookup"><span data-stu-id="d3bf1-124">In this query, each record indicates assessment summary on a single server.</span></span>

<span data-ttu-id="d3bf1-125">После входа в hello **поиска журналов**, tooobtain различных запросов можно ввести дополнительные сведения об оценке базовые hello web.</span><span class="sxs-lookup"><span data-stu-id="d3bf1-125">Once you are in hello **Log Search**, you can type different queries tooobtain more information about hello web baseline assessment.</span></span> <span data-ttu-id="d3bf1-126">В дополнение к этому toohello предыдущего запроса, также можно hello следующие функции в этой предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="d3bf1-126">In addition toohello previous query, you can also use hello following ones in this preview.</span></span>

<span data-ttu-id="d3bf1-127">**Web Baseline Rule Assessment** (Оценка правила базовых показателей в Интернете). Каждая запись представляет оценку правила базовых показателей в Интернете на одном сервере.</span><span class="sxs-lookup"><span data-stu-id="d3bf1-127">**Web Baseline Rule Assessment**: Each record represents a single web baseline rule evaluation on a single server.</span></span> <span data-ttu-id="d3bf1-128">Он включает все данные для правила hello, местоположение, hello ожидаемый результат и фактический результат hello.</span><span class="sxs-lookup"><span data-stu-id="d3bf1-128">It includes all data for hello rule, location, hello expected result, and hello actual result.</span></span>

<span data-ttu-id="d3bf1-129">**Запрос**: Type*=SecurityBaseline BaselineType=web*</span><span class="sxs-lookup"><span data-stu-id="d3bf1-129">**Query**: Type*=SecurityBaseline BaselineType=web*</span></span>

![Оценка правила базовых показателей в Интернете](./media/oms-security-web-baseline/oms-security-web-baseline-fig2.png)

<span data-ttu-id="d3bf1-131">**Показать все результаты для конкретного сервера**: этот запрос указывает, каким образом результаты toosee определенного сервера.</span><span class="sxs-lookup"><span data-stu-id="d3bf1-131">**Show all results for a specific server**: This query shows how toosee results of a specific server.</span></span>

<span data-ttu-id="d3bf1-132">**Запрос**: *Type=SecurityBaseline BaselineType=web Computer=BaselineTestVM1*</span><span class="sxs-lookup"><span data-stu-id="d3bf1-132">**Query**: *Type=SecurityBaseline BaselineType=web Computer=BaselineTestVM1*</span></span>

![Все результаты](./media/oms-security-web-baseline/oms-security-web-baseline-fig3.png)

<span data-ttu-id="d3bf1-134">Также можно использовать эти toocreate записей и запросы собственных панелей мониторинга, отчеты и оповещения.</span><span class="sxs-lookup"><span data-stu-id="d3bf1-134">You can also use these records/queries toocreate your own dashboards, reports, or alerts.</span></span> <span data-ttu-id="d3bf1-135">экран приветствия, показанный ниже имеет образец пользовательского интерфейса элемента управления, можно добавить панель мониторинга tooyour.</span><span class="sxs-lookup"><span data-stu-id="d3bf1-135">hello screen below has a sample UI control that you can add tooyour dashboard.</span></span> <span data-ttu-id="d3bf1-136">Рассказывается, как toovisualize данных с помощью конструктора представлений OMS [здесь](https://blogs.technet.microsoft.com/msoms/2016/06/30/oms-view-designer-visualize-your-data-your-way/).</span><span class="sxs-lookup"><span data-stu-id="d3bf1-136">You can learn how toovisualize your data using OMS View Designer [here](https://blogs.technet.microsoft.com/msoms/2016/06/30/oms-view-designer-visualize-your-data-your-way/).</span></span> <span data-ttu-id="d3bf1-137">экран приветствия, показанный ниже является примером как плитку hello будет выглядеть после такой настройки.</span><span class="sxs-lookup"><span data-stu-id="d3bf1-137">hello screen below is an example of how hello tile will look like once you make this customization.</span></span>

![Пример пользовательского интерфейса](./media/oms-security-web-baseline/oms-security-web-baseline-fig4.png)

> [!NOTE]
> <span data-ttu-id="d3bf1-139">Если вы хотите tooknow hello параметры, которые проверяются на наличие базовых показателей оценки hello, можно загрузить [электронную таблицу Excel](https://gallery.technet.microsoft.com/OMS-Web-Baseline-1e811690) , содержащий эти параметры.</span><span class="sxs-lookup"><span data-stu-id="d3bf1-139">If you would like tooknow hello settings that are checked for hello baseline assessment, you can download [this Excel spreadsheet](https://gallery.technet.microsoft.com/OMS-Web-Baseline-1e811690) that contains these settings.</span></span>

## <a name="see-also"></a><span data-ttu-id="d3bf1-140">См. также</span><span class="sxs-lookup"><span data-stu-id="d3bf1-140">See also</span></span>
<span data-ttu-id="d3bf1-141">В этом документе вы узнали о процедуре оценки базовых показателей в Интернете в решении OMS "Безопасность и аудит".</span><span class="sxs-lookup"><span data-stu-id="d3bf1-141">In this document, you learned about OMS Security and Audit web baseline assessment.</span></span> <span data-ttu-id="d3bf1-142">toolearn Дополнительные сведения о безопасности OMS см. следующие статьи hello.</span><span class="sxs-lookup"><span data-stu-id="d3bf1-142">toolearn more about OMS Security, see hello following articles:</span></span>

* [<span data-ttu-id="d3bf1-143">Общие сведения об Operations Management Suite (OMS)</span><span class="sxs-lookup"><span data-stu-id="d3bf1-143">Operations Management Suite (OMS) overview</span></span>](operations-management-suite-overview.md)
* [<span data-ttu-id="d3bf1-144">Мониторинг и реагирование tooSecurity оповещения в Operations Management Suite безопасности и аудита решения</span><span class="sxs-lookup"><span data-stu-id="d3bf1-144">Monitoring and Responding tooSecurity Alerts in Operations Management Suite Security and Audit Solution</span></span>](oms-security-responding-alerts.md)
* [<span data-ttu-id="d3bf1-145">Мониторинг ресурсов в решении "Безопасность и аудит" Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="d3bf1-145">Monitoring Resources in Operations Management Suite Security and Audit Solution</span></span>](oms-security-monitoring-resources.md)

