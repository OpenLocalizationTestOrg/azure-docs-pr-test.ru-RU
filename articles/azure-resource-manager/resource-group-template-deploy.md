---
title: "Развертывание ресурсов с помощью PowerShell и шаблона | Документация Майкрософт"
description: "Узнайте, как использовать Azure Resource Manager и Azure PowerShell для развертывания ресурсов в Azure. Эти ресурсы определяются в шаблоне Resource Manager."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 55903f35-6c16-4c6d-bf52-dbf365605c3f
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: tomfitz
ms.openlocfilehash: 5f395abf8ebdfbac18fd17d8183b392673e280ec
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-azure-powershell"></a><span data-ttu-id="a944b-104">Развертывание ресурсов с использованием шаблонов Resource Manager и Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="a944b-104">Deploy resources with Resource Manager templates and Azure PowerShell</span></span>

<span data-ttu-id="a944b-105">В этом разделе объясняется, как использовать Azure PowerShell с шаблонами Resource Manager для развертывания ресурсов в Azure.</span><span class="sxs-lookup"><span data-stu-id="a944b-105">This topic explains how to use Azure PowerShell with Resource Manager templates to deploy your resources to Azure.</span></span> <span data-ttu-id="a944b-106">Если вы не знакомы с основными понятиями, связанными с развертыванием решений Azure и управлением ими, то см. [обзор Azure Resource Manager](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a944b-106">If you are not familiar with the concepts of deploying and managing your Azure solutions, see [Azure Resource Manager overview](resource-group-overview.md).</span></span>

<span data-ttu-id="a944b-107">Развертываемый шаблон Resource Manager может быть локальным файлом на вашем компьютере или внешним файлом, расположенным в репозитории, например в GitHub.</span><span class="sxs-lookup"><span data-stu-id="a944b-107">The Resource Manager template you deploy can either be a local file on your machine, or an external file that is located in a repository like GitHub.</span></span> <span data-ttu-id="a944b-108">Шаблон, развертываемый в этой статье, доступен в разделе [Пример шаблона](#sample-template) или как [шаблон учетной записи хранения в GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/101-storage-account-create/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="a944b-108">The template you deploy in this article is available in the [Sample template](#sample-template) section, or as [storage account template in GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/101-storage-account-create/azuredeploy.json).</span></span>

[!INCLUDE [sample-powershell-install](../../includes/sample-powershell-install.md)]

<a id="deploy-local-template" />

## <a name="deploy-a-template-from-your-local-machine"></a><span data-ttu-id="a944b-109">Развертывание шаблона с локального компьютера</span><span class="sxs-lookup"><span data-stu-id="a944b-109">Deploy a template from your local machine</span></span>

<span data-ttu-id="a944b-110">При развертывании ресурсов в Azure выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="a944b-110">When deploying resources to Azure, you:</span></span>

1. <span data-ttu-id="a944b-111">Вход в учетную запись Azure</span><span class="sxs-lookup"><span data-stu-id="a944b-111">Log in to your Azure account</span></span>
2. <span data-ttu-id="a944b-112">Создайте группу ресурсов, которая послужит в качестве контейнера для развертываемых ресурсов.</span><span class="sxs-lookup"><span data-stu-id="a944b-112">Create a resource group that serves as the container for the deployed resources.</span></span> <span data-ttu-id="a944b-113">Имя группы ресурсов может содержать только буквы, цифры, точки, знаки подчеркивания, дефисы и скобки.</span><span class="sxs-lookup"><span data-stu-id="a944b-113">The name of the resource group can only include alphanumeric characters, periods, underscores, hyphens, and parenthesis.</span></span> <span data-ttu-id="a944b-114">Оно может содержать до 90 знаков и</span><span class="sxs-lookup"><span data-stu-id="a944b-114">It can be up to 90 characters.</span></span> <span data-ttu-id="a944b-115">не может заканчиваться точкой.</span><span class="sxs-lookup"><span data-stu-id="a944b-115">It cannot end in a period.</span></span>
3. <span data-ttu-id="a944b-116">Разверните в группе ресурсов шаблон, определяющий ресурсы, которые необходимо создать.</span><span class="sxs-lookup"><span data-stu-id="a944b-116">Deploy to the resource group the template that defines the resources to create</span></span>

<span data-ttu-id="a944b-117">Шаблон может включать параметры, которые позволяют настроить развертывание.</span><span class="sxs-lookup"><span data-stu-id="a944b-117">A template can include parameters that enable you to customize the deployment.</span></span> <span data-ttu-id="a944b-118">Например, вы можете предоставить значения, предназначенные для конкретной среды (такой как среда разработки, тестирования и рабочая среда).</span><span class="sxs-lookup"><span data-stu-id="a944b-118">For example, you can provide values that are tailored for a particular environment (such as dev, test, and production).</span></span> <span data-ttu-id="a944b-119">Пример шаблона определяет параметр для номера SKU учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="a944b-119">The sample template defines a parameter for the storage account SKU.</span></span>

<span data-ttu-id="a944b-120">В следующем примере создается группа ресурсов и развертывается шаблон с локального компьютера:</span><span class="sxs-lookup"><span data-stu-id="a944b-120">The following example creates a resource group, and deploys a template from your local machine:</span></span>

```powershell
Login-AzureRmAccount
 
New-AzureRmResourceGroup -Name ExampleResourceGroup -Location "South Central US"
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateFile c:\MyTemplates\storage.json -storageAccountType Standard_GRS
```

<span data-ttu-id="a944b-121">Развертывание может занять несколько минут.</span><span class="sxs-lookup"><span data-stu-id="a944b-121">The deployment can take a few minutes to complete.</span></span> <span data-ttu-id="a944b-122">По завершении появится сообщение, содержащее результат:</span><span class="sxs-lookup"><span data-stu-id="a944b-122">When it finishes, you see a message that includes the result:</span></span>

```powershell
ProvisioningState       : Succeeded
```

## <a name="deploy-a-template-from-an-external-source"></a><span data-ttu-id="a944b-123">Развертывание шаблона из внешнего источника</span><span class="sxs-lookup"><span data-stu-id="a944b-123">Deploy a template from an external source</span></span>

<span data-ttu-id="a944b-124">Шаблоны Resource Manager можно хранить не на локальном компьютере, а на внешнем источнике.</span><span class="sxs-lookup"><span data-stu-id="a944b-124">Instead of storing Resource Manager templates on your local machine, you may prefer to store them in an external location.</span></span> <span data-ttu-id="a944b-125">Вы можете хранить шаблоны в репозитории системы управления версиями (например, GitHub).</span><span class="sxs-lookup"><span data-stu-id="a944b-125">You can store templates in a source control repository (such as GitHub).</span></span> <span data-ttu-id="a944b-126">А также их можно хранить в учетной записи хранения Azure для общего доступа в организации.</span><span class="sxs-lookup"><span data-stu-id="a944b-126">Or, you can store them in an Azure storage account for shared access in your organization.</span></span>

<span data-ttu-id="a944b-127">Для развертывания внешнего шаблона используйте параметр **TemplateUri**.</span><span class="sxs-lookup"><span data-stu-id="a944b-127">To deploy an external template, use the **TemplateUri** parameter.</span></span> <span data-ttu-id="a944b-128">Используйте универсальный код ресурса (URI) в примере для развертывания примера шаблона из GitHub.</span><span class="sxs-lookup"><span data-stu-id="a944b-128">Use the URI in the example to deploy the sample template from GitHub.</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json `
  -storageAccountType Standard_GRS
```

<span data-ttu-id="a944b-129">В предыдущем примере для шаблона требуется общедоступный код URI, который подходит для большинства сценариев, так как шаблон не должен содержать конфиденциальные данные.</span><span class="sxs-lookup"><span data-stu-id="a944b-129">The preceding example requires a publicly accessible URI for the template, which works for most scenarios because your template should not include sensitive data.</span></span> <span data-ttu-id="a944b-130">Если необходимо указать конфиденциальные данные (например, пароль администратора), то передайте это значение с помощью безопасного параметра.</span><span class="sxs-lookup"><span data-stu-id="a944b-130">If you need to specify sensitive data (like an admin password), pass that value as a secure parameter.</span></span> <span data-ttu-id="a944b-131">Но если вы не хотите, чтобы шаблон был общедоступным, то можно защитить его, сохранив в закрытом контейнере хранилища.</span><span class="sxs-lookup"><span data-stu-id="a944b-131">However, if you do not want your template to be publicly accessible, you can protect it by storing it in a private storage container.</span></span> <span data-ttu-id="a944b-132">Сведения о развертывании шаблона, требующего маркер подписанного URL-адреса (SAS), см. в статье [Развертывание частного шаблона Resource Manager с использованием токена SAS и Azure PowerShell](resource-manager-powershell-sas-token.md).</span><span class="sxs-lookup"><span data-stu-id="a944b-132">For information about deploying a template that requires a shared access signature (SAS) token, see [Deploy private template with SAS token](resource-manager-powershell-sas-token.md).</span></span>

## <a name="parameter-files"></a><span data-ttu-id="a944b-133">Файлы параметров</span><span class="sxs-lookup"><span data-stu-id="a944b-133">Parameter files</span></span>

<span data-ttu-id="a944b-134">Вместо передачи параметров в виде встроенных значений в сценарии вам может быть проще использовать JSON-файл, содержащий значения параметров.</span><span class="sxs-lookup"><span data-stu-id="a944b-134">Rather than passing parameters as inline values in your script, you may find it easier to use a JSON file that contains the parameter values.</span></span> <span data-ttu-id="a944b-135">Файл параметров должен быть в указанном ниже формате.</span><span class="sxs-lookup"><span data-stu-id="a944b-135">The parameter file must be in the following format:</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
     "storageAccountType": {
         "value": "Standard_GRS"
     }
  }
}
```

<span data-ttu-id="a944b-136">Обратите внимание, что раздел parameters содержит имя параметра, которое совпадает с параметром, определенным в шаблоне (storageAccountType).</span><span class="sxs-lookup"><span data-stu-id="a944b-136">Notice that the parameters section includes a parameter name that matches the parameter defined in your template (storageAccountType).</span></span> <span data-ttu-id="a944b-137">Файл параметров содержит значение для параметра.</span><span class="sxs-lookup"><span data-stu-id="a944b-137">The parameter file contains a value for the parameter.</span></span> <span data-ttu-id="a944b-138">Во время развертывания это значение автоматически передается в шаблон.</span><span class="sxs-lookup"><span data-stu-id="a944b-138">This value is automatically passed to the template during deployment.</span></span> <span data-ttu-id="a944b-139">Можно создать несколько файлов параметров для различных сценариев развертывания, а затем передать соответствующий файл параметров.</span><span class="sxs-lookup"><span data-stu-id="a944b-139">You can create multiple parameter files for different deployment scenarios, and then pass in the appropriate parameter file.</span></span> 

<span data-ttu-id="a944b-140">Скопируйте предыдущий пример и сохраните его как файл с именем `storage.parameters.json`.</span><span class="sxs-lookup"><span data-stu-id="a944b-140">Copy the preceding example and save it as a file named `storage.parameters.json`.</span></span>

<span data-ttu-id="a944b-141">Чтобы передать локальный файл параметров, используйте параметр **TemplateParameterFile**:</span><span class="sxs-lookup"><span data-stu-id="a944b-141">To pass a local parameter file, use the **TemplateParameterFile** parameter:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateFile c:\MyTemplates\storage.json `
  -TemplateParameterFile c:\MyTemplates\storage.parameters.json
