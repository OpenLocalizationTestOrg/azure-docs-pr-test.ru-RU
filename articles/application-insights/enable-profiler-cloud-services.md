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
# <a name="enable-application-insights-profiler-on-an-azure-cloud-services-resource"></a><span data-ttu-id="92ad0-103">Включение Azure Application Insights Profiler в ресурсе облачных служб</span><span class="sxs-lookup"><span data-stu-id="92ad0-103">Enable Application Insights Profiler on an Azure Cloud Services resource</span></span>

<span data-ttu-id="92ad0-104">В этом пошаговом руководстве показано, как tooenable профилировщик аналитики приложений Azure в приложении ASP.NET, размещенных по ресурсам облачных служб Azure.</span><span class="sxs-lookup"><span data-stu-id="92ad0-104">This walkthrough demonstrates how tooenable Azure Application Insights Profiler on an ASP.NET application hosted by an Azure Cloud Services resource.</span></span> <span data-ttu-id="92ad0-105">Примеры Hello включают поддержку виртуальных машин Azure, наборы масштабирования виртуальных машин и Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="92ad0-105">hello examples include support for Azure Virtual Machines, virtual machine scale sets, and Azure Service Fabric.</span></span> <span data-ttu-id="92ad0-106">Все примеры Hello полагаться на шаблоны, которые поддерживают hello модели развертывания диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="92ad0-106">hello examples all rely on templates that support hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="92ad0-107">Дополнительные сведения о модели развертывания hello [диспетчера ресурсов Azure и классическое развертывание: Обзор модели развертывания и hello состояния ресурсов](/azure-resource-manager/resource-manager-deployment-model).</span><span class="sxs-lookup"><span data-stu-id="92ad0-107">For more information about hello deployment model, review [Azure Resource Manager vs. classic deployment: Understand deployment models and hello state of your resources](/azure-resource-manager/resource-manager-deployment-model).</span></span>

## <a name="overview"></a><span data-ttu-id="92ad0-108">Обзор</span><span class="sxs-lookup"><span data-stu-id="92ad0-108">Overview</span></span>

<span data-ttu-id="92ad0-109">Следующая схема Hello показано, как профилировщик hello работает для облачных служб Azure ресурсов.</span><span class="sxs-lookup"><span data-stu-id="92ad0-109">hello following diagram illustrates how hello profiler works for Azure Cloud Services resources.</span></span> <span data-ttu-id="92ad0-110">Виртуальная машина Azure используется в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="92ad0-110">It uses an Azure virtual machine as an example.</span></span>

<span data-ttu-id="92ad0-111">![Общие сведения о](./media/enable-profiler-compute/overview.png) toocollect сведения для обработки и отображения на Здравствуйте портал Azure, необходимо установить компонент диагностики агента hello ресурсов hello облачных служб Azure.</span><span class="sxs-lookup"><span data-stu-id="92ad0-111">![Overview](./media/enable-profiler-compute/overview.png) toocollect information for processing and display on hello Azure portal, you must install hello Diagnostics Agent component for hello Azure Cloud Services resources.</span></span> <span data-ttu-id="92ad0-112">Hello остальной части hello Пошаговое руководство предоставляет инструкции по tooinstall и настройте агент диагностики hello tooenable профилировщик аналитики приложений.</span><span class="sxs-lookup"><span data-stu-id="92ad0-112">hello rest of hello walkthrough provides guidance on how tooinstall and configure hello Diagnostics Agent tooenable Application Insights Profiler.</span></span>

## <a name="prerequisites-for-hello-walkthrough"></a><span data-ttu-id="92ad0-113">Необходимые условия для пошагового руководства hello</span><span class="sxs-lookup"><span data-stu-id="92ad0-113">Prerequisites for hello walkthrough</span></span>

