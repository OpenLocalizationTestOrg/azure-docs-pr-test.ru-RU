---
title: "Создание первого шаблона Azure Resource Manager | Документация Майкрософт"
description: "Пошаговые инструкции по созданию первого шаблона Azure Resource Manager. Здесь объясняется, как создать шаблон, указав в нем ссылку на учетную запись хранения."
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
ms.openlocfilehash: 49086b51e2db1aebed45746306ae14b6f1feb631
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="create-and-deploy-your-first-azure-resource-manager-template"></a><span data-ttu-id="e86a8-104">Создание и развертывание первого шаблона Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e86a8-104">Create and deploy your first Azure Resource Manager template</span></span>
<span data-ttu-id="e86a8-105">В этой статье рассматриваются действия по созданию первого шаблона Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e86a8-105">This topic walks you through the steps of creating your first Azure Resource Manager template.</span></span> <span data-ttu-id="e86a8-106">Шаблоны Resource Manager — это JSON-файлы, которые определяют ресурсы, необходимые для развертывания решения.</span><span class="sxs-lookup"><span data-stu-id="e86a8-106">Resource Manager templates are JSON files that define the resources you need to deploy for your solution.</span></span> <span data-ttu-id="e86a8-107">Основные понятия, связанные с развертыванием и управлением решений Azure, см. в [обзоре Azure Resource Manager](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e86a8-107">To understand the concepts associated with deploying and managing your Azure solutions, see [Azure Resource Manager overview](resource-group-overview.md).</span></span> <span data-ttu-id="e86a8-108">Если вы уже развернули ресурсы и хотите получить для них шаблон, см. статью [Экспорт шаблона Azure Resource Manager из существующих ресурсов](resource-manager-export-template.md).</span><span class="sxs-lookup"><span data-stu-id="e86a8-108">If you have existing resources and want to get a template for those resources, see [Export an Azure Resource Manager template from existing resources](resource-manager-export-template.md).</span></span>

