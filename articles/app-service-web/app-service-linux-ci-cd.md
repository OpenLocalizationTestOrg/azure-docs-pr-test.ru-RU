---
title: "aaaContinuous развертывания с веб-приложения Azure для Linux | Документы Microsoft"
description: "Как toosetup непрерывного развертывания в веб-приложения Azure в Linux."
keywords: "служба приложений azure, linux, oss, acr"
services: app-service
documentationcenter: 
author: ahmedelnably
manager: erikre
editor: 
ms.assetid: a47fb43a-bbbd-4751-bdc1-cd382eae49f8
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: aelnably;wesmc
ms.openlocfilehash: f94d837e27605da58428f507ab2b0eb3af3297e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-deployment-with-azure-web-app-on-linux"></a>Непрерывное развертывание для веб-приложения Azure на платформе Linux

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

В этом руководстве описывается настройка непрерывного развертывания для настраиваемого образа контейнера из управляемых репозиториев [реестра контейнеров Azure](https://azure.microsoft.com/en-us/services/container-registry/) или [Docker Hub](https://hub.docker.com).

## <a name="step-1---sign-in-tooazure"></a>Шаг 1. вход tooAzure

Войдите в toohello портал Azure по адресу http://portal.azure.com

## <a name="step-2---enable-container-continuous-deployment-feature"></a>Шаг 2. Включение функции непрерывного развертывания контейнера

Можно включить с помощью функции hello непрерывного развертывания [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) и выполнив следующую команду hello

```azurecli-interactive
az webapp deployment container config -n sname -g rgname -e true
``` 

В hello  **[портал Azure](https://portal.azure.com/)**, нажмите кнопку hello **службы приложений** параметр hello левой части страницы приветствия.

Щелкните имя нужного tooconfigure Docker Hub непрерывного развертывания для приложения hello.

В hello **параметры приложения**, добавьте параметр приложения `DOCKER_ENABLE_CI` со значением hello `true`.

![Изображение добавления параметра приложения](./media/app-service-webapp-service-linux-ci-cd/step2.png)

## <a name="step-3---prepare-webhook-url"></a>Шаг 3 . Подготовка URL-адреса Webhook

Можно получить с помощью URL-адрес веб-перехватчика hello [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) и выполнив следующую команду hello

```azurecli-interactive
az webapp deployment container -n sname1 -g rgname -e true --show-cd-url
``` 

Для hello URL-адрес веб-перехватчика необходимо toohave hello, следующая конечная точка: `https://<publishingusername>:<publishingpwd>@<sitename>.scm.azurewebsites.net/docker/hook`.

Вы можете получить ваш `publishingusername` и `publishingpwd` путем загрузки веб-приложения hello опубликовать профиль, воспользовавшись hello портал Azure.

![Изображение добавления webhook 2](./media/app-service-webapp-service-linux-ci-cd/step3-3.png)

## <a name="step-4---add-a-web-hook"></a>Шаг 4. Добавление webhook

### <a name="azure-container-registry"></a>Реестр контейнеров Azure

В колонке реестра щелкните **Webhooks** (Объекты webhook), создайте webhook, нажав кнопку **Добавить**. В hello **создать веб-перехватчика** колонки, присвойте имя вашего веб-перехватчика. Для hello URI веб-перехватчика необходимо hello tooprovide URL-адрес, полученный от **шаг 3**

Убедитесь, что определение области hello как hello репозитория, который содержит образ контейнера.

![изображение webhook](./media/app-service-webapp-service-linux-ci-cd/step3ACRWebhook-1.png)

При обновлении образа hello, веб-приложения hello автоматически обновляться при hello нового образа.

### <a name="docker-hub"></a>Docker Hub

На своей странице Docker Hub щелкните **Webhooks** (Объекты webhook), затем щелкните **CREATE A WEBHOOK** (Создать webhook).

![Изображение добавления webhook 1](./media/app-service-webapp-service-linux-ci-cd/step3-1.png)

Для hello URL-адрес веб-перехватчика необходимо hello tooprovide URL-адрес, полученный от **шаг 3**

![Изображение добавления webhook 2](./media/app-service-webapp-service-linux-ci-cd/step3-2.png)

При обновлении образа hello, веб-приложения hello автоматически обновляться при hello нового образа.

## <a name="next-steps"></a>Дальнейшие действия
* [Что такое веб-приложение Azure на платформе Linux?](./app-service-linux-intro.md)
* [Реестр контейнеров Azure](https://azure.microsoft.com/en-us/services/container-registry/)
* [Использование конфигурации PM2 для Node.js в веб-приложении Azure на платформе Linux](app-service-linux-using-nodejs-pm2.md)
* [Использование .NET Core в веб-приложении Azure на платформе Linux](app-service-linux-using-dotnetcore.md)
* [Использование Ruby в веб-приложении Azure на платформе Linux](app-service-linux-ruby-get-started.md)
* [Как toouse пользовательские Docker изображения для веб-приложения Azure в Linux](./app-service-linux-using-custom-docker-image.md)
* [Вопросы и ответы о веб-приложении службы приложений Azure на платформе Linux](./app-service-linux-faq.md) 
* [Управление веб-приложением на платформе Linux с помощью Azure CLI](./app-service-linux-cli.md)



