---
title: "Установка Azure IoT Edge в ОС Windows IoT Базовая | Документация Майкрософт"
description: "Установка среды выполнения Azure IoT Edge на устройстве под управлением ОС Windows IoT Базовая"
services: iot-edge
keywords: 
author: kgremban
manager: timlt
ms.author: kgremban
ms.reviewer: veyalla
ms.date: 12/06/2017
ms.topic: article
ms.service: iot-edge
ms.openlocfilehash: cc34e5cecafe485608ba428395b690ba57f71e9c
ms.sourcegitcommit: 4ac89872f4c86c612a71eb7ec30b755e7df89722
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="install-the-iot-edge-runtime-on-windows-iot-core---preview"></a>Установка среды выполнения Azure IoT Edge в ОС Windows IoT Базовая (предварительная версия)

Azure IoT Edge и [Windows IoT базовая](https://docs.microsoft.com/windows/iot-core/) действуют совместно, чтобы включить edge вычислительные ресурсы даже небольшие устройства. Среда выполнения Azure IoT Edge может работать даже на крошечных одноплатных устройствах (SBC), которые весьма распространены в отрасли Интернета вещей. 

В этой статье мы рассмотрим подготовку среды выполнения на плате разработки [MinnowBoard Turbot][lnk-minnow] под управлением Windows IoT Базовая. Windows IoT базовая поддерживает Azure IoT края только в x64-разрядных процессоров Intel. 

## <a name="install-the-runtime"></a>Установка среды выполнения

1. Установите [панель мониторинга Windows 10 IoT Базовая][lnk-core] на хост-системе.
1. Выполните [инструкции][lnk-board] по настройке образа MinnowBoard Turbot/MAX (сборка 16299) на плате. 
1. Включите устройство и [войдите на него удаленно через PowerShell][lnk-powershell].
1. В консоли PowerShell установите среду выполнения контейнеров. 

   ```powershell
   Invoke-WebRequest https://master.dockerproject.org/windows/x86_64/docker-17.06.0-dev.zip -o temp.zip
   Expand-Archive .\temp.zip $env:ProgramFiles -f
   Remove-Item .\temp.zip
   $env:Path += ";$env:programfiles\docker"
   SETX /M PATH "$env:Path"
   dockerd --register-service
   start-service docker
   ```

   >[!NOTE]
   >Эта среда выполнения контейнеров взята из сервера сборки проекта Moby и предназначена только для ознакомительных целей. Команда Docker не тестировала эту среду, не рекомендует ее и не поддерживает.

1. Установите среду выполнения IoT Edge и проверьте свою конфигурацию.

   ```powershell
   Invoke-Expression (Invoke-WebRequest -useb https://aka.ms/iotedgewin)
   ```

   Этот скрипт обеспечивает следующее: 
   * Python 3.6;
   * скрипт управления IoT Edge (iotedgectl.exe).

В окне удаленной консоли PowerShell могут появиться информационные выходные данные средства iotedgectl.exe, отображаемые зеленым цветом. Это не обязательно свидетельствует об ошибках. 

## <a name="next-steps"></a>Дальнейшие действия

Теперь, когда на устройстве запущена среда выполнения IoT Edge, узнайте, как [развертывать и отслеживать модули IoT Edge в нужном масштабе][lnk-deploy].

<!--Links-->
[lnk-minnow]: https://minnowboard.org/ 
[lnk-core]: https://docs.microsoft.com/windows/iot-core/connect-your-device/iotdashboard
[lnk-board]: https://developer.microsoft.com/windows/iot/Docs/GetStarted/mbm/sdcard/stable/getstartedstep2
[lnk-powershell]: https://docs.microsoft.com/windows/iot-core/connect-your-device/powershell
[lnk-deploy]: how-to-deploy-monitor.md
[lnk-docker-install]: https://docs.docker.com/engine/installation/linux/docker-ce/binaries#install-server-and-client-binaries-on-windows
[lnk-docker-containers]: https://docs.microsoft.com/virtualization/windowscontainers/quick-start/quick-start-windows-10#2-switch-to-windows-containers
