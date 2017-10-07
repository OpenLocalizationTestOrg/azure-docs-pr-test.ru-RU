---
title: "hello aaaUse расширения виртуальной Машины Azure Docker | Документы Microsoft"
description: "Узнайте, как toouse hello tooquickly расширение ВМ Docker и безопасное развертывание среды Docker в Azure с помощью шаблонов диспетчера ресурсов и hello Azure CLI 2.0"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 936d67d7-6921-4275-bf11-1e0115e66b7f
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 8e43adc594192773466ccd2d3e455105f14c1a61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-docker-environment-in-azure-using-hello-docker-vm-extension"></a>Создание среды Docker в Azure с помощью расширения виртуальной Машины Docker hello
Docker — это популярный контейнер управления и работы с образами платформу, которая позволяет tooquickly работы с контейнерами в Linux. В Azure существует несколько способов, которые можно развернуть в соответствии с потребностями tooyour Docker. В этой статье описывается использование расширение ВМ Docker hello и шаблоны Azure Resource Manager с hello Azure CLI 2.0. Можно также выполнить следующие действия с hello [Azure CLI 1.0](dockerextension-nodejs.md).

## <a name="azure-docker-vm-extension-overview"></a>Общие сведения о расширении виртуальных машин Docker для Azure
Hello расширение ВМ Docker Azure устанавливает и настраивает управляющую программу Docker hello, клиент Docker и Docker Compose в Linux виртуальной машины (VM). С помощью расширения виртуальной Машины Azure Docker hello, имеют больший контроль и возможностей, чем просто с помощью машины Docker или создании узла Docker hello самостоятельно. Эти дополнительные возможности, например [Docker Compose](https://docs.docker.com/compose/overview/), подготовить расширение виртуальной Машины Azure Docker hello подходит для более надежной разработчика или рабочей среде.

Дополнительные сведения о hello различных способов развертывания, включая использование машины Docker и контейнер служб Azure см. следующие статьи hello:

* прототип tooquickly приложения, можно создать с помощью одного узла Docker [машины Docker](docker-machine.md).
* toobuild рабочей среде, масштабируемых средах, предоставляющих дополнительные средства планирования и управления развертыванием [кластера с помощью Docker Swarm на контейнер служб Azure](../../container-service/dcos-swarm/container-service-deployment.md).

## <a name="deploy-a-template-with-hello-azure-docker-vm-extension"></a>Развертывание шаблона с hello расширения виртуальной Машины Azure Docker
Позволяет использовать существующий шаблон краткого руководства toocreate Виртуальной машине Ubuntu, использующий tooinstall расширения виртуальной Машины Azure Docker hello и настройка узла Docker hello. Можно просмотреть здесь шаблон hello: [простое развертывание Виртуальной машине Ubuntu с помощью Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu). Hello требуется последняя версия [Azure CLI 2.0](/cli/azure/install-az-cli2) установлен и войти в систему с учетной записью Azure tooan [входа az](/cli/azure/#login).

Сначала создайте группу ресурсов с помощью команды [az group create](/cli/azure/group#create). Hello следующий пример создает группу ресурсов с именем *myResourceGroup* в hello *westus* расположение:

```azurecli
az group create --name myResourceGroup --location westus
```

Затем разверните виртуальную Машину с [создания развертывания группы az](/cli/azure/group/deployment#create) , включает в себя расширение виртуальной Машины Azure Docker hello из [этого шаблона диспетчера ресурсов Azure на GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu). Укажите собственные значения для параметров *newStorageAccountName*, *adminUsername*, *adminPassword* и *dnsNameForPublicIP*, как показано ниже:

```azurecli
az group deployment create --resource-group myResourceGroup \
  --parameters '{"newStorageAccountName": {"value": "mystorageaccount"},
    "adminUsername": {"value": "azureuser"},
    "adminPassword": {"value": "P@ssw0rd!"},
    "dnsNameForPublicIP": {"value": "mypublicdns"}}' \
  --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/docker-simple-on-ubuntu/azuredeploy.json
```

Он занимает несколько минут для развертывания toofinish hello. После завершения развертывания hello [переместить шаг toonext](#deploy-your-first-nginx-container) tooSSH tooyour виртуальной Машины. 

При необходимости строки toohello tooinstead возвращаемого элемента управления и позволяют hello развертывания по-прежнему в фоновом режиме hello, добавьте hello `--no-wait` флаг toohello предшествующий команды. Этот процесс позволяет tooperform другие действия в hello CLI во время развертывания hello продолжается несколько минут. 

Затем можно просмотреть подробные сведения о состоянии узла Docker hello с [Показать ВМ az](/cli/azure/vm#show). Hello следующий пример проверяет состояние виртуальной Машины с именем hello hello *myDockerVM* (имя по умолчанию на основе шаблона hello hello — не изменять это имя) в группе ресурсов hello с именем *myResourceGroup*:

```azurecli
az vm show \
    --resource-group myResourceGroup \
    --name myDockerVM \
    --query [provisioningState] \
    --output tsv
```

Если эта команда возвращает *успешно*, завершения развертывания hello и вы можете toohello SSH виртуальной Машины в даст hello.

## <a name="deploy-your-first-nginx-container"></a>Развертывание первого контейнера nginx
использовать сведения о tooview виртуальной машины, включая hello DNS-имя `az vm show -g myResourceGroup -n myDockerVM -d --query [fqdns] -o tsv`. SSH tooyour новый Docker размещения с локального компьютера следующим образом:

```bash
ssh azureuser@mypublicdns.westus.cloudapp.azure.com
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

toosee контейнера в действие, откройте веб-обозреватель и введите hello DNS-имя узла Docker:

![Запущенный контейнер nginx](./media/dockerextension/nginxrunning.png)

## <a name="azure-docker-vm-extension-template-reference"></a>Пример шаблона расширения виртуальной машины Docker для Azure
Hello в предыдущем примере существующий шаблон краткого руководства. Можно также развернуть hello расширения виртуальной Машины Azure Docker с помощью собственных шаблонов диспетчера ресурсов. toodo таким образом, добавить hello следующие шаблоны диспетчера ресурсов tooyour, определение hello `vmName` вашей виртуальной машины соответствующим образом:

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
    "typeHandlerVersion": "1.*",
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

