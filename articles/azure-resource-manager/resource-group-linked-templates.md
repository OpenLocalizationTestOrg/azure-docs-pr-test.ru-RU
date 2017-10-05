---
title: "Связывание шаблонов для развертывания Azure | Документация Майкрософт"
description: "Описывает, как использовать связанные шаблоны в шаблоне диспетчера ресурсов Azure для создания решения модульных шаблонов. Показывает, как передавать значения параметров, указывать файл параметров и динамически создаваемые URL-адреса."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 27d8c4b2-1e24-45fe-88fd-8cf98a6bb2d2
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/31/2017
ms.author: tomfitz
ms.openlocfilehash: 8b58a83ffd473500dd3f76c09e251f9208527d4f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="using-linked-templates-when-deploying-azure-resources"></a><span data-ttu-id="8c43b-104">Использование связанных шаблонов в при развертывании ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="8c43b-104">Using linked templates when deploying Azure resources</span></span>
<span data-ttu-id="8c43b-105">Один шаблон Azure Resource Manager можно связать с другим шаблоном, что позволяет разбивать развертывания на несколько целевых шаблонов с определенным назначением.</span><span class="sxs-lookup"><span data-stu-id="8c43b-105">From within one Azure Resource Manager template, you can link to another template, which enables you to decompose your deployment into a set of targeted, purpose-specific templates.</span></span> <span data-ttu-id="8c43b-106">Как и при разбивке приложения на несколько классов, декомпозиция развертывания гораздо удобнее в контексте тестирования, повторного использования и удобства чтения.</span><span class="sxs-lookup"><span data-stu-id="8c43b-106">As with decomposing an application into several code classes, decomposition provides benefits in terms of testing, reuse, and readability.</span></span>  

<span data-ttu-id="8c43b-107">Можно передавать параметры из основного шаблона в связанный шаблон. Кроме того, эти параметры можно напрямую сопоставить с параметрами или переменными, предоставляемыми вызывающим шаблоном.</span><span class="sxs-lookup"><span data-stu-id="8c43b-107">You can pass parameters from a main template to a linked template, and those parameters can directly map to parameters or variables exposed by the calling template.</span></span> <span data-ttu-id="8c43b-108">Связанный шаблон может также передать выходную переменную в исходный шаблон, что позволяет активировать двусторонний обмен данными между шаблонами.</span><span class="sxs-lookup"><span data-stu-id="8c43b-108">The linked template can also pass an output variable back to the source template, enabling a two-way data exchange between templates.</span></span>

## <a name="linking-to-a-template"></a><span data-ttu-id="8c43b-109">Создание связи с шаблоном</span><span class="sxs-lookup"><span data-stu-id="8c43b-109">Linking to a template</span></span>
<span data-ttu-id="8c43b-110">Чтобы создать связь между двумя шаблонами, добавьте ресурс развертывания в основном шаблоне, который указывает на связанный шаблон.</span><span class="sxs-lookup"><span data-stu-id="8c43b-110">You create a link between two templates by adding a deployment resource within the main template that points to the linked template.</span></span> <span data-ttu-id="8c43b-111">Задайте для свойства **templateLink** URI связанного шаблона.</span><span class="sxs-lookup"><span data-stu-id="8c43b-111">You set the **templateLink** property to the URI of the linked template.</span></span> <span data-ttu-id="8c43b-112">Значения параметров для связанного шаблона можно указать непосредственно в шаблоне или в файле параметров.</span><span class="sxs-lookup"><span data-stu-id="8c43b-112">You can provide parameter values for the linked template directly in your template or in a parameter file.</span></span> <span data-ttu-id="8c43b-113">В следующем примере используется свойство **parameters** для непосредственного указания значения параметра.</span><span class="sxs-lookup"><span data-stu-id="8c43b-113">The following example uses the **parameters** property to specify a parameter value directly.</span></span>

```json
"resources": [ 
  { 
      "apiVersion": "2017-05-10", 
      "name": "linkedTemplate", 
      "type": "Microsoft.Resources/deployments", 
      "properties": { 
        "mode": "incremental", 
        "templateLink": {
          "uri": "https://www.contoso.com/AzureTemplates/newStorageAccount.json",
          "contentVersion": "1.0.0.0"
        }, 
        "parameters": { 
          "StorageAccountName":{"value": "[parameters('StorageAccountName')]"} 
        } 
      } 
  } 
] 
```

