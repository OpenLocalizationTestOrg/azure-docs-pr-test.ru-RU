---
title: "состояние Деградация aaaTroubleshooting о диспетчере трафика Azure"
description: "Как с состоянием деградации tootroubleshoot профилей диспетчера трафика, если он показан как."
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
ms.assetid: 8af0433d-e61b-4761-adcc-7bc9b8142fc6
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/03/2017
ms.author: kumud
ms.openlocfilehash: fd95697781472b52e98d856e66beb7b89dfeaf23
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-degraded-state-on-azure-traffic-manager"></a><span data-ttu-id="ee346-103">Устранение неполадок, связанных со сбоем диспетчера трафика</span><span class="sxs-lookup"><span data-stu-id="ee346-103">Troubleshooting degraded state on Azure Traffic Manager</span></span>

<span data-ttu-id="ee346-104">В этой статье описывается, как tootroubleshoot профиль диспетчера трафика Azure показан ограниченной состояния.</span><span class="sxs-lookup"><span data-stu-id="ee346-104">This article describes how tootroubleshoot an Azure Traffic Manager profile that is showing a degraded status.</span></span> <span data-ttu-id="ee346-105">В этом случае рассмотрите возможность настройки профиля диспетчера трафика, указывающий toosome cloudapp.net размещенных служб.</span><span class="sxs-lookup"><span data-stu-id="ee346-105">For this scenario, consider that you have configured a Traffic Manager profile pointing toosome of your cloudapp.net hosted services.</span></span> <span data-ttu-id="ee346-106">Если отображает hello работоспособности из диспетчера трафика **Деградация** состояние, а затем hello состояние одного или нескольких конечных точек может быть **Деградация**:</span><span class="sxs-lookup"><span data-stu-id="ee346-106">If hello health of your Traffic Manager displays a **Degraded** status, then hello status of one or more endpoints may be **Degraded**:</span></span>

![состояние "Деградация" конечной точки](./media/traffic-manager-troubleshooting-degraded/traffic-manager-degradedifonedegraded.png)

<span data-ttu-id="ee346-108">Если отображает hello работоспособности из диспетчера трафика **неактивно** состояние, а затем обе конечные точки могут быть **отключено**:</span><span class="sxs-lookup"><span data-stu-id="ee346-108">If hello health of your Traffic Manager displays an **Inactive** status, then both end points may be **Disabled**:</span></span>

![состояние "Неактивно" диспетчера трафика](./media/traffic-manager-troubleshooting-degraded/traffic-manager-inactive.png)

## <a name="understanding-traffic-manager-probes"></a><span data-ttu-id="ee346-110">Общие сведения о проверках диспетчера трафика</span><span class="sxs-lookup"><span data-stu-id="ee346-110">Understanding Traffic Manager probes</span></span>

