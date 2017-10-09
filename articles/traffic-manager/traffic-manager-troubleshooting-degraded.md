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
# <a name="troubleshooting-degraded-state-on-azure-traffic-manager"></a>Устранение неполадок, связанных со сбоем диспетчера трафика

В этой статье описывается, как tootroubleshoot профиль диспетчера трафика Azure показан ограниченной состояния. В этом случае рассмотрите возможность настройки профиля диспетчера трафика, указывающий toosome cloudapp.net размещенных служб. Если отображает hello работоспособности из диспетчера трафика **Деградация** состояние, а затем hello состояние одного или нескольких конечных точек может быть **Деградация**:

![состояние "Деградация" конечной точки](./media/traffic-manager-troubleshooting-degraded/traffic-manager-degradedifonedegraded.png)

Если отображает hello работоспособности из диспетчера трафика **неактивно** состояние, а затем обе конечные точки могут быть **отключено**:

![состояние "Неактивно" диспетчера трафика](./media/traffic-manager-troubleshooting-degraded/traffic-manager-inactive.png)

## <a name="understanding-traffic-manager-probes"></a>Общие сведения о проверках диспетчера трафика

* Диспетчер трафика считает toobe конечной точки сети только в том случае, если проверка hello получения ответа HTTP 200 обратно из пути проверки hello. Любой другой ответ, отличный от указанного, свидетельствует об ошибке.
* Перенаправление 30 x завершается ошибкой, даже если hello перенаправление URL-адрес возвращает 200.
* При проверках HTTP ошибки сертификата пропускаются.
* фактическое содержимое Hello hello проверки пути не имеет значения, при условии, что возвращается ответ 200. Проверка URL-адрес toosome статического содержимого like «/ favicon.ico»-это стандартная техника. Динамическое содержимое, например ASP-страницы приветствия, могут не всегда возвращать 200, даже в том случае, если приложение hello находится в работоспособном состоянии.
* Лучший способ — hello tooset проверки toosomething путь, имеет достаточно toodetermine логику, hello сайта является вверх или вниз. В hello предыдущего примера, задав hello too"/favicon.ico путь», то только отвечает тестирование, w3wp.exe. Эта проверка может не показать, работоспособно ли веб-приложение. Лучшим вариантом будет tooset tooa путь такие как «/ Probe.aspx», содержащее логику toodetermine hello работоспособности сайта hello. Например можно использовать использования tooCPU счетчики производительности или мер hello число неудачных запросов. Или можно случайно tooaccess ресурсы базы данных или работы веб-приложения hello toomake состояния сеанса.
* Если снижение работоспособности всех конечных точек в профиле, затем диспетчер трафика считает все конечные точки Исправен и маршруты трафик tooall конечных точек. Такое поведение гарантирует, что неполадки проверки механизм hello не приводят к полном сбое службы.

## <a name="troubleshooting"></a>Устранение неполадок

tootroubleshoot сбой проверки необходимо это средство, отображающее hello код состояния HTTP возвращаемого из hello проверки URL-адреса. Существует множество инструментов, Показать hello необработанные HTTP-ответа.

* [Fiddler](http://www.telerik.com/fiddler)
* [curl](https://curl.haxx.se/)
* [wget](http://gnuwin32.sourceforge.net/packages/wget.htm).

Кроме того можно используйте вкладку сети hello hello F12 средства отладки в Internet Explorer tooview hello HTTP-ответов.

В этом примере мы хотим toosee hello ответа из наших проверки URL-адреса: http://watestsdp2008r2.cloudapp.net:80 или проверки. Следующий пример PowerShell Hello показана проблема hello.

```powershell
Invoke-WebRequest 'http://watestsdp2008r2.cloudapp.net/Probe' -MaximumRedirection 0 -ErrorAction SilentlyContinue | Select-Object StatusCode,StatusDescription
```

Выходные данные примера:

    StatusCode StatusDescription
    ---------- -----------------
           301 Moved Permanently

Обратите внимание, что получен ответ перенаправления. Как упоминалось ранее, любое состояние кода, отличное от 200, свидетельствует о сбое. Изменения диспетчера трафика hello tooOffline состояние конечной точки. tooresolve hello проблему, проверьте веб-сайт hello конфигурации tooensure, hello правильную StatusCode могут быть возвращены из hello проверки пути. Перенастройте hello диспетчера трафика проверки toopoint tooa путь, который возвращает ответ 200.

Если ваш пробы используется hello протокола HTTPS, может потребоваться сертификат toodisable проверку ошибок SSL/TLS tooavoid во время тестирования. Hello следующие инструкции PowerShell отключить проверку сертификата для hello текущий сеанс PowerShell:

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

## <a name="next-steps"></a>Дальнейшие действия

[О методах маршрутизации трафика в диспетчере трафика](traffic-manager-routing-methods.md)

[Что такое диспетчер трафика](traffic-manager-overview.md)

[Облачные службы](http://go.microsoft.com/fwlink/?LinkId=314074)

[Веб-приложения Azure](https://azure.microsoft.com/documentation/services/app-service/web/)

[Операции с диспетчером трафика (справочник по REST API)](http://go.microsoft.com/fwlink/?LinkId=313584)

[Командлеты для диспетчера трафика Azure][1]

[1]: https://msdn.microsoft.com/library/mt125941(v=azure.200).aspx