<span data-ttu-id="8c43b-114">Как и для прочих типов ресурсов, вы можете задать зависимости между связанным шаблоном и другими ресурсами.</span><span class="sxs-lookup"><span data-stu-id="8c43b-114">Like other resource types, you can set dependencies between the linked template and other resources.</span></span> <span data-ttu-id="8c43b-115">Следовательно, если другим ресурсам требуется выходное значение из связанного шаблона, то вы можете обеспечить развертывание данного шаблона прежде этих ресурсов.</span><span class="sxs-lookup"><span data-stu-id="8c43b-115">Therefore, when other resources require an output value from the linked template, you can make sure the linked template is deployed before them.</span></span> <span data-ttu-id="8c43b-116">Или, если связанный шаблон зависит от других ресурсов, то вы можете обеспечить их развертывание перед развертыванием связанного шаблона.</span><span class="sxs-lookup"><span data-stu-id="8c43b-116">Or, when the linked template relies on other resources, you can make sure other resources are deployed before the linked template.</span></span> <span data-ttu-id="8c43b-117">Извлечь значение из связанного шаблона можно с помощью приведенного ниже синтаксиса.</span><span class="sxs-lookup"><span data-stu-id="8c43b-117">You can retrieve a value from a linked template with the following syntax:</span></span>

```json
"[reference('linkedTemplate').outputs.exampleProperty.value]"
```

<span data-ttu-id="8c43b-118">Служба Resource Manager должна иметь доступ к связанному шаблону.</span><span class="sxs-lookup"><span data-stu-id="8c43b-118">The Resource Manager service must be able to access the linked template.</span></span> <span data-ttu-id="8c43b-119">В качестве связанного шаблона нельзя указать локальный файл или файл, доступный только в локальной сети.</span><span class="sxs-lookup"><span data-stu-id="8c43b-119">You cannot specify a local file or a file that is only available on your local network for the linked template.</span></span> <span data-ttu-id="8c43b-120">Можно предоставить только универсальный код ресурса (URI), который включает в себя **http** или **https**.</span><span class="sxs-lookup"><span data-stu-id="8c43b-120">You can only provide a URI value that includes either **http** or **https**.</span></span> <span data-ttu-id="8c43b-121">Один из вариантов — разместить связанный шаблон в учетной записи хранения и использовать универсальный код ресурса (URI) этого элемента, как показано в примере ниже.</span><span class="sxs-lookup"><span data-stu-id="8c43b-121">One option is to place your linked template in a storage account, and use the URI for that item, such as shown in the following example:</span></span>

```json
"templateLink": {
    "uri": "http://mystorageaccount.blob.core.windows.net/templates/template.json",
    "contentVersion": "1.0.0.0",
}
```

<span data-ttu-id="8c43b-122">Хотя связанный шаблон должны быть доступен извне, он не должен быть общедоступным.</span><span class="sxs-lookup"><span data-stu-id="8c43b-122">Although the linked template must be externally available, it does not need to be generally available to the public.</span></span> <span data-ttu-id="8c43b-123">Шаблон можно добавить к личной учетной записи хранения, доступ к которой есть только у владельца учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="8c43b-123">You can add your template to a private storage account that is accessible to only the storage account owner.</span></span> <span data-ttu-id="8c43b-124">Затем создайте маркер подписанного URL-адреса для использования при развертывании.</span><span class="sxs-lookup"><span data-stu-id="8c43b-124">Then, you create a shared access signature (SAS) token to enable access during deployment.</span></span> <span data-ttu-id="8c43b-125">Этот маркер SAS добавляется в универсальный код ресурса (URI) связанного шаблона.</span><span class="sxs-lookup"><span data-stu-id="8c43b-125">You add that SAS token to the URI for the linked template.</span></span> <span data-ttu-id="8c43b-126">Действия по настройке шаблона в учетной записи хранения и созданию маркера SAS описаны в разделах [Развертывание ресурсов с использованием шаблонов Resource Manager и Azure PowerShell](resource-group-template-deploy.md) и [Развертывание ресурсов с использованием шаблонов Resource Manager и Azure CLI](resource-group-template-deploy-cli.md).</span><span class="sxs-lookup"><span data-stu-id="8c43b-126">For steps on setting up a template in a storage account and generating a SAS token, see [Deploy resources with Resource Manager templates and Azure PowerShell](resource-group-template-deploy.md) or [Deploy resources with Resource Manager templates and Azure CLI](resource-group-template-deploy-cli.md).</span></span> 

