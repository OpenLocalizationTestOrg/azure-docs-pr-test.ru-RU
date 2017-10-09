---
title: "aaaCloud Cruiser и выставление счетов интеграции API Microsoft Azure | Документы Microsoft"
description: "Предоставляет уникальный взгляд из Microsoft Azure Billing партнер Cruiser облака опытом интеграции hello API-интерфейсов выставления счетов Azure в своих продуктах.  Эти сведения особенно полезны для клиентов Azure и Cloud Cruiser, которые хотели бы использовать Cloud Cruiser для Microsoft Azure Pack или уже рассматривают такой вариант."
services: 
documentationcenter: 
author: BryanLa
manager: tonguyen
editor: 
tags: billing
ms.assetid: b65128cf-5d4d-4cbd-b81e-d3dceab44271
ms.service: billing
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: billing
ms.date: 02/03/2017
ms.author: mobandyo;sirishap;bryanla
ms.openlocfilehash: 74cc19bdeed26c6684210736caa0cb365e8f8821
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="cloud-cruiser-and-microsoft-azure-billing-api-integration"></a>Интеграция Cloud Cruiser и API выставления счетов Microsoft Azure
В этой статье описывается, как стоимость hello сведения, собранные из hello новый выставления счетов интерфейсов API Microsoft Azure, которая может использоваться в облаке Cruiser для рабочего процесса, моделирования и анализа.

## <a name="azure-ratecard-api"></a>API RateCard Azure
Hello RateCard API предоставляет данные о курсе из Azure. После проверки подлинности с правильными учетными данными hello, может запросить hello API toocollect метаданные о службах hello, доступный в Azure, вместе с hello ставки, связанный с вашей предлагают ID.

Hello ниже приведен пример ответа от API hello, показывающая hello цены для hello A0 (Windows) экземпляр:

    {
        "MeterId": "0e59ad56-03e5-4c3d-90d4-6670874d7e29",
        "MeterName": "Compute Hours",
        "MeterCategory": "Virtual Machines",
        "MeterSubCategory": "A0 VM (Windows)",
        "Unit": "Hours",
        "MeterRates":
        {
            "0": 0.029
        },
        "EffectiveDate": "2014-08-01T00:00:00Z",
        "IncludedQuantity": 0.0,
        "MeterStatus": "Active"
    },

### <a name="cloud-cruisers-interface-tooazure-ratecard-api"></a>Cloud Cruiser элемента интерфейса tooAzure RateCard API
Cruiser облаке могут использовать сведения об RateCard API hello различными способами. В этой статье мы рассмотрим, как его можно использовать toomake IaaS рабочей нагрузки стоимость моделирование и анализа.

toodemonstrate это вариант использования, представьте себе рабочей нагрузки нескольких экземпляров, работающих на Microsoft Azure Pack (MAP). Цель Hello является toosimulate этой же рабочей нагрузки в Azure, а также оценить затраты hello выполнения такой миграции. Чтобы toocreate имитации, существует два toobe основные задачи выполнены:

1. **Процесс импорта и hello службы данных, собираемых из hello RateCard API.** Эта задача также выполняется на книгах hello, где hello извлечение из hello RateCard API — новый план скорость tooa преобразованный и опубликована. Нового плана скорость будет использоваться на tooestimate имитаций hello hello Azure цены.
2. **Нормализация служб WAP и служб Azure для IaaS.** По умолчанию службы WAP основаны на отдельных ресурсах (ЦП, объем памяти, размер диска и т. д.), а службы Azure основаны на размере экземпляра (A0, A1, A2 и т. д.). Первой задаче можно выполняемых ядром ETL Cruiser облака, вызывается книг, где может поставляться эти ресурсы вместе с размером экземпляра, аналогичный tooAzure экземпляр служб.

### <a name="import-data-from-hello-ratecard-api"></a>Импорт данных из hello RateCard API
Книги Cruiser облака с информацией автоматической toocollect и процесс из hello RateCard API.  Книги ETL (извлечение — преобразование — загрузка) позволяют tooconfigure hello коллекции, преобразования и публикации данных в базу данных облака Cruiser hello.

