---
title: "Устранение неполадок с состоянием \"Деградация\" в диспетчере трафика Azure"
description: "Устранение неполадок с профилями диспетчера трафика при отображении состояния \"Деградация\"."
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
ms.openlocfilehash: b1d00fb84695d2289f37647f55a7c56cf28c8c96
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-degraded-state-on-azure-traffic-manager"></a><span data-ttu-id="65265-103">Устранение неполадок, связанных со сбоем диспетчера трафика</span><span class="sxs-lookup"><span data-stu-id="65265-103">Troubleshooting degraded state on Azure Traffic Manager</span></span>

<span data-ttu-id="65265-104">В этой статье описывается устранение неполадок в профиле диспетчера трафика Azure, который находится в состоянии пониженной функциональности.</span><span class="sxs-lookup"><span data-stu-id="65265-104">This article describes how to troubleshoot an Azure Traffic Manager profile that is showing a degraded status.</span></span> <span data-ttu-id="65265-105">Для этого сценария предположим, что вы настроили профиль диспетчера трафика, указывающего на некоторые из размещенных служб .cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="65265-105">For this scenario, consider that you have configured a Traffic Manager profile pointing to some of your cloudapp.net hosted services.</span></span> <span data-ttu-id="65265-106">Если в диспетчере трафика отображается состояние **Деградация**, одна или несколько конечных точек также могут иметь состояние **Деградация**.</span><span class="sxs-lookup"><span data-stu-id="65265-106">If the health of your Traffic Manager displays a **Degraded** status, then the status of one or more endpoints may be **Degraded**:</span></span>

![состояние "Деградация" конечной точки](./media/traffic-manager-troubleshooting-degraded/traffic-manager-degradedifonedegraded.png)

<span data-ttu-id="65265-108">Если в диспетчере трафика отображается состояние **Неактивно**, обе конечные точки могут находиться в режиме **Отключено**.</span><span class="sxs-lookup"><span data-stu-id="65265-108">If the health of your Traffic Manager displays an **Inactive** status, then both end points may be **Disabled**:</span></span>

![состояние "Неактивно" диспетчера трафика](./media/traffic-manager-troubleshooting-degraded/traffic-manager-inactive.png)

## <a name="understanding-traffic-manager-probes"></a><span data-ttu-id="65265-110">Общие сведения о проверках диспетчера трафика</span><span class="sxs-lookup"><span data-stu-id="65265-110">Understanding Traffic Manager probes</span></span>

