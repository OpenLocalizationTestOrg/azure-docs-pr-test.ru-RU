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
> <span data-ttu-id="a55d6-104">Это необходимо для работы с кластерами ACS на основе контроллеров домена или ОС.</span><span class="sxs-lookup"><span data-stu-id="a55d6-104">This is for working with DC/OS-based ACS clusters.</span></span> <span data-ttu-id="a55d6-105">Нет нет необходимости toodo это для кластеров под управлением группу мелких объектов ACS.</span><span class="sxs-lookup"><span data-stu-id="a55d6-105">There is no need toodo this for Swarm-based ACS clusters.</span></span>
> 
> 

<span data-ttu-id="a55d6-106">Во-первых, [подключения кластера tooyour ACS на основе контроллера домена или ОС](../articles/container-service/container-service-connect.md).</span><span class="sxs-lookup"><span data-stu-id="a55d6-106">First, [connect tooyour DC/OS-based ACS cluster](../articles/container-service/container-service-connect.md).</span></span> <span data-ttu-id="a55d6-107">Сделав это, можно установить на клиентском компьютере с приведенную ниже команду hello hello CLI DC/OS:</span><span class="sxs-lookup"><span data-stu-id="a55d6-107">Once you have done this, you can install hello DC/OS CLI on your client machine with hello commands below:</span></span>

```bash
sudo pip install virtualenv
mkdir dcos && cd dcos
wget https://raw.githubusercontent.com/mesosphere/dcos-cli/master/bin/install/install-optout-dcos-cli.sh
chmod +x install-optout-dcos-cli.sh
./install-optout-dcos-cli.sh . http://localhost --add-path yes
```

<span data-ttu-id="a55d6-108">Если вы используете старую версию Python, можно заметить предупреждения о незащищенной платформе (InsecurePlatformWarnings).</span><span class="sxs-lookup"><span data-stu-id="a55d6-108">If you are using an old version of Python, you may notice some "InsecurePlatformWarnings".</span></span> <span data-ttu-id="a55d6-109">Эти предупреждения можно игнорировать.</span><span class="sxs-lookup"><span data-stu-id="a55d6-109">You can safely ignore these.</span></span>

<span data-ttu-id="a55d6-110">В порядке tooget работы без перезапуска оболочка выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="a55d6-110">In order tooget started without restarting your shell, run:</span></span>

```bash
source ~/.bashrc
```

<span data-ttu-id="a55d6-111">Этот шаг не нужно выполнять при запуске новой оболочки.</span><span class="sxs-lookup"><span data-stu-id="a55d6-111">This step will not be necessary when you start new shells.</span></span>

<span data-ttu-id="a55d6-112">Теперь можно проверить, hello установлен CLI:</span><span class="sxs-lookup"><span data-stu-id="a55d6-112">Now you can confirm that hello CLI is installed:</span></span>

```bash
dcos --help
```