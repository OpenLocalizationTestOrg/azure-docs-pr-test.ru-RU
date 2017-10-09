---
title: "размещает toocreate aaaUse машины Docker Linux в Azure | Документы Microsoft"
description: "Описывает способ размещения toocreate машины Docker toouse Docker в Azure."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
ms.assetid: 164b47de-6b17-4e29-8b7d-4996fa65bea4
ms.service: virtual-machines-linux
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: iainfou
ms.openlocfilehash: 905c645add51c78305aac85a7013441b3a73972f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-docker-machine-toocreate-hosts-in-azure"></a>Способ размещения toocreate toouse машины Docker в Azure
Это статье сведения как toouse [машины Docker](https://docs.docker.com/machine/) toocreate узлов в Azure. Hello `docker-machine` команда создает Linux виртуальной машины (VM) в Azure, после чего устанавливает Docker. Затем можно будет управлять узлах Docker в Azure с помощью hello же локальные средства и рабочие процессы.

## <a name="create-vms-with-docker-machine"></a>Создание виртуальных машин с помощью машины Docker
Сначала получите идентификатор подписки Azure с помощью команды [az account show](/cli/azure/account#show) следующим образом:

```azurecli
sub=$(az account show --query "id" -o tsv)
```

Создание виртуальных машин узла Docker в Azure с помощью `docker-machine create` , указав *azure* как драйвер hello. Дополнительные сведения см. в разделе hello [документации по драйверу Azure Docker](https://docs.docker.com/machine/drivers/azure/)

Hello следующий пример создает Виртуальную машину с именем *myVM*, создает учетную запись пользователя с именем *azureuser*и открывает порт *80* с hello узел виртуальной Машины. Выполните все запросы toolog в tooyour учетная запись Azure и предоставить разрешения toocreate машины Docker и управлять ресурсами.

```bash
docker-machine create -d azure \
    --azure-subscription-id $sub \
    --azure-ssh-user azureuser \
    --azure-open-port 80 \
    myvm
```

Hello выходные данные выглядят аналогично toohello в следующем примере:

```bash
Creating CA: /Users/user/.docker/machine/certs/ca.pem
Creating client certificate: /Users/user/.docker/machine/certs/cert.pem
Running pre-create checks...
(myvmdocker) Completed machine pre-create checks.
Creating machine...
(myvmdocker) Querying existing resource group.  name="docker-machine"
(myvmdocker) Creating resource group.  name="docker-machine" location="westus"
(myvmdocker) Configuring availability set.  name="docker-machine"
(myvmdocker) Configuring network security group.  name="myvmdocker-firewall" location="westus"
(myvmdocker) Querying if virtual network already exists.  rg="docker-machine" location="westus" name="docker-machine-vnet"
(myvmdocker) Creating virtual network.  name="docker-machine-vnet" rg="docker-machine" location="westus"
(myvmdocker) Configuring subnet.  name="docker-machine" vnet="docker-machine-vnet" cidr="192.168.0.0/16"
(myvmdocker) Creating public IP address.  name="myvmdocker-ip" static=false
(myvmdocker) Creating network interface.  name="myvmdocker-nic"
(myvmdocker) Creating storage account.  sku=Standard_LRS name="vhdski0hvfazyd8mn991cg50" location="westus"
(myvmdocker) Creating virtual machine.  location="westus" size="Standard_A2" username="azureuser" osImage="canonical:UbuntuServer:16.04.0-LTS:latest" name="myvmdocker"
Waiting for machine toobe running, this may take a few minutes...
Detecting operating system of created instance...
Waiting for SSH toobe available...
Detecting hello provisioner...
Provisioning with ubuntu(systemd)...
Installing Docker...
Copying certs toohello local machine directory...
Copying certs toohello remote machine...
Setting Docker configuration on hello remote daemon...
Checking connection tooDocker...
Docker is up and running!
toosee how tooconnect your Docker Client toohello Docker Engine running on this virtual machine, run: docker-machine env myvmdocker
```

## <a name="configure-your-docker-shell"></a>Настройка оболочки Docker
узел Docker tooyour tooconnect в Azure, определите hello соответствующих параметров подключения. Как уже отмечалось в конце hello hello выходных данных, просмотрите hello сведения о соединении для узла Docker следующим образом: 

```bash
docker-machine env myvmdocker
```

Hello вывода будет примерно toohello следующий пример:

```bash
export DOCKER_TLS_VERIFY="1"
export DOCKER_HOST="tcp://40.68.254.142:2376"
export DOCKER_CERT_PATH="/Users/user/.docker/machine/machines/machine"
export DOCKER_MACHINE_NAME="machine"
# Run this command tooconfigure your shell:
# eval $(docker-machine env myvmdocker)
```

Вы можете либо выполнения hello параметры подключения hello toodefine предлагаемый команда конфигурации (`eval $(docker-machine env myvmdocker)`), или вручную задать переменные среды hello. 

## <a name="run-a-container"></a>Запуск контейнера
toosee контейнера в действии, позволяет выполнить основные веб-сервер NGINX. Создайте контейнер с `docker run` и настройте порт 80 для веб-трафика следующим образом:

```bash
docker run -d -p 80:80 --restart=always nginx
```

Hello вывода будет примерно toohello следующий пример:

```bash
Unable toofind image 'nginx:latest' locally
latest: Pulling from library/nginx
ff3d52d8f55f: Pull complete
226f4ec56ba3: Pull complete
53d7dd52b97d: Pull complete
Digest: sha256:41ad9967ea448d7c2b203c699b429abe1ed5af331cd92533900c6d77490e0268
Status: Downloaded newer image for nginx:latest
675e6056cb81167fe38ab98bf397164b01b998346d24e567f9eb7a7e94fba14a
```

Проверьте запущенные контейнеры с помощью `docker ps`: Hello в выводе следующего примера показано контейнера NGINX hello, запущенного с портом 80 предоставляется.

```bash
CONTAINER ID    IMAGE    COMMAND                   CREATED          STATUS          PORTS                          NAMES
d5b78f27b335    nginx    "nginx -g 'daemon off"    5 minutes ago    Up 5 minutes    0.0.0.0:80->80/tcp, 443/tcp    festive_mirzakhani
```

## <a name="test-hello-container"></a>Тестовый контейнер hello
Получите hello общедоступный IP-адрес узла Docker следующим образом:


```bash
docker-machine ip myvmdocker
```

контейнер toosee hello в действии, откройте веб-браузер и введите hello общедоступный IP-адрес, указаны в выходные данные hello hello предшествующий команды:

![Запущенный контейнер nginx](./media/docker-machine/nginx.png)

## <a name="next-steps"></a>Дальнейшие действия
Можно также создать узлы с hello [расширение ВМ Docker](dockerextension.md). Примеры использования Docker Compose см. в статье [Приступая к работе с Docker и Compose для определения и запуска многоконтейнерного приложения в Azure](docker-compose-quickstart.md).
