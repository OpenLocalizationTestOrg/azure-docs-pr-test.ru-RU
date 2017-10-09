---
title: "размещает aaaCreate Docker в Azure с машины Docker | Документы Microsoft"
description: "Описывает использование узлов docker toocreate машин Docker в Azure."
services: azure-container-service
documentationcenter: na
author: mlearned
manager: douge
editor: 
ms.assetid: 7a3ff6e1-fa93-4a62-b524-ab182d2fea08
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 06/08/2016
ms.author: mlearned
ms.openlocfilehash: fbf67e8189bbf33f874c4a9b619a931f28ccee12
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-docker-hosts-in-azure-with-docker-machine"></a>Создание узлов Docker в Azure с помощью машины Docker
Под управлением [Docker](https://www.docker.com/) контейнеры требует узла виртуальной Машины выполняющегося hello управляющей программы docker.
В этом разделе описывается способ toouse hello [машины docker](https://docs.docker.com/machine/) команда toocreate новые виртуальные машины Linux настроены hello управляющей программы Docker в Azure. 

**Примечание.** 

* *Для выполнения действий, описанных в этой статье, требуется машина Docker версии 0.9.0-rc2 или более поздней версии.*
* *Контейнеры Windows поддерживаются через docker машину в hello ближайшее будущее*

## <a name="create-vms-with-docker-machine"></a>Создание виртуальных машин с помощью машины Docker
Создание docker узлов виртуальных машин в Azure с hello `docker-machine create` команду, указав hello `azure` драйвера. 

Hello Azure драйвер требуется идентификатор вашей подписки. Можно использовать hello [Azure CLI](cli-install-nodejs.md) или hello [портала Azure](https://portal.azure.com) tooretrieve подписки Azure. 

**С помощью портала Azure hello**

* Выберите **подписки** из hello левой панели навигации страницы и скопируйте hello идентификатор подписки.

**С помощью hello Azure CLI**

* Тип ```azure account list``` и идентификатор подписки hello копирования.

Тип `docker-machine create --driver azure` toosee hello параметры и их значения по умолчанию.
Можно также просмотреть hello [документации по драйверу Azure Docker](https://docs.docker.com/machine/drivers/azure/) Дополнительные сведения. 

Hello примере полагается на hello [значения по умолчанию](https://github.com/docker/machine/blob/master/drivers/azure/azure.go#L22), но при необходимости значение эти значения: 

* dns Azure для hello имя, связанное с общедоступным IP-hello и сертификаты, созданные. Это hello DNS-имя виртуальной машины. Hello ВМ можно затем безопасно остановить, выпуск hello динамических IP-адресов и предоставляют возможность tooreconnect hello после ВМ hello снова начинается с новый IP-адрес. префикс имени Hello должно быть уникальным для той области UNIQUE_DNSNAME_PREFIX.westus.cloudapp.azure.com.
* Открытие порта 80 в hello виртуальной Машины для исходящего доступа к Интернету
* размер hello хранилище быстрее premium tooutilize виртуальной Машины
* хранилище Premium, используемый для диска ВМ hello

```
docker-machine create -d azure --azure-subscription-id <Your AZURE_SUBSCRIPTION_ID> --azure-dns <Your UNIQUE_DNSNAME_PREFIX> --azure-open-port 80 --azure-size Standard_DS1_v2 --azure-storage-type "Premium_LRS" mydockerhost 
```

## <a name="choose-a-docker-host-with-docker-machine"></a>Выбор узла Docker с помощью машины Docker
При наличии запись машины docker для узла, можно задать узел по умолчанию hello при выполнении команды docker.

## <a name="using-powershell"></a>с использованием PowerShell.
```powershell
docker-machine env MyDockerHost | Invoke-Expression 
```

## <a name="using-bash"></a>Использование Bash
```bash
eval $(docker-machine env MyDockerHost)
```

Теперь можно запускать команды docker с указанным узлом hello

```
docker ps
docker info
```

## <a name="run-a-container"></a>Запуск контейнера
С настройки узла можно запустить простой web server tootest ли узла был настроен правильно.
Здесь мы использовать стандартный nginx образ, указать, что он должен прослушивать порт 80 и, если hello узла виртуальная машина перезапускается, hello контейнер будет перезапустить также (`--restart=always`). 

```bash
docker run -d -p 80:80 --restart=always nginx
```

Hello вывод должен выглядеть примерно hello следующим образом:

```
Unable toofind image 'nginx:latest' locally
latest: Pulling from library/nginx
efd26ecc9548: Pull complete
a3ed95caeb02: Pull complete
83f52fbfa5f8: Pull complete
fa664caa1402: Pull complete
Digest: sha256:12127e07a75bda1022fbd4ea231f5527a1899aad4679e3940482db3b57383b1d
Status: Downloaded newer image for nginx:latest
25942c35d86fe43c688d0c03ad478f14cc9c16913b0e1c2971cb32eb4d0ab721
```

## <a name="test-hello-container"></a>Тестовый контейнер hello
Проверьте запущенные контейнеры с помощью `docker ps`:

```bash
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                         NAMES
d5b78f27b335        nginx               "nginx -g 'daemon off"   5 minutes ago       Up 5 minutes        0.0.0.0:80->80/tcp, 443/tcp   goofy_mahavira
```

И, в контейнер типа запускается hello toosee `docker-machine ip <VM name>` tooenter toofind hello IP адрес в браузере hello:

```
PS C:\> docker-machine ip MyDockerHost
191.237.46.90
```

![Запущенный контейнер nginx](./media/vs-azure-tools-docker-machine-azure-config/nginxsuccess.png)

## <a name="summary"></a>Сводка
С помощью машины Docker можно легко подготовить узлы Docker в Azure к выполнению проверок отдельных узлов Docker.
Для рабочей среды размещения контейнеров, в разделе hello [контейнера службы Azure](http://aka.ms/AzureContainerService)

toodevelop основных приложений .NET в Visual Studio, в разделе [Docker средства для Visual Studio](http://aka.ms/DockerToolsForVS)

