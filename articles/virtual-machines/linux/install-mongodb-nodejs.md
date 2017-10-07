---
title: "Здравствуйте, aaaInstall MongoDB на виртуальной Машине Linux с помощью Azure CLI 1.0 | Документы Microsoft"
description: "Узнайте, как tooinstall и настройте на виртуальной машине Linux в Azure с помощью модели развертывания диспетчера ресурсов hello MongoDB."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 3f55b546-86df-4442-9ef4-8a25fae7b96e
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 4ce21a2c63da7d00a4422e0a6766e2103e7f12d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooinstall-and-configure-mongodb-on-a-linux-vm-using-hello-azure-cli-10"></a>Как tooinstall и настройте MongoDB на ВМ Linux с помощью hello Azure CLI 1.0
[MongoDB](http://www.mongodb.org) — это популярная высокопроизводительная база данных NoSQL с открытым кодом. В этой статье показано, как tooinstall и настройте на виртуальной Машине Linux в Azure с помощью модели развертывания диспетчера ресурсов hello MongoDB. Изучив представленные примеры, вы узнаете, как:

* [установить и настроить базовый экземпляр MongoDB вручную](#manually-install-and-configure-mongodb-on-a-vm);
* [создать базовый экземпляр MongoDB на основе шаблона Resource Manager](#create-basic-mongodb-instance-on-centos-using-a-template);
* [создать сложный сегментированный кластер MongoDB с набором реплик с использованием шаблона Resource Manager](#create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template).


## <a name="cli-versions-toocomplete-hello-task"></a>Задача hello toocomplete версии CLI
Можно выполнить с помощью одного из следующих версий CLI hello задачу hello.

- Azure CLI 1.0 — нашей CLI для hello классический и ресурса управления развертывания моделей (в этой статье)
- [Azure CLI 2.0](create-cli-complete-nodejs.md) -нашей нового поколения CLI для модели развертывания hello ресурсов управления


## <a name="manually-install-and-configure-mongodb-on-a-vm"></a>Установка и настройка MongoDB на виртуальной машине вручную
База данных MongoDB [содержит инструкции по установке](https://docs.mongodb.com/manual/administration/install-on-linux/) для дистрибутивов Linux, в том числе Red Hat, CentOS, SUSE, Ubuntu и Debian. Hello следующий пример создает *CentOS* виртуальную Машину с помощью ключа SSH, хранящиеся в *~/.ssh/id_rsa.pub*. Hello ответов запрашивает имя учетной записи хранения, DNS-имя и учетные данные администратора:

```azurecli
azure vm quick-create \
    --image-urn CentOS \
    --ssh-publickey-file ~/.ssh/id_rsa.pub 
```

Войдите на toohello виртуальной Машины с помощью hello общедоступный IP-адрес отображается в конце hello hello предшествующий этап создания виртуальной Машины:

```bash
ssh azureuser@40.78.23.145
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

По умолчанию в образах CentOS принудительно используется SELinux. Это препятствует доступу к MongoDB. Установка средств управления политиками и настройка SELinux tooallow MongoDB toooperate на порт TCP по умолчанию 27017 следующим образом. 

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
Можно создать базовый экземпляр MongoDB на одной виртуальной Машины CentOS с помощью hello следующую Azure примеры использования шаблона из GitHub. Этот шаблон использует расширение hello пользовательский сценарий для Linux tooadd `yum` tooyour репозитория вновь созданные ВМ CentOS, а затем установите MongoDB.

* [Базовый экземпляр MongoDB на виртуальной машине CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-on-centos): https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json.

Hello следующий пример создает группу ресурсов с именем hello `myResourceGroup` в hello `eastus` области. Введите свои значения следующим образом:

```azurecli
azure group create \
    --name myResourceGroup \
    --location eastus \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json
```

> [!NOTE]
> Hello Azure CLI возвращает строки tooa через несколько секунд создания hello развертывания, но попытка установки hello и конфигурация принимает toocomplete несколько минут. Проверьте состояние развертывания hello с hello `azure group deployment show myResourceGroup`, введя hello имя группы ресурсов соответствующим образом. Подождите, пока hello **ProvisioningState** показывает *успешно* перед идет tooSSH toohello виртуальной Машины.

После развертывания hello завершить, toohello SSH виртуальной Машины. Получить IP-адрес виртуальной Машины с помощью hello hello `azure vm show` команду как hello в следующем примере:

```azurecli
azure vm show --resource-group myResourceGroup --name myLinuxVM
```

Конец hello hello выходные данные отображается hello общедоступный IP-адрес. Tooyour SSH виртуальной Машины с IP-адресом hello вашей виртуальной машины:

```bash
ssh azureuser@138.91.149.74
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

Hello следующий пример создает группу ресурсов с именем hello *myResourceGroup* в hello *eastus* области. Введите свои значения следующим образом:

```azurecli
azure group create \
    --name myResourceGroup \
    --location eastus \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json
```

> [!NOTE]
> Hello Azure CLI возвращает строки tooa через несколько секунд создания hello развертывания, но hello установки и настройки может взять на себя toocomplete час. Проверьте состояние развертывания hello с hello `azure group deployment show myResourceGroup`, соответственно изменив hello имя группы ресурсов. Подождите, пока hello **ProvisioningState** показывает *успешно* перед подключением toohello виртуальных машин.


## <a name="next-steps"></a>Дальнейшие действия
В этих примерах подключения toohello MongoDB экземпляра локально из hello виртуальной Машины. Если экземпляр MongoDB toohello tooconnect из другой виртуальной Машины или сети, убедитесь, соответствующие hello [создаются правила группы безопасности сети](nsg-quickstart.md).

Дополнительные сведения о создании с помощью шаблонов см. в разделе hello [Обзор диспетчера ресурсов Azure](../../azure-resource-manager/resource-group-overview.md).

шаблоны Azure Resource Manager Hello использовать toodownload hello настраиваемое расширение скриптов и выполнения скриптов на ВМ. Дополнительные сведения см. в разделе [использование hello Azure настраиваемое расширение скриптов с виртуальных машин Linux](extensions-customscript.md).

