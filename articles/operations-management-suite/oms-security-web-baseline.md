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
# <a name="web-baseline-assessment-in-operations-management-suite-security-and-audit-solution"></a>Оценка базовых показателей в Интернете в решении "Безопасность и аудит" Operations Management Suite
Этот документ поможет вам toouse [решение аудита и безопасности Operations Management Suite (OMS)](operations-management-suite-overview.md) веб-оценки базовые возможности tooaccess hello безопасном состоянии отслеживаемых ресурсов.

## <a name="what-is-web-baseline-assessment"></a>Что такое оценка базовых показателей в Интернете?
В настоящее время система безопасности OMS предоставляет оценку базовых показателей безопасности для операционных систем. Он проверяет параметры операционной системы hello серверов каждые 24 часа и дает представление об потенциально уязвимой параметры. Дополнительные сведения об этой возможности см. в статье [Оценка базовых показателей в решении "Безопасность и аудит" Operations Management Suite](oms-security-baseline.md).

Цель Hello hello web базовых показателей оценки — toofind потенциально уязвимой веб-сервере параметров. Здравствуйте три основных источника для являются базовой конфигурации hello веб-: конфигурации .NET, ASP.NET и IIS.  Так же, как hello оценки базовой операционной системы, безопасность OMS будет tooscan вашего веб-серверах каждые 24-часовом и предоставляет доступ к состояние безопасности из них.  В Internet Information Service (IIS), конфигурации являются широкие возможности настройки, позволяющее различные toobe уровни сайт и приложение переопределен. сканер Hello проверяет параметры hello на каждом уровне приложения или на сайте, в добавление toohello по умолчанию корневого уровня. Это помогает tooidentify потенциальной уязвимости параметры расположения и быстро устранять.


## <a name="web-security-baseline-assessment"></a>Оценка базовых показателей безопасности в Интернете
Для этой предварительной версии этой функции будет toobe, получить доступ с помощью параметра поиска OMS hello. Выполните действия hello под запросом tooperform hello appropriated.

1. В hello **Microsoft Operations Management Suite** основной панели мониторинга щелкните **безопасность и аудит** плитки.
2. В hello **безопасность и аудит** панели мониторинга, щелкните **поиска журналов** кнопки.
3. Hello первый запрос, который можно использовать — hello **Сводка по оценке базовые Web**. В hello **начинает поиск здесь** введите этот запрос: тип*= SecurityBaselineSummary BaselineType = web*. Следующий экран приветствия имеет образец вывода:

![Сводка по оценке базовых показателей в Интернете](./media/oms-security-web-baseline/oms-security-web-baseline-fig1-new.png)

> [!NOTE]
> В этом запросе каждая запись указывает сводку оценки на одном сервере.

После входа в hello **поиска журналов**, tooobtain различных запросов можно ввести дополнительные сведения об оценке базовые hello web. В дополнение к этому toohello предыдущего запроса, также можно hello следующие функции в этой предварительной версии.

**Web Baseline Rule Assessment** (Оценка правила базовых показателей в Интернете). Каждая запись представляет оценку правила базовых показателей в Интернете на одном сервере. Он включает все данные для правила hello, местоположение, hello ожидаемый результат и фактический результат hello.

**Запрос**: Type*=SecurityBaseline BaselineType=web*

![Оценка правила базовых показателей в Интернете](./media/oms-security-web-baseline/oms-security-web-baseline-fig2.png)

**Показать все результаты для конкретного сервера**: этот запрос указывает, каким образом результаты toosee определенного сервера.

**Запрос**: *Type=SecurityBaseline BaselineType=web Computer=BaselineTestVM1*

![Все результаты](./media/oms-security-web-baseline/oms-security-web-baseline-fig3.png)

Также можно использовать эти toocreate записей и запросы собственных панелей мониторинга, отчеты и оповещения. экран приветствия, показанный ниже имеет образец пользовательского интерфейса элемента управления, можно добавить панель мониторинга tooyour. Рассказывается, как toovisualize данных с помощью конструктора представлений OMS [здесь](https://blogs.technet.microsoft.com/msoms/2016/06/30/oms-view-designer-visualize-your-data-your-way/). экран приветствия, показанный ниже является примером как плитку hello будет выглядеть после такой настройки.

![Пример пользовательского интерфейса](./media/oms-security-web-baseline/oms-security-web-baseline-fig4.png)

> [!NOTE]
> Если вы хотите tooknow hello параметры, которые проверяются на наличие базовых показателей оценки hello, можно загрузить [электронную таблицу Excel](https://gallery.technet.microsoft.com/OMS-Web-Baseline-1e811690) , содержащий эти параметры.

## <a name="see-also"></a>См. также
В этом документе вы узнали о процедуре оценки базовых показателей в Интернете в решении OMS "Безопасность и аудит". toolearn Дополнительные сведения о безопасности OMS см. следующие статьи hello.

* [Общие сведения об Operations Management Suite (OMS)](operations-management-suite-overview.md)
* [Мониторинг и реагирование tooSecurity оповещения в Operations Management Suite безопасности и аудита решения](oms-security-responding-alerts.md)
* [Мониторинг ресурсов в решении "Безопасность и аудит" Operations Management Suite](oms-security-monitoring-resources.md)