```

<span data-ttu-id="a944b-142">Чтобы передать внешний файл параметров, используйте параметр **TemplateParameterUri**:</span><span class="sxs-lookup"><span data-stu-id="a944b-142">To pass an external parameter file, use the **TemplateParameterUri** parameter:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json `
  -TemplateParameterUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.parameters.json
```

<span data-ttu-id="a944b-143">Вы можете использовать в ходе одной операции развертывания как встроенные параметры, так и локальный файл параметров.</span><span class="sxs-lookup"><span data-stu-id="a944b-143">You can use inline parameters and a local parameter file in the same deployment operation.</span></span> <span data-ttu-id="a944b-144">Например, часть значений можно указать в локальном файле параметров, а другую часть — в команде развертывания.</span><span class="sxs-lookup"><span data-stu-id="a944b-144">For example, you can specify some values in the local parameter file and add other values inline during deployment.</span></span> <span data-ttu-id="a944b-145">Если значения для одного параметра указаны одновременно и в локальном файле параметров, и в командной строке, более высокий приоритет имеет значение из командной строки.</span><span class="sxs-lookup"><span data-stu-id="a944b-145">If you provide values for a parameter in both the local parameter file and inline, the inline value takes precedence.</span></span>

<span data-ttu-id="a944b-146">Тем не менее при использовании внешнего файла параметров нельзя передавать другие значения в командной строке или локальном файле.</span><span class="sxs-lookup"><span data-stu-id="a944b-146">However, when you use an external parameter file, you cannot pass other values either inline or from a local file.</span></span> <span data-ttu-id="a944b-147">Если в параметре **TemplateParameterUri** указан файл параметров, все параметры командной строки игнорируются.</span><span class="sxs-lookup"><span data-stu-id="a944b-147">When you specify a parameter file in the **TemplateParameterUri** parameter, all inline parameters are ignored.</span></span> <span data-ttu-id="a944b-148">Все значения параметров следует указать во внешнем файле.</span><span class="sxs-lookup"><span data-stu-id="a944b-148">Provide all parameter values in the external file.</span></span> <span data-ttu-id="a944b-149">Если в шаблоне используется конфиденциальное значение, которое нельзя включать в файл параметров, то его можно передать в хранилище ключей. Кроме того, можно динамически указать значения всех параметров в командной строке.</span><span class="sxs-lookup"><span data-stu-id="a944b-149">If your template includes a sensitive value that you cannot include in the parameter file, either add that value to a key vault, or dynamically provide all parameter values inline.</span></span>

<span data-ttu-id="a944b-150">Если шаблон содержит параметр, имя которого совпадает с именем одного из параметров в команде PowerShell, параметр из шаблон отображается с постфиксом **FromTemplate**.</span><span class="sxs-lookup"><span data-stu-id="a944b-150">If your template includes a parameter with the same name as one of the parameters in the PowerShell command, PowerShell presents the parameter from your template with the postfix **FromTemplate**.</span></span> <span data-ttu-id="a944b-151">Предположим, что параметр **ResourceGroupName** в шаблоне конфликтует с параметром **ResourceGroupName** в командлете [New-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment).</span><span class="sxs-lookup"><span data-stu-id="a944b-151">For example, a parameter named **ResourceGroupName** in your template conflicts with the **ResourceGroupName** parameter in the [New-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment) cmdlet.</span></span> <span data-ttu-id="a944b-152">Вам будет предложено указать значение для параметра **ResourceGroupNameFromTemplate**.</span><span class="sxs-lookup"><span data-stu-id="a944b-152">You are prompted to provide a value for **ResourceGroupNameFromTemplate**.</span></span> <span data-ttu-id="a944b-153">В общем случае следует избегать этой путаницы, не присваивая параметрам имена параметров, используемых для операций развертывания.</span><span class="sxs-lookup"><span data-stu-id="a944b-153">In general, you should avoid this confusion by not naming parameters with the same name as parameters used for deployment operations.</span></span>

## <a name="test-a-template-deployment"></a><span data-ttu-id="a944b-154">Тестовое развертывание шаблона</span><span class="sxs-lookup"><span data-stu-id="a944b-154">Test a template deployment</span></span>

<span data-ttu-id="a944b-155">Чтобы проверить шаблон и значения параметров без фактического развертывания ресурсов, используйте [Test-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/test-azurermresourcegroupdeployment).</span><span class="sxs-lookup"><span data-stu-id="a944b-155">To test your template and parameter values without actually deploying any resources, use [Test-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/test-azurermresourcegroupdeployment).</span></span> 

```powershell
Test-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateFile c:\MyTemplates\storage.json -storageAccountType Standard_GRS
```

<span data-ttu-id="a944b-156">Если ошибок не обнаружено, то команда завершается без ответа.</span><span class="sxs-lookup"><span data-stu-id="a944b-156">If no errors are detected, the command finishes without a response.</span></span> <span data-ttu-id="a944b-157">Если обнаруживается ошибка, то команда возвращает сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="a944b-157">If an error is detected, the command returns an error message.</span></span> <span data-ttu-id="a944b-158">Например, при попытке передать недопустимое значение для номера SKU учетной записи хранения возвращается следующая ошибка:</span><span class="sxs-lookup"><span data-stu-id="a944b-158">For example, attempting to pass an incorrect value for the storage account SKU, returns the following error:</span></span>

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName testgroup `
  -TemplateFile c:\MyTemplates\storage.json -storageAccountType badSku

