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
# <a name="using-linked-templates-when-deploying-azure-resources"></a>Использование связанных шаблонов в при развертывании ресурсов Azure
Из одного шаблона Azure Resource Manager, можно связать tooanother шаблона, который позволяет toodecompose в набор шаблонов с целевым, зависящие от цели развертывания. Как и при разбивке приложения на несколько классов, декомпозиция развертывания гораздо удобнее в контексте тестирования, повторного использования и удобства чтения.  

Из связанного шаблона tooa основного шаблона можно передавать параметры, и эти параметры можно непосредственно сопоставьте tooparameters или переменные, предоставляемые hello вызове шаблона. Hello связанного шаблона можно также передать выходные данные переменной задней toohello исходный шаблон, включение двусторонней данных exchange между шаблонами.

## <a name="linking-tooa-template"></a>Связывание tooa шаблона
Можно создать связь между двух шаблонов, добавив ресурс развертывания в главном шаблоне hello связанного шаблона toohello этой точки. Задать hello **templateLink** toohello свойство URI связанного шаблона hello. Можно указать их значения для связанного шаблона hello непосредственно в шаблоне или в файле параметров. Hello следующий пример использует hello **параметры** toospecify свойство непосредственно значение параметра.

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

Как и другие типы ресурсов можно задать зависимости между связанного шаблона hello и другие ресурсы. Таким образом Если другие ресурсы требуются выходное значение из связанного шаблона hello, гарантированно hello связанного шаблона развертывания перед их. Либо, если hello связанного шаблона зависит от других ресурсов, можно убедиться, что другие ресурсы развертываются перед hello связанного шаблона. Значение можно получить из шаблона, связанного с hello, используя синтаксис:

```json
"[reference('linkedTemplate').outputs.exampleProperty.value]"
```

Hello службы диспетчера ресурсов должно быть связанного шаблона может tooaccess hello. Нельзя указать локальный файл или файл, доступный только в локальной сети для связанного шаблона hello. Можно предоставить только универсальный код ресурса (URI), который включает в себя **http** или **https**. Один из вариантов — tooplace связанного шаблона в учетную запись хранения и использования hello URI для этого элемента, как показано в следующий пример hello:

```json
"templateLink": {
    "uri": "http://mystorageaccount.blob.core.windows.net/templates/template.json",
    "contentVersion": "1.0.0.0",
}
```

Хотя hello связанного шаблона должен быть внешним доступом, не обязательно toobe общедоступной toohello public. Вы можете добавить ваш шаблон tooa личной учетной записи хранения, владелец учетной записи хранилища доступен tooonly hello. Затем создается tooenable токена доступа адреса (SAS) с общего доступа во время развертывания. Добавьте этот SAS маркера toohello URI для связанного шаблона hello. Действия по настройке шаблона в учетной записи хранения и созданию маркера SAS описаны в разделах [Развертывание ресурсов с использованием шаблонов Resource Manager и Azure PowerShell](resource-group-template-deploy.md) и [Развертывание ресурсов с использованием шаблонов Resource Manager и Azure CLI](resource-group-template-deploy-cli.md). 

Следующий пример Hello показан шаблон родительского шаблона tooanother ссылки. Hello связанного шаблона осуществляется с помощью токена SAS, передаваемый в качестве параметра.

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

Несмотря на то, что hello маркер передается в виде защищенной строки, hello URI связанного шаблона hello, включая маркер SAS hello, регистрируется в hello операции развертывания. Уязвимость toolimit задать срок действия маркера hello.

Resource Manager обрабатывает каждый связанный шаблон как отдельное развертывание. В hello журнала развертывания для группы ресурсов hello просмотреть отдельные развертывания для родительского hello и вложенных шаблонов.

![журнал развертываний](./media/resource-group-linked-templates/linked-deployment-history.png)

## <a name="linking-tooa-parameter-file"></a>Файл параметров для связывания tooa
Следующий пример Hello использует hello **parametersLink** файл параметров tooa toolink свойство.

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

значение Hello URI hello параметра связанного файла не может быть локальный файл и необходимо включить **http** или **https**. файл параметров Hello также может быть только tooaccess через маркер SAS.

## <a name="using-variables-toolink-templates"></a>С помощью шаблонов toolink переменных
Hello предыдущих примерах показано жестко закодированные значения URL-адрес ссылки шаблона hello. Этот подход может подойти для простого шаблона, но он не действует при работе с большим набором модульных шаблонов. Вместо этого можно создать статическую переменную, которая содержит базовый URL-адрес для основного шаблона hello и динамически создавать URL-адреса для hello связанных шаблонов из базового URL-адреса. Hello преимущество этого подхода заключается в том, вы можете легко шаблона hello вилки или перемещения, так как требуется только toochange hello статической переменной в главном шаблоне hello. основной шаблон Hello передает hello правильных идентификаторы URI на протяжении hello разложить шаблона.

Hello следующем примере показано, как toouse базового toocreate URL-адреса двух URL-адресов для связанных шаблонов (**sharedTemplateUrl** и **vmTemplate**). 

```json
"variables": {
    "templateBaseUrl": "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/postgresql-on-ubuntu/",
    "sharedTemplateUrl": "[concat(variables('templateBaseUrl'), 'shared-resources.json')]",
    "vmTemplateUrl": "[concat(variables('templateBaseUrl'), 'database-2disk-resources.json')]"
}
```

Можно также использовать [deployment()](resource-group-template-functions-deployment.md#deployment) tooget hello базовый URL-адрес для текущего шаблона hello и использовать этот URL-адрес tooget hello для других шаблонов в hello местоположения. Этот подход полезен при изменении местоположения шаблон (возможно из-за tooversioning) или вы хотите tooavoid жесткого кодирования URL-адреса в файле шаблона hello. 

```json
"variables": {
    "sharedTemplateUrl": "[uri(deployment().properties.templateLink.uri, 'shared-resources.json')]"
}
```

## <a name="complete-example"></a>Полный пример
следующие шаблоны пример Hello Показывать упрощенный ряд связанных шаблонов tooillustrate некоторые основные понятия hello в этой статье. Предполагается, что шаблоны hello были добавлены toohello же контейнера в учетной записи хранения с общий доступ отключен. Hello связанного шаблона передает значение задней toohello основного шаблона hello **выводит** раздела.

Hello **parent.json** файл состоит из:

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

Hello **helloworld.json** файл состоит из:

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

В PowerShell получить токен для контейнера hello и развертывания шаблонов hello с:

```powershell
Set-AzureRmCurrentStorageAccount -ResourceGroupName ManageGroup -Name storagecontosotemplates
$token = New-AzureStorageContainerSASToken -Name templates -Permission r -ExpiryTime (Get-Date).AddMinutes(30.0)
$url = (Get-AzureStorageBlob -Container templates -Blob parent.json).ICloudBlob.uri.AbsoluteUri
New-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup -TemplateUri ($url + $token) -containerSasToken $token
```

В версии 2.0 Azure CLI получить токен для контейнера hello и развертывания шаблонов hello с hello, следующий код:

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

## <a name="next-steps"></a>Дальнейшие действия
* toolearn о hello определение hello порядком развертывания для ресурсов, в разделе [Определение зависимостей в шаблоны Azure Resource Manager](resource-group-define-dependencies.md)
* toolearn toodefine один ресурс, но создавать большое количество экземпляров, в статье [создание нескольких экземпляров ресурсов в диспетчере ресурсов Azure](resource-group-create-multiple.md)

