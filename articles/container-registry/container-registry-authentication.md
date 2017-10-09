---
title: "aaaAuthenticate с реестром контейнер Azure | Документы Microsoft"
description: "Как toolog в реестре tooan контейнер Azure, Azure Active Directory с помощью службы учетную запись администратора или участника"
services: container-registry
documentationcenter: 
author: stevelas
manager: balans
editor: cristyg
tags: 
keywords: 
ms.assetid: 128a937a-766a-415b-b9fc-35a6c2f27417
ms.service: container-registry
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2017
ms.author: stevelas
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a0b0462e8432b2567689debca322e2426baa7fa2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-with-a-private-docker-container-registry"></a>Аутентификация с помощью частного реестра контейнеров Docker
toowork с образы контейнеров в контейнер Azure реестра вы вошли с использованием hello `docker login` команды. Вы можете войти, используя **[субъект-службу Azure Active Directory](../active-directory/active-directory-application-objects.md)** или специальную **учетную запись администратора**. В этой статье содержатся подробные сведения об этих удостоверениях.



## <a name="service-principal"></a>Субъект-служба

Вы можете [назначить участника службы](container-registry-get-started-azure-cli.md#assign-a-service-principal) tooyour реестра и использовать его для обычной проверки подлинности Docker. Мы рекомендуем использовать субъект-службу в большинстве сценариев. Укажите идентификатор приложения hello и пароль toohello основной службы hello `docker login` команды, как показано в следующий пример hello:

```
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

После входа Docker кэширует hello учетные данные, вам требуется идентификатор tooremember hello приложений.

> [!TIP]
> Если требуется, можно создать повторно hello пароль субъекта-службы, выполнив hello `az ad sp reset-credentials` команды.
>


Разрешить участников службы [доступа на основе ролей](../active-directory/role-based-access-control-configure.md) tooa реестра. Доступные роли:
  * Читатель (доступ только для получения).
  * Участник (получение и отправка).
  * Владелец (запросу, отправку и назначить роли tooother пользователей).

Анонимный доступ к реестрам контейнеров Azure невозможен. Для общедоступных образов можно использовать [концентратор Docker](https://docs.docker.com/docker-hub/).

Можно назначить несколько участников службы реестра tooa, позволяющий получить доступ toodefine для различных пользователей или приложений. Также можно включить субъекты-службы реестра tooa «без монитора» подключение в разработчик или DevOps сценариев, таких как hello следующие примеры:

  * Развертывания контейнера из систем tooorchestration реестра, включая DC/OS, помощью Docker Swarm и Kubernetes. Можно также извлечь контейнера реестры toorelated служб Azure например [контейнера службы](../container-service/index.yml), [службы приложений](../app-service/index.md), [пакета](../batch/index.md), [Service Fabric](/azure/service-fabric/)и др.

  * Непрерывной интеграции и развертывания решений (например, Visual Studio Team Services или Jenkins), создающие образов контейнеров и отправить их tooa реестра.





## <a name="admin-account"></a>Учетная запись администратора
При создании реестра вместе с ним автоматически создается учетная запись администратора. По умолчанию hello учетная запись отключена, но вы можете включить его и управлять hello учетные данные, например с помощью hello [портала](container-registry-get-started-portal.md#manage-registry-settings) или с помощью hello [команды Azure CLI 2.0](container-registry-get-started-azure-cli.md#manage-admin-credentials). Каждой учетной записи администратора предоставляются два пароля, каждый из которых можно создать повторно. два пароля Hello разрешить реестра toohello toomaintain подключения с помощью один пароль при повторном создании hello другим паролем. Если включена учетная запись hello, можно передать имя пользователя hello и либо пароль toohello `docker login` для обычной проверки подлинности toohello реестра. Например:

```
docker login myregistry.azurecr.io -u myAdminName -p myPassword1
```

> [!IMPORTANT]
> Учетная запись администратора Hello предназначен для реестра hello tooaccess одного пользователя, главным образом для целей тестирования. Не рекомендуется учетных данных администратора hello tooshare среди других пользователей. Все пользователи отображаются в виде файла реестра toohello одного пользователя. Отключает доступ к реестру для всех пользователей, которые используют учетные данные hello, изменения или отключения этой учетной записи.
>


### <a name="next-steps"></a>Дальнейшие действия
* [Принудительная первый образ с помощью Docker CLI hello](container-registry-get-started-docker-cli.md).
* Дополнительные сведения о проверке подлинности в режиме предварительного просмотра hello реестре контейнеров см. в разделе hello [блога](https://blogs.msdn.microsoft.com/stevelasker/2016/11/17/azure-container-registry-user-accounts/).
