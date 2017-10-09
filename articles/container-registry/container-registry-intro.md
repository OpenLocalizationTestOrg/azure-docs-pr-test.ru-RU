---
title: "aaaPrivate Docker контейнера реестры в Azure | Документы Microsoft"
description: "Введение toohello службы реестра контейнера Azure, предоставляя Облачное, управляемый частных реестрах Docker."
services: container-registry
documentationcenter: 
author: stevelas
manager: balans
editor: dlepow
tags: 
keywords: 
ms.assetid: ee2b652b-fb7c-455b-8275-b8d4d08ffeb3
ms.service: container-registry
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2017
ms.author: stevelas
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f6edcf0bf947b7770ee0a4e4a5cfbf4ef8b7392a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooprivate-docker-container-registries"></a>Введение tooprivate Docker контейнера реестры


Azure реестра контейнер является управляемой [реестра Docker](https://docs.docker.com/registry/) службы на основании hello 2.0 реестра Docker открытым исходным кодом. Создать и поддерживать Azure контейнера реестры toostore и управлять к частной [контейнера Docker](https://www.docker.com/what-docker) изображения. Использование контейнера реестры в Azure с помощью существующего контейнера разработки и развертывания конвейеры и отрисовки в тексте hello опытом сообщества Docker.

Общие сведения о Docker и контейнерах см. в следующих источниках:

* [Руководство пользователя Docker](https://docs.docker.com/engine/userguide/)




## <a name="use-cases"></a>Варианты использования
По запросу изображений из контейнера Azure целевых объектов развертывания toovarious реестра:

* **Масштабируемые системы управления**, управляющие контейнерными приложениями в кластерах узлов, в том числе [DC/OS](https://docs.mesosphere.com/), [Docker Swarm](https://docs.docker.com/swarm/) и [Kubernetes](http://kubernetes.io/docs/).
* **Службы Azure**, поддерживающие создание и выполнение масштабированных приложений, в том числе [служба контейнеров](../container-service/index.yml), [служба приложений](/app-service/index.md), [пакетная служба](../batch/index.md), [Service Fabric](/azure/service-fabric/) и т. д.

Разработчики также можно передать реестра tooa контейнер в рамках рабочего процесса разработки контейнера. Например, они могут получить доступ к реестру контейнеров из средства развертывания и обеспечения непрерывной интеграции, например [Visual Studio Team Services](https://www.visualstudio.com/docs/overview) или [Jenkins](https://jenkins.io/).





## <a name="key-concepts"></a>Основные понятия
* **Реестр.** Создайте один или несколько реестров контейнеров в своей подписке Azure. Стандартная Azure резервируется каждого реестра [учетной записи хранилища](../storage/common/storage-introduction.md) в hello местоположения. Воспользоваться преимуществами локальной сети закрыть хранилища образов контейнера, создав реестра в hello же расположению Azure развертываний. Имя полное реестра имеет вид hello `myregistry.azurecr.io`.

  Вы [управления доступом](container-registry-authentication.md) tooa контейнер реестра с помощью резервного Azure Active Directory [участника-службы](../active-directory/active-directory-application-objects.md) или предоставленный администратора учетной записи. Стандартная выполнения hello `docker login` tooauthenticate команда с помощью реестра.

* **Управляемый реестр.** Это уровень, который предоставляет дополнительные возможности для реестров в трех SKU — "Базовый", "Стандартный" и "Премиум". Hello изображения в этих продуктов хранятся в учетных записях хранения управляется hello Azure контейнера реестры службу, которая повышает надежность и новые возможности. Новые возможности включают интеграцию веб-перехватчика, проверку подлинности репозитория с помощью Azure Active Directory и поддержку функции удаления. Пользователи имеют toochoose параметр hello между управляемого реестров или toocreate реестра, поддерживаемый свои собственные учетные записи хранения при создании реестров.

* **Репозиторий.** Каждый реестр содержит по крайней мере один репозиторий, представляющий собой группу образов контейнеров. Реестр контейнеров Azure поддерживает многоуровневые пространства имен для репозитория. Эта функция позволяет вам toogroup коллекции изображений связанные tooa определенного приложения или коллекции toospecific разработки приложений или рабочей группы. Например:

  * `myregistry.azurecr.io/aspnetcore:1.0.1` представляет образ, используемый в организации;
  * `myregistry.azurecr.io/warrantydept/dotnet-build`Представляет изображение используется toobuild приложений .NET, совместно отдел гарантии hello
  * `myregistry.azrecr.io/warrantydept/customersubmissions/web`представляет веб-изображения, сгруппированных в приложение отправок hello клиента, принадлежащих отдел гарантии hello

* **Образ.** Это моментальный снимок контейнера Docker с доступом только для чтения, который хранится в репозитории. Реестры контейнеров Azure могут содержать образы Windows и Linux. Имена образов нужно указывать для всех развертываний контейнеров. Стандартные [команды Docker](https://docs.docker.com/engine/reference/commandline/) toopush изображений в хранилище или запросу изображения из репозитория.

* **Контейнер.** Контейнер определяет программное приложение и его зависимости, содержащиеся в полной файловой системе, которая включает в себя код, среду выполнения, служебные программы и библиотеки. Запустите контейнеры Docker на основе образов Windows или Linux, извлеченных из реестра контейнеров. Контейнерами на одном компьютере совместно используют hello ядра операционной системы. Контейнеры docker — полностью переносимые tooall основных дистрибутивы Linux, Mac и Windows.




## <a name="next-steps"></a>Дальнейшие действия
* [Создание контейнера реестра, с помощью портала Azure hello](container-registry-get-started-portal.md)
* [Создание контейнера реестра, с помощью hello Azure CLI](container-registry-get-started-azure-cli.md)
* [Принудительная первый образ с помощью hello Docker CLI](container-registry-get-started-docker-cli.md)
* toobuild непрерывной интеграции и рабочий процесс развертывания с помощью Visual Studio Team Services, службы контейнера Azure и Azure контейнер реестра, в разделе [этого учебника](../container-service/dcos-swarm/container-service-docker-swarm-setup-ci-cd.md).
* Если tooset собственные Docker частного реестра в Azure (без общедоступной конечной точки), см. [развертывание свой собственный закрытый Docker реестра в Azure](../virtual-machines/virtual-machines-linux-docker-registry-in-blob-storage.md).
