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
# <a name="mounting-an-azure-file-share-with-azure-container-instances"></a>Подключение файлового ресурса Azure с помощью Экземпляров контейнеров Azure

По умолчанию в Экземплярах контейнеров Azure не отслеживается состояние. Если контейнер hello аварийно завершает работу или останавливается, свое состояние будет потеряно. toopersist состояния вне пределов продолжительности hello hello контейнера, необходимо подключить том из внешнего хранилища. В этой статье показано, как toomount Azure общей папки для использования с экземплярами Azure контейнера.

## <a name="create-an-azure-file-share"></a>Создание файлового ресурса Azure

Перед использованием файлового ресурса Azure с Экземплярами контейнеров Azure необходимо создать его. Запустите следующий сценарий toocreate общей папки хранилища учетной записи toohost hello и hello общей папки самого hello. Обратите внимание, что имя учетной записи хранения, hello должно быть глобально уникальным, поэтому скрипт hello добавляет строку базовый toohello случайное значение.

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

## <a name="acquire-storage-account-access-details"></a>Получение данных для доступа к учетной записи хранения

toomount файл Azure совместное использование в качестве тома в Azure экземпляров контейнера, требуются три значения: hello имя учетной записи хранения, имя общего ресурса hello и ключ доступа к хранилищу hello. 

Если вы использовали hello сценарий, приведенный выше, имя учетной записи хранения hello был создан случайным значением в конце hello. Окончательная строка hello tooquery (включая hello случайных часть), используйте hello, следующие команды:

```azurecli-interactive
STORAGE_ACCOUNT=$(az storage account list --resource-group myResourceGroup --query "[?contains(name,'mystorageaccount')].[name]" -o tsv)
echo $STORAGE_ACCOUNT
```

Hello имя общего ресурса уже известна (это *acishare* в скрипте hello выше), поэтому все, остается только hello ключ учетной записи хранения, которую можно найти с помощью hello следующую команду:

```azurecli-interactive
$STORAGE_KEY=$(az storage account keys list --resource-group myResourceGroup --account-name $STORAGE_ACCOUNT --query "[0].value" -o tsv)
echo $STORAGE_KEY
```

## <a name="store-storage-account-access-details-with-azure-key-vault"></a>Сохранение сведений о доступе к учетной записи хранения с помощью хранилища ключей Azure

Ключи учетной записи хранения защиты доступа к данным tooyour, поэтому рекомендуется хранить их в хранилище ключей Azure. 

Создание хранилища ключей с hello Azure CLI:

```azurecli-interactive
KEYVAULT_NAME=aci-keyvault
az keyvault create -n $KEYVAULT_NAME --enabled-for-template-deployment -g myResourceGroup
```

Hello `enabled-for-template-deployment` переключатель Azure Resource Manager toopull секретов из хранилища ключей во время развертывания.

Хранить ключ учетной записи хранения hello как новый секрет в хранилище ключей hello:

```azurecli-interactive
KEYVAULT_SECRET_NAME=azurefilesstoragekey
az keyvault secret set --vault-name $KEYVAULT_NAME --name $KEYVAULT_SECRET_NAME --value $STORAGE_KEY
```

## <a name="mount-hello-volume"></a>Подключить том hello

Подключение файлового ресурса Azure как тома в контейнере состоит из двух этапов. Во-первых вы подробно hello hello общей папки, как часть определения группы контейнеров hello, а затем укажите способ hello тома подключены в один или несколько контейнеров hello в группе hello.

Добавление тома hello toodefine требуется toomake доступны для монтажа, `volumes` массива toohello определение группы контейнера в шаблоне hello диспетчера ресурсов Azure, а затем ссылаться на них в определении hello hello отдельных контейнеров.

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

Hello шаблон включает в себя имя учетной записи хранения hello и ключ как параметры, которые могут быть предоставлены в файле отдельных параметров. файл параметров toopopulate hello, вам потребуются три значения: hello имя учетной записи хранения, hello идентификатор ресурса хранилища ключей Azure и hello использования ключа хранилища hello toostore секретное имя хранилища ключей. Если выполнены предыдущие шаги, эти значения можно получить с hello следующий скрипт:

```azurecli-interactive
echo $STORAGE_ACCOUNT
echo $KEYVAULT_SECRET_NAME
az keyvault show --name $KEYVAULT_NAME --query [id] -o tsv
```

Вставьте значения hello в файле параметров hello:

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

## <a name="deploy-hello-container-and-manage-files"></a>Развертывание контейнера hello и управление файлами

С шаблоном hello определен можно создать контейнер hello и подключить его с помощью Azure CLI hello том. Предположим, что hello файл шаблона называется *azuredeploy.json* , именем файла параметров hello *azuredeploy.parameters.json*, то командная строка hello:

```azurecli-interactive
az group deployment create --name hellofilesdeployment --template-file azuredeploy.json --parameters @azuredeploy.parameters.json --resource-group myResourceGroup
```

После запуска контейнера hello, можно использовать hello простого веб-приложения, развернутые с помощью hello **seanmckenna, aci-hellofiles** изображения, toohello управления файлами в hello Azure общей папки на указанный путь подключения hello. Получите hello IP-адрес для веб-приложения hello через hello следующее:

```azurecli-interactive
az container show --resource-group myResourceGroup --name hellofiles -o table
```

Можно использовать средства, подобного hello [Microsoft Azure Storage Explorer](http://storageexplorer.com) tooretrieve и проверить hello файл writen toohello общей папки.

>[!NOTE]
> toolearn Дополнительные сведения о с помощью шаблонов диспетчера ресурсов Azure, файлы параметров и развертывание с помощью hello Azure CLI см. в разделе [развертывания ресурсов с помощью шаблонов диспетчера ресурсов и Azure CLI](../azure-resource-manager/resource-group-template-deploy-cli.md).

## <a name="next-steps"></a>Дальнейшие действия

- Развертывание первого контейнера с помощью экземпляров контейнера Azure hello [быстрого запуска](container-instances-quickstart.md)
- Дополнительные сведения о hello [отношение между экземплярами контейнера Azure и контейнер orchestrators](container-instances-orchestrator-relationship.md)
