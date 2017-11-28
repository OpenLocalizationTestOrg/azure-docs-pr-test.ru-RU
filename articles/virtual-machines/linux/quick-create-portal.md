---
title: "Быстрый запуск - aaaAzure создания виртуальной Машины портала | Документы Microsoft"
description: "Краткое руководство по созданию виртуальной машины с помощью портала Azure."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/15/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 984a400c976e349a59f873210d6e04bcdea39e1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-linux-virtual-machine-with-hello-azure-portal"></a><span data-ttu-id="60542-103">Создание виртуальной машины Linux с hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="60542-103">Create a Linux virtual machine with hello Azure portal</span></span>

<span data-ttu-id="60542-104">Виртуальные машины Azure могут создаваться через портал Azure hello.</span><span class="sxs-lookup"><span data-stu-id="60542-104">Azure virtual machines can be created through hello Azure portal.</span></span> <span data-ttu-id="60542-105">В этом случае для создания и настройки виртуальных машин и всех связанных ресурсов Azure используется пользовательский интерфейс на основе браузера.</span><span class="sxs-lookup"><span data-stu-id="60542-105">This method provides a browser-based user interface for creating and configuring virtual machines and all related resources.</span></span> <span data-ttu-id="60542-106">Это краткое руководство пошаговые инструкции для создания виртуальной машины и установка веб-сервере, на hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="60542-106">This Quickstart steps through creating a virtual machine and installing a webserver on hello VM.</span></span>

