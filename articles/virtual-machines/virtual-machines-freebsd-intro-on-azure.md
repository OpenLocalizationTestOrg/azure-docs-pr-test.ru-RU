---
title: "Введение в FreeBSD в Azure | Документация Майкрософт"
description: "Узнайте о том, как использовать виртуальные машины FreeBSD в Azure."
services: virtual-machines-linux
documentationcenter: 
author: KylieLiang
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 32b87a5f-d024-4da0-8bf0-77e233d1422b
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/28/2017
ms.author: kyliel
ms.openlocfilehash: d0fc5de34f7d9e5a607495eb97d9e35dc9eb21f9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="introduction-to-freebsd-on-azure"></a><span data-ttu-id="a21bb-103">Введение в FreeBSD в Azure</span><span class="sxs-lookup"><span data-stu-id="a21bb-103">Introduction to FreeBSD on Azure</span></span>
<span data-ttu-id="a21bb-104">В этом разделе представлен обзор запуска виртуальной машины FreeBSD в Azure.</span><span class="sxs-lookup"><span data-stu-id="a21bb-104">This topic provides an overview of running a FreeBSD virtual machine in Azure.</span></span>

## <a name="overview"></a><span data-ttu-id="a21bb-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="a21bb-105">Overview</span></span>
<span data-ttu-id="a21bb-106">FreeBSD для Microsoft Azure — это расширенная операционная система, которая использовалась для управления мощными современными серверами, настольными компьютерами и внедренными платформами.</span><span class="sxs-lookup"><span data-stu-id="a21bb-106">FreeBSD for Microsoft Azure is an advanced computer operating system used to power modern servers, desktops, and embedded platforms.</span></span>