Code    : InvalidTemplate
Message : Deployment template validation failed: 'The provided value 'badSku' for the template parameter 'storageAccountType'
          at line '15' and column '24' is not valid. The parameter value is not part of the allowed value(s):
          'Standard_LRS,Standard_ZRS,Standard_GRS,Standard_RAGRS,Premium_LRS'.'.
Details :
```

<span data-ttu-id="a944b-159">Если шаблон содержит синтаксическую ошибку, то команда возвращает сообщение об ошибке, указывающее, что ей не удалось проанализировать шаблон.</span><span class="sxs-lookup"><span data-stu-id="a944b-159">If your template has a syntax error, the command returns an error indicating it could not parse the template.</span></span> <span data-ttu-id="a944b-160">В сообщении указывается номер строки и позиция ошибки синтаксического анализа.</span><span class="sxs-lookup"><span data-stu-id="a944b-160">The message indicates the line number and position of the parsing error.</span></span>

```powershell
Test-AzureRmResourceGroupDeployment : After parsing a value an unexpected character was encountered: 
  ". Path 'variables', line 31, position 3.
```

[!INCLUDE [resource-manager-deployments](../../includes/resource-manager-deployments.md)]

<span data-ttu-id="a944b-161">Чтобы использовать полный режим, используйте параметр `Mode`.</span><span class="sxs-lookup"><span data-stu-id="a944b-161">To use complete mode, use the `Mode` parameter:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Mode Complete -Name ExampleDeployment `
  -ResourceGroupName ExampleResourceGroup -TemplateFile c:\MyTemplates\storage.json 
