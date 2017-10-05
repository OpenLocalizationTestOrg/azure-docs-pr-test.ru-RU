---
title: "Настройка SSHD на виртуальных машинах Azure Linux | Документация Майкрософт"
description: "Вы можете настроить SSHD в соответствии с рекомендациями по обеспечению безопасности для блокировки SSH на виртуальных машин Azure Linux."
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 11/21/2016
ms.author: v-livech
ms.openlocfilehash: 0195c385b00ab92b2b92ce8ff00983a0d91bf3a1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="configure-sshd-on-azure-linux-vms"></a><span data-ttu-id="60f89-103">Настройка SSHD на виртуальных машинах Azure Linux</span><span class="sxs-lookup"><span data-stu-id="60f89-103">Configure SSHD on Azure Linux VMs</span></span>

<span data-ttu-id="60f89-104">В этой статье показано, как выполнить блокировку SSH Server на платформе Linux, чтобы реализовать рекомендации по обеспечению безопасности и ускорить процедуру входа SSH с использованием ключей SSH, а не паролей.</span><span class="sxs-lookup"><span data-stu-id="60f89-104">This article shows how to lockdown the SSH Server on Linux, to provide best practices security and also to speed up the SSH login process by using SSH keys instead of passwords.</span></span>  <span data-ttu-id="60f89-105">Для блокировки SSHD мы отключим возможность входа для привилегированных пользователей, ограничим вход пользователей вход с помощью списка утвержденных групп, отключим протокол SSH версии 1, установим минимальное число бит для ключа и настроим автоматический выход неактивных пользователей.</span><span class="sxs-lookup"><span data-stu-id="60f89-105">To further lockdown SSHD we are going to disable the root user from being able to login, limit the users that are allowed to login via an approved group list, disabling SSH protocol version 1, set a minimum key bit, and configure auto-logout of idle users.</span></span>  <span data-ttu-id="60f89-106">Требования для работы с этим руководством: учетная запись Azure ([получите бесплатную пробную версию](https://azure.microsoft.com/pricing/free-trial/)) и [файлы открытого и закрытого ключей SSH](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="60f89-106">The requirements for this article are: an Azure account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/)) and [SSH public and private key files](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="quick-commands"></a><span data-ttu-id="60f89-107">Быстрые команды</span><span class="sxs-lookup"><span data-stu-id="60f89-107">Quick Commands</span></span>

<span data-ttu-id="60f89-108">Настройте `/etc/ssh/sshd_config`, используя следующие параметры.</span><span class="sxs-lookup"><span data-stu-id="60f89-108">Configure `/etc/ssh/sshd_config` with the following settings:</span></span>

### <a name="disable-password-logins"></a><span data-ttu-id="60f89-109">Отключение входа с использованием пароля</span><span class="sxs-lookup"><span data-stu-id="60f89-109">Disable password logins</span></span>

```bash
PasswordAuthentication no
```

### <a name="disable-login-by-the-root-user"></a><span data-ttu-id="60f89-110">Отключение входа для привилегированного пользователя</span><span class="sxs-lookup"><span data-stu-id="60f89-110">Disable login by the root user</span></span>

```bash
PermitRootLogin no
```

### <a name="allowed-groups-list"></a><span data-ttu-id="60f89-111">Список разрешенных групп</span><span class="sxs-lookup"><span data-stu-id="60f89-111">Allowed groups list</span></span>

```bash
AllowGroups wheel
```

### <a name="allowed-users-list"></a><span data-ttu-id="60f89-112">Список разрешенных пользователей</span><span class="sxs-lookup"><span data-stu-id="60f89-112">Allowed users list</span></span>

```bash
AllowUsers ahmet ralph
```

### <a name="disable-ssh-protocol-version-1"></a><span data-ttu-id="60f89-113">Отключение протокола SSH версии 1</span><span class="sxs-lookup"><span data-stu-id="60f89-113">Disable SSH protocol version 1</span></span>

```bash
Protocol 2
```

### <a name="minimum-key-bits"></a><span data-ttu-id="60f89-114">Минимальное число битов в ключе</span><span class="sxs-lookup"><span data-stu-id="60f89-114">Minimum key bits</span></span>

```bash
ServerKeyBits 2048
```

### <a name="disconnect-idle-users"></a><span data-ttu-id="60f89-115">Отключение неактивных пользователей</span><span class="sxs-lookup"><span data-stu-id="60f89-115">Disconnect idle users</span></span>

```bash
ClientAliveInterval 300
ClientAliveCountMax 0
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="60f89-116">Подробное пошаговое руководство</span><span class="sxs-lookup"><span data-stu-id="60f89-116">Detailed Walkthrough</span></span>

<span data-ttu-id="60f89-117">SSHD — это SSH-сервер, работающий на виртуальной машине Linux.</span><span class="sxs-lookup"><span data-stu-id="60f89-117">SSHD is the SSH Server that runs on the Linux VM.</span></span>  <span data-ttu-id="60f89-118">SSH — это клиент, который запускается из оболочки на рабочей станции MacBook или Linux, а также из Bash в Windows.</span><span class="sxs-lookup"><span data-stu-id="60f89-118">SSH is a client that runs from a shell on your MacBook, Linux workstation, or from a Bash on Windows.</span></span>  <span data-ttu-id="60f89-119">SSH — это также протокол, используемый для защиты и шифрования обмена данными между рабочей станцией и виртуальной машиной Linux. Иными словами, SSH также является VPN (виртуальной частной сетью).</span><span class="sxs-lookup"><span data-stu-id="60f89-119">SSH is also the protocol used to secure and encrypt the communication between your workstation and the Linux VM making SSH also a VPN (Virtual Private Network).</span></span>

<span data-ttu-id="60f89-120">Для работы с этим руководством статьи очень важно не закрывать один сеанс работы с виртуальной машиной Linux, пока вы не выполните все инструкции.</span><span class="sxs-lookup"><span data-stu-id="60f89-120">For this article, it is very important to keep one login to your Linux VM open for the entire walk-through.</span></span>  <span data-ttu-id="60f89-121">Установленное SSH-подключение сохраняется, пока открыто окно сеанса.</span><span class="sxs-lookup"><span data-stu-id="60f89-121">Once an SSH connection is established, it remains as an open session as long as the window is not closed.</span></span>  <span data-ttu-id="60f89-122">Работа с одним терминалом позволяет вносить изменения в службу SSHD без блокировки в случае критических изменений.</span><span class="sxs-lookup"><span data-stu-id="60f89-122">Having one terminal logged in, allows for changes to be made to the SSHD service without being locked out if a breaking change is made.</span></span>  <span data-ttu-id="60f89-123">Если ВМ Linux заблокирована с помощью неработающей конфигурации SSHD, Azure поможет вам сбросить ее, используя [расширения для доступа к ВМ Azure](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="60f89-123">If you do get locked out of your Linux VM with a broken SSHD configuration, Azure offers the ability to reset a broken SSHD configuration with the [Azure VM Access Extension](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="60f89-124">Для этого мы откроем два терминала и установим подключение SSH к ВМ Linux в каждом из них.</span><span class="sxs-lookup"><span data-stu-id="60f89-124">For this reason we open two terminals and SSH to the Linux VM from both of them.</span></span>  <span data-ttu-id="60f89-125">Первый терминал будет использоваться для изменений файла конфигурации SSHD и перезапуска службы SSHD.</span><span class="sxs-lookup"><span data-stu-id="60f89-125">We use the first terminal to make the changes to SSHDs configuration file and restart the SSHD service.</span></span>  <span data-ttu-id="60f89-126">Второй терминал будет использоваться для тестирования этих изменений после перезапуска службы.</span><span class="sxs-lookup"><span data-stu-id="60f89-126">We use the second terminal to test those changes once the service is restarted.</span></span>  <span data-ttu-id="60f89-127">Поскольку мы отключаем SSH-пароли и полагаемся исключительно на SSH-ключи, если ваши SSH-ключи неверны и вы закроете подключение к виртуальной машине, эта виртуальная машины окажется безвозвратно заблокированной. Никто не сможет войти в нее, поэтому ее придется удалить и создать заново.</span><span class="sxs-lookup"><span data-stu-id="60f89-127">Because we are disabling SSH passwords and relying strictly on SSH keys, if your SSH keys are not correct and you close the connection to the VM, the VM will be permanently locked and no one will be able to login to it requiring it to be deleted and recreated.</span></span>

## <a name="disable-password-logins"></a><span data-ttu-id="60f89-128">Отключение входа с использованием пароля</span><span class="sxs-lookup"><span data-stu-id="60f89-128">Disable password logins</span></span>

<span data-ttu-id="60f89-129">Отключить вход с использованием пароля — самый быстрый способ защитить ВМ Linux.</span><span class="sxs-lookup"><span data-stu-id="60f89-129">The quickest way to secure you Linux VM is to disable password logins.</span></span>  <span data-ttu-id="60f89-130">Когда вход с использованием пароля включен, программы-роботы, которые сканируют содержимое в Интернете, немедленно начнут попытки подобрать пароль к виртуальной ВМ Linux с помощью SSH.</span><span class="sxs-lookup"><span data-stu-id="60f89-130">When password logins are enabled, bots crawling the web will immediately start attempting to brute force guess the password for your Linux VM using SSH.</span></span>  <span data-ttu-id="60f89-131">Когда вход с помощью пароля отключен, сервер SSH игнорирует все попытки входа с использованием пароля.</span><span class="sxs-lookup"><span data-stu-id="60f89-131">Disabling password logins completely, enables the SSH server to ignore all password login attempts.</span></span>

```bash
PasswordAuthentication no
```

## <a name="disable-login-by-the-root-user"></a><span data-ttu-id="60f89-132">Отключение входа для привилегированного пользователя</span><span class="sxs-lookup"><span data-stu-id="60f89-132">Disable login by the root user</span></span>

<span data-ttu-id="60f89-133">В соответствии с рекомендациями по работе с Linux, пользователи `root` не должны входить с помощью SSH или `sudo su`.</span><span class="sxs-lookup"><span data-stu-id="60f89-133">Following Linux best practices, the `root` user should never be logged into over SSH or using `sudo su`.</span></span>  <span data-ttu-id="60f89-134">Все команды, требующие привилегированного доступа, всегда должны выполняться с использованием команды `sudo`, которая регистрирует все действия для будущего аудита.</span><span class="sxs-lookup"><span data-stu-id="60f89-134">All commands needing root level permissions should always be run through the `sudo` command, which logs all actions for future auditing.</span></span>  <span data-ttu-id="60f89-135">Отключение для пользователя `root` возможности входа с помощью SSH — это лучший способ защиты, который разрешает эту процедуру только авторизованным пользователям.</span><span class="sxs-lookup"><span data-stu-id="60f89-135">Disabling the `root` user from logging in via SSH is a security best practices step that ensures only authorized users are allowed to SSH.</span></span>

```bash
PermitRootLogin no
```

## <a name="allowed-groups-list"></a><span data-ttu-id="60f89-136">Список разрешенных групп</span><span class="sxs-lookup"><span data-stu-id="60f89-136">Allowed groups list</span></span>

<span data-ttu-id="60f89-137">SSH предусматривает способ ограничить для пользователей и групп возможность входа с помощью SSH.</span><span class="sxs-lookup"><span data-stu-id="60f89-137">SSH offers a method of restricting users and group that are allowed or disallowed from logging in over SSH.</span></span>  <span data-ttu-id="60f89-138">Эта функция использует списки для утверждения или отклонения запросов на вход, поступающих от определенных пользователей и групп.</span><span class="sxs-lookup"><span data-stu-id="60f89-138">This feature uses lists to approve or deny specific users and groups from logging in.</span></span>  <span data-ttu-id="60f89-139">Включив группу wheel в список `AllowGroups`, вы разрешите возможность входа по протоколу SSH только для учетных записей пользователей, входящих в группу wheel.</span><span class="sxs-lookup"><span data-stu-id="60f89-139">Setting the wheel group to the `AllowGroups` list restricts approved logins over SSH to just user accounts that are in the wheel group.</span></span>

```bash
AllowGroups wheel
```

## <a name="allowed-users-list"></a><span data-ttu-id="60f89-140">Список разрешенных пользователей</span><span class="sxs-lookup"><span data-stu-id="60f89-140">Allowed users list</span></span>

<span data-ttu-id="60f89-141">Ограничение входа по протоколу SSH только для пользователей — это частный пример выполнения этой задачи с помощью `AllowGroups`.</span><span class="sxs-lookup"><span data-stu-id="60f89-141">Restricting SSH logins to just users is a more specific way to accomplish the same task that `AllowGroups` is.</span></span>  

```bash
AllowUsers ahmet ralph
```

## <a name="disable-ssh-protocol-version-1"></a><span data-ttu-id="60f89-142">Отключение протокола SSH версии 1</span><span class="sxs-lookup"><span data-stu-id="60f89-142">Disable SSH protocol version 1</span></span>

<span data-ttu-id="60f89-143">Протокол SSH версии 1 является небезопасным и должен быть отключен.</span><span class="sxs-lookup"><span data-stu-id="60f89-143">SSH protocol version 1 is insecure and should be disabled.</span></span>  <span data-ttu-id="60f89-144">Протокол SSH версии 2 — это текущая версия, которая обеспечивает безопасный способ использования SSH на сервере.</span><span class="sxs-lookup"><span data-stu-id="60f89-144">SSH protocol version 2 is the current version that offers a secure way to SSH to your server.</span></span>  <span data-ttu-id="60f89-145">Отключение SSH версии 1 запрещает любым SSH-клиентам подключаться к серверу SSH с помощью SSH версии 1.</span><span class="sxs-lookup"><span data-stu-id="60f89-145">Disabling SSH version 1 denies any SSH clients that are attempting to establish a connection with the SSH server using SSH version 1.</span></span>  <span data-ttu-id="60f89-146">Подключаться к серверу SSH разрешено только через SSH версии 2.</span><span class="sxs-lookup"><span data-stu-id="60f89-146">Only SSH version 2 connections are allowed to negotiate a connection with the SSH server.</span></span>

```bash
Protocol 2
```

## <a name="minimum-key-bits"></a><span data-ttu-id="60f89-147">Минимальное число битов в ключе</span><span class="sxs-lookup"><span data-stu-id="60f89-147">Minimum key bits</span></span>

<span data-ttu-id="60f89-148">Рекомендации по обеспечению безопасности требуют отключать вход SSH с использованием пароля и выполнять проверку подлинности на SSH-сервере только с использованием SSH-ключей.</span><span class="sxs-lookup"><span data-stu-id="60f89-148">Following security best practices, password SSH logins are disabled and only SSH keys are allowed to be used to authenticate with the SSH server.</span></span>  <span data-ttu-id="60f89-149">Эти SSH-ключи могут быть разной длины (измеряется в битах).</span><span class="sxs-lookup"><span data-stu-id="60f89-149">These SSH keys can be created using different length keys, measured in bits.</span></span>  <span data-ttu-id="60f89-150">Рекомендуется использовать ключи длиной не менее 2048 бит.</span><span class="sxs-lookup"><span data-stu-id="60f89-150">Best practices states that keys of 2048 bits in length are the minimum acceptable key strength.</span></span>  <span data-ttu-id="60f89-151">Ключи меньше 2048 бит теоретически могут быть повреждены.</span><span class="sxs-lookup"><span data-stu-id="60f89-151">Keys of less than 2048 bits could theoretically be broken.</span></span>  <span data-ttu-id="60f89-152">Присвоив параметру `ServerKeyBits` значение `2048`, вы разрешите все подключения с использованием ключей длиной от 2048 бит и, соответственно, запретите использование более коротких ключей (до 2048 бит).</span><span class="sxs-lookup"><span data-stu-id="60f89-152">Setting the `ServerKeyBits` to `2048` allows any connections using keys of 2048 bits or greater and deny connections of less than 2048 bits.</span></span>

```bash
ServerKeyBits 2048
```

## <a name="disconnect-idle-users"></a><span data-ttu-id="60f89-153">Отключение неактивных пользователей</span><span class="sxs-lookup"><span data-stu-id="60f89-153">Disconnect idle users</span></span>

<span data-ttu-id="60f89-154">SSH может отключать пользователей с открытыми подключениями, которые остаются в состоянии простоя в течение заданного периода в секундах.</span><span class="sxs-lookup"><span data-stu-id="60f89-154">SSH has the ability to disconnect users that have open connections that have remained idle for more than a set period of seconds.</span></span>  <span data-ttu-id="60f89-155">Сохранение открытых сеансов только для активных пользователей ограничивает возможность доступа к ВМ Linux.</span><span class="sxs-lookup"><span data-stu-id="60f89-155">Keeping open sessions to only those users who are active limits the exposure of the Linux VM.</span></span>

```bash
ClientAliveInterval 300
ClientAliveCountMax 0
```

## <a name="restart-sshd"></a><span data-ttu-id="60f89-156">Перезапуск SSHD</span><span class="sxs-lookup"><span data-stu-id="60f89-156">Restart SSHD</span></span>

<span data-ttu-id="60f89-157">Чтобы включить параметры в `/etc/ssh/sshd_config`, перезапустите процесс SSHD, что, в свою очередь, перезапустит сервер SSH.</span><span class="sxs-lookup"><span data-stu-id="60f89-157">To enable the settings in `/etc/ssh/sshd_config` restart the SSHD process which restarts the SSH server.</span></span>  <span data-ttu-id="60f89-158">Окно терминала, используемое для перезапуска сервера SSH, останется открытым без потери сеанса SSH.</span><span class="sxs-lookup"><span data-stu-id="60f89-158">The terminal window you use to restart the SSH server remain open without losing the open SSH session.</span></span>  <span data-ttu-id="60f89-159">Чтобы проверить новые параметры SSH сервера, используйте второе окно или вкладку терминала.</span><span class="sxs-lookup"><span data-stu-id="60f89-159">To test the new SSH server settings use a second terminal window or tab.</span></span>  <span data-ttu-id="60f89-160">Используя разные терминалы для проверки SSH-подключения, вы сможете вернуться и внести в первом терминале дополнительные изменения в `/etc/ssh/sshd_config` без блокировки SSHD при внесении критических изменений.</span><span class="sxs-lookup"><span data-stu-id="60f89-160">Using a separate terminal to test the SSH connection allows you to go back and make additional changes to the `/etc/ssh/sshd_config` in the first terminal, without being locked out by a breaking SSHD change.</span></span>  

### <a name="on-redhat-centos-and-fedora"></a><span data-ttu-id="60f89-161">В Redhat, Centos и Fedora</span><span class="sxs-lookup"><span data-stu-id="60f89-161">On Redhat, Centos and Fedora</span></span>

```bash
service sshd restart
```

### <a name="on-debian--ubuntu"></a><span data-ttu-id="60f89-162">В Debian и Ubuntu</span><span class="sxs-lookup"><span data-stu-id="60f89-162">On Debian & Ubuntu</span></span>

```bash
service ssh restart
```

## <a name="reset-sshd-using-azure-reset-access"></a><span data-ttu-id="60f89-163">Сброс SSHD с помощью команды Azure reset-access</span><span class="sxs-lookup"><span data-stu-id="60f89-163">Reset SSHD using Azure reset-access</span></span>

<span data-ttu-id="60f89-164">Если у вас заблокирована возможность вносить критические изменения в конфигурацию SSHD, можно использовать расширение доступа к ВМ Azure, чтобы сбросить конфигурацию SSHD до исходной.</span><span class="sxs-lookup"><span data-stu-id="60f89-164">If you are locked out from a breaking change to the SSHD configuration you can use the Azure VM access-extension to reset the SSHD configuration back to the original configuration.</span></span>

<span data-ttu-id="60f89-165">Замените все имена в примере собственными.</span><span class="sxs-lookup"><span data-stu-id="60f89-165">Replace any example names with your own.</span></span>

```azurecli
azure vm reset-access \
--resource-group myResourceGroup \
--name myVM \
--reset-ssh
```

## <a name="install-fail2ban"></a><span data-ttu-id="60f89-166">Установка Fail2ban</span><span class="sxs-lookup"><span data-stu-id="60f89-166">Install Fail2ban</span></span>

<span data-ttu-id="60f89-167">Настоятельно рекомендуется установить и настроить приложение с открытым исходным кодом Fail2ban, которое блокирует повторные попытки входа на ВМ Linux по протоколу SSH методом подбора.</span><span class="sxs-lookup"><span data-stu-id="60f89-167">It is strongly recommended to install and setup the open source app Fail2ban, which blocks repeated attempts to login to your Linux VM over SSH using brute force.</span></span>  <span data-ttu-id="60f89-168">Fail2ban регистрирует повторяющиеся неудачные попытки входа по протоколу SSH, а затем создает правила брандмауэра, чтобы заблокировать IP-адрес, связанный с этими попытками.</span><span class="sxs-lookup"><span data-stu-id="60f89-168">Fail2ban logs repeated failed attempts to login over SSH and then creates firewall rules to block the IP address that the attempts are originating from.</span></span>

* [<span data-ttu-id="60f89-169">Домашняя страница Fail2ban</span><span class="sxs-lookup"><span data-stu-id="60f89-169">Fail2ban homepage</span></span>](http://www.fail2ban.org/wiki/index.php/Main_Page)

## <a name="next-steps"></a><span data-ttu-id="60f89-170">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="60f89-170">Next Steps</span></span>

<span data-ttu-id="60f89-171">Теперь, когда вы настроили и заблокировали сервер SSH на ВМ Linux, можно переходить к изучению дополнительных рекомендаций по обеспечению безопасности.</span><span class="sxs-lookup"><span data-stu-id="60f89-171">Now that you have configured and locked down the SSH server on your Linux VM there are additional security best practices you can follow.</span></span>  

* [<span data-ttu-id="60f89-172">Управление пользователями, SSH и проверка или восстановление дисков в виртуальных машинах Azure с помощью расширения VMAccess</span><span class="sxs-lookup"><span data-stu-id="60f89-172">Manage users, SSH, and check or repair disks on Azure Linux VMs using the VMAccess Extension</span></span>](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

* <span data-ttu-id="60f89-173">[Encrypt disks on a Linux VM using the Azure CLI](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Шифрование дисков на виртуальной машине Linux с помощью интерфейса командной строки Azure)</span><span class="sxs-lookup"><span data-stu-id="60f89-173">[Encrypt disks on a Linux VM using the Azure CLI](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

* [<span data-ttu-id="60f89-174">Доступ и безопасность в шаблонах Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="60f89-174">Access and security in Azure Resource Manager templates</span></span>](dotnet-core-3-access-security.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
