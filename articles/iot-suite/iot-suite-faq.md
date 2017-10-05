---
title: "Часто задаваемые вопросы по Azure IoT Suite | Документация Майкрософт"
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
ms.openlocfilehash: 85867fb8d18377637b3aa848555831a8d9b53512
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="frequently-asked-questions-for-iot-suite"></a><span data-ttu-id="b21a9-103">Часто задаваемые вопросы об IoT Suite</span><span class="sxs-lookup"><span data-stu-id="b21a9-103">Frequently asked questions for IoT Suite</span></span>

<span data-ttu-id="b21a9-104">Дополнительные сведения см. также в статье [Часто задаваемые вопросы о предварительно настроенном решении для подключенной фабрики IoT Suite](iot-suite-faq-cf.md).</span><span class="sxs-lookup"><span data-stu-id="b21a9-104">See also, the connected factory specific [FAQ](iot-suite-faq-cf.md).</span></span>

### <a name="where-can-i-find-the-source-code-for-the-preconfigured-solutions"></a><span data-ttu-id="b21a9-105">Где можно найти исходный код для предварительно настроенных решений?</span><span class="sxs-lookup"><span data-stu-id="b21a9-105">Where can I find the source code for the preconfigured solutions?</span></span>

<span data-ttu-id="b21a9-106">Исходный код хранится в следующих репозиториях GitHub:</span><span class="sxs-lookup"><span data-stu-id="b21a9-106">The source code is stored in the following GitHub repositories:</span></span>
* <span data-ttu-id="b21a9-107">[Предварительно настроенное решение для удаленного мониторинга][lnk-remote-monitoring-github]</span><span class="sxs-lookup"><span data-stu-id="b21a9-107">[Remote monitoring preconfigured solution][lnk-remote-monitoring-github]</span></span>
* <span data-ttu-id="b21a9-108">[Предварительно настроенное решение по диагностическому обслуживанию][lnk-predictive-maintenance-github]</span><span class="sxs-lookup"><span data-stu-id="b21a9-108">[Predictive maintenance preconfigured solution][lnk-predictive-maintenance-github]</span></span>
* [<span data-ttu-id="b21a9-109">Предварительно настроенное решение для подключенной фабрики</span><span class="sxs-lookup"><span data-stu-id="b21a9-109">Connected factory preconfigured solution</span></span>](https://github.com/Azure/azure-iot-connected-factory)

### <a name="how-do-i-update-to-the-latest-version-of-the-remote-monitoring-preconfigured-solution-that-uses-the-iot-hub-device-management-features"></a><span data-ttu-id="b21a9-110">Как обновить до последней версии предварительно настроенное решение удаленного мониторинга, которое использует функции управления устройствами Центра Интернета вещей?</span><span class="sxs-lookup"><span data-stu-id="b21a9-110">How do I update to the latest version of the remote monitoring preconfigured solution that uses the IoT Hub device management features?</span></span>

* <span data-ttu-id="b21a9-111">При развертывании предварительно настроенного решения с сайта https://www.azureiotsuite.com/ всегда развертывается новый экземпляр последней его версии.</span><span class="sxs-lookup"><span data-stu-id="b21a9-111">If you deploy a preconfigured solution from the https://www.azureiotsuite.com/ site, it always deploys a new instance of the latest version of the solution.</span></span>
* <span data-ttu-id="b21a9-112">При развертывании предварительно настроенного решения с помощью командной строки можно обновить существующее развертывание, добавив новый код.</span><span class="sxs-lookup"><span data-stu-id="b21a9-112">If you deploy a preconfigured solution using the command line, you can update an existing deployment with new code.</span></span> <span data-ttu-id="b21a9-113">См. сведения о [развертывании в облаке][lnk-cloud-deployment] в [репозитории][lnk-remote-monitoring-github] GitHub.</span><span class="sxs-lookup"><span data-stu-id="b21a9-113">See [Cloud deployment][lnk-cloud-deployment] in the GitHub [repository][lnk-remote-monitoring-github].</span></span>

### <a name="how-can-i-add-support-for-a-new-device-method-to-the-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="b21a9-114">Как добавить поддержку нового метода устройства в предварительно настроенное решение для удаленного мониторинга?</span><span class="sxs-lookup"><span data-stu-id="b21a9-114">How can I add support for a new device method to the remote monitoring preconfigured solution?</span></span>

<span data-ttu-id="b21a9-115">См. сведения в разделе [Добавление в симулятор поддержки для нового метода][lnk-add-method] статьи [Настройка предварительно настроенного решения][lnk-customize].</span><span class="sxs-lookup"><span data-stu-id="b21a9-115">See the section [Add support for a new method to the simulator][lnk-add-method] in the [Customize a preconfigured solution][lnk-customize] article.</span></span>

### <a name="the-simulated-device-is-ignoring-my-desired-property-changes-why"></a><span data-ttu-id="b21a9-116">Почему виртуальное устройство игнорирует изменения требуемых свойств?</span><span class="sxs-lookup"><span data-stu-id="b21a9-116">The simulated device is ignoring my desired property changes, why?</span></span>
<span data-ttu-id="b21a9-117">В предварительно настроенном решении для мониторинга код виртуального устройства использует только требуемые свойства **Desired.Config.TemperatureMeanValue** и **Desired.Config.TelemetryInterval**, чтобы обновить сообщаемые свойства.</span><span class="sxs-lookup"><span data-stu-id="b21a9-117">In the remote monitoring preconfigured solution, the simulated device code only uses the **Desired.Config.TemperatureMeanValue** and **Desired.Config.TelemetryInterval** desired properties to update the reported properties.</span></span> <span data-ttu-id="b21a9-118">Все прочие запросы на изменение требуемых свойств игнорируются.</span><span class="sxs-lookup"><span data-stu-id="b21a9-118">All other desired property change requests are ignored.</span></span>

### <a name="my-device-does-not-appear-in-the-list-of-devices-in-the-solution-dashboard-why"></a><span data-ttu-id="b21a9-119">Почему устройство не отображается в списке устройств на панели мониторинга решения?</span><span class="sxs-lookup"><span data-stu-id="b21a9-119">My device does not appear in the list of devices in the solution dashboard, why?</span></span>

<span data-ttu-id="b21a9-120">Для возврата списка устройств на панели мониторинга решения используется запрос.</span><span class="sxs-lookup"><span data-stu-id="b21a9-120">The list of devices in the solution dashboard uses a query to return the list of devices.</span></span> <span data-ttu-id="b21a9-121">В настоящее время запрос не может возвращать более 10 000 устройств.</span><span class="sxs-lookup"><span data-stu-id="b21a9-121">Currently, a query cannot return more than 10K devices.</span></span> <span data-ttu-id="b21a9-122">Попробуйте ограничить условие поиска для запроса.</span><span class="sxs-lookup"><span data-stu-id="b21a9-122">Try making the search criteria for your query more restrictive.</span></span>

### <a name="whats-the-difference-between-deleting-a-resource-group-in-the-azure-portal-and-clicking-delete-on-a-preconfigured-solution-in-azureiotsuitecom"></a><span data-ttu-id="b21a9-123">В чем разница между удалением группы ресурсов на портале Azure и нажатием кнопки "Удалить" в предварительно настроенном решении на сайте azureiotsuite.com?</span><span class="sxs-lookup"><span data-stu-id="b21a9-123">What's the difference between deleting a resource group in the Azure portal and clicking delete on a preconfigured solution in azureiotsuite.com?</span></span>

* <span data-ttu-id="b21a9-124">Если удалить предварительно настроенное решение на сайте [azureiotsuite.com][lnk-azureiotsuite], будут удалены все ресурсы, подготовленные при создании этого решения.</span><span class="sxs-lookup"><span data-stu-id="b21a9-124">If you delete the preconfigured solution in [azureiotsuite.com][lnk-azureiotsuite], you delete all the resources that were provisioned when you created the preconfigured solution.</span></span> <span data-ttu-id="b21a9-125">Если вы добавляли в группу ресурсов дополнительные ресурсы, они также будут удалены.</span><span class="sxs-lookup"><span data-stu-id="b21a9-125">If you added additional resources to the resource group, these resources are also deleted.</span></span> 
* <span data-ttu-id="b21a9-126">Если удалить группу ресурсов на [портале Azure][lnk-azure-portal], будут удалены ресурсы в этой группе.</span><span class="sxs-lookup"><span data-stu-id="b21a9-126">If you delete the resource group in the [Azure portal][lnk-azure-portal], you only delete the resources in that resource group.</span></span> <span data-ttu-id="b21a9-127">Вам также придется удалить приложение Azure Active Directory, связанное с предварительно настроенным решением, на[ классическом портале Azure][lnk-classic-portal].</span><span class="sxs-lookup"><span data-stu-id="b21a9-127">You also need to delete the Azure Active Directory application associated with the preconfigured solution in the [Azure classic portal][lnk-classic-portal].</span></span>

### <a name="how-many-iot-hub-instances-can-i-provision-in-a-subscription"></a><span data-ttu-id="b21a9-128">Сколько экземпляров центров IoT можно подготовить в рамках одной подписки?</span><span class="sxs-lookup"><span data-stu-id="b21a9-128">How many IoT Hub instances can I provision in a subscription?</span></span>

<span data-ttu-id="b21a9-129">По умолчанию [в рамках одной подписки можно подготовить 10 экземпляров Центра Интернета вещей][link-azuresublimits].</span><span class="sxs-lookup"><span data-stu-id="b21a9-129">By default you can provision [10 IoT hubs per subscription][link-azuresublimits].</span></span> <span data-ttu-id="b21a9-130">Можно создать [запрос в службу поддержки Azure][link-azuresupportticket], чтобы увеличить этот лимит.</span><span class="sxs-lookup"><span data-stu-id="b21a9-130">You can create an [Azure support ticket][link-azuresupportticket] to raise this limit.</span></span> <span data-ttu-id="b21a9-131">Так как каждое предварительно настроенное решение подготавливает новый Центр Интернета вещей, в рамках одной подписки можно подготовить до 10 таких решений.</span><span class="sxs-lookup"><span data-stu-id="b21a9-131">As a result, since every preconfigured solution provisions a new IoT Hub, you can only provision up to 10 preconfigured solutions in a given subscription.</span></span> 

### <a name="how-many-azure-cosmos-db-instances-can-i-provision-in-a-subscription"></a><span data-ttu-id="b21a9-132">Сколько экземпляров Azure Cosmos DB можно подготовить в рамках одной подписки?</span><span class="sxs-lookup"><span data-stu-id="b21a9-132">How many Azure Cosmos DB instances can I provision in a subscription?</span></span>

<span data-ttu-id="b21a9-133">Пятьдесят.</span><span class="sxs-lookup"><span data-stu-id="b21a9-133">Fifty.</span></span> <span data-ttu-id="b21a9-134">Вы можете направить [запрос в службу поддержки Azure][link-azuresupportticket], чтобы увеличить это количество, но по умолчанию в рамках одной подписки можно подготовить только 50 экземпляров Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="b21a9-134">You can create an [Azure support ticket][link-azuresupportticket] to raise this limit, but by default, you can only provision 50 Cosmos DB instances per subscription.</span></span> 

### <a name="how-many-free-bing-maps-apis-can-i-provision-in-a-subscription"></a><span data-ttu-id="b21a9-135">Сколько бесплатных API-интерфейсов Карт Bing можно подготовить в рамках одной подписки?</span><span class="sxs-lookup"><span data-stu-id="b21a9-135">How many Free Bing Maps APIs can I provision in a subscription?</span></span>

<span data-ttu-id="b21a9-136">Два.</span><span class="sxs-lookup"><span data-stu-id="b21a9-136">Two.</span></span> <span data-ttu-id="b21a9-137">В рамках подписки Azure можно создать только две карты Bing уровня 1 с внутренними транзакциями для корпоративных планов.</span><span class="sxs-lookup"><span data-stu-id="b21a9-137">You can create only two Internal Transactions Level 1 Bing Maps for Enterprise plans in an Azure subscription.</span></span> <span data-ttu-id="b21a9-138">Решение для удаленного мониторинга по умолчанию подготавливается с помощью плана уровня 1 с внутренними транзакциями.</span><span class="sxs-lookup"><span data-stu-id="b21a9-138">The remote monitoring solution is provisioned by default with the Internal Transactions Level 1 plan.</span></span> <span data-ttu-id="b21a9-139">Иными словами, используя одну подписку, в которую не вносились изменения, вы можете подготовить не более двух решений для удаленного мониторинга.</span><span class="sxs-lookup"><span data-stu-id="b21a9-139">As a result, you can only provision up to two remote monitoring solutions in a subscription with no modifications.</span></span>

### <a name="i-have-a-remote-monitoring-solution-deployment-with-a-static-map-how-do-i-add-an-interactive-bing-map"></a><span data-ttu-id="b21a9-140">У меня есть развернутое решение для удаленного мониторинга со статической картой. Как мне добавить интерактивную карту Bing?</span><span class="sxs-lookup"><span data-stu-id="b21a9-140">I have a remote monitoring solution deployment with a static map, how do I add an interactive Bing map?</span></span>

1. <span data-ttu-id="b21a9-141">Получите на [портале Azure][lnk-azure-portal] ключ QueryKey API для Карт Bing для предприятий:</span><span class="sxs-lookup"><span data-stu-id="b21a9-141">Get your Bing Maps API for Enterprise QueryKey from [Azure portal][lnk-azure-portal]:</span></span> 
   
   1. <span data-ttu-id="b21a9-142">На [портале Azure][lnk-azure-portal] перейдите в группу ресурсов с учетной записью API для Карт Bing для предприятий.</span><span class="sxs-lookup"><span data-stu-id="b21a9-142">Navigate to the Resource Group where your Bing Maps API for Enterprise is in the [Azure portal][lnk-azure-portal].</span></span>
   2. <span data-ttu-id="b21a9-143">Щелкните **Все параметры** и **Управление ключами**.</span><span class="sxs-lookup"><span data-stu-id="b21a9-143">Click **All Settings**, then **Key Management**.</span></span> 
   3. <span data-ttu-id="b21a9-144">Вы увидите два ключа: **MasterKey** и **QueryKey**.</span><span class="sxs-lookup"><span data-stu-id="b21a9-144">You can see two keys: **MasterKey** and **QueryKey**.</span></span> <span data-ttu-id="b21a9-145">Скопируйте значение ключа **QueryKey**.</span><span class="sxs-lookup"><span data-stu-id="b21a9-145">Copy the value for **QueryKey**.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="b21a9-146">У вас нет учетной записи Bing Maps API for Enterprise?</span><span class="sxs-lookup"><span data-stu-id="b21a9-146">Don't have a Bing Maps API for Enterprise account?</span></span> <span data-ttu-id="b21a9-147">Создайте ее на [портале Azure][lnk-azure-portal], щелкнув "+ Создать". Затем найдите API для Карт Bing для предприятий и следуйте подсказкам по созданию.</span><span class="sxs-lookup"><span data-stu-id="b21a9-147">Create one in the [Azure portal][lnk-azure-portal] by clicking + New, searching for Bing Maps API for Enterprise and follow prompts to create.</span></span>
      > 
      > 
2. <span data-ttu-id="b21a9-148">Разверните последний фрагмент кода из архива [Azure-IoT-Remote-Monitoring][lnk-remote-monitoring-github].</span><span class="sxs-lookup"><span data-stu-id="b21a9-148">Pull down the latest code from the [Azure-IoT-Remote-Monitoring][lnk-remote-monitoring-github].</span></span>
3. <span data-ttu-id="b21a9-149">Запустите развертывание (локально или в облаке) в соответствии с руководством по развертыванию, которое находится в папке /docs/ репозитория.</span><span class="sxs-lookup"><span data-stu-id="b21a9-149">Run a local or cloud deployment following the command-line deployment guidance in the /docs/ folder in the repository.</span></span> 
4. <span data-ttu-id="b21a9-150">Запустив развертывание (локально или в облаке), найдите в корневой папке файл *.user.config, созданный во время развертывания.</span><span class="sxs-lookup"><span data-stu-id="b21a9-150">After you've run a local or cloud deployment, look in your root folder for the *.user.config file created during deployment.</span></span> <span data-ttu-id="b21a9-151">Откройте этот файл в текстовом редакторе.</span><span class="sxs-lookup"><span data-stu-id="b21a9-151">Open this file in a text editor.</span></span> 
5. <span data-ttu-id="b21a9-152">Измените следующую строку, чтобы включить скопированное из ключа **QueryKey** значение:</span><span class="sxs-lookup"><span data-stu-id="b21a9-152">Change the following line to include the value you copied from your **QueryKey**:</span></span> 
   
   `<setting name="MapApiQueryKey" value="" />`

### <a name="can-i-create-a-preconfigured-solution-if-i-have-microsoft-azure-for-dreamspark"></a><span data-ttu-id="b21a9-153">Можно ли создать предварительно настроенное решение при наличии Microsoft Azure для DreamSpark?</span><span class="sxs-lookup"><span data-stu-id="b21a9-153">Can I create a preconfigured solution if I have Microsoft Azure for DreamSpark?</span></span>

<span data-ttu-id="b21a9-154">Сейчас нельзя создавать предварительно настроенные решения с использованием учетной записи [Microsoft Azure для DreamSpark][lnk-dreamspark].</span><span class="sxs-lookup"><span data-stu-id="b21a9-154">Currently, you cannot create a preconfigured solution with a [Microsoft Azure for DreamSpark][lnk-dreamspark] account.</span></span> <span data-ttu-id="b21a9-155">Но вы можете создать [бесплатную пробную учетную запись Azure][lnk-30daytrial] всего за несколько минут. Это позволит вам создать предварительно настроенное решение.</span><span class="sxs-lookup"><span data-stu-id="b21a9-155">However, you can create a [free trial account for Azure][lnk-30daytrial] in just a couple of minutes that enables you create a preconfigured solution.</span></span>

### <a name="can-i-create-a-preconfigured-solution-if-i-have-cloud-solution-provider-csp-subscription"></a><span data-ttu-id="b21a9-156">Можно ли создать предварительно настроенное решение при наличии подписки поставщика облачных решений (CSP)?</span><span class="sxs-lookup"><span data-stu-id="b21a9-156">Can I create a preconfigured solution if I have Cloud Solution Provider (CSP) subscription?</span></span>

<span data-ttu-id="b21a9-157">В настоящее время создание предварительно настроенных решений с помощью подписки поставщика облачных решений (CSP) недоступно.</span><span class="sxs-lookup"><span data-stu-id="b21a9-157">Currently, you cannot create a preconfigured solution with a Cloud Solution Provider (CSP) subscription.</span></span> <span data-ttu-id="b21a9-158">Но вы можете создать [бесплатную пробную учетную запись Azure][lnk-30daytrial] всего за несколько минут. Это позволит вам создать предварительно настроенное решение.</span><span class="sxs-lookup"><span data-stu-id="b21a9-158">However, you can create a [free trial account for Azure][lnk-30daytrial] in just a couple of minutes that enables you create a preconfigured solution.</span></span>

### <a name="how-do-i-delete-an-aad-tenant"></a><span data-ttu-id="b21a9-159">Как удалить клиент AAD?</span><span class="sxs-lookup"><span data-stu-id="b21a9-159">How do I delete an AAD tenant?</span></span>

<span data-ttu-id="b21a9-160">Ознакомьтесь с записью блога Эрика Голпа (Eric Golpe) [Walkthrough of Deleting an Azure AD Tenant][lnk-delete-aad-tennant] (Пошаговое руководство по удалению клиента Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b21a9-160">See Eric Golpe's blog post [Walkthrough of Deleting an Azure AD Tenant][lnk-delete-aad-tennant].</span></span>

### <a name="next-steps"></a><span data-ttu-id="b21a9-161">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b21a9-161">Next steps</span></span>

<span data-ttu-id="b21a9-162">Вы также можете ознакомиться с другими функциями и возможностями предварительно настроенных решений IoT Suite.</span><span class="sxs-lookup"><span data-stu-id="b21a9-162">You can also explore some of the other features and capabilities of the IoT Suite preconfigured solutions:</span></span>

* <span data-ttu-id="b21a9-163">[Обзор предварительно настроенного решения прогнозируемого обслуживания][lnk-predictive-overview]</span><span class="sxs-lookup"><span data-stu-id="b21a9-163">[Predictive maintenance preconfigured solution overview][lnk-predictive-overview]</span></span>
* [<span data-ttu-id="b21a9-164">Начало работы с предварительно настроенным решением для подключенной фабрики</span><span class="sxs-lookup"><span data-stu-id="b21a9-164">Connected factory preconfigured solution overview</span></span>](iot-suite-connected-factory-overview.md)
* <span data-ttu-id="b21a9-165">[Все аспекты безопасности Интернета вещей][lnk-security-groundup]</span><span class="sxs-lookup"><span data-stu-id="b21a9-165">[IoT security from the ground up][lnk-security-groundup]</span></span>

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