* <span data-ttu-id="65265-111">Диспетчер трафика считает, что конечная точка работает В СЕТИ, только если из пути проверки получен ответ HTTP 200.</span><span class="sxs-lookup"><span data-stu-id="65265-111">Traffic Manager considers an endpoint to be ONLINE only when the probe receives an HTTP 200 response back from the probe path.</span></span> <span data-ttu-id="65265-112">Любой другой ответ, отличный от указанного, свидетельствует об ошибке.</span><span class="sxs-lookup"><span data-stu-id="65265-112">Any other non-200 response is a failure.</span></span>
* <span data-ttu-id="65265-113">Перенаправление 30x завершается ошибкой, даже если URL-адрес перенаправления вернет ответ 200.</span><span class="sxs-lookup"><span data-stu-id="65265-113">A 30x redirect fails, even if the redirected URL returns a 200.</span></span>
* <span data-ttu-id="65265-114">При проверках HTTP ошибки сертификата пропускаются.</span><span class="sxs-lookup"><span data-stu-id="65265-114">For HTTPs probes, certificate errors are ignored.</span></span>
* <span data-ttu-id="65265-115">Фактическое содержимое пути проверки не имеет значения, если возвращается ответ 200.</span><span class="sxs-lookup"><span data-stu-id="65265-115">The actual content of the probe path doesn't matter, as long as a 200 is returned.</span></span> <span data-ttu-id="65265-116">Как правило, URL-адрес проверяется на наличие статического содержимого, например /favicon.ico.</span><span class="sxs-lookup"><span data-stu-id="65265-116">Probing a URL to some static content like "/favicon.ico" is a common technique.</span></span> <span data-ttu-id="65265-117">Динамическое содержимое, например страницы поставщика услуг по предоставлению приложений в аренду (ASP), может не всегда возвращать ответ 200, даже если приложение работоспособно.</span><span class="sxs-lookup"><span data-stu-id="65265-117">Dynamic content, like the ASP pages, may not always return 200, even when the application is healthy.</span></span>
* <span data-ttu-id="65265-118">Мы рекомендуем указать путь проверки, содержащий достаточную логику, чтобы определить, работает сайт или нет.</span><span class="sxs-lookup"><span data-stu-id="65265-118">A best practice is to set the Probe path to something that has enough logic to determine that the site is up or down.</span></span> <span data-ttu-id="65265-119">В предыдущем примере, указав путь к /favicon.ico, вы проверяли, отвечает ли w3wp.exe.</span><span class="sxs-lookup"><span data-stu-id="65265-119">In the previous example, by setting the path to "/favicon.ico", you are only testing that w3wp.exe is responding.</span></span> <span data-ttu-id="65265-120">Эта проверка может не показать, работоспособно ли веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="65265-120">This probe may not indicate that your web application is healthy.</span></span> <span data-ttu-id="65265-121">Лучше было бы задать путь к элементу, например /Probe.aspx, содержащему логику для определения работоспособности сайта.</span><span class="sxs-lookup"><span data-stu-id="65265-121">A better option would be to set a path to a something such as "/Probe.aspx" that has logic to determine the health of the site.</span></span> <span data-ttu-id="65265-122">Например, можно использовать счетчики производительности для определения загрузки ЦП или определить число неудачных запросов.</span><span class="sxs-lookup"><span data-stu-id="65265-122">For example, you could use performance counters to CPU utilization or measure the number of failed requests.</span></span> <span data-ttu-id="65265-123">Кроме того, можно попытаться получить доступ к ресурсам базы данных или состоянию сеанса, чтобы убедиться, что веб-приложение работает.</span><span class="sxs-lookup"><span data-stu-id="65265-123">Or you could attempt to access database resources or session state to make sure that the web application is working.</span></span>
* <span data-ttu-id="65265-124">Если функциональность всех конечных точек в профиле снижена, то диспетчер трафика будет считать их работоспособными и будет перенаправлять трафик во все конечные точки.</span><span class="sxs-lookup"><span data-stu-id="65265-124">If all endpoints in a profile are degraded, then Traffic Manager treats all endpoints as healthy and routes traffic to all endpoints.</span></span> <span data-ttu-id="65265-125">Такое поведение гарантирует, что проблемы с механизмом проверки не приведут к сбою службы.</span><span class="sxs-lookup"><span data-stu-id="65265-125">This behavior ensures that problems with the probing mechanism do not result in a complete outage of your service.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="65265-126">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="65265-126">Troubleshooting</span></span>

<span data-ttu-id="65265-127">Чтобы устранить сбой проверки, необходимо средство, позволяющее просмотреть код состояния HTTP, возвращаемый после проверки URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="65265-127">To troubleshoot a probe failure, you need a tool that shows the HTTP status code return from the probe URL.</span></span> <span data-ttu-id="65265-128">Существует множество средств, позволяющих просмотреть необработанный ответ HTTP:</span><span class="sxs-lookup"><span data-stu-id="65265-128">There are many tools available that show you the raw HTTP response.</span></span>

