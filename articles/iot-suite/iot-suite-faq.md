---
title: "aaaAzure IoT Suite часто задаваемые вопросы | Документы Microsoft"
description: "Часто задаваемые вопросы об IoT Suite"
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: cb537749-a8a1-4e53-b3bf-f1b64a38188a
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: corywink
ms.openlocfilehash: cb39e24af6d1ce2afea554285512d05b2d7c721e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-for-iot-suite"></a><span data-ttu-id="82f3c-103">Часто задаваемые вопросы об IoT Suite</span><span class="sxs-lookup"><span data-stu-id="82f3c-103">Frequently asked questions for IoT Suite</span></span>

<span data-ttu-id="82f3c-104">См. также определенного подключенного фабрики hello [часто задаваемые вопросы о](iot-suite-faq-cf.md).</span><span class="sxs-lookup"><span data-stu-id="82f3c-104">See also, hello connected factory specific [FAQ](iot-suite-faq-cf.md).</span></span>

### <a name="where-can-i-find-hello-source-code-for-hello-preconfigured-solutions"></a><span data-ttu-id="82f3c-105">Где найти hello исходного кода для hello предварительно настроенных решений?</span><span class="sxs-lookup"><span data-stu-id="82f3c-105">Where can I find hello source code for hello preconfigured solutions?</span></span>