Каждую книгу можно иметь одну или несколько коллекций, позволяя toocorrelate информацию из разных источников toocomplement или дополнять данные об использовании hello. следующие два снимки экрана Показать как Hello toocreate новый *коллекции* в существующей рабочей книге, а также сведения об импорте hello *коллекции* из hello RateCard API:

![Рис. 1. Создание коллекции][1]

![Рис. 2 - Импорт данных из новой коллекции hello][2]

После импорта данных hello в книге hello, — возможно toocreate несколько шагов и процессов преобразования, toomodify и модели hello данных. Для этого примера поскольку нас интересуют только инфраструктуры как услуга (IaaS), мы используем hello преобразования действия tooremove ненужные строки или записи, связанные с tooservices Кроме IaaS.

Hello следующем снимке экрана показаны шаги преобразования hello используемых tooprocess hello данные, полученные от RateCard API:

![Рисунок 3. преобразование шаги tooprocess сбора данных из RateCard API][3]

### <a name="defining-new-services-and-rate-plans"></a>Определение новых служб и тарифных планов
Существуют различные способы toodefine службы на Cruiser облака. Один из способов hello является tooimport hello служб на основе данных об использовании hello. Этот метод часто используется при работе с общедоступных облаков, где уже определены hello служб поставщиком hello.

Тарифного плана — это набор курсов или цен, которые могут быть применен toodifferent службы, на основе даты вступления в силу или всех клиентов среди других параметров. Тарифные планы также может использоваться для моделирования toocreate Cruiser облака или сценарии «Что если», toounderstand влияние изменений в службах hello стоимость рабочей нагрузки.

В этом примере мы будем использовать сведения о службе hello из hello RateCard API toodefine новых служб в облаке Cruiser. В hello таким же способом, мы используем hello тарифы, действующие toohello служб toocreate новый тарифного плана на Cruiser облака.

В конце процесса преобразования hello hello он возможных toocreate новый шаг и опубликовать данные hello из hello RateCard API как новые службы и ставки.

![Рис. 4. Публикация данных hello из hello RateCard API как новые службы и скорости][4]

### <a name="verify-azure-services-and-rates"></a>Проверка служб Azure и тарифов
После публикации службы hello и ставки, вы можете проверить hello список импортированных служб в облаке Cruiser *служб* вкладки:

![Рис. 5 — проверка hello новых служб][5]

На hello *планы скорость* вкладку, можно проверить план скорость новых hello с именем «AzureSimulation» с показателями hello импортированы из hello RateCard API.

![Рис. 6 - проверка hello новый тарифного плана и связанные ставки][6]

### <a name="normalize-wap-and-azure-services"></a>Нормализация WAP и служб Azure
По умолчанию WAP предоставляет сведения об использовании на основе использования hello вычислений, памяти и сетевых ресурсов. В облаке Cruiser можно определить вашей служб на основе непосредственно для выделения hello или отслеживаемой использование этих ресурсов. Например можно задать базового уровня для каждый час ЦП или платы hello ГБ памяти, выделенный экземпляр tooan.

Например, в стоимость заказа toocompare между WAP и Azure мы должны tooaggregate hello уровня использования ресурсов на WAP на пакетов, которые затем могут быть tooAzure сопоставленных служб. Это преобразование можно легко реализовать в hello книги:

![Рис. 7. преобразование служб toonormalize данных WAP][7]

Последний шаг Hello в книге hello данные toopublish hello в базу данных облака Cruiser hello. На этом этапе данные об использовании hello теперь объединены в службы (, сопоставляемые toohello служб Azure) и привязывать toocreate hello toodefault ставки расходов.

После завершения hello книги можно автоматизировать hello обработку данных hello, путем добавления задачи в планировщике hello и указания hello частоту и время для hello toorun книги.

![Рис. 8. Планирование книги][8]

### <a name="create-reports-for-workload-cost-simulation-analysis"></a>Создание отчетов для анализа моделирования стоимости рабочей нагрузки
После использования hello собираются и расходы, загружаются в базы данных облака Cruiser hello, мы задействуем hello облака Cruiser аналитики модуля toocreate hello рабочей нагрузки стоимость моделирования, нам нужен.

В порядке toodemonstrate этот сценарий, мы создали hello следующих отчетов:

![Сравнение стоимости][9]

Hello верхней диаграмме показано сравнение стоимости службами сравнение цены hello выполняющаяся рабочая нагрузка hello каждой службы, определенные между WAP (Темно-синий) и Azure (светло-синий).

Hello нижней диаграмме отображается hello и те же данные, но с разбивкой по отделам. Это показывает hello затрат для каждого отдела toorun своей рабочей нагрузки WAP и Azure, наряду с hello различие между ними в строке экономии hello (зеленый цвет).

## <a name="azure-usage-api"></a>API Usage Azure
### <a name="introduction"></a>Введение
Недавно корпорация Майкрософт представила hello использования API Azure, допускающей запросу tooprogrammatically подписчиков в использования данных toogain анализировать их потребления. Это здорово для облака Cruiser клиентов, которые могут воспользоваться преимуществами hello богатый набор данных через этот интерфейс API.

Cruiser облака можно использовать hello интеграция с hello API использования несколькими способами. Гранулярность Hello (каждый час сведения об использовании) и сведения о метаданных ресурсов через API предоставляет приветствия hello необходимые dataset toosupport гибкие Потребительское или о гибком управлении ресурсами моделей. 

В этом учебнике мы представим одним из примеров как Cruiser облаке могут использовать преимущества hello сведения об использовании API. В частности мы будет создать группу ресурсов в Azure, свяжите теги для структуры hello учетной записи, а затем описан процесс запроса и обработки сведений о тегах hello в облаке Cruiser hello.

Hello конечной цели — отчеты могут toocreate toobe как hello, выполнив одно может tooanalyze затрат и и на основе структуры учетной записи hello заполняется по тегам hello потребления.

![Рис. 10. Отчет с разбивкой по тегам][10]

### <a name="microsoft-azure-tags"></a>Теги Microsoft Azure
Hello данные, доступные через hello API использования Azure включает в себя не только информация о потребленных, но метаданные ресурса, включая любые теги, связанные с ним. Теги предоставляют простой способ tooorganize ресурсов, но нужен tooensure действующие toobe заказа, который:

* Теги — это правильно примененных toohello ресурсы во время подготовки
* Теги используются должным образом на hello Потребительское/о гибком управлении ресурсами процесса tootie hello использования toohello учетной записи структуру организации.

Оба этих требования может быть сложной задачей, особенно в том случае, если ручной процесс подготовки hello или заряжается стороне. Неверный, неправильное или даже отсутствуют теги, распространенных проблем клиентов при с помощью меток и эти ошибки можно сделать на hello заряжается стороны очень сложно жизни.

Hello новые API для использования Azure, Cruiser облака можно ресурса, добавление тегов сведения по запросу и в программе сложных ETL вызывается книг, исправить эти общие тегов ошибки. Посредством преобразования с использованием регулярных выражений и корреляции данных Cruiser облака можно определить неправильно с тегами ресурсы и применить правильный тегов hello, обеспечивая hello правильный связывание hello ресурсы с hello потребителя.

На hello заряжается стороны облака Cruiser автоматизирует hello Потребительское/о гибком управлении ресурсами процесса и могут использовать hello тег сведения tootie hello использования toohello потребителя соответствующего (отдела, подразделения, проект, и т. д.). Автоматизация совершенствует процесс учета расходов и обеспечивает его согласованность и подконтрольность.

### <a name="creating-a-resource-group-with-tags-on-microsoft-azure"></a>Создание группы ресурсов с тегами в Microsoft Azure
Hello первым шагом в этом учебнике это toocreate группа ресурсов в hello портал Azure, а затем создание новых тегов tooassociate toohello ресурсов. В этом примере мы создадим hello следующие теги: отдел, среда, владелец проекта.

Снимок экрана приветствия ниже образец что теги, связанные с группой ресурсов с hello.

![Рис. 11. Группа ресурсов с сопоставленными тегами на портале Azure][11]

