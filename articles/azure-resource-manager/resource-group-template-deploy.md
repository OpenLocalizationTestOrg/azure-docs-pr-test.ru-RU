---
title: "aaaDeploy ресурсы с помощью PowerShell и шаблона | Документы Microsoft"
description: "С помощью диспетчера ресурсов Azure и Azure PowerShell toodeploy tooAzure ресурсов. Hello ресурсы определяются в шаблоне диспетчера ресурсов."
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
ms.openlocfilehash: 41506811ba3c2ea5df6313db70978ade50f71161
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-azure-powershell"></a><span data-ttu-id="88940-104">Развертывание ресурсов с использованием шаблонов Resource Manager и Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="88940-104">Deploy resources with Resource Manager templates and Azure PowerShell</span></span>

<span data-ttu-id="88940-105">В этом разделе объясняется, как toouse Azure PowerShell с toodeploy шаблонов диспетчера ресурсов вашей tooAzure ресурсов.</span><span class="sxs-lookup"><span data-stu-id="88940-105">This topic explains how toouse Azure PowerShell with Resource Manager templates toodeploy your resources tooAzure.</span></span> <span data-ttu-id="88940-106">Если вы не знакомы с основными понятиями hello развертывания и управлению решения Azure см [Обзор диспетчера ресурсов Azure](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="88940-106">If you are not familiar with hello concepts of deploying and managing your Azure solutions, see [Azure Resource Manager overview](resource-group-overview.md).</span></span>

<span data-ttu-id="88940-107">шаблон диспетчера ресурсов Hello развертывание может быть локальный файл на компьютере или внешнем файле, расположенном в репозитория GitHub.</span><span class="sxs-lookup"><span data-stu-id="88940-107">hello Resource Manager template you deploy can either be a local file on your machine, or an external file that is located in a repository like GitHub.</span></span> <span data-ttu-id="88940-108">шаблон Hello развертывания в этой статье доступен в hello [образец шаблона](#sample-template) раздел, или как [шаблона учетной записи хранилища в GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/101-storage-account-create/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="88940-108">hello template you deploy in this article is available in hello [Sample template](#sample-template) section, or as [storage account template in GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/101-storage-account-create/azuredeploy.json).</span></span>

[!INCLUDE [sample-powershell-install](../../includes/sample-powershell-install.md)]

<a id="deploy-local-template" />

## <a name="deploy-a-template-from-your-local-machine"></a><span data-ttu-id="88940-109">Развертывание шаблона с локального компьютера</span><span class="sxs-lookup"><span data-stu-id="88940-109">Deploy a template from your local machine</span></span>

<span data-ttu-id="88940-110">При развертывании tooAzure ресурсы можно:</span><span class="sxs-lookup"><span data-stu-id="88940-110">When deploying resources tooAzure, you:</span></span>

1. <span data-ttu-id="88940-111">Войдите в tooyour учетная запись Azure</span><span class="sxs-lookup"><span data-stu-id="88940-111">Log in tooyour Azure account</span></span>
2. <span data-ttu-id="88940-112">Создание группы ресурсов, выступающее в роли контейнера hello hello развертывания ресурсов.</span><span class="sxs-lookup"><span data-stu-id="88940-112">Create a resource group that serves as hello container for hello deployed resources.</span></span> <span data-ttu-id="88940-113">Имя группы ресурсов hello Hello может содержать только буквенно-цифровые символы, точки, символы подчеркивания, дефисы и скобки.</span><span class="sxs-lookup"><span data-stu-id="88940-113">hello name of hello resource group can only include alphanumeric characters, periods, underscores, hyphens, and parenthesis.</span></span> <span data-ttu-id="88940-114">Возможность ее too90 символов.</span><span class="sxs-lookup"><span data-stu-id="88940-114">It can be up too90 characters.</span></span> <span data-ttu-id="88940-115">не может заканчиваться точкой.</span><span class="sxs-lookup"><span data-stu-id="88940-115">It cannot end in a period.</span></span>
3. <span data-ttu-id="88940-116">Развертывание toohello группы ресурсов hello шаблона, определяющий ресурсы toocreate hello</span><span class="sxs-lookup"><span data-stu-id="88940-116">Deploy toohello resource group hello template that defines hello resources toocreate</span></span>

<span data-ttu-id="88940-117">Шаблон может включать параметры, позволяющие toocustomize hello развертывания.</span><span class="sxs-lookup"><span data-stu-id="88940-117">A template can include parameters that enable you toocustomize hello deployment.</span></span> <span data-ttu-id="88940-118">Например, вы можете предоставить значения, предназначенные для конкретной среды (такой как среда разработки, тестирования и рабочая среда).</span><span class="sxs-lookup"><span data-stu-id="88940-118">For example, you can provide values that are tailored for a particular environment (such as dev, test, and production).</span></span> <span data-ttu-id="88940-119">Образец Hello шаблона определяет параметр для учетной записи хранения hello SKU.</span><span class="sxs-lookup"><span data-stu-id="88940-119">hello sample template defines a parameter for hello storage account SKU.</span></span>

<span data-ttu-id="88940-120">Следующий пример Hello создает группу ресурсов и развертывает шаблона с локального компьютера:</span><span class="sxs-lookup"><span data-stu-id="88940-120">hello following example creates a resource group, and deploys a template from your local machine:</span></span>

```powershell
Login-AzureRmAccount
 
New-AzureRmResourceGroup -Name ExampleResourceGroup -Location "South Central US"
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateFile c:\MyTemplates\storage.json -storageAccountType Standard_GRS
```

<span data-ttu-id="88940-121">Hello развертывания может занять несколько минут toocomplete.</span><span class="sxs-lookup"><span data-stu-id="88940-121">hello deployment can take a few minutes toocomplete.</span></span> <span data-ttu-id="88940-122">По завершении появится сообщение, содержащее результат hello:</span><span class="sxs-lookup"><span data-stu-id="88940-122">When it finishes, you see a message that includes hello result:</span></span>

```powershell
ProvisioningState       : Succeeded
```

## <a name="deploy-a-template-from-an-external-source"></a><span data-ttu-id="88940-123">Развертывание шаблона из внешнего источника</span><span class="sxs-lookup"><span data-stu-id="88940-123">Deploy a template from an external source</span></span>

<span data-ttu-id="88940-124">Вместо сохранения шаблонов диспетчера ресурсов на локальном компьютере, то лучше toostore их во внешнем местоположении.</span><span class="sxs-lookup"><span data-stu-id="88940-124">Instead of storing Resource Manager templates on your local machine, you may prefer toostore them in an external location.</span></span> <span data-ttu-id="88940-125">Вы можете хранить шаблоны в репозитории системы управления версиями (например, GitHub).</span><span class="sxs-lookup"><span data-stu-id="88940-125">You can store templates in a source control repository (such as GitHub).</span></span> <span data-ttu-id="88940-126">А также их можно хранить в учетной записи хранения Azure для общего доступа в организации.</span><span class="sxs-lookup"><span data-stu-id="88940-126">Or, you can store them in an Azure storage account for shared access in your organization.</span></span>

<span data-ttu-id="88940-127">использовать toodeploy шаблоном внешних hello **TemplateUri** параметра.</span><span class="sxs-lookup"><span data-stu-id="88940-127">toodeploy an external template, use hello **TemplateUri** parameter.</span></span> <span data-ttu-id="88940-128">Используйте hello URI в шаблоне образец hello toodeploy пример hello из GitHub.</span><span class="sxs-lookup"><span data-stu-id="88940-128">Use hello URI in hello example toodeploy hello sample template from GitHub.</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json `
  -storageAccountType Standard_GRS
```

<span data-ttu-id="88940-129">Hello предыдущего примера требуется общедоступный код URI hello шаблона, который работает в большинстве случаев, поскольку шаблон не следует включать конфиденциальные данные.</span><span class="sxs-lookup"><span data-stu-id="88940-129">hello preceding example requires a publicly accessible URI for hello template, which works for most scenarios because your template should not include sensitive data.</span></span> <span data-ttu-id="88940-130">Если вам требуется toospecify конфиденциальные данные (например, пароль администратора), можно передайте в качестве безопасного параметра.</span><span class="sxs-lookup"><span data-stu-id="88940-130">If you need toospecify sensitive data (like an admin password), pass that value as a secure parameter.</span></span> <span data-ttu-id="88940-131">Тем не менее если не требуется toobe ваш шаблон доступен из Интернета, можно защитить его путем сохранения его в контейнер закрытого хранения.</span><span class="sxs-lookup"><span data-stu-id="88940-131">However, if you do not want your template toobe publicly accessible, you can protect it by storing it in a private storage container.</span></span> <span data-ttu-id="88940-132">Сведения о развертывании шаблона, требующего маркер подписанного URL-адреса (SAS), см. в статье [Развертывание частного шаблона Resource Manager с использованием токена SAS и Azure PowerShell](resource-manager-powershell-sas-token.md).</span><span class="sxs-lookup"><span data-stu-id="88940-132">For information about deploying a template that requires a shared access signature (SAS) token, see [Deploy private template with SAS token](resource-manager-powershell-sas-token.md).</span></span>

## <a name="parameter-files"></a><span data-ttu-id="88940-133">Файлы параметров</span><span class="sxs-lookup"><span data-stu-id="88940-133">Parameter files</span></span>

<span data-ttu-id="88940-134">Вместо передачи параметров в качестве встроенных значений в скрипте, может оказаться проще toouse JSON-файл, содержащий значения параметров hello.</span><span class="sxs-lookup"><span data-stu-id="88940-134">Rather than passing parameters as inline values in your script, you may find it easier toouse a JSON file that contains hello parameter values.</span></span> <span data-ttu-id="88940-135">файл параметров Hello должны быть hello следующий формат:</span><span class="sxs-lookup"><span data-stu-id="88940-135">hello parameter file must be in hello following format:</span></span>

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

<span data-ttu-id="88940-136">Обратите внимание, что раздел параметров hello содержит имя параметра, которое соответствует hello параметра, определенного в шаблоне (storageAccountType).</span><span class="sxs-lookup"><span data-stu-id="88940-136">Notice that hello parameters section includes a parameter name that matches hello parameter defined in your template (storageAccountType).</span></span> <span data-ttu-id="88940-137">файл параметров Hello содержит значение параметра hello.</span><span class="sxs-lookup"><span data-stu-id="88940-137">hello parameter file contains a value for hello parameter.</span></span> <span data-ttu-id="88940-138">Это значение автоматически передается toohello шаблона во время развертывания.</span><span class="sxs-lookup"><span data-stu-id="88940-138">This value is automatically passed toohello template during deployment.</span></span> <span data-ttu-id="88940-139">Можно создать несколько файлов параметров для различных сценариев развертывания и затем передайте файл hello соответствующий параметр.</span><span class="sxs-lookup"><span data-stu-id="88940-139">You can create multiple parameter files for different deployment scenarios, and then pass in hello appropriate parameter file.</span></span> 

<span data-ttu-id="88940-140">Скопируйте предшествующий пример hello и сохраните его как файл с именем `storage.parameters.json`.</span><span class="sxs-lookup"><span data-stu-id="88940-140">Copy hello preceding example and save it as a file named `storage.parameters.json`.</span></span>

<span data-ttu-id="88940-141">использовать файл локального параметра toopass hello **TemplateParameterFile** параметр:</span><span class="sxs-lookup"><span data-stu-id="88940-141">toopass a local parameter file, use hello **TemplateParameterFile** parameter:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateFile c:\MyTemplates\storage.json `
  -TemplateParameterFile c:\MyTemplates\storage.parameters.json
```

<span data-ttu-id="88940-142">toopass файл внешнего параметра использовать hello **TemplateParameterUri** параметр:</span><span class="sxs-lookup"><span data-stu-id="88940-142">toopass an external parameter file, use hello **TemplateParameterUri** parameter:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json `
  -TemplateParameterUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.parameters.json
```

<span data-ttu-id="88940-143">Можно использовать встроенные параметры и локального параметра файлов в hello же операции развертывания.</span><span class="sxs-lookup"><span data-stu-id="88940-143">You can use inline parameters and a local parameter file in hello same deployment operation.</span></span> <span data-ttu-id="88940-144">Например можно указать некоторые значения в файле локального параметра hello и добавить другие встроенные значения во время развертывания.</span><span class="sxs-lookup"><span data-stu-id="88940-144">For example, you can specify some values in hello local parameter file and add other values inline during deployment.</span></span> <span data-ttu-id="88940-145">При указании значения для параметра в файл локального параметра hello и встроенные hello встроенного значение имеет приоритет.</span><span class="sxs-lookup"><span data-stu-id="88940-145">If you provide values for a parameter in both hello local parameter file and inline, hello inline value takes precedence.</span></span>

<span data-ttu-id="88940-146">Тем не менее при использовании внешнего файла параметров нельзя передавать другие значения в командной строке или локальном файле.</span><span class="sxs-lookup"><span data-stu-id="88940-146">However, when you use an external parameter file, you cannot pass other values either inline or from a local file.</span></span> <span data-ttu-id="88940-147">При указании файла параметров в hello **TemplateParameterUri** параметр, все встроенные параметры игнорируются.</span><span class="sxs-lookup"><span data-stu-id="88940-147">When you specify a parameter file in hello **TemplateParameterUri** parameter, all inline parameters are ignored.</span></span> <span data-ttu-id="88940-148">Укажите все значения параметров в файле внешних hello.</span><span class="sxs-lookup"><span data-stu-id="88940-148">Provide all parameter values in hello external file.</span></span> <span data-ttu-id="88940-149">Если шаблон включает конфиденциальное значение, нельзя включать в файл параметров hello, добавьте хранилище ключей, значение tooa или динамически предоставляют встроенные значения параметра.</span><span class="sxs-lookup"><span data-stu-id="88940-149">If your template includes a sensitive value that you cannot include in hello parameter file, either add that value tooa key vault, or dynamically provide all parameter values inline.</span></span>

<span data-ttu-id="88940-150">Если шаблон включает параметр с hello точно такое же имя в качестве одного из параметров hello в hello команду PowerShell, PowerShell представляет параметр hello из шаблона с постфиксной hello **FromTemplate**.</span><span class="sxs-lookup"><span data-stu-id="88940-150">If your template includes a parameter with hello same name as one of hello parameters in hello PowerShell command, PowerShell presents hello parameter from your template with hello postfix **FromTemplate**.</span></span> <span data-ttu-id="88940-151">Например, параметр с именем **ResourceGroupName** на шаблон конфликтует с hello **ResourceGroupName** параметр в hello [New-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment)командлета.</span><span class="sxs-lookup"><span data-stu-id="88940-151">For example, a parameter named **ResourceGroupName** in your template conflicts with hello **ResourceGroupName** parameter in hello [New-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment) cmdlet.</span></span> <span data-ttu-id="88940-152">Запрос tooprovide являются значение для **ResourceGroupNameFromTemplate**.</span><span class="sxs-lookup"><span data-stu-id="88940-152">You are prompted tooprovide a value for **ResourceGroupNameFromTemplate**.</span></span> <span data-ttu-id="88940-153">В общем случае следует избегать этой путаницы, не присвоив имена параметров с hello точно такое же имя в качестве параметров, используемых для операций развертывания.</span><span class="sxs-lookup"><span data-stu-id="88940-153">In general, you should avoid this confusion by not naming parameters with hello same name as parameters used for deployment operations.</span></span>

## <a name="test-a-template-deployment"></a><span data-ttu-id="88940-154">Тестовое развертывание шаблона</span><span class="sxs-lookup"><span data-stu-id="88940-154">Test a template deployment</span></span>

<span data-ttu-id="88940-155">использовать ваш шаблон и значения параметров без фактического развертывания все ресурсы, tootest [AzureRmResourceGroupDeployment теста](/powershell/module/azurerm.resources/test-azurermresourcegroupdeployment).</span><span class="sxs-lookup"><span data-stu-id="88940-155">tootest your template and parameter values without actually deploying any resources, use [Test-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/test-azurermresourcegroupdeployment).</span></span> 

```powershell
Test-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateFile c:\MyTemplates\storage.json -storageAccountType Standard_GRS
```

<span data-ttu-id="88940-156">Если ошибки не обнаружены, завершения выполнения команды hello без ответа.</span><span class="sxs-lookup"><span data-stu-id="88940-156">If no errors are detected, hello command finishes without a response.</span></span> <span data-ttu-id="88940-157">Если обнаруживается ошибка, hello команда возвращает сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="88940-157">If an error is detected, hello command returns an error message.</span></span> <span data-ttu-id="88940-158">Например toopass неправильное значение для учетной записи хранения hello SKU, система выдаст hello следующая ошибка:</span><span class="sxs-lookup"><span data-stu-id="88940-158">For example, attempting toopass an incorrect value for hello storage account SKU, returns hello following error:</span></span>

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName testgroup `
  -TemplateFile c:\MyTemplates\storage.json -storageAccountType badSku

Code    : InvalidTemplate
Message : Deployment template validation failed: 'hello provided value 'badSku' for hello template parameter 'storageAccountType'
          at line '15' and column '24' is not valid. hello parameter value is not part of hello allowed value(s):
          'Standard_LRS,Standard_ZRS,Standard_GRS,Standard_RAGRS,Premium_LRS'.'.
Details :
```

<span data-ttu-id="88940-159">Если шаблон содержит синтаксическую ошибку, команда hello возвращает ошибку, указывающую, что не удалось проанализировать шаблон hello.</span><span class="sxs-lookup"><span data-stu-id="88940-159">If your template has a syntax error, hello command returns an error indicating it could not parse hello template.</span></span> <span data-ttu-id="88940-160">сообщение Hello указывает hello номер строки и положение hello Ошибка синтаксического анализа.</span><span class="sxs-lookup"><span data-stu-id="88940-160">hello message indicates hello line number and position of hello parsing error.</span></span>

```powershell
Test-AzureRmResourceGroupDeployment : After parsing a value an unexpected character was encountered: 
  ". Path 'variables', line 31, position 3.
```

[!INCLUDE [resource-manager-deployments](../../includes/resource-manager-deployments.md)]

<span data-ttu-id="88940-161">полный режим toouse, используйте hello `Mode` параметр:</span><span class="sxs-lookup"><span data-stu-id="88940-161">toouse complete mode, use hello `Mode` parameter:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Mode Complete -Name ExampleDeployment `
  -ResourceGroupName ExampleResourceGroup -TemplateFile c:\MyTemplates\storage.json 
```

## <a name="sample-template"></a><span data-ttu-id="88940-162">Пример шаблона</span><span class="sxs-lookup"><span data-stu-id="88940-162">Sample template</span></span>

<span data-ttu-id="88940-163">Hello следующий шаблон используется для hello примеры в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="88940-163">hello following template is used for hello examples in this topic.</span></span> <span data-ttu-id="88940-164">Скопируйте и сохраните его как файл с именем storage.json.</span><span class="sxs-lookup"><span data-stu-id="88940-164">Copy and save it as a file named storage.json.</span></span> <span data-ttu-id="88940-165">toounderstand как toocreate этого шаблона, в разделе [создать свой первый диспетчера ресурсов Azure](resource-manager-create-first-template.md).</span><span class="sxs-lookup"><span data-stu-id="88940-165">toounderstand how toocreate this template, see [Create your first Azure Resource Manager template](resource-manager-create-first-template.md).</span></span>  

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

## <a name="next-steps"></a><span data-ttu-id="88940-166">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="88940-166">Next steps</span></span>
* <span data-ttu-id="88940-167">Примеры Hello в этой статье развертывания группы ресурсов tooa ресурсы в подписке по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="88940-167">hello examples in this article deploy resources tooa resource group in your default subscription.</span></span> <span data-ttu-id="88940-168">toouse другую подписку, в разделе [управления несколькими подписками Azure](/powershell/azure/manage-subscriptions-azureps).</span><span class="sxs-lookup"><span data-stu-id="88940-168">toouse a different subscription, see [Manage multiple Azure subscriptions](/powershell/azure/manage-subscriptions-azureps).</span></span>
* <span data-ttu-id="88940-169">Полный пример сценария, развертывающего шаблон, см. в статье [Сценарий для развертывания шаблона Resource Manager](resource-manager-samples-powershell-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="88940-169">For a complete sample script that deploys a template, see [Resource Manager template deployment script](resource-manager-samples-powershell-deploy.md).</span></span>
* <span data-ttu-id="88940-170">toodefine параметры в шаблоне, в статье toounderstand [понять структуру hello и синтаксис шаблоны Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="88940-170">toounderstand how toodefine parameters in your template, see [Understand hello structure and syntax of Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="88940-171">Советы по устранению распространенных ошибок развертывания см. в разделе [Устранение распространенных ошибок развертывания в Azure с помощью Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="88940-171">For tips on resolving common deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="88940-172">Сведения о развертывании шаблона, которому нужен токен SAS, см. в статье [Развертывание частного шаблона с помощью маркера SAS](resource-manager-powershell-sas-token.md).</span><span class="sxs-lookup"><span data-stu-id="88940-172">For information about deploying a template that requires a SAS token, see [Deploy private template with SAS token](resource-manager-powershell-sas-token.md).</span></span>
* <span data-ttu-id="88940-173">Для получения рекомендаций по как предприятия могут использовать диспетчер ресурсов tooeffectively управление подписками см. в разделе [корпоративные функции формирования шаблонов - управление конкретные подписки](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="88940-173">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

