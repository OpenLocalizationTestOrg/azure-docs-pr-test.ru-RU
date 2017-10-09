---
title: "hello aaaUse расширения виртуальной Машины Azure Docker с hello Azure CLI 1.0 | Документы Microsoft"
description: "Узнайте, как toouse hello tooquickly расширение ВМ Docker и безопасного развертывания в среде Docker в Azure с помощью шаблонов диспетчера ресурсов."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 2133cdb1af741fe30093910fae5c3b2c91e8d5fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-docker-environment-in-azure-using-hello-docker-vm-extension-with-hello-azure-cli-10"></a>Создание среды Docker в Azure с помощью расширения виртуальной Машины Docker hello с hello Azure CLI 1.0
Docker — это популярный контейнер управления и работы с образами платформу, которая позволяет вам tooquickly работы с контейнерами Linux (а также Windows). В Azure существует несколько способов, которые можно развернуть в соответствии с потребностями tooyour Docker. В этой статье описывается использование расширение ВМ Docker hello и шаблоны Azure Resource Manager. 

Дополнительные сведения о hello различных способов развертывания, включая использование машины Docker и контейнер служб Azure см. следующие статьи hello:

* прототип tooquickly приложения, можно создать с помощью одного узла Docker [машины Docker](docker-machine.md).
* Для крупных и более стабильные средах, можно использовать расширения виртуальной Машины Azure Docker hello, которое также поддерживает [Docker Compose](https://docs.docker.com/compose/overview/) развертывания toogenerate согласованное контейнера. Этой статьи описаны с помощью расширения виртуальной Машины Azure Docker hello.
* toobuild рабочей среде, масштабируемых средах, предоставляющих дополнительные средства планирования и управления развертыванием [кластера с помощью Docker Swarm на контейнер служб Azure](../../container-service/dcos-swarm/container-service-deployment.md).

## <a name="cli-versions-toocomplete-hello-task"></a>Задача hello toocomplete версии CLI
Можно выполнить с помощью одного из следующих версий CLI hello задачу hello.

- [Azure CLI 1.0](#azure-docker-vm-extension-overview) — нашей CLI для hello классический и ресурса управления развертывания моделей (в этой статье)
- [Azure CLI 2.0](dockerextension.md) -нашей нового поколения CLI для модели развертывания hello ресурсов управления 

## <a name="azure-docker-vm-extension-overview"></a>Общие сведения о расширении виртуальных машин Docker для Azure
Hello расширение ВМ Docker Azure устанавливает и настраивает управляющую программу Docker hello, клиент Docker и Docker Compose в Linux виртуальной машины (VM). С помощью расширения виртуальной Машины Azure Docker hello, имеют больший контроль и возможностей, чем просто с помощью машины Docker или создании узла Docker hello самостоятельно. Эти дополнительные возможности, например [Docker Compose](https://docs.docker.com/compose/overview/), подготовить расширение виртуальной Машины Azure Docker hello подходит для более надежной разработчика или рабочей среде.

Шаблоны Azure Resource Manager определить структуру в целом hello среды. Шаблоны позволяют toocreate и настроить ресурсы, такие как узел Docker hello виртуальных машин, хранилища, средства управления доступом на основе ролей (RBAC) и диагностики. Можно повторно использовать эти шаблоны toocreate дополнительные развертывания согласованным образом. Дополнительные сведения об Azure Resource Manager и шаблонах см. в статье [Общие сведения об Azure Resource Manager ](../../azure-resource-manager/resource-group-overview.md). 

## <a name="deploy-a-template-with-hello-azure-docker-vm-extension"></a>Развертывание шаблона с hello расширения виртуальной Машины Azure Docker
Позволяет использовать существующий шаблон краткого руководства toocreate Виртуальной машине Ubuntu, использующий tooinstall расширения виртуальной Машины Azure Docker hello и настройка узла Docker hello. Можно просмотреть здесь шаблон hello: [простое развертывание Виртуальной машине Ubuntu с помощью Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu). 

Требуется hello [последние Azure CLI](../../cli-install-nodejs.md) установлен и вход с помощью режима диспетчера ресурсов hello следующим образом:

```azurecli
azure config mode arm
```

Развертывание шаблона hello, с помощью hello Azure CLI, указав hello шаблон URI. Hello следующий пример создает группу ресурсов с именем *myResourceGroup* в hello *westus* расположение. Укажите собственное имя группы ресурсов и расположение, как показано ниже.

```azurecli
azure group create \
    --name myResourceGroup \
    --location westus \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/docker-simple-on-ubuntu/azuredeploy.json
```

Ответить на запрос tooname hello вашей учетной записи хранилища, укажите имя пользователя и пароль и укажите DNS-имя. Hello вывода будет примерно toohello следующий пример:

```azurecli
info:    Executing command group create
+ Getting resource group myResourceGroup
+ Updating resource group myResourceGroup
info:    Updated resource group myResourceGroup
info:    Supply values for hello following parameters
newStorageAccountName: mystorageaccount
adminUsername: azureuser
adminPassword: P@ssword!
dnsNameForPublicIP: mypublicidns
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "azuredeploy"
data:    Id:                  /subscriptions/guid/resourceGroups/myResourceGroup
data:    Name:                myResourceGroup
data:    Location:            westus
data:    Provisioning State:  Succeeded
data:    Tags: null
data:
info:    group create command OK
```

Hello Azure CLI возвращает строки toohello только через несколько секунд, но узла Docker находится в процессе создания и настроить hello расширение ВМ Docker в Azure. Он занимает несколько минут для развертывания toofinish hello. Для просмотра сведений о состоянии узла Docker hello, с помощью hello `azure vm show` команды.

Hello следующий пример проверяет состояние виртуальной Машины с именем hello hello *myDockerVM* (имя по умолчанию на основе шаблона hello hello — не изменять это имя) в группе ресурсов hello с именем *myResourceGroup*. Введите имя группы ресурсов hello, созданный на предыдущих шага hello hello:

```azurecli
azure vm show --resource-group myResourceGroup --name myDockerVM
```

Здравствуйте, выходные данные hello `azure vm show` команды будет примерно toohello следующий пример:

```azurecli
info:    Executing command vm show
+ Looking up hello VM "myDockerVM"
+ Looking up hello NIC "myVMNicD"
+ Looking up hello public ip "myPublicIPD"
data:    Id                              :/subscriptions/guid/resourceGroups/myresourcegroup/providers/Microsoft.Compute/virtualMachines/MyDockerVM
data:    ProvisioningState               :Succeeded
data:    Name                            :MyDockerVM
data:    Location                        :westus
data:    Type                            :Microsoft.Compute/virtualMachines
[...]
data:
data:    Network Profile:
data:      Network Interfaces:
data:        Network Interface #1:
data:          Primary                   :true
data:          MAC Address               :00-0D-3A-33-D3-95
data:          Provisioning State        :Succeeded
data:          Name                      :myVMNicD
data:          Location                  :westus
data:            Public IP address       :13.91.107.235
data:            FQDN                    :mypublicdns.westus.cloudapp.azure.com
data:
data:    Diagnostics Instance View:
info:    vm show command OK
```

Верхней hello hello выходных данных вы видите hello **ProvisioningState** из hello виртуальной Машины. При этом выводится *успешно*, завершения развертывания hello и вы можете toohello SSH виртуальной Машины.

Концу hello вывода hello *полное доменное имя* отображает hello полное доменное имя узла Docker. Это полное доменное имя является то, что используется узел Docker tooyour tooSSH в hello, оставшиеся шаги.

## <a name="deploy-your-first-nginx-container"></a>Развертывание первого контейнера nginx
После завершения развертывания hello SSH tooyour новый узел Docker с локального компьютера. Введите собственное имя пользователя и полное доменное имя, как показано ниже.

```bash
ssh ops@mypublicdns.westus.cloudapp.azure.com
```

После входа в toohello узел Docker, запустим контейнер nginx:

```bash
sudo docker run -d -p 80:80 nginx
```

выходные данные Hello выглядят примерно toohello следующий пример, как загружается образ nginx hello и контейнер к работе:

```bash
Unable toofind image 'nginx:latest' locally
latest: Pulling from library/nginx
efd26ecc9548: Pull complete
a3ed95caeb02: Pull complete
a48df1751a97: Pull complete
8ddc2d7beb91: Pull complete
Digest: sha256:2ca2638e55319b7bc0c7d028209ea69b1368e95b01383e66dfe7e4f43780926d
Status: Downloaded newer image for nginx:latest
b6ed109fb743a762ff21a4606dd38d3e5d35aff43fa7f12e8d4ed1d920b0cd74
```

Проверьте состояние hello hello контейнеров, работающих на узле Docker следующим образом:

```bash
sudo docker ps
```

выходные данные Hello аналогичные toohello следующий пример, отображение этого контейнера nginx hello запущена и TCP-порты 80 и 443 и пересылки:

```bash
CONTAINER ID        IMAGE               COMMAND                  CREATED              STATUS              PORTS                         NAMES
b6ed109fb743        nginx               "nginx -g 'daemon off"   About a minute ago   Up About a minute   0.0.0.0:80->80/tcp, 443/tcp   adoring_payne
```

toosee контейнера в действие, откройте веб-обозреватель и введите полное ДОМЕННОЕ имя узла Docker hello:

![Запущенный контейнер nginx](./media/dockerextension/nginxrunning.png)

## <a name="azure-docker-vm-extension-template-reference"></a>Пример шаблона расширения виртуальной машины Docker для Azure
Hello в предыдущем примере существующий шаблон краткого руководства. Можно также развернуть hello расширения виртуальной Машины Azure Docker с помощью собственных шаблонов диспетчера ресурсов. toodo таким образом, добавить hello следующие шаблоны диспетчера ресурсов tooyour, определение hello *vmName* вашей виртуальной машины соответствующим образом:

```json
{
  "type": "Microsoft.Compute/virtualMachines/extensions",
  "name": "[concat(variables('vmName'), '/DockerExtension'))]",
  "apiVersion": "2015-05-01-preview",
  "location": "[parameters('location')]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
  ],
  "properties": {
    "publisher": "Microsoft.Azure.Extensions",
    "type": "DockerExtension",
    "typeHandlerVersion": "1.1",
    "autoUpgradeMinorVersion": true,
    "settings": {},
    "protectedSettings": {}
  }
}
```

Подробное пошаговое руководство по использованию шаблонов Resource Manager см. в статье [Общие сведения об Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).

## <a name="next-steps"></a>Дальнейшие действия
Вы можете слишком[настроить hello Docker daemon TCP-порт](https://docs.docker.com/engine/reference/commandline/dockerd/#/bind-docker-to-another-hostport-or-a-unix-socket), понять [безопасности Docker](https://docs.docker.com/engine/security/security/), или развернуть контейнеры с помощью [Docker Compose](https://docs.docker.com/compose/overview/). Дополнительные сведения о hello расширение ВМ Docker Azure сама разделе hello [GitHub проекта](https://github.com/Azure/azure-docker-extension/).

Прочтите Дополнительные сведения о дополнительных параметрах развертывания Docker hello в Azure:

* [Использовать компьютер Docker с hello Azure драйвера](docker-machine.md)  
* [Начало работы с Docker и составлять toodefine и запустите приложение контейнера несколькими на виртуальной машине Azure](docker-compose-quickstart.md).
* [Развертывание кластера службы контейнеров Azure](../../container-service/dcos-swarm/container-service-deployment.md)

