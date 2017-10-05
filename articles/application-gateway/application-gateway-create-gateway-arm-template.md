---
title: "Создание шлюза приложений Azure с помощью шаблонов | Документация Майкрософт"
description: "На этой странице приводятся инструкции по созданию шлюза приложений Azure с помощью шаблона диспетчера ресурсов Azure."
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
ms.openlocfilehash: 46cca89ccb5bd77d57fabc3e9027fcebd38da8e7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-application-gateway-by-using-the-azure-resource-manager-template"></a><span data-ttu-id="b26b6-103">Создание шлюза приложений с помощью шаблона диспетчера ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="b26b6-103">Create an application gateway by using the Azure Resource Manager template</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="b26b6-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="b26b6-104">Azure portal</span></span>](application-gateway-create-gateway-portal.md)
> * [<span data-ttu-id="b26b6-105">PowerShell и диспетчер ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="b26b6-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-gateway-arm.md)
> * [<span data-ttu-id="b26b6-106">Классическая модель — Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="b26b6-106">Azure Classic PowerShell</span></span>](application-gateway-create-gateway.md)
> * [<span data-ttu-id="b26b6-107">Шаблон диспетчера ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="b26b6-107">Azure Resource Manager template</span></span>](application-gateway-create-gateway-arm-template.md)
> * [<span data-ttu-id="b26b6-108">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="b26b6-108">Azure CLI</span></span>](application-gateway-create-gateway-cli.md)

<span data-ttu-id="b26b6-109">Шлюз приложений — это балансировщик нагрузки уровня 7.</span><span class="sxs-lookup"><span data-stu-id="b26b6-109">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="b26b6-110">Он отвечает за отработку отказов и эффективную маршрутизацию HTTP-запросов между разными серверами (облачными и локальными).</span><span class="sxs-lookup"><span data-stu-id="b26b6-110">It provides failover and performance-routing HTTP requests between different servers, whether they are on the cloud or on-premises.</span></span> <span data-ttu-id="b26b6-111">Шлюз приложений выполняет многие функции контроллера доставки приложений (ADC), включая балансировку нагрузки HTTP, определение сходства сеансов на основе файлов cookie, разгрузку SSL, выполнение пользовательской проверки работоспособности, поддержку нескольких сайтов и т. д.</span><span class="sxs-lookup"><span data-stu-id="b26b6-111">Application Gateway provides many application delivery controller (ADC) features including HTTP load balancing, cookie-based session affinity, Secure Sockets Layer (SSL) offload, custom health probes, support for multi-site, and many others.</span></span> <span data-ttu-id="b26b6-112">Полный список поддерживаемых функций представлен в [обзоре шлюза приложений](application-gateway-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b26b6-112">To find a complete list of supported features, visit [Application Gateway overview](application-gateway-introduction.md)</span></span>

<span data-ttu-id="b26b6-113">В этой статье вы узнаете, как скачать и изменить существующий шаблон Azure Resource Manager из GitHub, а также развернуть шаблон из GitHub, PowerShell и интерфейса командной строки Azure (Azure CLI).</span><span class="sxs-lookup"><span data-stu-id="b26b6-113">This article walks you through downloading and modifying an existing Azure Resource Manager template from GitHub and deploying the template from GitHub, PowerShell, and the Azure CLI.</span></span>

<span data-ttu-id="b26b6-114">Если вы развертываете шаблон ARM непосредственно из GitHub без изменений, перейдите к соответствующему разделу.</span><span class="sxs-lookup"><span data-stu-id="b26b6-114">If you are simply deploying the Azure Resource Manager template directly from GitHub without any changes, skip to deploy a template from GitHub.</span></span>

## <a name="scenario"></a><span data-ttu-id="b26b6-115">Сценарий</span><span class="sxs-lookup"><span data-stu-id="b26b6-115">Scenario</span></span>

<span data-ttu-id="b26b6-116">Из этой статьи вы узнаете:</span><span class="sxs-lookup"><span data-stu-id="b26b6-116">In this scenario you will:</span></span>

* <span data-ttu-id="b26b6-117">как создать шлюз приложений с брандмауэром веб-приложения;</span><span class="sxs-lookup"><span data-stu-id="b26b6-117">Create an application gateway with web application firewall.</span></span>
* <span data-ttu-id="b26b6-118">как создать виртуальную сеть с именем VirtualNetwork1 и зарезервированным блоком CIDR (10.0.0.0/16);</span><span class="sxs-lookup"><span data-stu-id="b26b6-118">Create a virtual network named VirtualNetwork1 with a reserved CIDR block of 10.0.0.0/16.</span></span>
* <span data-ttu-id="b26b6-119">как создать подсеть с именем Appgatewaysubnet и блоком CIDR (10.0.0.0/28);</span><span class="sxs-lookup"><span data-stu-id="b26b6-119">Create a subnet called Appgatewaysubnet that uses 10.0.0.0/28 as its CIDR block.</span></span>
* <span data-ttu-id="b26b6-120">как задать два ранее настроенных внутренних IP-адреса для веб-серверов, которые будут балансировать трафик.</span><span class="sxs-lookup"><span data-stu-id="b26b6-120">Set up two previously configured back-end IPs for the web servers you want to load balance the traffic.</span></span> <span data-ttu-id="b26b6-121">В этом примере в качестве внутренних IP-адресов используются адреса 10.0.1.10 и 10.0.1.11.</span><span class="sxs-lookup"><span data-stu-id="b26b6-121">In this template example, the back-end IPs are 10.0.1.10 and 10.0.1.11.</span></span>

> [!NOTE]
> <span data-ttu-id="b26b6-122">Приведенные значения представляют в этом шаблоне параметры.</span><span class="sxs-lookup"><span data-stu-id="b26b6-122">Those settings are the parameters for this template.</span></span> <span data-ttu-id="b26b6-123">Чтобы настроить шаблон, можно изменить правила, прослушиватель, SSL и другие параметры в файле azuredeploy.json.</span><span class="sxs-lookup"><span data-stu-id="b26b6-123">To customize the template, you can change rules, the listener, SSL, and other options in the azuredeploy.json file.</span></span>

![Сценарий](./media/application-gateway-create-gateway-arm-template/scenario.png)

## <a name="download-and-understand-the-azure-resource-manager-template"></a><span data-ttu-id="b26b6-125">Скачивание и использование шаблона диспетчера ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="b26b6-125">Download and understand the Azure Resource Manager template</span></span>

<span data-ttu-id="b26b6-126">Вы можете скачать из GitHub уже существующий шаблон диспетчера ресурсов Azure (ARM), чтобы создать виртуальную сеть и две подсети, а также внести в него нужные изменения и применить.</span><span class="sxs-lookup"><span data-stu-id="b26b6-126">You can download the existing Azure Resource Manager template to create a virtual network and two subnets from GitHub, make any changes you might want, and reuse it.</span></span> <span data-ttu-id="b26b6-127">Для этого выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="b26b6-127">To do so, use the following steps:</span></span>

1. <span data-ttu-id="b26b6-128">Перейдите к статье [Create Application Gateway with web application firewall enabled](https://github.com/Azure/azure-quickstart-templates/tree/master/101-application-gateway-waf) (Создание шлюза приложения с включенным брандмауэром веб-приложений).</span><span class="sxs-lookup"><span data-stu-id="b26b6-128">Navigate to [Create Application Gateway with web application firewall enabled](https://github.com/Azure/azure-quickstart-templates/tree/master/101-application-gateway-waf).</span></span>
1. <span data-ttu-id="b26b6-129">Щелкните **azuredeploy.json** и нажмите кнопку **RAW**.</span><span class="sxs-lookup"><span data-stu-id="b26b6-129">Click **azuredeploy.json**, and then click **RAW**.</span></span>
1. <span data-ttu-id="b26b6-130">Сохраните файл в локальную папку на своем компьютере.</span><span class="sxs-lookup"><span data-stu-id="b26b6-130">Save the file to a local folder on your computer.</span></span>
1. <span data-ttu-id="b26b6-131">Если вы знакомы с шаблонами ARM, перейдите к шагу 7.</span><span class="sxs-lookup"><span data-stu-id="b26b6-131">If you are familiar with Azure Resource Manager templates, skip to step 7.</span></span>
1. <span data-ttu-id="b26b6-132">Откройте только что сохраненный файл и просмотрите содержимое раздела **parameters** в строке</span><span class="sxs-lookup"><span data-stu-id="b26b6-132">Open the file that you saved and look at the contents under **parameters** in line</span></span>
1. <span data-ttu-id="b26b6-133">В параметрах шаблона ARM есть заполнитель для значений, которые могут подставляться во время развертывания.</span><span class="sxs-lookup"><span data-stu-id="b26b6-133">Azure Resource Manager template parameters provide a placeholder for values that can be filled out during deployment.</span></span>

  | <span data-ttu-id="b26b6-134">Параметр</span><span class="sxs-lookup"><span data-stu-id="b26b6-134">Parameter</span></span> | <span data-ttu-id="b26b6-135">Описание</span><span class="sxs-lookup"><span data-stu-id="b26b6-135">Description</span></span> |
  | --- | --- |
  | <span data-ttu-id="b26b6-136">**subnetPrefix**</span><span class="sxs-lookup"><span data-stu-id="b26b6-136">**subnetPrefix**</span></span> |<span data-ttu-id="b26b6-137">Блок CIDR для подсети шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="b26b6-137">CIDR block for the application gateway subnet.</span></span> |
  | <span data-ttu-id="b26b6-138">**applicationGatewaySize**</span><span class="sxs-lookup"><span data-stu-id="b26b6-138">**applicationGatewaySize**</span></span> | <span data-ttu-id="b26b6-139">Размер шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="b26b6-139">Size of the application gateway.</span></span>  <span data-ttu-id="b26b6-140">WAF позволяет только средний и крупный.</span><span class="sxs-lookup"><span data-stu-id="b26b6-140">WAF only allows medium and large.</span></span> |
  | <span data-ttu-id="b26b6-141">**backendIpaddress1**</span><span class="sxs-lookup"><span data-stu-id="b26b6-141">**backendIpaddress1**</span></span> |<span data-ttu-id="b26b6-142">IP-адрес первого веб-сервера.</span><span class="sxs-lookup"><span data-stu-id="b26b6-142">IP address of the first web server.</span></span> |
  | <span data-ttu-id="b26b6-143">**backendIpaddress2**</span><span class="sxs-lookup"><span data-stu-id="b26b6-143">**backendIpaddress2**</span></span> |<span data-ttu-id="b26b6-144">IP-адрес второго веб-сервера.</span><span class="sxs-lookup"><span data-stu-id="b26b6-144">IP address of the second web server.</span></span> |
  | <span data-ttu-id="b26b6-145">**wafEnabled**</span><span class="sxs-lookup"><span data-stu-id="b26b6-145">**wafEnabled**</span></span> | <span data-ttu-id="b26b6-146">Параметр, определяющий, включен ли WAF.</span><span class="sxs-lookup"><span data-stu-id="b26b6-146">Setting to determine if WAF is enabled.</span></span>|
  | <span data-ttu-id="b26b6-147">**wafMode**</span><span class="sxs-lookup"><span data-stu-id="b26b6-147">**wafMode**</span></span> | <span data-ttu-id="b26b6-148">Режим брандмауэра веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="b26b6-148">Mode of the web application firewall.</span></span>  <span data-ttu-id="b26b6-149">Доступные варианты: **Предотвращение** или **Защита**.</span><span class="sxs-lookup"><span data-stu-id="b26b6-149">Available options are **prevention** or **detection**.</span></span>|
  | <span data-ttu-id="b26b6-150">**wafRuleSetType**</span><span class="sxs-lookup"><span data-stu-id="b26b6-150">**wafRuleSetType**</span></span> | <span data-ttu-id="b26b6-151">Тип набора правил для WAF.</span><span class="sxs-lookup"><span data-stu-id="b26b6-151">Ruleset type for WAF.</span></span>  <span data-ttu-id="b26b6-152">В настоящее время поддерживается только OWASP.</span><span class="sxs-lookup"><span data-stu-id="b26b6-152">Currently OWASP is the only supported option.</span></span> |
  | <span data-ttu-id="b26b6-153">**wafRuleSetVersion**</span><span class="sxs-lookup"><span data-stu-id="b26b6-153">**wafRuleSetVersion**</span></span> |<span data-ttu-id="b26b6-154">Версия набора правил.</span><span class="sxs-lookup"><span data-stu-id="b26b6-154">Ruleset version.</span></span> <span data-ttu-id="b26b6-155">Поддерживаются только OWASP CRS 2.2.9 и 3.0.</span><span class="sxs-lookup"><span data-stu-id="b26b6-155">OWASP CRS 2.2.9 and 3.0 are currently the supported options.</span></span> |

1. <span data-ttu-id="b26b6-156">Проверьте содержимое раздела **resources** и обратите внимание на следующие свойства.</span><span class="sxs-lookup"><span data-stu-id="b26b6-156">Check the content under **resources** and notice the following properties:</span></span>

   * <span data-ttu-id="b26b6-157">**type**.</span><span class="sxs-lookup"><span data-stu-id="b26b6-157">**type**.</span></span> <span data-ttu-id="b26b6-158">Тип ресурса, созданного на основе шаблона.</span><span class="sxs-lookup"><span data-stu-id="b26b6-158">Type of resource being created by the template.</span></span> <span data-ttu-id="b26b6-159">В этом случае используется тип `Microsoft.Network/applicationGateways`, представляющий шлюз приложений.</span><span class="sxs-lookup"><span data-stu-id="b26b6-159">In this case, the type is `Microsoft.Network/applicationGateways`, which represents an application gateway.</span></span>
   * <span data-ttu-id="b26b6-160">**name**.</span><span class="sxs-lookup"><span data-stu-id="b26b6-160">**name**.</span></span> <span data-ttu-id="b26b6-161">Имя ресурса.</span><span class="sxs-lookup"><span data-stu-id="b26b6-161">Name for the resource.</span></span> <span data-ttu-id="b26b6-162">Обратите внимание на применение `[parameters('applicationGatewayName')]`. Эта строка кода означает, что имя предоставляется пользователем или извлекается из файла параметров при развертывании.</span><span class="sxs-lookup"><span data-stu-id="b26b6-162">Notice the use of `[parameters('applicationGatewayName')]`, which means that the name is provided as input by you or by a parameter file during deployment.</span></span>
   * <span data-ttu-id="b26b6-163">**properties**.</span><span class="sxs-lookup"><span data-stu-id="b26b6-163">**properties**.</span></span> <span data-ttu-id="b26b6-164">Список свойств для ресурса.</span><span class="sxs-lookup"><span data-stu-id="b26b6-164">List of properties for the resource.</span></span> <span data-ttu-id="b26b6-165">Во время создания шлюза приложений этот шаблон использует виртуальную сеть и общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="b26b6-165">This template uses the virtual network and public IP address during application gateway creation.</span></span>

   > [!NOTE]
   > <span data-ttu-id="b26b6-166">Дополнительные сведения о шаблонах Resource Manager см. [здесь](/templates/).</span><span class="sxs-lookup"><span data-stu-id="b26b6-166">For more information on templates visit: [Resource Manager templates reference](/templates/)</span></span>

1. <span data-ttu-id="b26b6-167">Вернитесь на страницу [https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf/](https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf).</span><span class="sxs-lookup"><span data-stu-id="b26b6-167">Navigate back to [https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf/](https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf).</span></span>
1. <span data-ttu-id="b26b6-168">Щелкните **azuredeploy-parameters.json** и нажмите кнопку **RAW**.</span><span class="sxs-lookup"><span data-stu-id="b26b6-168">Click **azuredeploy-parameters.json**, and then click **RAW**.</span></span>
1. <span data-ttu-id="b26b6-169">Сохраните файл в локальную папку на своем компьютере.</span><span class="sxs-lookup"><span data-stu-id="b26b6-169">Save the file to a local folder on your computer.</span></span>
1. <span data-ttu-id="b26b6-170">Откройте сохраненный файл и измените значения параметров.</span><span class="sxs-lookup"><span data-stu-id="b26b6-170">Open the file that you saved and edit the values for the parameters.</span></span> <span data-ttu-id="b26b6-171">Чтобы развернуть шлюз приложений в соответствии с задачами этого руководства, используйте следующие значения.</span><span class="sxs-lookup"><span data-stu-id="b26b6-171">Use the following values to deploy the application gateway described in our scenario.</span></span>

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

1. <span data-ttu-id="b26b6-172">Сохраните файл.</span><span class="sxs-lookup"><span data-stu-id="b26b6-172">Save the file.</span></span> <span data-ttu-id="b26b6-173">Вы можете проверить шаблон JSON и шаблон параметров с помощью таких веб-инструментов проверки JSON, как [JSlint.com](http://www.jslint.com/).</span><span class="sxs-lookup"><span data-stu-id="b26b6-173">You can test the JSON template and parameter template by using online JSON validation tools like [JSlint.com](http://www.jslint.com/).</span></span>

## <a name="deploy-the-azure-resource-manager-template-by-using-powershell"></a><span data-ttu-id="b26b6-174">Развертывание шаблона диспетчера ресурсов Azure с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="b26b6-174">Deploy the Azure Resource Manager template by using PowerShell</span></span>

<span data-ttu-id="b26b6-175">Если вы ранее не использовали Azure PowerShell, то ознакомьтесь со статьей об [установке и настройке Azure PowerShell](/powershell/azure/overview). Следуйте инструкциям, приведенным в статье, чтобы войти в Azure и выбрать подписку.</span><span class="sxs-lookup"><span data-stu-id="b26b6-175">If you have never used Azure PowerShell, visit: [How to install and configure Azure PowerShell](/powershell/azure/overview) and follow the instructions to sign into Azure and select your subscription.</span></span>

1. <span data-ttu-id="b26b6-176">Войдите в PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b26b6-176">Login to PowerShell</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

1. <span data-ttu-id="b26b6-177">Просмотрите подписки учетной записи.</span><span class="sxs-lookup"><span data-stu-id="b26b6-177">Check the subscriptions for the account.</span></span>

    ```powershell
    Get-AzureRmSubscription
    ```

    <span data-ttu-id="b26b6-178">Вам будет предложено указать свои учетные данные для проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="b26b6-178">You are prompted to authenticate with your credentials.</span></span>

1. <span data-ttu-id="b26b6-179">Выберите подписку Azure.</span><span class="sxs-lookup"><span data-stu-id="b26b6-179">Choose which of your Azure subscriptions to use.</span></span>

    ```powershell
    Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
    ```

1. <span data-ttu-id="b26b6-180">При необходимости создайте новую группу ресурсов с помощью командлета **New-AzureResourceGroup** .</span><span class="sxs-lookup"><span data-stu-id="b26b6-180">If needed, create a resource group by using the **New-AzureResourceGroup** cmdlet.</span></span> <span data-ttu-id="b26b6-181">В примере ниже создается группа ресурсов с именем AppgatewayRG, расположенная в восточной части США.</span><span class="sxs-lookup"><span data-stu-id="b26b6-181">In the following example, you create a resource group called AppgatewayRG in East US location.</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name AppgatewayRG -Location "West US"
    ```

1. <span data-ttu-id="b26b6-182">Запустите командлет **New-AzureRmResourceGroupDeployment** , чтобы развернуть новую виртуальную сеть с помощью шаблона и файлов параметров, которые вы скачали и изменили ранее.</span><span class="sxs-lookup"><span data-stu-id="b26b6-182">Run the **New-AzureRmResourceGroupDeployment** cmdlet to deploy the new virtual network by using the preceding template and parameter files you downloaded and modified.</span></span>
    
    ```powershell
    New-AzureRmResourceGroupDeployment -Name TestAppgatewayDeployment -ResourceGroupName AppgatewayRG `
    -TemplateFile C:\ARM\azuredeploy.json -TemplateParameterFile C:\ARM\azuredeploy-parameters.json
    ```

## <a name="deploy-the-azure-resource-manager-template-by-using-the-azure-cli"></a><span data-ttu-id="b26b6-183">Развертывание шаблона ARM с помощью интерфейса командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="b26b6-183">Deploy the Azure Resource Manager template by using the Azure CLI</span></span>

<span data-ttu-id="b26b6-184">Чтобы развернуть шаблон ARM, скачанный с помощью Azure CLI, выполните следующее.</span><span class="sxs-lookup"><span data-stu-id="b26b6-184">To deploy the Azure Resource Manager template you downloaded by using Azure CLI, follow the following steps:</span></span>

1. <span data-ttu-id="b26b6-185">Если вы еще не использовали Azure CLI, ознакомьтесь со статьей [Установка и настройка CLI Azure](/cli/azure/install-azure-cli) и следуйте инструкциям вплоть до выбора учетной записи Azure и подписки.</span><span class="sxs-lookup"><span data-stu-id="b26b6-185">If you have never used Azure CLI, see [Install and configure the Azure CLI](/cli/azure/install-azure-cli) and follow the instructions up to the point where you select your Azure account and subscription.</span></span>

1. <span data-ttu-id="b26b6-186">При необходимости выполните команду `az group create`, как показано во фрагменте кода ниже, чтобы создать группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="b26b6-186">If necessary, run the `az group create` command to create a resource group, as shown in the following code snippet.</span></span> <span data-ttu-id="b26b6-187">Обратите внимание на результат выполнения команды.</span><span class="sxs-lookup"><span data-stu-id="b26b6-187">Notice the output of the command.</span></span> <span data-ttu-id="b26b6-188">В списке, который откроется после выполнения команды, будут указаны используемые параметры.</span><span class="sxs-lookup"><span data-stu-id="b26b6-188">The list shown after the output explains the parameters used.</span></span> <span data-ttu-id="b26b6-189">Дополнительные сведения о группах ресурсов см. в статье [Общие сведения о диспетчере ресурсов Azure](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b26b6-189">For more information about resource groups, visit [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

    ```azurecli
    az group create --location westus --name appgatewayRG
    ```
    
    <span data-ttu-id="b26b6-190">**-n (или --name)**.</span><span class="sxs-lookup"><span data-stu-id="b26b6-190">**-n (or --name)**.</span></span> <span data-ttu-id="b26b6-191">Имя для новой группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="b26b6-191">Name for the new resource group.</span></span> <span data-ttu-id="b26b6-192">В нашем примере это *appgatewayRG*.</span><span class="sxs-lookup"><span data-stu-id="b26b6-192">For our scenario, it's *appgatewayRG*.</span></span>
    
    <span data-ttu-id="b26b6-193">**-l (или --location)**.</span><span class="sxs-lookup"><span data-stu-id="b26b6-193">**-l (or --location)**.</span></span> <span data-ttu-id="b26b6-194">Регион Azure, в котором создается группа ресурсов.</span><span class="sxs-lookup"><span data-stu-id="b26b6-194">Azure region where the new resource group is created.</span></span> <span data-ttu-id="b26b6-195">В нашем примере это *westus*.</span><span class="sxs-lookup"><span data-stu-id="b26b6-195">For our scenario, it's *westus*.</span></span>

1. <span data-ttu-id="b26b6-196">Выполните командлет `az group deployment create`, чтобы развернуть новую виртуальную сеть с помощью шаблона и файлов параметров, которые вы скачали и изменили на предыдущем шаге.</span><span class="sxs-lookup"><span data-stu-id="b26b6-196">Run the `az group deployment create` cmdlet to deploy the new virtual network by using the template and parameter files you downloaded and modified in the preceding step.</span></span> <span data-ttu-id="b26b6-197">В списке, который откроется после выполнения команды, будут указаны используемые параметры.</span><span class="sxs-lookup"><span data-stu-id="b26b6-197">The list shown after the output explains the parameters used.</span></span>

    ```azurecli
    az group deployment create --resource-group appgatewayRG --name TestAppgatewayDeployment --template-file azuredeploy.json --parameters @azuredeploy-parameters.json
    ```

## <a name="deploy-the-azure-resource-manager-template-by-using-click-to-deploy"></a><span data-ttu-id="b26b6-198">Развертывание шаблона ARM с помощью интерфейса кнопки развертывания</span><span class="sxs-lookup"><span data-stu-id="b26b6-198">Deploy the Azure Resource Manager template by using click-to-deploy</span></span>

<span data-ttu-id="b26b6-199">Развертывание с помощью кнопки развертывания — еще один способ использования шаблонов ARM.</span><span class="sxs-lookup"><span data-stu-id="b26b6-199">Click-to-deploy is another way to use Azure Resource Manager templates.</span></span> <span data-ttu-id="b26b6-200">Он позволяет быстро и удобно работать с шаблонами на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="b26b6-200">It's an easy way to use templates with the Azure portal.</span></span>

1. <span data-ttu-id="b26b6-201">Перейдите к статье о [создании шлюза приложений с брандмауэром веб-приложения](https://azure.microsoft.com/documentation/templates/101-application-gateway-waf/).</span><span class="sxs-lookup"><span data-stu-id="b26b6-201">Go to [Create an application gateway with web application firewall](https://azure.microsoft.com/documentation/templates/101-application-gateway-waf/).</span></span>

1. <span data-ttu-id="b26b6-202">Нажмите кнопку **Развернуть в Azure**.</span><span class="sxs-lookup"><span data-stu-id="b26b6-202">Click **Deploy to Azure**.</span></span>

    ![Развернуть в Azure](./media/application-gateway-create-gateway-arm-template/deploytoazure.png)
    
1. <span data-ttu-id="b26b6-204">На портале укажите параметры шаблона развертывания и нажмите кнопку **OК**.</span><span class="sxs-lookup"><span data-stu-id="b26b6-204">Fill out the parameters for the deployment template on the portal and click **OK**.</span></span>

    ![Параметры](./media/application-gateway-create-gateway-arm-template/ibiza1.png)
    
1. <span data-ttu-id="b26b6-206">Установите флажок **Я принимаю указанные выше условия** и нажмите кнопку **Приобрести**.</span><span class="sxs-lookup"><span data-stu-id="b26b6-206">Select **I agree to the terms and conditions stated above** and click **Purchase**.</span></span>

1. <span data-ttu-id="b26b6-207">В колонке "Настраиваемое развертывание" щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="b26b6-207">On the Custom deployment blade, click **Create**.</span></span>

## <a name="providing-certificate-data-to-resource-manager-templates"></a><span data-ttu-id="b26b6-208">Добавление данных сертификата в шаблоны Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b26b6-208">Providing certificate data to Resource Manager templates</span></span>

<span data-ttu-id="b26b6-209">При использовании протокола SSL с шаблоном сертификат необходимо указать в виде строки в формате base64, а не передать его.</span><span class="sxs-lookup"><span data-stu-id="b26b6-209">When using SSL with a template, the certificate needs to be provided in a base64 string instead of being uploaded.</span></span> <span data-ttu-id="b26b6-210">Для преобразования PFX- или CER-файла в строку base64, используйте одну из следующих команд.</span><span class="sxs-lookup"><span data-stu-id="b26b6-210">To convert a .pfx or .cer to a base64 string use one of the following commands.</span></span> <span data-ttu-id="b26b6-211">Следующие команды преобразуют сертификат в строку base64, которую можно указать для шаблона.</span><span class="sxs-lookup"><span data-stu-id="b26b6-211">The following commands convert the certificate to a base64 string, which can be provided to the template.</span></span> <span data-ttu-id="b26b6-212">Ожидаемым результатом является строка, которую можно сохранить в переменной и вставить в шаблон.</span><span class="sxs-lookup"><span data-stu-id="b26b6-212">The expected output is a string that can be stored in a variable and pasted in the template.</span></span>

### <a name="macos"></a><span data-ttu-id="b26b6-213">macOS</span><span class="sxs-lookup"><span data-stu-id="b26b6-213">macOS</span></span>
```bash
cert=$( base64 <certificate path and name>.pfx )
echo $cert
```

### <a name="windows"></a><span data-ttu-id="b26b6-214">Windows</span><span class="sxs-lookup"><span data-stu-id="b26b6-214">Windows</span></span>
```powershell
[System.Convert]::ToBase64String([System.IO.File]::ReadAllBytes("<certificate path and name>.pfx"))
```

## <a name="delete-all-resources"></a><span data-ttu-id="b26b6-215">Удаление всех ресурсов</span><span class="sxs-lookup"><span data-stu-id="b26b6-215">Delete all resources</span></span>

<span data-ttu-id="b26b6-216">Чтобы удалить все ресурсы, созданные в этой статье, выполните одно из следующих действий:</span><span class="sxs-lookup"><span data-stu-id="b26b6-216">To delete all resources created in this article, complete one of the following steps:</span></span>

### <a name="powershell"></a><span data-ttu-id="b26b6-217">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b26b6-217">PowerShell</span></span>

```powershell
Remove-AzureRmResourceGroup -Name appgatewayRG
```

### <a name="azure-cli"></a><span data-ttu-id="b26b6-218">Инфраструктура CLI Azure</span><span class="sxs-lookup"><span data-stu-id="b26b6-218">Azure CLI</span></span>

```azurecli
az group delete --name appgatewayRG
```

## <a name="next-steps"></a><span data-ttu-id="b26b6-219">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b26b6-219">Next steps</span></span>

<span data-ttu-id="b26b6-220">Чтобы настроить разгрузку SSL, ознакомьтесь с [настройкой шлюза приложений для разгрузки SSL](application-gateway-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="b26b6-220">If you want to configure SSL offload, visit: [Configure an application gateway for SSL offload](application-gateway-ssl.md).</span></span>

<span data-ttu-id="b26b6-221">Указания по настройке шлюза приложений для использования с внутренним балансировщиком нагрузки см. в статье [Создание шлюза приложений с внутренней подсистемой балансировщика нагрузки (ILB)](application-gateway-ilb.md).</span><span class="sxs-lookup"><span data-stu-id="b26b6-221">If you want to configure an application gateway to use with an internal load balancer, visit: [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

<span data-ttu-id="b26b6-222">Дополнительные сведения о параметрах балансировки нагрузки в целом см. в статьях:</span><span class="sxs-lookup"><span data-stu-id="b26b6-222">If you want more information about load balancing options in general, visit:</span></span>

* [<span data-ttu-id="b26b6-223">Подсистема балансировщика нагрузки Azure</span><span class="sxs-lookup"><span data-stu-id="b26b6-223">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="b26b6-224">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="b26b6-224">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

