---
title: "aaaConfigure SSHD виртуальных машин Linux в Azure | Документы Microsoft"
description: "Настройте SSHD рекомендации по обеспечению безопасности и tooAzure SSH toolockdown виртуальных машин Linux."
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
ms.openlocfilehash: c2361be7199a24b129c06acfc899dd32f6e1d6fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-sshd-on-azure-linux-vms"></a><span data-ttu-id="c5fa2-103">Настройка SSHD на виртуальных машинах Azure Linux</span><span class="sxs-lookup"><span data-stu-id="c5fa2-103">Configure SSHD on Azure Linux VMs</span></span>

<span data-ttu-id="c5fa2-104">В этой статье показано, как toolockdown hello SSH сервера в Linux, tooprovide советы и рекомендации безопасности, а также toospeed процесс входа hello SSH с использованием ключей SSH вместо паролей.</span><span class="sxs-lookup"><span data-stu-id="c5fa2-104">This article shows how toolockdown hello SSH Server on Linux, tooprovide best practices security and also toospeed up hello SSH login process by using SSH keys instead of passwords.</span></span>  <span data-ttu-id="c5fa2-105">блокировки toofurther SSHD, мы будем toodisable hello привилегированного пользователя не может toologin максимальное разрешенное toologin через список утвержденных групп пользователей hello отключение протокол SSH версии 1, немного минимального ключа и настройте auto выхода неактивных пользователей.</span><span class="sxs-lookup"><span data-stu-id="c5fa2-105">toofurther lockdown SSHD we are going toodisable hello root user from being able toologin, limit hello users that are allowed toologin via an approved group list, disabling SSH protocol version 1, set a minimum key bit, and configure auto-logout of idle users.</span></span>  <span data-ttu-id="c5fa2-106">Hello требования для этой статьи: учетная запись Azure ([получить бесплатную пробную версию](https://azure.microsoft.com/pricing/free-trial/)) и [файлы SSH открытого и закрытого ключей](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c5fa2-106">hello requirements for this article are: an Azure account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/)) and [SSH public and private key files](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="quick-commands"></a><span data-ttu-id="c5fa2-107">Быстрые команды</span><span class="sxs-lookup"><span data-stu-id="c5fa2-107">Quick Commands</span></span>

<span data-ttu-id="c5fa2-108">Настройка `/etc/ssh/sshd_config` с hello следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="c5fa2-108">Configure `/etc/ssh/sshd_config` with hello following settings:</span></span>

### <a name="disable-password-logins"></a><span data-ttu-id="c5fa2-109">Отключение входа с использованием пароля</span><span class="sxs-lookup"><span data-stu-id="c5fa2-109">Disable password logins</span></span>

```bash
PasswordAuthentication no
```

### <a name="disable-login-by-hello-root-user"></a><span data-ttu-id="c5fa2-110">Отключить вход с hello привилегированного пользователя</span><span class="sxs-lookup"><span data-stu-id="c5fa2-110">Disable login by hello root user</span></span>

```bash
PermitRootLogin no
```

### <a name="allowed-groups-list"></a><span data-ttu-id="c5fa2-111">Список разрешенных групп</span><span class="sxs-lookup"><span data-stu-id="c5fa2-111">Allowed groups list</span></span>

```bash
AllowGroups wheel
```

### <a name="allowed-users-list"></a><span data-ttu-id="c5fa2-112">Список разрешенных пользователей</span><span class="sxs-lookup"><span data-stu-id="c5fa2-112">Allowed users list</span></span>

```bash
AllowUsers ahmet ralph
```

### <a name="disable-ssh-protocol-version-1"></a><span data-ttu-id="c5fa2-113">Отключение протокола SSH версии 1</span><span class="sxs-lookup"><span data-stu-id="c5fa2-113">Disable SSH protocol version 1</span></span>

```bash
Protocol 2
```

### <a name="minimum-key-bits"></a><span data-ttu-id="c5fa2-114">Минимальное число битов в ключе</span><span class="sxs-lookup"><span data-stu-id="c5fa2-114">Minimum key bits</span></span>

```bash
ServerKeyBits 2048
```

### <a name="disconnect-idle-users"></a><span data-ttu-id="c5fa2-115">Отключение неактивных пользователей</span><span class="sxs-lookup"><span data-stu-id="c5fa2-115">Disconnect idle users</span></span>

```bash
ClientAliveInterval 300
ClientAliveCountMax 0
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="c5fa2-116">Подробное пошаговое руководство</span><span class="sxs-lookup"><span data-stu-id="c5fa2-116">Detailed Walkthrough</span></span>

<span data-ttu-id="c5fa2-117">SSHD — hello SSH сервера, работающего на виртуальной Машине Linux hello.</span><span class="sxs-lookup"><span data-stu-id="c5fa2-117">SSHD is hello SSH Server that runs on hello Linux VM.</span></span>  <span data-ttu-id="c5fa2-118">SSH — это клиент, который запускается из оболочки на рабочей станции MacBook или Linux, а также из Bash в Windows.</span><span class="sxs-lookup"><span data-stu-id="c5fa2-118">SSH is a client that runs from a shell on your MacBook, Linux workstation, or from a Bash on Windows.</span></span>  <span data-ttu-id="c5fa2-119">Также является SSH hello протокол используется toosecure и шифрования hello обмена данными между рабочей станцией и hello виртуальных Машин Linux, делая SSH также виртуальной частной сети (виртуальной частной сети).</span><span class="sxs-lookup"><span data-stu-id="c5fa2-119">SSH is also hello protocol used toosecure and encrypt hello communication between your workstation and hello Linux VM making SSH also a VPN (Virtual Private Network).</span></span>

<span data-ttu-id="c5fa2-120">В этой статье это очень важно tookeep одно имя входа tooyour ВМ Linux открыть руководство всей hello.</span><span class="sxs-lookup"><span data-stu-id="c5fa2-120">For this article, it is very important tookeep one login tooyour Linux VM open for hello entire walk-through.</span></span>  <span data-ttu-id="c5fa2-121">После установления SSH-подключения, он остается открытым сеанс до тех пор, пока не закрывается окно приветствия.</span><span class="sxs-lookup"><span data-stu-id="c5fa2-121">Once an SSH connection is established, it remains as an open session as long as hello window is not closed.</span></span>  <span data-ttu-id="c5fa2-122">Наличие одного терминала вход, позволяет toohello toobe внесенные изменения SSHD службы без попытки блокируются при внесении критических изменений.</span><span class="sxs-lookup"><span data-stu-id="c5fa2-122">Having one terminal logged in, allows for changes toobe made toohello SSHD service without being locked out if a breaking change is made.</span></span>  <span data-ttu-id="c5fa2-123">Если вы блокируются ВМ Linux с конфигурацией SSHD нарушена, Azure предлагает возможность tooreset hello неработающие SSHD конфигурации с hello [расширения Access ВМ Azure](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c5fa2-123">If you do get locked out of your Linux VM with a broken SSHD configuration, Azure offers hello ability tooreset a broken SSHD configuration with hello [Azure VM Access Extension](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="c5fa2-124">По этой причине мы откройте два терминальных и SSH toohello виртуальной Машине Linux из них.</span><span class="sxs-lookup"><span data-stu-id="c5fa2-124">For this reason we open two terminals and SSH toohello Linux VM from both of them.</span></span>  <span data-ttu-id="c5fa2-125">Мы используем hello первый терминалов toomake hello изменения tooSSHDs файла конфигурации и перезапустите службу hello SSHD.</span><span class="sxs-lookup"><span data-stu-id="c5fa2-125">We use hello first terminal toomake hello changes tooSSHDs configuration file and restart hello SSHD service.</span></span>  <span data-ttu-id="c5fa2-126">Мы используем терминалов tootest с второй hello эти изменения, после перезапуска службы hello.</span><span class="sxs-lookup"><span data-stu-id="c5fa2-126">We use hello second terminal tootest those changes once hello service is restarted.</span></span>  <span data-ttu-id="c5fa2-127">Так как мы выполняется отключение SSH пароли и полагаться исключительно на ключи SSH, если ключи SSH неверны и закрыть toohello hello подключения виртуальной Машины, hello виртуальной Машины будут окончательно заблокирован и никто будут tooit toologin может запрашивать ее toobe удалена и создана заново.</span><span class="sxs-lookup"><span data-stu-id="c5fa2-127">Because we are disabling SSH passwords and relying strictly on SSH keys, if your SSH keys are not correct and you close hello connection toohello VM, hello VM will be permanently locked and no one will be able toologin tooit requiring it toobe deleted and recreated.</span></span>

## <a name="disable-password-logins"></a><span data-ttu-id="c5fa2-128">Отключение входа с использованием пароля</span><span class="sxs-lookup"><span data-stu-id="c5fa2-128">Disable password logins</span></span>

<span data-ttu-id="c5fa2-129">Здравствуйте, быстрый способ toosecure вы виртуальных Машин Linux — toodisable пароль входа.</span><span class="sxs-lookup"><span data-stu-id="c5fa2-129">hello quickest way toosecure you Linux VM is toodisable password logins.</span></span>  <span data-ttu-id="c5fa2-130">При включении пароль входа программы-роботы обходе hello web немедленно начать попытка toobrute принудительно предположение hello пароль для ВМ Linux с помощью SSH.</span><span class="sxs-lookup"><span data-stu-id="c5fa2-130">When password logins are enabled, bots crawling hello web will immediately start attempting toobrute force guess hello password for your Linux VM using SSH.</span></span>  <span data-ttu-id="c5fa2-131">Отключает имена входа пароль полностью, позволяет tooignore сервера SSH hello всех попыток входа пароль.</span><span class="sxs-lookup"><span data-stu-id="c5fa2-131">Disabling password logins completely, enables hello SSH server tooignore all password login attempts.</span></span>

```bash
PasswordAuthentication no
```

## <a name="disable-login-by-hello-root-user"></a><span data-ttu-id="c5fa2-132">Отключить вход с hello привилегированного пользователя</span><span class="sxs-lookup"><span data-stu-id="c5fa2-132">Disable login by hello root user</span></span>

<span data-ttu-id="c5fa2-133">Следующие рекомендации Linux hello `root` пользователя никогда не будут занесены в через SSH или с помощью `sudo su`.</span><span class="sxs-lookup"><span data-stu-id="c5fa2-133">Following Linux best practices, hello `root` user should never be logged into over SSH or using `sudo su`.</span></span>  <span data-ttu-id="c5fa2-134">Все команды, которым требуются разрешения на уровне корневого всегда должен выполняться через hello `sudo` команду, которая регистрирует все действия выполнять дальнейший аудит.</span><span class="sxs-lookup"><span data-stu-id="c5fa2-134">All commands needing root level permissions should always be run through hello `sudo` command, which logs all actions for future auditing.</span></span>  <span data-ttu-id="c5fa2-135">Отключение hello `root` лучшие методики шаг для обеспечения безопасности, гарантирует только авторизованным пользователям разрешено tooSSH является пользователь войти в систему по протоколу SSH.</span><span class="sxs-lookup"><span data-stu-id="c5fa2-135">Disabling hello `root` user from logging in via SSH is a security best practices step that ensures only authorized users are allowed tooSSH.</span></span>

```bash
PermitRootLogin no
```

## <a name="allowed-groups-list"></a><span data-ttu-id="c5fa2-136">Список разрешенных групп</span><span class="sxs-lookup"><span data-stu-id="c5fa2-136">Allowed groups list</span></span>

<span data-ttu-id="c5fa2-137">SSH предусматривает способ ограничить для пользователей и групп возможность входа с помощью SSH.</span><span class="sxs-lookup"><span data-stu-id="c5fa2-137">SSH offers a method of restricting users and group that are allowed or disallowed from logging in over SSH.</span></span>  <span data-ttu-id="c5fa2-138">Эта функция использует списки tooapprove или запретить вход определенных пользователей и групп.</span><span class="sxs-lookup"><span data-stu-id="c5fa2-138">This feature uses lists tooapprove or deny specific users and groups from logging in.</span></span>  <span data-ttu-id="c5fa2-139">Параметр toohello группы колесо hello `AllowGroups` список ограничивает утвержденные имена входа по SSH toojust учетных записей, которые находятся в одной группе hello колесико мыши.</span><span class="sxs-lookup"><span data-stu-id="c5fa2-139">Setting hello wheel group toohello `AllowGroups` list restricts approved logins over SSH toojust user accounts that are in hello wheel group.</span></span>

```bash
AllowGroups wheel
```

## <a name="allowed-users-list"></a><span data-ttu-id="c5fa2-140">Список разрешенных пользователей</span><span class="sxs-lookup"><span data-stu-id="c5fa2-140">Allowed users list</span></span>

<span data-ttu-id="c5fa2-141">Ограничение toojust учетные данные SSH пользователи является более особым образом tooaccomplish hello же задача, которая `AllowGroups` —.</span><span class="sxs-lookup"><span data-stu-id="c5fa2-141">Restricting SSH logins toojust users is a more specific way tooaccomplish hello same task that `AllowGroups` is.</span></span>  

```bash
AllowUsers ahmet ralph
```

## <a name="disable-ssh-protocol-version-1"></a><span data-ttu-id="c5fa2-142">Отключение протокола SSH версии 1</span><span class="sxs-lookup"><span data-stu-id="c5fa2-142">Disable SSH protocol version 1</span></span>

<span data-ttu-id="c5fa2-143">Протокол SSH версии 1 является небезопасным и должен быть отключен.</span><span class="sxs-lookup"><span data-stu-id="c5fa2-143">SSH protocol version 1 is insecure and should be disabled.</span></span>  <span data-ttu-id="c5fa2-144">Протокол SSH версии 2 — hello текущей версии, которая предлагает серверу tooyour tooSSH безопасным способом.</span><span class="sxs-lookup"><span data-stu-id="c5fa2-144">SSH protocol version 2 is hello current version that offers a secure way tooSSH tooyour server.</span></span>  <span data-ttu-id="c5fa2-145">Отключение SSH версии 1 запрещает любые SSH клиенты, пытающиеся tooestablish соединение с сервером SSH hello, с помощью SSH версии 1.</span><span class="sxs-lookup"><span data-stu-id="c5fa2-145">Disabling SSH version 1 denies any SSH clients that are attempting tooestablish a connection with hello SSH server using SSH version 1.</span></span>  <span data-ttu-id="c5fa2-146">Только для соединений по протоколу SSH версии 2 разрешены toonegotiate подключение к серверу SSH hello.</span><span class="sxs-lookup"><span data-stu-id="c5fa2-146">Only SSH version 2 connections are allowed toonegotiate a connection with hello SSH server.</span></span>

```bash
Protocol 2
```

## <a name="minimum-key-bits"></a><span data-ttu-id="c5fa2-147">Минимальное число битов в ключе</span><span class="sxs-lookup"><span data-stu-id="c5fa2-147">Minimum key bits</span></span>

<span data-ttu-id="c5fa2-148">Следующие рекомендации по обеспечению безопасности пароль входа по протоколу SSH отключены и разрешены только ключи SSH toobe использовать tooauthenticate с сервера SSH hello.</span><span class="sxs-lookup"><span data-stu-id="c5fa2-148">Following security best practices, password SSH logins are disabled and only SSH keys are allowed toobe used tooauthenticate with hello SSH server.</span></span>  <span data-ttu-id="c5fa2-149">Эти SSH-ключи могут быть разной длины (измеряется в битах).</span><span class="sxs-lookup"><span data-stu-id="c5fa2-149">These SSH keys can be created using different length keys, measured in bits.</span></span>  <span data-ttu-id="c5fa2-150">Советы и рекомендации, ключи длиной 2048 бит стойкость ключа минимального допустимого hello состояний.</span><span class="sxs-lookup"><span data-stu-id="c5fa2-150">Best practices states that keys of 2048 bits in length are hello minimum acceptable key strength.</span></span>  <span data-ttu-id="c5fa2-151">Ключи меньше 2048 бит теоретически могут быть повреждены.</span><span class="sxs-lookup"><span data-stu-id="c5fa2-151">Keys of less than 2048 bits could theoretically be broken.</span></span>  <span data-ttu-id="c5fa2-152">Параметр hello `ServerKeyBits` слишком`2048` разрешены все соединения, с использованием ключей 2048 бит или больше и запретить подключения меньше 2048 бит.</span><span class="sxs-lookup"><span data-stu-id="c5fa2-152">Setting hello `ServerKeyBits` too`2048` allows any connections using keys of 2048 bits or greater and deny connections of less than 2048 bits.</span></span>

```bash
ServerKeyBits 2048
```

## <a name="disconnect-idle-users"></a><span data-ttu-id="c5fa2-153">Отключение неактивных пользователей</span><span class="sxs-lookup"><span data-stu-id="c5fa2-153">Disconnect idle users</span></span>

<span data-ttu-id="c5fa2-154">SSH имеет hello возможность toodisconnect пользователей, имеющих открытые соединения, остаются простоя в течение определенного периода секунд.</span><span class="sxs-lookup"><span data-stu-id="c5fa2-154">SSH has hello ability toodisconnect users that have open connections that have remained idle for more than a set period of seconds.</span></span>  <span data-ttu-id="c5fa2-155">Сохранение открытых сеансов tooonly тем пользователям, которые являются раскрытия hello active ограничения hello виртуальной Машины с Linux.</span><span class="sxs-lookup"><span data-stu-id="c5fa2-155">Keeping open sessions tooonly those users who are active limits hello exposure of hello Linux VM.</span></span>

```bash
ClientAliveInterval 300
ClientAliveCountMax 0
```

## <a name="restart-sshd"></a><span data-ttu-id="c5fa2-156">Перезапуск SSHD</span><span class="sxs-lookup"><span data-stu-id="c5fa2-156">Restart SSHD</span></span>

<span data-ttu-id="c5fa2-157">Параметры tooenable hello в `/etc/ssh/sshd_config` перезапуска процесса SSHD hello, который перезапускает сервер SSH hello.</span><span class="sxs-lookup"><span data-stu-id="c5fa2-157">tooenable hello settings in `/etc/ssh/sshd_config` restart hello SSHD process which restarts hello SSH server.</span></span>  <span data-ttu-id="c5fa2-158">использовать сервер SSH hello toorestart окно терминала Hello остаются открытыми без потери Привет открыть сеанс SSH.</span><span class="sxs-lookup"><span data-stu-id="c5fa2-158">hello terminal window you use toorestart hello SSH server remain open without losing hello open SSH session.</span></span>  <span data-ttu-id="c5fa2-159">параметры нового сервера SSH tootest hello используйте второе окно терминала или на отдельной вкладке.  С помощью отдельных терминалов tootest hello SSH-подключения можно toogo назад и внести дополнительные изменения toohello `/etc/ssh/sshd_config` в первый терминалов hello, без блокировки SSHD критических изменений.</span><span class="sxs-lookup"><span data-stu-id="c5fa2-159">tootest hello new SSH server settings use a second terminal window or tab.  Using a separate terminal tootest hello SSH connection allows you toogo back and make additional changes toohello `/etc/ssh/sshd_config` in hello first terminal, without being locked out by a breaking SSHD change.</span></span>  

### <a name="on-redhat-centos-and-fedora"></a><span data-ttu-id="c5fa2-160">В Redhat, Centos и Fedora</span><span class="sxs-lookup"><span data-stu-id="c5fa2-160">On Redhat, Centos and Fedora</span></span>

```bash
service sshd restart
```

### <a name="on-debian--ubuntu"></a><span data-ttu-id="c5fa2-161">В Debian и Ubuntu</span><span class="sxs-lookup"><span data-stu-id="c5fa2-161">On Debian & Ubuntu</span></span>

```bash
service ssh restart
```

## <a name="reset-sshd-using-azure-reset-access"></a><span data-ttu-id="c5fa2-162">Сброс SSHD с помощью команды Azure reset-access</span><span class="sxs-lookup"><span data-stu-id="c5fa2-162">Reset SSHD using Azure reset-access</span></span>

<span data-ttu-id="c5fa2-163">Если заблокированы из toohello SSHD критические изменения конфигурации можно использовать расширение доступа виртуальной Машины Azure hello tooreset hello SSHD конфигурации задней toohello исходной конфигурации.</span><span class="sxs-lookup"><span data-stu-id="c5fa2-163">If you are locked out from a breaking change toohello SSHD configuration you can use hello Azure VM access-extension tooreset hello SSHD configuration back toohello original configuration.</span></span>

<span data-ttu-id="c5fa2-164">Замените все имена в примере собственными.</span><span class="sxs-lookup"><span data-stu-id="c5fa2-164">Replace any example names with your own.</span></span>

```azurecli
azure vm reset-access \
--resource-group myResourceGroup \
--name myVM \
--reset-ssh
```

## <a name="install-fail2ban"></a><span data-ttu-id="c5fa2-165">Установка Fail2ban</span><span class="sxs-lookup"><span data-stu-id="c5fa2-165">Install Fail2ban</span></span>

<span data-ttu-id="c5fa2-166">Настоятельно рекомендуется tooinstall и установки открытой приложение hello Fail2ban, какие блоки повторных попыток toologin tooyour ВМ Linux через SSH с помощью подбора.</span><span class="sxs-lookup"><span data-stu-id="c5fa2-166">It is strongly recommended tooinstall and setup hello open source app Fail2ban, which blocks repeated attempts toologin tooyour Linux VM over SSH using brute force.</span></span>  <span data-ttu-id="c5fa2-167">Повторяющиеся журналы Fail2ban Сбой попытки toologin через SSH, а затем создает правила брандмауэра tooblock hello IP-адрес, инициированный попыток hello.</span><span class="sxs-lookup"><span data-stu-id="c5fa2-167">Fail2ban logs repeated failed attempts toologin over SSH and then creates firewall rules tooblock hello IP address that hello attempts are originating from.</span></span>

* [<span data-ttu-id="c5fa2-168">Домашняя страница Fail2ban</span><span class="sxs-lookup"><span data-stu-id="c5fa2-168">Fail2ban homepage</span></span>](http://www.fail2ban.org/wiki/index.php/Main_Page)

## <a name="next-steps"></a><span data-ttu-id="c5fa2-169">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c5fa2-169">Next Steps</span></span>

<span data-ttu-id="c5fa2-170">Теперь, когда вы настроили и блокировки сервера SSH hello на ВМ Linux существуют дополнительные рекомендации по безопасности, необходимо выполнить.</span><span class="sxs-lookup"><span data-stu-id="c5fa2-170">Now that you have configured and locked down hello SSH server on your Linux VM there are additional security best practices you can follow.</span></span>  

* [<span data-ttu-id="c5fa2-171">Управлять пользователями, SSH и проверку или восстановление дисков на виртуальных машинах Linux в Azure с помощью hello расширения VMAccess</span><span class="sxs-lookup"><span data-stu-id="c5fa2-171">Manage users, SSH, and check or repair disks on Azure Linux VMs using hello VMAccess Extension</span></span>](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

* [<span data-ttu-id="c5fa2-172">Шифрование дисков на виртуальной Машине Linux с помощью hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="c5fa2-172">Encrypt disks on a Linux VM using hello Azure CLI</span></span>](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

* [<span data-ttu-id="c5fa2-173">Доступ и безопасность в шаблонах Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c5fa2-173">Access and security in Azure Resource Manager templates</span></span>](dotnet-core-3-access-security.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
