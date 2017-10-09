---
title: "веб-приложения на платформе Linux с помощью Azure CLI 2.0 aaaManage | Документы Microsoft"
description: "Управляйте веб-приложением на платформе Linux с помощью Azure CLI."
keywords: "служба приложений azure, веб-приложение, cli, linux, oss"
services: app-service
documentationCenter: 
author: ahmedelnably
manager: erikre
editor: 
ms.assetid: 
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: aelnably
ms.openlocfilehash: 5e8e0da8a362450c56d2e87e087f77598ec874ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-web-app-on-linux-using-azure-cli"></a>Управление веб-приложением на платформе Linux с помощью Azure CLI

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

С помощью команд hello в этой статье вы можете toocreate и управлять веб-приложения на платформе Linux с помощью Azure CLI 2.0.
Можно приступить к использованию новой версии hello hello CLI двумя способами:

* [установить Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) на компьютер;
* использовать [Azure Cloud Shell (предварительная версия)](../cloud-shell/overview.md).


## <a name="create-a-linux-app-service-plan"></a>Создание плана службы приложений Linux

toocreate план службы Linux приложений, можно использовать hello следующую команду:

```azurecli-interactive
az appservice plan create -n appname -g rgname --islinux -l "South Central US" --sku S1 --number-of-workers 1
``` 

## <a name="create-a-custom-docker-container-web-app"></a>Создание пользовательского веб-приложения контейнера Docker

toocreate веб-приложения и его настройки toorun пользовательский контейнер Docker, можно использовать hello следующую команду:

```azurecli-interactive
az webapp create -n sname -g rgname -p pname -i elnably/dockerimagetest
```
 
## <a name="activate-hello-docker-container-logging"></a>Активация ведения журнала контейнера Docker hello

tooactivate Здравствуйте ведения журнала контейнера Docker, можно использовать hello следующую команду:

```azurecli-interactive
az webapp log config -n sname -g rgname --web-server-logging filesystem
```
 
## <a name="change-hello-custom-docker-container-for-an-existing-web-app-on-linux-app"></a>Изменить пользовательский контейнер Docker hello для существующего веб-приложения, для приложения Linux

toochange ранее созданное приложение, из hello текущего изображения tooa нового образа Docker, можно использовать hello следующую команду:

```azurecli-interactive
az webapp config container set -n sname -g rgname -c apurvajo/mariohtml5
``` 

## <a name="using-docker-images-from-a-private-registry"></a>Использование образов Docker из частного реестра

Вы можете настроить toouse изображений для вашего приложения из частного реестра. Требуется URL-адрес hello tooprovide для реестра, имя пользователя и пароль. Это можно сделать с помощью hello следующую команду:

```azurecli-interactive
az webapp config container set -n sname1 -g rgname -c <container name> -r <server url> -u <username> -p <password>
``` 

## <a name="enable-continuous-deployments-for-custom-docker-images"></a>Включение непрерывного развертывания для пользовательских образов Docker

С hello следующую команду можно включить функции hello компакт-диска и получить URL-адрес веб-перехватчика hello. Этот URL-адрес может быть используется tooconfigure вы DockerHub или реестр контейнера Azure репозиториев.

```azurecli-interactive
az webapp deployment container config -n sname -g rgname -e true
``` 

## <a name="create-a-web-app-on-linux-app-using-one-of-our-built-in-runtime-frameworks"></a>Создание веб-приложения в приложении Linux с помощью одной из наших встроенных платформ среды выполнения

toocreate веб-приложения PHP 5.6 приложения Linux, можно использовать следующую команду hello.

```azurecli-interactive
az webapp create -n sname -g rgname -p pname -r "php|5.6"
``` 

## <a name="change-framework-version-for-an-existing-web-app-on-linux-app"></a>Изменение версии платформы для имеющегося веб-приложения в приложении Linux

toochange ранее созданное приложение, из версии tooNode.js hello текущего framework 6.11 можно использовать hello следующую команду:

```azurecli-interactive
az webapp config set -n sname -g rgname --linux-fx-version "node|6.11"
``` 

## <a name="set-up-git-deployments-for-your-web-app"></a>Настройка развертываний Git для веб-приложения

tooset копирование Git развертывания для приложения можно использовать hello следующую команду:

```azurecli-interactive
az webapp deployment source config -n sname -g rgname --repo-url <gitrepo url> --branch <branch>
``` 


## <a name="next-steps"></a>Дальнейшие действия
* [Что такое веб-приложение Azure на платформе Linux?](app-service-linux-intro.md)
* [Установите Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).
* [Обзор Azure Cloud Shell (предварительная версия)](../cloud-shell/overview.md)
* [Настройка промежуточных сред в службе приложений Azure](./web-sites-staged-publishing.md)
* [Непрерывное развертывание для веб-приложения Azure на платформе Linux](./app-service-linux-ci-cd.md)
