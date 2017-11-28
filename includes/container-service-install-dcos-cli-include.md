---
title: "Установка интерфейса командной строки контроллера домена или ОС | Документация Майкрософт"
description: "Установка интерфейса командной строки контроллера домена или ОС."
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
ms.openlocfilehash: a8ea47f158c0d666340815d2e039995c7483257f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
> [!NOTE]
> <span data-ttu-id="c21bf-104">Это необходимо для работы с кластерами ACS на основе контроллеров домена или ОС.</span><span class="sxs-lookup"><span data-stu-id="c21bf-104">This is for working with DC/OS-based ACS clusters.</span></span> <span data-ttu-id="c21bf-105">Это не требуется для кластеров ACS под управлением Swarm.</span><span class="sxs-lookup"><span data-stu-id="c21bf-105">There is no need to do this for Swarm-based ACS clusters.</span></span>
> 
> 

<span data-ttu-id="c21bf-106">Сначала [подключитесь к кластеру ACS на основе контроллеров домена или ОС](../articles/container-service/container-service-connect.md).</span><span class="sxs-lookup"><span data-stu-id="c21bf-106">First, [connect to your DC/OS-based ACS cluster](../articles/container-service/container-service-connect.md).</span></span> <span data-ttu-id="c21bf-107">Теперь вы можете установить интерфейс командной строки контроллера домена или операционной системы на клиентский компьютер с помощью приведенной ниже команды:</span><span class="sxs-lookup"><span data-stu-id="c21bf-107">Once you have done this, you can install the DC/OS CLI on your client machine with the commands below:</span></span>

```bash
sudo pip install virtualenv
mkdir dcos && cd dcos
wget https://raw.githubusercontent.com/mesosphere/dcos-cli/master/bin/install/install-optout-dcos-cli.sh
chmod +x install-optout-dcos-cli.sh
./install-optout-dcos-cli.sh . http://localhost --add-path yes
```

<span data-ttu-id="c21bf-108">Если вы используете старую версию Python, можно заметить предупреждения о незащищенной платформе (InsecurePlatformWarnings).</span><span class="sxs-lookup"><span data-stu-id="c21bf-108">If you are using an old version of Python, you may notice some "InsecurePlatformWarnings".</span></span> <span data-ttu-id="c21bf-109">Эти предупреждения можно игнорировать.</span><span class="sxs-lookup"><span data-stu-id="c21bf-109">You can safely ignore these.</span></span>

<span data-ttu-id="c21bf-110">Чтобы приступить к работе без перезагрузки оболочки, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="c21bf-110">In order to get started without restarting your shell, run:</span></span>

```bash
source ~/.bashrc
```

<span data-ttu-id="c21bf-111">Этот шаг не нужно выполнять при запуске новой оболочки.</span><span class="sxs-lookup"><span data-stu-id="c21bf-111">This step will not be necessary when you start new shells.</span></span>

<span data-ttu-id="c21bf-112">Теперь можно проверить, установлен ли интерфейс командной строки:</span><span class="sxs-lookup"><span data-stu-id="c21bf-112">Now you can confirm that the CLI is installed:</span></span>

```bash
dcos --help
```