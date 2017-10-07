---
title: "aaaDeploy ASP.NET Core Linux Docker контейнера tooa удаленному узлу Docker | Документы Microsoft"
description: "Узнайте, как toouse Visual Studio Tools для Docker toodeploy ASP.NET Core веб-контейнера Docker tooa приложения, запущенного на виртуальной Машине Linux Azure узла Docker"
services: azure-container-service
documentationcenter: .net
author: mlearned
manager: douge
editor: 
ms.assetid: e5e81c5e-dd18-4d5a-a24d-a932036e78b9
ms.service: azure-container-service
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/08/2016
ms.author: mlearned
ms.openlocfilehash: 27b0c6420628c73220200bc071b47a4cd89fff58
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-aspnet-container-tooa-remote-docker-host"></a><span data-ttu-id="2fc65-103">Развертывание ASP.NET tooa удаленного Docker узла контейнера</span><span class="sxs-lookup"><span data-stu-id="2fc65-103">Deploy an ASP.NET container tooa remote Docker host</span></span>
## <a name="overview"></a><span data-ttu-id="2fc65-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="2fc65-104">Overview</span></span>
<span data-ttu-id="2fc65-105">Docker — это механизм упрощенный контейнер, аналогично некоторые способы tooa виртуальной машины, которые можно использовать toohost приложений и служб.</span><span class="sxs-lookup"><span data-stu-id="2fc65-105">Docker is a lightweight container engine, similar in some ways tooa virtual machine, which you can use toohost applications and services.</span></span>
<span data-ttu-id="2fc65-106">Этот учебник знакомит с помощью hello [средств Visual Studio для Docker](https://docs.microsoft.com/en-us/dotnet/articles/core/docker/visual-studio-tools-for-docker) toodeploy расширение узла ASP.NET Core приложения tooa Docker в Azure с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2fc65-106">This tutorial walks you through using hello [Visual Studio Tools for Docker](https://docs.microsoft.com/en-us/dotnet/articles/core/docker/visual-studio-tools-for-docker) extension toodeploy an ASP.NET Core app tooa Docker host on Azure using PowerShell.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2fc65-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="2fc65-107">Prerequisites</span></span>
<span data-ttu-id="2fc65-108">следующие Hello является обязательным toocomplete этого учебника:</span><span class="sxs-lookup"><span data-stu-id="2fc65-108">hello following is required toocomplete this tutorial:</span></span>

* <span data-ttu-id="2fc65-109">Создайте узел виртуальной Машины Azure Docker, как описано в [как toouse-машины docker с помощью Azure](virtual-machines/linux/docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="2fc65-109">Create an Azure Docker Host VM as described in [How toouse docker-machine with Azure](virtual-machines/linux/docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>
* <span data-ttu-id="2fc65-110">Установить hello последнюю версию [Visual Studio](https://www.visualstudio.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="2fc65-110">Install hello latest version of [Visual Studio](https://www.visualstudio.com/downloads/)</span></span>
* <span data-ttu-id="2fc65-111">Загрузите hello [пакет SDK для Microsoft ASP.NET Core 1.0](https://go.microsoft.com/fwlink/?LinkID=809122)</span><span class="sxs-lookup"><span data-stu-id="2fc65-111">Download hello [Microsoft ASP.NET Core 1.0 SDK](https://go.microsoft.com/fwlink/?LinkID=809122)</span></span>
* <span data-ttu-id="2fc65-112">Установить [Docker для Windows](https://docs.docker.com/docker-for-windows/install/).</span><span class="sxs-lookup"><span data-stu-id="2fc65-112">Install [Docker for Windows](https://docs.docker.com/docker-for-windows/install/)</span></span>

## <a name="1-create-an-aspnet-core-web-app"></a><span data-ttu-id="2fc65-113">1. Создание веб-приложения ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="2fc65-113">1. Create an ASP.NET Core web app</span></span>
<span data-ttu-id="2fc65-114">Hello следующее пошаговый процесс создания приложений ASP.NET Core basic, который будет использоваться в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="2fc65-114">hello following steps guide you through creating a basic ASP.NET Core app that will be used in this tutorial.</span></span>

[!INCLUDE [create-aspnet5-app](../includes/create-aspnet5-app.md)]

## <a name="2-add-docker-support"></a><span data-ttu-id="2fc65-115">2. Добавление поддержки Docker</span><span class="sxs-lookup"><span data-stu-id="2fc65-115">2. Add Docker support</span></span>
[!INCLUDE [create-aspnet5-app](../includes/vs-azure-tools-docker-add-docker-support.md)]

## <a name="3-use-hello-dockertaskps1-powershell-script"></a><span data-ttu-id="2fc65-116">3. Использовать сценарий PowerShell DockerTask.ps1 hello</span><span class="sxs-lookup"><span data-stu-id="2fc65-116">3. Use hello DockerTask.ps1 PowerShell Script</span></span>
1. <span data-ttu-id="2fc65-117">Откройте PowerShell prompt toohello корневой каталог проекта.</span><span class="sxs-lookup"><span data-stu-id="2fc65-117">Open a PowerShell prompt toohello root directory of your project.</span></span> 
   
   ```
   PS C:\Src\WebApplication1>
   ```
2. <span data-ttu-id="2fc65-118">Проверка выполняется hello удаленного узла.</span><span class="sxs-lookup"><span data-stu-id="2fc65-118">Validate hello remote host is running.</span></span> <span data-ttu-id="2fc65-119">Должно отображаться состояние Running.</span><span class="sxs-lookup"><span data-stu-id="2fc65-119">You should see state = Running</span></span> 
   
   ```
   docker-machine ls
   NAME         ACTIVE   DRIVER   STATE     URL                        SWARM   DOCKER    ERRORS
   MyDockerHost -        azure    Running   tcp://xxx.xxx.xxx.xxx:2376         v1.10.3
   ```
   
3. <span data-ttu-id="2fc65-120">С помощью приложения hello сборки hello - параметра построения</span><span class="sxs-lookup"><span data-stu-id="2fc65-120">Build hello app using hello -Build parameter</span></span>
   
   ```
   PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Build -Environment Release -Machine mydockerhost
   ```  

   > ```
   > PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Build -Environment Release 
   > ```  
   > 
   > 
4. <span data-ttu-id="2fc65-121">Выполните приложение hello, с помощью hello - параметр запуска</span><span class="sxs-lookup"><span data-stu-id="2fc65-121">Run hello app, using hello -Run parameter</span></span>
   
   ```
   PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Run -Environment Release -Machine mydockerhost
   ```
   
   > ```
   > PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Run -Environment Release 
   > ```
   > 
   > 
   
   <span data-ttu-id="2fc65-122">По завершении docker вы увидите примерно toohello следующие результаты:</span><span class="sxs-lookup"><span data-stu-id="2fc65-122">Once docker completes, you should see results similar toohello following:</span></span>
   
   ![Просмотр приложения][3]

[0]:./media/vs-azure-tools-docker-hosting-web-apps-in-docker/docker-props-in-solution-explorer.png
[1]:./media/vs-azure-tools-docker-hosting-web-apps-in-docker/change-docker-machine-name.png
[2]:./media/vs-azure-tools-docker-hosting-web-apps-in-docker/launch-application.png
[3]:./media/vs-azure-tools-docker-hosting-web-apps-in-docker/view-application.png
