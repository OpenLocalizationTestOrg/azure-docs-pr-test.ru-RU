---
title: "Системная tooa aaaRemote виртуальных Машин Linux | Документы Microsoft"
description: "Узнайте, как tooinstall и настроить удаленный рабочий стол tooconnect tooa виртуальной Машине Microsoft Azure Linux для hello классической модели развертывания"
services: virtual-machines-linux
documentationcenter: 
author: SuperScottz
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 34348659-ddb7-41da-82d6-b5885859e7e4
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: mingzhan
ms.openlocfilehash: aadd6e87883cf9cacf9d198b680669d594206e61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="using-remote-desktop-tooconnect-tooa-microsoft-azure-linux-vm"></a>С помощью удаленного рабочего стола tooconnect tooa виртуальной Машине Microsoft Azure Linux
> [!IMPORTANT] 
> В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../../../resource-manager-deployment-model.md). В этой статье описан с помощью hello классической модели развертывания. Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов. Hello обновленную версию диспетчера ресурсов в этой статье, см. в разделе [здесь](../use-remote-desktop.md).

## <a name="overview"></a>Обзор
RDP (протокол удаленного рабочего стола) — это защищаемый протокол, используемый для Windows. Как можно использовать tooa tooconnect протокола удаленного рабочего СТОЛА виртуальной Машины с Linux (виртуальная машина) удаленно?

В этом руководстве выдаст ответ hello! Это поможет определить xrdp tooinstall и конфигурации на ВМ Microsoft Azure Linux, позволяющее подключиться tooit удаленного рабочего стола с помощью компьютера Windows. Мы будем использовать Виртуальным машинам Ubuntu или OpenSUSE в качестве примера hello в этом руководстве.

Hello xrdp оно с открытым исходным кодом сервера RDP, который позволяет вам tooconnect сервера Linux с помощью удаленного рабочего стола с компьютера Windows. Производительность сервера RDP лучше, чем производительность VNC (Virtual Network Computing). VNC выполняет подготовку с помощью графики в качестве JPEG, и это занимает некоторое время, тогда как RDP работает быстро и без проблем.

> [!NOTE]
> Вам необходима виртуальная машина Microsoft Azure под управлением Linux. toocreate и настройка виртуальной Машины Linux, см. раздел hello [виртуальной Машине Linux Azure учебника](createportal.md).
> 
> 

## <a name="create-an-endpoint-for-remote-desktop"></a>Создание конечной точки для удаленного рабочего стола
Мы будем использовать конечную точку по умолчанию hello 3389 для удаленного рабочего стола в документе. Настройка 3389 конечную точку в качестве `Remote Desktop` tooyour виртуальных Машин Linux, аналогичные показанным ниже:

![изображение](./media/remote-desktop/endpoint-for-linux-server.png)

Если вы не знаете, как tooset доступ к конечной точке для виртуальной Машины, в разделе [в этом руководстве](setup-endpoints.md).

## <a name="install-gnome-desktop"></a>Установка Gnome Desktop
Подключение виртуальных Машин Linux tooyour через `putty`и установить `Gnome Desktop`.

Для Ubuntu используйте:

    #sudo apt-get update
    #sudo apt-get install ubuntu-desktop


Для OpenSUSE используйте следующую команду:

    #sudo zypper install gnome-session

## <a name="install-xrdp"></a>Установка xrdp
Для Ubuntu используйте:

    #sudo apt-get install xrdp

Для OpenSUSE используйте следующую команду:

> [!NOTE]
> Обновите версию OpenSUSE hello hello версии, которую вы используете в hello следующую команду. Hello ниже приведен пример для `OpenSUSE 13.2`.
> 
> 

    #sudo zypper in http://download.opensuse.org/repositories/X11:/RemoteDesktop/openSUSE_13.2/x86_64/xrdp-0.9.0git.1401423964-2.1.x86_64.rpm
    #sudo zypper install tigervnc xorg-x11-Xvnc xterm remmina-plugin-vnc


## <a name="start-xrdp-and-set-xdrp-service-at-boot-up"></a>Запуск xrdp и настройка запуска xdrp при загрузке системы
Для OpenSUSE используйте следующую команду:

    #sudo systemctl start xrdp
    #sudo systemctl enable xrdp

В Ubuntu после установки управляющей программы xrdp она автоматически запустится и включится при загрузке системы.

## <a name="using-xfce-if-you-are-using-an-ubuntu-version-later-than-ubuntu-1204lts"></a>Использование xfce при работе с версией Ubuntu, выпущенной после Ubuntu 12.04LTS
Поскольку текущая версия xrdp hello не поддерживает Gnome рабочего стола для Ubuntu версии позже, чем Ubuntu 12.04LTS, мы будем использовать `xfce` рабочего стола вместо него.

tooinstall `xfce`, используйте следующую команду:

    #sudo apt-get install xubuntu-desktop

Затем включите `xfce` с помощью команды:

    #echo xfce4-session >~/.xsession

Измените файл конфигурации hello `/etc/xrdp/startwm.sh`:

    #sudo vi /etc/xrdp/startwm.sh   

Добавьте строку hello `xfce4-session` перед строкой hello `/etc/X11/Xsession`.

toorestart Здравствуйте xrdp службы, этот метод следует использовать:

    #sudo service xrdp restart


## <a name="connect-your-linux-vm-from-a-windows-machine"></a>Подключение к виртуальной машине на базе Linux с компьютера Windows
В компьютере с ОС Windows запустите клиент удаленного рабочего стола hello и введите свое имя DNS виртуальной Машины Linux. Или перейдите toohello панели мониторинга виртуальной машины в hello портал Azure и нажмите кнопку `Connect` tooconnect ВМ Linux. В этом случае появится окно входа hello:

![изображение](./media/remote-desktop/no2.png)

Войдите в систему hello имя пользователя и пароль вашей виртуальной машины Linux.

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения об использовании xrdp см. здесь: [http://www.xrdp.org/](http://www.xrdp.org/).
