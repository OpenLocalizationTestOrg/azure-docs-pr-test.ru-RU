---
title: "aaaMounting томе файлов Azure в экземплярах контейнера Azure"
description: "Узнайте, как toomount Azure файлы toopersist состояние томов с экземплярами контейнера Azure"
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: d87215e06d5e5af40bfebcad17768ee45ccabbb2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="mounting-an-azure-file-share-with-azure-container-instances"></a><span data-ttu-id="216bd-103">Подключение файлового ресурса Azure с помощью Экземпляров контейнеров Azure</span><span class="sxs-lookup"><span data-stu-id="216bd-103">Mounting an Azure file share with Azure Container Instances</span></span>

<span data-ttu-id="216bd-104">По умолчанию в Экземплярах контейнеров Azure не отслеживается состояние.</span><span class="sxs-lookup"><span data-stu-id="216bd-104">By default, Azure Container Instances are stateless.</span></span> <span data-ttu-id="216bd-105">Если контейнер hello аварийно завершает работу или останавливается, свое состояние будет потеряно.</span><span class="sxs-lookup"><span data-stu-id="216bd-105">If hello container crashes or stops, all of its state is lost.</span></span> <span data-ttu-id="216bd-106">toopersist состояния вне пределов продолжительности hello hello контейнера, необходимо подключить том из внешнего хранилища.</span><span class="sxs-lookup"><span data-stu-id="216bd-106">toopersist state beyond hello lifetime of hello container, you must mount a volume from an external store.</span></span> <span data-ttu-id="216bd-107">В этой статье показано, как toomount Azure общей папки для использования с экземплярами Azure контейнера.</span><span class="sxs-lookup"><span data-stu-id="216bd-107">This article shows how toomount an Azure file share for use with Azure Container Instances.</span></span>

## <a name="create-an-azure-file-share"></a><span data-ttu-id="216bd-108">Создание файлового ресурса Azure</span><span class="sxs-lookup"><span data-stu-id="216bd-108">Create an Azure file share</span></span>

<span data-ttu-id="216bd-109">Перед использованием файлового ресурса Azure с Экземплярами контейнеров Azure необходимо создать его.</span><span class="sxs-lookup"><span data-stu-id="216bd-109">Before using an Azure file share with Azure Container Instances, you must create it.</span></span> <span data-ttu-id="216bd-110">Запустите следующий сценарий toocreate общей папки хранилища учетной записи toohost hello и hello общей папки самого hello.</span><span class="sxs-lookup"><span data-stu-id="216bd-110">Run hello following script toocreate a storage account toohost hello file share and hello share itself.</span></span> <span data-ttu-id="216bd-111">Обратите внимание, что имя учетной записи хранения, hello должно быть глобально уникальным, поэтому скрипт hello добавляет строку базовый toohello случайное значение.</span><span class="sxs-lookup"><span data-stu-id="216bd-111">Note that hello storage account name must be globally unique, so hello script adds a random value toohello base string.</span></span>

```azurecli-interactive
# Change these four parameters
ACI_PERS_STORAGE_ACCOUNT_NAME=mystorageaccount$RANDOM
ACI_PERS_RESOURCE_GROUP=myResourceGroup
ACI_PERS_LOCATION=eastus
ACI_PERS_SHARE_NAME=acishare

# Create hello storage account with hello parameters
az storage account create -n $ACI_PERS_STORAGE_ACCOUNT_NAME -g $ACI_PERS_RESOURCE_GROUP -l $ACI_PERS_LOCATION --sku Standard_LRS

# Export hello connection string as an environment variable, this is used when creating hello Azure file share
export AZURE_STORAGE_CONNECTION_STRING=`az storage account show-connection-string -n $ACI_PERS_STORAGE_ACCOUNT_NAME -g $ACI_PERS_RESOURCE_GROUP -o tsv`

# Create hello share
az storage share create -n $ACI_PERS_SHARE_NAME
```

## <a name="acquire-storage-account-access-details"></a><span data-ttu-id="216bd-112">Получение данных для доступа к учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="216bd-112">Acquire storage account access details</span></span>

