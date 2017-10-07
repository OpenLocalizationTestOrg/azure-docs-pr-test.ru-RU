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
# <a name="deploy-an-aspnet-container-tooa-remote-docker-host"></a>Развертывание ASP.NET tooa удаленного Docker узла контейнера
## <a name="overview"></a>Обзор
Docker — это механизм упрощенный контейнер, аналогично некоторые способы tooa виртуальной машины, которые можно использовать toohost приложений и служб.
Этот учебник знакомит с помощью hello [средств Visual Studio для Docker](https://docs.microsoft.com/en-us/dotnet/articles/core/docker/visual-studio-tools-for-docker) toodeploy расширение узла ASP.NET Core приложения tooa Docker в Azure с помощью PowerShell.

## <a name="prerequisites"></a>Предварительные требования
следующие Hello является обязательным toocomplete этого учебника:

* Создайте узел виртуальной Машины Azure Docker, как описано в [как toouse-машины docker с помощью Azure](virtual-machines/linux/docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* Установить hello последнюю версию [Visual Studio](https://www.visualstudio.com/downloads/)
* Загрузите hello [пакет SDK для Microsoft ASP.NET Core 1.0](https://go.microsoft.com/fwlink/?LinkID=809122)
* Установить [Docker для Windows](https://docs.docker.com/docker-for-windows/install/).

## <a name="1-create-an-aspnet-core-web-app"></a>1. Создание веб-приложения ASP.NET Core
Hello следующее пошаговый процесс создания приложений ASP.NET Core basic, который будет использоваться в этом учебнике.

[!INCLUDE [create-aspnet5-app](../includes/create-aspnet5-app.md)]

## <a name="2-add-docker-support"></a>2. Добавление поддержки Docker
[!INCLUDE [create-aspnet5-app](../includes/vs-azure-tools-docker-add-docker-support.md)]

## <a name="3-use-hello-dockertaskps1-powershell-script"></a>3. Использовать сценарий PowerShell DockerTask.ps1 hello
1. Откройте PowerShell prompt toohello корневой каталог проекта. 
   
   ```
   PS C:\Src\WebApplication1>
   ```
2. Проверка выполняется hello удаленного узла. Должно отображаться состояние Running. 
   
   ```
   docker-machine ls
   NAME         ACTIVE   DRIVER   STATE     URL                        SWARM   DOCKER    ERRORS
   MyDockerHost -        azure    Running   tcp://xxx.xxx.xxx.xxx:2376         v1.10.3
   ```
   
3. С помощью приложения hello сборки hello - параметра построения
   
   ```
   PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Build -Environment Release -Machine mydockerhost
   ```  

   > ```
   > PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Build -Environment Release 
   > ```  
   > 
   > 
4. Выполните приложение hello, с помощью hello - параметр запуска
   
   ```
   PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Run -Environment Release -Machine mydockerhost
   ```
   
   > ```
   > PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Run -Environment Release 
   > ```
   > 
   > 
   
   По завершении docker вы увидите примерно toohello следующие результаты:
   
   ![Просмотр приложения][3]

[0]:./media/vs-azure-tools-docker-hosting-web-apps-in-docker/docker-props-in-solution-explorer.png
[1]:./media/vs-azure-tools-docker-hosting-web-apps-in-docker/change-docker-machine-name.png
[2]:./media/vs-azure-tools-docker-hosting-web-apps-in-docker/launch-application.png
[3]:./media/vs-azure-tools-docker-hosting-web-apps-in-docker/view-application.png
