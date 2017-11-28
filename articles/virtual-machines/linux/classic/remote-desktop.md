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
# <a name="using-remote-desktop-tooconnect-tooa-microsoft-azure-linux-vm"></a><span data-ttu-id="50dcb-103">С помощью удаленного рабочего стола tooconnect tooa виртуальной Машине Microsoft Azure Linux</span><span class="sxs-lookup"><span data-stu-id="50dcb-103">Using Remote Desktop tooconnect tooa Microsoft Azure Linux VM</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="50dcb-104">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="50dcb-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="50dcb-105">В этой статье описан с помощью hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="50dcb-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="50dcb-106">Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="50dcb-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="50dcb-107">Hello обновленную версию диспетчера ресурсов в этой статье, см. в разделе [здесь](../use-remote-desktop.md).</span><span class="sxs-lookup"><span data-stu-id="50dcb-107">For hello updated Resource Manager version of this article, see [here](../use-remote-desktop.md).</span></span>

## <a name="overview"></a><span data-ttu-id="50dcb-108">Обзор</span><span class="sxs-lookup"><span data-stu-id="50dcb-108">Overview</span></span>
<span data-ttu-id="50dcb-109">RDP (протокол удаленного рабочего стола) — это защищаемый протокол, используемый для Windows.</span><span class="sxs-lookup"><span data-stu-id="50dcb-109">RDP (Remote Desktop Protocol) is a proprietary protocol used for Windows.</span></span> <span data-ttu-id="50dcb-110">Как можно использовать tooa tooconnect протокола удаленного рабочего СТОЛА виртуальной Машины с Linux (виртуальная машина) удаленно?</span><span class="sxs-lookup"><span data-stu-id="50dcb-110">How can we use RDP tooconnect tooa Linux VM (virtual machine) remotely?</span></span>

<span data-ttu-id="50dcb-111">В этом руководстве выдаст ответ hello!</span><span class="sxs-lookup"><span data-stu-id="50dcb-111">This guidance will give you hello answer!</span></span> <span data-ttu-id="50dcb-112">Это поможет определить xrdp tooinstall и конфигурации на ВМ Microsoft Azure Linux, позволяющее подключиться tooit удаленного рабочего стола с помощью компьютера Windows.</span><span class="sxs-lookup"><span data-stu-id="50dcb-112">It will help you tooinstall and config xrdp on your Microsoft Azure Linux VM, which lets you connect tooit with Remote Desktop from a Windows machine.</span></span> <span data-ttu-id="50dcb-113">Мы будем использовать Виртуальным машинам Ubuntu или OpenSUSE в качестве примера hello в этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="50dcb-113">We will use Linux VM running Ubuntu or OpenSUSE as hello example in this guidance.</span></span>

<span data-ttu-id="50dcb-114">Hello xrdp оно с открытым исходным кодом сервера RDP, который позволяет вам tooconnect сервера Linux с помощью удаленного рабочего стола с компьютера Windows.</span><span class="sxs-lookup"><span data-stu-id="50dcb-114">hello xrdp tool is an open source RDP server that allows you tooconnect your Linux server with Remote Desktop from a Windows machine.</span></span> <span data-ttu-id="50dcb-115">Производительность сервера RDP лучше, чем производительность VNC (Virtual Network Computing).</span><span class="sxs-lookup"><span data-stu-id="50dcb-115">RDP has better performance than VNC (Virtual Network Computing).</span></span> <span data-ttu-id="50dcb-116">VNC выполняет подготовку с помощью графики в качестве JPEG, и это занимает некоторое время, тогда как RDP работает быстро и без проблем.</span><span class="sxs-lookup"><span data-stu-id="50dcb-116">VNC renders using JPEG-quality graphics and can be slow, whereas RDP is fast and crystal clear.</span></span>

> [!NOTE]
> <span data-ttu-id="50dcb-117">Вам необходима виртуальная машина Microsoft Azure под управлением Linux.</span><span class="sxs-lookup"><span data-stu-id="50dcb-117">You must already have an Microsoft Azure VM running Linux.</span></span> <span data-ttu-id="50dcb-118">toocreate и настройка виртуальной Машины Linux, см. раздел hello [виртуальной Машине Linux Azure учебника](createportal.md).</span><span class="sxs-lookup"><span data-stu-id="50dcb-118">toocreate and set up a Linux VM, see hello [Azure Linux VM tutorial](createportal.md).</span></span>
> 
> 

