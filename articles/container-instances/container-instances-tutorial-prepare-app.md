---
title: "aaaAzure экземпляры контейнером учебника - Подготовка приложения к | Azure документы"
description: "Подготовка приложения для развертывания tooAzure экземпляры контейнером"
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
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: 406ba796e5fefb1527f2e894cc3f7bbd8f7a5fd1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-container-for-deployment-tooazure-container-instances"></a>Создание контейнера для развертывания tooAzure экземпляры контейнером

Служба "Экземпляры контейнеров Azure" позволяет развертывать контейнеры Docker в инфраструктуре Azure без подготовки виртуальных машин или применения службы более высокого уровня. В этом руководстве мы создадим простое веб-приложение на Node.js и упакуем его в контейнер, который можно запустить в службе "Экземпляры контейнеров Azure". Мы рассмотрим:

> [!div class="checklist"]
> * Клонирование источника приложения из GitHub.  
> * Создание образов контейнеров из источника приложения.
> * Тестирование изображения hello в локальной среде Docker

В последующих учебниках можно отправить ваш образ tooan реестра контейнера Azure и развернуть их tooAzure экземпляры контейнером.

## <a name="before-you-begin"></a>Перед началом работы

Для выполнения действий, описанных в этом руководстве, необходимо базовое понимание основных понятий Docker, таких как контейнеры, образы контейнеров и основные команды Docker. При необходимости см. статью о [начале работы с Docker]( https://docs.docker.com/get-started/), чтобы ознакомиться с основами работы с контейнерами. 

toocomplete этого учебника требуется среда разработки Docker. Docker содержит пакеты, которые позволяют быстро настроить Docker в любой системе [Mac](https://docs.docker.com/docker-for-mac/), [Windows](https://docs.docker.com/docker-for-windows/) или [Linux](https://docs.docker.com/engine/installation/#supported-platforms).

## <a name="get-application-code"></a>Получение кода приложения

Образец Hello в этом учебнике включает простое веб-приложение [Node.js](http://nodejs.org). приложение Hello служит статических HTML-страницы и выглядит следующим образом:

![Приложение из руководства, отображающееся в браузере][aci-tutorial-app]

Использование образца hello toodownload git:

```bash
git clone https://github.com/Azure-Samples/aci-helloworld.git
```

## <a name="build-hello-container-image"></a>Создать образ контейнера hello

Hello Dockerfile, предоставленный в репозитории образец hello показано построение hello контейнера. Он начинается с [официальный изображения Node.js] [ dockerhub-nodeimage] на основе [Alpine Linux](https://alpinelinux.org/), небольшой распределение, которое является хорошо подходит toouse с контейнерами. Затем копирует файлы приложения hello в контейнер hello, устанавливает зависимостей с помощью диспетчера пакетов Node hello и затем запускает приложение hello.

```
FROM node:8.2.0-alpine
RUN mkdir -p /usr/src/app
COPY ./app/* /usr/src/app/
WORKDIR /usr/src/app
RUN npm install
CMD node /usr/src/app/index.js
```

Используйте hello `docker build` команда toocreate hello образ контейнера, как теги *aci учебника приложения*:

```bash
docker build ./aci-helloworld -t aci-tutorial-app
```

Используйте hello `docker images` toosee hello построения образа:

```bash
docker images
```

Выходные данные:

```bash
REPOSITORY                   TAG                 IMAGE ID            CREATED              SIZE
aci-tutorial-app             latest              5c745774dfa9        39 seconds ago       68.1 MB
```

## <a name="run-hello-container-locally"></a>Запустите контейнер hello локально

Прежде чем развертывание tooAzure контейнера hello экземпляров контейнера, запустите его локально tooconfirm его работы. Hello `-d` коммутатора позволяет контейнера hello выполняются в фоновом режиме hello, пока `-p` позволяет toomap порту произвольный вашей вычислений tooport 80 в контейнере hello.

```bash
docker run -d -p 8080:80 aci-tutorial-app
```

Привет открыть браузер toohttp://localhost:8080 tooconfirm, hello контейнер работает под управлением.

![Выполняемого приложения hello локально в браузере hello][aci-tutorial-app-local]

## <a name="next-steps"></a>Дальнейшие действия

В этом учебнике вы создали образа контейнера, который может быть экземпляров развернутых tooAzure контейнера. Привет, следующие шаги были выполнены:

> [!div class="checklist"]
> * Клонирование источника приложения hello из GitHub  
> * Создание образов контейнеров из источника приложения.
> * Тестирование локально контейнера hello

Переместить следующий учебник toolearn toohello о хранении образы контейнеров в контейнер Azure реестра.

> [!div class="nextstepaction"]
> [Принудительная tooAzure образов контейнера реестра](./container-instances-tutorial-prepare-acr.md)

<!-- LINKS -->
[dockerhub-nodeimage]: https://hub.docker.com/r/library/node/tags/8.2.0-alpine/

<!--- IMAGES --->
[aci-tutorial-app]:./media/container-instances-quickstart/aci-app-browser.png
[aci-tutorial-app-local]: ./media/container-instances-tutorial-prepare-app/aci-app-browser-local.png