---
title: "aaaApplication или пользовательские службы Marathon | Документы Microsoft"
description: "Создание службы Marathon с настройками для приложения или пользователя"
services: container-service
documentationcenter: 
author: rgardler
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Контейнеры, Marathon, микрослужбы, DC/OS, Azure"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/12/2016
ms.author: rogardle
ms.custom: mvc
ms.openlocfilehash: 1e6f69ed64e113a3a059788a71ddb57b6d3ad8da
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-or-user-specific-marathon-service"></a>Создание службы Marathon с настройками для приложения или пользователя
Служба контейнеров Azure предоставляет набор главных серверов с предварительно настроенными решениями Apache Mesos и Marathon. Это могут быть используется tooorchestrate приложений на кластере hello, но он является наилучшим образом не toouse hello главных серверов для этой цели. Например, изменение конфигурации hello Marathon требует регистрации в самих серверов master hello и внесения изменений — это поощряет уникальный главных серверов, немного отличаются от стандартных hello и необходимость toobe карточки для и управляемых независимо друг от друга. Кроме того hello конфигурацию, необходимую для одной группы может быть hello оптимальной конфигурации для другой команды.

В этой статье объясняется, как tooadd службу Marathon приложения или конкретного пользователя.

Так как эта служба будет принадлежать tooa одного пользователя или группы, они могут бесплатно tooconfigure его каким-либо образом, что пожелает. Кроме того служба контейнера Azure будет гарантировать, что служба hello сохраняется toorun. Если происходит сбой службы hello, Azure контейнера служба будет перезапущена его автоматически. Большую часть времени hello вы не даже Обратите внимание, что за время простоя.

## <a name="prerequisites"></a>Предварительные требования
[Разверните экземпляр службы Azure контейнера](container-service-deployment.md) с orchestrator введите DC/OS и [убедитесь, что ваш клиент может подключаться кластера tooyour](../container-service-connect.md). Кроме того hello следующие действия.

[!INCLUDE [install hello DC/OS CLI](../../../includes/container-service-install-dcos-cli-include.md)]

## <a name="create-an-application-or-user-specific-marathon-service"></a>Создание службы Marathon с настройками для приложения или пользователя
Начните с создания файла конфигурации JSON, который определяет имя службы приложения hello, что требуется toocreate hello. Здесь мы используем `marathon-alice` как hello имя платформы. Сохраните файл hello наподобие `marathon-alice.json`:

```json
{"marathon": {"framework-name": "marathon-alice" }}
```

Затем выполните hello CLI DC/OS tooinstall hello Marathon экземпляра с параметрами hello, которые заданы в файле конфигурации.

```bash
dcos package install --options=marathon-alice.json marathon
```

Теперь вы увидите вашей `marathon-alice` службе, запущенной на вкладке hello службы контроллера домена/OS пользовательского интерфейса. Hello пользовательского интерфейса будет `http://<hostname>/service/marathon-alice/` Если tooaccess напрямую.

## <a name="set-hello-dcos-cli-tooaccess-hello-service"></a>Настройте tooaccess CLI DC/OS hello hello
Также можно настроить вашей tooaccess CLI DC/OS новой службы, Настройка hello `marathon.url` toohello toopoint свойство `marathon-alice` экземпляра следующим образом:

```bash
dcos config set marathon.url http://<hostname>/service/marathon-alice/
```

Можно проверить, какой экземпляр Marathon, ваш CLI работает с hello `dcos config show` команды. Вы можете восстановить toousing master Marathon службы с помощью команды hello `dcos config unset marathon.url`.

