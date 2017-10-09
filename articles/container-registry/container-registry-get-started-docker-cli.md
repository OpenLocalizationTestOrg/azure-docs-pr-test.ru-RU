---
title: "tooprivate образа Docker aaaPush реестра Azure | Документы Microsoft"
description: "По запросу и принудительные Docker реестра закрытый контейнер tooa образы в Azure с помощью hello Docker CLI"
services: container-registry
documentationcenter: 
author: stevelas
manager: balans
editor: cristyg
tags: 
keywords: 
ms.assetid: 64fbe43f-fdde-4c17-a39a-d04f2d6d90a1
ms.service: container-registry
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2017
ms.author: stevelas
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a81a6f4bfcb23642a89ac7631348d40e2f4911a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="push-your-first-image-tooa-private-docker-container-registry-using-hello-docker-cli"></a>Первый изображения tooa закрытый Docker контейнер реестра hello Docker CLI с помощью принудительной отправки
В реестре контейнер Azure хранит данные и управляет закрытый [Docker](http://hub.docker.com) образы контейнеров, аналогичные toohello способом [Docker Hub](https://hub.docker.com/) хранит общедоступные образы Docker. Использовать hello [интерфейс командной строки Docker](https://docs.docker.com/engine/reference/commandline/cli/) (Docker CLI) для [входа](https://docs.docker.com/engine/reference/commandline/login/), [принудительной](https://docs.docker.com/engine/reference/commandline/push/), [запросу](https://docs.docker.com/engine/reference/commandline/pull/)и других операций в контейнер реестр.

Дополнительные сведения и основные понятия в разделе [Здравствуйте, Обзор](container-registry-intro.md)



## <a name="prerequisites"></a>Предварительные требования
* **Реестр контейнеров Azure.** Создайте реестр контейнеров в своей подписке Azure. Например, использовать hello [портал Azure](container-registry-get-started-portal.md) или hello [Azure CLI 2.0](container-registry-get-started-azure-cli.md).
* **Docker CLI** -tooset ваш локальный компьютер как узла и доступа к hello Docker CLI команды Docker, установите [подсистемы Docker](https://docs.docker.com/engine/installation/).

## <a name="log-in-tooa-registry"></a>Войдите в реестре tooa
Запустите `docker login` toolog в реестре контейнеров tooyour с вашей [учетные данные реестра](container-registry-authentication.md).

Hello следующий пример hello ID и пароль передаются из Azure Active Directory [участника-службы](../active-directory/active-directory-application-objects.md). Например которые были назначены реестр службы основной tooyour сценария автоматизации.

```
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

> [!TIP]
> Создать убедиться, что toospecify hello реестра полное имя (прописными буквами). В нашем примере поисковый запрос будет выглядеть так: `myregistry.azurecr.io`.

## <a name="steps-toopull-and-push-an-image"></a>Toopull действия и отправка изображения
Hello выполнить пример, что загрузка hello Nginx изображения из реестра Docker Hub, открытого с hello, теги в реестр закрытый контейнер Azure, отправляющий ее tooyour реестра, а затем извлекает его еще раз.

**1. Официальный образа Docker hello по запросу для Nginx**

Сначала по запросу hello открытый Nginx tooyour локального компьютера-образца.

```
docker pull nginx
```
**2. Запустите контейнер Nginx hello**

Hello следующая команда запускает hello локального Nginx контейнера интерактивно через порт 8080, позволяя toosee вывод Nginx. Удаляет контейнер после остановки запускается hello.

```
docker run -it --rm -p 8080:80 nginx
```

Обзор слишком[http://localhost: 8080](http://localhost:8080) tooview hello контейнер запускается. Вы увидите примерно toohello экрана, выполнив одно.

![Nginx на локальном компьютере](./media/container-registry-get-started-docker-cli/nginx.png)

toostop Здравствуйте запущенного контейнера, нажмите клавишу [CTRL] + [C].

**3. Создайте псевдоним hello изображения в реестре**

Hello следующая команда создает псевдоним изображения hello с реестра tooyour полный путь. В этом примере указывается hello `samples` перегруженность hello корень реестра hello tooavoid пространства имен.

```
docker tag nginx myregistry.azurecr.io/samples/nginx
```  

**4. Изображение tooyour принудительной hello реестра**

```
docker push myregistry.azurecr.io/samples/nginx
```

**5. Изображение hello запросу из системного реестра**

```
docker pull myregistry.azurecr.io/samples/nginx
```

**6. Запустите контейнер Nginx hello из системного реестра**

```
docker run -it --rm -p 8080:80 myregistry.azurecr.io/samples/nginx
```

Обзор слишком[http://localhost: 8080](http://localhost:8080) tooview hello контейнер запускается.

toostop Здравствуйте запущенного контейнера, нажмите клавишу [CTRL] + [C].

**7. (Необязательно) Удаление образа hello**

```
docker rmi myregistry.azurecr.io/samples/nginx
```

##<a name="concurrent-limits"></a>Ограничения на параллельную обработку
В некоторых случаях параллельное выполнение вызовов может привести к ошибкам. в следующей таблице Hello содержит hello ограничения количества одновременных вызовов «Push» и «Pull» операции на контейнер Azure реестра:

| Операция  | Ограничение                                  |
| ---------- | -------------------------------------- |
| PULL       | Копирование too10 параллельных запрашивает в реестре |
| PUSH       | Копирование too5 параллельных помещает в реестре |

## <a name="next-steps"></a>Дальнейшие действия
Теперь, вы знаете основы hello, все готово toostart, с помощью реестра! Например, начать развертывание контейнера изображений tooan [контейнера службы Azure](https://azure.microsoft.com/documentation/services/container-service/) кластера.
