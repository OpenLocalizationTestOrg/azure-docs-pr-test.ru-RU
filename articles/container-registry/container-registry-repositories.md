---
title: "aaaAzure контейнер реестра репозиториев | Документы Microsoft"
description: "Как toouse репозиториями реестра контейнера Azure для Docker images"
services: container-registry
documentationcenter: 
author: cristy
manager: balans
editor: dlepow
ms.service: container-registry
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2017
ms.author: cristyg
ms.openlocfilehash: 108622c565e41777fbb1fc9da9a01168abc7a7fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-container-registry-repositories"></a>Репозитории реестра контейнеров Azure

Контейнер Azure реестра позволяет toostore образы контейнеров в репозитории. Это позволяет содержать группы образов (версии образов) в изолированных средах. При выполнении отправки изображений tooyour реестра можно указать эти репозиториев.


## <a name="prerequisites"></a>Предварительные требования
* **Реестр контейнеров Azure.** Создайте реестр контейнеров в своей подписке Azure. Например, использовать hello [портал Azure](container-registry-get-started-portal.md) или hello [Azure CLI 2.0](container-registry-get-started-azure-cli.md).
* **Docker CLI** -tooset ваш локальный компьютер как узла и доступа к hello Docker CLI команды Docker, установите [подсистемы Docker](https://docs.docker.com/engine/installation/).
* **Изображение по запросу** — извлечь изображение из открытого реестра Docker Hub hello пометить ее и принудительно отправить его tooyour реестра. Рекомендации о том, как push и pull образов см. в разделе [Push Docker изображения tooAzure частного реестра](container-registry-get-started-docker-cli.md).


## <a name="viewing-repositories-in-hello-portal"></a>Просмотр репозитории в hello портала

После помещается реестра контейнера tooyour изображения, можно просмотреть список репозиториев hello размещение изображений hello в hello портал Azure.

Если вы следовали инструкциям hello hello [Push Docker изображения tooAzure частного реестра](container-registry-get-started-docker-cli.md) статьи, вы добавили изображения Nginx в реестре контейнера. Как часть инструкции hello следует указано пространство имен для hello изображения. В следующем примере hello команда hello помещает репозитория hello NGinx образов toohello «samples»:

```
docker push myregistry.azurecr.io/samples/nginx
```
 Реестр контейнеров Azure поддерживает многоуровневые пространства имен для репозитория. Эта функция позволяет вам toogroup коллекции изображений связанные tooa определенного приложения или коллекции toospecific разработки приложений или рабочей группы. tooread Дополнительные сведения о репозитории в контейнера реестры, в разделе [Docker закрытого контейнера реестры в Azure](container-registry-intro.md).

tooview hello контейнер реестра хранилища:

1. Войдите в toohello портал Azure
2. На hello **реестра контейнера Azure** колонку, вы хотите tooinspect реестра выберите hello
3. В колонке hello реестра щелкните **репозиториев** toosee список всех репозиториев hello и изображений
4. (Необязательно) Выберите теги toosee определенного образа

![Репозитории в портале hello](./media/container-registry-repositories/container-registry-repositories.png)


## <a name="next-steps"></a>Дальнейшие действия
Теперь, вы знаете основы hello, все готово toostart, с помощью реестра! Например, начать развертывание контейнера изображений tooan [контейнера службы Azure](https://azure.microsoft.com/documentation/services/container-service/) кластера.