## <a name="create-an-endpoint-for-remote-desktop"></a><span data-ttu-id="50dcb-119">Создание конечной точки для удаленного рабочего стола</span><span class="sxs-lookup"><span data-stu-id="50dcb-119">Create an endpoint for Remote Desktop</span></span>
<span data-ttu-id="50dcb-120">Мы будем использовать конечную точку по умолчанию hello 3389 для удаленного рабочего стола в документе. Настройка 3389 конечную точку в качестве `Remote Desktop` tooyour виртуальных Машин Linux, аналогичные показанным ниже:</span><span class="sxs-lookup"><span data-stu-id="50dcb-120">We will use hello default endpoint 3389 for Remote Desktop in this doc. Set up 3389 endpoint as `Remote Desktop` tooyour Linux VM like below:</span></span>

![изображение](./media/remote-desktop/endpoint-for-linux-server.png)

<span data-ttu-id="50dcb-122">Если вы не знаете, как tooset доступ к конечной точке для виртуальной Машины, в разделе [в этом руководстве](setup-endpoints.md).</span><span class="sxs-lookup"><span data-stu-id="50dcb-122">If you don't know how tooset up an endpoint for your VM, see [this guidance](setup-endpoints.md).</span></span>

## <a name="install-gnome-desktop"></a><span data-ttu-id="50dcb-123">Установка Gnome Desktop</span><span class="sxs-lookup"><span data-stu-id="50dcb-123">Install Gnome Desktop</span></span>
<span data-ttu-id="50dcb-124">Подключение виртуальных Машин Linux tooyour через `putty`и установить `Gnome Desktop`.</span><span class="sxs-lookup"><span data-stu-id="50dcb-124">Connect tooyour Linux VM through `putty`, and install `Gnome Desktop`.</span></span>

<span data-ttu-id="50dcb-125">Для Ubuntu используйте:</span><span class="sxs-lookup"><span data-stu-id="50dcb-125">For Ubuntu, use:</span></span>

    #sudo apt-get update
    #sudo apt-get install ubuntu-desktop


<span data-ttu-id="50dcb-126">Для OpenSUSE используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="50dcb-126">For OpenSUSE, use:</span></span>

    #sudo zypper install gnome-session

## <a name="install-xrdp"></a><span data-ttu-id="50dcb-127">Установка xrdp</span><span class="sxs-lookup"><span data-stu-id="50dcb-127">Install xrdp</span></span>
<span data-ttu-id="50dcb-128">Для Ubuntu используйте:</span><span class="sxs-lookup"><span data-stu-id="50dcb-128">For Ubuntu, use:</span></span>

    #sudo apt-get install xrdp

<span data-ttu-id="50dcb-129">Для OpenSUSE используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="50dcb-129">For OpenSUSE, use:</span></span>

> [!NOTE]
> <span data-ttu-id="50dcb-130">Обновите версию OpenSUSE hello hello версии, которую вы используете в hello следующую команду.</span><span class="sxs-lookup"><span data-stu-id="50dcb-130">Update hello OpenSUSE version with hello version you are using in hello following command.</span></span> <span data-ttu-id="50dcb-131">Hello ниже приведен пример для `OpenSUSE 13.2`.</span><span class="sxs-lookup"><span data-stu-id="50dcb-131">hello example below is for `OpenSUSE 13.2`.</span></span>
> 
> 

    #sudo zypper in http://download.opensuse.org/repositories/X11:/RemoteDesktop/openSUSE_13.2/x86_64/xrdp-0.9.0git.1401423964-2.1.x86_64.rpm
    #sudo zypper install tigervnc xorg-x11-Xvnc xterm remmina-plugin-vnc


## <a name="start-xrdp-and-set-xdrp-service-at-boot-up"></a><span data-ttu-id="50dcb-132">Запуск xrdp и настройка запуска xdrp при загрузке системы</span><span class="sxs-lookup"><span data-stu-id="50dcb-132">Start xrdp and set xdrp service at boot-up</span></span>
<span data-ttu-id="50dcb-133">Для OpenSUSE используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="50dcb-133">For OpenSUSE, use:</span></span>

    #sudo systemctl start xrdp
    #sudo systemctl enable xrdp

<span data-ttu-id="50dcb-134">В Ubuntu после установки управляющей программы xrdp она автоматически запустится и включится при загрузке системы.</span><span class="sxs-lookup"><span data-stu-id="50dcb-134">For Ubuntu, xrdp will be started and eanbled at boot-up automatically after installation.</span></span>