<span data-ttu-id="8c43b-127">В следующем примере показан родительский шаблон, связанный с другим шаблоном.</span><span class="sxs-lookup"><span data-stu-id="8c43b-127">The following example shows a parent template that links to another template.</span></span> <span data-ttu-id="8c43b-128">Для доступа к связанному шаблону используется маркер SAS, который передается в качестве параметра.</span><span class="sxs-lookup"><span data-stu-id="8c43b-128">The linked template is accessed with a SAS token that is passed in as a parameter.</span></span>

```json
"parameters": {
    "sasToken": { "type": "securestring" }
},
"resources": [
    {
        "apiVersion": "2017-05-10",
        "name": "linkedTemplate",
        "type": "Microsoft.Resources/deployments",
        "properties": {
          "mode": "incremental",
          "templateLink": {
            "uri": "[concat('https://storagecontosotemplates.blob.core.windows.net/templates/helloworld.json', parameters('sasToken'))]",
            "contentVersion": "1.0.0.0"
          }
        }
    }
],
```

<span data-ttu-id="8c43b-129">Несмотря на то, что маркер передается в защищенной строке, универсальный код ресурса (URI) связанного шаблона, включающий в себя маркер SAS, добавляется в журнал операций развертывания.</span><span class="sxs-lookup"><span data-stu-id="8c43b-129">Even though the token is passed in as a secure string, the URI of the linked template, including the SAS token, is logged in the deployment operations.</span></span> <span data-ttu-id="8c43b-130">Чтобы снизить риск раскрытия, задайте срок действия маркера.</span><span class="sxs-lookup"><span data-stu-id="8c43b-130">To limit exposure, set an expiration for the token.</span></span>

<span data-ttu-id="8c43b-131">Resource Manager обрабатывает каждый связанный шаблон как отдельное развертывание.</span><span class="sxs-lookup"><span data-stu-id="8c43b-131">Resource Manager handles each linked template as a separate deployment.</span></span> <span data-ttu-id="8c43b-132">В журнале развертывания группы ресурсов отображаются отдельные операции развертывания для родительских и вложенных шаблонов.</span><span class="sxs-lookup"><span data-stu-id="8c43b-132">In the deployment history for the resource group, you see separate deployments for the parent and nested templates.</span></span>

![журнал развертываний](./media/resource-group-linked-templates/linked-deployment-history.png)

## <a name="linking-to-a-parameter-file"></a><span data-ttu-id="8c43b-134">Создание связи с файлом параметров</span><span class="sxs-lookup"><span data-stu-id="8c43b-134">Linking to a parameter file</span></span>
<span data-ttu-id="8c43b-135">В следующем примере используется свойство **parametersLink** привязки к файлу параметров.</span><span class="sxs-lookup"><span data-stu-id="8c43b-135">The next example uses the **parametersLink** property to link to a parameter file.</span></span>

```json
"resources": [ 
  { 
     "apiVersion": "2017-05-10", 
     "name": "linkedTemplate", 
     "type": "Microsoft.Resources/deployments", 
     "properties": { 
       "mode": "incremental", 
       "templateLink": {
          "uri":"https://www.contoso.com/AzureTemplates/newStorageAccount.json",
          "contentVersion":"1.0.0.0"
       }, 
       "parametersLink": { 
          "uri":"https://www.contoso.com/AzureTemplates/parameters.json",
          "contentVersion":"1.0.0.0"
       } 
     } 
  } 
] 
```

<span data-ttu-id="8c43b-136">Значением универсального кода ресурса (URI) для связанного файла параметров не может быть локальный файл, оно должно содержать **http** или **https**.</span><span class="sxs-lookup"><span data-stu-id="8c43b-136">The URI value for the linked parameter file cannot be a local file, and must include either **http** or **https**.</span></span> <span data-ttu-id="8c43b-137">Доступ к файлу параметров также можно ограничить с помощью маркера SAS.</span><span class="sxs-lookup"><span data-stu-id="8c43b-137">The parameter file can also be limited to access through a SAS token.</span></span>

