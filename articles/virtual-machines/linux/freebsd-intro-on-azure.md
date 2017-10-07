---
title: "tooFreeBSD aaaIntroduction в Azure | Документы Microsoft"
description: "Узнайте о том, как использовать виртуальные машины FreeBSD в Azure."
services: virtual-machines-linux
documentationcenter: 
author: KylieLiang
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 32b87a5f-d024-4da0-8bf0-77e233d1422b
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/28/2017
ms.author: kyliel
ms.openlocfilehash: 43ba7a70ed21e7fb8b331f4a26db0426e098c4aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toofreebsd-on-azure"></a><span data-ttu-id="4ce8a-103">TooFreeBSD введение в Azure</span><span class="sxs-lookup"><span data-stu-id="4ce8a-103">Introduction tooFreeBSD on Azure</span></span>
<span data-ttu-id="4ce8a-104">В этом разделе представлен обзор запуска виртуальной машины FreeBSD в Azure.</span><span class="sxs-lookup"><span data-stu-id="4ce8a-104">This topic provides an overview of running a FreeBSD virtual machine in Azure.</span></span>

## <a name="overview"></a><span data-ttu-id="4ce8a-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="4ce8a-105">Overview</span></span>
<span data-ttu-id="4ce8a-106">FreeBSD для Microsoft Azure — Дополнительно операционной системы используется toopower современных серверов, настольных компьютеров и внедренные платформы.</span><span class="sxs-lookup"><span data-stu-id="4ce8a-106">FreeBSD for Microsoft Azure is an advanced computer operating system used toopower modern servers, desktops, and embedded platforms.</span></span>

