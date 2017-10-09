---
title: "Шлюз приложений Azure — шаблоны aaaCreate | Документы Microsoft"
description: "Эта страница содержит toocreate инструкции шлюза приложения Azure с помощью шаблона Azure Resource Manager hello"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: fc18e553852551326d6a302abe2c7f8a08c2eb6c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-by-using-hello-azure-resource-manager-template"></a><span data-ttu-id="0cd43-103">Создание шлюза приложения с помощью шаблона Azure Resource Manager hello</span><span class="sxs-lookup"><span data-stu-id="0cd43-103">Create an application gateway by using hello Azure Resource Manager template</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="0cd43-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="0cd43-104">Azure portal</span></span>](application-gateway-create-gateway-portal.md)
> * [<span data-ttu-id="0cd43-105">PowerShell и диспетчер ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="0cd43-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-gateway-arm.md)
> * [<span data-ttu-id="0cd43-106">Классическая модель — Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="0cd43-106">Azure Classic PowerShell</span></span>](application-gateway-create-gateway.md)
> * [<span data-ttu-id="0cd43-107">Шаблон диспетчера ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="0cd43-107">Azure Resource Manager template</span></span>](application-gateway-create-gateway-arm-template.md)
> * [<span data-ttu-id="0cd43-108">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="0cd43-108">Azure CLI</span></span>](application-gateway-create-gateway-cli.md)

<span data-ttu-id="0cd43-109">Шлюз приложений — это балансировщик нагрузки уровня 7.</span><span class="sxs-lookup"><span data-stu-id="0cd43-109">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="0cd43-110">Он предоставляет отработки отказа и маршрутизации производительности HTTP-запросов между различными серверами, являются ли они на hello облачной или локальной.</span><span class="sxs-lookup"><span data-stu-id="0cd43-110">It provides failover and performance-routing HTTP requests between different servers, whether they are on hello cloud or on-premises.</span></span> <span data-ttu-id="0cd43-111">Шлюз приложений выполняет многие функции контроллера доставки приложений (ADC), включая балансировку нагрузки HTTP, определение сходства сеансов на основе файлов cookie, разгрузку SSL, выполнение пользовательской проверки работоспособности, поддержку нескольких сайтов и т. д.</span><span class="sxs-lookup"><span data-stu-id="0cd43-111">Application Gateway provides many application delivery controller (ADC) features including HTTP load balancing, cookie-based session affinity, Secure Sockets Layer (SSL) offload, custom health probes, support for multi-site, and many others.</span></span> <span data-ttu-id="0cd43-112">Полный список поддерживаемых функций toofind посетите [Обзор шлюза приложения](application-gateway-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="0cd43-112">toofind a complete list of supported features, visit [Application Gateway overview](application-gateway-introduction.md)</span></span>

<span data-ttu-id="0cd43-113">В этой статье описывается загрузка и изменение существующего шаблона диспетчера ресурсов Azure из GitHub и развертывания шаблона hello из GitHub, PowerShell и hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="0cd43-113">This article walks you through downloading and modifying an existing Azure Resource Manager template from GitHub and deploying hello template from GitHub, PowerShell, and hello Azure CLI.</span></span>

<span data-ttu-id="0cd43-114">При развертывании просто hello шаблона диспетчера ресурсов Azure непосредственно из GitHub без изменений, пропустите toodeploy шаблона в GitHub.</span><span class="sxs-lookup"><span data-stu-id="0cd43-114">If you are simply deploying hello Azure Resource Manager template directly from GitHub without any changes, skip toodeploy a template from GitHub.</span></span>

## <a name="scenario"></a><span data-ttu-id="0cd43-115">Сценарий</span><span class="sxs-lookup"><span data-stu-id="0cd43-115">Scenario</span></span>

<span data-ttu-id="0cd43-116">Из этой статьи вы узнаете:</span><span class="sxs-lookup"><span data-stu-id="0cd43-116">In this scenario you will:</span></span>

* <span data-ttu-id="0cd43-117">как создать шлюз приложений с брандмауэром веб-приложения;</span><span class="sxs-lookup"><span data-stu-id="0cd43-117">Create an application gateway with web application firewall.</span></span>
* <span data-ttu-id="0cd43-118">как создать виртуальную сеть с именем VirtualNetwork1 и зарезервированным блоком CIDR (10.0.0.0/16);</span><span class="sxs-lookup"><span data-stu-id="0cd43-118">Create a virtual network named VirtualNetwork1 with a reserved CIDR block of 10.0.0.0/16.</span></span>
* <span data-ttu-id="0cd43-119">как создать подсеть с именем Appgatewaysubnet и блоком CIDR (10.0.0.0/28);</span><span class="sxs-lookup"><span data-stu-id="0cd43-119">Create a subnet called Appgatewaysubnet that uses 10.0.0.0/28 as its CIDR block.</span></span>
* <span data-ttu-id="0cd43-120">Требуется настроить два ранее настроенный серверной части IP-адреса для веб-серверов hello tooload Балансировка трафика hello.</span><span class="sxs-lookup"><span data-stu-id="0cd43-120">Set up two previously configured back-end IPs for hello web servers you want tooload balance hello traffic.</span></span> <span data-ttu-id="0cd43-121">В этом примере шаблон hello серверной части IP-адреса являются 10.0.1.10 и 10.0.1.11.</span><span class="sxs-lookup"><span data-stu-id="0cd43-121">In this template example, hello back-end IPs are 10.0.1.10 and 10.0.1.11.</span></span>

> [!NOTE]
> <span data-ttu-id="0cd43-122">Эти параметры являются параметрами hello для этого шаблона.</span><span class="sxs-lookup"><span data-stu-id="0cd43-122">Those settings are hello parameters for this template.</span></span> <span data-ttu-id="0cd43-123">toocustomize hello шаблона, можно изменить правила, прослушиватель hello, SSL и другие параметры в файле azuredeploy.json hello.</span><span class="sxs-lookup"><span data-stu-id="0cd43-123">toocustomize hello template, you can change rules, hello listener, SSL, and other options in hello azuredeploy.json file.</span></span>

![Сценарий](./media/application-gateway-create-gateway-arm-template/scenario.png)

## <a name="download-and-understand-hello-azure-resource-manager-template"></a><span data-ttu-id="0cd43-125">Загрузите и понять hello шаблона диспетчера ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="0cd43-125">Download and understand hello Azure Resource Manager template</span></span>

<span data-ttu-id="0cd43-126">Можно загрузить шаблон toocreate hello существующего диспетчера ресурсов Azure виртуальной сети и две подсети из GitHub, внесите изменения можно будет и использовать его.</span><span class="sxs-lookup"><span data-stu-id="0cd43-126">You can download hello existing Azure Resource Manager template toocreate a virtual network and two subnets from GitHub, make any changes you might want, and reuse it.</span></span> <span data-ttu-id="0cd43-127">Таким образом, toodo используйте hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="0cd43-127">toodo so, use hello following steps:</span></span>

1. <span data-ttu-id="0cd43-128">Перейдите в слишком[создать шлюз приложения при включенном брандмауэре приложения web](https://github.com/Azure/azure-quickstart-templates/tree/master/101-application-gateway-waf).</span><span class="sxs-lookup"><span data-stu-id="0cd43-128">Navigate too[Create Application Gateway with web application firewall enabled](https://github.com/Azure/azure-quickstart-templates/tree/master/101-application-gateway-waf).</span></span>
1. <span data-ttu-id="0cd43-129">Щелкните **azuredeploy.json** и нажмите кнопку **RAW**.</span><span class="sxs-lookup"><span data-stu-id="0cd43-129">Click **azuredeploy.json**, and then click **RAW**.</span></span>
1. <span data-ttu-id="0cd43-130">Сохранение hello файл tooa локальную папку на компьютере.</span><span class="sxs-lookup"><span data-stu-id="0cd43-130">Save hello file tooa local folder on your computer.</span></span>
1. <span data-ttu-id="0cd43-131">Если вы знакомы с шаблоны Azure Resource Manager, пропустите toostep 7.</span><span class="sxs-lookup"><span data-stu-id="0cd43-131">If you are familiar with Azure Resource Manager templates, skip toostep 7.</span></span>
1. <span data-ttu-id="0cd43-132">Откройте сохраненный файл hello и просмотрите содержимое hello в **параметры** в строке</span><span class="sxs-lookup"><span data-stu-id="0cd43-132">Open hello file that you saved and look at hello contents under **parameters** in line</span></span>
1. <span data-ttu-id="0cd43-133">В параметрах шаблона ARM есть заполнитель для значений, которые могут подставляться во время развертывания.</span><span class="sxs-lookup"><span data-stu-id="0cd43-133">Azure Resource Manager template parameters provide a placeholder for values that can be filled out during deployment.</span></span>

  | <span data-ttu-id="0cd43-134">Параметр</span><span class="sxs-lookup"><span data-stu-id="0cd43-134">Parameter</span></span> | <span data-ttu-id="0cd43-135">Описание</span><span class="sxs-lookup"><span data-stu-id="0cd43-135">Description</span></span> |
  | --- | --- |
  | <span data-ttu-id="0cd43-136">**subnetPrefix**</span><span class="sxs-lookup"><span data-stu-id="0cd43-136">**subnetPrefix**</span></span> |<span data-ttu-id="0cd43-137">Блок CIDR для подсети шлюза приложения hello.</span><span class="sxs-lookup"><span data-stu-id="0cd43-137">CIDR block for hello application gateway subnet.</span></span> |
  | <span data-ttu-id="0cd43-138">**applicationGatewaySize**</span><span class="sxs-lookup"><span data-stu-id="0cd43-138">**applicationGatewaySize**</span></span> | <span data-ttu-id="0cd43-139">Размер шлюза приложения hello.</span><span class="sxs-lookup"><span data-stu-id="0cd43-139">Size of hello application gateway.</span></span>  <span data-ttu-id="0cd43-140">WAF позволяет только средний и крупный.</span><span class="sxs-lookup"><span data-stu-id="0cd43-140">WAF only allows medium and large.</span></span> |
  | <span data-ttu-id="0cd43-141">**backendIpaddress1**</span><span class="sxs-lookup"><span data-stu-id="0cd43-141">**backendIpaddress1**</span></span> |<span data-ttu-id="0cd43-142">IP-адрес hello первого веб-сервера.</span><span class="sxs-lookup"><span data-stu-id="0cd43-142">IP address of hello first web server.</span></span> |
  | <span data-ttu-id="0cd43-143">**backendIpaddress2**</span><span class="sxs-lookup"><span data-stu-id="0cd43-143">**backendIpaddress2**</span></span> |<span data-ttu-id="0cd43-144">IP-адрес hello второй веб-сервер.</span><span class="sxs-lookup"><span data-stu-id="0cd43-144">IP address of hello second web server.</span></span> |
  | <span data-ttu-id="0cd43-145">**wafEnabled**</span><span class="sxs-lookup"><span data-stu-id="0cd43-145">**wafEnabled**</span></span> | <span data-ttu-id="0cd43-146">Параметр toodetermine, если включен WAF.</span><span class="sxs-lookup"><span data-stu-id="0cd43-146">Setting toodetermine if WAF is enabled.</span></span>|
  | <span data-ttu-id="0cd43-147">**wafMode**</span><span class="sxs-lookup"><span data-stu-id="0cd43-147">**wafMode**</span></span> | <span data-ttu-id="0cd43-148">Режим hello брандмауэр веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="0cd43-148">Mode of hello web application firewall.</span></span>  <span data-ttu-id="0cd43-149">Доступные варианты: **Предотвращение** или **Защита**.</span><span class="sxs-lookup"><span data-stu-id="0cd43-149">Available options are **prevention** or **detection**.</span></span>|
  | <span data-ttu-id="0cd43-150">**wafRuleSetType**</span><span class="sxs-lookup"><span data-stu-id="0cd43-150">**wafRuleSetType**</span></span> | <span data-ttu-id="0cd43-151">Тип набора правил для WAF.</span><span class="sxs-lookup"><span data-stu-id="0cd43-151">Ruleset type for WAF.</span></span>  <span data-ttu-id="0cd43-152">В настоящее время OWASP — hello поддерживается только параметр.</span><span class="sxs-lookup"><span data-stu-id="0cd43-152">Currently OWASP is hello only supported option.</span></span> |
  | <span data-ttu-id="0cd43-153">**wafRuleSetVersion**</span><span class="sxs-lookup"><span data-stu-id="0cd43-153">**wafRuleSetVersion**</span></span> |<span data-ttu-id="0cd43-154">Версия набора правил.</span><span class="sxs-lookup"><span data-stu-id="0cd43-154">Ruleset version.</span></span> <span data-ttu-id="0cd43-155">CRS OWASP 2.2.9 и 3.0 в настоящий момент параметры hello поддерживается.</span><span class="sxs-lookup"><span data-stu-id="0cd43-155">OWASP CRS 2.2.9 and 3.0 are currently hello supported options.</span></span> |

1. <span data-ttu-id="0cd43-156">Проверьте содержимое hello в **ресурсов** и уведомление hello следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="0cd43-156">Check hello content under **resources** and notice hello following properties:</span></span>

   * <span data-ttu-id="0cd43-157">**type**.</span><span class="sxs-lookup"><span data-stu-id="0cd43-157">**type**.</span></span> <span data-ttu-id="0cd43-158">Тип ресурса, создаваемого шаблоном hello.</span><span class="sxs-lookup"><span data-stu-id="0cd43-158">Type of resource being created by hello template.</span></span> <span data-ttu-id="0cd43-159">В этом случае тип hello — `Microsoft.Network/applicationGateways`, который представляет шлюз приложений.</span><span class="sxs-lookup"><span data-stu-id="0cd43-159">In this case, hello type is `Microsoft.Network/applicationGateways`, which represents an application gateway.</span></span>
   * <span data-ttu-id="0cd43-160">**name**.</span><span class="sxs-lookup"><span data-stu-id="0cd43-160">**name**.</span></span> <span data-ttu-id="0cd43-161">Имя ресурса hello.</span><span class="sxs-lookup"><span data-stu-id="0cd43-161">Name for hello resource.</span></span> <span data-ttu-id="0cd43-162">Использование уведомления hello `[parameters('applicationGatewayName')]`, что означает это имя hello предоставляется как вход пользователем или файл параметров во время развертывания.</span><span class="sxs-lookup"><span data-stu-id="0cd43-162">Notice hello use of `[parameters('applicationGatewayName')]`, which means that hello name is provided as input by you or by a parameter file during deployment.</span></span>
   * <span data-ttu-id="0cd43-163">**properties**.</span><span class="sxs-lookup"><span data-stu-id="0cd43-163">**properties**.</span></span> <span data-ttu-id="0cd43-164">Список свойств для ресурса hello.</span><span class="sxs-lookup"><span data-stu-id="0cd43-164">List of properties for hello resource.</span></span> <span data-ttu-id="0cd43-165">Этот шаблон использует hello виртуальную сеть и общедоступный IP-адрес во время создания шлюза приложения.</span><span class="sxs-lookup"><span data-stu-id="0cd43-165">This template uses hello virtual network and public IP address during application gateway creation.</span></span>

   > [!NOTE]
   > <span data-ttu-id="0cd43-166">Дополнительные сведения о шаблонах Resource Manager см. [здесь](/templates/).</span><span class="sxs-lookup"><span data-stu-id="0cd43-166">For more information on templates visit: [Resource Manager templates reference](/templates/)</span></span>

1. <span data-ttu-id="0cd43-167">Переход назад слишком[https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf/](https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf).</span><span class="sxs-lookup"><span data-stu-id="0cd43-167">Navigate back too[https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf/](https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf).</span></span>
1. <span data-ttu-id="0cd43-168">Щелкните **azuredeploy-parameters.json** и нажмите кнопку **RAW**.</span><span class="sxs-lookup"><span data-stu-id="0cd43-168">Click **azuredeploy-parameters.json**, and then click **RAW**.</span></span>
1. <span data-ttu-id="0cd43-169">Сохранение hello файл tooa локальную папку на компьютере.</span><span class="sxs-lookup"><span data-stu-id="0cd43-169">Save hello file tooa local folder on your computer.</span></span>
1. <span data-ttu-id="0cd43-170">Откройте сохраненный файл hello и отредактируйте hello значения для параметров hello.</span><span class="sxs-lookup"><span data-stu-id="0cd43-170">Open hello file that you saved and edit hello values for hello parameters.</span></span> <span data-ttu-id="0cd43-171">Используйте следующие значения toodeploy hello приложения шлюза, описанной в нашем сценарии hello.</span><span class="sxs-lookup"><span data-stu-id="0cd43-171">Use hello following values toodeploy hello application gateway described in our scenario.</span></span>

    ```json
    {
        "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "addressPrefix": {
            "value": "10.0.0.0/16"
            },
            "subnetPrefix": {
            "value": "10.0.0.0/28"
            },
            "applicationGatewaySize": {
            "value": "WAF_Medium"
            },
            "capacity": {
            "value": 2
            },
            "backendIpAddress1": {
            "value": "10.0.1.10"
            },
            "backendIpAddress2": {
            "value": "10.0.1.11"
            },
            "wafEnabled": {
            "value": true
            },
            "wafMode": {
            "value": "Detection"
            },
            "wafRuleSetType": {
            "value": "OWASP"
            },
            "wafRuleSetVersion": {
            "value": "3.0"
            }
        }
    }
    ```

1. <span data-ttu-id="0cd43-172">Сохраните файл hello.</span><span class="sxs-lookup"><span data-stu-id="0cd43-172">Save hello file.</span></span> <span data-ttu-id="0cd43-173">Можно проверить hello JSON и параметра шаблона с помощью документации средства проверки JSON, как [JSlint.com](http://www.jslint.com/).</span><span class="sxs-lookup"><span data-stu-id="0cd43-173">You can test hello JSON template and parameter template by using online JSON validation tools like [JSlint.com](http://www.jslint.com/).</span></span>

## <a name="deploy-hello-azure-resource-manager-template-by-using-powershell"></a><span data-ttu-id="0cd43-174">Развертывание шаблона hello диспетчера ресурсов Azure с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="0cd43-174">Deploy hello Azure Resource Manager template by using PowerShell</span></span>

<span data-ttu-id="0cd43-175">Если ранее не пользовались Azure PowerShell, посетите: [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview) и следуйте инструкциям toosign hello в Azure и выберите свою подписку.</span><span class="sxs-lookup"><span data-stu-id="0cd43-175">If you have never used Azure PowerShell, visit: [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) and follow hello instructions toosign into Azure and select your subscription.</span></span>

1. <span data-ttu-id="0cd43-176">TooPowerShell входа</span><span class="sxs-lookup"><span data-stu-id="0cd43-176">Login tooPowerShell</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

1. <span data-ttu-id="0cd43-177">Проверьте hello подписки для учетной записи hello.</span><span class="sxs-lookup"><span data-stu-id="0cd43-177">Check hello subscriptions for hello account.</span></span>

    ```powershell
    Get-AzureRmSubscription
    ```

    <span data-ttu-id="0cd43-178">С помощью учетных данных, запрашиваемых tooauthenticate.</span><span class="sxs-lookup"><span data-stu-id="0cd43-178">You are prompted tooauthenticate with your credentials.</span></span>

1. <span data-ttu-id="0cd43-179">Выберите, какие toouse вашей подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="0cd43-179">Choose which of your Azure subscriptions toouse.</span></span>

    ```powershell
    Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
    ```

1. <span data-ttu-id="0cd43-180">При необходимости создайте группу ресурсов с помощью hello **New AzureResourceGroup** командлета.</span><span class="sxs-lookup"><span data-stu-id="0cd43-180">If needed, create a resource group by using hello **New-AzureResourceGroup** cmdlet.</span></span> <span data-ttu-id="0cd43-181">В следующем примере hello создать группу ресурсов под названием AppgatewayRG в расположении, восток США.</span><span class="sxs-lookup"><span data-stu-id="0cd43-181">In hello following example, you create a resource group called AppgatewayRG in East US location.</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name AppgatewayRG -Location "West US"
    ```

1. <span data-ttu-id="0cd43-182">Запустите hello **New AzureRmResourceGroupDeployment** командлет toodeploy hello новую виртуальную сеть с помощью hello предшествующий файлы шаблонов и параметров загрузки и изменения.</span><span class="sxs-lookup"><span data-stu-id="0cd43-182">Run hello **New-AzureRmResourceGroupDeployment** cmdlet toodeploy hello new virtual network by using hello preceding template and parameter files you downloaded and modified.</span></span>
    
    ```powershell
    New-AzureRmResourceGroupDeployment -Name TestAppgatewayDeployment -ResourceGroupName AppgatewayRG `
    -TemplateFile C:\ARM\azuredeploy.json -TemplateParameterFile C:\ARM\azuredeploy-parameters.json
    ```

## <a name="deploy-hello-azure-resource-manager-template-by-using-hello-azure-cli"></a><span data-ttu-id="0cd43-183">Развертывание с помощью Azure CLI hello hello шаблона диспетчера ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="0cd43-183">Deploy hello Azure Resource Manager template by using hello Azure CLI</span></span>

<span data-ttu-id="0cd43-184">toodeploy hello Azure Resource Manager загруженный шаблон с помощью Azure CLI, выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="0cd43-184">toodeploy hello Azure Resource Manager template you downloaded by using Azure CLI, follow hello following steps:</span></span>

1. <span data-ttu-id="0cd43-185">Если ранее не пользовались Azure CLI, см. раздел [установить и настроить hello Azure CLI](/cli/azure/install-azure-cli) и следуйте инструкциям hello toohello точку, где выбирается учетная запись Azure и подписки.</span><span class="sxs-lookup"><span data-stu-id="0cd43-185">If you have never used Azure CLI, see [Install and configure hello Azure CLI](/cli/azure/install-azure-cli) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>

1. <span data-ttu-id="0cd43-186">При необходимости выполнения hello `az group create` команда toocreate группы ресурсов, как показано в следующий фрагмент кода hello.</span><span class="sxs-lookup"><span data-stu-id="0cd43-186">If necessary, run hello `az group create` command toocreate a resource group, as shown in hello following code snippet.</span></span> <span data-ttu-id="0cd43-187">Обратите внимание, hello выходные данные команды hello.</span><span class="sxs-lookup"><span data-stu-id="0cd43-187">Notice hello output of hello command.</span></span> <span data-ttu-id="0cd43-188">Список Hello отображаться после вывода hello объясняется hello параметров, используемых.</span><span class="sxs-lookup"><span data-stu-id="0cd43-188">hello list shown after hello output explains hello parameters used.</span></span> <span data-ttu-id="0cd43-189">Дополнительные сведения о группах ресурсов см. в статье [Общие сведения о диспетчере ресурсов Azure](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0cd43-189">For more information about resource groups, visit [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

    ```azurecli
    az group create --location westus --name appgatewayRG
    ```
    
    <span data-ttu-id="0cd43-190">**-n (или --name)**.</span><span class="sxs-lookup"><span data-stu-id="0cd43-190">**-n (or --name)**.</span></span> <span data-ttu-id="0cd43-191">Имя для новой группы ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="0cd43-191">Name for hello new resource group.</span></span> <span data-ttu-id="0cd43-192">В нашем примере это *appgatewayRG*.</span><span class="sxs-lookup"><span data-stu-id="0cd43-192">For our scenario, it's *appgatewayRG*.</span></span>
    
    <span data-ttu-id="0cd43-193">**-l (или --location)**.</span><span class="sxs-lookup"><span data-stu-id="0cd43-193">**-l (or --location)**.</span></span> <span data-ttu-id="0cd43-194">Регион Azure, где создается новая группа ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="0cd43-194">Azure region where hello new resource group is created.</span></span> <span data-ttu-id="0cd43-195">В нашем примере это *westus*.</span><span class="sxs-lookup"><span data-stu-id="0cd43-195">For our scenario, it's *westus*.</span></span>

1. <span data-ttu-id="0cd43-196">Запустите hello `az group deployment create` командлет toodeploy hello новую виртуальную сеть с помощью шаблона hello и параметр файлы загружены и изменен в предшествующих шаг hello.</span><span class="sxs-lookup"><span data-stu-id="0cd43-196">Run hello `az group deployment create` cmdlet toodeploy hello new virtual network by using hello template and parameter files you downloaded and modified in hello preceding step.</span></span> <span data-ttu-id="0cd43-197">Список Hello отображаться после вывода hello объясняется hello параметров, используемых.</span><span class="sxs-lookup"><span data-stu-id="0cd43-197">hello list shown after hello output explains hello parameters used.</span></span>

    ```azurecli
    az group deployment create --resource-group appgatewayRG --name TestAppgatewayDeployment --template-file azuredeploy.json --parameters @azuredeploy-parameters.json
    ```

## <a name="deploy-hello-azure-resource-manager-template-by-using-click-to-deploy"></a><span data-ttu-id="0cd43-198">Развертывание шаблона hello Azure Resource Manager с помощью щелкните развертывание</span><span class="sxs-lookup"><span data-stu-id="0cd43-198">Deploy hello Azure Resource Manager template by using click-to-deploy</span></span>

<span data-ttu-id="0cd43-199">Нажмите кнопку развертывания является другим способом toouse шаблоны Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="0cd43-199">Click-to-deploy is another way toouse Azure Resource Manager templates.</span></span> <span data-ttu-id="0cd43-200">Это легко toouse шаблонов hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="0cd43-200">It's an easy way toouse templates with hello Azure portal.</span></span>

1. <span data-ttu-id="0cd43-201">Go слишком[создать шлюз приложений с брандмауэр веб-приложения](https://azure.microsoft.com/documentation/templates/101-application-gateway-waf/).</span><span class="sxs-lookup"><span data-stu-id="0cd43-201">Go too[Create an application gateway with web application firewall](https://azure.microsoft.com/documentation/templates/101-application-gateway-waf/).</span></span>

1. <span data-ttu-id="0cd43-202">Нажмите кнопку **развертывание tooAzure**.</span><span class="sxs-lookup"><span data-stu-id="0cd43-202">Click **Deploy tooAzure**.</span></span>

    ![Развертывание tooAzure](./media/application-gateway-create-gateway-arm-template/deploytoazure.png)
    
1. <span data-ttu-id="0cd43-204">Заполните параметры hello hello шаблон развертывания на портале hello и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="0cd43-204">Fill out hello parameters for hello deployment template on hello portal and click **OK**.</span></span>

    ![Параметры](./media/application-gateway-create-gateway-arm-template/ibiza1.png)
    
1. <span data-ttu-id="0cd43-206">Выберите **я принимаю условия, указанных выше, toohello** и нажмите кнопку **покупки**.</span><span class="sxs-lookup"><span data-stu-id="0cd43-206">Select **I agree toohello terms and conditions stated above** and click **Purchase**.</span></span>

1. <span data-ttu-id="0cd43-207">В колонке развертывания пользовательского hello, нажмите кнопку **создать**.</span><span class="sxs-lookup"><span data-stu-id="0cd43-207">On hello Custom deployment blade, click **Create**.</span></span>

## <a name="providing-certificate-data-tooresource-manager-templates"></a><span data-ttu-id="0cd43-208">Предоставление сертификата tooResource данных диспетчер шаблонов</span><span class="sxs-lookup"><span data-stu-id="0cd43-208">Providing certificate data tooResource Manager templates</span></span>

<span data-ttu-id="0cd43-209">При использовании SSL с помощью шаблона, hello сертификат должен toobe в строку base64, вместо загружена.</span><span class="sxs-lookup"><span data-stu-id="0cd43-209">When using SSL with a template, hello certificate needs toobe provided in a base64 string instead of being uploaded.</span></span> <span data-ttu-id="0cd43-210">Строка base64 tooa PFX или CER tooconvert используйте одну из hello, следующие команды.</span><span class="sxs-lookup"><span data-stu-id="0cd43-210">tooconvert a .pfx or .cer tooa base64 string use one of hello following commands.</span></span> <span data-ttu-id="0cd43-211">Hello ниже команды преобразуют hello сертификат tooa base64 строку, которая может быть указано toohello шаблона.</span><span class="sxs-lookup"><span data-stu-id="0cd43-211">hello following commands convert hello certificate tooa base64 string, which can be provided toohello template.</span></span> <span data-ttu-id="0cd43-212">Hello тесты на ожидаемые выходные данные — это строка, хранится в переменной и вставить в шаблоне hello.</span><span class="sxs-lookup"><span data-stu-id="0cd43-212">hello expected output is a string that can be stored in a variable and pasted in hello template.</span></span>

### <a name="macos"></a><span data-ttu-id="0cd43-213">macOS</span><span class="sxs-lookup"><span data-stu-id="0cd43-213">macOS</span></span>
```bash
cert=$( base64 <certificate path and name>.pfx )
echo $cert
```

### <a name="windows"></a><span data-ttu-id="0cd43-214">Windows</span><span class="sxs-lookup"><span data-stu-id="0cd43-214">Windows</span></span>
```powershell
[System.Convert]::ToBase64String([System.IO.File]::ReadAllBytes("<certificate path and name>.pfx"))
```

## <a name="delete-all-resources"></a><span data-ttu-id="0cd43-215">Удаление всех ресурсов</span><span class="sxs-lookup"><span data-stu-id="0cd43-215">Delete all resources</span></span>

<span data-ttu-id="0cd43-216">toodelete все ресурсы, которые созданы в этой статье, выполнение одного из hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="0cd43-216">toodelete all resources created in this article, complete one of hello following steps:</span></span>

### <a name="powershell"></a><span data-ttu-id="0cd43-217">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0cd43-217">PowerShell</span></span>

```powershell
Remove-AzureRmResourceGroup -Name appgatewayRG
```

### <a name="azure-cli"></a><span data-ttu-id="0cd43-218">Инфраструктура CLI Azure</span><span class="sxs-lookup"><span data-stu-id="0cd43-218">Azure CLI</span></span>

```azurecli
az group delete --name appgatewayRG
```

## <a name="next-steps"></a><span data-ttu-id="0cd43-219">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0cd43-219">Next steps</span></span>

<span data-ttu-id="0cd43-220">Если вы хотите tooconfigure разгрузки SSL, посетите: [настройки шлюза приложения для разгрузки SSL](application-gateway-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="0cd43-220">If you want tooconfigure SSL offload, visit: [Configure an application gateway for SSL offload](application-gateway-ssl.md).</span></span>

<span data-ttu-id="0cd43-221">Если вы хотите tooconfigure toouse шлюза приложения с внутренней подсистемы балансировки нагрузки, посетите: [создать шлюз приложений с внутренней подсистемы балансировки нагрузки (ILB)](application-gateway-ilb.md).</span><span class="sxs-lookup"><span data-stu-id="0cd43-221">If you want tooconfigure an application gateway toouse with an internal load balancer, visit: [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

<span data-ttu-id="0cd43-222">Дополнительные сведения о параметрах балансировки нагрузки в целом см. в статьях:</span><span class="sxs-lookup"><span data-stu-id="0cd43-222">If you want more information about load balancing options in general, visit:</span></span>

* [<span data-ttu-id="0cd43-223">Подсистема балансировщика нагрузки Azure</span><span class="sxs-lookup"><span data-stu-id="0cd43-223">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="0cd43-224">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="0cd43-224">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

