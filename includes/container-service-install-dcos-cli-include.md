---
title: "hello aaaInstall CLI DC/OS | Документы Microsoft"
description: "Установка контроллера домена/OS CLI hello."
services: container-service
documentationcenter: 
author: rgardler
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Контейнеры, микрослужбы, DC/OS, Azure"
ms.service: container-service
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/10/2016
ms.author: rogardle
ms.openlocfilehash: b077c05beff9a5638486ea5efe9df31089e32701
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
> [!NOTE]
> Это необходимо для работы с кластерами ACS на основе контроллеров домена или ОС. Нет нет необходимости toodo это для кластеров под управлением группу мелких объектов ACS.
> 
> 

Во-первых, [подключения кластера tooyour ACS на основе контроллера домена или ОС](../articles/container-service/container-service-connect.md). Сделав это, можно установить на клиентском компьютере с приведенную ниже команду hello hello CLI DC/OS:

```bash
sudo pip install virtualenv
mkdir dcos && cd dcos
wget https://raw.githubusercontent.com/mesosphere/dcos-cli/master/bin/install/install-optout-dcos-cli.sh
chmod +x install-optout-dcos-cli.sh
./install-optout-dcos-cli.sh . http://localhost --add-path yes
```

Если вы используете старую версию Python, можно заметить предупреждения о незащищенной платформе (InsecurePlatformWarnings). Эти предупреждения можно игнорировать.

В порядке tooget работы без перезапуска оболочка выполните следующую команду:

```bash
source ~/.bashrc
```

Этот шаг не нужно выполнять при запуске новой оболочки.

Теперь можно проверить, hello установлен CLI:

```bash
dcos --help
```