* [<span data-ttu-id="65265-129">Fiddler</span><span class="sxs-lookup"><span data-stu-id="65265-129">Fiddler</span></span>](http://www.telerik.com/fiddler)
* [<span data-ttu-id="65265-130">curl</span><span class="sxs-lookup"><span data-stu-id="65265-130">curl</span></span>](https://curl.haxx.se/)
* <span data-ttu-id="65265-131">[wget](http://gnuwin32.sourceforge.net/packages/wget.htm).</span><span class="sxs-lookup"><span data-stu-id="65265-131">[wget](http://gnuwin32.sourceforge.net/packages/wget.htm)</span></span>

<span data-ttu-id="65265-132">Кроме того, для просмотра ответа HTTP можно воспользоваться вкладкой "Сеть" средств отладки F12 в Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="65265-132">Also, you can use the Network tab of the F12 Debugging Tools in Internet Explorer to view the HTTP responses.</span></span>

<span data-ttu-id="65265-133">В этом примере нам нужно вывести ответ, полученный после проверки URL-адреса http://watestsdp2008r2.cloudapp.net:80.</span><span class="sxs-lookup"><span data-stu-id="65265-133">For this example we want to see the response from our probe URL: http://watestsdp2008r2.cloudapp.net:80/Probe.</span></span> <span data-ttu-id="65265-134">Проблема продемонстрирована в приведенном ниже примере PowerShell.</span><span class="sxs-lookup"><span data-stu-id="65265-134">The following PowerShell example illustrates the problem.</span></span>

```powershell
Invoke-WebRequest 'http://watestsdp2008r2.cloudapp.net/Probe' -MaximumRedirection 0 -ErrorAction SilentlyContinue | Select-Object StatusCode,StatusDescription
```

<span data-ttu-id="65265-135">Выходные данные примера:</span><span class="sxs-lookup"><span data-stu-id="65265-135">Example output:</span></span>

    StatusCode StatusDescription
    ---------- -----------------
           301 Moved Permanently

<span data-ttu-id="65265-136">Обратите внимание, что получен ответ перенаправления.</span><span class="sxs-lookup"><span data-stu-id="65265-136">Notice that we received a redirect response.</span></span> <span data-ttu-id="65265-137">Как упоминалось ранее, любое состояние кода, отличное от 200, свидетельствует о сбое.</span><span class="sxs-lookup"><span data-stu-id="65265-137">As stated previously, any StatusCode other than 200 is considered a failure.</span></span> <span data-ttu-id="65265-138">Диспетчер трафика изменяет состояние конечной точки на Offline (Не в сети).</span><span class="sxs-lookup"><span data-stu-id="65265-138">Traffic Manager changes the endpoint status to Offline.</span></span> <span data-ttu-id="65265-139">Для решения проблемы проверьте конфигурацию веб-сайта, чтобы обеспечить возврат соответствующего кода состояния из пути проверки.</span><span class="sxs-lookup"><span data-stu-id="65265-139">To resolve the problem, check the website configuration to ensure that the proper StatusCode can be returned from the probe path.</span></span> <span data-ttu-id="65265-140">Перенастройте проверку диспетчера трафика таким образом, чтобы она указывала на путь, возвращающий ответ 200.</span><span class="sxs-lookup"><span data-stu-id="65265-140">Reconfigure the Traffic Manager probe to point to a path that returns a 200.</span></span>

<span data-ttu-id="65265-141">Если при проверке используется протокол HTTPS, может потребоваться отключить проверку сертификата во избежание ошибок SSL/TLS.</span><span class="sxs-lookup"><span data-stu-id="65265-141">If your probe is using the HTTPS protocol, you may need to disable certificate checking to avoid SSL/TLS errors during your test.</span></span> <span data-ttu-id="65265-142">Следующая инструкция PowerShell отключает проверку сертификата в текущем сеансе PowerShell:</span><span class="sxs-lookup"><span data-stu-id="65265-142">The following PowerShell statements disable certificate validation for the current PowerShell session:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="65265-143">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="65265-143">Next Steps</span></span>

[<span data-ttu-id="65265-144">О методах маршрутизации трафика в диспетчере трафика</span><span class="sxs-lookup"><span data-stu-id="65265-144">About Traffic Manager traffic routing methods</span></span>](traffic-manager-routing-methods.md)

[<span data-ttu-id="65265-145">Что такое диспетчер трафика</span><span class="sxs-lookup"><span data-stu-id="65265-145">What is Traffic Manager</span></span>](traffic-manager-overview.md)

[<span data-ttu-id="65265-146">Облачные службы</span><span class="sxs-lookup"><span data-stu-id="65265-146">Cloud Services</span></span>](http://go.microsoft.com/fwlink/?LinkId=314074)

[<span data-ttu-id="65265-147">Веб-приложения Azure</span><span class="sxs-lookup"><span data-stu-id="65265-147">Azure Web Apps</span></span>](https://azure.microsoft.com/documentation/services/app-service/web/)

[<span data-ttu-id="65265-148">Операции с диспетчером трафика (справочник по REST API)</span><span class="sxs-lookup"><span data-stu-id="65265-148">Operations on Traffic Manager (REST API Reference)</span></span>](http://go.microsoft.com/fwlink/?LinkId=313584)

<span data-ttu-id="65265-149">[Командлеты для диспетчера трафика Azure][1]</span><span class="sxs-lookup"><span data-stu-id="65265-149">[Azure Traffic Manager Cmdlets][1]</span></span>

[1]: https://msdn.microsoft.com/library/mt125941(v=azure.200).aspx
