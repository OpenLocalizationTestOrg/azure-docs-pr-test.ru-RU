---
title: "aaaUse Docker Compose на виртуальной Машине Linux в Azure | Документы Microsoft"
description: "Как toouse Docker и создать на виртуальных машинах Linux с hello Azure CLI"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 02ab8cf9-318d-4a28-9d0c-4a31dccc2a84
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: cf7254ad4813ccdc641fcacbb06ed1514a93cee5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-docker-and-compose-toodefine-and-run-a-multi-container-application-in-azure"></a>Получить работы с Docker и составление toodefine и запустите приложение контейнера несколькими в Azure
С [составление](http://github.com/docker/compose), используйте toodefine простой текстовый файл приложения, состоящего из нескольких контейнеров Docker. Затем вы запустили приложение с помощью одной команды, которая поддерживает все toodeploy в определенной среде. Например в этой статье рассказывается, как tooquickly настроить блог WordPress с серверной базы данных MariaDB SQL на Виртуальной машине Ubuntu. Также можно создать tooset копирование более сложных приложений.


## <a name="set-up-a-linux-vm-as-a-docker-host"></a>Настройка виртуальной машины Linux как узла Docker
Можно использовать различные процедуры Azure и доступных образов или шаблонов диспетчера ресурсов в Azure Marketplace hello toocreate виртуальной Машины Linux и настроить его для использования в качестве узла Docker. Просмотреть, например [среды с помощью hello расширение ВМ Docker toodeploy](dockerextension.md) tooquickly Создание Виртуальной машине Ubuntu с hello расширения виртуальной Машины Azure Docker с помощью [шаблоном краткого руководства](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu). 

При использовании расширение ВМ Docker hello ВМ автоматически настроить узел Docker и составление уже установлена.


### <a name="create-docker-host-with-azure-cli-20"></a>Создание узлов Docker с помощью Azure CLI 2.0
Последняя версия hello установки [Azure CLI 2.0](/cli/azure/install-az-cli2) и войти в систему с учетной записью Azure tooan [входа az](/cli/azure/#login).

Сначала создайте группу ресурсов для среды Docker командой [az group create](/cli/azure/group#create). Hello следующий пример создает группу ресурсов с именем *myResourceGroup* в hello *westus* расположение:

```azurecli
az group create --name myResourceGroup --location westus
```

Затем разверните виртуальную Машину с [создания развертывания группы az](/cli/azure/group/deployment#create) , включает в себя расширение виртуальной Машины Azure Docker hello из [этого шаблона диспетчера ресурсов Azure на GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu). Укажите собственные значения для параметров *newStorageAccountName*, *adminUsername*, *adminPassword* и *dnsNameForPublicIP*:

```azurecli
az group deployment create --resource-group myResourceGroup \
  --parameters '{"newStorageAccountName": {"value": "mystorageaccount"},
    "adminUsername": {"value": "azureuser"},
    "adminPassword": {"value": "P@ssw0rd!"},
    "dnsNameForPublicIP": {"value": "mypublicdns"}}' \
  --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/docker-simple-on-ubuntu/azuredeploy.json
```

Он занимает несколько минут для развертывания toofinish hello. После завершения развертывания hello [переместить шаг toonext](#verify-that-compose-is-installed) tooSSH tooyour виртуальной Машины. 

При необходимости строки toohello tooinstead возвращаемого элемента управления и позволяют hello развертывания по-прежнему в фоновом режиме hello, добавьте hello `--no-wait` флаг toohello предшествующий команды. Этот процесс позволяет tooperform другие действия в hello CLI во время развертывания hello продолжается несколько минут. Затем можно просмотреть подробные сведения о состоянии узла Docker hello с [Показать ВМ az](/cli/azure/vm#show). Hello следующий пример проверяет состояние виртуальной Машины с именем hello hello *myDockerVM* (имя по умолчанию на основе шаблона hello hello — не изменять это имя) в группе ресурсов hello с именем *myResourceGroup*:

```azurecli
az vm show \
    --resource-group myResourceGroup \
    --name myDockerVM \
    --query [provisioningState] \
    --output tsv
```

Если эта команда возвращает *успешно*, завершения развертывания hello и вы можете toohello SSH виртуальной Машины в даст hello.


## <a name="verify-that-compose-is-installed"></a>Проверка установки Compose
После завершения развертывания hello SSH tooyour новый узел Docker с помощью DNS-имя hello указанный во время развертывания. Можно использовать `az vm show -g myResourceGroup -n myDockerVM -d --query [fqdns] -o tsv` tooview подробные сведения о виртуальной Машины, включая hello DNS-имя.

```bash
ssh azureuser@mypublicdns.westus.cloudapp.azure.com
```

toocheck, составления устанавливается на hello виртуальных Машин, запустите hello следующую команду:

```bash
docker-compose --version
```

Увидеть результаты, аналогичные слишком*1.6.2 docker создания, построения 4d 72027*.

> [!TIP]
> Если используется другой метод toocreate узел Docker и требуется tooinstall составления самостоятельно, см. раздел hello [составления документации](https://github.com/docker/compose/blob/882dc673ce84b0b29cd59b6815cb93f74a6c4134/docs/install.md).


## <a name="create-a-docker-composeyml-configuration-file"></a>Создание файла конфигурации docker-compose.yml
Далее нужно создать `docker-compose.yml` файл, который является просто текстового файла конфигурации, toorun контейнеры Docker toodefine hello на hello виртуальной Машины. файл Hello указывает toorun hello изображения на каждый контейнер (или может быть сборки из файла Dockerfile), необходимые переменные среды и зависимости, порты и hello ссылки между контейнерами. Дополнительные сведения о синтаксисе YML-файла приведены в [справке по файлу Compose](https://docs.docker.com/compose/compose-file/).

Создать hello *docker compose.yml* следующим образом:

```bash
touch docker-compose.yml
```

Используйте вашей tooadd привычном текстовом редакторе файл toohello некоторых данных. Hello следующий пример использует hello *vi* редактора:

```bash
vi docker-compose.yml
```

Вставьте следующий пример в текстовый файл hello. Эта конфигурация использует изображения из hello [DockerHub реестра](https://registry.hub.docker.com/_/wordpress/) tooinstall WordPress (Привет открыть источник ведения блогов и система управления содержимым) и связанные базы данных MariaDB SQL базы данных. Введите собственное значение *MYSQL_ROOT_PASSWORD* следующим образом:

```sh
wordpress:
  image: wordpress
  links:
    - db:mysql
  ports:
    - 80:80

db:
  image: mariadb
  environment:
    MYSQL_ROOT_PASSWORD: <your password>
```

## <a name="start-hello-containers-with-compose"></a>Начать с создания сообщения hello контейнеров
В hello же каталоге, что ваш *docker compose.yml* файл, запустите следующую команду hello (в зависимости от среды, может потребоваться toorun `docker-compose` с помощью `sudo`):

```bash
docker-compose up -d
```

Эта команда запускает контейнеры Docker hello, указанный в *docker compose.yml*. Он принимает одну или две для этого шага toocomplete минуты. Можно увидеть примерно toohello вывода следующий пример:

```bash
Creating wordpress_db_1...
Creating wordpress_wordpress_1...
...
```

> [!NOTE]
> Быть убедиться, что hello toouse **-d** параметра при запуске, чтобы контейнеры hello выполняться непрерывно в фоновом режиме hello.


tooverify, функционируют контейнеры hello типа `docker-compose ps`. Вы увидите нечто вроде этого:

```bash
        Name                       Command               State         Ports
-----------------------------------------------------------------------------------
azureuser_db_1          docker-entrypoint.sh mysqld      Up      3306/tcp
azureuser_wordpress_1   docker-entrypoint.sh apach ...   Up      0.0.0.0:80->80/tcp
```

Теперь можно подключиться tooWordPress непосредственно на hello виртуальной Машины на порт 80. Откройте веб-браузер и введите hello DNS-имя виртуальной Машины (например, `http://mypublicdns.westus.cloudapp.azure.com`). Теперь вы увидите экран, где можно завершить установку hello и приступить к работе с приложением hello запуска WordPress hello.

![Начальный экран WordPress][wordpress_start]

## <a name="next-steps"></a>Дальнейшие действия
* Go toohello [руководство пользователя по модулю виртуальной Машины Docker](https://github.com/Azure/azure-docker-extension/blob/master/README.md) Дополнительные параметры tooconfigure Docker и создать ВМ Docker. Например один вариант — Создать yml hello tooput файл (преобразованный tooJSON) непосредственно в конфигурации hello hello расширение ВМ Docker.
* Извлечение hello [составления Справочник по командной строке](http://docs.docker.com/compose/reference/) и [руководство пользователя по](http://docs.docker.com/compose/) Дополнительные примеры создания и развертывания приложений с несколькими контейнера.
* Использовать шаблон диспетчера ресурсов Azure, либо ваш собственный или один были получены из hello [сообщества](https://azure.microsoft.com/documentation/templates/), toodeploy ВМ Azure с Docker и приложения для установки создания. Здравствуйте, например, [развертывание блог WordPress с помощью Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-wordpress-mysql) Docker использует шаблон и создать tooquickly развертывание WordPress с серверной на Виртуальной машине Ubuntu MySQL.
* Попытайтесь интегрировать Docker Compose с кластером Docker Swarm. Сценарии приведены в статье [Using Swarm with Compose](https://docs.docker.com/compose/swarm/) (Совместное использование Compose и Swarm).

<!--Image references-->

[wordpress_start]: media/docker-compose-quickstart/WordPress.png