<span data-ttu-id="60542-107">Если у вас еще нет подписки Azure, [создайте бесплатную учетную запись Azure](https://azure.microsoft.com/free/?WT.mc_id=A261C142F), прежде чем начинать работу.</span><span class="sxs-lookup"><span data-stu-id="60542-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="create-ssh-key-pair"></a><span data-ttu-id="60542-108">Создание пары ключей SSH</span><span class="sxs-lookup"><span data-stu-id="60542-108">Create SSH key pair</span></span>

<span data-ttu-id="60542-109">В этом кратком руководстве вы должны toocomplete пару ключей SSH.</span><span class="sxs-lookup"><span data-stu-id="60542-109">You need an SSH key pair toocomplete this quick start.</span></span> <span data-ttu-id="60542-110">Если у вас уже есть пара ключей SSH, этот шаг можно пропустить.</span><span class="sxs-lookup"><span data-stu-id="60542-110">If you have an existing SSH key pair, this step can be skipped.</span></span>

<span data-ttu-id="60542-111">В оболочке Bash выполните следующую команду и следуйте hello на экране инструкциям.</span><span class="sxs-lookup"><span data-stu-id="60542-111">From a Bash shell, run this command and follow hello on-screen directions.</span></span> <span data-ttu-id="60542-112">выходные данные команды Hello включает имя файла hello hello файла открытого ключа.</span><span class="sxs-lookup"><span data-stu-id="60542-112">hello command output includes hello file name of hello public key file.</span></span> <span data-ttu-id="60542-113">Скопируйте содержимое буфера обмена toohello файла открытого ключа hello hello.</span><span class="sxs-lookup"><span data-stu-id="60542-113">Copy hello contents of hello public key file toohello clipboard.</span></span>

```bash
ssh-keygen -t rsa -b 2048
```

## <a name="log-in-tooazure"></a><span data-ttu-id="60542-114">Войдите в tooAzure</span><span class="sxs-lookup"><span data-stu-id="60542-114">Log in tooAzure</span></span> 

<span data-ttu-id="60542-115">Войдите в систему toohello портал Azure по адресу http://portal.azure.com.</span><span class="sxs-lookup"><span data-stu-id="60542-115">Log in toohello Azure portal at http://portal.azure.com.</span></span>

## <a name="create-virtual-machine"></a><span data-ttu-id="60542-116">Создание виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="60542-116">Create virtual machine</span></span>

1. <span data-ttu-id="60542-117">Нажмите кнопку hello **New** кнопка найдена в верхнем левом углу hello hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="60542-117">Click hello **New** button found on hello upper left-hand corner of hello Azure portal.</span></span>

2. <span data-ttu-id="60542-118">Выберите **Вычисления**, а затем — **Сервер Ubuntu 16.04 LTS**.</span><span class="sxs-lookup"><span data-stu-id="60542-118">Select **Compute**, and then select **Ubuntu Server 16.04 LTS**.</span></span> 

3. <span data-ttu-id="60542-119">Введите сведения о виртуальной машине hello.</span><span class="sxs-lookup"><span data-stu-id="60542-119">Enter hello virtual machine information.</span></span> <span data-ttu-id="60542-120">Для параметра **Тип проверки подлинности** выберите значение **Открытый ключ SSH**.</span><span class="sxs-lookup"><span data-stu-id="60542-120">For **Authentication type**, select **SSH public key**.</span></span> <span data-ttu-id="60542-121">При вставке в свой открытый ключ SSH, аккуратно tooremove все начальные и конечные пробелы.</span><span class="sxs-lookup"><span data-stu-id="60542-121">When pasting in your SSH public key, take care tooremove any leading or trailing white space.</span></span> <span data-ttu-id="60542-122">По завершении нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="60542-122">When complete, click **OK**.</span></span>

    ![Ввести основные сведения о ВМ в колонке портала hello](./media/quick-create-portal/create-vm-portal-basic-blade.png)

4. <span data-ttu-id="60542-124">Выберите размер виртуальной Машины hello.</span><span class="sxs-lookup"><span data-stu-id="60542-124">Select a size for hello VM.</span></span> <span data-ttu-id="60542-125">Выберите дополнительные размеры toosee **просмотреть все** или изменить hello **поддерживается тип диска** фильтра.</span><span class="sxs-lookup"><span data-stu-id="60542-125">toosee more sizes, select **View all** or change hello **Supported disk type** filter.</span></span> 

    ![Снимок экрана, на котором показаны размеры виртуальных машин](./media/quick-create-portal/create-linux-vm-portal-sizes.png)  

5. <span data-ttu-id="60542-127">В колонке параметров hello, оставьте значения по умолчанию hello и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="60542-127">On hello settings blade, keep hello defaults and click **OK**.</span></span>

6. <span data-ttu-id="60542-128">На странице сводки hello щелкните **ОК** развертывания виртуальной машины toostart hello.</span><span class="sxs-lookup"><span data-stu-id="60542-128">On hello summary page, click **Ok** toostart hello virtual machine deployment.</span></span>

7. <span data-ttu-id="60542-129">Hello виртуальной Машины будет закрепленных toohello Azure панели мониторинга портала.</span><span class="sxs-lookup"><span data-stu-id="60542-129">hello VM will be pinned toohello Azure portal dashboard.</span></span> <span data-ttu-id="60542-130">После завершения развертывания hello, автоматически откроется Сводка колонки hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="60542-130">Once hello deployment has completed, hello VM summary blade automatically opens.</span></span>


## <a name="connect-toovirtual-machine"></a><span data-ttu-id="60542-131">Подключиться к компьютеру toovirtual</span><span class="sxs-lookup"><span data-stu-id="60542-131">Connect toovirtual machine</span></span>

<span data-ttu-id="60542-132">Создайте SSH-подключения с hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="60542-132">Create an SSH connection with hello virtual machine.</span></span>

1. <span data-ttu-id="60542-133">Нажмите кнопку hello **Connect** кнопку hello колонке виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="60542-133">Click hello **Connect** button on hello virtual machine blade.</span></span> <span data-ttu-id="60542-134">Hello подключиться кнопки отображает строку подключения SSH, можно использовать tooconnect toohello виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="60542-134">hello connect button displays an SSH connection string that can be used tooconnect toohello virtual machine.</span></span>

    ![Портал 9](./media/quick-create-portal/portal-quick-start-9.png) 

2. <span data-ttu-id="60542-136">Выполнения hello следующая команда toocreate сеанс SSH.</span><span class="sxs-lookup"><span data-stu-id="60542-136">Run hello following command toocreate an SSH session.</span></span> <span data-ttu-id="60542-137">Замените строку соединения hello hello, один скопированной из hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="60542-137">Replace hello connection string with hello one you copied from hello Azure portal.</span></span>

```bash 
ssh azureuser@40.112.21.50
```

## <a name="install-nginx"></a><span data-ttu-id="60542-138">Установка nginx</span><span class="sxs-lookup"><span data-stu-id="60542-138">Install NGINX</span></span>

<span data-ttu-id="60542-139">Используйте hello ниже bash источники пакетов tooupdate сценария и установить последнюю версию пакета NGINX hello.</span><span class="sxs-lookup"><span data-stu-id="60542-139">Use hello following bash script tooupdate package sources and install hello latest NGINX package.</span></span> 

```bash 
#!/bin/bash

# update package source
sudo apt-get -y update

# install NGINX
sudo apt-get -y install nginx
```

<span data-ttu-id="60542-140">После этого завершите сеанс SSH hello и возвращает свойства виртуальной Машины hello hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="60542-140">When done, exit hello SSH session and return hello VM properties in hello Azure portal.</span></span>


## <a name="open-port-80-for-web-traffic"></a><span data-ttu-id="60542-141">Открытие порта 80 для веб-трафика</span><span class="sxs-lookup"><span data-stu-id="60542-141">Open port 80 for web traffic</span></span> 

<span data-ttu-id="60542-142">Группа безопасности сети (NSG) защищает входящий и исходящий трафик.</span><span class="sxs-lookup"><span data-stu-id="60542-142">A Network security group (NSG) secures inbound and outbound traffic.</span></span> <span data-ttu-id="60542-143">При создании виртуальной Машины из портала Azure hello входящее правило создается на порт 22 для соединений по протоколу SSH.</span><span class="sxs-lookup"><span data-stu-id="60542-143">When a VM is created from hello Azure portal, an inbound rule is created on port 22 for SSH connections.</span></span> <span data-ttu-id="60542-144">Поскольку эта виртуальная машина размещается веб-сервере, правило NSG должен toobe, созданное для порта 80.</span><span class="sxs-lookup"><span data-stu-id="60542-144">Because this VM hosts a webserver, an NSG rule needs toobe created for port 80.</span></span>

1. <span data-ttu-id="60542-145">На виртуальной машине hello, щелкните имя hello hello **группы ресурсов**.</span><span class="sxs-lookup"><span data-stu-id="60542-145">On hello virtual machine, click hello name of hello **Resource group**.</span></span>
2. <span data-ttu-id="60542-146">Выберите hello **сетевой группы безопасности**.</span><span class="sxs-lookup"><span data-stu-id="60542-146">Select hello **network security group**.</span></span> <span data-ttu-id="60542-147">Hello NSG можно определить с помощью hello **тип** столбца.</span><span class="sxs-lookup"><span data-stu-id="60542-147">hello NSG can be identified using hello **Type** column.</span></span> 
3. <span data-ttu-id="60542-148">Hello слева в разделе Параметры меню **безопасности правила для входящих подключений**.</span><span class="sxs-lookup"><span data-stu-id="60542-148">On hello left-hand menu, under settings, click **Inbound security rules**.</span></span>
4. <span data-ttu-id="60542-149">Щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="60542-149">Click on **Add**.</span></span>
5. <span data-ttu-id="60542-150">В поле **Имя** введите **http**.</span><span class="sxs-lookup"><span data-stu-id="60542-150">In **Name**, type **http**.</span></span> <span data-ttu-id="60542-151">Убедитесь, что **диапазон портов** задано too80 и **действия** задано слишком**Разрешить**.</span><span class="sxs-lookup"><span data-stu-id="60542-151">Make sure **Port range** is set too80 and **Action** is set too**Allow**.</span></span> 
6. <span data-ttu-id="60542-152">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="60542-152">Click **OK**.</span></span>


## <a name="view-hello-nginx-welcome-page"></a><span data-ttu-id="60542-153">Просмотр hello NGINX начальной страницы</span><span class="sxs-lookup"><span data-stu-id="60542-153">View hello NGINX welcome page</span></span>

<span data-ttu-id="60542-154">С NGINX установлены и порт 80 откройте tooyour виртуальных Машин, веб-сервер hello, теперь доступны из hello Интернета.</span><span class="sxs-lookup"><span data-stu-id="60542-154">With NGINX installed, and port 80 open tooyour VM, hello webserver can now be accessed from hello internet.</span></span> <span data-ttu-id="60542-155">Откройте веб-браузер и введите hello общедоступный IP-адрес hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="60542-155">Open a web browser, and enter hello public IP address of hello VM.</span></span> <span data-ttu-id="60542-156">Hello общедоступный IP-адрес можно найти на колонки виртуальной Машины hello в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="60542-156">hello public IP address can be found on hello VM blade in hello Azure portal.</span></span>

![Сайт nginx по умолчанию](./media/quick-create-cli/nginx.png) 

## <a name="clean-up-resources"></a><span data-ttu-id="60542-158">Очистка ресурсов</span><span class="sxs-lookup"><span data-stu-id="60542-158">Clean up resources</span></span>

<span data-ttu-id="60542-159">Когда больше не нужен, удалите hello группы ресурсов, виртуальные машины и все связанные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="60542-159">When no longer needed, delete hello resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="60542-160">toodo таким образом, выберите группу ресурсов hello hello колонке виртуальной машины и нажмите кнопку **удалить**.</span><span class="sxs-lookup"><span data-stu-id="60542-160">toodo so, select hello resource group from hello virtual machine blade and click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="60542-161">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="60542-161">Next steps</span></span>

<span data-ttu-id="60542-162">Из этого краткого руководства вы узнали о том, как развернуть простую виртуальную машину, о правилах группы безопасности сети и об установке веб-сервера.</span><span class="sxs-lookup"><span data-stu-id="60542-162">In this quick start, you’ve deployed a simple virtual machine, a network security group rule, and installed a web server.</span></span> <span data-ttu-id="60542-163">toolearn Дополнительные сведения о виртуальных машинах Azure, продолжить toohello учебника для виртуальных машин Linux.</span><span class="sxs-lookup"><span data-stu-id="60542-163">toolearn more about Azure virtual machines, continue toohello tutorial for Linux VMs.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="60542-164">Создание виртуальных машин Linux и управление ими с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="60542-164">Azure Linux virtual machine tutorials</span></span>](./tutorial-manage-vm.md)