## <a name="using-xfce-if-you-are-using-an-ubuntu-version-later-than-ubuntu-1204lts"></a><span data-ttu-id="50dcb-135">Использование xfce при работе с версией Ubuntu, выпущенной после Ubuntu 12.04LTS</span><span class="sxs-lookup"><span data-stu-id="50dcb-135">Using xfce if you are using an Ubuntu version later than Ubuntu 12.04LTS</span></span>
<span data-ttu-id="50dcb-136">Поскольку текущая версия xrdp hello не поддерживает Gnome рабочего стола для Ubuntu версии позже, чем Ubuntu 12.04LTS, мы будем использовать `xfce` рабочего стола вместо него.</span><span class="sxs-lookup"><span data-stu-id="50dcb-136">Because hello current version of xrdp does not support Gnome Desktop for  Ubuntu versions later than Ubuntu 12.04LTS, we will use `xfce` Desktop instead.</span></span>

<span data-ttu-id="50dcb-137">tooinstall `xfce`, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="50dcb-137">tooinstall `xfce`, use this command:</span></span>

    #sudo apt-get install xubuntu-desktop

<span data-ttu-id="50dcb-138">Затем включите `xfce` с помощью команды:</span><span class="sxs-lookup"><span data-stu-id="50dcb-138">Then enable `xfce` using this command:</span></span>

    #echo xfce4-session >~/.xsession

<span data-ttu-id="50dcb-139">Измените файл конфигурации hello `/etc/xrdp/startwm.sh`:</span><span class="sxs-lookup"><span data-stu-id="50dcb-139">Edit hello config file `/etc/xrdp/startwm.sh`:</span></span>

    #sudo vi /etc/xrdp/startwm.sh   

<span data-ttu-id="50dcb-140">Добавьте строку hello `xfce4-session` перед строкой hello `/etc/X11/Xsession`.</span><span class="sxs-lookup"><span data-stu-id="50dcb-140">Add hello line `xfce4-session` before hello line `/etc/X11/Xsession`.</span></span>

<span data-ttu-id="50dcb-141">toorestart Здравствуйте xrdp службы, этот метод следует использовать:</span><span class="sxs-lookup"><span data-stu-id="50dcb-141">toorestart hello xrdp service, use this:</span></span>

    #sudo service xrdp restart


## <a name="connect-your-linux-vm-from-a-windows-machine"></a><span data-ttu-id="50dcb-142">Подключение к виртуальной машине на базе Linux с компьютера Windows</span><span class="sxs-lookup"><span data-stu-id="50dcb-142">Connect your Linux VM from a Windows machine</span></span>
<span data-ttu-id="50dcb-143">В компьютере с ОС Windows запустите клиент удаленного рабочего стола hello и введите свое имя DNS виртуальной Машины Linux.</span><span class="sxs-lookup"><span data-stu-id="50dcb-143">In a Windows machine, start hello Remote Desktop client and input your Linux VM DNS name.</span></span> <span data-ttu-id="50dcb-144">Или перейдите toohello панели мониторинга виртуальной машины в hello портал Azure и нажмите кнопку `Connect` tooconnect ВМ Linux.</span><span class="sxs-lookup"><span data-stu-id="50dcb-144">Or go toohello Dashboard of your VM in hello Azure portal and click `Connect` tooconnect your Linux VM.</span></span> <span data-ttu-id="50dcb-145">В этом случае появится окно входа hello:</span><span class="sxs-lookup"><span data-stu-id="50dcb-145">In that case, you see hello login window:</span></span>

![изображение](./media/remote-desktop/no2.png)

<span data-ttu-id="50dcb-147">Войдите в систему hello имя пользователя и пароль вашей виртуальной машины Linux.</span><span class="sxs-lookup"><span data-stu-id="50dcb-147">Log in with hello user name and password of your Linux VM.</span></span>

## <a name="next-steps"></a><span data-ttu-id="50dcb-148">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="50dcb-148">Next steps</span></span>
<span data-ttu-id="50dcb-149">Дополнительные сведения об использовании xrdp см. здесь: [http://www.xrdp.org/](http://www.xrdp.org/).</span><span class="sxs-lookup"><span data-stu-id="50dcb-149">For more information about using xrdp, see [http://www.xrdp.org/](http://www.xrdp.org/).</span></span>