<span data-ttu-id="216bd-113">toomount файл Azure совместное использование в качестве тома в Azure экземпляров контейнера, требуются три значения: hello имя учетной записи хранения, имя общего ресурса hello и ключ доступа к хранилищу hello.</span><span class="sxs-lookup"><span data-stu-id="216bd-113">toomount an Azure file share as a volume in Azure Container Instances, you need three values: hello storage account name, hello share name, and hello storage access key.</span></span> 

<span data-ttu-id="216bd-114">Если вы использовали hello сценарий, приведенный выше, имя учетной записи хранения hello был создан случайным значением в конце hello.</span><span class="sxs-lookup"><span data-stu-id="216bd-114">If you used hello script above, hello storage account name was created with a random value at hello end.</span></span> <span data-ttu-id="216bd-115">Окончательная строка hello tooquery (включая hello случайных часть), используйте hello, следующие команды:</span><span class="sxs-lookup"><span data-stu-id="216bd-115">tooquery hello final string (including hello random portion), use hello following commands:</span></span>

```azurecli-interactive
STORAGE_ACCOUNT=$(az storage account list --resource-group myResourceGroup --query "[?contains(name,'mystorageaccount')].[name]" -o tsv)
echo $STORAGE_ACCOUNT
```

<span data-ttu-id="216bd-116">Hello имя общего ресурса уже известна (это *acishare* в скрипте hello выше), поэтому все, остается только hello ключ учетной записи хранения, которую можно найти с помощью hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="216bd-116">hello share name is already known (it is *acishare* in hello script above), so all that remains is hello storage account key, which can be found using hello following command:</span></span>

```azurecli-interactive
$STORAGE_KEY=$(az storage account keys list --resource-group myResourceGroup --account-name $STORAGE_ACCOUNT --query "[0].value" -o tsv)
echo $STORAGE_KEY
```

## <a name="store-storage-account-access-details-with-azure-key-vault"></a><span data-ttu-id="216bd-117">Сохранение сведений о доступе к учетной записи хранения с помощью хранилища ключей Azure</span><span class="sxs-lookup"><span data-stu-id="216bd-117">Store storage account access details with Azure key vault</span></span>

<span data-ttu-id="216bd-118">Ключи учетной записи хранения защиты доступа к данным tooyour, поэтому рекомендуется хранить их в хранилище ключей Azure.</span><span class="sxs-lookup"><span data-stu-id="216bd-118">Storage account keys protect access tooyour data, so we recommend storing them in an Azure key vault.</span></span> 

<span data-ttu-id="216bd-119">Создание хранилища ключей с hello Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="216bd-119">Create a key vault with hello Azure CLI:</span></span>

```azurecli-interactive
KEYVAULT_NAME=aci-keyvault
az keyvault create -n $KEYVAULT_NAME --enabled-for-template-deployment -g myResourceGroup
```

<span data-ttu-id="216bd-120">Hello `enabled-for-template-deployment` переключатель Azure Resource Manager toopull секретов из хранилища ключей во время развертывания.</span><span class="sxs-lookup"><span data-stu-id="216bd-120">hello `enabled-for-template-deployment` switch allows Azure Resource Manager toopull secrets from your key vault at deployment time.</span></span>

<span data-ttu-id="216bd-121">Хранить ключ учетной записи хранения hello как новый секрет в хранилище ключей hello:</span><span class="sxs-lookup"><span data-stu-id="216bd-121">Store hello storage account key as a new secret in hello key vault:</span></span>

```azurecli-interactive
KEYVAULT_SECRET_NAME=azurefilesstoragekey
az keyvault secret set --vault-name $KEYVAULT_NAME --name $KEYVAULT_SECRET_NAME --value $STORAGE_KEY
```

## <a name="mount-hello-volume"></a><span data-ttu-id="216bd-122">Подключить том hello</span><span class="sxs-lookup"><span data-stu-id="216bd-122">Mount hello volume</span></span>

