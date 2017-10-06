---
title: "Выставление счетов API-интерфейсы aaaAzure | Документы Microsoft"
description: "Дополнительные сведения об использовании выставления счетов Azure и RateCard API-интерфейсы, которые используется tooprovide анализировать потребление ресурсов Azure и тенденции."
services: 
documentationcenter: 
author: BryanLa
manager: tonguyen
editor: 
tags: billing
ms.assetid: 3e817b43-0696-400c-a02e-47b7817f9b77
ms.service: billing
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: billing
ms.date: 04/18/2017
ms.author: mobandyo;bryanla
ms.openlocfilehash: b3214996cc3279f76fdc7f0dbd2059c3ae7bb15c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-billing-apis-tooprogrammatically-get-insight-into-your-azure-usage"></a>Используйте API-интерфейсов выставления счетов Azure tooprogrammatically получить подробные сведения об использовании Azure
Используйте API-интерфейсов выставления счетов Azure toopull использования и данные ресурсов в вашей предпочтительный средства анализа. Hello использование ресурсов Azure и API-интерфейсы RateCard поможет вам точно спрогнозировать и затраты на управление. Hello API-интерфейсы реализуются как поставщик ресурсов и частью семейства hello API-интерфейсов, предоставляемых hello диспетчера ресурсов Azure.  