Hello следующим шагом является toopull hello сведения из API использования hello в Cruiser облака. в настоящее время Hello API использования предоставляет ответы в формате JSON. Ниже приведен пример извлекаемых данных hello.

    {
      "id": "/subscriptions/bb678b04-0e48-4b44-XXXX-XXXXXXX/providers/Microsoft.Commerce/UsageAggregates/Daily_BRSDT_20150623_0000",
      "name": "Daily_BRSDT_20150623_0000",
      "type": "Microsoft.Commerce/UsageAggregate",
      "properties":
      {
        "subscriptionId": "bb678b04-0e48-4b44-XXXX-XXXXXXXXX",
        "usageStartTime": "2015-06-22T00:00:00+00:00",
        "usageEndTime": "2015-06-23T00:00:00+00:00",
        "meterName": "Compute Hours",
        "meterRegion": "",
        "meterCategory": "Virtual Machines",
        "meterSubCategory": "Standard_D1 VM (Non-Windows)",
        "unit": "Hours",
        "instanceData": "{\"Microsoft.Resources\":{\"resourceUri\":\"/subscriptions/bb678b04-0e48-4b44-XXXX-XXXXXXXX/resourceGroups/DEMOUSAGEAPI/providers/Microsoft.Compute/virtualMachines/MyDockerVM\",\"location\":\"eastus\",\"tags\":{\"Department\":\"Sales\",\"Project\":\"Demo Usage API\",\"Environment\":\"Test\",\"Owner\":\"RSE\"},\"additionalInfo\":{\"ImageType\":\"Canonical\",\"ServiceType\":\"Standard_D1\"}}}",
        "meterId": "e60caf26-9ba0-413d-a422-6141f58081d6",
        "infoFields": {},
        "quantity": 8

      },
    },


### <a name="import-data-from-hello-usage-api-into-cloud-cruiser"></a>Импортировать данные из API использования hello в облаке Cruiser
Книги Cruiser облака с информацией автоматической toocollect и процесс из hello API использования. Книги ETL (извлечение — преобразование — загрузка) позволяет tooconfigure hello коллекции, преобразования и публикации данных в базу данных облака Cruiser hello.

Каждая книга может иметь одну или несколько коллекций. Это позволяет toocorrelate информацию из разных источников toocomplement или пополните hello данные об использовании. В этом примере мы создадим новый лист в книге hello Azure шаблона (*UsageAPI)* и задать новый *коллекции* tooimport сведения из hello API использования.

![Рисунок 3. Использование API данные, импортированные в лист UsageAPI hello][12]

Обратите внимание, что эта книга уже содержит другие листы tooimport служб из Azure (*ImportServices*) и обрабатывать данные потребления hello из hello API выставления счетов (*PublishData*).

Далее мы будем использовать hello API использования toopopulate hello *UsageAPI* лист и согласовывать hello информации hello потребления данных из hello API выставление счетов в hello *PublishData* листа.

### <a name="processing-hello-tag-information-from-hello-usage-api"></a>Сведения о тегах hello обработки из hello API использования
После импорта данных hello в книге hello, мы создадим действия преобразования в hello *UsageAPI* листа tooprocess hello информацию с hello API. Первым шагом является toouse «Расщеплений JSON» hello tooextract процессора теги из одного поля, а затем создать поля для каждого из них (отдел, проект, владелец и среде).

![Рис. 4. создать новые поля для сведений о тегах hello][13]

Hello уведомления службы «Сетевые возможности» отсутствуют данные тег hello (желтого прямоугольника), но мы убедимся, что он является частью hello одну группу ресурсов, просмотрев hello *ResourceGroupName* поля. Поскольку мы имеем hello теги для hello другие ресурсы из этой группы ресурсов, мы можно использовать этот сведения tooapply hello отсутствует ресурс toothis теги позже в процессе hello.

Hello следующим шагом является toocreate уточняющего запроса таблицы связывание hello сведения из hello теги toohello *ResourceGroupName*. Эту таблицу подстановки будет использоваться на hello следующего шага tooenrich hello потребления данных с сведения о тегах.

### <a name="adding-hello-tag-information-toohello-consumption-data"></a>Добавление hello тег сведения toohello потребления данных
Теперь перейдем toohello *PublishData* лист, какие процессы hello сведений о потреблении с hello API выставления счетов и добавить поля hello, извлеченных из тегов hello. Этот процесс выполняется, просмотрев таблицы подстановки hello создан для предыдущего шага hello, с помощью hello *ResourceGroupName* в качестве ключа hello hello уточняющих запросов.

