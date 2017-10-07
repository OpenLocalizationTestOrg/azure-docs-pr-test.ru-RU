---
title: "aaaInstall MongoDB на виртуальной Машине Linux с hello Azure CLI | Документы Microsoft"
description: "Узнайте, как tooinstall и настройте MongoDB на hello iusing виртуальной машине Linux Azure CLI 2.0"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 3f55b546-86df-4442-9ef4-8a25fae7b96e
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/23/2017
ms.author: iainfou
ms.openlocfilehash: 97a4d9913f0eeaf7b8bf15d7fc81befe538cdc8d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooinstall-and-configure-mongodb-on-a-linux-vm"></a>Как tooinstall и настройте MongoDB на виртуальной Машине Linux
[MongoDB](http://www.mongodb.org) — это популярная высокопроизводительная база данных NoSQL с открытым кодом. В этой статье показано, как tooinstall и настройте на виртуальной Машине Linux с hello Azure CLI 2.0 MongoDB. Можно также выполнить следующие действия с hello [Azure CLI 1.0](install-mongodb-nodejs.md). Изучив представленные примеры, вы узнаете, как:

* [установить и настроить базовый экземпляр MongoDB вручную](#manually-install-and-configure-mongodb-on-a-vm);
* [создать базовый экземпляр MongoDB на основе шаблона Resource Manager](#create-basic-mongodb-instance-on-centos-using-a-template);
* [создать сложный сегментированный кластер MongoDB с набором реплик с использованием шаблона Resource Manager](#create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template).


## <a name="manually-install-and-configure-mongodb-on-a-vm"></a>Установка и настройка MongoDB на виртуальной машине вручную
База данных MongoDB [содержит инструкции по установке](https://docs.mongodb.com/manual/administration/install-on-linux/) для дистрибутивов Linux, в том числе Red Hat, CentOS, SUSE, Ubuntu и Debian. Hello следующий пример создает *CentOS* виртуальной Машины. toocreate этой среды hello требуется последняя версия [Azure CLI 2.0](/cli/azure/install-az-cli2) установлен и войти в систему с учетной записью Azure tooan [входа az](/cli/azure/#login).

Создайте группу ресурсов с помощью команды [az group create](/cli/azure/group#create). Hello следующий пример создает группу ресурсов с именем *myResourceGroup* в hello *eastus* расположение:

```azurecli
az group create --name myResourceGroup --location eastus
```

Создайте виртуальную машину с помощью команды [az vm create](/cli/azure/vm#create). Hello следующий пример создает Виртуальную машину с именем *myVM* с именем пользователя *azureuser* с использованием открытого ключа проверки подлинности SSH

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image CentOS \
    --admin-username azureuser \
    --generate-ssh-keys
```

Toohello SSH виртуальную Машину с помощью имени пользователя и hello `publicIpAddress` перечисленные в выходных данных hello из предыдущего шага hello:

```bash
ssh azureuser@<publicIpAddress>
```

создать источник установки hello tooadd MongoDB, **yum** файл репозитория следующим образом:

```bash
sudo touch /etc/yum.repos.d/mongodb-org-3.4.repo
```

Откройте для редактирования файл репозитория hello MongoDB. Добавьте следующие строки hello:

```sh
[mongodb-org-3.4]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/3.4/x86_64/
gpgcheck=1
enabled=1
gpgkey=https://www.mongodb.org/static/pgp/server-3.4.asc
```

Установите MongoDB, используя **yum**, как показано ниже:

```bash
sudo yum install -y mongodb-org
```

По умолчанию в образах CentOS принудительно используется SELinux. Это препятствует доступу к MongoDB. Установка средств управления политиками и настройка SELinux tooallow MongoDB toooperate на порт TCP по умолчанию 27017 следующим образом:

```bash
sudo yum install -y policycoreutils-python
sudo semanage port -a -t mongod_port_t -p tcp 27017
```

Запуск службы MongoDB hello следующим образом:

```bash
sudo service mongod start
```

Проверка установки MongoDB hello при подключении с использованием локального hello `mongo` клиента:

```bash
mongo
```

Теперь можно проверьте экземпляр MongoDB hello, добавив некоторые данные и затем найти:

```sh
> db
test
> db.foo.insert( { a : 1 } )  
> db.foo.find()  
{ "_id" : ObjectId("57ec477cd639891710b90727"), "a" : 1 }
> exit
```

При необходимости настройте MongoDB toostart автоматически во время перезагрузки системы.

```bash
sudo chkconfig mongod on
```


## <a name="create-basic-mongodb-instance-on-centos-using-a-template"></a>Создание базового экземпляра MongoDB на виртуальной машине CentOS с использованием шаблона
Можно создать базовый экземпляр MongoDB на одной виртуальной Машины CentOS с помощью hello следующую Azure примеры использования шаблона из GitHub. Этот шаблон использует расширение hello пользовательский сценарий для Linux tooadd **yum** tooyour репозитория вновь созданные ВМ CentOS, а затем установите MongoDB.

* [Базовый экземпляр MongoDB на виртуальной машине CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-on-centos): https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json.

toocreate этой среды hello требуется последняя версия [Azure CLI 2.0](/cli/azure/install-az-cli2) установлен и войти в систему с учетной записью Azure tooan [входа az](/cli/azure/#login). Сначала создайте группу ресурсов с помощью команды [az group create](/cli/azure/group#create). Hello следующий пример создает группу ресурсов с именем *myResourceGroup* в hello *eastus* расположение:

```azurecli
az group create --name myResourceGroup --location eastus
```

Затем разверните шаблон hello MongoDB с [создания развертывания группы az](/cli/azure/group/deployment#create). Определите необходимые имена и размеры ресурсов, например *newStorageAccountName*, *virtualNetworkName* и *vmSize*:

```azurecli
az group deployment create --resource-group myResourceGroup \
  --parameters '{"newStorageAccountName": {"value": "mystorageaccount"},
    "adminUsername": {"value": "azureuser"},
    "adminPassword": {"value": "P@ssw0rd!"},
    "dnsNameForPublicIP": {"value": "mypublicdns"},
    "virtualNetworkName": {"value": "myVnet"},
    "vmSize": {"value": "Standard_DS2_v2"},
    "vmName": {"value": "myVM"},
    "publicIPAddressName": {"value": "myPublicIP"},
    "nicName": {"value": "myNic"}}' \
  --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json
```

Вход toohello виртуальной Машины с помощью hello общедоступный адрес DNS вашей виртуальной машины. Можно просмотреть hello общедоступный адрес DNS с [Показать ВМ az](/cli/azure/vm#show):

```azurecli
az vm show -g myResourceGroup -n myVM -d --query [fqdns] -o tsv
```

Tooyour SSH ВМ, используя имя пользователя и общедоступный адрес DNS:

```bash
ssh azureuser@mypublicdns.eastus.cloudapp.azure.com
```

Проверка установки MongoDB hello при подключении с использованием локального hello `mongo` клиента следующим образом:

```bash
mongo
```

Теперь тест hello экземпляр с помощью добавления данных и поиска следующим образом:

```sh
> db
test
> db.foo.insert( { a : 1 } )  
> db.foo.find()  
{ "_id" : ObjectId("57ec477cd639891710b90727"), "a" : 1 }
> exit
```


## <a name="create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template"></a>Создание сложного сегментированного кластера MongoDB на виртуальной машине CentOS с использованием шаблона
Можно создать сложные MongoDB сегментированных кластер, использующий hello следующую Azure примеры использования шаблона из GitHub. В этом шаблоне описываются hello [рекомендации сегментированных кластера MongoDB](https://docs.mongodb.com/manual/core/sharded-cluster-components/) tooprovide избыточность и высокий уровень доступности. шаблон Hello создает два сегментов с тремя узлами в каждом наборе реплик. Также создается одно конфигурации сервера реплику с тремя узлами, плюс два **mongos** маршрутизатора серверов tooprovide согласованности tooapplications из по сегментам hello.

* [Сегментированный кластер MongoDB на виртуальной машине CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-sharding-centos): https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json.

> [!WARNING]
> Развертывание этого сложного MongoDB сегментированных кластера требуется более чем 20 ядер, которой обычно является число ядер по умолчанию hello в одном регионе для подписки. Откройте запрос поддержки Azure tooincrease на число ядер.

toocreate этой среды hello требуется последняя версия [Azure CLI 2.0](/cli/azure/install-az-cli2) установлен и войти в систему с учетной записью Azure tooan [входа az](/cli/azure/#login). Сначала создайте группу ресурсов с помощью команды [az group create](/cli/azure/group#create). Hello следующий пример создает группу ресурсов с именем *myResourceGroup* в hello *eastus* расположение:

```azurecli
az group create --name myResourceGroup --location eastus
```

Затем разверните шаблон hello MongoDB с [создания развертывания группы az](/cli/azure/group/deployment#create). Определите необходимые имена и размеры ресурсов, например *mongoAdminUsername*, *sizeOfDataDiskInGB* и *configNodeVmSize*:

```azurecli
az group deployment create --resource-group myResourceGroup \
  --parameters '{"adminUsername": {"value": "azureuser"},
    "adminPassword": {"value": "P@ssw0rd!"},
    "mongoAdminUsername": {"value": "mongoadmin"},
    "mongoAdminPassword": {"value": "P@ssw0rd!"},
    "dnsNamePrefix": {"value": "mypublicdns"},
    "environment": {"value": "AzureCloud"},
    "numDataDisks": {"value": "4"},
    "sizeOfDataDiskInGB": {"value": 20},
    "centOsVersion": {"value": "7.0"},
    "routerNodeVmSize": {"value": "Standard_DS3_v2"},
    "configNodeVmSize": {"value": "Standard_DS3_v2"},
    "replicaNodeVmSize": {"value": "Standard_DS3_v2"},
    "zabbixServerIPAddress": {"value": "Null"}}' \
  --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json \
  --name myMongoDBCluster \
  --no-wait
```

Это развертывание может перехватить toodeploy час и настройте все экземпляры виртуальной Машины hello. Hello `--no-wait` флаг используется в конце hello hello предшествующий команда tooreturn управления toohello командной строки после развертывания шаблона hello после принятия hello платформы Azure. Затем можно просмотреть состояние развертывания hello с [Показать развертывания группы az](/cli/azure/group/deployment#show). Hello следующие представления пример hello состояние для hello *myMongoDBCluster* развертывания в hello *myResourceGroup* группа ресурсов:

```azurecli
az group deployment show \
    --resource-group myResourceGroup \
    --name myMongoDBCluster \
    --query [properties.provisioningState] \
    --output tsv
```

## <a name="next-steps"></a>Дальнейшие действия
В этих примерах подключения toohello MongoDB экземпляра локально из hello виртуальной Машины. Если экземпляр MongoDB toohello tooconnect из другой виртуальной Машины или сети, убедитесь, соответствующие hello [создаются правила группы безопасности сети](nsg-quickstart.md).

Эти примеры развертывания среды MongoDB core hello в целях разработки. Примените hello необходимые параметры конфигурации безопасности для вашей среды. Дополнительные сведения см. в разделе hello [docs безопасности MongoDB](https://docs.mongodb.com/manual/security/).

Дополнительные сведения о создании с помощью шаблонов см. в разделе hello [Обзор диспетчера ресурсов Azure](../../azure-resource-manager/resource-group-overview.md).

шаблоны Azure Resource Manager Hello использовать toodownload hello настраиваемое расширение скриптов и выполнения скриптов на ВМ. Дополнительные сведения см. в разделе [использование hello Azure настраиваемое расширение скриптов с виртуальных машин Linux](extensions-customscript.md).

