---
title: "шаблоны aaaLink для развертывания Azure | Документы Microsoft"
description: "Описывает, как toouse связанных шаблонов в toocreate шаблона диспетчера ресурсов Azure модульной шаблонное решение. Показывает, как значения параметров toopass, укажите файл параметров и динамически созданные URL-адреса."
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
ms.openlocfilehash: b935b1810db5ce894d009403cd4bb945cab34ba7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="using-linked-templates-when-deploying-azure-resources"></a><span data-ttu-id="03e1c-104">Использование связанных шаблонов в при развертывании ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="03e1c-104">Using linked templates when deploying Azure resources</span></span>
<span data-ttu-id="03e1c-105">Из одного шаблона Azure Resource Manager, можно связать tooanother шаблона, который позволяет toodecompose в набор шаблонов с целевым, зависящие от цели развертывания.</span><span class="sxs-lookup"><span data-stu-id="03e1c-105">From within one Azure Resource Manager template, you can link tooanother template, which enables you toodecompose your deployment into a set of targeted, purpose-specific templates.</span></span> <span data-ttu-id="03e1c-106">Как и при разбивке приложения на несколько классов, декомпозиция развертывания гораздо удобнее в контексте тестирования, повторного использования и удобства чтения.</span><span class="sxs-lookup"><span data-stu-id="03e1c-106">As with decomposing an application into several code classes, decomposition provides benefits in terms of testing, reuse, and readability.</span></span>  

<span data-ttu-id="03e1c-107">Из связанного шаблона tooa основного шаблона можно передавать параметры, и эти параметры можно непосредственно сопоставьте tooparameters или переменные, предоставляемые hello вызове шаблона.</span><span class="sxs-lookup"><span data-stu-id="03e1c-107">You can pass parameters from a main template tooa linked template, and those parameters can directly map tooparameters or variables exposed by hello calling template.</span></span> <span data-ttu-id="03e1c-108">Hello связанного шаблона можно также передать выходные данные переменной задней toohello исходный шаблон, включение двусторонней данных exchange между шаблонами.</span><span class="sxs-lookup"><span data-stu-id="03e1c-108">hello linked template can also pass an output variable back toohello source template, enabling a two-way data exchange between templates.</span></span>

## <a name="linking-tooa-template"></a><span data-ttu-id="03e1c-109">Связывание tooa шаблона</span><span class="sxs-lookup"><span data-stu-id="03e1c-109">Linking tooa template</span></span>
<span data-ttu-id="03e1c-110">Можно создать связь между двух шаблонов, добавив ресурс развертывания в главном шаблоне hello связанного шаблона toohello этой точки.</span><span class="sxs-lookup"><span data-stu-id="03e1c-110">You create a link between two templates by adding a deployment resource within hello main template that points toohello linked template.</span></span> <span data-ttu-id="03e1c-111">Задать hello **templateLink** toohello свойство URI связанного шаблона hello.</span><span class="sxs-lookup"><span data-stu-id="03e1c-111">You set hello **templateLink** property toohello URI of hello linked template.</span></span> <span data-ttu-id="03e1c-112">Можно указать их значения для связанного шаблона hello непосредственно в шаблоне или в файле параметров.</span><span class="sxs-lookup"><span data-stu-id="03e1c-112">You can provide parameter values for hello linked template directly in your template or in a parameter file.</span></span> <span data-ttu-id="03e1c-113">Hello следующий пример использует hello **параметры** toospecify свойство непосредственно значение параметра.</span><span class="sxs-lookup"><span data-stu-id="03e1c-113">hello following example uses hello **parameters** property toospecify a parameter value directly.</span></span>

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

<span data-ttu-id="03e1c-114">Как и другие типы ресурсов можно задать зависимости между связанного шаблона hello и другие ресурсы.</span><span class="sxs-lookup"><span data-stu-id="03e1c-114">Like other resource types, you can set dependencies between hello linked template and other resources.</span></span> <span data-ttu-id="03e1c-115">Таким образом Если другие ресурсы требуются выходное значение из связанного шаблона hello, гарантированно hello связанного шаблона развертывания перед их.</span><span class="sxs-lookup"><span data-stu-id="03e1c-115">Therefore, when other resources require an output value from hello linked template, you can make sure hello linked template is deployed before them.</span></span> <span data-ttu-id="03e1c-116">Либо, если hello связанного шаблона зависит от других ресурсов, можно убедиться, что другие ресурсы развертываются перед hello связанного шаблона.</span><span class="sxs-lookup"><span data-stu-id="03e1c-116">Or, when hello linked template relies on other resources, you can make sure other resources are deployed before hello linked template.</span></span> <span data-ttu-id="03e1c-117">Значение можно получить из шаблона, связанного с hello, используя синтаксис:</span><span class="sxs-lookup"><span data-stu-id="03e1c-117">You can retrieve a value from a linked template with hello following syntax:</span></span>