<span data-ttu-id="216bd-123">Подключение файлового ресурса Azure как тома в контейнере состоит из двух этапов.</span><span class="sxs-lookup"><span data-stu-id="216bd-123">Mounting an Azure file share as a volume in a container is a two-step process.</span></span> <span data-ttu-id="216bd-124">Во-первых вы подробно hello hello общей папки, как часть определения группы контейнеров hello, а затем укажите способ hello тома подключены в один или несколько контейнеров hello в группе hello.</span><span class="sxs-lookup"><span data-stu-id="216bd-124">First, you provide hello details of hello share as part of defining hello container group, then you specify how you want hello volume mounted within one or more of hello containers in hello group.</span></span>

<span data-ttu-id="216bd-125">Добавление тома hello toodefine требуется toomake доступны для монтажа, `volumes` массива toohello определение группы контейнера в шаблоне hello диспетчера ресурсов Azure, а затем ссылаться на них в определении hello hello отдельных контейнеров.</span><span class="sxs-lookup"><span data-stu-id="216bd-125">toodefine hello volumes you want toomake available for mounting, add a `volumes` array toohello container group definition in hello Azure Resource Manager template, then reference them in hello definition of hello individual containers.</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageaccountname": {
      "type": "string"
    },
    "storageaccountkey": {
      "type": "securestring"
    }
  },
  "resources":[{
    "name": "hellofiles",
    "type": "Microsoft.ContainerInstance/containerGroups",
    "apiVersion": "2017-08-01-preview",
    "location": "[resourceGroup().location]",
    "properties": {
      "containers": [{
        "name": "hellofiles",
        "properties": {
          "image": "seanmckenna/aci-hellofiles",
          "resources": {
            "requests": {
              "cpu": 1,
              "memoryInGb": 1.5
            }
          },
          "ports": [{
            "port": 80
          }],
          "volumeMounts": [{
            "name": "myvolume",
            "mountPath": "/aci/logs/"
          }]
        }  
      }],
      "osType": "Linux",
      "ipAddress": {
        "type": "Public",
        "ports": [{
          "protocol": "tcp",
          "port": "80"
        }]
      },
      "volumes": [{
        "name": "myvolume",
        "azureFile": {
          "shareName": "acishare",
          "storageAccountName": "[parameters('storageaccountname')]",
          "storageAccountKey": "[parameters('storageaccountkey')]"
        }
      }]
    }
  }]
}
```

<span data-ttu-id="216bd-126">Hello шаблон включает в себя имя учетной записи хранения hello и ключ как параметры, которые могут быть предоставлены в файле отдельных параметров.</span><span class="sxs-lookup"><span data-stu-id="216bd-126">hello template includes hello storage account name and key as parameters, which can be provided in a separate parameters file.</span></span> <span data-ttu-id="216bd-127">файл параметров toopopulate hello, вам потребуются три значения: hello имя учетной записи хранения, hello идентификатор ресурса хранилища ключей Azure и hello использования ключа хранилища hello toostore секретное имя хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="216bd-127">toopopulate hello parameters file, you will need three values: hello storage account name, hello resource ID of your Azure key vault, and hello key vault secret name that you used toostore hello storage key.</span></span> <span data-ttu-id="216bd-128">Если выполнены предыдущие шаги, эти значения можно получить с hello следующий скрипт:</span><span class="sxs-lookup"><span data-stu-id="216bd-128">If you have followed previous steps, you can get these values with hello following script:</span></span>

```azurecli-interactive
echo $STORAGE_ACCOUNT
echo $KEYVAULT_SECRET_NAME
az keyvault show --name $KEYVAULT_NAME --query [id] -o tsv
```

<span data-ttu-id="216bd-129">Вставьте значения hello в файле параметров hello:</span><span class="sxs-lookup"><span data-stu-id="216bd-129">Insert hello values into hello parameters file:</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageaccountname": {
      "value": "<my_storage_account_name>"
    },    
   "storageaccountkey": {
      "reference": {
        "keyVault": {
          "id": "<my_keyvault_id>"
        },
        "secretName": "<my_storage_account_key_secret_name>"
      }
    }
  }
}
```

