---
title: "aaaPrevent непредвиденных расходов управление выставлением счетов - Azure | Документы Microsoft"
description: "Узнайте, как tooavoid Непредвиденная расходы на счете Azure. Используйте функции отслеживания затрат и управления для подписки Microsoft Azure."
services: 
documentationcenter: 
author: tonguyen10
manager: tonguyen
editor: 
tags: billing
ms.assetid: 482191ac-147e-4eb6-9655-c40c13846672
ms.service: billing
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/10/2017
ms.author: tonguyen
ms.openlocfilehash: d380f27861531351ac8e570469c59a84b9ca99e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="prevent-unexpected-charges-with-azure-billing-and-cost-management"></a>Предотвращение непредвиденных расходов с помощью функции выставления счетов и управления затратами в Azure

При подписке на Azure существует ряд задач, можно сделать tooget более точное представление о вашей расходов. Hello [калькулятор](https://azure.microsoft.com/pricing/calculator/) можно предоставить оценку затрат, перед тем как создать ресурс Azure. Hello [портал Azure](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) предоставляет hello текущего детализация затрат и прогноз для вашей подписки. Рассмотрим toogroup и понять затраты для различных проектов или команды, [тегов ресурсов](../azure-resource-manager/resource-group-using-tags.md). Если ваша организация имеет системы отчетности, что вы предпочитаете toouse, извлечь hello [выставления счетов API-интерфейсы](billing-usage-rate-card-overview.md). 

Вы также можете [загрузки за счета и подробные сведения о файлах использования](billing-download-azure-invoice-daily-usage-date.md) toomake убедиться, что оплаченные правильно. Дополнительные сведения о том, как сравнить данные о ежедневном использовании со счетом, см. в статье [Расшифровка счета за использование Microsoft Azure](billing-understand-your-bill.md).

В случае подписки через Enterprise Agreement (EA), поставщика облачных решений (CSP) или спонсорство Azure ко многим функциям в этой статье не применяются tooyou. Для вас доступен другой набор инструментов, который можно использовать для управления затратами. Ознакомьтесь с разделом [Дополнительные ресурсы для клиентов с соглашением Enterprise (EA), поставщиков облачных решений (CSP) и участников спонсорского предложения Azure](#other-offers).

Если ваша подписка использует бесплатную пробную версию, [Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/), Azure с открытой лицензией (AIO) или BizSpark, то такая подписка будет автоматически деактивирована, когда будут израсходованы кредиты. Дополнительные сведения о [лимиты оплаты,](#spending-limit) tooavoid с подпиской unexpectantly отключена. 

## <a name="get-estimated-costs-before-adding-azure-services"></a>Перед добавлением служб Azure узнайте их расчетную стоимость

### <a name="estimate-cost-online-using-hello-pricing-calculator"></a>Оценка затрат в интерактивном режиме с помощью калькулятора цен hello

Извлечение hello [калькулятор](https://azure.microsoft.com/pricing/calculator/) tooget оценочная стоимость ежемесячные службы hello, вас интересует. Можно добавить любой первой стороной ресурсов Azure tooget оценки стоимости.

![Снимок экрана: hello ценовой калькулятор меню](./media/billing-getting-started/pricing-calc.png)

Например A1 виртуальной машины (ВМ) Windows не предполагаемое toocost 66.96 Долларов США в месяц в вычислений часы, если оставить hello всего времени выполнения.

![Снимок экрана: hello калькулятор вывода, что ВМ Windows A1 предполагаемое toocost 66.96 Долларов США в месяц](./media/billing-getting-started/pricing-calcVM.png)

Дополнительные сведения о ценах см. в этой статье с [часто задаваемыми вопросами](https://azure.microsoft.com/pricing/faq/). Или если вы хотите tootalk tooan Azure менеджеров по продажам, обратитесь к 1-800-867-1389.

### <a name="review-hello-estimated-cost-in-hello-azure-portal"></a>Просмотрите hello Предполагаемая стоимость в hello портал Azure

Обычно при добавлении службы в hello портал Azure имеет представление, которое показывает, как расчетные затраты в месяц. Например при выборе размера виртуальной Машины Windows hello видно, что hello предполагаемой Месячная стоимость за часы hello вычислений:

![Пример: A1 ВМ Windows — оценка toocost 66.96 Долларов США в месяц](./media/billing-getting-started/vm-size-cost.PNG)

### <a name="set-up-billing-alerts"></a>Настройка платежных оповещений

Настройка предупреждений о выставлении счета сообщения электронной почты tooget превышения сумму, которая указывается стоимость использования. При наличии ежемесячных кредитов настройте оповещения на случай, когда будет израсходована определенная сумма. Дополнительные сведения см. в статье [Настройка оповещений о выставлении счетов за подписки Microsoft Azure](billing-set-up-alerts.md).

![Снимок экрана сообщения электронной почты с оповещением о выставлении счетов](./media/billing-getting-started/billing-alert.png)

> [!NOTE]
> Пока что доступна только предварительная версия этой функции, поэтому следует регулярно просматривать свои сведения об использовании.

Может потребоваться оценки затрат hello toouse из hello калькулятор цен в качестве руководства для первого оповещения.

### <a name="spending-limit"></a> Проверьте, установлена ли предельная сумма расходов

При наличии подписки, использующей кредиты затем hello лимита оплаты включен автоматически по умолчанию. Это позволяет избежать снятия с кредитной карты, когда достигнута предельная сумма кредитных средств. В разделе hello [полный список Azure предлагает и доступность hello лимита оплаты](https://azure.microsoft.com/support/legal/offer-details/).

Однако, в случае достижения предельной суммы расходов работа служб приостанавливается. Это означает, что обслуживание виртуальных машин прекращается. tooavoid простоя службы, необходимо отключить ограничение на расходы hello. Любые расходы, превышающие эту сумму, будут списываться с зарегистрированной в системе кредитной карты. 

toosee, если вы получили лимита оплаты, go toohello [представления подписок в центре учетных записей hello](https://account.windowsazure.com/Subscriptions). Если предельная сумма расходов установлена, то отобразится следующий баннер:

![Снимок экрана, показывающий предупреждение о расходы, ограничение на в hello центр учетных записей](./media/billing-getting-started/spending-limit-banner.PNG)

Щелкните заголовок hello и следуйте hello tooremove запросы лимита оплаты. Если вы не ввели сведения о кредитной карте при регистрации, необходимо ввести его hello tooremove лимита оплаты. Дополнительные сведения см. в разделе [Azure предельную сумму расходов — как она работает и как tooenable или удалите его](https://azure.microsoft.com/pricing/spending-limits/).

## <a name="ways-toomonitor-your-costs-when-using-azure-services"></a>Способы toomonitor затраты при использовании служб Azure

### <a name="tags"></a>Добавьте теги tooyour ресурсов toogroup данные выставления счетов

Можно использовать теги toogroup выставления счетов для поддерживаемых служб. Например при запуске нескольких виртуальных машин для различных групп, можно использовать теги toocategorize затраты средой центр затрат (HR, маркетинга, финансов) или (рабочей среде, подготовительной, test). 

![Снимок экрана, показывающий настройку теги в портал hello](./media/billing-getting-started/tags.PNG)

Hello теги отображались на протяжении влияния различных представления отчетов. Например, они сразу отображаются в [представлении анализа затрат](#costs), а в [CSV-файле сведений об использовании](#invoice-and-usage) они появляются после завершения первого расчетного периода.

Дополнительные сведения см. в разделе [использование теги tooorganize ресурсам Azure](../azure-resource-manager/resource-group-using-tags.md).

### <a name="costs"></a>Регулярно проверять hello портал для разбиения затрат и темпа работ

Когда службы уже работают, регулярно проверяйте свои затраты на их использование. Вы увидите текущего hello расходов и темпа работ на портале Azure. 

1. Посетите hello [колонке подписки на портале Azure](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) и выберите подписку.

2. Должны видеть детализация затрат hello и темпа работ в колонке всплывающее окно приветствия. Он может не поддерживается для вашего предложения (предупреждение будет отображаться верхней hello).

    ![Снимок экрана темп работ и декомпозиции в hello портал Azure](./media/billing-getting-started/burn-rate.PNG)

3. Нажмите кнопку **анализ затрат** в hello список toohello левой toosee hello детализация затрат по ресурсам. Подождите 24 часа после добавления службы для hello toopopulate данных.

    ![Снимок экрана: hello представление анализ затрат на портале Azure](./media/billing-getting-started/cost-analysis.PNG)

4. Можно применять фильтрацию по различным свойствам, таким как [теги](#tags), группа ресурсов и интервал времени. Нажмите кнопку **применить** tooconfirm hello фильтры и **загрузки** Если требуется файл tooexport hello представления tooa значениями, разделенных запятыми (.csv).

5. Кроме того, можно щелкнуть ресурса toosee тратить журнал и сколько ресурсов hello обходится каждый день.

    ![Снимок экрана: hello тратить представление журнала на портале Azure](./media/billing-getting-started/costhistory.PNG)

Рекомендуется проверять затраты hello отображаемые hello оценки, который вы видели, когда выбрана установка служб hello. Если затраты на hello совершенно отличаются от оценки, проверьте hello ценовой план (vs A1 A0 VM, например), выбранный для ресурсов. 

### <a name="consider-enabling-cost-cutting-features-like-auto-shutdown-for-vms"></a>Рассмотрите возможность включения функций, сокращающих затраты, таких как автоматическое завершение работы виртуальных машин

В зависимости от вашего сценария вы можете настроить автоматическое завершение работы виртуальных машин в hello портал Azure. Дополнительные сведения см. в записи блога [Announcing auto-shutdown for VMs using Azure Resource Manager](https://azure.microsoft.com/blog/announcing-auto-shutdown-for-vms-using-azure-resource-manager/) (Представляем автоматическое завершение работы виртуальных машин с помощью Azure Resource Manager).

![Снимок экрана: параметр автоматического завершения работы на портале hello](./media/billing-getting-started/auto-shutdown.PNG)

Автоматическое завершение работы не hello же, как при завершении работы в hello виртуальную Машину с параметрами управления питанием. Автоматическое завершение работы останавливает и освобождает toostop вашей ВМ дополнительные расходы. Дополнительные сведения о состояниях виртуальных машин см. в разделе "Часто задаваемые вопросы" статей о ценах на виртуальные машины [Linux](https://azure.microsoft.com/pricing/details/virtual-machines/linux/) и [Windows](https://azure.microsoft.com/pricing/details/virtual-machines/windows/).

Дополнительные возможности сокращения затрат в среде разработки и тестирования описаны на странице [Azure DevTest Labs](https://azure.microsoft.com/services/devtest-lab/).

### <a name="turn-on-and-check-out-azure-advisor-recommendations"></a>Включите Azure Advisor и ознакомьтесь с рекомендациями

[Azure Advisor](../advisor/advisor-overview.md) — это предварительная версия функции, которая помогает снизить затраты, определяя ресурсы с низким уровнем использования. Включите в hello портала Azure:

![Снимок экрана кнопки Azure Advisor на портале Azure](./media/billing-getting-started/advisor-button.PNG)

Затем можно получить практические рекомендации в hello **стоимость** вкладку в панели мониторинга Advisor hello:

![Снимок экрана с примером рекомендации Azure Advisor](./media/billing-getting-started/advisor-action.PNG)

Дополнительные сведения см. в разделе [Рекомендации Azure Advisor по затратам](../advisor/advisor-cost-recommendations.md).

### <a name="billing-api"></a>API выставления счетов

Используйте наши API tooprogrammatically get об использовании выставления счетов. Используйте hello RateCard API и tooget вместе hello API использования платных использования. Дополнительные сведения см. в статье [Получение ценных сведений о потреблении ресурсов Microsoft Azure](billing-usage-rate-card-overview.md).

## <a name="other-offers"></a> Дополнительные ресурсы и особые случаи

### <a name="ea-csp-and-sponsorship-customers"></a>Клиенты с соглашением EA, со спонсорским предложением и партнеры по программе CSP
Можно также обратиться tooyour диспетчера учетных записей или tooget партнеру Azure к работе.

| ПРЕДЛОЖЕНИЕ | Ресурсы |
|-------------------------------|-----------------------------------------------------------------------------------|
| Соглашение Enterprise (EA) | [Портал EA](https://ea.azure.com/), [справочные документы](https://ea.azure.com/helpdocs) и [отчет Power BI](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-enterprise/) |
| Поставщик облачных решений (CSP) | Поставщик tooyour ток |
| Спонсорское предложение Azure | [Портал спонсорского предложения Azure](https://www.microsoftazuresponsorships.com/) |

Если вы управляете ИТ для большой организации, рекомендуется чтение [корпоративные функции формирования шаблонов](../azure-resource-manager/resource-manager-subscription-governance.md) и hello [корпоративных ИТ Технический документ](http://download.microsoft.com/download/F/F/F/FFF60E6C-DBA1-4214-BEFD-3130C340B138/Azure_Onboarding_Guide_for_IT_Organizations_EN_US.pdf) (загрузка .pdf, только на английском языке).

### <a name="check-your-subscription-and-access"></a>Проверьте подписку и доступ

Требуется Просмотр расходов [сведения toobilling доступа на уровне подписки](billing-manage-access.md), но только Здравствуйте, администратор учетной записи имеет доступ к hello [центр учетных записей](https://account.windowsazure.com/Home/Index), изменить сведения об оплате и управления подписками. Здравствуйте, администратор учетной записи — hello лицо, которое проходит процесс регистрации hello. Дополнительные сведения см. в разделе [добавить или изменить роли Администратор Azure, управлять hello подписки или службы](billing-add-change-azure-subscription-administrator.md).

toosee, если вы Здравствуйте, администратор учетной записи перейдите toohello [колонке подписки в hello портал Azure](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) и просмотрите список подписок, у вас есть доступ к hello. Просмотрите столбец **Моя роль**. Если в нем отображается роль *Администратор учетной записи*, то у вас есть необходимый доступ. Если отображается другая роль, например *Владелец*, то у вас нет всех прав доступа.

![Снимок экрана вашей роли в hello представление подписок на hello портал Azure](./media/billing-getting-started/sub-blade-view.PNG)

Если вы не Здравствуйте, администратор учетной записи, то кто-то, скорее всего, предлагает частичный доступ через [управления доступом на основе роли Azure Active Directory](../active-directory/role-based-access-control-configure.md) (RBAC). toomanage подписки и выставление счетов info, изменение [найти Здравствуйте, администратор учетной записи](billing-subscription-transfer.md#whoisaa) и попросите его задачи hello tooperform или [передачи tooyou подписки hello](billing-subscription-transfer.md).

Если администратор учетной записи больше не с вашей организацией и необходимости toomanage выставления счетов, [обратитесь в службу поддержки](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade). 
## <a name="need-help-contact-support"></a>Требуется помощь? Обратитесь в службу поддержки.

Если вам нужна помощь, [обратитесь в службу поддержки](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget быстро устранить проблему.
