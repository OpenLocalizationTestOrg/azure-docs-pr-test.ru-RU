---
title: "aaaUnderstand счета для Azure | Документы Microsoft"
description: "Узнайте, как tooread и проанализировать использование и счет для вашей подписки Azure"
services: 
documentationcenter: 
author: tonguyen10
manager: tonguyen
editor: 
tags: billing
ms.assetid: 32eea268-161c-4b93-8774-bc435d78a8c9
ms.service: billing
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/14/2017
ms.author: tonguyen
ms.openlocfilehash: a3195eb129b1576e8cb665aa6f88a1a2647edd78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="understand-your-bill-for-microsoft-azure"></a>Расшифровка счета за использование Microsoft Azure
toounderstand выставления счетов Azure, сравнить счет с hello подробного ежедневного использования файла и стоимости управления отчетами в hello портал Azure hello.

tooobtain счет PDF-ФАЙЛ и копия подробные ежедневного использования CSV загрузку файла, в разделе [получения счета и ежедневно данные об использовании выставления счетов Azure](billing-download-azure-invoice-daily-usage-date.md). 

Подробное описание терминов в счете и файле с данными о ежедневном использовании см. в статьях [Значение терминов в счете Microsoft Azure](billing-understand-your-invoice.md) и [Значение терминов в файле с подробными данными об использовании Microsoft Azure](billing-understand-your-usage.md). 

Дополнительные сведения о стоимости отчеты по управлению hello см [управление стоимостью портал Azure](https://docs.microsoft.com/en-us/azure/billing/billing-getting-started).


## <a name="charges"></a>Как сделать правильность расходов hello в Мой счет?
Если в вашем счете есть какое-то списание, о котором вы хотите узнать подробнее, то существует несколько вариантов это сделать.

### <a name="option-1-review-your-invoice-and-compare-hello-usage-and-costs-with-hello-detailed-usage-csv-file"></a>Вариант 1: Просмотрите счет и сравнить использование hello и расходы с hello подробные использование CSV-файла

Hello подробные сведения об использовании CSV-файла показано стоимость периода выставления счетов и ежедневном использовании. см. подробные сведения об использовании CSV-файл tooget [получения счета и ежедневно данные об использовании выставления счетов Azure](https://docs.microsoft.com/en-us/azure/billing/billing-download-azure-invoice-daily-usage-date).

Платы за использование отображаются на уровне индикатор hello. Hello следующие термины означают hello же в обоих счета hello и hello подробные сведения об использовании файла. Например hello выставления счетов цикла по счету hello — эквивалент toohello расчетного периода, показано в hello подробные сведения об использовании файла.

 | Счет (PDF) | Подробные данные об использовании (CSV)|
 | --- | --- |
|Цикл выставления счетов | Расчетный период |
 |Имя |Категория средства измерения |
 |Тип |Подкатегория средства измерения |
 |Ресурс |Имя средства измерения |
 |Регион |Регион средства измерения |
 |Потреблено |Потребленный объем |
 |Включено |Включенный объем |
 |Подлежит оплате |Избыточный объем |

Hello **сборам за использование** раздел счет содержит hello общее значение для каждого индикатора, которое было получено в течение периода выставления счетов. Например, hello следующем снимке экрана показано использование плата hello служба планировщика Azure.

![Плата за использование в счете](./media/billing-understand-your-bill/1.png)

Hello **инструкции** раздел из подробные сведения об использовании CSV показано hello же бесплатно. Оба hello *израсходовано* сумма и *значение* invoice hello совпадения.

![Плата за использование в CSV-файле](./media/billing-understand-your-bill/2.png)

декомпозиция издержек на ежедневной основе перейдите toohello toosee **ежедневном использовании** раздел hello CSV. Фильтр для «Планировщик» в разделе *индикатор категории* и можно увидеть, какие дни hello индикатор использовался и о том, сколько было получено. Hello *ресурсов* и *группы ресурсов* также приведены сведения для сравнения. Hello *израсходовано* значения следует добавлять вверх по toowhat отображаться на накладной hello.

![Ежедневные раздел Использование hello CSV](./media/billing-understand-your-bill/3.png)

tooget hello стоимость в день, умножьте hello *израсходовано* суммы с hello *скорость* значение из hello **инструкции** раздела.

toolearn Дополнительные сведения о счете hello. в разделе [понять Azure счет](billing-understand-your-invoice.md).

toolearn о каждого столбца hello hello CSV, в разделе [понять Azure подробные сведения об использовании](billing-understand-your-invoice.md).

### <a name="option-2-review-your-invoice-and-compare-with-hello-usage-and-costs-in-hello-azure-portal"></a>Вариант 2: Просмотрите счет и сравнить с использование hello и затрат в hello портал Azure

Hello портал Azure также может помочь вам стоимость. Hello портал Azure предоставляет стоимость управления диаграммы для быстрого обзора стоимость использования и hello на ваш счет.

toocontinue с hello приведенном выше примере, посетите hello [страница «подписки»](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade), выберите подписку, а затем выберите **анализ затрат**. После этого можно указать интервал времени, hello и издержки на использование для службы планировщика Azure hello в разделе.

![Представление "Анализ стоимости" на портале Azure](./media/billing-understand-your-bill/4.png)

Детализация hello ежедневно toosee затрат в **стоимости журнала**, щелкните строку hello.

![Представление "Журнал затрат" на портале Azure](./media/billing-understand-your-bill/5.png)

toolearn более, в разделе [предотвратить непредвиденные затраты на управление затрат и выставлению счетов Azure](billing-getting-started.md#costs).

## <a name="external"></a>Как узнать о расходах на внешние службы?
Внешние службы (также называемые заказами в Azure Marketplace) предоставляются независимыми поставщиками служб и оплачиваются отдельно. плата Hello не отображаются на ваш счет Azure. toolearn более, в разделе [понять Azure взимает плату внешней службы](billing-understand-your-azure-marketplace-charges.md).

## <a name="payment"></a>Как выполнить оплату?

Если вы настроили кредитной или дебетовой картой как метод оплаты, автоматически в течение 10 дней после окончания расчетного периода hello оплачивается hello оплаты. На вашем операторе кредитной карты скажет элементов строки hello **MSFT Azure**.

Если вы [оплаты по выставлению счетов](billing-how-to-pay-by-invoice.md), расположение toohello оплаты перечисленные внизу hello счет отправки. Для получения дополнительных сведений [обратитесь в службу поддержки](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).

## <a name="how-do-i-check-hello-status-of-a-payment-made-by-credit-card"></a>Как проверить состояние hello платеж по кредитной карте?

[Создайте запрос в службу поддержки](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooask статуса hello оплаты. 

## <a name="tips-for-cost-management"></a>Советы по управлению затратами
- Оценки затрат, с помощью hello [калькулятор](https://azure.microsoft.com/pricing/calculator/) и [совокупную стоимость владения калькулятора](https://aka.ms/azure-tco-calculator)и получить hello [подробные сведения о ценах для каждой службы](https://azure.microsoft.com/en-us/pricing/).
- [Настройте оповещения о выставлении счетов](billing-set-up-alerts.md).
- [Просмотреть использование и затраты регулярно в hello портал Azure](billing-getting-started.md#costs).

## <a name="need-help-contact-support"></a>Требуется помощь? Обратитесь в службу поддержки.

Если вы по-прежнему нужна помощь, [обратитесь в службу поддержки](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget быстро устранить проблему.
