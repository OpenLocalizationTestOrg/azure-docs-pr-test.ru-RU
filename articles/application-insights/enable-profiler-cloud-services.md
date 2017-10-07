---
title: "aaaEnable профилировщик аналитики приложений Azure для ресурса облачные службы | Документы Microsoft"
description: "Узнайте, как tooset копию профилировщика hello в приложении ASP.NET, расположенных на ресурс облачных служб Azure."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: bwren
ms.openlocfilehash: b9ac3bca513bf4518f44780389a9f2945f6ccc98
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="enable-application-insights-profiler-on-an-azure-cloud-services-resource"></a>Включение Azure Application Insights Profiler в ресурсе облачных служб

В этом пошаговом руководстве показано, как tooenable профилировщик аналитики приложений Azure в приложении ASP.NET, размещенных по ресурсам облачных служб Azure. Примеры Hello включают поддержку виртуальных машин Azure, наборы масштабирования виртуальных машин и Azure Service Fabric. Все примеры Hello полагаться на шаблоны, которые поддерживают hello модели развертывания диспетчера ресурсов Azure. Дополнительные сведения о модели развертывания hello [диспетчера ресурсов Azure и классическое развертывание: Обзор модели развертывания и hello состояния ресурсов](/azure-resource-manager/resource-manager-deployment-model).

## <a name="overview"></a>Обзор

Следующая схема Hello показано, как профилировщик hello работает для облачных служб Azure ресурсов. Виртуальная машина Azure используется в качестве примера.

![Общие сведения о](./media/enable-profiler-compute/overview.png) toocollect сведения для обработки и отображения на Здравствуйте портал Azure, необходимо установить компонент диагностики агента hello ресурсов hello облачных служб Azure. Hello остальной части hello Пошаговое руководство предоставляет инструкции по tooinstall и настройте агент диагностики hello tooenable профилировщик аналитики приложений.

## <a name="prerequisites-for-hello-walkthrough"></a>Необходимые условия для пошагового руководства hello

* Шаблон развертывания диспетчера ресурсов, устанавливает hello профилировщик агенты на hello виртуальных машин ([WindowsVirtualMachine.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachine.json)) или масштабирования наборы ([WindowsVirtualMachineScaleSet.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachineScaleSet.json)).