* <span data-ttu-id="92ad0-114">Шаблон развертывания диспетчера ресурсов, устанавливает hello профилировщик агенты на hello виртуальных машин ([WindowsVirtualMachine.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachine.json)) или масштабирования наборы ([WindowsVirtualMachineScaleSet.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachineScaleSet.json)).</span><span class="sxs-lookup"><span data-stu-id="92ad0-114">A deployment Resource Manager template that installs hello profiler agents on hello VMs ([WindowsVirtualMachine.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachine.json)) or scale sets ([WindowsVirtualMachineScaleSet.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachineScaleSet.json)).</span></span>

* <span data-ttu-id="92ad0-115">Экземпляр Application Insights, включенный для профилирования.</span><span class="sxs-lookup"><span data-stu-id="92ad0-115">An Application Insights instance enabled for profiling.</span></span> <span data-ttu-id="92ad0-116">Инструкции см. в разделе [включить профиль hello](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-profiler#enable-the-profiler).</span><span class="sxs-lookup"><span data-stu-id="92ad0-116">For instructions, see [Enable hello profile](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-profiler#enable-the-profiler).</span></span>

* <span data-ttu-id="92ad0-117">.NET framework 4.6.1 или более поздней версии, установленный на hello целевой ресурс облачных служб Azure.</span><span class="sxs-lookup"><span data-stu-id="92ad0-117">.NET Framework 4.6.1 or later installed on hello target Azure Cloud Services resource.</span></span>

## <a name="create-a-resource-group-in-your-azure-subscription"></a><span data-ttu-id="92ad0-118">Создание группы ресурсов в подписке Azure</span><span class="sxs-lookup"><span data-stu-id="92ad0-118">Create a resource group in your Azure subscription</span></span>
<span data-ttu-id="92ad0-119">Hello в следующем примере показано, как группировать toocreate ресурса с помощью сценария PowerShell:</span><span class="sxs-lookup"><span data-stu-id="92ad0-119">hello following example demonstrates how toocreate a resource group by using a PowerShell script:</span></span>

```
New-AzureRmResourceGroup -Name "Replace_With_Resource_Group_Name" -Location "Replace_With_Resource_Group_Location"
```

## <a name="create-an-application-insights-resource-in-hello-resource-group"></a><span data-ttu-id="92ad0-120">Создание ресурса Application Insights в группе ресурсов hello</span><span class="sxs-lookup"><span data-stu-id="92ad0-120">Create an Application Insights resource in hello resource group</span></span>
<span data-ttu-id="92ad0-121">На hello **Application Insights** колонке введите hello сведения для ресурса, как показано в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="92ad0-121">On hello **Application Insights** blade, enter hello information for your resource, as shown in this example:</span></span> 

![Колонка Application Insights](./media/enable-profiler-compute/createai.png)

## <a name="apply-an-application-insights-instrumentation-key-in-hello-azure-resource-manager-template"></a><span data-ttu-id="92ad0-123">Применить ключ инструментирования Application Insights в шаблоне hello диспетчера ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="92ad0-123">Apply an Application Insights instrumentation key in hello Azure Resource Manager template</span></span>

1. <span data-ttu-id="92ad0-124">Если еще не был загружен шаблон hello, загрузите его из [GitHub](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachine.json).</span><span class="sxs-lookup"><span data-stu-id="92ad0-124">If you haven't downloaded hello template yet, download it from [GitHub](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachine.json).</span></span>

2. <span data-ttu-id="92ad0-125">Поиск ключа Application Insights hello.</span><span class="sxs-lookup"><span data-stu-id="92ad0-125">Find hello Application Insights key.</span></span>
   
   ![Расположение ключа hello](./media/enable-profiler-compute/copyaikey.png)

3. <span data-ttu-id="92ad0-127">Замените значение шаблона hello.</span><span class="sxs-lookup"><span data-stu-id="92ad0-127">Replace hello template value.</span></span>
   
   ![Значение, замененное в шаблоне hello](./media/enable-profiler-compute/copyaikeytotemplate.png)

## <a name="create-an-azure-vm-toohost-hello-web-application"></a><span data-ttu-id="92ad0-129">Создать веб-приложение hello toohost ВМ Azure</span><span class="sxs-lookup"><span data-stu-id="92ad0-129">Create an Azure VM toohost hello web application</span></span>
1. <span data-ttu-id="92ad0-130">Создайте пароль hello toosave защищенной строки.</span><span class="sxs-lookup"><span data-stu-id="92ad0-130">Create a secure string toosave hello password.</span></span>

   ```
   $password = ConvertTo-SecureString -String "Replace_With_Your_Password" -AsPlainText -Force
   ```

2. <span data-ttu-id="92ad0-131">Развертывание шаблона диспетчера ресурсов Azure hello.</span><span class="sxs-lookup"><span data-stu-id="92ad0-131">Deploy hello Azure Resource Manager template.</span></span>

   <span data-ttu-id="92ad0-132">Измените каталог hello в папке toohello консоли PowerShell hello, содержащего шаблон диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="92ad0-132">Change hello directory in hello PowerShell console toohello folder that contains your Resource Manager template.</span></span> <span data-ttu-id="92ad0-133">toodeploy шаблон hello, запустите hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="92ad0-133">toodeploy hello template, run hello following command:</span></span>

   ```
   New-AzureRmResourceGroupDeployment -ResourceGroupName "Replace_With_Resource_Group_Name" -TemplateFile .\WindowsVirtualMachine.json -adminUsername "Replace_With_your_user_name" -adminPassword $password -dnsNameForPublicIP "Replace_WIth_your_DNS_Name" -Verbose
   ```

<span data-ttu-id="92ad0-134">После успешного выполнения сценария hello, вы должны найти Виртуальную машину с именем **MyWindowsVM** в группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="92ad0-134">After hello script runs successfully, you should find a VM named **MyWindowsVM** in your resource group.</span></span>

## <a name="configure-web-deploy-on-hello-vm"></a><span data-ttu-id="92ad0-135">Настройка веб-развертывания на hello виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="92ad0-135">Configure Web Deploy on hello VM</span></span>
<span data-ttu-id="92ad0-136">Убедитесь, что на виртуальной машине включено веб-развертывание, чтобы вы могли публиковать веб-приложения из Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="92ad0-136">Make sure that Web Deploy is enabled on your VM so you can publish your web application from Visual Studio.</span></span>

<span data-ttu-id="92ad0-137">см. веб-развертывания на виртуальной Машине вручную через WebPI, tooinstall [Установка и настройка веб-развертывания на IIS 8.0 и более поздней версии](https://docs.microsoft.com/en-us/iis/install/installing-publishing-technologies/installing-and-configuring-web-deploy-on-iis-80-or-later).</span><span class="sxs-lookup"><span data-stu-id="92ad0-137">tooinstall Web Deploy on a VM manually via WebPI, see [Installing and Configuring Web Deploy on IIS 8.0 or Later](https://docs.microsoft.com/en-us/iis/install/installing-publishing-technologies/installing-and-configuring-web-deploy-on-iis-80-or-later).</span></span> <span data-ttu-id="92ad0-138">Пример того, как tooautomate Установка веб-развертывания с помощью шаблона диспетчера ресурсов Azure, см. [создание, Настройка и развертывание tooan приложения web виртуальной Машины Azure](https://azure.microsoft.com/en-us/resources/templates/201-web-app-vm-dsc/).</span><span class="sxs-lookup"><span data-stu-id="92ad0-138">For an example of how tooautomate installing Web Deploy by using an Azure Resource Manager template, see [Create, configure, and deploy a web application tooan Azure VM](https://azure.microsoft.com/en-us/resources/templates/201-web-app-vm-dsc/).</span></span>

<span data-ttu-id="92ad0-139">При развертывании приложения ASP.NET MVC go tooServer Manager выберите **Добавить роли и компоненты** > **веб-сервер (IIS)** > **веб-сервере**  >  **Разработки приложений**и включите ASP.NET 4.5 на сервере.</span><span class="sxs-lookup"><span data-stu-id="92ad0-139">If you are deploying an ASP.NET MVC application, go tooServer Manager, select **Add Roles and Features** > **Web Server (IIS)** > **Web Server** > **Application Development**, and enable ASP.NET 4.5 on your server.</span></span>

![Добавление ASP.NET](./media/enable-profiler-compute/addaspnet45.png)

## <a name="install-hello-azure-application-insights-sdk-for-your-project"></a><span data-ttu-id="92ad0-141">Установка hello Azure пакет SDK Application Insights для проекта</span><span class="sxs-lookup"><span data-stu-id="92ad0-141">Install hello Azure Application Insights SDK for your project</span></span>
1. <span data-ttu-id="92ad0-142">Откройте веб-приложение ASP.NET в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="92ad0-142">Open your ASP.NET web application in Visual Studio.</span></span>

2. <span data-ttu-id="92ad0-143">Щелкните правой кнопкой мыши проект hello и выберите **добавить** > **подключенные службы**.</span><span class="sxs-lookup"><span data-stu-id="92ad0-143">Right-click hello project and select **Add** > **Connected Services**.</span></span>

3. <span data-ttu-id="92ad0-144">Выберите **Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="92ad0-144">Select **Application Insights**.</span></span>

4. <span data-ttu-id="92ad0-145">Выполните инструкции hello на странице приветствия.</span><span class="sxs-lookup"><span data-stu-id="92ad0-145">Follow hello instructions on hello page.</span></span> <span data-ttu-id="92ad0-146">Выберите ресурс Application Insights hello, которое было создано ранее.</span><span class="sxs-lookup"><span data-stu-id="92ad0-146">Select hello Application Insights resource that you created earlier.</span></span>

5. <span data-ttu-id="92ad0-147">Выберите hello **зарегистрировать** кнопки.</span><span class="sxs-lookup"><span data-stu-id="92ad0-147">Select hello **Register** button.</span></span>


## <a name="publish-hello-project-tooan-azure-vm"></a><span data-ttu-id="92ad0-148">Публикация проекта hello tooan ВМ Azure</span><span class="sxs-lookup"><span data-stu-id="92ad0-148">Publish hello project tooan Azure VM</span></span>
<span data-ttu-id="92ad0-149">Существует несколько способов toopublish tooan приложение виртуальной Машины Azure.</span><span class="sxs-lookup"><span data-stu-id="92ad0-149">There are several ways toopublish an application tooan Azure VM.</span></span> <span data-ttu-id="92ad0-150">Один из способов — toouse Visual Studio 2017 г.</span><span class="sxs-lookup"><span data-stu-id="92ad0-150">One way is toouse Visual Studio 2017.</span></span>

1. <span data-ttu-id="92ad0-151">Щелкните правой кнопкой мыши проект hello и выберите **публикации**.</span><span class="sxs-lookup"><span data-stu-id="92ad0-151">Right-click hello project and select **Publish**.</span></span>

2. <span data-ttu-id="92ad0-152">Выберите **виртуальные машины Microsoft Azure** как hello публикации целевой и выполните действия hello.</span><span class="sxs-lookup"><span data-stu-id="92ad0-152">Select **Microsoft Azure Virtual Machines** as hello publish target and follow hello steps.</span></span>

   ![Публикация из Visual Studio](./media/enable-profiler-compute/publishtoVM.png)

3. <span data-ttu-id="92ad0-154">Запустите нагрузочный тест для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="92ad0-154">Run a load test against your application.</span></span> <span data-ttu-id="92ad0-155">Вы увидите результаты на hello Application Insights экземпляр портала веб-странице.</span><span class="sxs-lookup"><span data-stu-id="92ad0-155">You should see results on hello Application Insights instance portal webpage.</span></span>


## <a name="enable-hello-profiler"></a><span data-ttu-id="92ad0-156">Включить профилировщик hello</span><span class="sxs-lookup"><span data-stu-id="92ad0-156">Enable hello profiler</span></span>
1. <span data-ttu-id="92ad0-157">Перейти в tooyour Application Insights **производительности** и выберите **Настройка**.</span><span class="sxs-lookup"><span data-stu-id="92ad0-157">Go tooyour Application Insights **Performance** blade and select **Configure**.</span></span>
   
   ![Значок настройки](./media/enable-profiler-compute/enableprofiler1.png)
 
2. <span data-ttu-id="92ad0-159">Выберите **Включить профилировщик**.</span><span class="sxs-lookup"><span data-stu-id="92ad0-159">Select **Enable Profiler**.</span></span>
   
   ![Значок включения профилировщика](./media/enable-profiler-compute/enableprofiler2.png)

## <a name="add-a-performance-test-tooyour-application"></a><span data-ttu-id="92ad0-161">Добавление приложения tooyour теста производительности</span><span class="sxs-lookup"><span data-stu-id="92ad0-161">Add a performance test tooyour application</span></span>
<span data-ttu-id="92ad0-162">Поэтому корпорация Майкрософт могла собрать некоторые toobe образец данных, отображаемых в профилировщик аналитики приложений, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="92ad0-162">Follow these steps so we can collect some sample data toobe displayed in Application Insights Profiler:</span></span>

1. <span data-ttu-id="92ad0-163">Выберите ресурс Application Insights toohello, которое было создано ранее.</span><span class="sxs-lookup"><span data-stu-id="92ad0-163">Browse toohello Application Insights resource that you created earlier.</span></span> 

2. <span data-ttu-id="92ad0-164">Go toohello **доступности** колонки и добавить тест производительности, который отправляет запросы tooyour приложения URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="92ad0-164">Go toohello **Availability** blade and add a performance test that sends web requests tooyour application URL.</span></span> 

   ![Добавление теста производительности](./media/enable-profiler-compute/AvailabilityTest.png)

## <a name="view-your-performance-data"></a><span data-ttu-id="92ad0-166">Просмотр данных о производительности</span><span class="sxs-lookup"><span data-stu-id="92ad0-166">View your performance data</span></span>

1. <span data-ttu-id="92ad0-167">Подождите 10 – 15 минут для toocollect профилировщик hello и анализировать данные hello.</span><span class="sxs-lookup"><span data-stu-id="92ad0-167">Wait 10-15 minutes for hello profiler toocollect and analyze hello data.</span></span> 

2. <span data-ttu-id="92ad0-168">Go toohello **производительности** колонки в ресурс Application Insights и представления, как выполнение приложения, когда он находится под высокой нагрузкой.</span><span class="sxs-lookup"><span data-stu-id="92ad0-168">Go toohello **Performance** blade in your Application Insights resource and view how your application is performing when it's under load.</span></span>

   ![Просмотр данных производительности](./media/enable-profiler-compute/aiperformance.png)

3. <span data-ttu-id="92ad0-170">Выберите hello рядом с заголовком **примеры** tooopen hello **представление трассировки** колонку.</span><span class="sxs-lookup"><span data-stu-id="92ad0-170">Select hello icon under **Examples** tooopen hello **Trace View** blade.</span></span>

   ![Открыв колонку hello представления трассировки](./media/enable-profiler-compute/traceview.png)


## <a name="work-with-an-existing-template"></a><span data-ttu-id="92ad0-172">Работа с имеющимся шаблоном</span><span class="sxs-lookup"><span data-stu-id="92ad0-172">Work with an existing template</span></span>

1. <span data-ttu-id="92ad0-173">Найдите объявление ресурса hello диагностики Azure в шаблон развертывания.</span><span class="sxs-lookup"><span data-stu-id="92ad0-173">Locate hello Azure Diagnostics resource declaration in your deployment template.</span></span>
   
   <span data-ttu-id="92ad0-174">Если у вас нет объявление, можно создать один похожа на объявление hello в следующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="92ad0-174">If you don't have a declaration, you can create one that resembles hello declaration in hello following example.</span></span> <span data-ttu-id="92ad0-175">Можно обновить шаблон hello из hello [обозревателя ресурсов Azure веб-сайт](https://resources.azure.com).</span><span class="sxs-lookup"><span data-stu-id="92ad0-175">You can update hello template from hello [Azure Resource Explorer website](https://resources.azure.com).</span></span>

2. <span data-ttu-id="92ad0-176">Издатель hello изменений из `Microsoft.Azure.Diagnostics` слишком`AIP.Diagnostics.Test`.</span><span class="sxs-lookup"><span data-stu-id="92ad0-176">Change hello publisher from `Microsoft.Azure.Diagnostics` too`AIP.Diagnostics.Test`.</span></span>

3. <span data-ttu-id="92ad0-177">Для `typeHandlerVersion` используйте `0.0`.</span><span class="sxs-lookup"><span data-stu-id="92ad0-177">For `typeHandlerVersion`, use `0.0`.</span></span>

4. <span data-ttu-id="92ad0-178">Убедитесь, что `autoUpgradeMinorVersion` задано слишком`true`.</span><span class="sxs-lookup"><span data-stu-id="92ad0-178">Make sure that `autoUpgradeMinorVersion` is set too`true`.</span></span>

5. <span data-ttu-id="92ad0-179">Добавить новый hello `ApplicationInsightsProfiler` приемник экземпляра в hello `WadCfg` объект параметров, как показано в следующий пример hello:</span><span class="sxs-lookup"><span data-stu-id="92ad0-179">Add hello new `ApplicationInsightsProfiler` sink instance in hello `WadCfg` settings object, as shown in hello following example:</span></span>

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

## <a name="enable-hello-profiler-on-virtual-machine-scale-sets"></a><span data-ttu-id="92ad0-180">Включить профилировщик hello на наборы масштабирования виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="92ad0-180">Enable hello profiler on virtual machine scale sets</span></span>
<span data-ttu-id="92ad0-181">toosee tooenable hello профилировщика, загрузите hello [WindowsVirtualMachineScaleSet.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachineScaleSet.json) шаблона.</span><span class="sxs-lookup"><span data-stu-id="92ad0-181">toosee how tooenable hello profiler, download hello [WindowsVirtualMachineScaleSet.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachineScaleSet.json) template.</span></span> <span data-ttu-id="92ad0-182">Примените hello же изменения в ресурс виртуальной Машины шаблон toohello диагностики расширения для набора масштабирования виртуальных машин hello.</span><span class="sxs-lookup"><span data-stu-id="92ad0-182">Apply hello same changes in a VM template toohello diagnostics extension resource for hello virtual machine scale set.</span></span>

<span data-ttu-id="92ad0-183">Каждый экземпляр в наборе масштабирования hello оставалось toohello доступа к Интернету.</span><span class="sxs-lookup"><span data-stu-id="92ad0-183">Make sure that each instance in hello scale set has access toohello internet.</span></span> <span data-ttu-id="92ad0-184">Hello агента профилировщик может передать hello собранные образцы tooApplication аналитики для отображения и анализа.</span><span class="sxs-lookup"><span data-stu-id="92ad0-184">hello Profiler Agent can then send hello collected samples tooApplication Insights for display and analysis.</span></span>

## <a name="enable-hello-profiler-on-service-fabric-applications"></a><span data-ttu-id="92ad0-185">Включить профилировщик hello на приложения Service Fabric</span><span class="sxs-lookup"><span data-stu-id="92ad0-185">Enable hello profiler on Service Fabric applications</span></span>
1. <span data-ttu-id="92ad0-186">Подготовка к работе hello Service Fabric кластера toohave hello Azure Diagnostics расширение, которое устанавливает hello профилировщик агента.</span><span class="sxs-lookup"><span data-stu-id="92ad0-186">Provision hello Service Fabric cluster toohave hello Azure Diagnostics extension that installs hello Profiler Agent.</span></span>

2. <span data-ttu-id="92ad0-187">Установка пакета SDK Application Insights hello в проекте hello и настройке ключа Application Insights hello.</span><span class="sxs-lookup"><span data-stu-id="92ad0-187">Install hello Application Insights SDK in hello project and configure hello Application Insights key.</span></span>

3. <span data-ttu-id="92ad0-188">Добавьте телеметрии tooinstrument кода приложения.</span><span class="sxs-lookup"><span data-stu-id="92ad0-188">Add application code tooinstrument telemetry.</span></span>

### <a name="provision-hello-service-fabric-cluster-toohave-hello-azure-diagnostics-extension-that-installs-hello-profiler-agent"></a><span data-ttu-id="92ad0-189">Toohave кластера hello расширение диагностики Azure, которое устанавливает hello профилировщик агента для подготовки hello Service Fabric</span><span class="sxs-lookup"><span data-stu-id="92ad0-189">Provision hello Service Fabric cluster toohave hello Azure Diagnostics extension that installs hello Profiler Agent</span></span>
<span data-ttu-id="92ad0-190">Кластер Service Fabric может быть безопасным или небезопасным.</span><span class="sxs-lookup"><span data-stu-id="92ad0-190">A Service Fabric cluster can be secure or non-secure.</span></span> <span data-ttu-id="92ad0-191">Можно установить один toobe кластера шлюза не является безопасной, сертификат не требуется для доступа.</span><span class="sxs-lookup"><span data-stu-id="92ad0-191">You can set one gateway cluster toobe non-secure so it doesn't require a certificate for access.</span></span> <span data-ttu-id="92ad0-192">Кластеры, содержащие бизнес-логику и данные, должны быть безопасными.</span><span class="sxs-lookup"><span data-stu-id="92ad0-192">Clusters that host business logic and data should be secure.</span></span> <span data-ttu-id="92ad0-193">Вы можете включить профилировщик hello на безопасные и небезопасные кластеров Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="92ad0-193">You can enable hello profiler on both secure and non-secure Service Fabric clusters.</span></span> <span data-ttu-id="92ad0-194">В этом пошаговом руководстве используется кластер небезопасные как пример tooexplain изменений, необходимых tooenable hello профилировщика.</span><span class="sxs-lookup"><span data-stu-id="92ad0-194">This walkthrough uses a non-secure cluster as an example tooexplain what changes are required tooenable hello profiler.</span></span> <span data-ttu-id="92ad0-195">Можно подготовить безопасного кластера в hello таким же образом.</span><span class="sxs-lookup"><span data-stu-id="92ad0-195">You can provision a secure cluster in hello same way.</span></span>

1. <span data-ttu-id="92ad0-196">Загрузите [ServiceFabricCluster.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/ServiceFabricCluster.json).</span><span class="sxs-lookup"><span data-stu-id="92ad0-196">Download [ServiceFabricCluster.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/ServiceFabricCluster.json).</span></span> <span data-ttu-id="92ad0-197">Замените `Application_Insights_Key` своим ключом Application Insights так же, как для виртуальных машин и масштабируемых наборов виртуальных машин:</span><span class="sxs-lookup"><span data-stu-id="92ad0-197">As you did for VMs and virtual machine scale sets, replace `Application_Insights_Key` with your Application Insights key:</span></span>

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

2. <span data-ttu-id="92ad0-198">Развертывание hello шаблона с помощью сценария PowerShell:</span><span class="sxs-lookup"><span data-stu-id="92ad0-198">Deploy hello template by using a PowerShell script:</span></span>

   ```
   Login-AzureRmAccount
   New-AzureRmResourceGroup -Name [Your_Resource_Group_Name] -Location [Your_Resource_Group_Location] -Verbose -Force
   New-AzureRmResourceGroupDeployment -Name [Choose_An_Arbitrary_Name] -ResourceGroupName [Your_Resource_Group_Name] -TemplateFile [Path_To_Your_Template]

   ```

### <a name="install-hello-application-insights-sdk-in-hello-project-and-configure-hello-application-insights-key"></a><span data-ttu-id="92ad0-199">Установка пакета SDK Application Insights hello в проекте hello и настройке ключа Application Insights hello</span><span class="sxs-lookup"><span data-stu-id="92ad0-199">Install hello Application Insights SDK in hello project and configure hello Application Insights key</span></span>
<span data-ttu-id="92ad0-200">Установите пакет SDK Application Insights hello из hello [пакет NuGet](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/).</span><span class="sxs-lookup"><span data-stu-id="92ad0-200">Install hello Application Insights SDK from hello [NuGet package](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/).</span></span> <span data-ttu-id="92ad0-201">Убедитесь, что устанавливается стабильная версия 2.3 или более поздняя.</span><span class="sxs-lookup"><span data-stu-id="92ad0-201">Make sure that you install a stable version, 2.3 or later.</span></span> 

<span data-ttu-id="92ad0-202">Сведения о настройке Application Insights в проектах см. в статье [Using Service Fabric with Application Insights](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/blob/dev/appinsights/ApplicationInsights.md) (Использование Service Fabric с Application Insights).</span><span class="sxs-lookup"><span data-stu-id="92ad0-202">For information about configuring Application Insights in your projects, see [Using Service Fabric with Application Insights](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/blob/dev/appinsights/ApplicationInsights.md).</span></span>

### <a name="add-application-code-tooinstrument-telemetry"></a><span data-ttu-id="92ad0-203">Добавить телеметрии tooinstrument кода приложения</span><span class="sxs-lookup"><span data-stu-id="92ad0-203">Add application code tooinstrument telemetry</span></span>
1. <span data-ttu-id="92ad0-204">Для любого фрагмента кода, которые должны tooinstrument добавить с помощью инструкции вокруг нее.</span><span class="sxs-lookup"><span data-stu-id="92ad0-204">For any piece of code that you want tooinstrument, add a using statement around it.</span></span> 

   <span data-ttu-id="92ad0-205">В следующем примере hello, hello `RunAsync` метод выполняет некоторые действия и hello `telemetryClient` класс регистрирует данные телеметрии hello после ее запуска.</span><span class="sxs-lookup"><span data-stu-id="92ad0-205">In hello following  example, hello `RunAsync` method is doing some work, and hello `telemetryClient` class captures hello telemetry after it starts.</span></span> <span data-ttu-id="92ad0-206">событие Hello требуется уникальное имя внутри приложения hello.</span><span class="sxs-lookup"><span data-stu-id="92ad0-206">hello event needs a unique name across hello application.</span></span>

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

2. <span data-ttu-id="92ad0-207">Развертывание кластера Service Fabric toohello приложения.</span><span class="sxs-lookup"><span data-stu-id="92ad0-207">Deploy your application toohello Service Fabric cluster.</span></span> <span data-ttu-id="92ad0-208">Подождите 10 минут для toorun приложения hello.</span><span class="sxs-lookup"><span data-stu-id="92ad0-208">Wait for hello app toorun for 10 minutes.</span></span> <span data-ttu-id="92ad0-209">Для повышения эффекта нагрузочный тест можно выполнять на приложение hello.</span><span class="sxs-lookup"><span data-stu-id="92ad0-209">For better effect, you can run a load test on hello app.</span></span> <span data-ttu-id="92ad0-210">Портал Application Insights перейдите toohello **производительности** колонки и увидеть примеры профилирования трассировки отображаются.</span><span class="sxs-lookup"><span data-stu-id="92ad0-210">Go toohello Application Insights portal's **Performance** blade, and you should see examples of profiling traces appear.</span></span>

<!---
Commenting out these sections for now
## Enable hello Profiler on Cloud Services applications
[TODO]
## Enable hello Profiler on classic Azure Virtual Machines
[TODO]
## Enable hello Profiler on on-premise servers
[TODO]
--->

## <a name="next-steps"></a><span data-ttu-id="92ad0-211">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="92ad0-211">Next steps</span></span>

- <span data-ttu-id="92ad0-212">Дополнительные сведения об устранении неполадок профилировщика см. в разделе [Устранение неполадок](app-insights-profiler.md#troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="92ad0-212">Find help with troubleshooting profiler issues in [Profiler troubleshooting](app-insights-profiler.md#troubleshooting).</span></span>

- <span data-ttu-id="92ad0-213">Дополнительные сведения о профилировщик hello в [профилировщик аналитики приложений](app-insights-profiler.md).</span><span class="sxs-lookup"><span data-stu-id="92ad0-213">Read more about hello profiler in [Application Insights Profiler](app-insights-profiler.md).</span></span>