## <a name="deploy-hello-container-and-manage-files"></a><span data-ttu-id="216bd-130">Развертывание контейнера hello и управление файлами</span><span class="sxs-lookup"><span data-stu-id="216bd-130">Deploy hello container and manage files</span></span>

<span data-ttu-id="216bd-131">С шаблоном hello определен можно создать контейнер hello и подключить его с помощью Azure CLI hello том.</span><span class="sxs-lookup"><span data-stu-id="216bd-131">With hello template defined, you can create hello container and mount its volume using hello Azure CLI.</span></span> <span data-ttu-id="216bd-132">Предположим, что hello файл шаблона называется *azuredeploy.json* , именем файла параметров hello *azuredeploy.parameters.json*, то командная строка hello:</span><span class="sxs-lookup"><span data-stu-id="216bd-132">Assuming that hello template file is named *azuredeploy.json* and that hello parameters file is named *azuredeploy.parameters.json*, then hello command line is:</span></span>

```azurecli-interactive
az group deployment create --name hellofilesdeployment --template-file azuredeploy.json --parameters @azuredeploy.parameters.json --resource-group myResourceGroup
```

<span data-ttu-id="216bd-133">После запуска контейнера hello, можно использовать hello простого веб-приложения, развернутые с помощью hello **seanmckenna, aci-hellofiles** изображения, toohello управления файлами в hello Azure общей папки на указанный путь подключения hello.</span><span class="sxs-lookup"><span data-stu-id="216bd-133">Once hello container starts up, you can use hello simple web app deployed via hello **seanmckenna/aci-hellofiles** image, toohello manage files in hello Azure file share at hello mount path that you specified.</span></span> <span data-ttu-id="216bd-134">Получите hello IP-адрес для веб-приложения hello через hello следующее:</span><span class="sxs-lookup"><span data-stu-id="216bd-134">Obtain hello ip address for hello web app via hello following:</span></span>

```azurecli-interactive
az container show --resource-group myResourceGroup --name hellofiles -o table
```

<span data-ttu-id="216bd-135">Можно использовать средства, подобного hello [Microsoft Azure Storage Explorer](http://storageexplorer.com) tooretrieve и проверить hello файл writen toohello общей папки.</span><span class="sxs-lookup"><span data-stu-id="216bd-135">You can use a tool like hello [Microsoft Azure Storage Explorer](http://storageexplorer.com) tooretrieve and inspect hello file writen toohello file share.</span></span>

>[!NOTE]
> <span data-ttu-id="216bd-136">toolearn Дополнительные сведения о с помощью шаблонов диспетчера ресурсов Azure, файлы параметров и развертывание с помощью hello Azure CLI см. в разделе [развертывания ресурсов с помощью шаблонов диспетчера ресурсов и Azure CLI](../azure-resource-manager/resource-group-template-deploy-cli.md).</span><span class="sxs-lookup"><span data-stu-id="216bd-136">toolearn more about using Azure Resource Manager templates, parameter files, and deploying with hello Azure CLI, see [Deploy resources with Resource Manager templates and Azure CLI](../azure-resource-manager/resource-group-template-deploy-cli.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="216bd-137">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="216bd-137">Next steps</span></span>

- <span data-ttu-id="216bd-138">Развертывание первого контейнера с помощью экземпляров контейнера Azure hello [быстрого запуска](container-instances-quickstart.md)</span><span class="sxs-lookup"><span data-stu-id="216bd-138">Deploy for your first container using hello Azure Container Instances [quick start](container-instances-quickstart.md)</span></span>
- <span data-ttu-id="216bd-139">Дополнительные сведения о hello [отношение между экземплярами контейнера Azure и контейнер orchestrators](container-instances-orchestrator-relationship.md)</span><span class="sxs-lookup"><span data-stu-id="216bd-139">Learn about hello [relationship between Azure Container Instances and container orchestrators](container-instances-orchestrator-relationship.md)</span></span>