![Рис. 5 — заполнение структуры счета hello hello данными из hello уточняющие запросы][14]

Обратите внимание, применения полей структуры hello соответствующую учетную запись для службы «Сетевые возможности» hello, исправления проблемы hello с hello отсутствуют теги. Мы заполняется полей структуры hello учетной записи для ресурсов, отличные от наших целевой группы ресурсов с «Другие», в порядке toodifferentiate их на hello отчеты.

Теперь нужно просто tooadd данные об использовании hello toopublish шаг. На этом этапе hello соответствующие ставки для каждой службы, определенные в нашем тарифного плана будет применяться toohello сведения об использовании, с hello результирующий бесплатно загрузить в базу данных hello.

лучше всего Hello является только наличие toogo таким образом один раз. После завершения hello книги, необходимо просто tooadd его toohello планировщика и он будет ежечасно или ежедневно в hello запланированного времени. Затем это лишь создание новых отчетов или настройка существующих в порядке tooanalyze hello данных tooget важные аналитические сведения из использовании облачных.

### <a name="next-steps"></a>Дальнейшие действия
* Для подробные инструкции по созданию Cruiser облака книг и отчетов, можно найти tooCloud Cruiser online [документации](http://docs.cloudcruiser.com/) (требуется допустимое имя входа).  Для получения дополнительных сведений о Cloud Cruiser обратитесь по адресу [info@cloudcruiser.com](mailto:info@cloudcruiser.com).
* В разделе [анализировать потребления ресурсов Microsoft Azure](billing-usage-rate-card-overview.md) Обзор hello использование ресурсов Azure и API-интерфейсов RateCard.
* Извлечение hello [выставления счетов Справочник API REST Azure](https://msdn.microsoft.com/library/azure/1ea5b323-54bb-423d-916f-190de96c6a3c) Дополнительные сведения о двух интерфейсов API, являющиеся частью hello набор API, предоставляемые hello диспетчера ресурсов Azure.
* Если вы хотите toodive прямо в образце кода hello, извлеките наших примеров Microsoft Azure Billing API код на [образцы кода Azure](https://azure.microsoft.com/documentation/samples/?term=billing).

### <a name="learn-more"></a>Подробнее
* В разделе hello [Обзор диспетчера ресурсов Azure](../azure-resource-manager/resource-group-overview.md) toolearn статьи о hello диспетчера ресурсов Azure.

<!--Image references-->

[1]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Create-New-Workbook-Collection.png "Рис. 1. Создание коллекции"
[2]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Import-Data-From-RateCard.png "Рис. 2 - Импорт данных из новой коллекции hello"
[3]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Transformation-Steps-Process-RateCard-Data.png "Рисунок 3. преобразование шаги tooprocess сбора данных из RateCard API"
[4]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Publish-RateCard-Data-New-Services-Rates.png "Рис. 4. Публикация данных hello из hello RateCard API как новые службы и скорости"
[5]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Verify-Azure-Services-And-Pricing1.png "Рис. 5 — проверка hello новых служб"
[6]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Verify-Azure-Services-And-Pricing2.png "Рис. 6 - проверка hello новый тарифного плана и связанные ставки"
[7]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Transforming-WAP-Normalize-Services.png "Рис. 7. преобразование служб toonormalize данных WAP"
[8]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Workbook-Scheduling.png "Рис. 8. Планирование книги"
[9]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Workload-Cost-Simulation-Report.png "Рис. 9 - образец отчета для сравнения затрат сценарий для hello рабочей нагрузки"
[10]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/1_ReportWithTags.png "Рис. 10. Отчет с разбивкой по тегам"
[11]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/2_ResourceGroupsWithTags.png "Рис. 11. Группа ресурсов с сопоставленными тегами на портале Azure"
[12]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/3_ImportIntoUsageAPISheet.png "Рис. 12 - данные об использовании API, импортируются в лист UsageAPI hello"
[13]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/4_NewTagField.png "Рис. 13 - создать новые поля для сведений о тегах hello"
[14]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/5_PopulateAccountStructure.png "Рис. 14 - заполнение структуры счета hello hello данными из hello уточняющие запросы"
