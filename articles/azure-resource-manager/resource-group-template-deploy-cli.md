---
title: "aaaDeploy ресурсами с помощью Azure CLI и шаблона | Документы Microsoft"
description: "С помощью диспетчера ресурсов Azure и Azure CLI toodeploy tooAzure ресурсов. Hello ресурсы определяются в шаблоне диспетчера ресурсов."
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
ms.openlocfilehash: 9f8bb9a8720399390a407030d2d32bcd97d32f13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-azure-cli"></a><span data-ttu-id="aee2d-104">Развертывание ресурсов с использованием шаблонов Resource Manager и Azure CLI</span><span class="sxs-lookup"><span data-stu-id="aee2d-104">Deploy resources with Resource Manager templates and Azure CLI</span></span>

<span data-ttu-id="aee2d-105">В этом разделе объясняется, как toouse Azure CLI 2.0 с toodeploy шаблонов диспетчера ресурсов вашей tooAzure ресурсов.</span><span class="sxs-lookup"><span data-stu-id="aee2d-105">This topic explains how toouse Azure CLI 2.0 with Resource Manager templates toodeploy your resources tooAzure.</span></span> <span data-ttu-id="aee2d-106">Если вы не знакомы с основными понятиями hello развертывания и управлению решения Azure см [Обзор диспетчера ресурсов Azure](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="aee2d-106">If you are not familiar with hello concepts of deploying and managing your Azure solutions, see [Azure Resource Manager overview](resource-group-overview.md).</span></span>  

<span data-ttu-id="aee2d-107">шаблон диспетчера ресурсов Hello развертывание может быть локальный файл на компьютере или внешнем файле, расположенном в репозитория GitHub.</span><span class="sxs-lookup"><span data-stu-id="aee2d-107">hello Resource Manager template you deploy can either be a local file on your machine, or an external file that is located in a repository like GitHub.</span></span> <span data-ttu-id="aee2d-108">шаблон Hello развертывания в этой статье доступен в hello [образец шаблона](#sample-template) раздел, или как [шаблона учетной записи хранилища в GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/101-storage-account-create/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="aee2d-108">hello template you deploy in this article is available in hello [Sample template](#sample-template) section, or as a [storage account template in GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/101-storage-account-create/azuredeploy.json).</span></span>

[!INCLUDE [sample-cli-install](../../includes/sample-cli-install.md)]

<span data-ttu-id="aee2d-109">Если у вас установлен Azure CLI, можно использовать hello [оболочки облака](#deploy-template-from-cloud-shell).</span><span class="sxs-lookup"><span data-stu-id="aee2d-109">If you do not have Azure CLI installed, you can use hello [Cloud Shell](#deploy-template-from-cloud-shell).</span></span>

## <a name="deploy-local-template"></a><span data-ttu-id="aee2d-110">Развертывание локального шаблона</span><span class="sxs-lookup"><span data-stu-id="aee2d-110">Deploy local template</span></span>

<span data-ttu-id="aee2d-111">При развертывании tooAzure ресурсы можно:</span><span class="sxs-lookup"><span data-stu-id="aee2d-111">When deploying resources tooAzure, you:</span></span>

1. <span data-ttu-id="aee2d-112">Войдите в tooyour учетная запись Azure</span><span class="sxs-lookup"><span data-stu-id="aee2d-112">Log in tooyour Azure account</span></span>
2. <span data-ttu-id="aee2d-113">Создание группы ресурсов, выступающее в роли контейнера hello hello развертывания ресурсов.</span><span class="sxs-lookup"><span data-stu-id="aee2d-113">Create a resource group that serves as hello container for hello deployed resources.</span></span> <span data-ttu-id="aee2d-114">Имя группы ресурсов hello Hello может содержать только буквенно-цифровые символы, точки, символы подчеркивания, дефисы и скобки.</span><span class="sxs-lookup"><span data-stu-id="aee2d-114">hello name of hello resource group can only include alphanumeric characters, periods, underscores, hyphens, and parenthesis.</span></span> <span data-ttu-id="aee2d-115">Возможность ее too90 символов.</span><span class="sxs-lookup"><span data-stu-id="aee2d-115">It can be up too90 characters.</span></span> <span data-ttu-id="aee2d-116">не может заканчиваться точкой.</span><span class="sxs-lookup"><span data-stu-id="aee2d-116">It cannot end in a period.</span></span>
3. <span data-ttu-id="aee2d-117">Развертывание toohello группы ресурсов hello шаблона, определяющий ресурсы toocreate hello</span><span class="sxs-lookup"><span data-stu-id="aee2d-117">Deploy toohello resource group hello template that defines hello resources toocreate</span></span>

<span data-ttu-id="aee2d-118">Шаблон может включать параметры, позволяющие toocustomize hello развертывания.</span><span class="sxs-lookup"><span data-stu-id="aee2d-118">A template can include parameters that enable you toocustomize hello deployment.</span></span> <span data-ttu-id="aee2d-119">Например, вы можете предоставить значения, предназначенные для конкретной среды (такой как среда разработки, тестирования и рабочая среда).</span><span class="sxs-lookup"><span data-stu-id="aee2d-119">For example, you can provide values that are tailored for a particular environment (such as dev, test, and production).</span></span> <span data-ttu-id="aee2d-120">Образец Hello шаблона определяет параметр для учетной записи хранения hello SKU.</span><span class="sxs-lookup"><span data-stu-id="aee2d-120">hello sample template defines a parameter for hello storage account SKU.</span></span> 

<span data-ttu-id="aee2d-121">Следующий пример Hello создает группу ресурсов и развертывает шаблона с локального компьютера:</span><span class="sxs-lookup"><span data-stu-id="aee2d-121">hello following example creates a resource group, and deploys a template from your local machine:</span></span>

```azurecli
az login

az group create --name ExampleGroup --location "Central US"
az group deployment create \
    --name ExampleDeployment \
    --resource-group ExampleGroup \
    --template-file storage.json \
    --parameters storageAccountType=Standard_GRS
```

<span data-ttu-id="aee2d-122">Hello развертывания может занять несколько минут toocomplete.</span><span class="sxs-lookup"><span data-stu-id="aee2d-122">hello deployment can take a few minutes toocomplete.</span></span> <span data-ttu-id="aee2d-123">По завершении появится сообщение, содержащее результат hello:</span><span class="sxs-lookup"><span data-stu-id="aee2d-123">When it finishes, you see a message that includes hello result:</span></span>

```azurecli
"provisioningState": "Succeeded",
```

## <a name="deploy-external-template"></a><span data-ttu-id="aee2d-124">Развертывание внешнего шаблона</span><span class="sxs-lookup"><span data-stu-id="aee2d-124">Deploy external template</span></span>

<span data-ttu-id="aee2d-125">Вместо сохранения шаблонов диспетчера ресурсов на локальном компьютере, то лучше toostore их во внешнем местоположении.</span><span class="sxs-lookup"><span data-stu-id="aee2d-125">Instead of storing Resource Manager templates on your local machine, you may prefer toostore them in an external location.</span></span> <span data-ttu-id="aee2d-126">Вы можете хранить шаблоны в репозитории системы управления версиями (например, GitHub).</span><span class="sxs-lookup"><span data-stu-id="aee2d-126">You can store templates in a source control repository (such as GitHub).</span></span> <span data-ttu-id="aee2d-127">А также их можно хранить в учетной записи хранения Azure для общего доступа в организации.</span><span class="sxs-lookup"><span data-stu-id="aee2d-127">Or, you can store them in an Azure storage account for shared access in your organization.</span></span>

<span data-ttu-id="aee2d-128">использовать toodeploy шаблоном внешних hello **шаблон uri** параметра.</span><span class="sxs-lookup"><span data-stu-id="aee2d-128">toodeploy an external template, use hello **template-uri** parameter.</span></span> <span data-ttu-id="aee2d-129">Используйте hello URI в шаблоне образец hello toodeploy пример hello из GitHub.</span><span class="sxs-lookup"><span data-stu-id="aee2d-129">Use hello URI in hello example toodeploy hello sample template from GitHub.</span></span>
   
```azurecli
az login

az group create --name ExampleGroup --location "Central US"
az group deployment create \
    --name ExampleDeployment \
    --resource-group ExampleGroup \
    --template-uri "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json" \
    --parameters storageAccountType=Standard_GRS
```

<span data-ttu-id="aee2d-130">Hello предыдущего примера требуется общедоступный код URI hello шаблона, который работает в большинстве случаев, поскольку шаблон не следует включать конфиденциальные данные.</span><span class="sxs-lookup"><span data-stu-id="aee2d-130">hello preceding example requires a publicly accessible URI for hello template, which works for most scenarios because your template should not include sensitive data.</span></span> <span data-ttu-id="aee2d-131">Если вам требуется toospecify конфиденциальные данные (например, пароль администратора), можно передайте в качестве безопасного параметра.</span><span class="sxs-lookup"><span data-stu-id="aee2d-131">If you need toospecify sensitive data (like an admin password), pass that value as a secure parameter.</span></span> <span data-ttu-id="aee2d-132">Тем не менее если не требуется toobe ваш шаблон доступен из Интернета, можно защитить его путем сохранения его в контейнер закрытого хранения.</span><span class="sxs-lookup"><span data-stu-id="aee2d-132">However, if you do not want your template toobe publicly accessible, you can protect it by storing it in a private storage container.</span></span> <span data-ttu-id="aee2d-133">Сведения о развертывании шаблона, требующего маркер подписанного URL-адреса (SAS), см. в статье [Развертывание частного шаблона Resource Manager с использованием токена SAS и Azure PowerShell](resource-manager-cli-sas-token.md).</span><span class="sxs-lookup"><span data-stu-id="aee2d-133">For information about deploying a template that requires a shared access signature (SAS) token, see [Deploy private template with SAS token](resource-manager-cli-sas-token.md).</span></span>

## <a name="deploy-template-from-cloud-shell"></a><span data-ttu-id="aee2d-134">Развертывание шаблона из Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="aee2d-134">Deploy template from Cloud Shell</span></span>

<span data-ttu-id="aee2d-135">Можно использовать [оболочки облака](../cloud-shell/overview.md) toorun hello Azure CLI команды для развертывания шаблона.</span><span class="sxs-lookup"><span data-stu-id="aee2d-135">You can use [Cloud Shell](../cloud-shell/overview.md) toorun hello Azure CLI commands for deploying your template.</span></span> <span data-ttu-id="aee2d-136">Тем не менее необходимо сначала загрузить шаблон в общей папке hello для вашей облачной среды.</span><span class="sxs-lookup"><span data-stu-id="aee2d-136">However, you must first load your template into hello file share for your Cloud Shell.</span></span> <span data-ttu-id="aee2d-137">Если вы еще не использовали Cloud Shell, ознакомьтесь со статьей [Обзор Azure Cloud Shell (предварительная версия)](../cloud-shell/overview.md), чтобы узнать о настройке службы.</span><span class="sxs-lookup"><span data-stu-id="aee2d-137">If you have not used Cloud Shell, see [Overview of Azure Cloud Shell](../cloud-shell/overview.md) for information about setting it up.</span></span>

1. <span data-ttu-id="aee2d-138">Войдите в toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="aee2d-138">Log in toohello [Azure portal](https://portal.azure.com).</span></span>   

2. <span data-ttu-id="aee2d-139">Выберите свою группу ресурсов Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="aee2d-139">Select your Cloud Shell resource group.</span></span> <span data-ttu-id="aee2d-140">шаблон имени Hello `cloud-shell-storage-<region>`.</span><span class="sxs-lookup"><span data-stu-id="aee2d-140">hello name pattern is `cloud-shell-storage-<region>`.</span></span>

   ![Выбор группы ресурсов](./media/resource-group-template-deploy-cli/select-cs-resource-group.png)

3. <span data-ttu-id="aee2d-142">Выберите учетную запись хранения hello для вашей облачной среды.</span><span class="sxs-lookup"><span data-stu-id="aee2d-142">Select hello storage account for your Cloud Shell.</span></span>

   ![Выбор учетной записи хранения](./media/resource-group-template-deploy-cli/select-storage.png)

4. <span data-ttu-id="aee2d-144">Выберите **Файлы**.</span><span class="sxs-lookup"><span data-stu-id="aee2d-144">Select **Files**.</span></span>

   ![Выбор файлов](./media/resource-group-template-deploy-cli/select-files.png)

5. <span data-ttu-id="aee2d-146">Выберите общую папку hello для облака оболочки.</span><span class="sxs-lookup"><span data-stu-id="aee2d-146">Select hello file share for Cloud Shell.</span></span> <span data-ttu-id="aee2d-147">шаблон имени Hello `cs-<user>-<domain>-com-<uniqueGuid>`.</span><span class="sxs-lookup"><span data-stu-id="aee2d-147">hello name pattern is `cs-<user>-<domain>-com-<uniqueGuid>`.</span></span>

   ![Выбор общего файлового ресурса](./media/resource-group-template-deploy-cli/select-file-share.png)

6. <span data-ttu-id="aee2d-149">Выберите **Добавить каталог**.</span><span class="sxs-lookup"><span data-stu-id="aee2d-149">Select **Add directory**.</span></span>

   ![Добавление каталога](./media/resource-group-template-deploy-cli/select-add-directory.png)

7. <span data-ttu-id="aee2d-151">Назовите его **templates** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="aee2d-151">Name it **templates**, and select **Okay**.</span></span>

   ![Присвоение имени каталогу](./media/resource-group-template-deploy-cli/name-templates.png)

8. <span data-ttu-id="aee2d-153">Выберите новый каталог.</span><span class="sxs-lookup"><span data-stu-id="aee2d-153">Select your new directory.</span></span>

   ![Выбор каталога](./media/resource-group-template-deploy-cli/select-templates.png)

9. <span data-ttu-id="aee2d-155">Щелкните **Отправить**.</span><span class="sxs-lookup"><span data-stu-id="aee2d-155">Select **Upload**.</span></span>

   ![Кнопка "Отправить"](./media/resource-group-template-deploy-cli/select-upload.png)

10. <span data-ttu-id="aee2d-157">Найдите и отправьте свой шаблон.</span><span class="sxs-lookup"><span data-stu-id="aee2d-157">Find and upload your template.</span></span>

   ![Отправка файла](./media/resource-group-template-deploy-cli/upload-files.png)

11. <span data-ttu-id="aee2d-159">Откройте hello строки.</span><span class="sxs-lookup"><span data-stu-id="aee2d-159">Open hello prompt.</span></span>

   ![Открытие Cloud Shell](./media/resource-group-template-deploy-cli/start-cloud-shell.png)

12. <span data-ttu-id="aee2d-161">Введите следующие команды в hello оболочки облака hello:</span><span class="sxs-lookup"><span data-stu-id="aee2d-161">Enter hello following commands in hello Cloud Shell:</span></span>

   ```azurecli
   az group create --name examplegroup --location "South Central US"
   az group deployment create --resource-group examplegroup --template-file clouddrive/templates/azuredeploy.json --parameters storageAccountType=Standard_GRS
   ```

## <a name="parameter-files"></a><span data-ttu-id="aee2d-162">Файлы параметров</span><span class="sxs-lookup"><span data-stu-id="aee2d-162">Parameter files</span></span>

<span data-ttu-id="aee2d-163">Вместо передачи параметров в качестве встроенных значений в скрипте, может оказаться проще toouse JSON-файл, содержащий значения параметров hello.</span><span class="sxs-lookup"><span data-stu-id="aee2d-163">Rather than passing parameters as inline values in your script, you may find it easier toouse a JSON file that contains hello parameter values.</span></span> <span data-ttu-id="aee2d-164">файл параметров Hello должны быть hello следующий формат:</span><span class="sxs-lookup"><span data-stu-id="aee2d-164">hello parameter file must be in hello following format:</span></span>

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

<span data-ttu-id="aee2d-165">Обратите внимание, что раздел параметров hello содержит имя параметра, которое соответствует hello параметра, определенного в шаблоне (storageAccountType).</span><span class="sxs-lookup"><span data-stu-id="aee2d-165">Notice that hello parameters section includes a parameter name that matches hello parameter defined in your template (storageAccountType).</span></span> <span data-ttu-id="aee2d-166">файл параметров Hello содержит значение параметра hello.</span><span class="sxs-lookup"><span data-stu-id="aee2d-166">hello parameter file contains a value for hello parameter.</span></span> <span data-ttu-id="aee2d-167">Это значение автоматически передается toohello шаблона во время развертывания.</span><span class="sxs-lookup"><span data-stu-id="aee2d-167">This value is automatically passed toohello template during deployment.</span></span> <span data-ttu-id="aee2d-168">Можно создать несколько файлов параметров для различных сценариев развертывания и затем передайте файл hello соответствующий параметр.</span><span class="sxs-lookup"><span data-stu-id="aee2d-168">You can create multiple parameter files for different deployment scenarios, and then pass in hello appropriate parameter file.</span></span> 

<span data-ttu-id="aee2d-169">Скопируйте предшествующий пример hello и сохраните его как файл с именем `storage.parameters.json`.</span><span class="sxs-lookup"><span data-stu-id="aee2d-169">Copy hello preceding example and save it as a file named `storage.parameters.json`.</span></span>

<span data-ttu-id="aee2d-170">использовать файл локального параметра toopass `@` toospecify локальный файл с именем storage.parameters.json.</span><span class="sxs-lookup"><span data-stu-id="aee2d-170">toopass a local parameter file, use `@` toospecify a local file named storage.parameters.json.</span></span>

```azurecli
az group deployment create \
    --name ExampleDeployment \
    --resource-group ExampleGroup \
    --template-file storage.json \
    --parameters @storage.parameters.json
```

## <a name="test-a-template-deployment"></a><span data-ttu-id="aee2d-171">Тестовое развертывание шаблона</span><span class="sxs-lookup"><span data-stu-id="aee2d-171">Test a template deployment</span></span>

<span data-ttu-id="aee2d-172">использовать ваш шаблон и значения параметров без фактического развертывания все ресурсы, tootest [проверить развертывание группы az](/cli/azure/group/deployment#validate).</span><span class="sxs-lookup"><span data-stu-id="aee2d-172">tootest your template and parameter values without actually deploying any resources, use [az group deployment validate](/cli/azure/group/deployment#validate).</span></span> 

```azurecli
az group deployment validate \
    --resource-group ExampleGroup \
    --template-file storage.json \
    --parameters @storage.parameters.json
```

<span data-ttu-id="aee2d-173">Если ошибки не обнаружены, hello команда возвращает сведения о развертывании тестов hello.</span><span class="sxs-lookup"><span data-stu-id="aee2d-173">If no errors are detected, hello command returns information about hello test deployment.</span></span> <span data-ttu-id="aee2d-174">В частности, обратите внимание, что hello **ошибка** имеет значение null.</span><span class="sxs-lookup"><span data-stu-id="aee2d-174">In particular, notice that hello **error** value is null.</span></span>

```azurecli
{
  "error": null,
  "properties": {
      ...
```

<span data-ttu-id="aee2d-175">Если обнаруживается ошибка, hello команда возвращает сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="aee2d-175">If an error is detected, hello command returns an error message.</span></span> <span data-ttu-id="aee2d-176">Например toopass неправильное значение для учетной записи хранения hello SKU, система выдаст hello следующая ошибка:</span><span class="sxs-lookup"><span data-stu-id="aee2d-176">For example, attempting toopass an incorrect value for hello storage account SKU, returns hello following error:</span></span>

```azurecli
{
  "error": {
    "code": "InvalidTemplate",
    "details": null,
    "message": "Deployment template validation failed: 'hello provided value 'badSKU' for hello template parameter 
      'storageAccountType' at line '13' and column '20' is not valid. hello parameter value is not part of hello allowed 
      value(s): 'Standard_LRS,Standard_ZRS,Standard_GRS,Standard_RAGRS,Premium_LRS'.'.",
    "target": null
  },
  "properties": null
}
```

<span data-ttu-id="aee2d-177">Если шаблон содержит синтаксическую ошибку, команда hello возвращает ошибку, указывающую, что не удалось проанализировать шаблон hello.</span><span class="sxs-lookup"><span data-stu-id="aee2d-177">If your template has a syntax error, hello command returns an error indicating it could not parse hello template.</span></span> <span data-ttu-id="aee2d-178">сообщение Hello указывает hello номер строки и положение hello Ошибка синтаксического анализа.</span><span class="sxs-lookup"><span data-stu-id="aee2d-178">hello message indicates hello line number and position of hello parsing error.</span></span>

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

<span data-ttu-id="aee2d-179">полный режим toouse, используйте hello `mode` параметр:</span><span class="sxs-lookup"><span data-stu-id="aee2d-179">toouse complete mode, use hello `mode` parameter:</span></span>

```azurecli
az group deployment create \
    --name ExampleDeployment \
    --mode Complete \
    --resource-group ExampleGroup \
    --template-file storage.json \
    --parameters storageAccountType=Standard_GRS
```

## <a name="sample-template"></a><span data-ttu-id="aee2d-180">Пример шаблона</span><span class="sxs-lookup"><span data-stu-id="aee2d-180">Sample template</span></span>

<span data-ttu-id="aee2d-181">Hello следующий шаблон используется для hello примеры в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="aee2d-181">hello following template is used for hello examples in this topic.</span></span> <span data-ttu-id="aee2d-182">Скопируйте и сохраните его как файл с именем storage.json.</span><span class="sxs-lookup"><span data-stu-id="aee2d-182">Copy and save it as a file named storage.json.</span></span> <span data-ttu-id="aee2d-183">toounderstand как toocreate этого шаблона, в разделе [создать свой первый диспетчера ресурсов Azure](resource-manager-create-first-template.md).</span><span class="sxs-lookup"><span data-stu-id="aee2d-183">toounderstand how toocreate this template, see [Create your first Azure Resource Manager template](resource-manager-create-first-template.md).</span></span>  

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

## <a name="next-steps"></a><span data-ttu-id="aee2d-184">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="aee2d-184">Next steps</span></span>
* <span data-ttu-id="aee2d-185">Примеры Hello в этой статье развертывания группы ресурсов tooa ресурсы в подписке по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="aee2d-185">hello examples in this article deploy resources tooa resource group in your default subscription.</span></span> <span data-ttu-id="aee2d-186">toouse другую подписку, в разделе [управления несколькими подписками Azure](/cli/azure/manage-azure-subscriptions-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="aee2d-186">toouse a different subscription, see [Manage multiple Azure subscriptions](/cli/azure/manage-azure-subscriptions-azure-cli).</span></span>
* <span data-ttu-id="aee2d-187">Полный пример сценария, развертывающего шаблон, см. в статье [Сценарий для развертывания шаблона Resource Manager](resource-manager-samples-cli-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="aee2d-187">For a complete sample script that deploys a template, see [Resource Manager template deployment script](resource-manager-samples-cli-deploy.md).</span></span>
* <span data-ttu-id="aee2d-188">toodefine параметры в шаблоне, в статье toounderstand [понять структуру hello и синтаксис шаблоны Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="aee2d-188">toounderstand how toodefine parameters in your template, see [Understand hello structure and syntax of Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="aee2d-189">Советы по устранению распространенных ошибок развертывания см. в разделе [Устранение распространенных ошибок развертывания в Azure с помощью Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="aee2d-189">For tips on resolving common deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="aee2d-190">Сведения о развертывании шаблона, которому нужен токен SAS, см. в статье [Развертывание частного шаблона с помощью маркера SAS](resource-manager-cli-sas-token.md).</span><span class="sxs-lookup"><span data-stu-id="aee2d-190">For information about deploying a template that requires a SAS token, see [Deploy private template with SAS token](resource-manager-cli-sas-token.md).</span></span>
* <span data-ttu-id="aee2d-191">Для получения рекомендаций по как предприятия могут использовать диспетчер ресурсов tooeffectively управление подписками см. в разделе [корпоративные функции формирования шаблонов - управление конкретные подписки](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="aee2d-191">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>
