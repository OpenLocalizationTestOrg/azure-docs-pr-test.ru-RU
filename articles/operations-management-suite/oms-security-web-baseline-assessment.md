---
title: "aaaWeb базовых показателей оценки в Operations Management Suite безопасности и аудита базовое решение | Документы Microsoft"
description: "В этом документе объясняется, как toouse веб-базовых показателей оценки в OMS безопасность и аудит tooperform решения оценку базовые всех отслеживаемых веб-серверов в целях обеспечения соответствия и безопасности."
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 17837c8b-3e79-47c0-9b83-a51c6ca44ca6
ms.service: operations-management-suite
ms.custom: oms-security
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2017
ms.author: yurid
ms.openlocfilehash: dafa9d3d93fae31748306b60ee40b285dd59c802
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="web-baseline-assessment-in-operations-management-suite-security-and-audit-solution"></a>Оценка базовых показателей в Интернете в решении "Безопасность и аудит" Operations Management Suite
В этом документе дает возможность использовать OMS безопасности и аудита web базовых показателей оценки возможностей tooaccess hello безопасном состоянии отслеживаемых ресурсов.

## <a name="what-is-web-baseline-assessment"></a>Что такое оценка базовых показателей в Интернете?
В настоящее время система безопасности OMS предоставляет оценку базовых показателей безопасности для операционных систем. Он проверяет параметры настройки ОС hello серверов каждые 24 часа и дает представление об потенциально уязвимой параметры. Дополнительные сведения об этой возможности см. в статье [Оценка базовых показателей в решении "Безопасность и аудит" Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/oms-security-baseline).

Цель Hello hello Web базовой оценки — toofind потенциально уязвимой веб-сервере параметров. Здравствуйте три основных источника для являются базовой конфигурации hello веб-: конфигурации .NET, ASP.NET и IIS.  Так же, как hello оценки базовой операционной системы, безопасность OMS будет tooscan вашего веб-серверах каждые 24-часовом и предоставляет доступ к состояние безопасности из них.  В Internet Information Service (IIS), конфигурации являются широкие возможности настройки, позволяющее различные toobe уровни сайт и приложение переопределен. сканер Hello проверяет параметры hello на каждом уровне приложения или на сайте, в добавление toohello по умолчанию корневого уровня. Это помогает tooidentify потенциально уязвимой параметры и быстро устранять, а также рекомендации корпорации Майкрософт для этих параметров.

>[!NOTE] 
>Можно загрузить hello общие идентификаторы конфигурации и базовые правила, используемые OMS безопасности в этом [страницы](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335?redir=0).


## <a name="web-security-baseline-assessment"></a>Оценка базовых показателей безопасности в Интернете

Для этой предварительной версии функции hello может осуществляться через параметр поиска OMS hello и hello OMS безопасности и аудита панели мониторинга. Выполните действия hello под запросом tooperform hello appropriated.

1. В hello **Microsoft Operations Management Suite** основной панели мониторинга, щелкните **безопасность и аудит** плитки.
2. В hello **безопасность и аудит** панели мониторинга, вы увидите hello Web базовые перспективы Далее toohello ОС базовые перспективы.
   
    ![Оценка базовых показателей безопасности в Интернете в решении OMS "Безопасность и аудит"](./media/oms-security-web-baseline/oms-security-web-baseline-fig5.png)

3. Hello левая панель отображает hello число toohello базовой веб-серверов по сравнению, средний процент hello правил, переданный на всех серверах вычисляется hello и hello список серверов, на которых была выполнена.
4. Hello правой панели содержится список уникальных hello правила, не выполненный *серьезность*, и *RuleType*. Щелкнув любое из правил hello правой панели отображаются подробные сведения hello этого правила. Пример показан в hello под изображением. правило Hello, которое вычисляется находится в списке *Настройка правила*. Hello *AzId* поле, которое является уникальным идентификатором для каждого правила, которые используются корпорацией Майкрософт для отслеживания hello правила базовых показателей. В дополнение к этому toothat пользователям hello *ожидаемый результат* (корпорации Майкрософт рекомендуется значение), и другие сведения в отношении влияния на безопасность hello hello правила.
    
    ![Запрос](./media/oms-security-web-baseline/oms-security-web-baseline-fig6.png)

5. Можно создавать собственные запросы tooreview hello результаты. 

Hello первый запрос, который можно использовать — hello **Сводка по оценке базовые Web**. В hello **начинает поиск здесь** введите этот запрос: *тип = SecurityBaselineSummary BaselineType = Web*. Hello ниже приведен пример выходных данных.

![Результат запроса](./media/oms-security-web-baseline/oms-security-web-baseline-fig7.png)

>[!NOTE] 
>В этом запросе каждая запись указывает сводку оценки на одном сервере.

После входа в hello **поиска журналов**, tooobtain различных запросов можно ввести дополнительные сведения об оценке базовые hello web. В дополнение к этому toohello предыдущего запроса, также можно hello следующие функции в этой предварительной версии:

**Web Baseline Rule Assessment** (Оценка правила базовых показателей в Интернете). Каждая запись представляет оценку правила базовых показателей в Интернете на одном сервере. Он содержит все данные для неудачных правила hello *SitePath* на какие hello правило было вычислено, hello *ожидаемый результат*и hello *фактический результат*.

Запрос: *Type=SecurityBaseline BaselineType=Web AnalyzeResult=Failed*

![Результат запроса 2](./media/oms-security-web-baseline/oms-security-web-baseline-fig8.png)

**Показать все результаты для конкретного сервера**: этот запрос указывает, каким образом результаты toosee определенного сервера: запрос: *тип = SecurityBaseline BaselineType = компьютера веб = BaselineTestVM1*

![Результат запроса 3](./media/oms-security-web-baseline/oms-security-web-baseline-fig3.png)

Эти toocreate записей и запросы можно использовать собственные информационные панели, отчеты и оповещения. Ниже приведен пример пользовательского интерфейса элемента управления, можно добавить панель мониторинга tooyour. Рассказывается, как toovisualize данных с помощью конструктора представлений OMS [здесь](https://blogs.technet.microsoft.com/msoms/2016/06/30/oms-view-designer-visualize-your-data-your-way/). экран приветствия, показанный ниже является примером как плитку hello будет выглядеть после такой настройки.

!["Веб-транзакции"](./media/oms-security-web-baseline/oms-security-web-baseline-fig4.png)

## <a name="see-also"></a>См. также
Из этого документа вы узнали о процедуре оценки базовых показателей в Интернете в решении OMS "Безопасность и аудит". toolearn Дополнительные сведения о безопасности OMS см. следующие статьи hello.

* [Общие сведения об Operations Management Suite (OMS)](operations-management-suite-overview.md)
* [Мониторинг и реагирование tooSecurity оповещения в Operations Management Suite безопасности и аудита решения](oms-security-responding-alerts.md)
* [Мониторинг ресурсов в решении "Безопасность и аудит" Operations Management Suite](oms-security-monitoring-resources.md)

