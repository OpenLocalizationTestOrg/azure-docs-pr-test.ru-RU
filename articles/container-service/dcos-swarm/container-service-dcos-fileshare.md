---
title: "aaaFile общего ресурса для кластера DC/ОС Azure | Документы Microsoft"
description: "Создать и подключить tooa DC/OS файл общего ресурса кластера в службе контейнера Azure"
services: container-service
documentationcenter: 
author: julienstroheker
manager: dcaro
editor: 
tags: acs, azure-container-service
keywords: "Docker, контейнеры, микрослужбы, Mesos, Azure, FileShare, cifs"
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/07/2017
ms.author: juliens
ms.custom: mvc
ms.openlocfilehash: d18090d414a3e00202ccde442ac9b865d74f1e34
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-mount-a-file-share-tooa-dcos-cluster"></a>Создать и подключить tooa DC/OS файл общего ресурса кластера
Подробное описание этого учебника, как toocreate файл общего доступа в Azure и подключить его для каждого агента и образец hello DC/OS кластера. Настройка общей папки позволяет проще tooshare файлы в кластере, например конфигурации, доступ, журналы и многое другое. в этом учебнике выполняются Hello следующие задачи:

> [!div class="checklist"]
> * Создание учетной записи хранения Azure
> * Создайте общую папку
> * Подключить hello общего ресурса в кластере DC/OS hello

Вы должны ACS DC/OS hello toocomplete кластера шаги в этом учебнике. При необходимости его можно создать с помощью следующего [примера сценария](./../kubernetes/scripts/container-service-cli-deploy-dcos.md).

Упражнений этого учебника требуется hello Azure CLI версия 2.0.4 или более поздней версии. Запустите `az --version` версии toofind hello. Получить tooupgrade [установить CLI Azure 2.0]( /cli/azure/install-azure-cli). 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="create-a-file-share-on-microsoft-azure"></a>Создание файлового ресурса в Microsoft Azure

Перед использованием Azure файловый ресурс кластера с ACS DC/OS, hello хранилища учетной записи и общей папки должен быть создан. Запустите следующий скрипт toocreate hello хранилища и общей папки hello. Обновление параметров hello с данными из вашей среды.

```azurecli-interactive
# Change these four parameters
DCOS_PERS_STORAGE_ACCOUNT_NAME=mystorageaccount$RANDOM
DCOS_PERS_RESOURCE_GROUP=myResourceGroup
DCOS_PERS_LOCATION=eastus
DCOS_PERS_SHARE_NAME=dcosshare

# Create hello storage account with hello parameters
az storage account create -n $DCOS_PERS_STORAGE_ACCOUNT_NAME -g $DCOS_PERS_RESOURCE_GROUP -l $DCOS_PERS_LOCATION --sku Standard_LRS

# Export hello connection string as an environment variable, this is used when creating hello Azure file share
export AZURE_STORAGE_CONNECTION_STRING=`az storage account show-connection-string -n $DCOS_PERS_STORAGE_ACCOUNT_NAME -g $DCOS_PERS_RESOURCE_GROUP -o tsv`

# Create hello share
az storage share create -n $DCOS_PERS_SHARE_NAME
```

## <a name="mount-hello-share-in-your-cluster"></a>Подключить hello общего ресурса в кластере

Далее hello общего файла требуется toobe на каждой виртуальной машине внутри кластера. Эта задача выполняется с помощью средства cifs hello и протокола. на каждом узле кластера hello, или путем выполнения сценария для каждого узла в кластере hello Hello операции подключения можно выполнить вручную.

В этом примере выполняются два сценария, один toomount hello Azure файлов общей папки, а второй toorun этот скрипт на каждом узле кластера DC/OS hello.

Во-первых необходимы имя учетной записи хранилища Azure hello и ключ доступа. Выполните следующие команды tooget hello эти сведения. Запомните или запишите эти значения — они будут использоваться в последующих шагах.

Имя учетной записи хранения:

