---
title: "aaaGet к выполнению тестов в рабочей среде для веб-приложений"
description: "Дополнительные сведения о hello тестирования в рабочей среде (TiP) функция в веб-приложениях службы приложений Azure."
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 4623468d-886e-4203-8012-8f86deb2790b
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/13/2016
ms.author: cephalin
ms.openlocfilehash: 2ddbd532ffe2a4f3e07fd386d9741a3fde3639ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-test-in-production-for-web-apps"></a>Введение в тестирование веб-приложений в рабочей среде
Тестирование в рабочей среде или тестирование веб-приложения с использованием текущего пользовательского трафика является популярной стратегией тестирования, которую разработчики приложений широко интегрируют в методологию [гибкой разработки](https://en.wikipedia.org/wiki/Agile_software_development). Благодаря этому можно tootest hello качества приложений с динамической пользовательский трафик в рабочей среде, в противоположность toosynthesized данных в тестовой среде. Путем предоставления доступа к новым пользователям tooreal приложения, могут получать уведомления на hello серьезные проблемы, которые могут возникнуть приложения после его развертывания. Можно проверить функциональные возможности hello, производительность и обновления приложения от hello тома, скорости и разнообразных трафик реальному пользователю, который никогда не может получить приблизительный в тестовой среде.

## <a name="traffic-routing-in-app-service-web-apps"></a>Маршрутизация трафика в веб-приложениях службы приложений
С hello маршрутизации трафика, входящего в [службе приложений Azure](http://go.microsoft.com/fwlink/?LinkId=529714), можно направить часть tooone трафик динамической пользователя или более [слоты развертывания](web-sites-staged-publishing.md)и затем анализ приложения с [приложения Azure Аналитики](/services/application-insights/) или [Azure HDInsight](/services/hdinsight/), или стороннего средства, такие как [New Relic](/marketplace/partners/newrelic/newrelic/) toovalidate внесенные изменения. Например можно реализовать следующие сценарии с службой приложения hello.

* Обнаружение ошибок работы или выявить узкие места производительности в развертывании обновлений предыдущего уровня toosite
* Выполнить «управляемой тестовой рейсов» изменений путем измерения метрики удобства использования на приложение hello бета-версии
* Постепенно освоить tooa новым обновлением и корректно обратно вниз toohello текущей версии, при возникновении ошибки 
* Оптимизация результатов бизнес-приложения путем выполнения [альфа- и бета-тестирования](https://en.wikipedia.org/wiki/A/B_testing) или [многовариантного тестирования](https://en.wikipedia.org/wiki/Multivariate_testing_in_marketing) в нескольких слотах развертывания.

### <a name="requirements-for-using-traffic-routing-in-web-apps"></a>Требования для использования маршрутизации трафика в веб-приложениях
* Веб-приложение должно выполняться в категории **Стандартный** или **Премиум**, так как это требуется для нескольких слотов развертывания.
* В порядке toowork надлежащим образом, для маршрутизации трафика требуется toobe файлы Cookie включены в браузере hello пользователей. Маршрутизации трафика использует файлы cookie toopin слота развертывания tooa браузера клиента для сеанса клиента hello жизни hello.
* Маршрутизация трафика поддерживает расширенные сценарии тестирования в рабочей среде с использованием командлетов Azure PowerShell.

## <a name="route-traffic-segment-tooa-deployment-slot"></a>Слот развертывания tooa сегмент трафик маршрута
На уровне basic hello в каждом сценарии TiP маршрутизацию стандартному проценту от ваш слот развертывания нерабочей tooa трафик динамической. toodo это, выполните hello шаги:

> [!NOTE]
> Hello при выполнении шагов предполагается, что уже [слот развертывания нерабочей](web-sites-staged-publishing.md) и что hello требуемого приложения веб-содержимого уже [развертывания](web-sites-deploy.md) tooit.
> 
> 

1. Войти в hello [портала Azure](https://portal.azure.com/).
2. В колонке веб-приложения щелкните **Параметры** > **Маршрутизация трафика**.
   ![](./media/app-service-web-test-in-production/01-traffic-routing.png)
3. Выберите hello слот, где требуется tooroute tooand трафика hello процент hello всего трафика, вам нужен, а затем нажмите кнопку **Сохранить**.
   
    ![](./media/app-service-web-test-in-production/02-select-slot.png)
4. Перейдите в колонку слот развертывания toohello. Теперь вы увидите, перенаправленное tooit трафик динамической.
   
    ![](./media/app-service-web-test-in-production/03-traffic-routed.png)

После настройки маршрутизации трафика hello указанный процент клиентов будет случайным образом перенаправленное tooyour не производственный слот. Однако это важно toonote, что после клиент автоматически перенаправленное tooa конкретных слот, она будет слот «закрепленные» toothat hello время жизни сеанса клиента. Это сделано с помощью сеанса пользователя hello toopin куки-файл. Проверить, hello HTTP-запросов, вы обнаружите `TipMix` каждый последующий запрос в файле cookie.

![](./media/app-service-web-test-in-production/04-tip-cookie.png)

## <a name="force-client-requests-tooa-specific-slot"></a>Принудительно слот конкретных tooa запросы клиента
В добавление tooautomatic для маршрутизации трафика, службы приложений является может tooroute запросов tooa конкретных слота. Это полезно при необходимости вашей может tooopt toobe пользователи — в или отказаться от бета-версии приложения. toodo это, используйте hello `x-ms-routing-name` параметр запроса.

tooreroute пользователи tooa конкретных слот с помощью `x-ms-routing-name`, необходимо проверить этот слот hello уже добавлен в список маршрутизации трафика toohello. Поскольку слот tooa tooroute необходимо явным образом, hello фактическое маршрутизации процентное соотношение задать не имеет значения. Если требуется, можно создать «бета-версии ссылку», пользователи могут щелкнуть tooaccess hello бета-версии приложения.

![](./media/app-service-web-test-in-production/06-enable-x-ms-routing-name.png)

### <a name="opt-users-out-of-beta-app"></a>Отказ пользователей от использования бета-версии приложения
Пользователи toolet отказаться от бета-версии приложения, например, можно поместить эту ссылку на веб-странице:

    <a href="<webappname>.azurewebsites.net/?x-ms-routing-name=self">Go back tooproduction app</a>

Здравствуйте, строка `x-ms-routing-name=self` указывает hello производственный слот. После hello hello ссылки доступа к браузера клиента, не только его перенаправлено toohello производственный слот, но каждый последующий запрос будет содержать hello `x-ms-routing-name=self` файл cookie, который фиксирует hello сеанса toohello производственный слот.

![](./media/app-service-web-test-in-production/05-access-production-slot.png)

### <a name="opt-users-in-toobeta-app"></a>Выбрать пользователей в приложении toobeta
Пользователи toolet согласие tooyour бета-версии приложения, набора hello же запрос имени параметра toohello слота нерабочей hello, например:

        <webappname>.azurewebsites.net/?x-ms-routing-name=staging

## <a name="more-resources"></a>Дополнительные ресурсы
* [Настройка промежуточных сред для веб-приложений в службе приложений Azure](web-sites-staged-publishing.md)
* [Предсказуемое развертывание сложного приложения в Azure](app-service-deploy-complex-application-predictably.md)
* [Гибкая разработка программного обеспечения с помощью службы приложений Azure.](app-service-agile-software-development.md)
* [Эффективное использование сред разработки и операций для веб-приложений](app-service-web-staged-publishing-realworld-scenarios.md)