* Экземпляр Application Insights, включенный для профилирования. Инструкции см. в разделе [включить профиль hello](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-profiler#enable-the-profiler).

* .NET framework 4.6.1 или более поздней версии, установленный на hello целевой ресурс облачных служб Azure.

## <a name="create-a-resource-group-in-your-azure-subscription"></a>Создание группы ресурсов в подписке Azure
Hello в следующем примере показано, как группировать toocreate ресурса с помощью сценария PowerShell:

```
New-AzureRmResourceGroup -Name "Replace_With_Resource_Group_Name" -Location "Replace_With_Resource_Group_Location"
```

## <a name="create-an-application-insights-resource-in-hello-resource-group"></a>Создание ресурса Application Insights в группе ресурсов hello
На hello **Application Insights** колонке введите hello сведения для ресурса, как показано в следующем примере: 

![Колонка Application Insights](./media/enable-profiler-compute/createai.png)

## <a name="apply-an-application-insights-instrumentation-key-in-hello-azure-resource-manager-template"></a>Применить ключ инструментирования Application Insights в шаблоне hello диспетчера ресурсов Azure

1. Если еще не был загружен шаблон hello, загрузите его из [GitHub](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachine.json).

2. Поиск ключа Application Insights hello.
   
   ![Расположение ключа hello](./media/enable-profiler-compute/copyaikey.png)

3. Замените значение шаблона hello.
   
   ![Значение, замененное в шаблоне hello](./media/enable-profiler-compute/copyaikeytotemplate.png)

## <a name="create-an-azure-vm-toohost-hello-web-application"></a>Создать веб-приложение hello toohost ВМ Azure
1. Создайте пароль hello toosave защищенной строки.

   ```
   $password = ConvertTo-SecureString -String "Replace_With_Your_Password" -AsPlainText -Force
   ```

2. Развертывание шаблона диспетчера ресурсов Azure hello.

   Измените каталог hello в папке toohello консоли PowerShell hello, содержащего шаблон диспетчера ресурсов. toodeploy шаблон hello, запустите hello следующую команду:

   ```
   New-AzureRmResourceGroupDeployment -ResourceGroupName "Replace_With_Resource_Group_Name" -TemplateFile .\WindowsVirtualMachine.json -adminUsername "Replace_With_your_user_name" -adminPassword $password -dnsNameForPublicIP "Replace_WIth_your_DNS_Name" -Verbose
   ```

После успешного выполнения сценария hello, вы должны найти Виртуальную машину с именем **MyWindowsVM** в группе ресурсов.

## <a name="configure-web-deploy-on-hello-vm"></a>Настройка веб-развертывания на hello виртуальной Машины
Убедитесь, что на виртуальной машине включено веб-развертывание, чтобы вы могли публиковать веб-приложения из Visual Studio.

см. веб-развертывания на виртуальной Машине вручную через WebPI, tooinstall [Установка и настройка веб-развертывания на IIS 8.0 и более поздней версии](https://docs.microsoft.com/en-us/iis/install/installing-publishing-technologies/installing-and-configuring-web-deploy-on-iis-80-or-later). Пример того, как tooautomate Установка веб-развертывания с помощью шаблона диспетчера ресурсов Azure, см. [создание, Настройка и развертывание tooan приложения web виртуальной Машины Azure](https://azure.microsoft.com/en-us/resources/templates/201-web-app-vm-dsc/).

При развертывании приложения ASP.NET MVC go tooServer Manager выберите **Добавить роли и компоненты** > **веб-сервер (IIS)** > **веб-сервере**  >  **Разработки приложений**и включите ASP.NET 4.5 на сервере.

![Добавление ASP.NET](./media/enable-profiler-compute/addaspnet45.png)

## <a name="install-hello-azure-application-insights-sdk-for-your-project"></a>Установка hello Azure пакет SDK Application Insights для проекта
1. Откройте веб-приложение ASP.NET в Visual Studio.

2. Щелкните правой кнопкой мыши проект hello и выберите **добавить** > **подключенные службы**.

3. Выберите **Application Insights**.

4. Выполните инструкции hello на странице приветствия. Выберите ресурс Application Insights hello, которое было создано ранее.

5. Выберите hello **зарегистрировать** кнопки.


## <a name="publish-hello-project-tooan-azure-vm"></a>Публикация проекта hello tooan ВМ Azure
Существует несколько способов toopublish tooan приложение виртуальной Машины Azure. Один из способов — toouse Visual Studio 2017 г.

1. Щелкните правой кнопкой мыши проект hello и выберите **публикации**.

2. Выберите **виртуальные машины Microsoft Azure** как hello публикации целевой и выполните действия hello.

   ![Публикация из Visual Studio](./media/enable-profiler-compute/publishtoVM.png)

3. Запустите нагрузочный тест для вашего приложения. Вы увидите результаты на hello Application Insights экземпляр портала веб-странице.


## <a name="enable-hello-profiler"></a>Включить профилировщик hello
1. Перейти в tooyour Application Insights **производительности** и выберите **Настройка**.
   
   ![Значок настройки](./media/enable-profiler-compute/enableprofiler1.png)
 
2. Выберите **Включить профилировщик**.
   
   ![Значок включения профилировщика](./media/enable-profiler-compute/enableprofiler2.png)

## <a name="add-a-performance-test-tooyour-application"></a>Добавление приложения tooyour теста производительности
Поэтому корпорация Майкрософт могла собрать некоторые toobe образец данных, отображаемых в профилировщик аналитики приложений, выполните следующие действия.

1. Выберите ресурс Application Insights toohello, которое было создано ранее. 

2. Go toohello **доступности** колонки и добавить тест производительности, который отправляет запросы tooyour приложения URL-адрес. 

   ![Добавление теста производительности](./media/enable-profiler-compute/AvailabilityTest.png)

## <a name="view-your-performance-data"></a>Просмотр данных о производительности

1. Подождите 10 – 15 минут для toocollect профилировщик hello и анализировать данные hello. 

2. Go toohello **производительности** колонки в ресурс Application Insights и представления, как выполнение приложения, когда он находится под высокой нагрузкой.

   ![Просмотр данных производительности](./media/enable-profiler-compute/aiperformance.png)

3. Выберите hello рядом с заголовком **примеры** tooopen hello **представление трассировки** колонку.

   ![Открыв колонку hello представления трассировки](./media/enable-profiler-compute/traceview.png)


## <a name="work-with-an-existing-template"></a>Работа с имеющимся шаблоном

1. Найдите объявление ресурса hello диагностики Azure в шаблон развертывания.
   
   Если у вас нет объявление, можно создать один похожа на объявление hello в следующий пример hello. Можно обновить шаблон hello из hello [обозревателя ресурсов Azure веб-сайт](https://resources.azure.com).

2. Издатель hello изменений из `Microsoft.Azure.Diagnostics` слишком`AIP.Diagnostics.Test`.

3. Для `typeHandlerVersion` используйте `0.0`.

4. Убедитесь, что `autoUpgradeMinorVersion` задано слишком`true`.

5. Добавить новый hello `ApplicationInsightsProfiler` приемник экземпляра в hello `WadCfg` объект параметров, как показано в следующий пример hello:

```
"resources": [
        {
          "type": "extensions",
          "name": "Microsoft.Insights.VMDiagnosticsSettings",
          "apiVersion": "2016-03-30",
          "properties": {
            "publisher": "AIP.Diagnostics.Test",
            "type": "IaaSDiagnostics",
            "typeHandlerVersion": "0.0",
            "autoUpgradeMinorVersion": true,
            "settings": {
              "WadCfg": {
                "SinksConfig": {
                  "Sink": [
                    {
                      "name": "Give a descriptive short name. E.g.: MyApplicationInsightsProfilerSink",
                      "ApplicationInsightsProfiler": "Enter hello Application Insights instance instrumentation key guid here"
                    }
                  ]
                },
                "DiagnosticMonitorConfiguration": {
                    ...
                }
                ...
              }
              ...
            }
            ...
          }
          ...
]
```

## <a name="enable-hello-profiler-on-virtual-machine-scale-sets"></a>Включить профилировщик hello на наборы масштабирования виртуальных машин
toosee tooenable hello профилировщика, загрузите hello [WindowsVirtualMachineScaleSet.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachineScaleSet.json) шаблона. Примените hello же изменения в ресурс виртуальной Машины шаблон toohello диагностики расширения для набора масштабирования виртуальных машин hello.

Каждый экземпляр в наборе масштабирования hello оставалось toohello доступа к Интернету. Hello агента профилировщик может передать hello собранные образцы tooApplication аналитики для отображения и анализа.

## <a name="enable-hello-profiler-on-service-fabric-applications"></a>Включить профилировщик hello на приложения Service Fabric
1. Подготовка к работе hello Service Fabric кластера toohave hello Azure Diagnostics расширение, которое устанавливает hello профилировщик агента.

2. Установка пакета SDK Application Insights hello в проекте hello и настройке ключа Application Insights hello.

3. Добавьте телеметрии tooinstrument кода приложения.

### <a name="provision-hello-service-fabric-cluster-toohave-hello-azure-diagnostics-extension-that-installs-hello-profiler-agent"></a>Toohave кластера hello расширение диагностики Azure, которое устанавливает hello профилировщик агента для подготовки hello Service Fabric
Кластер Service Fabric может быть безопасным или небезопасным. Можно установить один toobe кластера шлюза не является безопасной, сертификат не требуется для доступа. Кластеры, содержащие бизнес-логику и данные, должны быть безопасными. Вы можете включить профилировщик hello на безопасные и небезопасные кластеров Service Fabric. В этом пошаговом руководстве используется кластер небезопасные как пример tooexplain изменений, необходимых tooenable hello профилировщика. Можно подготовить безопасного кластера в hello таким же образом.

1. Загрузите [ServiceFabricCluster.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/ServiceFabricCluster.json). Замените `Application_Insights_Key` своим ключом Application Insights так же, как для виртуальных машин и масштабируемых наборов виртуальных машин:

   ```
   "publisher": "AIP.Diagnostics.Test",
                 "settings": {
                   "WadCfg": {
                     "SinksConfig": {
                       "Sink": [
                         {
                           "name": "MyApplicationInsightsProfilerSinkVMSS",
                           "ApplicationInsightsProfiler": "[Application_Insights_Key]"
                         }
                       ]
                     },
   ```

2. Развертывание hello шаблона с помощью сценария PowerShell:

   ```
   Login-AzureRmAccount
   New-AzureRmResourceGroup -Name [Your_Resource_Group_Name] -Location [Your_Resource_Group_Location] -Verbose -Force
   New-AzureRmResourceGroupDeployment -Name [Choose_An_Arbitrary_Name] -ResourceGroupName [Your_Resource_Group_Name] -TemplateFile [Path_To_Your_Template]

   ```

### <a name="install-hello-application-insights-sdk-in-hello-project-and-configure-hello-application-insights-key"></a>Установка пакета SDK Application Insights hello в проекте hello и настройке ключа Application Insights hello
Установите пакет SDK Application Insights hello из hello [пакет NuGet](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/). Убедитесь, что устанавливается стабильная версия 2.3 или более поздняя. 

Сведения о настройке Application Insights в проектах см. в статье [Using Service Fabric with Application Insights](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/blob/dev/appinsights/ApplicationInsights.md) (Использование Service Fabric с Application Insights).

### <a name="add-application-code-tooinstrument-telemetry"></a>Добавить телеметрии tooinstrument кода приложения
1. Для любого фрагмента кода, которые должны tooinstrument добавить с помощью инструкции вокруг нее. 

   В следующем примере hello, hello `RunAsync` метод выполняет некоторые действия и hello `telemetryClient` класс регистрирует данные телеметрии hello после ее запуска. событие Hello требуется уникальное имя внутри приложения hello.

   ```
   protected override async Task RunAsync(CancellationToken cancellationToken)
       {
           // TODO: Replace hello following sample code with your own logic
           //       or remove this RunAsync override if it's not needed in your service.

           while (true)
           {
               using( var operation = telemetryClient.StartOperation<RequestTelemetry>("[Insert_Event_Unique_Name]"))
               {
                   cancellationToken.ThrowIfCancellationRequested();

                   ++this.iterations;

                   ServiceEventSource.Current.ServiceMessage(this.Context, "Working-{0}", this.iterations);

                   await Task.Delay(TimeSpan.FromSeconds(1), cancellationToken);
               }

           }
       }
   ```

2. Развертывание кластера Service Fabric toohello приложения. Подождите 10 минут для toorun приложения hello. Для повышения эффекта нагрузочный тест можно выполнять на приложение hello. Портал Application Insights перейдите toohello **производительности** колонки и увидеть примеры профилирования трассировки отображаются.

<!---
Commenting out these sections for now
## Enable hello Profiler on Cloud Services applications
[TODO]
## Enable hello Profiler on classic Azure Virtual Machines
[TODO]
## Enable hello Profiler on on-premise servers
[TODO]
--->

## <a name="next-steps"></a>Дальнейшие действия

- Дополнительные сведения об устранении неполадок профилировщика см. в разделе [Устранение неполадок](app-insights-profiler.md#troubleshooting).

- Дополнительные сведения о профилировщик hello в [профилировщик аналитики приложений](app-insights-profiler.md).