```azurecli-interactive
STORAGE_ACCT=$(az storage account list --resource-group myResourceGroup --query "[?contains(name,'mystorageaccount')].[name]" -o tsv)
echo $STORAGE_ACCT
```

Ключ доступа к учетной записи хранения:

```azurecli-interactive
az storage account keys list --resource-group myResourceGroup --account-name $STORAGE_ACCT --query "[0].value" -o tsv
```

Затем следует получите hello полное доменное имя hello DC/OS-шаблоны и сохранить его в переменной.

```azurecli-interactive
FQDN=$(az acs list --resource-group myResourceGroup --query "[0].masterProfile.fqdn" --output tsv)
```

Скопируйте на главном узле toohello закрытого ключа. Этот ключ является необходимые toocreate ssh соединения с узлами в кластере hello. Обновите имя пользователя hello, если значение не по умолчанию использовался при создании кластера hello. 

```azurecli-interactive
scp ~/.ssh/id_rsa azureuser@$FQDN:~/.ssh
```

Создайте SSH-подключения с hello master (или первый образец hello) кластера на базе контроллера домена/ОС. Обновите имя пользователя hello, если значение не по умолчанию использовался при создании кластера hello.

```azurecli-interactive
ssh azureuser@$FQDN
```

Создайте файл с именем **cifsMount.sh**, и hello копировать содержимое в него. 

Этот скрипт является используется toomount hello Azure общей папки. Обновление hello `STORAGE_ACCT_NAME` и `ACCESS_KEY` переменных с hello сведения, собранные ранее.

```azurecli-interactive
#!/bin/bash

# Azure storage account name and access key
STORAGE_ACCT_NAME=mystorageaccount
ACCESS_KEY=mystorageaccountKey

# Install hello cifs utils, should be already installed
sudo apt-get update && sudo apt-get -y install cifs-utils

# Create hello local folder that will contain our share
if [ ! -d "/mnt/share/dcosshare" ]; then sudo mkdir -p "/mnt/share/dcosshare" ; fi

# Mount hello share under hello previous local folder created
sudo mount -t cifs //$STORAGE_ACCT_NAME.file.core.windows.net/dcosshare /mnt/share/dcosshare -o vers=3.0,username=$STORAGE_ACCT_NAME,password=$ACCESS_KEY,dir_mode=0777,file_mode=0777
```
Создайте второй файл с именем **getNodesRunScript.sh** и hello копировать содержимое в файл hello. 

Этот сценарий обнаруживает все узлы кластера, а затем запускает hello **cifsMount.sh** сценарий toomount hello общую папку на каждом.

```azurecli-interactive
#!/bin/bash

# Install jq used for hello next command
sudo apt-get install jq -y

# Get hello IP address of each node using hello mesos API and store it inside a file called nodes
curl http://leader.mesos:1050/system/health/v1/nodes | jq '.nodes[].host_ip' | sed 's/\"//g' | sed '/172/d' > nodes

# From hello previous file created, run our script toomount our share on each node
cat nodes | while read line
do
  ssh `whoami`@$line -o StrictHostKeyChecking=no < ./cifsMount.sh
  done
```

Hello выполнения сценария toomount hello Azure общей папки на всех узлах кластера hello.

```azurecli-interactive
sh ./getNodesRunScript.sh
```  

Hello общей папки теперь доступны в `/mnt/share/dcosshare` на каждом узле кластера hello.

## <a name="next-steps"></a>Дальнейшие действия

В этом учебнике Azure общей папки был сделан доступных tooa DC/OS кластер, использующий hello действия:

> [!div class="checklist"]
> * Создание учетной записи хранения Azure
> * Создайте общую папку
> * Подключить hello общего ресурса в кластере DC/OS hello

Переместить toohello Далее учебника toolearn об интеграции Azure контейнер реестра с контроллера домена или ОС в Azure.  

> [!div class="nextstepaction"]
> [Приложения балансировки нагрузки](container-service-dcos-acr.md)