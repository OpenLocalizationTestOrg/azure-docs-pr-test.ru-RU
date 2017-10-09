---
title: "aaaMicrosoft использования Azure и Cloudyn включить API-интерфейсы RateCard tooProvide ITFM для клиентов | Документы Microsoft"
description: "Предоставляет уникальный взгляд из Microsoft Azure Billing партнер Cloudyn, опытом интеграции hello API-интерфейсов выставления счетов Azure в своих продуктах.  Эти сведения особенно полезны для клиентов Azure и Cloudyn, которые хотели бы использовать Cloudyn для служб Azure или уже рассматривают такой вариант."
services: 
documentationcenter: 
author: BryanLa
manager: tonguyen
editor: 
tags: billing
ms.assetid: f1397397-7e92-4c20-9862-ab6b93afefb7
ms.service: billing
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: billing
ms.date: 02/03/2017
ms.author: mobandyo;bryanla
ms.openlocfilehash: e221ac8b8feebb725a1cc669c8143ab829621a8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-azure-usage-and-ratecard-apis-enable-cloudyn-tooprovide-itfm-for-customers"></a>Использование Microsoft Azure и Cloudyn включить API-интерфейсы RateCard tooProvide ITFM для клиентов
Cloudyn, разработки партнера Майкрософт и ведущим поставщиком облачных вариантах управления, был выбран для личной ознакомительной учетной записи новый hello использование ресурсов Microsoft Azure и API-интерфейсы RateCard.  Hello API использования предоставляет доступ к данным Azure потребления tooestimated для подписки. Hello RateCard API предоставляет полные сведения о ценах всех служб Azure, для клиентов, не являющихся - соглашение предприятия. Вместе эти API обеспечивают полноценную платформу для ввода данных в ИТ-средства финансового управления (IT Financial Management — ITFM), такие как Cloudyn.

## <a name="introduction"></a>Введение
Здравствуйте, так называемые «умножение» данных из hello API использования с данными из hello RateCard API (цена за использование [единицы] [$unit] = подробные сведения об использовании и стоимость) создает hello наиболее детальным, точной и надежной выставления счетов данных, доступных для Azure сегодня.

![Обзор ITFM][1]

Использует эти API предоставляет основные сведения об использовании клиентов и затрат, учетным записям пользователей tooanalyze Cloudyn в простой, программным способом, а tooperform различные задачи ITFM для своих клиентов.

