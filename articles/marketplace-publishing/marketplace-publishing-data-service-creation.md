---
title: "aaaGuide toocreating службы данных для hello Marketplace | Документы Microsoft"
description: "Подробные инструкции, как toocreate, сертификации и развертывать службу данных для приобретения на hello Azure Marketplace."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 96194198-6991-43b4-918e-ee337e250339
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: hascipio; avikova
ms.openlocfilehash: 0220d357ae0ec89e7d4f6399605850e57c646f73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="data-service-publishing-guide-for-hello-azure-marketplace"></a>Данные службы руководство по публикации для hello Azure Marketplace
> [!IMPORTANT]
> **В настоящее время мы больше не подключаем новые издатели служб данных. Новые службы данных не будут утверждены для добавления в список.** Если у вас есть бизнес-приложений SaaS хотелось бы toopublish Дополнительные сведения можно найти на AppSource [здесь](https://appsource.microsoft.com/partners). Если у вас есть приложениях IaaS или разработчик службы вы бы как toopublish в Azure Marketplace можно найти дополнительные сведения о [здесь](https://azure.microsoft.com/marketplace/programs/certified/).
> 
> 

После завершения hello шага 1, [создания учетной записи и регистрации](marketplace-publishing-accounts-creation-registration.md), мы предложены вы hello [общие нетехнических](marketplace-publishing-pre-requisites.md) и [технические требования](marketplace-publishing-data-service-creation-prerequisites.md) службы данных предложить в Azure Marketplace. Теперь мы поможет hello шаги для создания предложения службы данных на hello [портал публикации] [ link-pubportal] для hello Azure Marketplace.

## <a name="1----login-toohello-publishing-portal"></a>1.    Toohello входа портал публикации.
Go слишком[https://publish.windowsazure.com](https://publish.windowsazure.com.)

**Для первого tooPublishing входа время портала используйте hello же учетную запись, с которым профиль компании продавца, зарегистрированные в центре разработчиков.**  (Позднее можно добавить любой сотрудник компании как соадминистратора в hello портал публикации).

Щелкните hello **публикации служб данных** плитке, если это hello при первом входе в портал публикации hello.

## <a name="2----choose-data-services-in-hello-navigation-menu-on-hello-left-side"></a>2.    Выберите **Data Services** выберите в меню навигации hello hello слева.
  ![рисунок](media/marketplace-publishing-data-service-creation/pubportal-main-nav.png)

## <a name="3----create-a-new-data-service"></a>3.    Создание новой службы данных
Введите название hello вашей новой службы данных, предложения и нажмите на «+» в правом hello.

  ![рисунок](media/marketplace-publishing-data-service-creation/step-3.png)

## <a name="4----review-hello-sub-menu-under-hello-newly-created-data-service-in-hello-navigation-menu"></a>4.    Службы данных новые hello подменю проверку под hello в меню навигации hello.
Щелкните hello **Пошаговое руководство** и проверьте все необходимые действия, необходимые toopublish hello правильно службы данных на hello Azure Marketplace.

> [!TIP]
> Всегда можно щелкнуть hello ссылки на странице «Пошаговое руководство» hello или используйте вкладки на предложение службы данных hello подменю в левой части hello.
> 
> 

## <a name="5----create-a-new-plan"></a>5.    Создание нового плана
### <a name="offers-plans-transactions"></a>Предложения, планы, транзакции.
Каждое предложение может иметь несколько планов, но не менее одного (1). Когда конечные пользователи подписка предложение tooyour они подписаны для одного плана hello предложения. Каждый план определяет, как будет конечным пользователям быть toouse доступ к службе.

В настоящее время Azure Marketplace поддержка только ежемесячные подписки транзакции в соответствии с модели для служб данных, т. е. конечные пользователи будут уделять toohello цены hello конкретный план, они подписались tooand в соответствии с ежемесячная плата будет может tooconsume числом каждого месяца транзакции, определенной hello плана.

Каждая транзакция, обычно определяется как число записей, возвращаемых службы данных на основании hello запроса, отправленного toohello службы. по умолчанию Hello равно 100. Число транзакций, возвращаемых tooeach запрос будет число записей делится на 100 и округленное до ближайшего целого в toohello.

Это служба Azure Marketplace слоя ответственности toomonitor (метр) количество транзакций, потребляемых каждым запросом.

> [!IMPORTANT]
> Конечные пользователи, которых достиг ограничения на операции hello hello месяц будет блокирована toouse hello службы до завершения их ежемесячного цикла подписки.
> 
> Hello плана или одной из схем hello можно (но не должен) содержать неограниченное количество транзакций.
> 
> 

### <a name="create-a-plan"></a>Создание плана.
1. Щелкните **«+»** Далее toohello «добавить новый план».
2. Выберите один из вариантов hello: **неограниченное количество** или **ограниченный** использования для этого плана.  Если Limited, затем укажите номер hello транзакции hello плана позволит tooconsume в месяц.
   
    ![рисунок](media/marketplace-publishing-data-service-creation/step-5.1.png)  
   
    Публикацию портала также предложит «Идентификатор плана», которое будет toohello используется toocommunicate конечных пользователей hello имя плана hello в hello пользовательского интерфейса и также используются программой hello tooidentify hello рынок службы плана. При желании можно изменить hello «Планирование идентификатор».
   
   > [!NOTE]
   > Hello «Идентификатор плана» должно быть уникальным в пределах области hello каждого предложения. При использовании других идентификаторов в hello публикации портала планирование идентификатор будет заблокирована после hello первой публикации tooproduction и вы не будет возможности toochange этот идентификатор.
   > 
   > 
3. Щелкните tooaccept вашему выбору.
4. Затем вам будет предложено ответить на несколько дополнительных вопросов о новом плане.
   
    ![рисунок](media/marketplace-publishing-data-service-creation/step-5.2.png)

| Вопрос | Значимость |
| --- | --- |
| **Этот план бесплатный и доступен во всем мире?** |Можно создать полностью бесплатный план. Его hello только план на это предложение — означает, что вы публикуете «Свободного предлагаются» в hello Marketplace. Если это только для одного (из лишь немногие) плана hello позволяет конечным пользователям параметр toooffer, toolearn Дополнительные сведения о службе с помощью относительно небольшого числа транзакций в месяц.  Если hello ответ «Да», затем будет предложено без дополнительных вопросов. |

> [!NOTE]
> Конечным пользователям всегда можно обновить toohello платная планов.
> 
> 

| Вопрос | Значимость |
| --- | --- |
| **Предусмотрена ли бесплатная пробная версия?** |Можно выбрать «Нет пробная версия» вообще или предоставить параметр toouse план «Месяц». Издатели, например toouse, этот параметр tooprovide конечным пользователям hello вероятность toounderstand hello преимущества hello предлагают бесплатно в течение месяца. |

> [!IMPORTANT]
> Конечным пользователям будет в toopurchase возможности использования бесплатной пробной версии, только если у них установлены платежного средства например кредитной карты, соглашение enterprise agreement.
> 
> Через месяц hello бесплатной пробной версии Azure Marketplace начнется заряжается клиентов hello цены на момент выхода hello hello подписки, если клиента hello инициировал hello отмены подписки. Специальные уведомление не будет предоставляться toohello конечных пользователей.
> 
> 

| Вопрос | Значимость |
| --- | --- |
| **Для этого тарифа необходим toopurchase код рекламной акции?** |Издатели имеют параметр toolimit доступа tootheir планы обслуживания, предоставляя специального кода, называется «Promocode» toospecific клиентов. Только конечные пользователи, имеющие это Promocode будет может toosubscribe toohello плана. Если выбрать «Нет», то вы согласны, каждый из которых приобрести hello региона hello доступен (см. [руководство по содержимому маркетинга Marketplace](marketplace-publishing-push-to-staging.md) подробнее) будет может toosubscribe toothis плана. Дополнительных вопросов больше не будет. |
| **Скрыть этот план от всех, у кого нет действующего промокода?** |Если hello ответов toohello предыдущий вопрос — «Yes» hello издатель имеет параметр toocompletely этот план удаляется из отображаются в Интерфейсе hello Marketplace hello. Это означает, клиенты не будут видеть этот план на hello предложение «подробности». Конечные пользователи, которые будут получать promocode toopurchase, будут tooit toosubscribe может с помощью этого promocode. |

## <a name="6----create-your-marketplace-marketing-content"></a>6.    Создание маркетинговых материалов Marketplace
Для как tooprovide сведения, необходимые в **отдела маркетинга, цены, поддержки и категории** вкладок перейдите на страницу [руководство по содержимому маркетинга Marketplace](marketplace-publishing-push-to-staging.md) это общие tooall артефакты, публикуемые в hello Azure Marketplace.  

## <a name="7----connect-your-offer-tooyour-service-sql-azure-based-or-web-service-based"></a>7.    Подключитесь к tooyour предложение службы (на основе SQL Azure или веб-службы).
Щелкните hello **Data Services** подменю.

В верхней части страницы приветствия hello запрашивается предложение hello tooprovide **пространства имен**.  

  ![рисунок](media/marketplace-publishing-data-service-creation/step-7.png)

Hello ниже вопрос будет определена как hello издатель будет вновь созданные tooexpose предложение tooAzure Marketplace. (Дополнительные сведения см. в разделе hello [руководство технической готовности к установке служб данных](marketplace-publishing-data-service-creation-prerequisites.md)).

  ![рисунок](media/marketplace-publishing-data-service-creation/step-7.2.png)

**Публикация hello служба на основе базы данных**

Щелкните **База данных**. Появится следующая страница приветствия.

  ![рисунок](media/marketplace-publishing-data-service-creation/step-7.3.png)

toocreate сопоставление языка CSDL для hello набора данных, основанный на hello базу данных SQL Azure:

  ![рисунок](media/marketplace-publishing-data-service-creation/step-7.4.png)

А затем для каждой таблицы

  ![рисунок](media/marketplace-publishing-data-service-creation/step-7.5.png)

  ![рисунок](media/marketplace-publishing-data-service-creation/step-7.6.png)

Для веб-службы укажите следующее.

  ![рисунок](media/marketplace-publishing-data-service-creation/step-7.7.png)

> [!IMPORTANT]
> Чтение [сопоставление существующего веб-службы tooOData через CSDL](marketplace-publishing-data-service-creation-odata-mapping.md) подробные инструкции и примеры для создания веб-службе языка CSDL.
> 
> 

## <a name="next-steps"></a>Дальнейшие действия
После создания службы данных предложение убедитесь, необходимо выполнить инструкции hello в hello [руководство по содержимому маркетинга Marketplace](marketplace-publishing-push-to-staging.md) перед перемещением вперед слишком[тестирование службы данных в промежуточной](marketplace-publishing-data-service-test-in-staging.md).

## <a name="see-also"></a>См. также
* [Приступая к работе: Как toopublish toohello предложение Azure Marketplace](marketplace-publishing-getting-started.md)
* Если вы заинтересованы в общее представление о hello общий процесс сопоставления OData и цели, эта статья [данных службы OData сопоставления](marketplace-publishing-data-service-creation-odata-mapping.md) tooreview определений, структуры и инструкции.
* Если вы заинтересованы в обучении и основные сведения о hello конкретных узлов и их параметров, эта статья [узлы сопоставление данных службы OData](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) для определения и объяснения, примеры и контекст вариантов использования.
* Если вы заинтересованы в просмотре примеров, эта статья [примеры сопоставление данных службы OData](marketplace-publishing-data-service-creation-odata-mapping-examples.md) toosee образцы кода и понимания синтаксиса кода и контекста.

[link-pubportal]:https://publish.windowsazure.com