<span data-ttu-id="82f3c-106">Hello исходный код хранится в hello, следуя репозиториях GitHub:</span><span class="sxs-lookup"><span data-stu-id="82f3c-106">hello source code is stored in hello following GitHub repositories:</span></span>
* <span data-ttu-id="82f3c-107">[Предварительно настроенное решение для удаленного мониторинга][lnk-remote-monitoring-github]</span><span class="sxs-lookup"><span data-stu-id="82f3c-107">[Remote monitoring preconfigured solution][lnk-remote-monitoring-github]</span></span>
* <span data-ttu-id="82f3c-108">[Предварительно настроенное решение по диагностическому обслуживанию][lnk-predictive-maintenance-github]</span><span class="sxs-lookup"><span data-stu-id="82f3c-108">[Predictive maintenance preconfigured solution][lnk-predictive-maintenance-github]</span></span>
* [<span data-ttu-id="82f3c-109">Предварительно настроенное решение для подключенной фабрики</span><span class="sxs-lookup"><span data-stu-id="82f3c-109">Connected factory preconfigured solution</span></span>](https://github.com/Azure/azure-iot-connected-factory)

### <a name="how-do-i-update-toohello-latest-version-of-hello-remote-monitoring-preconfigured-solution-that-uses-hello-iot-hub-device-management-features"></a><span data-ttu-id="82f3c-110">Как обновить toohello последнюю версию решения удаленного мониторинга предварительно настроенных hello hello, использует функциональные возможности управления устройствами центра IoT?</span><span class="sxs-lookup"><span data-stu-id="82f3c-110">How do I update toohello latest version of hello remote monitoring preconfigured solution that uses hello IoT Hub device management features?</span></span>

* <span data-ttu-id="82f3c-111">При развертывании предварительно настроенных решений с сайта https://www.azureiotsuite.com/ hello всегда развертывает новый экземпляр hello последнюю версию решения hello.</span><span class="sxs-lookup"><span data-stu-id="82f3c-111">If you deploy a preconfigured solution from hello https://www.azureiotsuite.com/ site, it always deploys a new instance of hello latest version of hello solution.</span></span>
* <span data-ttu-id="82f3c-112">При развертывании предварительно настроенных решений с помощью командной строки hello, можно обновить существующее развертывание с нового кода.</span><span class="sxs-lookup"><span data-stu-id="82f3c-112">If you deploy a preconfigured solution using hello command line, you can update an existing deployment with new code.</span></span> <span data-ttu-id="82f3c-113">В разделе [облако развертывания] [ lnk-cloud-deployment] в hello GitHub [репозитория][lnk-remote-monitoring-github].</span><span class="sxs-lookup"><span data-stu-id="82f3c-113">See [Cloud deployment][lnk-cloud-deployment] in hello GitHub [repository][lnk-remote-monitoring-github].</span></span>

### <a name="how-can-i-add-support-for-a-new-device-method-toohello-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="82f3c-114">Как добавить поддержку нового устройства метод toohello удаленное наблюдение предварительно настроенных решений?</span><span class="sxs-lookup"><span data-stu-id="82f3c-114">How can I add support for a new device method toohello remote monitoring preconfigured solution?</span></span>

<span data-ttu-id="82f3c-115">В разделе hello [добавить поддержку нового симулятор toohello метод] [ lnk-add-method] в hello [настроить предварительно настроенных решений] [ lnk-customize] статьи.</span><span class="sxs-lookup"><span data-stu-id="82f3c-115">See hello section [Add support for a new method toohello simulator][lnk-add-method] in hello [Customize a preconfigured solution][lnk-customize] article.</span></span>

### <a name="hello-simulated-device-is-ignoring-my-desired-property-changes-why"></a><span data-ttu-id="82f3c-116">имитированное устройство Hello игнорирует изменения нужное свойство, почему?</span><span class="sxs-lookup"><span data-stu-id="82f3c-116">hello simulated device is ignoring my desired property changes, why?</span></span>
<span data-ttu-id="82f3c-117">В hello удаленный мониторинг предварительно настроенное решение, код hello имитируемые устройства использует только hello **Desired.Config.TemperatureMeanValue** и **Desired.Config.TelemetryInterval** требуемого свойства tooupdate hello сообщил свойства.</span><span class="sxs-lookup"><span data-stu-id="82f3c-117">In hello remote monitoring preconfigured solution, hello simulated device code only uses hello **Desired.Config.TemperatureMeanValue** and **Desired.Config.TelemetryInterval** desired properties tooupdate hello reported properties.</span></span> <span data-ttu-id="82f3c-118">Все прочие запросы на изменение требуемых свойств игнорируются.</span><span class="sxs-lookup"><span data-stu-id="82f3c-118">All other desired property change requests are ignored.</span></span>

### <a name="my-device-does-not-appear-in-hello-list-of-devices-in-hello-solution-dashboard-why"></a><span data-ttu-id="82f3c-119">Устройство не отображается в hello список устройств на панели мониторинга решения hello, почему?</span><span class="sxs-lookup"><span data-stu-id="82f3c-119">My device does not appear in hello list of devices in hello solution dashboard, why?</span></span>

<span data-ttu-id="82f3c-120">Hello список устройств на панели мониторинга hello решение использует список hello tooreturn запрос устройств.</span><span class="sxs-lookup"><span data-stu-id="82f3c-120">hello list of devices in hello solution dashboard uses a query tooreturn hello list of devices.</span></span> <span data-ttu-id="82f3c-121">В настоящее время запрос не может возвращать более 10 000 устройств.</span><span class="sxs-lookup"><span data-stu-id="82f3c-121">Currently, a query cannot return more than 10K devices.</span></span> <span data-ttu-id="82f3c-122">Попробуйте сделать более строгим hello критериев поиска для запроса.</span><span class="sxs-lookup"><span data-stu-id="82f3c-122">Try making hello search criteria for your query more restrictive.</span></span>

### <a name="whats-hello-difference-between-deleting-a-resource-group-in-hello-azure-portal-and-clicking-delete-on-a-preconfigured-solution-in-azureiotsuitecom"></a><span data-ttu-id="82f3c-123">Что такое hello различие между при удалении группы ресурсов в Azure, портала и затем выбрав удаление предварительно настроенного решения в azureiotsuite.com hello</span><span class="sxs-lookup"><span data-stu-id="82f3c-123">What's hello difference between deleting a resource group in hello Azure portal and clicking delete on a preconfigured solution in azureiotsuite.com?</span></span>

* <span data-ttu-id="82f3c-124">При удалении hello предварительно настроенное решение в [azureiotsuite.com][lnk-azureiotsuite], удалить все ресурсы hello, заданные при создании hello предварительно настроенных решений.</span><span class="sxs-lookup"><span data-stu-id="82f3c-124">If you delete hello preconfigured solution in [azureiotsuite.com][lnk-azureiotsuite], you delete all hello resources that were provisioned when you created hello preconfigured solution.</span></span> <span data-ttu-id="82f3c-125">Если вы добавили группы ресурсов toohello дополнительные ресурсы, эти ресурсы также будут удалены.</span><span class="sxs-lookup"><span data-stu-id="82f3c-125">If you added additional resources toohello resource group, these resources are also deleted.</span></span> 
* <span data-ttu-id="82f3c-126">Если удалить группу ресурсов hello в hello [портал Azure][lnk-azure-portal], необходимо удалить только hello ресурсов в этой группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="82f3c-126">If you delete hello resource group in hello [Azure portal][lnk-azure-portal], you only delete hello resources in that resource group.</span></span> <span data-ttu-id="82f3c-127">Необходимо также toodelete hello Azure Active Directory приложение, связанное с hello предварительно настроенное решение в hello [классический портал Azure][lnk-classic-portal].</span><span class="sxs-lookup"><span data-stu-id="82f3c-127">You also need toodelete hello Azure Active Directory application associated with hello preconfigured solution in hello [Azure classic portal][lnk-classic-portal].</span></span>

### <a name="how-many-iot-hub-instances-can-i-provision-in-a-subscription"></a><span data-ttu-id="82f3c-128">Сколько экземпляров центров IoT можно подготовить в рамках одной подписки?</span><span class="sxs-lookup"><span data-stu-id="82f3c-128">How many IoT Hub instances can I provision in a subscription?</span></span>

<span data-ttu-id="82f3c-129">По умолчанию [в рамках одной подписки можно подготовить 10 экземпляров Центра Интернета вещей][link-azuresublimits].</span><span class="sxs-lookup"><span data-stu-id="82f3c-129">By default you can provision [10 IoT hubs per subscription][link-azuresublimits].</span></span> <span data-ttu-id="82f3c-130">Можно создать [обращение в службу поддержки Azure] [ link-azuresupportticket] tooraise это ограничение.</span><span class="sxs-lookup"><span data-stu-id="82f3c-130">You can create an [Azure support ticket][link-azuresupportticket] tooraise this limit.</span></span> <span data-ttu-id="82f3c-131">В результате после каждой предварительно настроенных решений подготавливает центр IoT, вы можете только подготовки вверх too10 предварительно настроенных решений по данной подписке.</span><span class="sxs-lookup"><span data-stu-id="82f3c-131">As a result, since every preconfigured solution provisions a new IoT Hub, you can only provision up too10 preconfigured solutions in a given subscription.</span></span> 

### <a name="how-many-azure-cosmos-db-instances-can-i-provision-in-a-subscription"></a><span data-ttu-id="82f3c-132">Сколько экземпляров Azure Cosmos DB можно подготовить в рамках одной подписки?</span><span class="sxs-lookup"><span data-stu-id="82f3c-132">How many Azure Cosmos DB instances can I provision in a subscription?</span></span>

<span data-ttu-id="82f3c-133">Пятьдесят.</span><span class="sxs-lookup"><span data-stu-id="82f3c-133">Fifty.</span></span> <span data-ttu-id="82f3c-134">Можно создать [обращение в службу поддержки Azure] [ link-azuresupportticket] tooraise это ограничение, но по умолчанию можно указать только 50 экземпляров Cosmos DB на подписку.</span><span class="sxs-lookup"><span data-stu-id="82f3c-134">You can create an [Azure support ticket][link-azuresupportticket] tooraise this limit, but by default, you can only provision 50 Cosmos DB instances per subscription.</span></span> 

### <a name="how-many-free-bing-maps-apis-can-i-provision-in-a-subscription"></a><span data-ttu-id="82f3c-135">Сколько бесплатных API-интерфейсов Карт Bing можно подготовить в рамках одной подписки?</span><span class="sxs-lookup"><span data-stu-id="82f3c-135">How many Free Bing Maps APIs can I provision in a subscription?</span></span>

<span data-ttu-id="82f3c-136">Два.</span><span class="sxs-lookup"><span data-stu-id="82f3c-136">Two.</span></span> <span data-ttu-id="82f3c-137">В рамках подписки Azure можно создать только две карты Bing уровня 1 с внутренними транзакциями для корпоративных планов.</span><span class="sxs-lookup"><span data-stu-id="82f3c-137">You can create only two Internal Transactions Level 1 Bing Maps for Enterprise plans in an Azure subscription.</span></span> <span data-ttu-id="82f3c-138">решение для удаленного мониторинга Hello настраивается по умолчанию с планом hello внутренние транзакции уровня 1.</span><span class="sxs-lookup"><span data-stu-id="82f3c-138">hello remote monitoring solution is provisioned by default with hello Internal Transactions Level 1 plan.</span></span> <span data-ttu-id="82f3c-139">В результате могут только подготавливать tootwo удаленный мониторинг решений в подписке без изменений.</span><span class="sxs-lookup"><span data-stu-id="82f3c-139">As a result, you can only provision up tootwo remote monitoring solutions in a subscription with no modifications.</span></span>

### <a name="i-have-a-remote-monitoring-solution-deployment-with-a-static-map-how-do-i-add-an-interactive-bing-map"></a><span data-ttu-id="82f3c-140">У меня есть развернутое решение для удаленного мониторинга со статической картой. Как мне добавить интерактивную карту Bing?</span><span class="sxs-lookup"><span data-stu-id="82f3c-140">I have a remote monitoring solution deployment with a static map, how do I add an interactive Bing map?</span></span>

1. <span data-ttu-id="82f3c-141">Получите на [портале Azure][lnk-azure-portal] ключ QueryKey API для Карт Bing для предприятий:</span><span class="sxs-lookup"><span data-stu-id="82f3c-141">Get your Bing Maps API for Enterprise QueryKey from [Azure portal][lnk-azure-portal]:</span></span> 
   
   1. <span data-ttu-id="82f3c-142">Перейдите toohello группы ресурсов, где находится ваш API службы Bing Maps для предприятия в hello [портал Azure][lnk-azure-portal].</span><span class="sxs-lookup"><span data-stu-id="82f3c-142">Navigate toohello Resource Group where your Bing Maps API for Enterprise is in hello [Azure portal][lnk-azure-portal].</span></span>
   2. <span data-ttu-id="82f3c-143">Щелкните **Все параметры** и **Управление ключами**.</span><span class="sxs-lookup"><span data-stu-id="82f3c-143">Click **All Settings**, then **Key Management**.</span></span> 
   3. <span data-ttu-id="82f3c-144">Вы увидите два ключа: **MasterKey** и **QueryKey**.</span><span class="sxs-lookup"><span data-stu-id="82f3c-144">You can see two keys: **MasterKey** and **QueryKey**.</span></span> <span data-ttu-id="82f3c-145">Скопируйте значение hello для **QueryKey**.</span><span class="sxs-lookup"><span data-stu-id="82f3c-145">Copy hello value for **QueryKey**.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="82f3c-146">У вас нет учетной записи Bing Maps API for Enterprise?</span><span class="sxs-lookup"><span data-stu-id="82f3c-146">Don't have a Bing Maps API for Enterprise account?</span></span> <span data-ttu-id="82f3c-147">Создайте его в hello [портал Azure] [ lnk-azure-portal] , щелкнув + новый поиск Bing Maps API для выпусков Enterprise и выполните запрос toocreate.</span><span class="sxs-lookup"><span data-stu-id="82f3c-147">Create one in hello [Azure portal][lnk-azure-portal] by clicking + New, searching for Bing Maps API for Enterprise and follow prompts toocreate.</span></span>
      > 
      > 
2. <span data-ttu-id="82f3c-148">Подтягивают последнюю кода hello из hello [Azure IoT-удаленного-мониторинга][lnk-remote-monitoring-github].</span><span class="sxs-lookup"><span data-stu-id="82f3c-148">Pull down hello latest code from hello [Azure-IoT-Remote-Monitoring][lnk-remote-monitoring-github].</span></span>
3. <span data-ttu-id="82f3c-149">Запустите локальное или облачные развертывания следующие рекомендации hello развертывания из командной строки в папке /docs/ hello в репозитории hello.</span><span class="sxs-lookup"><span data-stu-id="82f3c-149">Run a local or cloud deployment following hello command-line deployment guidance in hello /docs/ folder in hello repository.</span></span> 
4. <span data-ttu-id="82f3c-150">После запуска локальной или облачной развертывания, проверьте в корневой папке для hello *. файл user.config, созданный во время развертывания.</span><span class="sxs-lookup"><span data-stu-id="82f3c-150">After you've run a local or cloud deployment, look in your root folder for hello *.user.config file created during deployment.</span></span> <span data-ttu-id="82f3c-151">Откройте этот файл в текстовом редакторе.</span><span class="sxs-lookup"><span data-stu-id="82f3c-151">Open this file in a text editor.</span></span> 
5. <span data-ttu-id="82f3c-152">Изменение hello следующая строка hello значение tooinclude, скопированный из вашего **QueryKey**:</span><span class="sxs-lookup"><span data-stu-id="82f3c-152">Change hello following line tooinclude hello value you copied from your **QueryKey**:</span></span> 
   
   `<setting name="MapApiQueryKey" value="" />`

### <a name="can-i-create-a-preconfigured-solution-if-i-have-microsoft-azure-for-dreamspark"></a><span data-ttu-id="82f3c-153">Можно ли создать предварительно настроенное решение при наличии Microsoft Azure для DreamSpark?</span><span class="sxs-lookup"><span data-stu-id="82f3c-153">Can I create a preconfigured solution if I have Microsoft Azure for DreamSpark?</span></span>

<span data-ttu-id="82f3c-154">Сейчас нельзя создавать предварительно настроенные решения с использованием учетной записи [Microsoft Azure для DreamSpark][lnk-dreamspark].</span><span class="sxs-lookup"><span data-stu-id="82f3c-154">Currently, you cannot create a preconfigured solution with a [Microsoft Azure for DreamSpark][lnk-dreamspark] account.</span></span> <span data-ttu-id="82f3c-155">Но вы можете создать [бесплатную пробную учетную запись Azure][lnk-30daytrial] всего за несколько минут. Это позволит вам создать предварительно настроенное решение.</span><span class="sxs-lookup"><span data-stu-id="82f3c-155">However, you can create a [free trial account for Azure][lnk-30daytrial] in just a couple of minutes that enables you create a preconfigured solution.</span></span>

### <a name="can-i-create-a-preconfigured-solution-if-i-have-cloud-solution-provider-csp-subscription"></a><span data-ttu-id="82f3c-156">Можно ли создать предварительно настроенное решение при наличии подписки поставщика облачных решений (CSP)?</span><span class="sxs-lookup"><span data-stu-id="82f3c-156">Can I create a preconfigured solution if I have Cloud Solution Provider (CSP) subscription?</span></span>

<span data-ttu-id="82f3c-157">В настоящее время создание предварительно настроенных решений с помощью подписки поставщика облачных решений (CSP) недоступно.</span><span class="sxs-lookup"><span data-stu-id="82f3c-157">Currently, you cannot create a preconfigured solution with a Cloud Solution Provider (CSP) subscription.</span></span> <span data-ttu-id="82f3c-158">Но вы можете создать [бесплатную пробную учетную запись Azure][lnk-30daytrial] всего за несколько минут. Это позволит вам создать предварительно настроенное решение.</span><span class="sxs-lookup"><span data-stu-id="82f3c-158">However, you can create a [free trial account for Azure][lnk-30daytrial] in just a couple of minutes that enables you create a preconfigured solution.</span></span>

### <a name="how-do-i-delete-an-aad-tenant"></a><span data-ttu-id="82f3c-159">Как удалить клиент AAD?</span><span class="sxs-lookup"><span data-stu-id="82f3c-159">How do I delete an AAD tenant?</span></span>

<span data-ttu-id="82f3c-160">Ознакомьтесь с записью блога Эрика Голпа (Eric Golpe) [Walkthrough of Deleting an Azure AD Tenant][lnk-delete-aad-tennant] (Пошаговое руководство по удалению клиента Azure AD).</span><span class="sxs-lookup"><span data-stu-id="82f3c-160">See Eric Golpe's blog post [Walkthrough of Deleting an Azure AD Tenant][lnk-delete-aad-tennant].</span></span>

### <a name="next-steps"></a><span data-ttu-id="82f3c-161">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="82f3c-161">Next steps</span></span>

<span data-ttu-id="82f3c-162">Можно также изучить некоторые hello и другие возможности hello IoT Suite предварительно настроенных решений:</span><span class="sxs-lookup"><span data-stu-id="82f3c-162">You can also explore some of hello other features and capabilities of hello IoT Suite preconfigured solutions:</span></span>

* <span data-ttu-id="82f3c-163">[Обзор предварительно настроенного решения прогнозируемого обслуживания][lnk-predictive-overview]</span><span class="sxs-lookup"><span data-stu-id="82f3c-163">[Predictive maintenance preconfigured solution overview][lnk-predictive-overview]</span></span>
* [<span data-ttu-id="82f3c-164">Начало работы с предварительно настроенным решением для подключенной фабрики</span><span class="sxs-lookup"><span data-stu-id="82f3c-164">Connected factory preconfigured solution overview</span></span>](iot-suite-connected-factory-overview.md)
* <span data-ttu-id="82f3c-165">[Основание безопасности IoT из hello,][lnk-security-groundup]</span><span class="sxs-lookup"><span data-stu-id="82f3c-165">[IoT security from hello ground up][lnk-security-groundup]</span></span>

[lnk-predictive-overview]: iot-suite-predictive-overview.md
[lnk-security-groundup]: securing-iot-ground-up.md

[link-azuresupportticket]: https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade 
[link-azuresublimits]: https://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/#iot-hub-limits
[lnk-azure-portal]: https://portal.azure.com
[lnk-azureiotsuite]: https://www.azureiotsuite.com/
[lnk-classic-portal]: https://manage.windowsazure.com
[lnk-remote-monitoring-github]: https://github.com/Azure/azure-iot-remote-monitoring 
[lnk-dreamspark]: https://www.dreamspark.com/Product/Product.aspx?productid=99 
[lnk-30daytrial]: https://azure.microsoft.com/free/
[lnk-delete-aad-tennant]: http://blogs.msdn.com/b/ericgolpe/archive/2015/04/30/walkthrough-of-deleting-an-azure-ad-tenant.aspx
[lnk-cloud-deployment]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/cloud-deployment.md
[lnk-add-method]: iot-suite-guidance-on-customizing-preconfigured-solutions.md#add-support-for-a-new-method-to-the-simulator
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-remote-monitoring-github]: https://github.com/Azure/azure-iot-remote-monitoring
[lnk-predictive-maintenance-github]: https://github.com/Azure/azure-iot-predictive-maintenance