```json
"[reference('linkedTemplate').outputs.exampleProperty.value]"
```

<span data-ttu-id="03e1c-118">Hello службы диспетчера ресурсов должно быть связанного шаблона может tooaccess hello.</span><span class="sxs-lookup"><span data-stu-id="03e1c-118">hello Resource Manager service must be able tooaccess hello linked template.</span></span> <span data-ttu-id="03e1c-119">Нельзя указать локальный файл или файл, доступный только в локальной сети для связанного шаблона hello.</span><span class="sxs-lookup"><span data-stu-id="03e1c-119">You cannot specify a local file or a file that is only available on your local network for hello linked template.</span></span> <span data-ttu-id="03e1c-120">Можно предоставить только универсальный код ресурса (URI), который включает в себя **http** или **https**.</span><span class="sxs-lookup"><span data-stu-id="03e1c-120">You can only provide a URI value that includes either **http** or **https**.</span></span> <span data-ttu-id="03e1c-121">Один из вариантов — tooplace связанного шаблона в учетную запись хранения и использования hello URI для этого элемента, как показано в следующий пример hello:</span><span class="sxs-lookup"><span data-stu-id="03e1c-121">One option is tooplace your linked template in a storage account, and use hello URI for that item, such as shown in hello following example:</span></span>

```json
"templateLink": {
    "uri": "http://mystorageaccount.blob.core.windows.net/templates/template.json",
    "contentVersion": "1.0.0.0",
}
```

<span data-ttu-id="03e1c-122">Хотя hello связанного шаблона должен быть внешним доступом, не обязательно toobe общедоступной toohello public.</span><span class="sxs-lookup"><span data-stu-id="03e1c-122">Although hello linked template must be externally available, it does not need toobe generally available toohello public.</span></span> <span data-ttu-id="03e1c-123">Вы можете добавить ваш шаблон tooa личной учетной записи хранения, владелец учетной записи хранилища доступен tooonly hello.</span><span class="sxs-lookup"><span data-stu-id="03e1c-123">You can add your template tooa private storage account that is accessible tooonly hello storage account owner.</span></span> <span data-ttu-id="03e1c-124">Затем создается tooenable токена доступа адреса (SAS) с общего доступа во время развертывания.</span><span class="sxs-lookup"><span data-stu-id="03e1c-124">Then, you create a shared access signature (SAS) token tooenable access during deployment.</span></span> <span data-ttu-id="03e1c-125">Добавьте этот SAS маркера toohello URI для связанного шаблона hello.</span><span class="sxs-lookup"><span data-stu-id="03e1c-125">You add that SAS token toohello URI for hello linked template.</span></span> <span data-ttu-id="03e1c-126">Действия по настройке шаблона в учетной записи хранения и созданию маркера SAS описаны в разделах [Развертывание ресурсов с использованием шаблонов Resource Manager и Azure PowerShell](resource-group-template-deploy.md) и [Развертывание ресурсов с использованием шаблонов Resource Manager и Azure CLI](resource-group-template-deploy-cli.md).</span><span class="sxs-lookup"><span data-stu-id="03e1c-126">For steps on setting up a template in a storage account and generating a SAS token, see [Deploy resources with Resource Manager templates and Azure PowerShell](resource-group-template-deploy.md) or [Deploy resources with Resource Manager templates and Azure CLI](resource-group-template-deploy-cli.md).</span></span> 

<span data-ttu-id="03e1c-127">Следующий пример Hello показан шаблон родительского шаблона tooanother ссылки.</span><span class="sxs-lookup"><span data-stu-id="03e1c-127">hello following example shows a parent template that links tooanother template.</span></span> <span data-ttu-id="03e1c-128">Hello связанного шаблона осуществляется с помощью токена SAS, передаваемый в качестве параметра.</span><span class="sxs-lookup"><span data-stu-id="03e1c-128">hello linked template is accessed with a SAS token that is passed in as a parameter.</span></span>

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

<span data-ttu-id="03e1c-129">Несмотря на то, что hello маркер передается в виде защищенной строки, hello URI связанного шаблона hello, включая маркер SAS hello, регистрируется в hello операции развертывания.</span><span class="sxs-lookup"><span data-stu-id="03e1c-129">Even though hello token is passed in as a secure string, hello URI of hello linked template, including hello SAS token, is logged in hello deployment operations.</span></span> <span data-ttu-id="03e1c-130">Уязвимость toolimit задать срок действия маркера hello.</span><span class="sxs-lookup"><span data-stu-id="03e1c-130">toolimit exposure, set an expiration for hello token.</span></span>

