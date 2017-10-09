---
title: "Первый шаблон диспетчера ресурсов Azure aaaCreate | Документы Microsoft"
description: "Пошаговое руководство по toocreating первый шаблон диспетчера ресурсов Azure. Он показывает, как toouse hello ссылка на шаблон для шаблона hello toocreate учетной записи хранилища."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 07/27/2017
ms.topic: get-started-article
ms.author: tomfitz
ms.openlocfilehash: 92e6d6bb7094fe0e4537ee080704967862804bdb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-your-first-azure-resource-manager-template"></a><span data-ttu-id="8bed9-104">Создание и развертывание первого шаблона Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="8bed9-104">Create and deploy your first Azure Resource Manager template</span></span>
<span data-ttu-id="8bed9-105">Этот раздел поможет выполнить этапы создания вашего первого шаблона Azure Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="8bed9-105">This topic walks you through hello steps of creating your first Azure Resource Manager template.</span></span> <span data-ttu-id="8bed9-106">Шаблоны диспетчера ресурсов являются JSON-файлов, которые определяют ресурсы hello нужна toodeploy в решении.</span><span class="sxs-lookup"><span data-stu-id="8bed9-106">Resource Manager templates are JSON files that define hello resources you need toodeploy for your solution.</span></span> <span data-ttu-id="8bed9-107">hello toounderstand основные понятия, связанные с развертыванием и управлением решений Azure, в разделе [Обзор диспетчера ресурсов Azure](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8bed9-107">toounderstand hello concepts associated with deploying and managing your Azure solutions, see [Azure Resource Manager overview](resource-group-overview.md).</span></span> <span data-ttu-id="8bed9-108">Если вы используете существующие ресурсы и требуется tooget шаблона для этих ресурсов, см. раздел [Экспорт шаблона диспетчера ресурсов Azure с существующие ресурсы](resource-manager-export-template.md).</span><span class="sxs-lookup"><span data-stu-id="8bed9-108">If you have existing resources and want tooget a template for those resources, see [Export an Azure Resource Manager template from existing resources](resource-manager-export-template.md).</span></span>

<span data-ttu-id="8bed9-109">шаблоны toocreate и проверьте, требуется редактор JSON.</span><span class="sxs-lookup"><span data-stu-id="8bed9-109">toocreate and revise templates, you need a JSON editor.</span></span> <span data-ttu-id="8bed9-110">например [Visual Studio Code](https://code.visualstudio.com/). Это упрощенный кроссплатформенный редактор с открытым исходным кодом.</span><span class="sxs-lookup"><span data-stu-id="8bed9-110">[Visual Studio Code](https://code.visualstudio.com/) is a lightweight, open-source, cross-platform code editor.</span></span> <span data-ttu-id="8bed9-111">Для создания шаблонов Resource Manager мы настоятельно рекомендуем использовать Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="8bed9-111">We strongly recommend using Visual Studio Code for creating Resource Manager templates.</span></span> <span data-ttu-id="8bed9-112">В этой статье предполагается, что вы используете VS Code. Но вы можете использовать и другой редактор JSON (например, Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="8bed9-112">This topic assumes you are using VS Code; however, if you have another JSON editor (like Visual Studio), you can use that editor.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8bed9-113">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="8bed9-113">Prerequisites</span></span>

* <span data-ttu-id="8bed9-114">Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="8bed9-114">Visual Studio Code.</span></span> <span data-ttu-id="8bed9-115">При необходимости установите его со страницы [https://code.visualstudio.com/](https://code.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="8bed9-115">If needed, install it from [https://code.visualstudio.com/](https://code.visualstudio.com/).</span></span>
* <span data-ttu-id="8bed9-116">Подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="8bed9-116">An Azure subscription.</span></span> <span data-ttu-id="8bed9-117">Если у вас еще нет подписки Azure, [создайте бесплатную учетную запись Azure](https://azure.microsoft.com/free/?WT.mc_id=A261C142F), прежде чем начинать работу.</span><span class="sxs-lookup"><span data-stu-id="8bed9-117">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="create-template"></a><span data-ttu-id="8bed9-118">Создание шаблона</span><span class="sxs-lookup"><span data-stu-id="8bed9-118">Create template</span></span>

<span data-ttu-id="8bed9-119">Давайте начнем с простой шаблон, который развертывает подписки tooyour учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="8bed9-119">Let's start with a simple template that deploys a storage account tooyour subscription.</span></span>

1. <span data-ttu-id="8bed9-120">Выберите **Файл** > **Создать файл**.</span><span class="sxs-lookup"><span data-stu-id="8bed9-120">Select **File** > **New File**.</span></span> 

   ![Создание файла](./media/resource-manager-create-first-template/new-file.png)

2. <span data-ttu-id="8bed9-122">Скопируйте и вставьте следующий синтаксис JSON в свой файл hello:</span><span class="sxs-lookup"><span data-stu-id="8bed9-122">Copy and paste hello following JSON syntax into your file:</span></span>

   ```json
   {
     "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
     "contentVersion": "1.0.0.0",
     "parameters": {
     },
     "variables": {
     },
     "resources": [
       {
         "name": "[concat('storage', uniqueString(resourceGroup().id))]",
         "type": "Microsoft.Storage/storageAccounts",
         "apiVersion": "2016-01-01",
         "sku": {
           "name": "Standard_LRS"
         },
         "kind": "Storage",
         "location": "South Central US",
         "tags": {},
         "properties": {}
       }
     ],
     "outputs": {  }
   }
   ```

   <span data-ttu-id="8bed9-123">Имена учетной записи хранения имеет несколько ограничений, которые делают их трудно tooset.</span><span class="sxs-lookup"><span data-stu-id="8bed9-123">Storage account names have several restrictions that make them difficult tooset.</span></span> <span data-ttu-id="8bed9-124">Hello имя должно быть в диапазоне от 3 до 24 символов в длину, используйте только цифры и строчные буквы и быть уникальными.</span><span class="sxs-lookup"><span data-stu-id="8bed9-124">hello name must be between 3 and 24 characters in length, use only numbers and lower-case letters, and be unique.</span></span> <span data-ttu-id="8bed9-125">Hello предыдущий шаблон использует hello [uniqueString](resource-group-template-functions-string.md#uniquestring) функции toogenerate хэш-значения.</span><span class="sxs-lookup"><span data-stu-id="8bed9-125">hello preceding template uses hello [uniqueString](resource-group-template-functions-string.md#uniquestring) function toogenerate a hash value.</span></span> <span data-ttu-id="8bed9-126">toogive этот хэш-значения в нескольких то есть, он добавляет префикс hello *хранения*.</span><span class="sxs-lookup"><span data-stu-id="8bed9-126">toogive this hash value more meaning, it adds hello prefix *storage*.</span></span> 

3. <span data-ttu-id="8bed9-127">Сохраните этот файл как **azuredeploy.json** tooa локальную папку.</span><span class="sxs-lookup"><span data-stu-id="8bed9-127">Save this file as **azuredeploy.json** tooa local folder.</span></span>

   ![Сохранение шаблона](./media/resource-manager-create-first-template/save-template.png)

## <a name="deploy-template"></a><span data-ttu-id="8bed9-129">Развертывание шаблона</span><span class="sxs-lookup"><span data-stu-id="8bed9-129">Deploy template</span></span>

<span data-ttu-id="8bed9-130">Вам будут готовы toodeploy этот шаблон.</span><span class="sxs-lookup"><span data-stu-id="8bed9-130">You are ready toodeploy this template.</span></span> <span data-ttu-id="8bed9-131">Можно использовать PowerShell или Azure CLI toocreate группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="8bed9-131">You use either PowerShell or Azure CLI toocreate a resource group.</span></span> <span data-ttu-id="8bed9-132">Разверните группу ресурсов toothat учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="8bed9-132">Then, you deploy a storage account toothat resource group.</span></span>

* <span data-ttu-id="8bed9-133">Для PowerShell используйте следующие команды из hello папку, содержащую шаблон hello hello:</span><span class="sxs-lookup"><span data-stu-id="8bed9-133">For PowerShell, use hello following commands from hello folder containing hello template:</span></span>

   ```powershell
   Login-AzureRmAccount
   
   New-AzureRmResourceGroup -Name examplegroup -Location "South Central US"
   New-AzureRmResourceGroupDeployment -ResourceGroupName examplegroup -TemplateFile azuredeploy.json
   ```

* <span data-ttu-id="8bed9-134">Для локальной установки Azure CLI используйте следующие команды из hello папку, содержащую шаблон hello hello.</span><span class="sxs-lookup"><span data-stu-id="8bed9-134">For a local installation of Azure CLI, use hello following commands from hello folder containing hello template:</span></span>

   ```azurecli
   az login

   az group create --name examplegroup --location "South Central US"
   az group deployment create --resource-group examplegroup --template-file azuredeploy.json
   ```

<span data-ttu-id="8bed9-135">После завершения развертывания в группе ресурсов hello существует вашей учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="8bed9-135">When deployment finishes, your storage account exists in hello resource group.</span></span>

## <a name="deploy-template-from-cloud-shell"></a><span data-ttu-id="8bed9-136">Развертывание шаблона из Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="8bed9-136">Deploy template from Cloud Shell</span></span>

<span data-ttu-id="8bed9-137">Можно использовать [оболочки облака](../cloud-shell/overview.md) toorun hello Azure CLI команды для развертывания шаблона.</span><span class="sxs-lookup"><span data-stu-id="8bed9-137">You can use [Cloud Shell](../cloud-shell/overview.md) toorun hello Azure CLI commands for deploying your template.</span></span> <span data-ttu-id="8bed9-138">Тем не менее необходимо сначала загрузить шаблон в общей папке hello для вашей облачной среды.</span><span class="sxs-lookup"><span data-stu-id="8bed9-138">However, you must first load your template into hello file share for your Cloud Shell.</span></span> <span data-ttu-id="8bed9-139">Если вы еще не использовали Cloud Shell, ознакомьтесь со статьей [Обзор Azure Cloud Shell (предварительная версия)](../cloud-shell/overview.md), чтобы узнать о настройке службы.</span><span class="sxs-lookup"><span data-stu-id="8bed9-139">If you have not used Cloud Shell, see [Overview of Azure Cloud Shell](../cloud-shell/overview.md) for information about setting it up.</span></span>

1. <span data-ttu-id="8bed9-140">Войдите в toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8bed9-140">Log in toohello [Azure portal](https://portal.azure.com).</span></span>   

2. <span data-ttu-id="8bed9-141">Выберите свою группу ресурсов Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="8bed9-141">Select your Cloud Shell resource group.</span></span> <span data-ttu-id="8bed9-142">шаблон имени Hello `cloud-shell-storage-<region>`.</span><span class="sxs-lookup"><span data-stu-id="8bed9-142">hello name pattern is `cloud-shell-storage-<region>`.</span></span>

   ![Выбор группы ресурсов](./media/resource-manager-create-first-template/select-cs-resource-group.png)

3. <span data-ttu-id="8bed9-144">Выберите учетную запись хранения hello для вашей облачной среды.</span><span class="sxs-lookup"><span data-stu-id="8bed9-144">Select hello storage account for your Cloud Shell.</span></span>

   ![Выбор учетной записи хранения](./media/resource-manager-create-first-template/select-storage.png)

4. <span data-ttu-id="8bed9-146">Выберите **Файлы**.</span><span class="sxs-lookup"><span data-stu-id="8bed9-146">Select **Files**.</span></span>

   ![Выбор файлов](./media/resource-manager-create-first-template/select-files.png)

5. <span data-ttu-id="8bed9-148">Выберите общую папку hello для облака оболочки.</span><span class="sxs-lookup"><span data-stu-id="8bed9-148">Select hello file share for Cloud Shell.</span></span> <span data-ttu-id="8bed9-149">шаблон имени Hello `cs-<user>-<domain>-com-<uniqueGuid>`.</span><span class="sxs-lookup"><span data-stu-id="8bed9-149">hello name pattern is `cs-<user>-<domain>-com-<uniqueGuid>`.</span></span>

   ![Выбор общего файлового ресурса](./media/resource-manager-create-first-template/select-file-share.png)

6. <span data-ttu-id="8bed9-151">Выберите **Добавить каталог**.</span><span class="sxs-lookup"><span data-stu-id="8bed9-151">Select **Add directory**.</span></span>

   ![Добавление каталога](./media/resource-manager-create-first-template/select-add-directory.png)

7. <span data-ttu-id="8bed9-153">Назовите его **templates** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="8bed9-153">Name it **templates**, and select **Okay**.</span></span>

   ![Присвоение имени каталогу](./media/resource-manager-create-first-template/name-templates.png)

8. <span data-ttu-id="8bed9-155">Выберите новый каталог.</span><span class="sxs-lookup"><span data-stu-id="8bed9-155">Select your new directory.</span></span>

   ![Выбор каталога](./media/resource-manager-create-first-template/select-templates.png)

9. <span data-ttu-id="8bed9-157">Щелкните **Отправить**.</span><span class="sxs-lookup"><span data-stu-id="8bed9-157">Select **Upload**.</span></span>

   ![Кнопка "Отправить"](./media/resource-manager-create-first-template/select-upload.png)

10. <span data-ttu-id="8bed9-159">Найдите и отправьте свой шаблон.</span><span class="sxs-lookup"><span data-stu-id="8bed9-159">Find and upload your template.</span></span>

   ![Отправка файла](./media/resource-manager-create-first-template/upload-files.png)

11. <span data-ttu-id="8bed9-161">Откройте hello строки.</span><span class="sxs-lookup"><span data-stu-id="8bed9-161">Open hello prompt.</span></span>

   ![Открытие Cloud Shell](./media/resource-manager-create-first-template/start-cloud-shell.png)

12. <span data-ttu-id="8bed9-163">Введите следующие команды в hello оболочки облака hello:</span><span class="sxs-lookup"><span data-stu-id="8bed9-163">Enter hello following commands in hello Cloud Shell:</span></span>

   ```azurecli
   az group create --name examplegroup --location "South Central US"
   az group deployment create --resource-group examplegroup --template-file clouddrive/templates/azuredeploy.json
   ```

<span data-ttu-id="8bed9-164">После завершения развертывания в группе ресурсов hello существует вашей учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="8bed9-164">When deployment finishes, your storage account exists in hello resource group.</span></span>

## <a name="customize-hello-template"></a><span data-ttu-id="8bed9-165">Настройка шаблона hello</span><span class="sxs-lookup"><span data-stu-id="8bed9-165">Customize hello template</span></span>

<span data-ttu-id="8bed9-166">шаблон Hello работает отлично, но не обладает гибкостью.</span><span class="sxs-lookup"><span data-stu-id="8bed9-166">hello template works fine, but it is not flexible.</span></span> <span data-ttu-id="8bed9-167">Он всегда развертывает локально избыточное хранилище tooSouth центральной части США.</span><span class="sxs-lookup"><span data-stu-id="8bed9-167">It always deploys a locally redundant storage tooSouth Central US.</span></span> <span data-ttu-id="8bed9-168">Имя Hello всегда является *хранения* следуют хэш-значения.</span><span class="sxs-lookup"><span data-stu-id="8bed9-168">hello name is always *storage* followed by a hash value.</span></span> <span data-ttu-id="8bed9-169">с помощью шаблона hello для различных сценариев tooenable добавить шаблон toohello параметров.</span><span class="sxs-lookup"><span data-stu-id="8bed9-169">tooenable using hello template for different scenarios, add parameters toohello template.</span></span>

<span data-ttu-id="8bed9-170">Hello пример hello раздела параметров с двумя параметрами.</span><span class="sxs-lookup"><span data-stu-id="8bed9-170">hello following example shows hello parameters section with two parameters.</span></span> <span data-ttu-id="8bed9-171">Здравствуйте, первый параметр `storageSKU` позволяет типа hello toospecify избыточности.</span><span class="sxs-lookup"><span data-stu-id="8bed9-171">hello first parameter `storageSKU` enables you toospecify hello type of redundancy.</span></span> <span data-ttu-id="8bed9-172">Этот параметр ограничивает число hello значения, которые можно передать в toovalues, которые являются допустимыми для учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="8bed9-172">It limits hello values you can pass in toovalues that are valid for a storage account.</span></span> <span data-ttu-id="8bed9-173">Он также задает значение по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="8bed9-173">It also specifies a default value.</span></span> <span data-ttu-id="8bed9-174">Здравствуйте, второй параметр `storageNamePrefix` является набор tooallow до 11 символов.</span><span class="sxs-lookup"><span data-stu-id="8bed9-174">hello second parameter `storageNamePrefix` is set tooallow a maximum of 11 characters.</span></span> <span data-ttu-id="8bed9-175">Он задает значение по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="8bed9-175">It specifies a default value.</span></span>

```json
"parameters": {
  "storageSKU": {
    "type": "string",
    "allowedValues": [
      "Standard_LRS",
      "Standard_ZRS",
      "Standard_GRS",
      "Standard_RAGRS",
      "Premium_LRS"
    ],
    "defaultValue": "Standard_LRS",
    "metadata": {
      "description": "hello type of replication toouse for hello storage account."
    }
  },
  "storageNamePrefix": {
    "type": "string",
    "maxLength": 11,
    "defaultValue": "storage",
    "metadata": {
      "description": "hello value toouse for starting hello storage account name. Use only lowercase letters and numbers."
    }
  }
},
```

<span data-ttu-id="8bed9-176">В разделе "переменные" hello, добавьте переменную с именем `storageName`.</span><span class="sxs-lookup"><span data-stu-id="8bed9-176">In hello variables section, add a variable named `storageName`.</span></span> <span data-ttu-id="8bed9-177">Он объединяет значение префикса hello из параметров hello и хэш-код от hello [uniqueString](resource-group-template-functions-string.md#uniquestring) функции.</span><span class="sxs-lookup"><span data-stu-id="8bed9-177">It combines hello prefix value from hello parameters and a hash value from hello [uniqueString](resource-group-template-functions-string.md#uniquestring) function.</span></span> <span data-ttu-id="8bed9-178">Она использует hello [toLower](resource-group-template-functions-string.md#tolower) функции tooconvert toolowercase все символы.</span><span class="sxs-lookup"><span data-stu-id="8bed9-178">It uses hello [toLower](resource-group-template-functions-string.md#tolower) function tooconvert all characters toolowercase.</span></span>

```json
"variables": {
  "storageName": "[concat(toLower(parameters('storageNamePrefix')), uniqueString(resourceGroup().id))]"
},
```

<span data-ttu-id="8bed9-179">toouse эти новые значения для вашей учетной записи, измените определение ресурса hello:</span><span class="sxs-lookup"><span data-stu-id="8bed9-179">toouse these new values for your storage account, change hello resource definition:</span></span>

```json
"resources": [
  {
    "name": "[variables('storageName')]",
    "type": "Microsoft.Storage/storageAccounts",
    "apiVersion": "2016-01-01",
    "sku": {
      "name": "[parameters('storageSKU')]"
    },
    "kind": "Storage",
    "location": "[resourceGroup().location]",
    "tags": {},
    "properties": {}
  }
],
```

<span data-ttu-id="8bed9-180">Обратите внимание, что hello теперь задано имя учетной записи хранения hello toohello переменной, которая была добавлена.</span><span class="sxs-lookup"><span data-stu-id="8bed9-180">Notice that hello name of hello storage account is now set toohello variable that you added.</span></span> <span data-ttu-id="8bed9-181">Имя SKU Hello задано toohello значение параметра hello.</span><span class="sxs-lookup"><span data-stu-id="8bed9-181">hello SKU name is set toohello value of hello parameter.</span></span> <span data-ttu-id="8bed9-182">Задайте расположение Hello hello местоположения hello группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="8bed9-182">hello location is set hello same location as hello resource group.</span></span>

<span data-ttu-id="8bed9-183">Сохраните файл.</span><span class="sxs-lookup"><span data-stu-id="8bed9-183">Save your file.</span></span> 

<span data-ttu-id="8bed9-184">После завершения шагов hello в этой статье, ваш шаблон теперь выглядит следующим образом.</span><span class="sxs-lookup"><span data-stu-id="8bed9-184">After completing hello steps in this article, your template now looks like:</span></span>

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageSKU": {
      "type": "string",
      "allowedValues": [
        "Standard_LRS",
        "Standard_ZRS",
        "Standard_GRS",
        "Standard_RAGRS",
        "Premium_LRS"
      ],
      "defaultValue": "Standard_LRS",
      "metadata": {
        "description": "hello type of replication toouse for hello storage account."
      }
    },   
    "storageNamePrefix": {
      "type": "string",
      "maxLength": 11,
      "defaultValue": "storage",
      "metadata": {
        "description": "hello value toouse for starting hello storage account name. Use only lowercase letters and numbers."
      }
    }
  },
  "variables": {
    "storageName": "[concat(toLower(parameters('storageNamePrefix')), uniqueString(resourceGroup().id))]"
  },
  "resources": [
    {
      "name": "[variables('storageName')]",
      "type": "Microsoft.Storage/storageAccounts",
      "apiVersion": "2016-01-01",
      "sku": {
        "name": "[parameters('storageSKU')]"
      },
      "kind": "Storage",
      "location": "[resourceGroup().location]",
      "tags": {},
      "properties": {}
    }
  ],
  "outputs": {  }
}
```

## <a name="redeploy-template"></a><span data-ttu-id="8bed9-185">Повторное развертывание шаблона</span><span class="sxs-lookup"><span data-stu-id="8bed9-185">Redeploy template</span></span>

<span data-ttu-id="8bed9-186">Повторное развертывание шаблона hello с разными значениями.</span><span class="sxs-lookup"><span data-stu-id="8bed9-186">Redeploy hello template with different values.</span></span>

<span data-ttu-id="8bed9-187">Для PowerShell используйте команду:</span><span class="sxs-lookup"><span data-stu-id="8bed9-187">For PowerShell, use:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName examplegroup -TemplateFile azuredeploy.json -storageNamePrefix newstore -storageSKU Standard_RAGRS
```

<span data-ttu-id="8bed9-188">Для интерфейса командной строки Azure:</span><span class="sxs-lookup"><span data-stu-id="8bed9-188">For Azure CLI, use:</span></span>

```azurecli
az group deployment create --resource-group examplegroup --template-file azuredeploy.json --parameters storageSKU=Standard_RAGRS storageNamePrefix=newstore
```

<span data-ttu-id="8bed9-189">Для hello оболочки облака необходимо отправьте измененный шаблон toohello файлового ресурса.</span><span class="sxs-lookup"><span data-stu-id="8bed9-189">For hello Cloud Shell, upload your changed template toohello file share.</span></span> <span data-ttu-id="8bed9-190">Перезаписать существующий файл hello.</span><span class="sxs-lookup"><span data-stu-id="8bed9-190">Overwrite hello existing file.</span></span> <span data-ttu-id="8bed9-191">Затем с помощью hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="8bed9-191">Then, use hello following command:</span></span>

```azurecli
az group deployment create --resource-group examplegroup --template-file clouddrive/templates/azuredeploy.json --parameters storageSKU=Standard_RAGRS storageNamePrefix=newstore
```

## <a name="clean-up-resources"></a><span data-ttu-id="8bed9-192">Очистка ресурсов</span><span class="sxs-lookup"><span data-stu-id="8bed9-192">Clean up resources</span></span>

<span data-ttu-id="8bed9-193">Если больше не нужен, удалите ресурсы hello развернутые путем удаления группы ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="8bed9-193">When no longer needed, clean up hello resources you deployed by deleting hello resource group.</span></span>

<span data-ttu-id="8bed9-194">Для PowerShell используйте команду:</span><span class="sxs-lookup"><span data-stu-id="8bed9-194">For PowerShell, use:</span></span>

```powershell
Remove-AzureRmResourceGroup -Name examplegroup
```

<span data-ttu-id="8bed9-195">Для интерфейса командной строки Azure:</span><span class="sxs-lookup"><span data-stu-id="8bed9-195">For Azure CLI, use:</span></span>

```azurecli
az group delete --name examplegroup
```

## <a name="next-steps"></a><span data-ttu-id="8bed9-196">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8bed9-196">Next steps</span></span>
* <span data-ttu-id="8bed9-197">toolearn Дополнительные сведения о структуре hello шаблона, в разделе [шаблоны разработки Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="8bed9-197">toolearn more about hello structure of a template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="8bed9-198">toolearn о свойствах hello для учетной записи хранения в разделе [ссылка на шаблон учетных записей хранения](/azure/templates/microsoft.storage/storageaccounts).</span><span class="sxs-lookup"><span data-stu-id="8bed9-198">toolearn about hello properties for a storage account, see [storage accounts template reference](/azure/templates/microsoft.storage/storageaccounts).</span></span>
* <span data-ttu-id="8bed9-199">tooview завершения шаблоны для различных типов решений, см. hello [шаблоны быстрый запуск Azure](https://azure.microsoft.com/documentation/templates/).</span><span class="sxs-lookup"><span data-stu-id="8bed9-199">tooview complete templates for many different types of solutions, see hello [Azure Quickstart Templates](https://azure.microsoft.com/documentation/templates/).</span></span>
