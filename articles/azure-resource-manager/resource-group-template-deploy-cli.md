---
title: "Развертывание ресурсов с помощью интерфейса командной строки Azure и шаблона | Документация Майкрософт"
description: "Узнайте, как использовать Azure Resource Manager и Azure CLI для развертывания ресурсов в Azure. Эти ресурсы определяются в шаблоне Resource Manager."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 493b7932-8d1e-4499-912c-26098282ec95
ms.service: azure-resource-manager
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/31/2017
ms.author: tomfitz
ms.openlocfilehash: 4f1d5f4cc48470f8906edb28628006dd1996bd3a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-azure-cli"></a><span data-ttu-id="36cf0-104">Развертывание ресурсов с использованием шаблонов Resource Manager и Azure CLI</span><span class="sxs-lookup"><span data-stu-id="36cf0-104">Deploy resources with Resource Manager templates and Azure CLI</span></span>

<span data-ttu-id="36cf0-105">В этой статье объясняется, как использовать Azure CLI 2.0 и шаблоны Resource Manager для развертывания ресурсов в Azure.</span><span class="sxs-lookup"><span data-stu-id="36cf0-105">This topic explains how to use Azure CLI 2.0 with Resource Manager templates to deploy your resources to Azure.</span></span> <span data-ttu-id="36cf0-106">Если вы не знакомы с основными понятиями, связанными с развертыванием решений Azure и управлением ими, то см. [обзор Azure Resource Manager](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="36cf0-106">If you are not familiar with the concepts of deploying and managing your Azure solutions, see [Azure Resource Manager overview](resource-group-overview.md).</span></span>  

<span data-ttu-id="36cf0-107">Развертываемый шаблон Resource Manager может быть локальным файлом на вашем компьютере или внешним файлом, расположенным в репозитории, например в GitHub.</span><span class="sxs-lookup"><span data-stu-id="36cf0-107">The Resource Manager template you deploy can either be a local file on your machine, or an external file that is located in a repository like GitHub.</span></span> <span data-ttu-id="36cf0-108">Шаблон, развертываемый в этой статье, доступен в разделе [Пример шаблона](#sample-template) или как [шаблон учетной записи хранения в GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/101-storage-account-create/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="36cf0-108">The template you deploy in this article is available in the [Sample template](#sample-template) section, or as a [storage account template in GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/101-storage-account-create/azuredeploy.json).</span></span>

[!INCLUDE [sample-cli-install](../../includes/sample-cli-install.md)]

<span data-ttu-id="36cf0-109">Если у вас не установлен интерфейс командной строки Azure CLI, то можете использовать [Cloud Shell](#deploy-template-from-cloud-shell).</span><span class="sxs-lookup"><span data-stu-id="36cf0-109">If you do not have Azure CLI installed, you can use the [Cloud Shell](#deploy-template-from-cloud-shell).</span></span>

## <a name="deploy-local-template"></a><span data-ttu-id="36cf0-110">Развертывание локального шаблона</span><span class="sxs-lookup"><span data-stu-id="36cf0-110">Deploy local template</span></span>

<span data-ttu-id="36cf0-111">При развертывании ресурсов в Azure выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="36cf0-111">When deploying resources to Azure, you:</span></span>

1. <span data-ttu-id="36cf0-112">Вход в учетную запись Azure</span><span class="sxs-lookup"><span data-stu-id="36cf0-112">Log in to your Azure account</span></span>
2. <span data-ttu-id="36cf0-113">Создайте группу ресурсов, которая послужит в качестве контейнера для развертываемых ресурсов.</span><span class="sxs-lookup"><span data-stu-id="36cf0-113">Create a resource group that serves as the container for the deployed resources.</span></span> <span data-ttu-id="36cf0-114">Имя группы ресурсов может содержать только буквы, цифры, точки, знаки подчеркивания, дефисы и скобки.</span><span class="sxs-lookup"><span data-stu-id="36cf0-114">The name of the resource group can only include alphanumeric characters, periods, underscores, hyphens, and parenthesis.</span></span> <span data-ttu-id="36cf0-115">Оно может содержать до 90 знаков и</span><span class="sxs-lookup"><span data-stu-id="36cf0-115">It can be up to 90 characters.</span></span> <span data-ttu-id="36cf0-116">не может заканчиваться точкой.</span><span class="sxs-lookup"><span data-stu-id="36cf0-116">It cannot end in a period.</span></span>
3. <span data-ttu-id="36cf0-117">Разверните в группе ресурсов шаблон, определяющий ресурсы, которые необходимо создать.</span><span class="sxs-lookup"><span data-stu-id="36cf0-117">Deploy to the resource group the template that defines the resources to create</span></span>

<span data-ttu-id="36cf0-118">Шаблон может включать параметры, которые позволяют настроить развертывание.</span><span class="sxs-lookup"><span data-stu-id="36cf0-118">A template can include parameters that enable you to customize the deployment.</span></span> <span data-ttu-id="36cf0-119">Например, вы можете предоставить значения, предназначенные для конкретной среды (такой как среда разработки, тестирования и рабочая среда).</span><span class="sxs-lookup"><span data-stu-id="36cf0-119">For example, you can provide values that are tailored for a particular environment (such as dev, test, and production).</span></span> <span data-ttu-id="36cf0-120">Пример шаблона определяет параметр для номера SKU учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="36cf0-120">The sample template defines a parameter for the storage account SKU.</span></span> 

<span data-ttu-id="36cf0-121">В следующем примере создается группа ресурсов и развертывается шаблон с локального компьютера:</span><span class="sxs-lookup"><span data-stu-id="36cf0-121">The following example creates a resource group, and deploys a template from your local machine:</span></span>

```azurecli
az login

az group create --name ExampleGroup --location "Central US"
az group deployment create \
    --name ExampleDeployment \
    --resource-group ExampleGroup \
    --template-file storage.json \
    --parameters storageAccountType=Standard_GRS
```

<span data-ttu-id="36cf0-122">Развертывание может занять несколько минут.</span><span class="sxs-lookup"><span data-stu-id="36cf0-122">The deployment can take a few minutes to complete.</span></span> <span data-ttu-id="36cf0-123">По завершении появится сообщение, содержащее результат:</span><span class="sxs-lookup"><span data-stu-id="36cf0-123">When it finishes, you see a message that includes the result:</span></span>

```azurecli
"provisioningState": "Succeeded",
```

## <a name="deploy-external-template"></a><span data-ttu-id="36cf0-124">Развертывание внешнего шаблона</span><span class="sxs-lookup"><span data-stu-id="36cf0-124">Deploy external template</span></span>

<span data-ttu-id="36cf0-125">Шаблоны Resource Manager можно хранить не на локальном компьютере, а на внешнем источнике.</span><span class="sxs-lookup"><span data-stu-id="36cf0-125">Instead of storing Resource Manager templates on your local machine, you may prefer to store them in an external location.</span></span> <span data-ttu-id="36cf0-126">Вы можете хранить шаблоны в репозитории системы управления версиями (например, GitHub).</span><span class="sxs-lookup"><span data-stu-id="36cf0-126">You can store templates in a source control repository (such as GitHub).</span></span> <span data-ttu-id="36cf0-127">А также их можно хранить в учетной записи хранения Azure для общего доступа в организации.</span><span class="sxs-lookup"><span data-stu-id="36cf0-127">Or, you can store them in an Azure storage account for shared access in your organization.</span></span>

<span data-ttu-id="36cf0-128">Для развертывания внешнего шаблона используйте параметр **template-uri**.</span><span class="sxs-lookup"><span data-stu-id="36cf0-128">To deploy an external template, use the **template-uri** parameter.</span></span> <span data-ttu-id="36cf0-129">Используйте универсальный код ресурса (URI) в примере для развертывания примера шаблона из GitHub.</span><span class="sxs-lookup"><span data-stu-id="36cf0-129">Use the URI in the example to deploy the sample template from GitHub.</span></span>
   
```azurecli
az login

az group create --name ExampleGroup --location "Central US"
az group deployment create \
    --name ExampleDeployment \
    --resource-group ExampleGroup \
    --template-uri "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json" \
    --parameters storageAccountType=Standard_GRS
```

<span data-ttu-id="36cf0-130">В предыдущем примере для шаблона требуется общедоступный код URI, который подходит для большинства сценариев, так как шаблон не должен содержать конфиденциальные данные.</span><span class="sxs-lookup"><span data-stu-id="36cf0-130">The preceding example requires a publicly accessible URI for the template, which works for most scenarios because your template should not include sensitive data.</span></span> <span data-ttu-id="36cf0-131">Если необходимо указать конфиденциальные данные (например, пароль администратора), то передайте это значение с помощью безопасного параметра.</span><span class="sxs-lookup"><span data-stu-id="36cf0-131">If you need to specify sensitive data (like an admin password), pass that value as a secure parameter.</span></span> <span data-ttu-id="36cf0-132">Но если вы не хотите, чтобы шаблон был общедоступным, то можно защитить его, сохранив в закрытом контейнере хранилища.</span><span class="sxs-lookup"><span data-stu-id="36cf0-132">However, if you do not want your template to be publicly accessible, you can protect it by storing it in a private storage container.</span></span> <span data-ttu-id="36cf0-133">Сведения о развертывании шаблона, требующего маркер подписанного URL-адреса (SAS), см. в статье [Развертывание частного шаблона Resource Manager с использованием токена SAS и Azure PowerShell](resource-manager-cli-sas-token.md).</span><span class="sxs-lookup"><span data-stu-id="36cf0-133">For information about deploying a template that requires a shared access signature (SAS) token, see [Deploy private template with SAS token](resource-manager-cli-sas-token.md).</span></span>

## <a name="deploy-template-from-cloud-shell"></a><span data-ttu-id="36cf0-134">Развертывание шаблона из Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="36cf0-134">Deploy template from Cloud Shell</span></span>

<span data-ttu-id="36cf0-135">Вы можете использовать [Cloud Shell](../cloud-shell/overview.md) для выполнения команд Azure CLI для развертывания шаблона.</span><span class="sxs-lookup"><span data-stu-id="36cf0-135">You can use [Cloud Shell](../cloud-shell/overview.md) to run the Azure CLI commands for deploying your template.</span></span> <span data-ttu-id="36cf0-136">Однако сначала необходимо загрузить шаблон в общий файловый ресурс для Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="36cf0-136">However, you must first load your template into the file share for your Cloud Shell.</span></span> <span data-ttu-id="36cf0-137">Если вы еще не использовали Cloud Shell, ознакомьтесь со статьей [Обзор Azure Cloud Shell (предварительная версия)](../cloud-shell/overview.md), чтобы узнать о настройке службы.</span><span class="sxs-lookup"><span data-stu-id="36cf0-137">If you have not used Cloud Shell, see [Overview of Azure Cloud Shell](../cloud-shell/overview.md) for information about setting it up.</span></span>

1. <span data-ttu-id="36cf0-138">Войдите на [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="36cf0-138">Log in to the [Azure portal](https://portal.azure.com).</span></span>   

2. <span data-ttu-id="36cf0-139">Выберите свою группу ресурсов Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="36cf0-139">Select your Cloud Shell resource group.</span></span> <span data-ttu-id="36cf0-140">Шаблон имени — `cloud-shell-storage-<region>`.</span><span class="sxs-lookup"><span data-stu-id="36cf0-140">The name pattern is `cloud-shell-storage-<region>`.</span></span>

   ![Выбор группы ресурсов](./media/resource-group-template-deploy-cli/select-cs-resource-group.png)

3. <span data-ttu-id="36cf0-142">Выберите учетную запись хранения для Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="36cf0-142">Select the storage account for your Cloud Shell.</span></span>

   ![Выбор учетной записи хранения](./media/resource-group-template-deploy-cli/select-storage.png)

4. <span data-ttu-id="36cf0-144">Выберите **Файлы**.</span><span class="sxs-lookup"><span data-stu-id="36cf0-144">Select **Files**.</span></span>

   ![Выбор файлов](./media/resource-group-template-deploy-cli/select-files.png)

5. <span data-ttu-id="36cf0-146">Выберите общий файловый ресурс для Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="36cf0-146">Select the file share for Cloud Shell.</span></span> <span data-ttu-id="36cf0-147">Шаблон имени — `cs-<user>-<domain>-com-<uniqueGuid>`.</span><span class="sxs-lookup"><span data-stu-id="36cf0-147">The name pattern is `cs-<user>-<domain>-com-<uniqueGuid>`.</span></span>

   ![Выбор общего файлового ресурса](./media/resource-group-template-deploy-cli/select-file-share.png)

6. <span data-ttu-id="36cf0-149">Выберите **Добавить каталог**.</span><span class="sxs-lookup"><span data-stu-id="36cf0-149">Select **Add directory**.</span></span>

   ![Добавление каталога](./media/resource-group-template-deploy-cli/select-add-directory.png)

7. <span data-ttu-id="36cf0-151">Назовите его **templates** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="36cf0-151">Name it **templates**, and select **Okay**.</span></span>

   ![Присвоение имени каталогу](./media/resource-group-template-deploy-cli/name-templates.png)

8. <span data-ttu-id="36cf0-153">Выберите новый каталог.</span><span class="sxs-lookup"><span data-stu-id="36cf0-153">Select your new directory.</span></span>

   ![Выбор каталога](./media/resource-group-template-deploy-cli/select-templates.png)

9. <span data-ttu-id="36cf0-155">Щелкните **Отправить**.</span><span class="sxs-lookup"><span data-stu-id="36cf0-155">Select **Upload**.</span></span>

   ![Кнопка "Отправить"](./media/resource-group-template-deploy-cli/select-upload.png)

10. <span data-ttu-id="36cf0-157">Найдите и отправьте свой шаблон.</span><span class="sxs-lookup"><span data-stu-id="36cf0-157">Find and upload your template.</span></span>

   ![Отправка файла](./media/resource-group-template-deploy-cli/upload-files.png)

11. <span data-ttu-id="36cf0-159">Откройте командную строку.</span><span class="sxs-lookup"><span data-stu-id="36cf0-159">Open the prompt.</span></span>

   ![Открытие Cloud Shell](./media/resource-group-template-deploy-cli/start-cloud-shell.png)

12. <span data-ttu-id="36cf0-161">В Cloud Shell введите следующие команды:</span><span class="sxs-lookup"><span data-stu-id="36cf0-161">Enter the following commands in the Cloud Shell:</span></span>

   ```azurecli
   az group create --name examplegroup --location "South Central US"
   az group deployment create --resource-group examplegroup --template-file clouddrive/templates/azuredeploy.json --parameters storageAccountType=Standard_GRS
   ```

## <a name="parameter-files"></a><span data-ttu-id="36cf0-162">Файлы параметров</span><span class="sxs-lookup"><span data-stu-id="36cf0-162">Parameter files</span></span>

<span data-ttu-id="36cf0-163">Вместо передачи параметров в виде встроенных значений в сценарии вам может быть проще использовать JSON-файл, содержащий значения параметров.</span><span class="sxs-lookup"><span data-stu-id="36cf0-163">Rather than passing parameters as inline values in your script, you may find it easier to use a JSON file that contains the parameter values.</span></span> <span data-ttu-id="36cf0-164">Файл параметров должен быть в указанном ниже формате.</span><span class="sxs-lookup"><span data-stu-id="36cf0-164">The parameter file must be in the following format:</span></span>

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

<span data-ttu-id="36cf0-165">Обратите внимание, что раздел parameters содержит имя параметра, которое совпадает с параметром, определенным в шаблоне (storageAccountType).</span><span class="sxs-lookup"><span data-stu-id="36cf0-165">Notice that the parameters section includes a parameter name that matches the parameter defined in your template (storageAccountType).</span></span> <span data-ttu-id="36cf0-166">Файл параметров содержит значение для параметра.</span><span class="sxs-lookup"><span data-stu-id="36cf0-166">The parameter file contains a value for the parameter.</span></span> <span data-ttu-id="36cf0-167">Во время развертывания это значение автоматически передается в шаблон.</span><span class="sxs-lookup"><span data-stu-id="36cf0-167">This value is automatically passed to the template during deployment.</span></span> <span data-ttu-id="36cf0-168">Можно создать несколько файлов параметров для различных сценариев развертывания, а затем передать соответствующий файл параметров.</span><span class="sxs-lookup"><span data-stu-id="36cf0-168">You can create multiple parameter files for different deployment scenarios, and then pass in the appropriate parameter file.</span></span> 

<span data-ttu-id="36cf0-169">Скопируйте предыдущий пример и сохраните его как файл с именем `storage.parameters.json`.</span><span class="sxs-lookup"><span data-stu-id="36cf0-169">Copy the preceding example and save it as a file named `storage.parameters.json`.</span></span>

<span data-ttu-id="36cf0-170">Для передачи локального файла параметров используйте `@`, чтобы указать локальный файл с именем storage.parameters.json.</span><span class="sxs-lookup"><span data-stu-id="36cf0-170">To pass a local parameter file, use `@` to specify a local file named storage.parameters.json.</span></span>

```azurecli
az group deployment create \
    --name ExampleDeployment \
    --resource-group ExampleGroup \
    --template-file storage.json \
    --parameters @storage.parameters.json
```

## <a name="test-a-template-deployment"></a><span data-ttu-id="36cf0-171">Тестовое развертывание шаблона</span><span class="sxs-lookup"><span data-stu-id="36cf0-171">Test a template deployment</span></span>

<span data-ttu-id="36cf0-172">Чтобы проверить шаблон и значения параметров без фактического развертывания ресурсов, используйте [az group deployment validate](/cli/azure/group/deployment#validate).</span><span class="sxs-lookup"><span data-stu-id="36cf0-172">To test your template and parameter values without actually deploying any resources, use [az group deployment validate](/cli/azure/group/deployment#validate).</span></span> 

```azurecli
az group deployment validate \
    --resource-group ExampleGroup \
    --template-file storage.json \
    --parameters @storage.parameters.json
```

<span data-ttu-id="36cf0-173">Если ошибок не обнаружено, то команда возвращает сведения о тестовом развертывании.</span><span class="sxs-lookup"><span data-stu-id="36cf0-173">If no errors are detected, the command returns information about the test deployment.</span></span> <span data-ttu-id="36cf0-174">В частности, обратите внимание, что **error** имеет значение null.</span><span class="sxs-lookup"><span data-stu-id="36cf0-174">In particular, notice that the **error** value is null.</span></span>

```azurecli
{
  "error": null,
  "properties": {
      ...
```

<span data-ttu-id="36cf0-175">Если обнаруживается ошибка, то команда возвращает сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="36cf0-175">If an error is detected, the command returns an error message.</span></span> <span data-ttu-id="36cf0-176">Например, при попытке передать недопустимое значение для номера SKU учетной записи хранения возвращается следующая ошибка:</span><span class="sxs-lookup"><span data-stu-id="36cf0-176">For example, attempting to pass an incorrect value for the storage account SKU, returns the following error:</span></span>

```azurecli
{
  "error": {
    "code": "InvalidTemplate",
    "details": null,
    "message": "Deployment template validation failed: 'The provided value 'badSKU' for the template parameter 
      'storageAccountType' at line '13' and column '20' is not valid. The parameter value is not part of the allowed 
      value(s): 'Standard_LRS,Standard_ZRS,Standard_GRS,Standard_RAGRS,Premium_LRS'.'.",
    "target": null
  },
  "properties": null
}
```

<span data-ttu-id="36cf0-177">Если шаблон содержит синтаксическую ошибку, то команда возвращает сообщение об ошибке, указывающее, что ей не удалось проанализировать шаблон.</span><span class="sxs-lookup"><span data-stu-id="36cf0-177">If your template has a syntax error, the command returns an error indicating it could not parse the template.</span></span> <span data-ttu-id="36cf0-178">В сообщении указывается номер строки и позиция ошибки синтаксического анализа.</span><span class="sxs-lookup"><span data-stu-id="36cf0-178">The message indicates the line number and position of the parsing error.</span></span>

```azurecli
{
  "error": {
    "code": "InvalidTemplate",
    "details": null,
    "message": "Deployment template parse failed: 'After parsing a value an unexpected character was encountered:
      \". Path 'variables', line 31, position 3.'.",
    "target": null
  },
  "properties": null
}
```

[!INCLUDE [resource-manager-deployments](../../includes/resource-manager-deployments.md)]

<span data-ttu-id="36cf0-179">Чтобы использовать полный режим, используйте параметр `mode`.</span><span class="sxs-lookup"><span data-stu-id="36cf0-179">To use complete mode, use the `mode` parameter:</span></span>

```azurecli
az group deployment create \
    --name ExampleDeployment \
    --mode Complete \
    --resource-group ExampleGroup \
    --template-file storage.json \
    --parameters storageAccountType=Standard_GRS
```

## <a name="sample-template"></a><span data-ttu-id="36cf0-180">Пример шаблона</span><span class="sxs-lookup"><span data-stu-id="36cf0-180">Sample template</span></span>

<span data-ttu-id="36cf0-181">Для примеров в этой статье используется следующий шаблон.</span><span class="sxs-lookup"><span data-stu-id="36cf0-181">The following template is used for the examples in this topic.</span></span> <span data-ttu-id="36cf0-182">Скопируйте и сохраните его как файл с именем storage.json.</span><span class="sxs-lookup"><span data-stu-id="36cf0-182">Copy and save it as a file named storage.json.</span></span> <span data-ttu-id="36cf0-183">Сведения о создании этого шаблона см. в статье [Создание первого шаблона Azure Resource Manager](resource-manager-create-first-template.md).</span><span class="sxs-lookup"><span data-stu-id="36cf0-183">To understand how to create this template, see [Create your first Azure Resource Manager template](resource-manager-create-first-template.md).</span></span>  

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

## <a name="next-steps"></a><span data-ttu-id="36cf0-184">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="36cf0-184">Next steps</span></span>
* <span data-ttu-id="36cf0-185">В примерах этой статьи ресурсы развертываются в группу ресурсов в подписке по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="36cf0-185">The examples in this article deploy resources to a resource group in your default subscription.</span></span> <span data-ttu-id="36cf0-186">Чтобы использовать другую подписку, см. статью [Управление несколькими подписками Azure](/cli/azure/manage-azure-subscriptions-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="36cf0-186">To use a different subscription, see [Manage multiple Azure subscriptions](/cli/azure/manage-azure-subscriptions-azure-cli).</span></span>
* <span data-ttu-id="36cf0-187">Полный пример сценария, развертывающего шаблон, см. в статье [Сценарий для развертывания шаблона Resource Manager](resource-manager-samples-cli-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="36cf0-187">For a complete sample script that deploys a template, see [Resource Manager template deployment script](resource-manager-samples-cli-deploy.md).</span></span>
* <span data-ttu-id="36cf0-188">Сведения об определении параметров в шаблоне см. в статье [Описание структуры и синтаксиса шаблонов Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="36cf0-188">To understand how to define parameters in your template, see [Understand the structure and syntax of Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="36cf0-189">Советы по устранению распространенных ошибок развертывания см. в разделе [Устранение распространенных ошибок развертывания в Azure с помощью Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="36cf0-189">For tips on resolving common deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="36cf0-190">Сведения о развертывании шаблона, которому нужен токен SAS, см. в статье [Развертывание частного шаблона с помощью маркера SAS](resource-manager-cli-sas-token.md).</span><span class="sxs-lookup"><span data-stu-id="36cf0-190">For information about deploying a template that requires a SAS token, see [Deploy private template with SAS token](resource-manager-cli-sas-token.md).</span></span>
* <span data-ttu-id="36cf0-191">Руководство по использованию Resource Manager для эффективного управления подписками в организациях см [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md) (Шаблон Azure для организаций. Рекомендуемая система управления подпиской).</span><span class="sxs-lookup"><span data-stu-id="36cf0-191">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>