<span data-ttu-id="03e1c-131">Resource Manager обрабатывает каждый связанный шаблон как отдельное развертывание.</span><span class="sxs-lookup"><span data-stu-id="03e1c-131">Resource Manager handles each linked template as a separate deployment.</span></span> <span data-ttu-id="03e1c-132">В hello журнала развертывания для группы ресурсов hello просмотреть отдельные развертывания для родительского hello и вложенных шаблонов.</span><span class="sxs-lookup"><span data-stu-id="03e1c-132">In hello deployment history for hello resource group, you see separate deployments for hello parent and nested templates.</span></span>

![журнал развертываний](./media/resource-group-linked-templates/linked-deployment-history.png)

## <a name="linking-tooa-parameter-file"></a><span data-ttu-id="03e1c-134">Файл параметров для связывания tooa</span><span class="sxs-lookup"><span data-stu-id="03e1c-134">Linking tooa parameter file</span></span>
<span data-ttu-id="03e1c-135">Следующий пример Hello использует hello **parametersLink** файл параметров tooa toolink свойство.</span><span class="sxs-lookup"><span data-stu-id="03e1c-135">hello next example uses hello **parametersLink** property toolink tooa parameter file.</span></span>

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

<span data-ttu-id="03e1c-136">значение Hello URI hello параметра связанного файла не может быть локальный файл и необходимо включить **http** или **https**.</span><span class="sxs-lookup"><span data-stu-id="03e1c-136">hello URI value for hello linked parameter file cannot be a local file, and must include either **http** or **https**.</span></span> <span data-ttu-id="03e1c-137">файл параметров Hello также может быть только tooaccess через маркер SAS.</span><span class="sxs-lookup"><span data-stu-id="03e1c-137">hello parameter file can also be limited tooaccess through a SAS token.</span></span>

## <a name="using-variables-toolink-templates"></a><span data-ttu-id="03e1c-138">С помощью шаблонов toolink переменных</span><span class="sxs-lookup"><span data-stu-id="03e1c-138">Using variables toolink templates</span></span>
<span data-ttu-id="03e1c-139">Hello предыдущих примерах показано жестко закодированные значения URL-адрес ссылки шаблона hello.</span><span class="sxs-lookup"><span data-stu-id="03e1c-139">hello previous examples showed hard-coded URL values for hello template links.</span></span> <span data-ttu-id="03e1c-140">Этот подход может подойти для простого шаблона, но он не действует при работе с большим набором модульных шаблонов.</span><span class="sxs-lookup"><span data-stu-id="03e1c-140">This approach might work for a simple template but it does not work well when working with a large set of modular templates.</span></span> <span data-ttu-id="03e1c-141">Вместо этого можно создать статическую переменную, которая содержит базовый URL-адрес для основного шаблона hello и динамически создавать URL-адреса для hello связанных шаблонов из базового URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="03e1c-141">Instead, you can create a static variable that stores a base URL for hello main template and then dynamically create URLs for hello linked templates from that base URL.</span></span> <span data-ttu-id="03e1c-142">Hello преимущество этого подхода заключается в том, вы можете легко шаблона hello вилки или перемещения, так как требуется только toochange hello статической переменной в главном шаблоне hello.</span><span class="sxs-lookup"><span data-stu-id="03e1c-142">hello benefit of this approach is you can easily move or fork hello template because you only need toochange hello static variable in hello main template.</span></span> <span data-ttu-id="03e1c-143">основной шаблон Hello передает hello правильных идентификаторы URI на протяжении hello разложить шаблона.</span><span class="sxs-lookup"><span data-stu-id="03e1c-143">hello main template passes hello correct URIs throughout hello decomposed template.</span></span>

<span data-ttu-id="03e1c-144">Hello следующем примере показано, как toouse базового toocreate URL-адреса двух URL-адресов для связанных шаблонов (**sharedTemplateUrl** и **vmTemplate**).</span><span class="sxs-lookup"><span data-stu-id="03e1c-144">hello following example shows how toouse a base URL toocreate two URLs for linked templates (**sharedTemplateUrl** and **vmTemplate**).</span></span> 

```json
"variables": {
    "templateBaseUrl": "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/postgresql-on-ubuntu/",
    "sharedTemplateUrl": "[concat(variables('templateBaseUrl'), 'shared-resources.json')]",
    "vmTemplateUrl": "[concat(variables('templateBaseUrl'), 'database-2disk-resources.json')]"
}
```

