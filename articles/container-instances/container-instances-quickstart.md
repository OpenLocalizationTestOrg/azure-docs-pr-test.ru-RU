---
title: "aaaCreate первого контейнера экземпляры контейнером Azure | Azure документы"
description: "Начало работы со службой \"Экземпляры контейнеров Azure\" и развертывание в ней"
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: na
ms.topic: quickstart
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/26/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: b57c52714933bd3b28c44d33f9af7cd1f23fb951
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-container-in-azure-container-instances"></a>Создание первого контейнера в службе "Экземпляры контейнеров Azure"

Экземпляры контейнером Azure позволяет легко toocreate контейнеров и управления ими в Azure. В этом кратком руководстве вы создадите контейнер в Azure и предоставлять его toohello Интернет, общий IP-адрес. Эта операция выполняется при помощи одной команды. Через несколько секунд контейнер отобразится в браузере:

![Приложение, развернутое с помощью службы "Экземпляры контейнеров Azure" (просмотр в браузере)][aci-app-browser]

Если у вас еще нет подписки Azure, [создайте бесплатную учетную запись Azure](https://azure.microsoft.com/free/?WT.mc_id=A261C142F), прежде чем начинать работу.

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Если выбрать tooinstall и использовать hello CLI локально, краткого руководства требуется управлением hello Azure CLI версии 2.0.12 или более поздней версии. Запустите `az --version` версии toofind hello. Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli). 

## <a name="create-a-resource-group"></a>Создание группы ресурсов

Служба "Экземпляры контейнеров Azure" является ресурсом Azure и должна быть помещена в группу ресурсов Azure — логическую коллекцию, в которой выполняется развертывание ресурсов Azure и управление ими.

Создание группы ресурсов с hello [Создание группы az](/cli/azure/group#create) команды. 

Hello следующий пример создает группу ресурсов с именем *myResourceGroup* в hello *eastus* расположение.

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-a-container"></a>Создание контейнера

Чтобы создать контейнер, нужно указать его имя, образ Docker и группу ресурсов Azure. Может предоставлять toohello контейнера hello Интернет, общий IP-адрес. В этом случае мы используем контейнер, в котором размещено очень простое веб-приложение, написанное на [Node.js](http://nodejs.org).

```azurecli-interactive
az container create --name mycontainer --image microsoft/aci-helloworld --resource-group myResourceGroup --ip-address public 
```

Через несколько секунд вы должны получить tooyour запрос ответа. Изначально hello контейнер будет в **создание** состояние, но при этом следует запустить через несколько секунд. Можно проверить состояние hello, с помощью hello `show` команды:

```azurecli-interactive
az container show --name mycontainer --resource-group myResourceGroup
```

Внизу hello hello выходных данных вы увидите состояние подготовки hello контейнера и его IP-адрес:

```json
...
"ipAddress": {
      "ip": "13.88.8.148",
      "ports": [
        {
          "port": 80,
          "protocol": "TCP"
        }
      ]
    },
    "osType": "Linux",
    "provisioningState": "Succeeded"
...
```

После hello контейнер перемещает toohello **успешно** состояния, требуется получить доступ в браузере hello, с помощью IP-адрес hello предоставлен. 

![Приложение, развернутое с помощью службы "Экземпляры контейнеров Azure" (просмотр в браузере)][aci-app-browser]

## <a name="pull-hello-container-logs"></a>Журналы контейнера hello по запросу

Вы можете извлечь hello журналы для контейнера hello, созданных с помощью hello `logs` команды:

```azurecli-interactive
az container logs --name mycontainer --resource-group myResourceGroup
```

Выходные данные:

```bash
listening on port 80
::ffff:10.240.255.105 - - [21/Jul/2017:00:01:46 +0000] "GET / HTTP/1.1" 200 1663 "-" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
::ffff:10.240.255.105 - - [21/Jul/2017:00:01:46 +0000] "GET /favicon.ico HTTP/1.1" 404 150 "http://104.210.39.122/" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
```

## <a name="delete-hello-container"></a>Удаление контейнера hello

Закончив с контейнером hello, его можно удалить с помощью hello `delete` команды:

```azurecli-interactive
az container delete --name mycontainer --resource-group myResourceGroup
```

## <a name="next-steps"></a>Дальнейшие действия

Все hello кода для hello контейнер, используемый в данном кратком доступен [на GitHub][app-github-repo], вместе с его Dockerfile. При желании tootry его самостоятельно ее построении и развертывании экземпляры контейнером tooAzure, с помощью hello Azure контейнер реестра продолжить работу с учебником toohello экземпляров контейнера Azure.

> [!div class="nextstepaction"]
> [Руководства по использованию службы "Экземпляры контейнеров Azure"](./container-instances-tutorial-prepare-app.md)


<!-- LINKS -->
[app-github-repo]: https://github.com/Azure-Samples/aci-helloworld.git

<!-- IMAGES -->
[aci-app-browser]: ./media/container-instances-quickstart/aci-app-browser.png