---
title: "aaaWhat является Microsoft Power BI Embedded?"
description: "Power BI Embedded позволяет toointegrate отчеты Power BI в веб-приложения или приложения для мобильных устройств требуется toobuild пользовательских решений."
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 03649b72-b7d7-40ca-b077-12356d72d4f3
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/20/2017
ms.author: asaxton
ms.openlocfilehash: 0353938b6cdd9bb58b123b250f45f76b8cc7abe6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-microsoft-power-bi-embedded"></a>Что такое Microsoft Power BI Embedded?
С помощью **Power BI Embedded**можно интегрировать отчеты Power BI прямо в веб- или мобильные приложения.

![](media/powerbi-embedded-whats-is/what-is.png)

Power BI Embedded — **службы Azure** , позволяет независимым поставщикам программного обеспечения и взаимодействие с toosurface разработчики приложения Power BI данные в свои приложения. У приложений, создаваемых разработчиками, есть собственные пользователи и отдельный набор функций. Эти приложения также может произойти toohave некоторые встроенные элементы данных, такие как диаграммы и отчеты, которые теперь могут быть включены с Microsoft Power BI Embedded. Не требуется учетная запись Power BI toouse приложения. Можно продолжить toosign в приложении tooyour так же, как и прежде и просматривать и взаимодействовать с hello работы с отчетами Power BI, не требуя дополнительной лицензии.

## <a name="licensing-for-microsoft-power-bi-embedded"></a>Лицензирование Microsoft Power BI Embedded
В hello **Microsoft Power BI Embedded** модель использования, лицензирования для Power BI не несет ответственность за hello hello для конечных пользователей.  Вместо этого **сеансы** приобретенных разработчиком hello приложения hello, которое занимает hello визуальных элементов и взимается toohello подписке, владеющей этими ресурсами. Дополнительные сведения можно найти на hello [странице цен](https://azure.microsoft.com/en-us/pricing/details/power-bi-embedded/).

## <a name="microsoft-power-bi-embedded-conceptual-model"></a>Концептуальная модель Microsoft Power BI Embedded

![](media/powerbi-embedded-whats-is/model.png)

Как и любая другая служба в Azure, ресурсы для Power BI Embedded подготовленные в hello [API диспетчера ресурсов Azure](https://msdn.microsoft.com/library/mt712306.aspx). В этом случае является hello ресурсов, для которого подготовку **коллекции рабочей области Power BI**.

## <a name="workspace-collection"></a>Коллекция рабочих областей
Объект **коллекции рабочей** — hello контейнер верхнего уровня Azure для ресурсов, содержащая 0 или более **рабочие области**.  A **рабочей** **коллекции** все стандартные свойства Azure hello, а также hello следующее:

* **Ключи доступа** — ключи, используемые при вызове безопасного hello Power BI API-интерфейсы, (описан в следующем разделе).
* **Пользователи** — Azure Active Directory (AAD) пользователи, имеющие toomanage права администратора hello коллекции рабочей области Power BI через портал Azure hello или API диспетчера ресурсов Azure.
* **Область** — в рамках подготовки **коллекции рабочей**, можно выбрать область toobe, подготовленный в. Дополнительные сведения см. на странице [Регионы Azure](https://azure.microsoft.com/regions/).

## <a name="workspace"></a>Рабочая область
**Рабочая область** представляет собой контейнер для содержимого Power BI, в том числе наборов данных и отчетов. После создания **рабочая область** пуста. Будет создавать содержимое с помощью Power BI Desktop и в рабочей области с помощью hello программно вы развернете hello PBIX [импорта API Power BI](https://msdn.microsoft.com/library/mt711504.aspx). Вы также можете программным способом создать набор данных и в самом приложении создать отчеты, а не делать это с помощью Power BI Desktop.

## <a name="using-workspace-collections-and-workspaces"></a>Использование коллекций рабочих областей и рабочих областей
**Рабочая область коллекций** и **рабочих областей** являются контейнерами содержимое, организованные в любой наилучшим образом подходит для hello проект приложения hello, построении и использовать. Будет несколькими различными способами, что может упорядочить их hello содержимое. Вы можете tooput все содержимое в одной рабочей области и затем toofurther маркеры приложения более поздних версий используйте подразделять содержимое hello среди клиентов. Можно также выбрать tooput все пользователи в отдельных рабочих областей таким образом, что некоторые разделение между ними. Или можно выбрать пользователей tooorganize по региону, а не по клиентам. Это гибкая конфигурация позволяет toochoose hello лучшим способом tooorganize содержимого.

## <a name="cached-datasets"></a>Кэшированные наборы данных
Вы можете использовать кэшированные наборы данных.  Однако обновить кэшированные данные после их загрузки в **Microsoft Power BI Embedded**нельзя. Кэшированный набор данных означает, что были импортированы в Power BI Desktop hello данных вместо использования DirectQuery.

## <a name="authentication-and-authorization-with-app-tokens"></a>Проверка подлинности и авторизация с маркерами приложений
**Microsoft Power BI Embedded** откладывает tooperform приложения tooyour все hello необходимые аутентификации и авторизации пользователей. При этом явно не требуется, чтобы ваши пользователи использовали Azure Active Directory (Azure AD).  Вместо этого приложение выражает слишком**Microsoft Power BI Embedded** toorender авторизации отчета Power BI с помощью **токены проверки подлинности приложения (приложения токены)**.  Эти **токенов приложения** создаются по мере необходимости, когда приложение хочет toorender отчета.

![](media/powerbi-embedded-whats-is/app-tokens.png)

**Токены проверки подлинности приложения (приложения токены)** , используемые tooauthenticate от **Microsoft Power BI Embedded**.  Существует три типа **маркеров приложений**:

1. Маркеры подготовки используются при подготовке новой **рабочей области** в **коллекции рабочих областей**.
2. Разработка маркерами - при внесении напрямую вызывает toohello **API-интерфейс REST Power BI**
3. Внедрение токенов — используется при создании toorender вызовы внедренный отчет в hello iframe

Эти маркеры используются для hello различных фаз взаимодействия с **Microsoft Power BI Embedded**.  токены Hello разрабатываются, поэтому вы можете делегировать разрешения из вашего приложения tooPower бизнес-Аналитики. Дополнительные сведения см. в статье [Аутентификация и авторизация в Power BI Embedded](power-bi-embedded-app-token-flow.md).

## <a name="create-or-edit-reports-within-your-application"></a>Создание и изменение отчетов в приложении

Теперь можно изменить существует отчеты или создавать новые отчеты непосредственно в приложении без необходимости toouse Power BI Desktop. Для этого необходимо, чтобы в рабочей области уже существовал набор данных.

## <a name="see-also"></a>Дополнительные материалы

[Типичные сценарии использования Microsoft Power BI Embedded](power-bi-embedded-scenarios.md)  
[Начало работы с Microsoft Power BI Embedded (предварительная версия)](power-bi-embedded-get-started.md)  
[Приступая к работе с примером Microsoft Power BI Embedded](power-bi-embedded-get-started-sample.md)  
[Внедрение отчета в Power BI Embedded](power-bi-embedded-embed-report.md)  
[Аутентификация и авторизация в Power BI Embedded](power-bi-embedded-app-token-flow.md)  
[Пример внедрения JavaScript](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
[Репозиторий PowerBI-CSharp на сайте GitHub](https://github.com/Microsoft/PowerBI-CSharp)  
[Репозиторий PowerBI-Node на сайте GitHub](https://github.com/Microsoft/PowerBI-Node)  
У вас имеются и другие вопросы? [Повторите hello сообщества Power BI](http://community.powerbi.com/)
