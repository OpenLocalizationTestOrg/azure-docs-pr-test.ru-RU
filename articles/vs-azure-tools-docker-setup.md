---
title: "Настройка узла Docker с помощью VirtualBox | Документация Майкрософт"
description: "Пошаговые инструкции по настройке экземпляра Docker по умолчанию с помощью машины Docker и VirtualBox."
services: azure-container-service
documentationcenter: na
author: mlearned
manager: douge
editor: 
ms.assetid: 0b1335a2-7720-42a8-8260-4e06fc00c9f6
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 06/08/2016
ms.author: mlearned
ms.openlocfilehash: e9465afb560a73d74f853c19094b3ee75b8c470c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="configure-a-docker-host-with-virtualbox"></a><span data-ttu-id="d7a3a-103">Настройка узла Docker с помощью VirtualBox</span><span class="sxs-lookup"><span data-stu-id="d7a3a-103">Configure a Docker Host with VirtualBox</span></span>
## <a name="overview"></a><span data-ttu-id="d7a3a-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="d7a3a-104">Overview</span></span>
<span data-ttu-id="d7a3a-105">В этой статье приводятся инструкции по настройке экземпляра Docker по умолчанию с помощью машины Docker и VirtualBox.</span><span class="sxs-lookup"><span data-stu-id="d7a3a-105">This article guides you through configuring a default Docker instance using Docker Machine and VirtualBox.</span></span> <span data-ttu-id="d7a3a-106">При использовании [бета-версии Docker для Windows](http://beta.docker.com/)эта настройка не требуется.</span><span class="sxs-lookup"><span data-stu-id="d7a3a-106">If you’re using the [Docker for Windows beta](http://beta.docker.com/), this configuration is not necessary.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d7a3a-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="d7a3a-107">Prerequisites</span></span>
<span data-ttu-id="d7a3a-108">Должны быть установлены следующие средства.</span><span class="sxs-lookup"><span data-stu-id="d7a3a-108">The following tools need to be installed.</span></span>

* [<span data-ttu-id="d7a3a-109">Docker Toolbox</span><span class="sxs-lookup"><span data-stu-id="d7a3a-109">Docker Toolbox</span></span>](https://www.docker.com/products/overview#/docker_toolbox)

## <a name="configuring-the-docker-client-with-windows-powershell"></a><span data-ttu-id="d7a3a-110">Настройка клиента Docker с помощью Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="d7a3a-110">Configuring the Docker client with Windows PowerShell</span></span>
<span data-ttu-id="d7a3a-111">Чтобы настроить клиент Docker, просто откройте Windows PowerShell и выполните указанные ниже действия:</span><span class="sxs-lookup"><span data-stu-id="d7a3a-111">To configure a Docker client, simply open Windows PowerShell, and perform the following steps:</span></span>

1. <span data-ttu-id="d7a3a-112">Создайте экземпляр узла Docker по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="d7a3a-112">Create a default docker host instance.</span></span>
   
    ```PowerShell
    docker-machine create --driver virtualbox default
    ```
2. <span data-ttu-id="d7a3a-113">Убедитесь в том, что экземпляр по умолчанию настроен и выполняется.</span><span class="sxs-lookup"><span data-stu-id="d7a3a-113">Verify the default instance is configured and running.</span></span> <span data-ttu-id="d7a3a-114">(Должен быть запущен экземпляр с именем default.</span><span class="sxs-lookup"><span data-stu-id="d7a3a-114">(You should see an instance named \`default' running.</span></span>
   
    ```PowerShell
    docker-machine ls 
    ```
   
    ![Вывод: docker-machine ls][0]
3. <span data-ttu-id="d7a3a-116">Задайте экземпляр по умолчанию в качестве текущего узла и настройте оболочку.</span><span class="sxs-lookup"><span data-stu-id="d7a3a-116">Set default as the current host, and configure your shell.</span></span>
   
    ```PowerShell
    docker-machine env default | Invoke-Expression
    ```
4. <span data-ttu-id="d7a3a-117">Отобразите активные контейнеры Docker.</span><span class="sxs-lookup"><span data-stu-id="d7a3a-117">Display the active Docker containers.</span></span> <span data-ttu-id="d7a3a-118">Список должен быть пустым.</span><span class="sxs-lookup"><span data-stu-id="d7a3a-118">The list should be empty.</span></span>
   
    ```PowerShell
    docker ps
    ```
   
    ![Вывод: docker ps][1]

> [!NOTE]
> <span data-ttu-id="d7a3a-120">Каждый раз, когда перезагружается компьютер разработки, необходимо перезапускать локальный узел Docker.</span><span class="sxs-lookup"><span data-stu-id="d7a3a-120">Each time you reboot your development machine, you’ll need to restart your local docker host.</span></span>
> <span data-ttu-id="d7a3a-121">Для этого выполните в командной строке следующую команду: `docker-machine start default`.</span><span class="sxs-lookup"><span data-stu-id="d7a3a-121">To do this, issue the following command at a command prompt: `docker-machine start default`.</span></span>
> 
> 

[0]: ./media/vs-azure-tools-docker-setup/docker-machine-ls.png
[1]: ./media/vs-azure-tools-docker-setup/docker-ps.png
