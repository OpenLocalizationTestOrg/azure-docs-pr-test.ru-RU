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
# <a name="configure-a-docker-host-with-virtualbox"></a>Настройка узла Docker с помощью VirtualBox
## <a name="overview"></a>Обзор
В этой статье приводятся инструкции по настройке экземпляра Docker по умолчанию с помощью машины Docker и VirtualBox. Если вы используете hello [бета-версии Docker для Windows](http://beta.docker.com/), эта конфигурация не требуется.

## <a name="prerequisites"></a>Предварительные требования
Hello следующие средства необходимо установить toobe.

* [Docker Toolbox](https://www.docker.com/products/overview#/docker_toolbox)

## <a name="configuring-hello-docker-client-with-windows-powershell"></a>Настройка клиента hello Docker с помощью Windows PowerShell
tooconfigure клиента Docker, просто откройте Windows PowerShell и выполните следующие шаги hello.

1. Создайте экземпляр узла Docker по умолчанию.
   
    ```PowerShell
    docker-machine create --driver virtualbox default
    ```
2. Убедитесь, что экземпляр по умолчанию hello настроена и запущена. (Должен быть запущен экземпляр с именем default.
   
    ```PowerShell
    docker-machine ls 
    ```
   
    ![Вывод: docker-machine ls][0]
3. По умолчанию как hello текущего узла и настройте оболочка.
   
    ```PowerShell
    docker-machine env default | Invoke-Expression
    ```
4. Отображение активных контейнеров Docker hello. Список Hello должно быть пустым.
   
    ```PowerShell
    docker ps
    ```
   
    ![Вывод: docker ps][1]

> [!NOTE]
> Каждый раз при перезагрузке компьютера разработки необходимо toorestart узла локального docker.
> toodo hello, проблема, следующую команду в командной строке: `docker-machine start default`.
> 
> 

[0]: ./media/vs-azure-tools-docker-setup/docker-machine-ls.png
[1]: ./media/vs-azure-tools-docker-setup/docker-ps.png