<span data-ttu-id="a21bb-107">Корпорация Майкрософт предоставляет образы FreeBSD на платформе Azure с предварительно настроенным [гостевым агентом виртуальной машины Azure](https://github.com/Azure/WALinuxAgent/).</span><span class="sxs-lookup"><span data-stu-id="a21bb-107">Microsoft Corporation is making images of FreeBSD available on Azure with the [Azure VM Guest Agent](https://github.com/Azure/WALinuxAgent/) pre-configured.</span></span> <span data-ttu-id="a21bb-108">В настоящее время она предлагает образы FreeBSD следующих версий:</span><span class="sxs-lookup"><span data-stu-id="a21bb-108">Currently, the following FreeBSD versions are offered as images by Microsoft:</span></span>

- <span data-ttu-id="a21bb-109">FreeBSD 10.3-RELEASE</span><span class="sxs-lookup"><span data-stu-id="a21bb-109">FreeBSD 10.3-RELEASE</span></span>
- <span data-ttu-id="a21bb-110">FreeBSD 11.0-RELEASE</span><span class="sxs-lookup"><span data-stu-id="a21bb-110">FreeBSD 11.0-RELEASE</span></span>

<span data-ttu-id="a21bb-111">Этот агент отвечает за обмен данными между виртуальной машиной FreeBSD и Azure Fabric при таких операциях, как подготовка виртуальной машины к первому использованию (имя пользователя, пароль или ключ SSH, имя узла и т. д.) и выборочное включение функций расширений виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="a21bb-111">The agent is responsible for communication between the FreeBSD VM and the Azure fabric for operations such as provisioning the VM on first use (user name, password or SSH key, host name, etc.) and enabling functionality for selective VM extensions.</span></span>

<span data-ttu-id="a21bb-112">Стратегия в отношении текущей и будущих версий FreeBSD — обеспечивать актуальность и предоставлять последние версии вскоре после их публикации командой технических специалистов по выпуску FreeBSD.</span><span class="sxs-lookup"><span data-stu-id="a21bb-112">As for future versions of FreeBSD, the strategy is to stay current and make the latest releases available shortly after they are published by the FreeBSD release engineering team.</span></span>

## <a name="deploying-a-freebsd-virtual-machine"></a><span data-ttu-id="a21bb-113">Развертывание виртуальной машины FreeBSD</span><span class="sxs-lookup"><span data-stu-id="a21bb-113">Deploying a FreeBSD virtual machine</span></span>
<span data-ttu-id="a21bb-114">В развертывании образа виртуальной машины FreeBSD с помощью образа из Azure Marketplace и портала Azure нет ничего сложного:</span><span class="sxs-lookup"><span data-stu-id="a21bb-114">Deploying a FreeBSD virtual machine is a straightforward process using an image from the Azure Marketplace from the Azure portal:</span></span>

- [<span data-ttu-id="a21bb-115">FreeBSD 10.3 на Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="a21bb-115">FreeBSD 10.3 on the Azure Marketplace</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd103/)
- [<span data-ttu-id="a21bb-116">FreeBSD 11.0 на Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="a21bb-116">FreeBSD 11.0 on the Azure Marketplace</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd110/)

### <a name="create-a-freebsd-vm-through-azure-cli-20-on-freebsd"></a><span data-ttu-id="a21bb-117">Создайте виртуальную машину FreeBSD с помощью Azure CLI 2.0 в FreeBSD.</span><span class="sxs-lookup"><span data-stu-id="a21bb-117">Create a FreeBSD VM through Azure CLI 2.0 on FreeBSD</span></span>
<span data-ttu-id="a21bb-118">Сначала необходимо установить [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), выполнив следующую команду на компьютере FreeBSD.</span><span class="sxs-lookup"><span data-stu-id="a21bb-118">First you need to install [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) though following command on a FreeBSD machine.</span></span>

```bash 
    curl -L https://aka.ms/InstallAzureCli | bash
```

<span data-ttu-id="a21bb-119">Если на компьютере FreeBSD не установлена оболочка bash, выполните следующую команду перед установкой.</span><span class="sxs-lookup"><span data-stu-id="a21bb-119">If bash is not installed on your FreeBSD machine, run following command before the installation.</span></span> 

```
    sudo pkg install bash
```

<span data-ttu-id="a21bb-120">Если на компьютере FreeBSD не установлен python, выполните следующие команды перед установкой.</span><span class="sxs-lookup"><span data-stu-id="a21bb-120">If python is not installed on your FreeBSD machine, run following commands before the installation.</span></span> 

```
    sudo pkg install python35
    cd /usr/local/bin 
    sudo rm /usr/local/bin/python 
    sudo ln -s /usr/local/bin/python3.5 /usr/local/bin/python
```

<span data-ttu-id="a21bb-121">Во время установки вам будет задан вопрос `Modify profile to update your $PATH and enable shell/tab completion now? (Y/n)`.</span><span class="sxs-lookup"><span data-stu-id="a21bb-121">During the installation, you are asked `Modify profile to update your $PATH and enable shell/tab completion now? (Y/n)`.</span></span> <span data-ttu-id="a21bb-122">Если вы ответили `y` и указали `/etc/rc.conf` в качестве `a path to an rc file to update`, может возникнуть следующая ошибка: `ERROR: [Errno 13] Permission denied`.</span><span class="sxs-lookup"><span data-stu-id="a21bb-122">If you answer `y` and enter `/etc/rc.conf` as `a path to an rc file to update`, you may meet the problem `ERROR: [Errno 13] Permission denied`.</span></span> <span data-ttu-id="a21bb-123">Чтобы устранить эту проблему, нужно предоставить текущему пользователю права на запись для файла `etc/rc.conf`.</span><span class="sxs-lookup"><span data-stu-id="a21bb-123">To resolve this problem, you should grant the write right to current user against the file `etc/rc.conf`.</span></span>

<span data-ttu-id="a21bb-124">Теперь можно войти в Azure и создать виртуальную машину FreeBSD.</span><span class="sxs-lookup"><span data-stu-id="a21bb-124">Now you can log in Azure and create your FreeBSD VM.</span></span> <span data-ttu-id="a21bb-125">Ниже приведен пример создания виртуальной машины FreeBSD версии 11.0.</span><span class="sxs-lookup"><span data-stu-id="a21bb-125">Below is an example to create a FreeBSD 11.0 VM.</span></span> <span data-ttu-id="a21bb-126">Также можно добавить параметр `--public-ip-address-dns-name` с глобальным именем DNS для созданного общедоступного IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="a21bb-126">You can also add the parameter `--public-ip-address-dns-name` with a globally unique DNS name for a newly created Public IP.</span></span> 

```azurecli
    az login 
    az group create -n myResourceGroup -l westus az vm create -n myFreeBSD11 -g myResourceGroup --image MicrosoftOSTC:FreeBSD:11.0:latest --admin-username azureuser --ssh-key-value /etc/ssh/ssh_host_rsa_key.pub 
```

<span data-ttu-id="a21bb-127">Затем вы сможете войти в виртуальную машину FreeBSD с помощью IP-адреса, который приведен в выходных данных описанного выше развертывания.</span><span class="sxs-lookup"><span data-stu-id="a21bb-127">Then you can log in to your FreeBSD VM through the ip address that printed in the output of above deployment.</span></span> 

```bash
    ssh azureuser@xx.xx.xx.xx -i /etc/ssh/ssh_host_rsa_key
```   

## <a name="vm-extensions-for-freebsd"></a><span data-ttu-id="a21bb-128">Расширения виртуальной машины для FreeBSD</span><span class="sxs-lookup"><span data-stu-id="a21bb-128">VM extensions for FreeBSD</span></span>
<span data-ttu-id="a21bb-129">Ниже приведены поддерживаемые во FreeBSD расширения виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="a21bb-129">Following are supported VM extensions in FreeBSD.</span></span>

### <a name="vmaccess"></a><span data-ttu-id="a21bb-130">VMAccess</span><span class="sxs-lookup"><span data-stu-id="a21bb-130">VMAccess</span></span>
<span data-ttu-id="a21bb-131">Возможности расширения [VMAccess](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess) :</span><span class="sxs-lookup"><span data-stu-id="a21bb-131">The [VMAccess](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess) extension can:</span></span>

* <span data-ttu-id="a21bb-132">сброс пароля исходного пользователя sudo;</span><span class="sxs-lookup"><span data-stu-id="a21bb-132">Reset the password of the original sudo user.</span></span>
* <span data-ttu-id="a21bb-133">создание пользователя sudo с указанным паролем;</span><span class="sxs-lookup"><span data-stu-id="a21bb-133">Create a new sudo user with the password specified.</span></span>
* <span data-ttu-id="a21bb-134">настройка заданного значения открытого ключа узла;</span><span class="sxs-lookup"><span data-stu-id="a21bb-134">Set the public host key with the key given.</span></span>
* <span data-ttu-id="a21bb-135">сброс открытого ключа узла, указанного во время подготовки виртуальной машины, если не указан ключ узла;</span><span class="sxs-lookup"><span data-stu-id="a21bb-135">Reset the public host key provided during VM provisioning if the host key is not provided.</span></span>
* <span data-ttu-id="a21bb-136">открытие порта SSH (22) и восстановление sshd_config, если для reset_ssh задано значение true;</span><span class="sxs-lookup"><span data-stu-id="a21bb-136">Open the SSH port (22) and restore the sshd_config if reset_ssh is set to true.</span></span>
* <span data-ttu-id="a21bb-137">удаление существующего пользователя;</span><span class="sxs-lookup"><span data-stu-id="a21bb-137">Remove the existing user.</span></span>
* <span data-ttu-id="a21bb-138">проверка дисков;</span><span class="sxs-lookup"><span data-stu-id="a21bb-138">Check disks.</span></span>
* <span data-ttu-id="a21bb-139">восстановление добавленного диска.</span><span class="sxs-lookup"><span data-stu-id="a21bb-139">Repair an added disk.</span></span>

### <a name="customscript"></a><span data-ttu-id="a21bb-140">CustomScript</span><span class="sxs-lookup"><span data-stu-id="a21bb-140">CustomScript</span></span>
<span data-ttu-id="a21bb-141">Возможности расширения [CustomScript](https://github.com/Azure/azure-linux-extensions/tree/master/CustomScript) :</span><span class="sxs-lookup"><span data-stu-id="a21bb-141">The [CustomScript](https://github.com/Azure/azure-linux-extensions/tree/master/CustomScript) extension can:</span></span>

* <span data-ttu-id="a21bb-142">скачивание предоставленных пользовательских сценариев из службы хранилища Azure или общедоступного внешнего хранилища (например, Github);</span><span class="sxs-lookup"><span data-stu-id="a21bb-142">If provided, download the customized scripts from Azure Storage or external public storage (for example, GitHub).</span></span>
* <span data-ttu-id="a21bb-143">выполнение сценария точки входа;</span><span class="sxs-lookup"><span data-stu-id="a21bb-143">Run the entry point script.</span></span>
* <span data-ttu-id="a21bb-144">поддержка встроенных команд;</span><span class="sxs-lookup"><span data-stu-id="a21bb-144">Support inline commands.</span></span>
* <span data-ttu-id="a21bb-145">автоматическое преобразование символа новой строки в стиле Windows в сценариях оболочки и Python;</span><span class="sxs-lookup"><span data-stu-id="a21bb-145">Convert Windows-style newline in shell and Python scripts automatically.</span></span>
* <span data-ttu-id="a21bb-146">автоматическое удаление спецификации в сценариях оболочки и Python;</span><span class="sxs-lookup"><span data-stu-id="a21bb-146">Remove BOM in shell and Python scripts automatically.</span></span>
* <span data-ttu-id="a21bb-147">защита конфиденциальных данных в commandToExecute.</span><span class="sxs-lookup"><span data-stu-id="a21bb-147">Protect sensitive data in CommandToExecute.</span></span>

> [!NOTE]
> <span data-ttu-id="a21bb-148">В настоящий момент виртуальная машина FreeBSD поддерживает только CustomScript версии 1.x.</span><span class="sxs-lookup"><span data-stu-id="a21bb-148">FreeBSD VM only supports CustomScript version 1.x by now.</span></span>  

## <a name="authentication-user-names-passwords-and-ssh-keys"></a><span data-ttu-id="a21bb-149">Аутентификация: имена пользователей, пароли и ключи SSH</span><span class="sxs-lookup"><span data-stu-id="a21bb-149">Authentication: user names, passwords, and SSH keys</span></span>
<span data-ttu-id="a21bb-150">При создании виртуальной машины FreeBSD с помощью портала Azure необходимо указать имя пользователя, пароль или открытый ключ SSH.</span><span class="sxs-lookup"><span data-stu-id="a21bb-150">When you're creating a FreeBSD virtual machine by using the Azure portal, you must provide a user name, password, or SSH public key.</span></span>
<span data-ttu-id="a21bb-151">Имена пользователей для развертывания виртуальной машины FreeBSD в Azure не должны совпадать с именами системных учетных записей (UID < 100), уже присутствующих в виртуальной машине (например, root).</span><span class="sxs-lookup"><span data-stu-id="a21bb-151">User names for deploying a FreeBSD virtual machine on Azure must not match names of system accounts (UID <100) already present in the virtual machine ("root", for example).</span></span>
<span data-ttu-id="a21bb-152">В настоящее время поддерживается только ключ SSH на основе RSA.</span><span class="sxs-lookup"><span data-stu-id="a21bb-152">Currently, only the RSA SSH key is supported.</span></span> <span data-ttu-id="a21bb-153">Многострочный ключ SSH должен начинаться с `---- BEGIN SSH2 PUBLIC KEY ----` и заканчиваться `---- END SSH2 PUBLIC KEY ----`.</span><span class="sxs-lookup"><span data-stu-id="a21bb-153">A multiline SSH key must begin with `---- BEGIN SSH2 PUBLIC KEY ----` and end with `---- END SSH2 PUBLIC KEY ----`.</span></span>

## <a name="obtaining-superuser-privileges"></a><span data-ttu-id="a21bb-154">Получение привилегий суперпользователя</span><span class="sxs-lookup"><span data-stu-id="a21bb-154">Obtaining superuser privileges</span></span>
<span data-ttu-id="a21bb-155">Учетная запись пользователя, указанная во время развертывания экземпляра виртуальной машины в Azure, является привилегированной учетной записью.</span><span class="sxs-lookup"><span data-stu-id="a21bb-155">The user account that is specified during virtual machine instance deployment on Azure is a privileged account.</span></span> <span data-ttu-id="a21bb-156">Пакет sudo установлен в опубликованном образе FreeBSD.</span><span class="sxs-lookup"><span data-stu-id="a21bb-156">The package of sudo was installed in the published FreeBSD image.</span></span>
<span data-ttu-id="a21bb-157">После входа в систему с помощью этой учетной записи пользователя вы сможете выполнять команды от учетной записи root, используя соответствующий синтаксис команд.</span><span class="sxs-lookup"><span data-stu-id="a21bb-157">After you're logged in through this user account, you can run commands as root by using the command syntax.</span></span>

```
    $ sudo <COMMAND>
```

<span data-ttu-id="a21bb-158">При необходимости можно получить доступ к оболочке root с помощью команды `sudo -s`.</span><span class="sxs-lookup"><span data-stu-id="a21bb-158">You can optionally obtain a root shell by using `sudo -s`.</span></span>

## <a name="known-issues"></a><span data-ttu-id="a21bb-159">Известные проблемы</span><span class="sxs-lookup"><span data-stu-id="a21bb-159">Known issues</span></span>
<span data-ttu-id="a21bb-160">[Гостевой агент виртуальной машины Azure](https://github.com/Azure/WALinuxAgent/) версии 2.2.2 имеет [известную проблему] (https://github.com/Azure/WALinuxAgent/pull/517), вызывающую сбой подготовки виртуальной машины FreeBSD в Azure.</span><span class="sxs-lookup"><span data-stu-id="a21bb-160">The [Azure VM Guest Agent](https://github.com/Azure/WALinuxAgent/) version 2.2.2 has a [known issue] (https://github.com/Azure/WALinuxAgent/pull/517) that causes the provision failure for FreeBSD VM on Azure.</span></span> <span data-ttu-id="a21bb-161">Ошибка исправлена в [гостевом агенте виртуальной машины Azure](https://github.com/Azure/WALinuxAgent/) версии 2.2.3 и более поздних выпусках.</span><span class="sxs-lookup"><span data-stu-id="a21bb-161">The fix was captured by [Azure VM Guest Agent](https://github.com/Azure/WALinuxAgent/) version 2.2.3 and later releases.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="a21bb-162">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a21bb-162">Next steps</span></span>
* <span data-ttu-id="a21bb-163">Перейдите на сайт [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd110/) , чтобы создать виртуальную машину FreeBSD.</span><span class="sxs-lookup"><span data-stu-id="a21bb-163">Go to [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd110/) to create a FreeBSD VM.</span></span>
* <span data-ttu-id="a21bb-164">Если вы хотите перенести свою собственную виртуальную машину FreeBSD в Azure, ознакомьтесь с разделом [Создание и отправка виртуального жесткого диска FreeBSD в Azure](linux/classic/freebsd-create-upload-vhd.md).</span><span class="sxs-lookup"><span data-stu-id="a21bb-164">If you want to bring your own FreeBSD to Azure, refer to [Create and upload a FreeBSD VHD to Azure](linux/classic/freebsd-create-upload-vhd.md).</span></span>