## <a name="azure-invoice-download-api-preview"></a>API для скачивания счетов Azure (предварительная версия)
Здравствуйте, один раз [участия в программе было завершено](billing-manage-access.md#opt-in), с помощью предварительной версии hello счетов загрузки [API счета](/rest/api/billing). функции Hello:

* **Azure Role-based Access Control** -Настройка доступа политики на hello [портал Azure](https://portal.azure.com) или через [командлетов Azure PowerShell](/powershell/azure/overview) toospecify, какие пользователи или приложения могут получить доступ данные об использовании toohello подписки. Вызывающие объекты должны использовать стандартные маркеры Azure Active Directory для проверки подлинности. Добавьте hello вызывающего объекта tooeither hello выставления счетов чтения, чтения, владельца или участника роли tooget toohello данных об использовании для определенной подписки Azure.
* **Дата, фильтрация** -hello используйте `$filter` tooget параметр, все счета hello в обратном хронологическом порядке по hello счет Дата окончания периода. 

> [!NOTE]
> Эта функция находится в первой версии preview и могут быть несовместимы toobackward изменения темы. Сейчас она недоступна для определенных предложений подписки (не поддерживаются EA, CSP, AIO), а также в Azure для Германии.

## <a name="azure-resource-usage-api-preview"></a>API использования ресурсов Azure (предварительная версия)
Используйте hello Azure [API использования ресурсов](https://msdn.microsoft.com/library/azure/mt219003) tooget оценка Azure потребления данных. включает Hello API:

* **Azure Role-based Access Control** -Настройка доступа политики на hello [портал Azure](https://portal.azure.com) или через [командлетов Azure PowerShell](/powershell/azure/overview) toospecify, какие пользователи или приложения могут получить доступ данные об использовании toohello подписки. Вызывающие объекты должны использовать стандартные маркеры Azure Active Directory для проверки подлинности. Добавьте hello вызывающего объекта tooeither hello выставления счетов чтения, чтения, владельца или участника роли tooget toohello данных об использовании для определенной подписки Azure.
* **Hourly or Daily Aggregations** (Агрегирование по часам или по дням) — вызывающие объекты могут указать, требуется ли получать данные об использовании Azure сегментами за каждый час или за каждый день. по умолчанию Hello — ежедневно.
* **Экземпляр метаданных (включая теги ресурсов)** — получение сведений уровня экземпляра как hello полное имя ресурса uri (/subscriptions/ {код_подписки} /..), hello тегов ресурсов и сведения о группе ресурсов. Эти метаданные помогает детерминированного и программно выделить использования по тегам hello, в целях как заряжается между.
* **Метаданные ресурса** -ресурсов как имя индикатора hello, индикатор категории, подкатегории индикатор, модульного и области приводятся подробные вызывающий hello хорошее представление о том, что было получено. Также мы работаем терминология метаданных ресурсов tooalign во всех hello портал Azure, Azure использование CSV, EA, CSV, выставление счетов и другие виды взаимодействия общедоступным, toolet сопоставлять данные между взаимодействий.
* **Usage for all offer types** (Использование для всех видов предложений). Данные об использовании доступны для всех видов предложений, таких как оплата по мере использования, MSDN, денежные обязательства, денежный кредит и EA.

## <a name="azure-resource-ratecard-api-preview"></a>API RateCard по ресурсам Azure (предварительная версия)
Используйте hello [API RateCard ресурсов Azure](https://msdn.microsoft.com/library/azure/mt219005) tooget hello список доступных ресурсов Azure и оценка сведения о ценах для каждого. включает Hello API:

* **Azure Role-based Access Control** -Настройка политик доступа на hello [портал Azure](https://portal.azure.com) или через [командлетов Azure PowerShell](/powershell/azure/overview) toospecify, какие пользователи или приложения могут получить доступ toohello RateCard данных. Вызывающие объекты должны использовать стандартные маркеры Azure Active Directory для проверки подлинности. Добавьте hello вызывающего объекта tooeither hello чтения, владельца или участника роли tooget toohello данных об использовании для определенной подписки Azure.
* **Support for Pay-as-you-go, MSDN, Monetary commitment, and Monetary credit offers (EA not supported)** (Поддержка оплаты по мере использования, MSDN, денежных обязательств, денежного кредита, EA не поддерживается). Этот API предоставляет сведения о тарифах Azure на уровне предложений.  Hello код, вызывающий этот API необходимо передавать сведения о ресурсах tooget сведения предложение hello и ставки. Мы ставки EA tooprovide в настоящее время не удается, так как предлагает EA настроили ставки по регистрации. 

## <a name="scenarios"></a>Сценарии
Ниже приведены некоторые сценарии hello, которые возможно сочетание hello hello использования и hello RateCard API-интерфейсы.

* **Потратьте Azure в течение месяца hello** -используйте сочетание hello hello использования и API-интерфейсы RateCard tooget улучшение анализа облачных тратить hello месяц. Можно анализировать hello каждый час и оценку контейнеров ежедневного использования и издержек.
* **Настройка оповещений** — использовать hello использования и hello tooget RateCard API-интерфейсы Оценка потребления облака и расходов и установка предупреждений на основе ресурсов или денежных.
* **Прогноз счета** — Get Оценка потребления и облако расходов и применить машинного обучения toopredict алгоритмы в конце hello hello цикл выставления счетов будет какие счета hello.
* **До использования анализ затрат** — использовать RateCard API toopredict hello, сколько счете мог бы быть ожидаемым использования при перемещении вашей tooAzure рабочих нагрузок. При наличии существующих рабочих нагрузок в других облаках или частных облаков, также можно сопоставить использования с hello Azure ставки tooget лучшую оценку Azure расходов. Это дает оценку hello toopivot возможности на предложение и сравнение и контрастности между типами другое предложение hello за оплату по мере использования, например денежных обязательств и Денежный кредит. также позволяет Hello API hello возможность toosee стоимость различия по региону, а также toodo toohelp стоимость гипотетического анализа, при принятии решений развертывания.
* **What-if analysis** -
  
  * Можно определить, является ли дополнительные рабочих нагрузок экономичное toorun в другой регион или в другой конфигурации hello ресурсов Azure. Ресурс Azure, могут отличаться затраты на основании hello регион Azure, которую вы используете.
  * Вы также можете определить, предоставляет ли другое предложение Azure более выгодный тариф на ресурс Azure.
  
## <a name="partner-solutions"></a>Решения партнеров
[Использование Microsoft Azure и Cloudyn включить API-интерфейсы RateCard tooProvide ITFM для клиентов](billing-usage-rate-card-partner-solution-cloudyn.md) описывается интеграция hello, предоставляемые API выставления счетов Azure партнера [Cloudyn](https://www.cloudyn.com/microsoft-azure/). В этой статье рассказывается о работе и включает в себя видео, в котором показано, как использовать Cloudyn и hello API-интерфейсов выставления счетов Azure tooget аналитики из данных использование Azure.

[Cloud Cruiser и выставление счетов интеграции API Microsoft Azure](billing-usage-rate-card-partner-solution-cloudcruiser.md) описывает способ [Cruiser облака Express для Azure Pack](http://www.cloudcruiser.com/partners/microsoft/) работает непосредственно с портала Windows Azure Pack (MAP) hello. Можно легко управлять обоих hello операционных и финансовых аспектами hello private или размещенного общедоступное облако Microsoft Azure с единого пользовательского интерфейса.   

## <a name="next-steps"></a>Дальнейшие действия
* Ознакомьтесь с примерами кода hello на GitHub:
  * [Пример кода API счетов](https://go.microsoft.com/fwlink/?linkid=845124)

  * [Пример кода API использования](https://github.com/Azure-Samples/billing-dotnet-usage-api)

  * [Пример кода API RateCard](https://github.com/Azure-Samples/billing-dotnet-ratecard-api)

* toolearn Дополнительные сведения о hello Azure Resource Manager в разделе [Обзор диспетчера ресурсов Azure](../azure-resource-manager/resource-group-overview.md). 

* Дополнительные сведения о hello набор инструментов, необходимые toohelp получить представление об облаке расходов, см. статьи hello [рынка руководство для средств управления финансовых ИТ (ITFM)](http://www.gartner.com/technology/reprints.do?id=1-212F7AL&ct=140909&st=sb).