## <a name="using-variables-to-link-templates"></a><span data-ttu-id="8c43b-138">Использование переменных для связывания шаблонов</span><span class="sxs-lookup"><span data-stu-id="8c43b-138">Using variables to link templates</span></span>
<span data-ttu-id="8c43b-139">В предыдущих примерах были показаны жестко запрограммированные значения URL-адреса для ссылок на шаблоны.</span><span class="sxs-lookup"><span data-stu-id="8c43b-139">The previous examples showed hard-coded URL values for the template links.</span></span> <span data-ttu-id="8c43b-140">Этот подход может подойти для простого шаблона, но он не действует при работе с большим набором модульных шаблонов.</span><span class="sxs-lookup"><span data-stu-id="8c43b-140">This approach might work for a simple template but it does not work well when working with a large set of modular templates.</span></span> <span data-ttu-id="8c43b-141">Вместо этого можно создать статическую переменную, которая содержит базовый URL-адрес для основного шаблона, а затем динамически создавать URL-адреса для связанных шаблонов на основе этого адреса.</span><span class="sxs-lookup"><span data-stu-id="8c43b-141">Instead, you can create a static variable that stores a base URL for the main template and then dynamically create URLs for the linked templates from that base URL.</span></span> <span data-ttu-id="8c43b-142">Преимущество этого подхода заключается в том, что можно легко переместить или разветвить шаблон, так как для этого необходимо лишь изменить статическую переменную в основном шаблоне.</span><span class="sxs-lookup"><span data-stu-id="8c43b-142">The benefit of this approach is you can easily move or fork the template because you only need to change the static variable in the main template.</span></span> <span data-ttu-id="8c43b-143">Основной шаблон передает правильные URI через разделенный шаблон.</span><span class="sxs-lookup"><span data-stu-id="8c43b-143">The main template passes the correct URIs throughout the decomposed template.</span></span>

<span data-ttu-id="8c43b-144">В следующем примере показано, как использовать базовый URL-адрес для создания двух URL-адресов для связанных шаблонов (**sharedTemplateUrl** и **vmTemplate**).</span><span class="sxs-lookup"><span data-stu-id="8c43b-144">The following example shows how to use a base URL to create two URLs for linked templates (**sharedTemplateUrl** and **vmTemplate**).</span></span> 

```json
"variables": {
    "templateBaseUrl": "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/postgresql-on-ubuntu/",
    "sharedTemplateUrl": "[concat(variables('templateBaseUrl'), 'shared-resources.json')]",
    "vmTemplateUrl": "[concat(variables('templateBaseUrl'), 'database-2disk-resources.json')]"
}
```