<span data-ttu-id="03e1c-145">Можно также использовать [deployment()](resource-group-template-functions-deployment.md#deployment) tooget hello базовый URL-адрес для текущего шаблона hello и использовать этот URL-адрес tooget hello для других шаблонов в hello местоположения.</span><span class="sxs-lookup"><span data-stu-id="03e1c-145">You can also use [deployment()](resource-group-template-functions-deployment.md#deployment) tooget hello base URL for hello current template, and use that tooget hello URL for other templates in hello same location.</span></span> <span data-ttu-id="03e1c-146">Этот подход полезен при изменении местоположения шаблон (возможно из-за tooversioning) или вы хотите tooavoid жесткого кодирования URL-адреса в файле шаблона hello.</span><span class="sxs-lookup"><span data-stu-id="03e1c-146">This approach is useful if your template location changes (maybe due tooversioning) or you want tooavoid hard coding URLs in hello template file.</span></span> 

```json
"variables": {
    "sharedTemplateUrl": "[uri(deployment().properties.templateLink.uri, 'shared-resources.json')]"
}
```

## <a name="complete-example"></a><span data-ttu-id="03e1c-147">Полный пример</span><span class="sxs-lookup"><span data-stu-id="03e1c-147">Complete example</span></span>
<span data-ttu-id="03e1c-148">следующие шаблоны пример Hello Показывать упрощенный ряд связанных шаблонов tooillustrate некоторые основные понятия hello в этой статье.</span><span class="sxs-lookup"><span data-stu-id="03e1c-148">hello following example templates show a simplified arrangement of linked templates tooillustrate several of hello concepts in this article.</span></span> <span data-ttu-id="03e1c-149">Предполагается, что шаблоны hello были добавлены toohello же контейнера в учетной записи хранения с общий доступ отключен.</span><span class="sxs-lookup"><span data-stu-id="03e1c-149">It assumes hello templates have been added toohello same container in a storage account with public access turned off.</span></span> <span data-ttu-id="03e1c-150">Hello связанного шаблона передает значение задней toohello основного шаблона hello **выводит** раздела.</span><span class="sxs-lookup"><span data-stu-id="03e1c-150">hello linked template passes a value back toohello main template in hello **outputs** section.</span></span>

<span data-ttu-id="03e1c-151">Hello **parent.json** файл состоит из:</span><span class="sxs-lookup"><span data-stu-id="03e1c-151">hello **parent.json** file consists of:</span></span>

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

<span data-ttu-id="03e1c-152">Hello **helloworld.json** файл состоит из:</span><span class="sxs-lookup"><span data-stu-id="03e1c-152">hello **helloworld.json** file consists of:</span></span>

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

<span data-ttu-id="03e1c-153">В PowerShell получить токен для контейнера hello и развертывания шаблонов hello с:</span><span class="sxs-lookup"><span data-stu-id="03e1c-153">In PowerShell, you get a token for hello container and deploy hello templates with:</span></span>

```powershell
Set-AzureRmCurrentStorageAccount -ResourceGroupName ManageGroup -Name storagecontosotemplates
$token = New-AzureStorageContainerSASToken -Name templates -Permission r -ExpiryTime (Get-Date).AddMinutes(30.0)
$url = (Get-AzureStorageBlob -Container templates -Blob parent.json).ICloudBlob.uri.AbsoluteUri
New-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup -TemplateUri ($url + $token) -containerSasToken $token
```

<span data-ttu-id="03e1c-154">В версии 2.0 Azure CLI получить токен для контейнера hello и развертывания шаблонов hello с hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="03e1c-154">In Azure CLI 2.0, you get a token for hello container and deploy hello templates with hello following code:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="03e1c-155">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="03e1c-155">Next steps</span></span>
* <span data-ttu-id="03e1c-156">toolearn о hello определение hello порядком развертывания для ресурсов, в разделе [Определение зависимостей в шаблоны Azure Resource Manager](resource-group-define-dependencies.md)</span><span class="sxs-lookup"><span data-stu-id="03e1c-156">toolearn about hello defining hello deployment order for your resources, see [Defining dependencies in Azure Resource Manager templates](resource-group-define-dependencies.md)</span></span>
* <span data-ttu-id="03e1c-157">toolearn toodefine один ресурс, но создавать большое количество экземпляров, в статье [создание нескольких экземпляров ресурсов в диспетчере ресурсов Azure](resource-group-create-multiple.md)</span><span class="sxs-lookup"><span data-stu-id="03e1c-157">toolearn how toodefine one resource but create many instances of it, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md)</span></span>