* <span data-ttu-id="ee346-111">Диспетчер трафика считает toobe конечной точки сети только в том случае, если проверка hello получения ответа HTTP 200 обратно из пути проверки hello.</span><span class="sxs-lookup"><span data-stu-id="ee346-111">Traffic Manager considers an endpoint toobe ONLINE only when hello probe receives an HTTP 200 response back from hello probe path.</span></span> <span data-ttu-id="ee346-112">Любой другой ответ, отличный от указанного, свидетельствует об ошибке.</span><span class="sxs-lookup"><span data-stu-id="ee346-112">Any other non-200 response is a failure.</span></span>
* <span data-ttu-id="ee346-113">Перенаправление 30 x завершается ошибкой, даже если hello перенаправление URL-адрес возвращает 200.</span><span class="sxs-lookup"><span data-stu-id="ee346-113">A 30x redirect fails, even if hello redirected URL returns a 200.</span></span>
* <span data-ttu-id="ee346-114">При проверках HTTP ошибки сертификата пропускаются.</span><span class="sxs-lookup"><span data-stu-id="ee346-114">For HTTPs probes, certificate errors are ignored.</span></span>
* <span data-ttu-id="ee346-115">фактическое содержимое Hello hello проверки пути не имеет значения, при условии, что возвращается ответ 200.</span><span class="sxs-lookup"><span data-stu-id="ee346-115">hello actual content of hello probe path doesn't matter, as long as a 200 is returned.</span></span> <span data-ttu-id="ee346-116">Проверка URL-адрес toosome статического содержимого like «/ favicon.ico»-это стандартная техника.</span><span class="sxs-lookup"><span data-stu-id="ee346-116">Probing a URL toosome static content like "/favicon.ico" is a common technique.</span></span> <span data-ttu-id="ee346-117">Динамическое содержимое, например ASP-страницы приветствия, могут не всегда возвращать 200, даже в том случае, если приложение hello находится в работоспособном состоянии.</span><span class="sxs-lookup"><span data-stu-id="ee346-117">Dynamic content, like hello ASP pages, may not always return 200, even when hello application is healthy.</span></span>
* <span data-ttu-id="ee346-118">Лучший способ — hello tooset проверки toosomething путь, имеет достаточно toodetermine логику, hello сайта является вверх или вниз.</span><span class="sxs-lookup"><span data-stu-id="ee346-118">A best practice is tooset hello Probe path toosomething that has enough logic toodetermine that hello site is up or down.</span></span> <span data-ttu-id="ee346-119">В hello предыдущего примера, задав hello too"/favicon.ico путь», то только отвечает тестирование, w3wp.exe.</span><span class="sxs-lookup"><span data-stu-id="ee346-119">In hello previous example, by setting hello path too"/favicon.ico", you are only testing that w3wp.exe is responding.</span></span> <span data-ttu-id="ee346-120">Эта проверка может не показать, работоспособно ли веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="ee346-120">This probe may not indicate that your web application is healthy.</span></span> <span data-ttu-id="ee346-121">Лучшим вариантом будет tooset tooa путь такие как «/ Probe.aspx», содержащее логику toodetermine hello работоспособности сайта hello.</span><span class="sxs-lookup"><span data-stu-id="ee346-121">A better option would be tooset a path tooa something such as "/Probe.aspx" that has logic toodetermine hello health of hello site.</span></span> <span data-ttu-id="ee346-122">Например можно использовать использования tooCPU счетчики производительности или мер hello число неудачных запросов.</span><span class="sxs-lookup"><span data-stu-id="ee346-122">For example, you could use performance counters tooCPU utilization or measure hello number of failed requests.</span></span> <span data-ttu-id="ee346-123">Или можно случайно tooaccess ресурсы базы данных или работы веб-приложения hello toomake состояния сеанса.</span><span class="sxs-lookup"><span data-stu-id="ee346-123">Or you could attempt tooaccess database resources or session state toomake sure that hello web application is working.</span></span>
* <span data-ttu-id="ee346-124">Если снижение работоспособности всех конечных точек в профиле, затем диспетчер трафика считает все конечные точки Исправен и маршруты трафик tooall конечных точек.</span><span class="sxs-lookup"><span data-stu-id="ee346-124">If all endpoints in a profile are degraded, then Traffic Manager treats all endpoints as healthy and routes traffic tooall endpoints.</span></span> <span data-ttu-id="ee346-125">Такое поведение гарантирует, что неполадки проверки механизм hello не приводят к полном сбое службы.</span><span class="sxs-lookup"><span data-stu-id="ee346-125">This behavior ensures that problems with hello probing mechanism do not result in a complete outage of your service.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="ee346-126">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="ee346-126">Troubleshooting</span></span>

<span data-ttu-id="ee346-127">tootroubleshoot сбой проверки необходимо это средство, отображающее hello код состояния HTTP возвращаемого из hello проверки URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="ee346-127">tootroubleshoot a probe failure, you need a tool that shows hello HTTP status code return from hello probe URL.</span></span> <span data-ttu-id="ee346-128">Существует множество инструментов, Показать hello необработанные HTTP-ответа.</span><span class="sxs-lookup"><span data-stu-id="ee346-128">There are many tools available that show you hello raw HTTP response.</span></span>