## <a name="integrating-cloudyn-with-hello-ratecard-and-usage-apis"></a>Интеграция Cloudyn с hello RateCard и использования API-интерфейсы
Hello RateCard API требуется несколько входных параметров — как сведения о регионе, валюты и языковой стандарт — но hello наиболее важных она OfferDurableID, который определяет тип hello Azure предложения hello клиента использует (по мере использования, устаревших 6 до 12-месячном обязательств планы, предлагает MSDN, MPN предложений, рекламных предложений и другие). Hello OfferDurableID можно найти в hello [использования Azure и портале выставления счетов](https://account.windowsazure.com/Subscriptions), в разделе hello «Предоставляют идентификатор» hello указанной подписки.

После регистрации для [Cloudyn для Azure](https://www.cloudyn.com/microsoft-azure/) служб, пользователь может добавить их OfferDurableID код, который позволяет Cloudyn toopull их hello RateCard API ценообразования сведения.  Сведения о различных типах hello предложений можно найти одну hello [сведения о Microsoft Azure предлагают](https://azure.microsoft.com/support/legal/offer-details/) страницы.

![Обзор подсистемы ITFM Cloudyn][2]

Cloudyn использует оба hello в toohello сложения производительности API Azure, дополнительные слои toocreate визуализации, аналитика, предупреждения, использование и API-интерфейсы RateCard, отчетов, стоимость управления и практические рекомендации, предоставляя клиентам Azure является надежным Средство ITFM облака.

## <a name="cloudyn-itfm-use-cases-enabled-by-usage-and-ratecard-api-integration"></a>Варианты использования ITFM Cloudyn, возможные благодаря интеграции API использования и RateCard
К наиболее распространенным вариантам использования ITFM Cloudyn, возможным благодаря интеграции API использования и RateCard, относятся следующие:

* **Анализ затрат** -позволяет облака обходится toobe разбивкой tooany собственного определения измерения (поставщик, service, учетная запись, региона и т. д.). Hello использования Azure и API-интерфейсы RateCard сделать эту сложной задачей, предоставляя hello самом детальном распределение данных об использовании и затрат на учетную запись, которой затем группируются и отфильтрованных по Cloudyn и представленных пользователя toohello в графических или табличной форме.

![Круговая диаграмма анализа затрат][3]

* **Стоимость распределения 360** -включает Финансы и hello toouncover ИТ диспетчеры фактических затрат декомпозиции, драйверов и тенденции их развертывания в облаке. Дополнительно предоставит менеджерам tooeasily расходы связан развертывания филиалов, отделов, областей и многое другое, предоставляя беспрецедентную аналитические данные в облако затраты и упрощение enterprise платежей и showbacks. Hello использования Azure и API-интерфейсы RateCard служат в качестве входного tooCloudyn стоимость распределения механизм, который дополняет hello API-интерфейсов определив методы и бизнес-логики при выделении ресурсов без тегов или untaggable.

![Диаграмма комплексного распределения затрат][4]

* **Экономичное изменения размера** -рекомендации определении размеров для недостаточно виртуальных машин, что уменьшает расходы hello клиента на компьютерах слишком большого размера или избыточной. Это осуществляется путем оценки метрик ЦП и ОЗУ виртуальной машины (посредством API производительности), времени работы (посредством API использования) и стоимости (посредством API RateCard). Cloudyn затем определении размеров рекомендации на основе недостаточно ресурсов ЦП и ОЗУ (производительность) и вычисляет Ожидаемая экономия умножением дельта цены hello (RateCard) между виртуальными машинами hello неэффективные hello фактическое время-(использования) из hello компьютер, недостаточно.

![Выбор размера с учетом рентабельности][5]

* **Cloud Porting Recommendations** (Рекомендации по переносу в облако) — советы финансового характера по переносу в облако. Он анализирует текущие затраты пользователя облачных ресурсов, которые будут развернуты на основными облачными поставщиками и сравнивает ее стоимость toohello эквивалентные развертывания в Azure. Затем она создает детальный каждого ресурса, финансовые основе перенос tooAzure рекомендации. После оценки развертывания эквивалентные hello, необходимые в Azure (с учетом производительности метрик и персональные настройки пользователя), Cloudyn использует RateCard API hello tooevaluate стоимость hello hello эквивалентные развертывания в Azure.
* **Отчеты о производительности** -включаемые производительности Azure API, эти отчеты содержат массив функций из данных об использовании ЦП и ОЗУ toooptimization рекомендации. Ниже приведен пример отчета об использовании экземпляра, где представлена декомпозиция экземпляра по средней загрузке ЦП.

![Performance Reports][6]

* **Менеджер категории** — это мощная функция, в Cloudyn, который позволяет упорядочить toounorganized облачных ресурсов. Он предоставляет toocreate свободу пользователям hello свои уникальные категории (теги) для эффективной измерение и отчетов, который имеет в соответствии с бизнес-процессов. Кроме того, пользователи могут легко контролировать и классифицировать несогласованные теги (т. е. опечатки и другие отклонения) и автоматически обнаруживать непомеченные ресурсы для определения точной стоимости.

![Диспетчер категорий][7]

## <a name="video"></a>Видео
Вот короткое видео, в котором показано, как Azure клиента можно использовать Cloudyn для Azure и hello Azure API выставления счетов, toogain аналитики из данных их использование Azure.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Cloudyn-Provides-Cloud-ITFM-Tools-Via-Microsoft-Azure-APIs/player]
> 
> 

## <a name="next-steps"></a>Дальнейшие действия
* Запустите бесплатную [Cloudyn для Azure](https://www.cloudyn.com/microsoft-azure/) toosee пробной версии, как можно получить стоимости прозрачности с создания пользовательских отчетов и аналитики для развертывания облака Microsoft Azure.
* В разделе [анализировать потребления ресурсов Microsoft Azure](billing-usage-rate-card-overview.md) Обзор hello использование ресурсов Azure и API-интерфейсов RateCard.
* Извлечение hello [выставления счетов Справочник API REST Azure](https://msdn.microsoft.com/library/azure/1ea5b323-54bb-423d-916f-190de96c6a3c) Дополнительные сведения о двух интерфейсов API, являющиеся частью hello набор API, предоставляемые hello диспетчера ресурсов Azure.
* Если вы хотите toodive прямо в образце кода hello, извлеките наших примеров Microsoft Azure Billing API код на [образцы кода Azure](https://azure.microsoft.com/documentation/samples/?term=billing).

## <a name="learn-more"></a>Подробнее
* toolearn Дополнительные сведения о предложениях службы Microsoft Azure Enterprise Agreement (EA), перейдите на страницу [лицензирования Azure для hello предприятия](https://azure.microsoft.com/pricing/enterprise-agreement/)
* В разделе hello [Обзор диспетчера ресурсов Azure](../azure-resource-manager/resource-group-overview.md) toolearn статьи о hello диспетчера ресурсов Azure.
* Дополнительные сведения о hello набор инструментов, тратить необходимые toohelp в способствуют пониманию облака, можно найти слишком статьи [рынка руководство для средств управления финансовых ИТ (ITFM)](http://www.gartner.com/technology/reprints.do?id=1-212F7AL&ct=140909&st=sb).

<!--Image references-->
[1]: ./media/billing-usage-rate-card-partner-solution-cloudyn/Cloudyn-ITFM-Overview.png
[2]: ./media/billing-usage-rate-card-partner-solution-cloudyn/Cloudyn-ITFM-Engine-Overview.png
[3]: ./media/billing-usage-rate-card-partner-solution-cloudyn/Cloudyn-Cost-Analysis-Pie-Chart.png
[4]: ./media/billing-usage-rate-card-partner-solution-cloudyn/Cloudyn-Cost-Allocation-360-Chart.png
[5]: ./media/billing-usage-rate-card-partner-solution-cloudyn/Cloudyn-Cost-Effective-Sizing.png
[6]: ./media/billing-usage-rate-card-partner-solution-cloudyn/Cloudyn-Performance-Reports.png
[7]: ./media/billing-usage-rate-card-partner-solution-cloudyn/Cloudyn-Category-Manager.png
