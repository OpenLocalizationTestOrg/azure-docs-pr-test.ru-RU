---
title: "aaaUsing hello Azure CLI в Windows | Документы Microsoft"
description: "С помощью Azure CLI hello в Windows"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 02/14/2017
ms.author: nepeters
ms.openlocfilehash: edca4a2701a7dfc0fc54df5649e8a5e7afc95490
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-cli-on-windows"></a>С помощью Azure CLI hello в Windows

Hello Azure интерфейс командной строки (CLI) предоставляет командной строки и среда сценариев для создания и управления ресурсами Azure. Hello Azure CLI доступна для операционных систем Windows, Linux и macOS. В этих операционных систем команды CLI hello идентичны, однако сценариев синтаксиса операционной системы может отличаться.

Этот документ сведения hello что образом hello Azure CLI могут устанавливаться и работать на Windows и сведения о синтаксических рекомендации для каждого. Подробную документацию по Azure CLI см. [здесь]( https://docs.microsoft.com/en-us/cli/azure/overview).

## <a name="windows-subsystem-for-linux"></a>Подсистема Windows для Linux

Hello подсистемы Windows для Linux (WSL) предоставляет среду Ubuntu Linux на годовщины Windows 10 и более поздней версии. Включив подсистему Windows для Linux, вы можете воспользоваться Bash для создания и выполнения сценариев Azure CLI. Благодаря этой возможности сценарии Azure CLI можно использовать в macOS, Linux и Windows, не изменяя их.

toouse hello Azure CLI в WSL, выполните следующие hello.

|Задача | Указания |
|---|---|
| Включение подсистемы Windows для Linux | [Документация по установке подсистемы Windows для Linux](https://msdn.microsoft.com/en-us/commandline/wsl/install_guide) |
| Установка hello Azure CLI |[Установите на WSL/Ubuntu 14.04 hello CLI](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2#ubuntu)|

## <a name="powershell"></a>PowerShell

Hello Azure CLI могут выполняться в собственном коде в Windows. В этой конфигурации hello Azure CLI пакет установлен в операционной системе Windows hello и команды, которые могут быть запущены из PowerShell. В такой конфигурации команды и скрипты Azure CLI можно выполнять в любой поддерживаемой версии Windows, но для этого потребуется синтаксис скрипта для конкретной платформы. Поэтому сценарии не обязательно совместно использовать в macOS, Linux и Windows, не изменяя их.

toouse hello Azure CLI в Windows, установите пакет hello, с помощью следующей процедуры [hello установить CLI в Windows](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2#windows).

## <a name="docker-image"></a>Образ Docker

При использовании Docker для Windows, образ Docker можно запустить, включающий hello Azure CLI. Этот образ создан на основе Linux и позволяет работать с Bash.  При использовании Docker для Windows и hello Azure CLI изображения, toobe сценарии общим macOS, Linux и Windows. 

toouse hello Azure CLI в Docker для Windows, убедитесь, что Docker для Windows работает и запустите следующую команду hello.

```bash
docker run -it azuresdk/azure-cli-python:latest bash
```

После завершения с помощью средств Azure CLI hello предварительно Bash, то есть начала сеанса.

## <a name="next-steps"></a>Дальнейшие действия

[Примеры сценариев интерфейса командной строки для виртуальных машин Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[Примеры сценариев интерфейса командной строки для веб-приложений Azure](../../app-service-web/app-service-cli-samples.md)

[Примеры сценариев интерфейса командной строки для SQL Azure](../../sql-database/sql-database-cli-samples.md)