* [<span data-ttu-id="ee346-129">Fiddler</span><span class="sxs-lookup"><span data-stu-id="ee346-129">Fiddler</span></span>](http://www.telerik.com/fiddler)
* [<span data-ttu-id="ee346-130">curl</span><span class="sxs-lookup"><span data-stu-id="ee346-130">curl</span></span>](https://curl.haxx.se/)
* <span data-ttu-id="ee346-131">[wget](http://gnuwin32.sourceforge.net/packages/wget.htm).</span><span class="sxs-lookup"><span data-stu-id="ee346-131">[wget](http://gnuwin32.sourceforge.net/packages/wget.htm)</span></span>

<span data-ttu-id="ee346-132">Кроме того можно используйте вкладку сети hello hello F12 средства отладки в Internet Explorer tooview hello HTTP-ответов.</span><span class="sxs-lookup"><span data-stu-id="ee346-132">Also, you can use hello Network tab of hello F12 Debugging Tools in Internet Explorer tooview hello HTTP responses.</span></span>

<span data-ttu-id="ee346-133">В этом примере мы хотим toosee hello ответа из наших проверки URL-адреса: http://watestsdp2008r2.cloudapp.net:80 или проверки.</span><span class="sxs-lookup"><span data-stu-id="ee346-133">For this example we want toosee hello response from our probe URL: http://watestsdp2008r2.cloudapp.net:80/Probe.</span></span> <span data-ttu-id="ee346-134">Следующий пример PowerShell Hello показана проблема hello.</span><span class="sxs-lookup"><span data-stu-id="ee346-134">hello following PowerShell example illustrates hello problem.</span></span>

```powershell
Invoke-WebRequest 'http://watestsdp2008r2.cloudapp.net/Probe' -MaximumRedirection 0 -ErrorAction SilentlyContinue | Select-Object StatusCode,StatusDescription
```

<span data-ttu-id="ee346-135">Выходные данные примера:</span><span class="sxs-lookup"><span data-stu-id="ee346-135">Example output:</span></span>

    StatusCode StatusDescription
    ---------- -----------------
           301 Moved Permanently

<span data-ttu-id="ee346-136">Обратите внимание, что получен ответ перенаправления.</span><span class="sxs-lookup"><span data-stu-id="ee346-136">Notice that we received a redirect response.</span></span> <span data-ttu-id="ee346-137">Как упоминалось ранее, любое состояние кода, отличное от 200, свидетельствует о сбое.</span><span class="sxs-lookup"><span data-stu-id="ee346-137">As stated previously, any StatusCode other than 200 is considered a failure.</span></span> <span data-ttu-id="ee346-138">Изменения диспетчера трафика hello tooOffline состояние конечной точки.</span><span class="sxs-lookup"><span data-stu-id="ee346-138">Traffic Manager changes hello endpoint status tooOffline.</span></span> <span data-ttu-id="ee346-139">tooresolve hello проблему, проверьте веб-сайт hello конфигурации tooensure, hello правильную StatusCode могут быть возвращены из hello проверки пути.</span><span class="sxs-lookup"><span data-stu-id="ee346-139">tooresolve hello problem, check hello website configuration tooensure that hello proper StatusCode can be returned from hello probe path.</span></span> <span data-ttu-id="ee346-140">Перенастройте hello диспетчера трафика проверки toopoint tooa путь, который возвращает ответ 200.</span><span class="sxs-lookup"><span data-stu-id="ee346-140">Reconfigure hello Traffic Manager probe toopoint tooa path that returns a 200.</span></span>

<span data-ttu-id="ee346-141">Если ваш пробы используется hello протокола HTTPS, может потребоваться сертификат toodisable проверку ошибок SSL/TLS tooavoid во время тестирования.</span><span class="sxs-lookup"><span data-stu-id="ee346-141">If your probe is using hello HTTPS protocol, you may need toodisable certificate checking tooavoid SSL/TLS errors during your test.</span></span> <span data-ttu-id="ee346-142">Hello следующие инструкции PowerShell отключить проверку сертификата для hello текущий сеанс PowerShell:</span><span class="sxs-lookup"><span data-stu-id="ee346-142">hello following PowerShell statements disable certificate validation for hello current PowerShell session:</span></span>

```powershell
add-type @"
using System.Net;
using System.Security.Cryptography.X509Certificates;
public class TrustAllCertsPolicy : ICertificatePolicy {
    public bool CheckValidationResult(
    ServicePoint srvPoint, X509Certificate certificate,
    WebRequest request, int certificateProblem) {
    return true;
    }
}
"@
[System.Net.ServicePointManager]::CertificatePolicy = New-Object TrustAllCertsPolicy
```

## <a name="next-steps"></a><span data-ttu-id="ee346-143">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ee346-143">Next Steps</span></span>

[<span data-ttu-id="ee346-144">О методах маршрутизации трафика в диспетчере трафика</span><span class="sxs-lookup"><span data-stu-id="ee346-144">About Traffic Manager traffic routing methods</span></span>](traffic-manager-routing-methods.md)

[<span data-ttu-id="ee346-145">Что такое диспетчер трафика</span><span class="sxs-lookup"><span data-stu-id="ee346-145">What is Traffic Manager</span></span>](traffic-manager-overview.md)

[<span data-ttu-id="ee346-146">Облачные службы</span><span class="sxs-lookup"><span data-stu-id="ee346-146">Cloud Services</span></span>](http://go.microsoft.com/fwlink/?LinkId=314074)

[<span data-ttu-id="ee346-147">Веб-приложения Azure</span><span class="sxs-lookup"><span data-stu-id="ee346-147">Azure Web Apps</span></span>](https://azure.microsoft.com/documentation/services/app-service/web/)

[<span data-ttu-id="ee346-148">Операции с диспетчером трафика (справочник по REST API)</span><span class="sxs-lookup"><span data-stu-id="ee346-148">Operations on Traffic Manager (REST API Reference)</span></span>](http://go.microsoft.com/fwlink/?LinkId=313584)

<span data-ttu-id="ee346-149">[Командлеты для диспетчера трафика Azure][1]</span><span class="sxs-lookup"><span data-stu-id="ee346-149">[Azure Traffic Manager Cmdlets][1]</span></span>

[1]: https://msdn.microsoft.com/library/mt125941(v=azure.200).aspx