```

## <a name="sample-template"></a><span data-ttu-id="a944b-162">Пример шаблона</span><span class="sxs-lookup"><span data-stu-id="a944b-162">Sample template</span></span>

<span data-ttu-id="a944b-163">Для примеров в этой статье используется следующий шаблон.</span><span class="sxs-lookup"><span data-stu-id="a944b-163">The following template is used for the examples in this topic.</span></span> <span data-ttu-id="a944b-164">Скопируйте и сохраните его как файл с именем storage.json.</span><span class="sxs-lookup"><span data-stu-id="a944b-164">Copy and save it as a file named storage.json.</span></span> <span data-ttu-id="a944b-165">Сведения о создании этого шаблона см. в статье [Создание первого шаблона Azure Resource Manager](resource-manager-create-first-template.md).</span><span class="sxs-lookup"><span data-stu-id="a944b-165">To understand how to create this template, see [Create your first Azure Resource Manager template](resource-manager-create-first-template.md).</span></span>  

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageAccountType": {
      "type": "string",
      "defaultValue": "Standard_LRS",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS",
        "Standard_ZRS",
        "Premium_LRS"
      ],
      "metadata": {
        "description": "Storage Account type"
      }
    }
  },
  "variables": {
    "storageAccountName": "[concat(uniquestring(resourceGroup().id), 'standardsa')]"
  },
  "resources": [
    {
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[variables('storageAccountName')]",
      "apiVersion": "2016-01-01",
      "location": "[resourceGroup().location]",
      "sku": {
          "name": "[parameters('storageAccountType')]"
      },
      "kind": "Storage", 
      "properties": {
      }
    }
  ],
  "outputs": {
      "storageAccountName": {
          "type": "string",
          "value": "[variables('storageAccountName')]"
      }
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="a944b-166">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a944b-166">Next steps</span></span>
* <span data-ttu-id="a944b-167">В примерах этой статьи ресурсы развертываются в группу ресурсов в подписке по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="a944b-167">The examples in this article deploy resources to a resource group in your default subscription.</span></span> <span data-ttu-id="a944b-168">Чтобы использовать другую подписку, см. статью [Управление несколькими подписками Azure](/powershell/azure/manage-subscriptions-azureps).</span><span class="sxs-lookup"><span data-stu-id="a944b-168">To use a different subscription, see [Manage multiple Azure subscriptions](/powershell/azure/manage-subscriptions-azureps).</span></span>
* <span data-ttu-id="a944b-169">Полный пример сценария, развертывающего шаблон, см. в статье [Сценарий для развертывания шаблона Resource Manager](resource-manager-samples-powershell-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="a944b-169">For a complete sample script that deploys a template, see [Resource Manager template deployment script](resource-manager-samples-powershell-deploy.md).</span></span>
* <span data-ttu-id="a944b-170">Сведения об определении параметров в шаблоне см. в статье [Описание структуры и синтаксиса шаблонов Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="a944b-170">To understand how to define parameters in your template, see [Understand the structure and syntax of Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="a944b-171">Советы по устранению распространенных ошибок развертывания см. в разделе [Устранение распространенных ошибок развертывания в Azure с помощью Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="a944b-171">For tips on resolving common deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="a944b-172">Сведения о развертывании шаблона, которому нужен токен SAS, см. в статье [Развертывание частного шаблона с помощью маркера SAS](resource-manager-powershell-sas-token.md).</span><span class="sxs-lookup"><span data-stu-id="a944b-172">For information about deploying a template that requires a SAS token, see [Deploy private template with SAS token](resource-manager-powershell-sas-token.md).</span></span>
* <span data-ttu-id="a944b-173">Руководство по использованию Resource Manager для эффективного управления подписками в организациях см [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md) (Шаблон Azure для организаций. Рекомендуемая система управления подпиской).</span><span class="sxs-lookup"><span data-stu-id="a944b-173">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

