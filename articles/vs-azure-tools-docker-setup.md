---
title: "Узел Docker с VirtualBox aaaConfigure | Документы Microsoft"
description: "Значение по умолчанию Docker экземпляра с помощью машины Docker и VirtualBox tooconfigure пошаговые инструкции"
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
ms.openlocfilehash: 1df2da4482444a803d05e413e019edcc57269062
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-docker-host-with-virtualbox"></a><span data-ttu-id="48151-103">Настройка узла Docker с помощью VirtualBox</span><span class="sxs-lookup"><span data-stu-id="48151-103">Configure a Docker Host with VirtualBox</span></span>
## <a name="overview"></a><span data-ttu-id="48151-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="48151-104">Overview</span></span>
<span data-ttu-id="48151-105">В этой статье приводятся инструкции по настройке экземпляра Docker по умолчанию с помощью машины Docker и VirtualBox.</span><span class="sxs-lookup"><span data-stu-id="48151-105">This article guides you through configuring a default Docker instance using Docker Machine and VirtualBox.</span></span> <span data-ttu-id="48151-106">Если вы используете hello [бета-версии Docker для Windows](http://beta.docker.com/), эта конфигурация не требуется.</span><span class="sxs-lookup"><span data-stu-id="48151-106">If you’re using hello [Docker for Windows beta](http://beta.docker.com/), this configuration is not necessary.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="48151-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="48151-107">Prerequisites</span></span>
<span data-ttu-id="48151-108">Hello следующие средства необходимо установить toobe.</span><span class="sxs-lookup"><span data-stu-id="48151-108">hello following tools need toobe installed.</span></span>

* [<span data-ttu-id="48151-109">Docker Toolbox</span><span class="sxs-lookup"><span data-stu-id="48151-109">Docker Toolbox</span></span>](https://www.docker.com/products/overview#/docker_toolbox)

## <a name="configuring-hello-docker-client-with-windows-powershell"></a><span data-ttu-id="48151-110">Настройка клиента hello Docker с помощью Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="48151-110">Configuring hello Docker client with Windows PowerShell</span></span>
<span data-ttu-id="48151-111">tooconfigure клиента Docker, просто откройте Windows PowerShell и выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="48151-111">tooconfigure a Docker client, simply open Windows PowerShell, and perform hello following steps:</span></span>

1. <span data-ttu-id="48151-112">Создайте экземпляр узла Docker по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="48151-112">Create a default docker host instance.</span></span>
   
    ```PowerShell
    docker-machine create --driver virtualbox default
    ```
2. <span data-ttu-id="48151-113">Убедитесь, что экземпляр по умолчанию hello настроена и запущена.</span><span class="sxs-lookup"><span data-stu-id="48151-113">Verify hello default instance is configured and running.</span></span> <span data-ttu-id="48151-114">(Должен быть запущен экземпляр с именем default.</span><span class="sxs-lookup"><span data-stu-id="48151-114">(You should see an instance named \`default' running.</span></span>
   
    ```PowerShell
    docker-machine ls 
    ```
   
    ![Вывод: docker-machine ls][0]
3. <span data-ttu-id="48151-116">По умолчанию как hello текущего узла и настройте оболочка.</span><span class="sxs-lookup"><span data-stu-id="48151-116">Set default as hello current host, and configure your shell.</span></span>
   
    ```PowerShell
    docker-machine env default | Invoke-Expression
    ```
4. <span data-ttu-id="48151-117">Отображение активных контейнеров Docker hello.</span><span class="sxs-lookup"><span data-stu-id="48151-117">Display hello active Docker containers.</span></span> <span data-ttu-id="48151-118">Список Hello должно быть пустым.</span><span class="sxs-lookup"><span data-stu-id="48151-118">hello list should be empty.</span></span>
   
    ```PowerShell
    docker ps
    ```
   
    ![Вывод: docker ps][1]

> [!NOTE]
> <span data-ttu-id="48151-120">Каждый раз при перезагрузке компьютера разработки необходимо toorestart узла локального docker.</span><span class="sxs-lookup"><span data-stu-id="48151-120">Each time you reboot your development machine, you’ll need toorestart your local docker host.</span></span>
> <span data-ttu-id="48151-121">toodo hello, проблема, следующую команду в командной строке: `docker-machine start default`.</span><span class="sxs-lookup"><span data-stu-id="48151-121">toodo this, issue hello following command at a command prompt: `docker-machine start default`.</span></span>
> 
> 

[0]: ./media/vs-azure-tools-docker-setup/docker-machine-ls.png
[1]: ./media/vs-azure-tools-docker-setup/docker-ps.png
