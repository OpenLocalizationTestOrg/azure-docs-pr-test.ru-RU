---
title: "Учебник экземпляры контейнером aaaAzure - развертывание приложения | Документы Microsoft"
description: "Руководство по службе \"Экземпляры контейнеров Azure\". Развертывание приложения"
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
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/04/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: b9fb098d9491e1073f0be4b14a0b9b1a18f16095
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-container-tooazure-container-instances"></a>Разверните контейнер tooAzure экземпляры контейнером

Это hello последнего учебника трех частей. В предыдущих разделах [был создан образ контейнера](container-instances-tutorial-prepare-app.md) и [помещается tooan реестра контейнера Azure](container-instances-tutorial-prepare-acr.md). В этом разделе завершает учебник hello, развернув контейнер hello tooAzure экземпляры контейнером. В частности, рассматриваются такие шаги:

> [!div class="checklist"]
> * Определение группы контейнеров с использованием шаблона Azure Resource Manager
> * Развертывание группы hello контейнера, с помощью hello Azure CLI
> * Просмотр журналов контейнера

## <a name="deploy-hello-container-using-hello-azure-cli"></a>Развертывание с помощью Azure CLI hello контейнера hello

Hello Azure CLI обеспечивает развертывание контейнера tooAzure экземпляры контейнером с помощью одной команды. Поскольку образ контейнера hello размещается в hello частного реестра контейнера Azure, следует включить tooaccess необходимые учетные данные hello его. При необходимости их можно запросить, как показано ниже.

Сервер входа в реестр контейнеров (укажите используемое имя реестра):

```azurecli-interactive
az acr show --name <acrName> --query loginServer
```

Пароль для реестра контейнеров:

```azurecli-interactive
az acr credential show --name <acrName> --query "passwords[0].value"
```

toodeploy образ контейнера из реестра hello контейнера с ресурсом запрос 1 ядра Процессора и 1 ГБ памяти, запустите следующую команду hello:

```azurecli-interactive
az container create --name aci-tutorial-app --image <acrLoginServer>/aci-tutorial-app:v1 --cpu 1 --memory 1 --registry-password <acrPassword> --ip-address public -g myResourceGroup
```

В течение нескольких секунд вы получите исходный ответ Azure Resource Manager. состояние hello tooview hello развертывания, используйте:

```azurecli-interactive
az container show --name aci-tutorial-app --resource-group myResourceGroup --query state
```

Мы можем продолжать выполнение этой команды, пока не изменится состояние hello из *ожидающие* слишком*под управлением*. Затем можно продолжить.

## <a name="view-hello-application-and-container-logs"></a>Просмотр журналов приложений и контейнер hello

После успешного развертывания hello, откройте браузер toohello IP-адреса в выходные данные hello hello следующую команду:

```bash
az container show --name aci-tutorial-app --resource-group myResourceGroup --query ipAddress.ip
```

```json
"13.88.176.27"
```

![Приложение Hello world в браузере hello][aci-app-browser]

Можно также просмотреть выходные данные журнала hello hello контейнера:

```azurecli-interactive
az container logs --name aci-tutorial-app -g myResourceGroup
```

Выходные данные:

```bash
listening on port 80
::ffff:10.240.0.4 - - [21/Jul/2017:06:00:02 +0000] "GET / HTTP/1.1" 200 1663 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
::ffff:10.240.0.4 - - [21/Jul/2017:06:00:02 +0000] "GET /favicon.ico HTTP/1.1" 404 150 "http://13.88.176.27/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
```

## <a name="next-steps"></a>Дальнейшие действия

В этом учебнике вы выполнили hello процесс развертывания вашего контейнеры tooAzure экземпляры контейнером. Привет, следующие шаги были выполнены:

> [!div class="checklist"]
> * Развертывание hello контейнера с помощью реестра контейнера Azure hello hello Azure CLI
> * Приложение hello для просмотра в браузере hello
> * Просмотр журналов контейнера hello

<!-- LINKS -->
[prepare-app]: ./container-instances-tutorial-prepare-app.md

<!-- IMAGES -->
[aci-app-browser]: ./media/container-instances-quickstart/aci-app-browser.png