<span data-ttu-id="e86a8-109">Для создания и изменения шаблонов нужен редактор JSON,</span><span class="sxs-lookup"><span data-stu-id="e86a8-109">To create and revise templates, you need a JSON editor.</span></span> <span data-ttu-id="e86a8-110">например [Visual Studio Code](https://code.visualstudio.com/). Это упрощенный кроссплатформенный редактор с открытым исходным кодом.</span><span class="sxs-lookup"><span data-stu-id="e86a8-110">[Visual Studio Code](https://code.visualstudio.com/) is a lightweight, open-source, cross-platform code editor.</span></span> <span data-ttu-id="e86a8-111">Для создания шаблонов Resource Manager мы настоятельно рекомендуем использовать Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="e86a8-111">We strongly recommend using Visual Studio Code for creating Resource Manager templates.</span></span> <span data-ttu-id="e86a8-112">В этой статье предполагается, что вы используете VS Code. Но вы можете использовать и другой редактор JSON (например, Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="e86a8-112">This topic assumes you are using VS Code; however, if you have another JSON editor (like Visual Studio), you can use that editor.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e86a8-113">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="e86a8-113">Prerequisites</span></span>

* <span data-ttu-id="e86a8-114">Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="e86a8-114">Visual Studio Code.</span></span> <span data-ttu-id="e86a8-115">При необходимости установите его со страницы [https://code.visualstudio.com/](https://code.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="e86a8-115">If needed, install it from [https://code.visualstudio.com/](https://code.visualstudio.com/).</span></span>
* <span data-ttu-id="e86a8-116">Подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="e86a8-116">An Azure subscription.</span></span> <span data-ttu-id="e86a8-117">Если у вас еще нет подписки Azure, [создайте бесплатную учетную запись Azure](https://azure.microsoft.com/free/?WT.mc_id=A261C142F), прежде чем начинать работу.</span><span class="sxs-lookup"><span data-stu-id="e86a8-117">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="create-template"></a><span data-ttu-id="e86a8-118">Создание шаблона</span><span class="sxs-lookup"><span data-stu-id="e86a8-118">Create template</span></span>

<span data-ttu-id="e86a8-119">Давайте начнем с простого шаблона, который развертывает учетную запись хранения в подписке.</span><span class="sxs-lookup"><span data-stu-id="e86a8-119">Let's start with a simple template that deploys a storage account to your subscription.</span></span>

1. <span data-ttu-id="e86a8-120">Выберите **Файл** > **Создать файл**.</span><span class="sxs-lookup"><span data-stu-id="e86a8-120">Select **File** > **New File**.</span></span> 

   ![Создание файла](./media/resource-manager-create-first-template/new-file.png)

2. <span data-ttu-id="e86a8-122">Скопируйте и вставьте в него следующий синтаксис JSON:</span><span class="sxs-lookup"><span data-stu-id="e86a8-122">Copy and paste the following JSON syntax into your file:</span></span>

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

   <span data-ttu-id="e86a8-123">Для имен учетных записей хранения существует несколько ограничений, которые усложняют настройку имен.</span><span class="sxs-lookup"><span data-stu-id="e86a8-123">Storage account names have several restrictions that make them difficult to set.</span></span> <span data-ttu-id="e86a8-124">Имя должно содержать от 3 до 24 символов, состоять только из цифр и букв нижнего регистра и быть уникальным.</span><span class="sxs-lookup"><span data-stu-id="e86a8-124">The name must be between 3 and 24 characters in length, use only numbers and lower-case letters, and be unique.</span></span> <span data-ttu-id="e86a8-125">Для создания значения хэша предыдущий шаблон использует функцию [uniqueString](resource-group-template-functions-string.md#uniquestring).</span><span class="sxs-lookup"><span data-stu-id="e86a8-125">The preceding template uses the [uniqueString](resource-group-template-functions-string.md#uniquestring) function to generate a hash value.</span></span> <span data-ttu-id="e86a8-126">Чтобы присвоить этому значению хэша дополнительное значение, он добавляет префикс *storage*.</span><span class="sxs-lookup"><span data-stu-id="e86a8-126">To give this hash value more meaning, it adds the prefix *storage*.</span></span> 

3. <span data-ttu-id="e86a8-127">Сохраните этот файл как **azuredeploy.json** в локальной папке.</span><span class="sxs-lookup"><span data-stu-id="e86a8-127">Save this file as **azuredeploy.json** to a local folder.</span></span>

   ![Сохранение шаблона](./media/resource-manager-create-first-template/save-template.png)

## <a name="deploy-template"></a><span data-ttu-id="e86a8-129">Развертывание шаблона</span><span class="sxs-lookup"><span data-stu-id="e86a8-129">Deploy template</span></span>

<span data-ttu-id="e86a8-130">Теперь вы можете развернуть этот шаблон.</span><span class="sxs-lookup"><span data-stu-id="e86a8-130">You are ready to deploy this template.</span></span> <span data-ttu-id="e86a8-131">Чтобы создать группу ресурсов, вы можете использовать PowerShell или Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="e86a8-131">You use either PowerShell or Azure CLI to create a resource group.</span></span> <span data-ttu-id="e86a8-132">Затем можно развернуть учетную запись хранения в этой группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="e86a8-132">Then, you deploy a storage account to that resource group.</span></span>

* <span data-ttu-id="e86a8-133">Для PowerShell используйте следующие команды из папки, содержащей шаблон:</span><span class="sxs-lookup"><span data-stu-id="e86a8-133">For PowerShell, use the following commands from the folder containing the template:</span></span>

   ```powershell
   Login-AzureRmAccount
   
   New-AzureRmResourceGroup -Name examplegroup -Location "South Central US"
   New-AzureRmResourceGroupDeployment -ResourceGroupName examplegroup -TemplateFile azuredeploy.json
   ```

* <span data-ttu-id="e86a8-134">Для локальной установки Azure CLI используйте следующие команды из папки, содержащей шаблон:</span><span class="sxs-lookup"><span data-stu-id="e86a8-134">For a local installation of Azure CLI, use the following commands from the folder containing the template:</span></span>

   ```azurecli
   az login

   az group create --name examplegroup --location "South Central US"
   az group deployment create --resource-group examplegroup --template-file azuredeploy.json
   ```

<span data-ttu-id="e86a8-135">После завершения развертывания учетная запись хранения будет находиться в группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="e86a8-135">When deployment finishes, your storage account exists in the resource group.</span></span>

## <a name="deploy-template-from-cloud-shell"></a><span data-ttu-id="e86a8-136">Развертывание шаблона из Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="e86a8-136">Deploy template from Cloud Shell</span></span>

<span data-ttu-id="e86a8-137">Вы можете использовать [Cloud Shell](../cloud-shell/overview.md) для выполнения команд Azure CLI для развертывания шаблона.</span><span class="sxs-lookup"><span data-stu-id="e86a8-137">You can use [Cloud Shell](../cloud-shell/overview.md) to run the Azure CLI commands for deploying your template.</span></span> <span data-ttu-id="e86a8-138">Однако сначала необходимо загрузить шаблон в общий файловый ресурс для Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="e86a8-138">However, you must first load your template into the file share for your Cloud Shell.</span></span> <span data-ttu-id="e86a8-139">Если вы еще не использовали Cloud Shell, ознакомьтесь со статьей [Обзор Azure Cloud Shell (предварительная версия)](../cloud-shell/overview.md), чтобы узнать о настройке службы.</span><span class="sxs-lookup"><span data-stu-id="e86a8-139">If you have not used Cloud Shell, see [Overview of Azure Cloud Shell](../cloud-shell/overview.md) for information about setting it up.</span></span>

1. <span data-ttu-id="e86a8-140">Войдите на [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e86a8-140">Log in to the [Azure portal](https://portal.azure.com).</span></span>   

2. <span data-ttu-id="e86a8-141">Выберите свою группу ресурсов Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="e86a8-141">Select your Cloud Shell resource group.</span></span> <span data-ttu-id="e86a8-142">Шаблон имени — `cloud-shell-storage-<region>`.</span><span class="sxs-lookup"><span data-stu-id="e86a8-142">The name pattern is `cloud-shell-storage-<region>`.</span></span>

   ![Выбор группы ресурсов](./media/resource-manager-create-first-template/select-cs-resource-group.png)

3. <span data-ttu-id="e86a8-144">Выберите учетную запись хранения для Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="e86a8-144">Select the storage account for your Cloud Shell.</span></span>

   ![Выбор учетной записи хранения](./media/resource-manager-create-first-template/select-storage.png)

4. <span data-ttu-id="e86a8-146">Выберите **Файлы**.</span><span class="sxs-lookup"><span data-stu-id="e86a8-146">Select **Files**.</span></span>

   ![Выбор файлов](./media/resource-manager-create-first-template/select-files.png)

5. <span data-ttu-id="e86a8-148">Выберите общий файловый ресурс для Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="e86a8-148">Select the file share for Cloud Shell.</span></span> <span data-ttu-id="e86a8-149">Шаблон имени — `cs-<user>-<domain>-com-<uniqueGuid>`.</span><span class="sxs-lookup"><span data-stu-id="e86a8-149">The name pattern is `cs-<user>-<domain>-com-<uniqueGuid>`.</span></span>

   ![Выбор общего файлового ресурса](./media/resource-manager-create-first-template/select-file-share.png)

6. <span data-ttu-id="e86a8-151">Выберите **Добавить каталог**.</span><span class="sxs-lookup"><span data-stu-id="e86a8-151">Select **Add directory**.</span></span>

   ![Добавление каталога](./media/resource-manager-create-first-template/select-add-directory.png)

7. <span data-ttu-id="e86a8-153">Назовите его **templates** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="e86a8-153">Name it **templates**, and select **Okay**.</span></span>

   ![Присвоение имени каталогу](./media/resource-manager-create-first-template/name-templates.png)

8. <span data-ttu-id="e86a8-155">Выберите новый каталог.</span><span class="sxs-lookup"><span data-stu-id="e86a8-155">Select your new directory.</span></span>

   ![Выбор каталога](./media/resource-manager-create-first-template/select-templates.png)

9. <span data-ttu-id="e86a8-157">Щелкните **Отправить**.</span><span class="sxs-lookup"><span data-stu-id="e86a8-157">Select **Upload**.</span></span>

   ![Кнопка "Отправить"](./media/resource-manager-create-first-template/select-upload.png)

10. <span data-ttu-id="e86a8-159">Найдите и отправьте свой шаблон.</span><span class="sxs-lookup"><span data-stu-id="e86a8-159">Find and upload your template.</span></span>

   ![Отправка файла](./media/resource-manager-create-first-template/upload-files.png)

11. <span data-ttu-id="e86a8-161">Откройте командную строку.</span><span class="sxs-lookup"><span data-stu-id="e86a8-161">Open the prompt.</span></span>

   ![Открытие Cloud Shell](./media/resource-manager-create-first-template/start-cloud-shell.png)

12. <span data-ttu-id="e86a8-163">В Cloud Shell введите следующие команды:</span><span class="sxs-lookup"><span data-stu-id="e86a8-163">Enter the following commands in the Cloud Shell:</span></span>

   ```azurecli
   az group create --name examplegroup --location "South Central US"
   az group deployment create --resource-group examplegroup --template-file clouddrive/templates/azuredeploy.json
   ```

<span data-ttu-id="e86a8-164">После завершения развертывания учетная запись хранения будет находиться в группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="e86a8-164">When deployment finishes, your storage account exists in the resource group.</span></span>

## <a name="customize-the-template"></a><span data-ttu-id="e86a8-165">Настройка шаблона</span><span class="sxs-lookup"><span data-stu-id="e86a8-165">Customize the template</span></span>

<span data-ttu-id="e86a8-166">Шаблон работает, как и полагается, но не обладает гибкостью.</span><span class="sxs-lookup"><span data-stu-id="e86a8-166">The template works fine, but it is not flexible.</span></span> <span data-ttu-id="e86a8-167">Он всегда развертывает локально избыточное хранилище в юго-центральный регион США.</span><span class="sxs-lookup"><span data-stu-id="e86a8-167">It always deploys a locally redundant storage to South Central US.</span></span> <span data-ttu-id="e86a8-168">Именем всегда является *storage*, за которым следует значение хэша.</span><span class="sxs-lookup"><span data-stu-id="e86a8-168">The name is always *storage* followed by a hash value.</span></span> <span data-ttu-id="e86a8-169">Чтобы использовать шаблон для различных сценариев, добавьте к нему параметры.</span><span class="sxs-lookup"><span data-stu-id="e86a8-169">To enable using the template for different scenarios, add parameters to the template.</span></span>

<span data-ttu-id="e86a8-170">В примере ниже показан раздел параметров с двумя параметрами.</span><span class="sxs-lookup"><span data-stu-id="e86a8-170">The following example shows the parameters section with two parameters.</span></span> <span data-ttu-id="e86a8-171">Первый параметр, `storageSKU`, позволяет указать тип избыточности.</span><span class="sxs-lookup"><span data-stu-id="e86a8-171">The first parameter `storageSKU` enables you to specify the type of redundancy.</span></span> <span data-ttu-id="e86a8-172">Он ограничивает значения, которые можно передать в значения, допустимые для учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="e86a8-172">It limits the values you can pass in to values that are valid for a storage account.</span></span> <span data-ttu-id="e86a8-173">Он также задает значение по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="e86a8-173">It also specifies a default value.</span></span> <span data-ttu-id="e86a8-174">Второй параметр, `storageNamePrefix`, допускает максимум 11 знаков.</span><span class="sxs-lookup"><span data-stu-id="e86a8-174">The second parameter `storageNamePrefix` is set to allow a maximum of 11 characters.</span></span> <span data-ttu-id="e86a8-175">Он задает значение по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="e86a8-175">It specifies a default value.</span></span>

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
      "description": "The type of replication to use for the storage account."
    }
  },
  "storageNamePrefix": {
    "type": "string",
    "maxLength": 11,
    "defaultValue": "storage",
    "metadata": {
      "description": "The value to use for starting the storage account name. Use only lowercase letters and numbers."
    }
  }
},
```

<span data-ttu-id="e86a8-176">В разделе переменных добавьте переменную с именем `storageName`.</span><span class="sxs-lookup"><span data-stu-id="e86a8-176">In the variables section, add a variable named `storageName`.</span></span> <span data-ttu-id="e86a8-177">Она объединяет значение префикса из параметров и значение хэша из функции [uniqueString](resource-group-template-functions-string.md#uniquestring).</span><span class="sxs-lookup"><span data-stu-id="e86a8-177">It combines the prefix value from the parameters and a hash value from the [uniqueString](resource-group-template-functions-string.md#uniquestring) function.</span></span> <span data-ttu-id="e86a8-178">Эта переменная использует функцию [toLower](resource-group-template-functions-string.md#tolower) для преобразования всех знаков в нижний регистр.</span><span class="sxs-lookup"><span data-stu-id="e86a8-178">It uses the [toLower](resource-group-template-functions-string.md#tolower) function to convert all characters to lowercase.</span></span>

```json
"variables": {
  "storageName": "[concat(toLower(parameters('storageNamePrefix')), uniqueString(resourceGroup().id))]"
},
```

<span data-ttu-id="e86a8-179">Чтобы использовать эти новые значения для учетной записи хранения, измените определение ресурса:</span><span class="sxs-lookup"><span data-stu-id="e86a8-179">To use these new values for your storage account, change the resource definition:</span></span>

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

<span data-ttu-id="e86a8-180">Обратите внимание, что имени учетной записи хранения теперь присвоена добавленная переменная.</span><span class="sxs-lookup"><span data-stu-id="e86a8-180">Notice that the name of the storage account is now set to the variable that you added.</span></span> <span data-ttu-id="e86a8-181">Имени номера SKU присваивается значение параметра.</span><span class="sxs-lookup"><span data-stu-id="e86a8-181">The SKU name is set to the value of the parameter.</span></span> <span data-ttu-id="e86a8-182">Расположению присваивается то же расположение, что и группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="e86a8-182">The location is set the same location as the resource group.</span></span>

<span data-ttu-id="e86a8-183">Сохраните файл.</span><span class="sxs-lookup"><span data-stu-id="e86a8-183">Save your file.</span></span> 

<span data-ttu-id="e86a8-184">После завершения действий, описанных в этой статье, шаблон будет выглядеть так:</span><span class="sxs-lookup"><span data-stu-id="e86a8-184">After completing the steps in this article, your template now looks like:</span></span>

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
        "description": "The type of replication to use for the storage account."
      }
    },   
    "storageNamePrefix": {
      "type": "string",
      "maxLength": 11,
      "defaultValue": "storage",
      "metadata": {
        "description": "The value to use for starting the storage account name. Use only lowercase letters and numbers."
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

## <a name="redeploy-template"></a><span data-ttu-id="e86a8-185">Повторное развертывание шаблона</span><span class="sxs-lookup"><span data-stu-id="e86a8-185">Redeploy template</span></span>

<span data-ttu-id="e86a8-186">Разверните повторно шаблон с другими значениями.</span><span class="sxs-lookup"><span data-stu-id="e86a8-186">Redeploy the template with different values.</span></span>

<span data-ttu-id="e86a8-187">Для PowerShell используйте команду:</span><span class="sxs-lookup"><span data-stu-id="e86a8-187">For PowerShell, use:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName examplegroup -TemplateFile azuredeploy.json -storageNamePrefix newstore -storageSKU Standard_RAGRS
```

<span data-ttu-id="e86a8-188">Для интерфейса командной строки Azure:</span><span class="sxs-lookup"><span data-stu-id="e86a8-188">For Azure CLI, use:</span></span>

```azurecli
az group deployment create --resource-group examplegroup --template-file azuredeploy.json --parameters storageSKU=Standard_RAGRS storageNamePrefix=newstore
```

<span data-ttu-id="e86a8-189">Для Cloud Shell отправьте измененный шаблон в общий файловый ресурс.</span><span class="sxs-lookup"><span data-stu-id="e86a8-189">For the Cloud Shell, upload your changed template to the file share.</span></span> <span data-ttu-id="e86a8-190">Перезапишите существующий файл.</span><span class="sxs-lookup"><span data-stu-id="e86a8-190">Overwrite the existing file.</span></span> <span data-ttu-id="e86a8-191">Затем используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="e86a8-191">Then, use the following command:</span></span>

```azurecli
az group deployment create --resource-group examplegroup --template-file clouddrive/templates/azuredeploy.json --parameters storageSKU=Standard_RAGRS storageNamePrefix=newstore
```

## <a name="clean-up-resources"></a><span data-ttu-id="e86a8-192">Очистка ресурсов</span><span class="sxs-lookup"><span data-stu-id="e86a8-192">Clean up resources</span></span>

<span data-ttu-id="e86a8-193">Если развернутые ресурсы вам больше не нужны, вы можете их удалить. Для этого удалите группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="e86a8-193">When no longer needed, clean up the resources you deployed by deleting the resource group.</span></span>

<span data-ttu-id="e86a8-194">Для PowerShell используйте команду:</span><span class="sxs-lookup"><span data-stu-id="e86a8-194">For PowerShell, use:</span></span>

```powershell
Remove-AzureRmResourceGroup -Name examplegroup
```

<span data-ttu-id="e86a8-195">Для интерфейса командной строки Azure:</span><span class="sxs-lookup"><span data-stu-id="e86a8-195">For Azure CLI, use:</span></span>

```azurecli
az group delete --name examplegroup
```

## <a name="next-steps"></a><span data-ttu-id="e86a8-196">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e86a8-196">Next steps</span></span>
* <span data-ttu-id="e86a8-197">Дополнительные сведения о структуре шаблона см. в статье [Создание шаблонов Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="e86a8-197">To learn more about the structure of a template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="e86a8-198">Дополнительные сведения о свойствах учетной записи хранения см. в статье [Microsoft.Storage/storageAccounts template reference](/azure/templates/microsoft.storage/storageaccounts) (Справочник по шаблону Microsoft.Storage/storageAccounts).</span><span class="sxs-lookup"><span data-stu-id="e86a8-198">To learn about the properties for a storage account, see [storage accounts template reference](/azure/templates/microsoft.storage/storageaccounts).</span></span>
* <span data-ttu-id="e86a8-199">Полные шаблоны для различных типов решений доступны на странице [Шаблоны быстрого запуска Azure](https://azure.microsoft.com/documentation/templates/).</span><span class="sxs-lookup"><span data-stu-id="e86a8-199">To view complete templates for many different types of solutions, see the [Azure Quickstart Templates](https://azure.microsoft.com/documentation/templates/).</span></span>