<span data-ttu-id="8c43b-145">Вы также можете получить базовый URL-адрес текущего шаблона с помощью функции [deployment()](resource-group-template-functions-deployment.md#deployment) , а затем использовать его для получения URL-адресов других шаблонов в том же расположении.</span><span class="sxs-lookup"><span data-stu-id="8c43b-145">You can also use [deployment()](resource-group-template-functions-deployment.md#deployment) to get the base URL for the current template, and use that to get the URL for other templates in the same location.</span></span> <span data-ttu-id="8c43b-146">Это полезно, если расположение шаблонов меняется (например, при выходе новой версии) или если вы не хотите указывать URL-адреса непосредственно в файле шаблона.</span><span class="sxs-lookup"><span data-stu-id="8c43b-146">This approach is useful if your template location changes (maybe due to versioning) or you want to avoid hard coding URLs in the template file.</span></span> 

```json
"variables": {
    "sharedTemplateUrl": "[uri(deployment().properties.templateLink.uri, 'shared-resources.json')]"
}
```

## <a name="complete-example"></a><span data-ttu-id="8c43b-147">Полный пример</span><span class="sxs-lookup"><span data-stu-id="8c43b-147">Complete example</span></span>
<span data-ttu-id="8c43b-148">В следующих примерах шаблонов показано упрощенное размещение связанных шаблонов, чтобы проиллюстрировать некоторые основные понятия, используемые в этой статье.</span><span class="sxs-lookup"><span data-stu-id="8c43b-148">The following example templates show a simplified arrangement of linked templates to illustrate several of the concepts in this article.</span></span> <span data-ttu-id="8c43b-149">Предполагается, что шаблоны были добавлены в один контейнер в учетной записи хранения, для которой отключен общий доступ.</span><span class="sxs-lookup"><span data-stu-id="8c43b-149">It assumes the templates have been added to the same container in a storage account with public access turned off.</span></span> <span data-ttu-id="8c43b-150">Связанный шаблон передает значение обратно в основной шаблон в разделе **outputs** .</span><span class="sxs-lookup"><span data-stu-id="8c43b-150">The linked template passes a value back to the main template in the **outputs** section.</span></span>

<span data-ttu-id="8c43b-151">Содержимое файла **Parent.json** :</span><span class="sxs-lookup"><span data-stu-id="8c43b-151">The **parent.json** file consists of:</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "containerSasToken": { "type": "string" }
  },
  "resources": [
    {
      "apiVersion": "2017-05-10",
      "name": "linkedTemplate",
      "type": "Microsoft.Resources/deployments",
      "properties": {
        "mode": "incremental",
        "templateLink": {
          "uri": "[concat(uri(deployment().properties.templateLink.uri, 'helloworld.json'), parameters('containerSasToken'))]",
          "contentVersion": "1.0.0.0"
        }
      }
    }
  ],
  "outputs": {
    "result": {
      "type": "string",
      "value": "[reference('linkedTemplate').outputs.result.value]"
    }
  }
}
```

<span data-ttu-id="8c43b-152">Содержимое файла **helloworld.json** :</span><span class="sxs-lookup"><span data-stu-id="8c43b-152">The **helloworld.json** file consists of:</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {},
  "variables": {},
  "resources": [],
  "outputs": {
    "result": {
        "value": "Hello World",
        "type" : "string"
    }
  }
}
```

<span data-ttu-id="8c43b-153">В PowerShell происходит получение маркера для контейнера и развертывание шаблонов с помощью следующей команды.</span><span class="sxs-lookup"><span data-stu-id="8c43b-153">In PowerShell, you get a token for the container and deploy the templates with:</span></span>

```powershell
Set-AzureRmCurrentStorageAccount -ResourceGroupName ManageGroup -Name storagecontosotemplates
$token = New-AzureStorageContainerSASToken -Name templates -Permission r -ExpiryTime (Get-Date).AddMinutes(30.0)
$url = (Get-AzureStorageBlob -Container templates -Blob parent.json).ICloudBlob.uri.AbsoluteUri
New-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup -TemplateUri ($url + $token) -containerSasToken $token
```

<span data-ttu-id="8c43b-154">В Azure CLI 2.0 осуществляется получение маркера для контейнера и развертывание шаблонов с помощью следующего кода.</span><span class="sxs-lookup"><span data-stu-id="8c43b-154">In Azure CLI 2.0, you get a token for the container and deploy the templates with the following code:</span></span>

```azurecli
expiretime=$(date -u -d '30 minutes' +%Y-%m-%dT%H:%MZ)
connection=$(az storage account show-connection-string \
    --resource-group ManageGroup \
    --name storagecontosotemplates \
    --query connectionString)
token=$(az storage container generate-sas \
    --name templates \
    --expiry $expiretime \
    --permissions r \
    --output tsv \
    --connection-string $connection)
url=$(az storage blob url \
    --container-name templates \
    --name parent.json \
    --output tsv \
    --connection-string $connection)
parameter='{"containerSasToken":{"value":"?'$token'"}}'
az group deployment create --resource-group ExampleGroup --template-uri $url?$token --parameters $parameter
```

## <a name="next-steps"></a><span data-ttu-id="8c43b-155">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8c43b-155">Next steps</span></span>
* <span data-ttu-id="8c43b-156">Сведения о том, как определить порядок развертывания ресурсов, см. в статье [Определение зависимостей в шаблонах Azure Resource Manager](resource-group-define-dependencies.md).</span><span class="sxs-lookup"><span data-stu-id="8c43b-156">To learn about the defining the deployment order for your resources, see [Defining dependencies in Azure Resource Manager templates](resource-group-define-dependencies.md)</span></span>
* <span data-ttu-id="8c43b-157">Сведения о том, как определить один ресурс и создать несколько экземпляров, см. в статье [Создание нескольких экземпляров ресурсов в Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="8c43b-157">To learn how to define one resource but create many instances of it, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md)</span></span>