<span data-ttu-id="4ce8a-107">Корпорация Майкрософт предоставление FreeBSD образы в Azure с hello [гостевой агент виртуальной Машины Azure](https://github.com/Azure/WALinuxAgent/) предварительно настроен.</span><span class="sxs-lookup"><span data-stu-id="4ce8a-107">Microsoft Corporation is making images of FreeBSD available on Azure with hello [Azure VM Guest Agent](https://github.com/Azure/WALinuxAgent/) pre-configured.</span></span> <span data-ttu-id="4ce8a-108">В настоящее время hello следующие версии FreeBSD предлагается как изображения корпорацией Майкрософт:</span><span class="sxs-lookup"><span data-stu-id="4ce8a-108">Currently, hello following FreeBSD versions are offered as images by Microsoft:</span></span>

- <span data-ttu-id="4ce8a-109">FreeBSD 10.3-RELEASE</span><span class="sxs-lookup"><span data-stu-id="4ce8a-109">FreeBSD 10.3-RELEASE</span></span>
- <span data-ttu-id="4ce8a-110">FreeBSD 11.0-RELEASE</span><span class="sxs-lookup"><span data-stu-id="4ce8a-110">FreeBSD 11.0-RELEASE</span></span>

<span data-ttu-id="4ce8a-111">агент Hello отвечает за обмен данными между hello FreeBSD ВМ и hello Azure fabric для операции, такие как подготовка hello виртуальной Машины на первом использовании (имя пользователя, пароль или ключ SSH, имя узла, т. д.) и включение функций для выборочного расширения виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="4ce8a-111">hello agent is responsible for communication between hello FreeBSD VM and hello Azure fabric for operations such as provisioning hello VM on first use (user name, password or SSH key, host name, etc.) and enabling functionality for selective VM extensions.</span></span>

<span data-ttu-id="4ce8a-112">Как и для будущих версий FreeBSD стратегии hello toostay текущего и сделать hello последних выпусках доступных вскоре после их публикации hello FreeBSD выпуска инженеров.</span><span class="sxs-lookup"><span data-stu-id="4ce8a-112">As for future versions of FreeBSD, hello strategy is toostay current and make hello latest releases available shortly after they are published by hello FreeBSD release engineering team.</span></span>

## <a name="deploying-a-freebsd-virtual-machine"></a><span data-ttu-id="4ce8a-113">Развертывание виртуальной машины FreeBSD</span><span class="sxs-lookup"><span data-stu-id="4ce8a-113">Deploying a FreeBSD virtual machine</span></span>
<span data-ttu-id="4ce8a-114">Развертывание виртуальной машины FreeBSD представляет собой простой процесс, с помощью образа из hello Azure Marketplace из hello портала Azure:</span><span class="sxs-lookup"><span data-stu-id="4ce8a-114">Deploying a FreeBSD virtual machine is a straightforward process using an image from hello Azure Marketplace from hello Azure portal:</span></span>

- [<span data-ttu-id="4ce8a-115">10.3 FreeBSD на hello Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="4ce8a-115">FreeBSD 10.3 on hello Azure Marketplace</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd103/)
- [<span data-ttu-id="4ce8a-116">11.0 FreeBSD на hello Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="4ce8a-116">FreeBSD 11.0 on hello Azure Marketplace</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd110/)

### <a name="create-a-freebsd-vm-through-azure-cli-20-on-freebsd"></a><span data-ttu-id="4ce8a-117">Создайте виртуальную машину FreeBSD с помощью Azure CLI 2.0 в FreeBSD.</span><span class="sxs-lookup"><span data-stu-id="4ce8a-117">Create a FreeBSD VM through Azure CLI 2.0 on FreeBSD</span></span>
<span data-ttu-id="4ce8a-118">Сначала необходимо tooinstall [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) хотя следующую команду на компьютере FreeBSD.</span><span class="sxs-lookup"><span data-stu-id="4ce8a-118">First you need tooinstall [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) though following command on a FreeBSD machine.</span></span>

```bash 
curl -L https://aka.ms/InstallAzureCli | bash
```

<span data-ttu-id="4ce8a-119">Если bash не установлены на компьютере FreeBSD, выполните следующую команду перед установкой hello.</span><span class="sxs-lookup"><span data-stu-id="4ce8a-119">If bash is not installed on your FreeBSD machine, run following command before hello installation.</span></span> 

```bash
sudo pkg install bash
```

<span data-ttu-id="4ce8a-120">Если python не установлены на компьютере FreeBSD, выполните следующие команды перед установкой hello.</span><span class="sxs-lookup"><span data-stu-id="4ce8a-120">If python is not installed on your FreeBSD machine, run following commands before hello installation.</span></span> 

```bash
sudo pkg install python35
cd /usr/local/bin 
sudo rm /usr/local/bin/python 
sudo ln -s /usr/local/bin/python3.5 /usr/local/bin/python
```

<span data-ttu-id="4ce8a-121">Во время установки hello, будет предложено `Modify profile tooupdate your $PATH and enable shell/tab completion now? (Y/n)`.</span><span class="sxs-lookup"><span data-stu-id="4ce8a-121">During hello installation, you are asked `Modify profile tooupdate your $PATH and enable shell/tab completion now? (Y/n)`.</span></span> <span data-ttu-id="4ce8a-122">При выборе варианта `y` и введите `/etc/rc.conf` как `a path tooan rc file tooupdate`, может отвечать hello проблема `ERROR: [Errno 13] Permission denied`.</span><span class="sxs-lookup"><span data-stu-id="4ce8a-122">If you answer `y` and enter `/etc/rc.conf` as `a path tooan rc file tooupdate`, you may meet hello problem `ERROR: [Errno 13] Permission denied`.</span></span> <span data-ttu-id="4ce8a-123">tooresolve эту проблему, следует предоставить hello записи справа toocurrent пользователя по файлу hello `etc/rc.conf`.</span><span class="sxs-lookup"><span data-stu-id="4ce8a-123">tooresolve this problem, you should grant hello write right toocurrent user against hello file `etc/rc.conf`.</span></span>

<span data-ttu-id="4ce8a-124">Теперь можно войти в Azure и создать виртуальную машину FreeBSD.</span><span class="sxs-lookup"><span data-stu-id="4ce8a-124">Now you can log in Azure and create your FreeBSD VM.</span></span> <span data-ttu-id="4ce8a-125">Ниже приведен пример toocreate 11.0 FreeBSD виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="4ce8a-125">Below is an example toocreate a FreeBSD 11.0 VM.</span></span> <span data-ttu-id="4ce8a-126">Можно также добавить параметр hello `--public-ip-address-dns-name` глобально уникальное имя DNS для только что созданный общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="4ce8a-126">You can also add hello parameter `--public-ip-address-dns-name` with a globally unique DNS name for a newly created Public IP.</span></span> 

```azurecli
az login 
az group create --name myResourceGroup --location eastus
az vm create --name myFreeBSD11 \
    --resource-group myResourceGroup \
    --image MicrosoftOSTC:FreeBSD:11.0:latest \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="4ce8a-127">Затем вы можете войти tooyour FreeBSD ВМ через hello IP-адрес, печатаются в hello выше выходных данных для развертывания.</span><span class="sxs-lookup"><span data-stu-id="4ce8a-127">Then you can log in tooyour FreeBSD VM through hello ip address that printed in hello output of above deployment.</span></span> 

```bash
ssh azureuser@xx.xx.xx.xx -i /etc/ssh/ssh_host_rsa_key
```   

## <a name="vm-extensions-for-freebsd"></a><span data-ttu-id="4ce8a-128">Расширения виртуальной машины для FreeBSD</span><span class="sxs-lookup"><span data-stu-id="4ce8a-128">VM extensions for FreeBSD</span></span>
<span data-ttu-id="4ce8a-129">Ниже приведены поддерживаемые во FreeBSD расширения виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="4ce8a-129">Following are supported VM extensions in FreeBSD.</span></span>

### <a name="vmaccess"></a><span data-ttu-id="4ce8a-130">VMAccess</span><span class="sxs-lookup"><span data-stu-id="4ce8a-130">VMAccess</span></span>
<span data-ttu-id="4ce8a-131">Hello [VMAccess](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess) расширения можно:</span><span class="sxs-lookup"><span data-stu-id="4ce8a-131">hello [VMAccess](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess) extension can:</span></span>

* <span data-ttu-id="4ce8a-132">Сброс пароля hello hello исходного пользователя sudo.</span><span class="sxs-lookup"><span data-stu-id="4ce8a-132">Reset hello password of hello original sudo user.</span></span>
* <span data-ttu-id="4ce8a-133">Создайте нового пользователя sudo задан пароль hello.</span><span class="sxs-lookup"><span data-stu-id="4ce8a-133">Create a new sudo user with hello password specified.</span></span>
* <span data-ttu-id="4ce8a-134">Задать ключ hello общедоступного узла с заданным ключом hello.</span><span class="sxs-lookup"><span data-stu-id="4ce8a-134">Set hello public host key with hello key given.</span></span>
* <span data-ttu-id="4ce8a-135">Сброс ключа общедоступного узла hello, указанные во время подготовки, если не указан ключ hello узла виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="4ce8a-135">Reset hello public host key provided during VM provisioning if hello host key is not provided.</span></span>
* <span data-ttu-id="4ce8a-136">Откройте порт SSH hello (22) и восстановления hello sshd_config, если reset_ssh tootrue.</span><span class="sxs-lookup"><span data-stu-id="4ce8a-136">Open hello SSH port (22) and restore hello sshd_config if reset_ssh is set tootrue.</span></span>
* <span data-ttu-id="4ce8a-137">Удаление существующего пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="4ce8a-137">Remove hello existing user.</span></span>
* <span data-ttu-id="4ce8a-138">проверка дисков;</span><span class="sxs-lookup"><span data-stu-id="4ce8a-138">Check disks.</span></span>
* <span data-ttu-id="4ce8a-139">восстановление добавленного диска.</span><span class="sxs-lookup"><span data-stu-id="4ce8a-139">Repair an added disk.</span></span>

### <a name="customscript"></a><span data-ttu-id="4ce8a-140">CustomScript</span><span class="sxs-lookup"><span data-stu-id="4ce8a-140">CustomScript</span></span>
<span data-ttu-id="4ce8a-141">Hello [CustomScript](https://github.com/Azure/azure-linux-extensions/tree/master/CustomScript) расширения можно:</span><span class="sxs-lookup"><span data-stu-id="4ce8a-141">hello [CustomScript](https://github.com/Azure/azure-linux-extensions/tree/master/CustomScript) extension can:</span></span>

* <span data-ttu-id="4ce8a-142">Если указано, загрузите hello пользовательские скрипты из хранилища Azure или открытый внешнего хранилища (например, GitHub).</span><span class="sxs-lookup"><span data-stu-id="4ce8a-142">If provided, download hello customized scripts from Azure Storage or external public storage (for example, GitHub).</span></span>
* <span data-ttu-id="4ce8a-143">Запустите сценарий точки входа hello.</span><span class="sxs-lookup"><span data-stu-id="4ce8a-143">Run hello entry point script.</span></span>
* <span data-ttu-id="4ce8a-144">поддержка встроенных команд;</span><span class="sxs-lookup"><span data-stu-id="4ce8a-144">Support inline commands.</span></span>
* <span data-ttu-id="4ce8a-145">автоматическое преобразование символа новой строки в стиле Windows в сценариях оболочки и Python;</span><span class="sxs-lookup"><span data-stu-id="4ce8a-145">Convert Windows-style newline in shell and Python scripts automatically.</span></span>
* <span data-ttu-id="4ce8a-146">автоматическое удаление спецификации в сценариях оболочки и Python;</span><span class="sxs-lookup"><span data-stu-id="4ce8a-146">Remove BOM in shell and Python scripts automatically.</span></span>
* <span data-ttu-id="4ce8a-147">защита конфиденциальных данных в commandToExecute.</span><span class="sxs-lookup"><span data-stu-id="4ce8a-147">Protect sensitive data in CommandToExecute.</span></span>

> [!NOTE]
> <span data-ttu-id="4ce8a-148">В настоящий момент виртуальная машина FreeBSD поддерживает только CustomScript версии 1.x.</span><span class="sxs-lookup"><span data-stu-id="4ce8a-148">FreeBSD VM only supports CustomScript version 1.x by now.</span></span>  

## <a name="authentication-user-names-passwords-and-ssh-keys"></a><span data-ttu-id="4ce8a-149">Аутентификация: имена пользователей, пароли и ключи SSH</span><span class="sxs-lookup"><span data-stu-id="4ce8a-149">Authentication: user names, passwords, and SSH keys</span></span>
<span data-ttu-id="4ce8a-150">При создании FreeBSD виртуальной машины с помощью hello портал Azure, необходимо указать имя пользователя, пароль или открытый ключ SSH.</span><span class="sxs-lookup"><span data-stu-id="4ce8a-150">When you're creating a FreeBSD virtual machine by using hello Azure portal, you must provide a user name, password, or SSH public key.</span></span>
<span data-ttu-id="4ce8a-151">Имена пользователей для развертывания виртуальной машины в Azure FreeBSD не должны совпадать с именами системных учетных записей (UID < 100) уже существует в виртуальной машине hello (например, «root»).</span><span class="sxs-lookup"><span data-stu-id="4ce8a-151">User names for deploying a FreeBSD virtual machine on Azure must not match names of system accounts (UID <100) already present in hello virtual machine ("root", for example).</span></span>
<span data-ttu-id="4ce8a-152">В настоящее время поддерживается только hello RSA SSH-ключа.</span><span class="sxs-lookup"><span data-stu-id="4ce8a-152">Currently, only hello RSA SSH key is supported.</span></span> <span data-ttu-id="4ce8a-153">Многострочный ключ SSH должен начинаться с `---- BEGIN SSH2 PUBLIC KEY ----` и заканчиваться `---- END SSH2 PUBLIC KEY ----`.</span><span class="sxs-lookup"><span data-stu-id="4ce8a-153">A multiline SSH key must begin with `---- BEGIN SSH2 PUBLIC KEY ----` and end with `---- END SSH2 PUBLIC KEY ----`.</span></span>

## <a name="obtaining-superuser-privileges"></a><span data-ttu-id="4ce8a-154">Получение привилегий суперпользователя</span><span class="sxs-lookup"><span data-stu-id="4ce8a-154">Obtaining superuser privileges</span></span>
<span data-ttu-id="4ce8a-155">Hello учетная запись пользователя, который указывается в процессе развертывания экземпляр виртуальной машины в Azure является привилегированной учетной записи.</span><span class="sxs-lookup"><span data-stu-id="4ce8a-155">hello user account that is specified during virtual machine instance deployment on Azure is a privileged account.</span></span> <span data-ttu-id="4ce8a-156">Hello пакет sudo установлена в hello опубликованных FreeBSD изображения.</span><span class="sxs-lookup"><span data-stu-id="4ce8a-156">hello package of sudo was installed in hello published FreeBSD image.</span></span>
<span data-ttu-id="4ce8a-157">После выполнен вход с этой учетной записью пользователя, команды запускаются как корень, используя синтаксис команды hello.</span><span class="sxs-lookup"><span data-stu-id="4ce8a-157">After you're logged in through this user account, you can run commands as root by using hello command syntax.</span></span>

```
$ sudo <COMMAND>
```

<span data-ttu-id="4ce8a-158">При необходимости можно получить доступ к оболочке root с помощью команды `sudo -s`.</span><span class="sxs-lookup"><span data-stu-id="4ce8a-158">You can optionally obtain a root shell by using `sudo -s`.</span></span>

## <a name="known-issues"></a><span data-ttu-id="4ce8a-159">Известные проблемы</span><span class="sxs-lookup"><span data-stu-id="4ce8a-159">Known issues</span></span>
<span data-ttu-id="4ce8a-160">Hello [гостевой агент виртуальной Машины Azure](https://github.com/Azure/WALinuxAgent/) версии 2.2.2 [известная проблема] (https://github.com/Azure/WALinuxAgent/pull/517), вызывает сбой подготовки hello для FreeBSD виртуальной Машины в Azure.</span><span class="sxs-lookup"><span data-stu-id="4ce8a-160">hello [Azure VM Guest Agent](https://github.com/Azure/WALinuxAgent/) version 2.2.2 has a [known issue] (https://github.com/Azure/WALinuxAgent/pull/517) that causes hello provision failure for FreeBSD VM on Azure.</span></span> <span data-ttu-id="4ce8a-161">Hello исправление было захвачено [гостевой агент виртуальной Машины Azure](https://github.com/Azure/WALinuxAgent/) версии 2.2.3 и более поздние версии.</span><span class="sxs-lookup"><span data-stu-id="4ce8a-161">hello fix was captured by [Azure VM Guest Agent](https://github.com/Azure/WALinuxAgent/) version 2.2.3 and later releases.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="4ce8a-162">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4ce8a-162">Next steps</span></span>
* <span data-ttu-id="4ce8a-163">Go слишком[Azure Marketplace](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd110/) toocreate FreeBSD виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="4ce8a-163">Go too[Azure Marketplace](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd110/) toocreate a FreeBSD VM.</span></span>
* <span data-ttu-id="4ce8a-164">Следует toobring собственные tooAzure FreeBSD ссылаться слишком[Создание и отправка виртуального жесткого диска FreeBSD tooAzure](classic/freebsd-create-upload-vhd.md).</span><span class="sxs-lookup"><span data-stu-id="4ce8a-164">If you want toobring your own FreeBSD tooAzure, refer too[Create and upload a FreeBSD VHD tooAzure](classic/freebsd-create-upload-vhd.md).</span></span>
