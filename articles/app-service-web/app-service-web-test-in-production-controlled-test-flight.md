---
title: "Развертывание aaaFlighting (бета-тестирования) в службе приложений Azure"
description: "Узнайте, как tooflight новые функции в приложении или бета-версии протестировать изменения в этом учебнике начала до конца. Этот режим тестирования объединяет такие функции службы приложений, как непрерывная публикация, управление слотами, маршрутизация трафика и интеграция с Application Insights."
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 17953c51-38f8-442d-bb0b-f69c1542f0e9
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/02/2016
ms.author: cephalin
ms.openlocfilehash: e83477b1fe46be09e5baa7bc2bd239b840b05cf7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="flighting-deployment-beta-testing-in-azure-app-service"></a>Развертывание в режиме фокус-тестирования (бета-тестирование) в службе приложений Azure
В этом учебнике показано как toodo *развертываний в проекте, которая должна* интегрируя hello различные функциональные возможности [службе приложений Azure](http://go.microsoft.com/fwlink/?LinkId=529714) и [Azure Application Insights](/services/application-insights/).

*Фокус-тестирование* — это процесс развертывания, в ходе которого выполняется проверка новой функции или внесенного изменения с привлечением ограниченного количества реальных клиентов. В рабочих сценариях это основной режим тестирования. Это Иванов toobeta тестирования и иногда называется «управляемой тестовой рейсов». Многие крупные предприятия, обозначившие свое веб-присутствие, используют этот подход для выполнения ранней проверки обновлений своих приложений в рамках методологии [гибкой разработки](https://en.wikipedia.org/wiki/Agile_software_development). Служба приложений Azure позволяет toointegrate тестирования в рабочей среде с непрерывной публикации и Application Insights tooimplement hello одного сценария DevOps. Этот подход отличается следующими преимуществами.

* **Получить данные реальном *перед* обновления, выпущенные tooproduction** -hello только лучше, чем получения отзывов по мере выпуска приобретает все отзывы перед выпуском. Как можно раньше в жизненном цикле продукта hello можно проверить обновления с реальными пользовательского трафика и поведения.
* **Оптимизация [непрерывной разработки на основе тестирования (CTDD)](https://en.wikipedia.org/wiki/Continuous_test-driven_development)**. Непрерывная интеграция в рабочую среду процессов тестирования и инструментирования средствами Application Insights делает возможным раннюю автоматическую проверку с привлечением пользователей, выполняемую на требуемом этапе жизненного цикла продукта. Это помогает сократить временные затраты при выполнении тестирования вручную.
* **Оптимизировать процесс тестирования** -путем автоматизации тестирования в рабочей среде с непрерывной инструментария мониторинга, можно потенциально решать hello задачи разные виды тестов в одном процессе, такие как [интеграции](https://en.wikipedia.org/wiki/Integration_testing), [регрессии](https://en.wikipedia.org/wiki/Regression_testing), [удобство использования](https://en.wikipedia.org/wiki/Usability_testing), доступность, локализации, [производительности](https://en.wikipedia.org/wiki/Software_performance_testing), [безопасности](https://en.wikipedia.org/wiki/Security_testing), и [ Принятие](https://en.wikipedia.org/wiki/Acceptance_testing).

Развертывание в режиме фокус-тестирования используется не только для маршрутизации текущего трафика. В такой среде требуется анализ toogain как можно скорее, будь непредвиденные ошибки, снижение производительности, проблемы взаимодействия пользователя. Помните: вы имеете дело с реальными пользователями. Поэтому toodo его вправо, необходимо убедиться, что вы настроили ваш flighting toogather развертывания все hello данные, необходимые в заказе toomake обоснованное решение для перехода к следующему этапу. В этом учебнике показано использование toocollect данных с помощью Application Insights, но New Relic или других технологий, подходящий для вашего сценария.

## <a name="what-you-will-do"></a>Выполняемая задача
В этом учебнике вы узнаете, как toobring hello следующие сценарии вместе tootest приложение службы приложений в рабочей среде:

* [Перенаправлять трафик рабочей](app-service-web-test-in-production-get-start.md) tooyour бета-версии приложения
* [Инструментирование приложения](../application-insights/app-insights-web-track-usage.md) tooobtain полезных метрик
* Непрерывное развертывание бета-версии приложения с отслеживанием метрик в режиме реального времени.
* Показатели сравнения между рабочее приложение hello и toosee приложения hello бета-версии, как меняется код преобразования tooresults

## <a name="what-you-will-need"></a>Необходимые условия
* Учетная запись Azure.
* Учетная запись [GitHub](https://github.com/) .
* Visual Studio 2015 — вы можете загрузить hello [Community edition](https://www.visualstudio.com/en-us/products/visual-studio-express-vs.aspx).
* Оболочка Git (устанавливается вместе с [GitHub для Windows](https://windows.github.com/))-это позволяет вам toorun обе команды Git и PowerShell hello в hello того же сеанса
* Последняя версия [Azure PowerShell](https://github.com/Azure/azure-powershell/releases/download/v0.9.8-September2015/azure-powershell.0.9.8.msi) .
* Базовое представление о hello следующее:
  * Развертывание шаблона [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) (ознакомьтесь также с разделом [Предсказуемое развертывание сложного приложения в Azure](app-service-deploy-complex-application-predictably.md)).
  * [Git.](http://git-scm.com/documentation)
  * [PowerShell](https://technet.microsoft.com/library/bb978526.aspx)

> [!NOTE]
> Требуется учетная запись Azure toocomplete этого учебника:
>
> * Вы можете [открыть учетную запись Azure бесплатно](https://azure.microsoft.com/pricing/free-trial/) -вы получаете кредиты можно использовать tootry out платных служб Azure и даже после того, они используются hello учетной записи, можно сохранить и использовать освободить служб Azure, таких как веб-приложений.
> * Вы можете [активировать преимущества подписчика Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) — каждый месяц ваша подписка Visual Studio предоставляет вам кредиты, которые можно использовать для оплаты служб Azure.
>
> Tooget работы в службе приложений Azure перед регистрацией учетную запись Azure, перейдите слишком[повторите служб приложений](https://azure.microsoft.com/try/app-service/), в котором можно немедленно создать кратковременных начальный веб-приложения в службе приложений. Никаких кредитных карт и обязательств.
>
>

## <a name="set-up-your-production-web-app"></a>Настройка рабочего веб-приложения
> [!NOTE]
> сценарий Hello, используемые в этом учебнике автоматически настраивает непрерывной публикации из репозитория GitHub. Это требует учетные данные GitHub уже были сохранены в Azure, в противном случае возникнет hello в скрипт развертывания, при попытке tooconfigure параметры системы управления версиями для веб-приложения hello.
>
> toostore GitHub учетные данные в Azure, создайте веб-приложения в hello [портала Azure](https://portal.azure.com/) и [настройки развертывания GitHub](app-service-continuous-deployment.md). Требуется только toodo этом один раз.
>
>

В типичном сценарии DevOps у вас есть приложение, которое работает в активном состоянии в Azure и требуется toomake tooit изменения в непрерывной публикации. В этом сценарии будет развернуть tooproduction шаблона, разработки и тестирования.

1. Создание собственных вилки hello [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) репозитория. Дополнительные сведения о создании разветвления см. в статье [Fork a Repo](https://help.github.com/articles/fork-a-repo/) (Разветвление репозитория). После создания разветвления его можно просматривать в браузере.

   ![](./media/app-service-agile-software-development/production-1-private-repo.png)
2. Откройте сеанс Git Shell. Если у вас нет Git Shell, установите [GitHub для Windows](https://windows.github.com/) .
3. Создайте локальный клон на разветвление, выполнив следующую команду hello:

     git clone https://github.com/<разветвление>/ToDoApp.git
4. При наличии локального клона перейдите слишком*&lt;repository_root >*\ARMTemplates и выполнения hello deploy.ps1 скрипт с уникальный суффикс, как показано ниже:

     .\deploy.ps1 –RepoUrl https://github.com/<разветвление>/todoapp.git -ResourceGroupSuffix <суффикс>
5. При появлении запроса введите hello необходимое имя пользователя и пароль для доступа к базе данных. Запомнить учетные данные базы данных, поскольку они потребуются toospecify их еще раз при обновлении hello группы ресурсов.

   Вы увидите ход выполнения различных ресурсов Azure подготовки hello. После завершения развертывания hello скрипта запустите приложение hello в браузере hello и позволяют понятное звукового сигнала.
   ![](./media/app-service-web-test-in-production-controlled-test-flight/00.1-app-in-browser.png)
6. Вернитесь в сеанс Git Shell и выполните следующую команду:

     .\swap –Name ToDoApp<суффикс>

   ![](./media/app-service-web-test-in-production-controlled-test-flight/00.2-swap-to-production.png)
7. После завершения скрипта hello, вернитесь к предыдущему окну адрес внешнего интерфейса toohello toobrowse (http://ToDoApp*&lt;your_suffix >*.azurewebsites.net/) toosee приложения hello, работающего в производственной среде.
8. Войти в hello [портала Azure](https://portal.azure.com/) Обратите внимание на то, что создается.

   После этого можно будет toosee двух веб-приложений в hello одну группу ресурсов, один из которых hello `Api` суффикса в имени hello. Если взглянуть на представление группы ресурсов hello, также появится hello базы данных SQL и сервер, hello план служб приложений и hello промежуточных слотов для hello веб-приложений. Просматривать различные ресурсы hello и сравнить их с  *&lt;repository_root >*toosee \ARMTemplates\ProdAndStage.json, как они настроены в шаблоне hello.

   ![](./media/app-service-web-test-in-production-controlled-test-flight/00.3-resource-group-view.png)

Настройки производства приложение hello.  Теперь предположим, вы получите отзыв, низка, удобство использования для приложения hello. Поэтому определить tooinvestigate. Вы собираетесь tooinstrument toogive вашего приложения вы обратной связи.

## <a name="investigate-instrument-your-client-app-for-monitoringmetrics"></a>Анализ: инструментирование клиентского приложения для мониторинга метрик
1. Откройте в Visual Studio файл *&lt;корень_репозитория>*\src\MultiChannelToDo.sln.
2. Восстановите все пакеты NuGet, щелкнув правой кнопкой мыши нужное решение и выбрав **Управление пакетами NuGet для решения** > **Восстановить**.
3. Щелкните правой кнопкой мыши **MultiChannelToDo.Web** > **добавить Телеметрию Application Insights** > **Настройка параметров** > изменить группу ресурсов tooToDoApp*&lt;your_suffix >* > **tooProject добавить Application Insights**.
4. В hello портал Azure, откройте колонку hello для hello **MultiChannelToDo.Web** Application Insight ресурсов. Затем в hello **работоспособности приложения** часть, нажмите кнопку **узнать, как страница обозревателя toocollect загрузки данных** > скопируйте код.
5. Добавить hello скопировать код инструментирования JS слишком*&lt;repository_root >*\src\MultiChannelToDo.Web\app\Index.cshtml непосредственно перед закрывающим hello `<heading>` тег. Она должна содержать ключ hello уникальный инструментирования Application Insight ресурса.

        <script type="text/javascript">
        var appInsights=window.appInsights||function(config){
            function s(config){t[config]=function(){var i=arguments;t.queue.push(function(){t[config].apply(t,i)})}}var t={config:config},r=document,f=window,e="script",o=r.createElement(e),i,u;for(o.src=config.url||"//az416426.vo.msecnd.net/scripts/a/ai.0.js",r.getElementsByTagName(e)[0].parentNode.appendChild(o),t.cookie=r.cookie,t.queue=[],i=["Event","Exception","Metric","PageView","Trace"];i.length;)s("track"+i.pop());return config.disableExceptionTracking||(i="onerror",s("_"+i),u=f[i],f[i]=function(config,r,f,e,o){var s=u&&u(config,r,f,e,o);return s!==!0&&t["_"+i](config,r,f,e,o),s}),t
        }({
            instrumentationKey:"<your_unique_instrumentation_key>"
        });

        window.appInsights=appInsights;
        appInsights.trackPageView();
        </script>
6. Отправьте tooApplication аналитики для щелчки мышью пользовательских событий, добавив следующий код toohello внизу текста hello:

       <script>
           $(document.body).find("*").click(function(event) {

               appInsights.trackEvent(event.target.tagName + ": " + event.target.className);
           });
       </script>

   Этот фрагмент JavaScript отправляет tooApplication пользовательское событие аналитики каждый раз при щелчке в любом месте в веб-приложения hello.
7. В оболочке Git зафиксируйте и отправьте на разветвление tooyour изменения в GitHub. Дождитесь, пока клиенты toorefresh браузера.

       git add -A :/
       git commit -m "add AI configuration for client app"
       git push origin master
8. Поменяйте tooproduction изменения приложения hello развертывания:

     .\swap –Name ToDoApp<суффикс>
9. Обзор toohello Application Insights ресурс, который можно настроить. Щелкните «Настраиваемые события».

   ![](./media/app-service-web-test-in-production-controlled-test-flight/01-custom-events.png)

   Если вы не видите метрик, характеризующих пользовательские события, подождите несколько минут и щелкните **Обновить**.

Предположим, что вы видите диаграмму, похожую на представленную ниже:

![](./media/app-service-web-test-in-production-controlled-test-flight/02-custom-events-chart-view.png)

И сетки событий hello под ней:

![](./media/app-service-web-test-in-production-controlled-test-flight/03-custom-event-grid-view.png)

Здравствуйте, в соответствии с кодом приложения ToDoApp tooyour, **кнопку** событие соответствует toohello кнопку "Отправить" и hello **ввода** событие соответствует toohello текстовое поле. С этим все понятно. Однако, похоже, имеется достаточно большой объем щелчками мышью и очень мало щелчков мыши на элементы задача hello (hello **LI** событий).

На основе этого, вы формы предположение, некоторым пользователям не путать hello какой части пользовательского интерфейса являются интерактивными и тем, что курсор hello реализуется для выделения текста, при его наведении на элементы списка hello и соответствующие значки.

![](./media/app-service-web-test-in-production-controlled-test-flight/04-to-do-list-item-ui.png)

Этот пример может выглядеть несколько надуманным. Тем не менее вы будете toomake текущее приложение tooyour улучшения, а затем выполните flighting отзыв удобство использования tooget развертывания от динамической клиентов.

### <a name="instrument-your-server-app-for-monitoringmetrics"></a>Инструментирование серверного приложения для получения метрик и для мониторинга
Это касательной, поскольку сценарий hello, демонстрируются в данном учебнике рассматриваются только hello клиентского приложения. Тем не менее для обеспечения полноты вы настроите серверное приложение hello.

1. Щелкните правой кнопкой мыши **MultiChannelToDo** > **добавить Телеметрию Application Insights** > **Настройка параметров** > изменить группу ресурсов tooToDoApp*&lt;your_suffix >* > **tooProject добавить Application Insights**.
2. В оболочке Git зафиксируйте и отправьте на разветвление tooyour изменения в GitHub. Дождитесь, пока клиенты toorefresh браузера.

       git add -A :/
       git commit -m "add AI configuration for server app"
       git push origin master
3. Поменяйте tooproduction изменения приложения hello развертывания:

     .\swap –Name ToDoApp<суффикс>

Вот и все!

## <a name="investigate-add-slot-specific-tags-tooyour-client-app-metrics"></a>Изучить: Добавление слота специальные теги tooyour клиентского приложения метрик
В этом разделе вы настроите hello развертывания слоты toosend телеметрии конкретного слот toohello того же ресурса Application Insights. Таким образом, можно сравнить телеметрии данных между трафик от tooeasily различных слотов (сред развертывания). в статье hello влияние изменения приложения. AT hello же времени, можно отделить hello рабочего трафика от hello rest, чтобы продолжить toomonitor на рабочее приложение при необходимости.

Так как при сборе данных на поведение клиента будет [добавить tooyour инициализатора телеметрии код JavaScript](../application-insights/app-insights-api-filtering-sampling.md) в index.cshtml. Если вы хотите tootest производительности на стороне сервера, например, аналогичную процедуру можно также выполнить в коде сервера (в разделе [Application Insights API пользовательские события и метрики](../application-insights/app-insights-api-custom-events-metrics.md).

1. Сначала добавьте hello bewteen кода hello двух `//` комментарии ниже в блоке hello JavaScript, которые добавлены toohello `<heading>` тег ранее.

        window.appInsights = appInsights;

        // Begin new code
        appInsights.queue.push(function () {
            appInsights.context.addTelemetryInitializer(function (envelope) {
                var telemetryItem = envelope.data.baseData;
                telemetryItem.properties = telemetryItem.properties || {};
                telemetryItem.properties["Environment"] = "@System.Configuration.ConfigurationManager.AppSettings["environment"]";
            });
        });
        // End new code

        appInsights.trackPageView();

    Этот код инициализатор вызывает hello `appInsights` настраиваемое свойство hello объекта tooadd `Environment` tooevery часть отправляет данные телеметрии.
2. Затем добавьте это пользовательское свойство как [параметр слота](web-sites-staged-publishing.md#AboutConfiguration) для веб-приложения Azure. toodo, выполнения hello, следующие команды в сеансе оболочки Git.

        $app = Get-AzureWebsite -Name todoapp<your_suffix> -Slot production
        $app.AppSettings.Add("environment", "Production")
        $app.SlotStickyAppSettingNames.Add("environment")
        $app | Set-AzureWebsite -Name todoapp<your_suffix> -Slot production

    Hello Web.config в проекте уже имеется определение hello `environment` параметра приложения. Этот параметр при тестировании локально, приложение hello показатели будут тегом `VS Debugger`. Однако при выполнении отправки к tooAzure изменения, Azure будет найти и использовать hello `environment` приложения, вместо этого параметра в конфигурации веб-приложения hello и показатели будут тегом `Production`.
3. Фиксация и нажать на разветвление tooyour изменения кода на GitHub и ожидание пользователей toouse hello нового приложения (требуется toorefresh hello браузер). Он занимает около 15 минут для нового свойства tooshow hello в вашей Application Insights `MultiChannelToDo.Web` ресурсов.

        git add -A :/
        git commit -m "add environment property tooAI events for client app"
        git push origin master
4. Теперь перейдите toohello **пользовательские события** снова колонки и фильтр hello метрики на `Environment=Production`. Теперь должен быть доступ toosee hello новые пользовательские события в рабочей среде hello слот с данным фильтром.

    ![](./media/app-service-web-test-in-production-controlled-test-flight/05-filter-on-production-environment.png)
5. Нажмите кнопку hello **Избранное** как кнопка toosave hello текущего обозревателя метрик параметры toosomething **пользовательские события: рабочей**. Позже вы сможете легко переключаться между этим представлением и представлением слота развертывания.

   > [!TIP]
   > Если вам нужны более мощные средства аналитики, рассмотрите возможность [интеграции ресурса Application Insights с Power BI](../application-insights/app-insights-export-power-bi.md).
   >
   >

### <a name="add-slot-specific-tags-tooyour-server-app-metrics"></a>Добавить метрики приложений гнездо специальные теги tooyour сервера
Опять же для обеспечения полноты вы настроите серверное приложение hello. В отличие от клиентского приложения hello которой инструментированы на языке JavaScript слот специальные теги для серверного приложения hello снабжается кода .NET.

1. Откройте файл *&lt;корень_репозитория>*\src\MultiChannelToDo\Global.asax.cs. Добавьте блок кода hello ниже, перед закрывающей фигурной скобки имен hello.

        namespace MultiChannelToDo
        {
                ...

                // Begin new code
            public class ConfigInitializer
            : ITelemetryInitializer
            {
                void ITelemetryInitializer.Initialize(ITelemetry telemetry)
                {
                    telemetry.Context.Properties["Environment"] = System.Configuration.ConfigurationManager.AppSettings["environment"];
                }
            }
                // End new code
        }
2. Исправьте ошибки разрешения имен hello, добавив hello `using` инструкции ниже toohello начало hello файла:

        using Microsoft.ApplicationInsights.Channel;
        using Microsoft.ApplicationInsights.Extensibility;
3. Добавьте код hello под toohello начало hello `Application_Start()` метод:

        TelemetryConfiguration.Active.TelemetryInitializers.Add(new ConfigInitializer());
4. Фиксация и нажать на разветвление tooyour изменения кода на GitHub и ожидание пользователей toouse hello нового приложения (требуется toorefresh hello браузер). Он занимает около 15 минут для нового свойства tooshow hello в вашей Application Insights `MultiChannelToDo` ресурсов.

        git add -A :/
        git commit -m "add environment property tooAI events for server app"
        git push origin master

## <a name="update-set-up-your-beta-branch"></a>Обновление: настройка ветви бета-версии
1. Откройте  *&lt;repository_root >*\ARMTemplates\ProdAndStagetest.json и найти hello `appsettings` ресурсы (поиск `"name": "appsettings"`). Существует 4 таких ресурса, по одному для каждого слота.
2. Для каждого `appsettings` ресурса, добавление `"environment": "[parameters('slotName')]"` приложения параметр toohello конец hello `properties` массива. Не забывайте tooend hello предыдущей строки с помощью символа запятой.

    ![](./media/app-service-web-test-in-production-controlled-test-flight/06-arm-app-setting-with-slot-name.png)

    Вы только что добавили hello `environment` параметр tooall слоты hello в шаблоне hello приложения.
3. В hello того же файла, найти hello `slotconfignames` ресурсы (поиск `"name": "slotconfignames"`). Существует 2 таких ресурса, по одному для каждого приложения.
4. Для каждого `slotconfignames` ресурса, добавление `"environment"` toohello конец hello `appSettingNames` массива. Не забывайте tooend hello предыдущей строки с помощью символа запятой.

    Только что внесенные hello `environment` приложения параметр манипулятор tooits соответствующих слот развернутого приложения для обоих приложений.  
5. В сеансе оболочки Git следующие hello выполнения команды с помощью hello же суффикс группы ресурсов, который использовался ранее.

        git checkout -b beta
        git push origin beta
        .\deploy.ps1 -RepoUrl https://github.com/<your_fork>/ToDoApp.git -ResourceGroupSuffix <your_suffix> -SlotName beta -Branch beta
6. При появлении запроса укажите hello же учетные данные базы данных SQL, как и раньше. Затем, ответ на вопрос о группе ресурсов hello tooupdate, тип `Y`, затем `ENTER`.

    После завершения скрипта hello, сохраняются все ресурсы в группе ресурсов исходного hello, но новый слот с именем «бета» создания в ней с hello же конфигурацию, что и слот «Staging» hello, созданный в начале hello.

   > [!NOTE]
   > Этот метод создания сред развертывания отличается от метода hello в [гибкой разработки программного обеспечения с помощью службы приложения Azure](app-service-agile-software-development.md). Он предполагает создание сред развертывания со слотами развертывания — как если бы вы создавали среды развертывания с группами ресурсов. Управление средами развертывания с группами ресурсов позволяет off-limits toodevelopers tookeep hello рабочей среды, но это не просто toodo тестирования в рабочей среде, в которой можно легко сделать с помощью слотов.
   >
   >

При желании вы можете создать альфа-версию приложения, запустив следующий код:

    git checkout -b alpha
    git push origin alpha
    .\deploy.ps1 -RepoUrl https://github.com/<your_fork>/ToDoApp.git -ResourceGroupSuffix <your_suffix> -SlotName beta -Branch alpha

Этот учебник предполагает использование бета-версии приложения.

## <a name="update-push-your-updates-toohello-beta-app"></a>Обновление: Push toohello бета-версии обновления приложения
Назад tooyour приложения, которые должны tooimprove.

1. Убедитесь, что вы находитесь в ветке бета-версии.

        git checkout beta
2. В  *&lt;repository_root >*\src\MultiChannelToDo.Web\app\Index.cshtml, найти hello `<li>` теги и добавить hello `style="cursor:pointer"` атрибута, как показано ниже.

    ![](./media/app-service-web-test-in-production-controlled-test-flight/07-change-cursor-style-on-li.png)
3. Зафиксируйте и отправьте tooAzure.
4. Убедитесь, что изменение hello теперь отражается в слот hello бета-версии, перейдя по toohttp://todoapp*&lt;your_suffix >*-beta.azurewebsites.net/. Если вы не видите hello изменение еще не, обновите браузер tooget hello новый код javascript.

    ![](./media/app-service-web-test-in-production-controlled-test-flight/08-verify-change-in-beta-site.png)

Теперь, у вас есть изменения в слот hello бета-версии, все готово tooperform flighting развертывания.

## <a name="validate-route-traffic-toohello-beta-app"></a>Проверка: Приложение бета-версии toohello маршрутизации трафика
В этом разделе будет направлять трафик toohello бета-версии приложения. Для ясности демонстрации ты tooroute значительную часть трафика tooit hello пользователя. На самом деле hello объем трафика, который вы хотите tooroute будет зависеть от конкретной ситуации. Например если веб-сайт будет в масштабе hello объекта microsoft.com, может потребоваться меньше 1% всего трафика в порядке toogain полезных данных.

1. В сеансе оболочки Git выполните следующие команды tooroute hello половины hello производственный трафика toohello бета-версии слот:

        $siteName = "ToDoApp<your suffix>"
        $rule = New-Object Microsoft.WindowsAzure.Commands.Utilities.Websites.Services.WebEntities.RampUpRule
        $rule.ActionHostName = "$siteName-beta.azurewebsites.net"
        $rule.ReroutePercentage = 50
        $rule.Name = "beta"
        Set-AzureWebsite $siteName -Slot Production -RoutingRules $rule

   Hello `ReroutePercentage=50` свойство указывает, 50% от рабочего трафика hello URL-адреса перенаправленное toohello бета-версии приложения (определяемое hello `ActionHostName` свойство).
2. Теперь перейдите toohttp://ToDoApp*&lt;your_suffix >*. azurewebsites.net. 50% от трафика hello, теперь будет слот перенаправленный toohello бета-версии.
3. В ресурс Application Insights, отфильтровать показатели hello средой = «бета».

   > [!NOTE]
   > При сохранении этого отфильтрованное представление другой список избранного, можно легко отразить представления обозревателя метрик hello между производства и бета-версии представления.
   >
   >

Предположим, что в Application Insights вы видите что-нибудь подобное toohello следующее:

![](./media/app-service-web-test-in-production-controlled-test-flight/09-test-beta-site-in-production.png)

Не является это отображаются только что существует множество дополнительных переходов по hello `<li>` теги, но похоже, что toobe Наплыв щелчков мыши на `<li>` тегов. Затем можно заключить, что люди обнаружены новые hello `<li>` теги являются интерактивными и теперь очищаемой все их ранее выполненные задачи в приложение hello.

На основании данных hello flighting развертывания вы решите, новый пользовательский Интерфейс будет готов для рабочей среды.

## <a name="go-live-move-your-new-code-into-production"></a>Ввод в эксплуатацию: перенос нового кода в рабочую среду
Вы являетесь toomove теперь все готово к tooproduction обновления. Значительные является, теперь вы знаете, что обновление уже были проверены *перед* отправлена tooproduction. Теперь его можно с уверенностью развернуть. С момента внесения клиентского приложения AngularJS toohello обновления вы только проверить код на стороне клиента hello. Если toomake изменения toohello серверной части веб-API приложения, легко и точно так же можно проверить внесенные изменения.

1. В оболочке Git удалите правило маршрутизации трафика hello, выполнив hello следующую команду:

        Set-AzureWebsite $siteName -Slot Production -RoutingRules @()
2. Выполните команды Git hello.

        git checkout master
        git pull origin master
        git merge beta
        git push origin master
3. Подождите, пока в течение нескольких минут hello новые закодировать промежуточных слотах toohello toobe развертывания, а затем запустите http://ToDoApp*&lt;your_suffix >*-активированию tooverify staging.azurewebsites.net, hello нового обновления в промежуточной hello разъем. Помните, hello главную ветвь на разветвление является связанной toohello промежуточной области памяти приложения.
4. Теперь замены hello промежуточного слота в рабочей среде

        cd <ROOT>\ToDoApp\ARMTemplates
        .\swap.ps1 -Name todoapp<your_suffix>

## <a name="summary"></a>Сводка
Служба приложений Azure упрощает для предприятий малого размера toomedium tootest свои приложения с клиентом в рабочей среде, что-нибудь, традиционно выполнялась в больших организациях. Надеюсь, этого учебника вы получили hello знания, необходимые в вашей среде DevOps toobring вместе приложения службы и Application Insights toomake возможных проекте, которая должна развертывания и даже другие сценарии в тестовой.

## <a name="more-resources"></a>Дополнительные ресурсы
* [Гибкая разработка программного обеспечения с помощью службы приложений Azure.](app-service-agile-software-development.md)
* [Настройка промежуточных сред для веб-приложений в службе приложений Azure](web-sites-staged-publishing.md)
* [Предсказуемое развертывание сложного приложения в Azure](app-service-deploy-complex-application-predictably.md)
* [Создание шаблонов диспетчера ресурсов Azure](../azure-resource-manager/resource-group-authoring-templates.md)
* [JSONLint - hello JSON проверяющий элемент управления](http://jsonlint.com/)
* [Ветвление Git — основные ветвления и слияния](http://www.git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging)
* [Azure PowerShell](/powershell/azure/overview)
* [Вики-сайт проекта Kudu](https://github.com/projectkudu/kudu/wiki)
