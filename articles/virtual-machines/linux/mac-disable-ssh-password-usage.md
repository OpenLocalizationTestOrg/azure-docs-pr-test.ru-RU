---
title: "Отключение паролей SSH в виртуальной машине Linux в настройках SSHD | Документация Майкрософт"
description: "Защита виртуальной машины Linux в Azure посредством отключения входа с использованием пароля для SSH."
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: 
ms.assetid: 46137640-a7d2-40e5-a1e9-9effef7eb190
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/26/2016
ms.author: v-livech
ms.openlocfilehash: dc45a1cdce29cef061acc5c7e5b15d9d89265cd9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="disable-ssh-passwords-on-your-linux-vm-by-configuring-sshd"></a><span data-ttu-id="5c5b4-103">Отключение паролей SSH в виртуальной машине Linux в настройках SSHD</span><span class="sxs-lookup"><span data-stu-id="5c5b4-103">Disable SSH passwords on your Linux VM by configuring SSHD</span></span>
<span data-ttu-id="5c5b4-104">В этой статье рассматривается отключение защиты входа в систему в виртуальной машине Linux.</span><span class="sxs-lookup"><span data-stu-id="5c5b4-104">This article focuses on how to lock down the login security of your Linux VM.</span></span>  <span data-ttu-id="5c5b4-105">Если открыть SSH-порт номер 22, программы-роботы сразу же будут пытаться войти в систему путем подбора паролей.</span><span class="sxs-lookup"><span data-stu-id="5c5b4-105">As soon as the SSH port 22 is opened to the world bots start trying to login by guessing passwords.</span></span>  <span data-ttu-id="5c5b4-106">В этой статье мы отключим вход в систему с паролем по протоколу SSH.</span><span class="sxs-lookup"><span data-stu-id="5c5b4-106">What we will do in this article is disable password logins over SSH.</span></span>  <span data-ttu-id="5c5b4-107">За счет полного отключения возможности использовать пароли мы защитим виртуальную машину Linux от атак методом подбора.</span><span class="sxs-lookup"><span data-stu-id="5c5b4-107">By completely removing the ability to use passwords we protect the Linux VM from this type of brute force attack.</span></span>  <span data-ttu-id="5c5b4-108">Дополнительное преимущество состоит в том, что в настройках SSHD Linux вход в систему будет разрешен только с использованием открытых и закрытых ключей SSH, что является наиболее безопасным способом входа в ОС Linux.</span><span class="sxs-lookup"><span data-stu-id="5c5b4-108">The added bonus is we will configure Linux SSHD to only allow logins via SSH public & private keys, by far the most secure way to login to Linux.</span></span>  <span data-ttu-id="5c5b4-109">Число возможных комбинаций при поиске закрытого ключа методом подбора настолько велико, что программы-роботы даже не пытаются использовать этот метод для взлома SSH-ключей.</span><span class="sxs-lookup"><span data-stu-id="5c5b4-109">The possible combinations of it would require to guess the private key is immense and therefore discourages bots from even bothering to try to brute force SSH keys.</span></span>

## <a name="goals"></a><span data-ttu-id="5c5b4-110">Цели</span><span class="sxs-lookup"><span data-stu-id="5c5b4-110">Goals</span></span>
* <span data-ttu-id="5c5b4-111">Настройте SSHD, чтобы запретить:</span><span class="sxs-lookup"><span data-stu-id="5c5b4-111">Configure SSHD to disallow:</span></span>
  * <span data-ttu-id="5c5b4-112">Вход с использованием пароля</span><span class="sxs-lookup"><span data-stu-id="5c5b4-112">Password logins</span></span>
  * <span data-ttu-id="5c5b4-113">Вход привилегированного пользователя</span><span class="sxs-lookup"><span data-stu-id="5c5b4-113">Root user login</span></span>
  * <span data-ttu-id="5c5b4-114">Проверку подлинности через запрос и ответ</span><span class="sxs-lookup"><span data-stu-id="5c5b4-114">Challenge-response authentication</span></span>
* <span data-ttu-id="5c5b4-115">Настройте SSHD, чтобы разрешить:</span><span class="sxs-lookup"><span data-stu-id="5c5b4-115">Configure SSHD to allow:</span></span>
  * <span data-ttu-id="5c5b4-116">Вход только с использованием SSH-ключей</span><span class="sxs-lookup"><span data-stu-id="5c5b4-116">only SSH key logins</span></span>
* <span data-ttu-id="5c5b4-117">Перезапустите SSHD, не выходя из системы</span><span class="sxs-lookup"><span data-stu-id="5c5b4-117">Restart SSHD while still logged in</span></span>
* <span data-ttu-id="5c5b4-118">Протестируйте новую конфигурацию SSHD</span><span class="sxs-lookup"><span data-stu-id="5c5b4-118">Test the new SSHD configuration</span></span>

## <a name="introduction"></a><span data-ttu-id="5c5b4-119">Введение</span><span class="sxs-lookup"><span data-stu-id="5c5b4-119">Introduction</span></span>
[<span data-ttu-id="5c5b4-120">Определение SSH</span><span class="sxs-lookup"><span data-stu-id="5c5b4-120">SSH defined</span></span>](https://en.wikipedia.org/wiki/Secure_Shell)

<span data-ttu-id="5c5b4-121">SSHD — это SSH-сервер, работающий на виртуальной машине Linux.</span><span class="sxs-lookup"><span data-stu-id="5c5b4-121">SSHD is the SSH Server that runs on the Linux VM.</span></span>  <span data-ttu-id="5c5b4-122">SSH — это клиент, который запускается из оболочки на рабочей станции MacBook или Linux.</span><span class="sxs-lookup"><span data-stu-id="5c5b4-122">SSH is a client that runs from a shell on your MacBook or Linux workstation.</span></span>  <span data-ttu-id="5c5b4-123">SSH — это также протокол, используемый для защиты и шифрования обмена данными между рабочей станцией и виртуальной машиной Linux.</span><span class="sxs-lookup"><span data-stu-id="5c5b4-123">SSH is also the protocol used to secure and encrypt the communication between your workstation and the Linux VM.</span></span>

<span data-ttu-id="5c5b4-124">Для этой статьи очень важно держать открытым один сеанс работы с виртуальной машиной Linux в течение прохождения всего пошагового руководства.</span><span class="sxs-lookup"><span data-stu-id="5c5b4-124">For this article it is very important to keep one login to your Linux VM open for the entire walk through.</span></span>  <span data-ttu-id="5c5b4-125">По этой причине мы откроем два терминала и установим подключение SSH к виртуальной машине Linux из каждого из них.</span><span class="sxs-lookup"><span data-stu-id="5c5b4-125">For this reason we will open two terminals and SSH to the Linux VM from both of them.</span></span>  <span data-ttu-id="5c5b4-126">Первый терминал будет использоваться для изменений файла конфигурации SSHD и перезапуска службы SSHD.</span><span class="sxs-lookup"><span data-stu-id="5c5b4-126">We will use the first terminal to make the changes to SSHDs configuration file and restart the SSHD service.</span></span>  <span data-ttu-id="5c5b4-127">Второй терминал будет использоваться для тестирования этих изменений после перезапуска службы.</span><span class="sxs-lookup"><span data-stu-id="5c5b4-127">We will use the second terminal to test those changes once the service is restarted.</span></span>  <span data-ttu-id="5c5b4-128">Поскольку мы отключаем SSH-пароли и полагаемся исключительно на SSH-ключи, если ваши SSH-ключи неверны и вы закроете подключение к виртуальной машине, эта виртуальная машины окажется безвозвратно заблокированной. Никто не сможет войти в нее, поэтому ее придется удалить и создать заново.</span><span class="sxs-lookup"><span data-stu-id="5c5b4-128">Because we are disabling SSH passwords and relying strictly on SSH keys, if your SSH keys are not correct and you close the connection to the VM, the VM will be permanently locked and no one will be able to login to it requiring it to be deleted and recreated.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5c5b4-129">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="5c5b4-129">Prerequisites</span></span>
* [<span data-ttu-id="5c5b4-130">Создание ключей SSH для виртуальных машин Linux в ОС Linux и Mac в Azure</span><span class="sxs-lookup"><span data-stu-id="5c5b4-130">Create SSH keys on Linux and Mac for Linux VMs in Azure</span></span>](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* <span data-ttu-id="5c5b4-131">Учетная запись Azure</span><span class="sxs-lookup"><span data-stu-id="5c5b4-131">Azure account</span></span>
  * [<span data-ttu-id="5c5b4-132">Бесплатная пробная версия подписки</span><span class="sxs-lookup"><span data-stu-id="5c5b4-132">free trial signup</span></span>](https://azure.microsoft.com/pricing/free-trial/)
  * [<span data-ttu-id="5c5b4-133">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="5c5b4-133">Azure portal</span></span>](http://portal.azure.com)
* <span data-ttu-id="5c5b4-134">Виртуальная машина Linux в Azure</span><span class="sxs-lookup"><span data-stu-id="5c5b4-134">Linux VM running on azure</span></span>
* <span data-ttu-id="5c5b4-135">Открытый и закрытый SSH-ключ в `~/.ssh/`</span><span class="sxs-lookup"><span data-stu-id="5c5b4-135">SSH public & private key pair in `~/.ssh/`</span></span>
* <span data-ttu-id="5c5b4-136">Открытый SSH-ключ в `~/.ssh/authorized_keys` на виртуальной машине Linux</span><span class="sxs-lookup"><span data-stu-id="5c5b4-136">SSH public key in `~/.ssh/authorized_keys` on the Linux VM</span></span>
* <span data-ttu-id="5c5b4-137">Права sudo в виртуальной машине</span><span class="sxs-lookup"><span data-stu-id="5c5b4-137">Sudo rights on the VM</span></span>
* <span data-ttu-id="5c5b4-138">Открытый порт 22</span><span class="sxs-lookup"><span data-stu-id="5c5b4-138">Port 22 open</span></span>

## <a name="quick-commands"></a><span data-ttu-id="5c5b4-139">Быстрые команды</span><span class="sxs-lookup"><span data-stu-id="5c5b4-139">Quick Commands</span></span>
<span data-ttu-id="5c5b4-140">*Опытные администраторы Linux, которым требуется только версия TLDR, начинают здесь.  Всем остальным, кому нужно подробное описание и пошаговое руководство, следует пропустить этот раздел.*</span><span class="sxs-lookup"><span data-stu-id="5c5b4-140">*Seasoned Linux Admins who just want the TLDR version start here.  For everyone else that wants the detailed explanation and walk through skip this section.*</span></span>

```bash
sudo vim /etc/ssh/sshd_config
```

<span data-ttu-id="5c5b4-141">Измените файл конфигурации следующим образом:</span><span class="sxs-lookup"><span data-stu-id="5c5b4-141">Edit the config file as follows:</span></span>

```sh
# Change PasswordAuthentication to this:
PasswordAuthentication no

# Change PubkeyAuthentication to this:
PubkeyAuthentication yes

# Change PermitRootLogin to this:
PermitRootLogin no

# Change ChallengeResponseAuthentication to this:
ChallengeResponseAuthentication no
```

<span data-ttu-id="5c5b4-142">Перезапустите службу SSHD.</span><span class="sxs-lookup"><span data-stu-id="5c5b4-142">Restart the SSHD service.</span></span> <span data-ttu-id="5c5b4-143">На основе дистрибутивов Debian:</span><span class="sxs-lookup"><span data-stu-id="5c5b4-143">On Debian-based distros:</span></span>

```bash
sudo service ssh restart
```

<span data-ttu-id="5c5b4-144">На основе дистрибутивов Red Hat:</span><span class="sxs-lookup"><span data-stu-id="5c5b4-144">On Red Hat-based distros:</span></span>

```bash
sudo service sshd restart
```

## <a name="detailed-walk-through"></a><span data-ttu-id="5c5b4-145">Подробные пошаговые инструкции</span><span class="sxs-lookup"><span data-stu-id="5c5b4-145">Detailed Walk Through</span></span>
<span data-ttu-id="5c5b4-146">Выполните вход в виртуальную машину Linux с терминала 1 (T1).</span><span class="sxs-lookup"><span data-stu-id="5c5b4-146">Login to the Linux VM on terminal 1 (T1).</span></span>  <span data-ttu-id="5c5b4-147">Выполните вход в виртуальную машину Linux с терминала 2 (T2).</span><span class="sxs-lookup"><span data-stu-id="5c5b4-147">Login to the Linux VM on terminal 2 (T2).</span></span>

<span data-ttu-id="5c5b4-148">На T2 мы собираемся изменить файл конфигурации SSHD.</span><span class="sxs-lookup"><span data-stu-id="5c5b4-148">On T2 we are going to edit the SSHD configuration file.</span></span>  

```bash
sudo vim /etc/ssh/sshd_config
```

<span data-ttu-id="5c5b4-149">Здесь мы изменим только те параметры, которые отключат пароли и включат вход в систему с использованием SSH-ключей.</span><span class="sxs-lookup"><span data-stu-id="5c5b4-149">From here we will edit just the settings to disable passwords and enable SSH key logins.</span></span>  <span data-ttu-id="5c5b4-150">В этом файле множество параметров, которые необходимо изучить и изменить, чтобы организовать безопасность Linux и SSH на необходимом вам уровне.</span><span class="sxs-lookup"><span data-stu-id="5c5b4-150">There are many settings in this file that you should research and change to make Linux & SSH as secure as you need.</span></span>

#### <a name="disable-password-logins"></a><span data-ttu-id="5c5b4-151">Отключение входа с использованием пароля</span><span class="sxs-lookup"><span data-stu-id="5c5b4-151">Disable Password logins</span></span>

```sh
# Change PasswordAuthentication to this:
PasswordAuthentication no
```

#### <a name="enable-public-key-authentication"></a><span data-ttu-id="5c5b4-152">Включение проверки подлинности с использованием открытого ключа</span><span class="sxs-lookup"><span data-stu-id="5c5b4-152">Enable Public Key Authentication</span></span>

```sh
# Change PubkeyAuthentication to this:
PubkeyAuthentication yes
```

#### <a name="disable-root-login"></a><span data-ttu-id="5c5b4-153">Отключение корневого входа</span><span class="sxs-lookup"><span data-stu-id="5c5b4-153">Disable Root Login</span></span>

```sh
# Change PermitRootLogin to this:
PermitRootLogin no
```

#### <a name="disable-challenge-response-authentication"></a><span data-ttu-id="5c5b4-154">Отключение проверки подлинности через запрос и ответ</span><span class="sxs-lookup"><span data-stu-id="5c5b4-154">Disable Challenge-response Authentication</span></span>
```sh
# Change ChallengeResponseAuthentication to this:
ChallengeResponseAuthentication no
```

### <a name="restart-sshd"></a><span data-ttu-id="5c5b4-155">Перезапуск SSHD</span><span class="sxs-lookup"><span data-stu-id="5c5b4-155">Restart SSHD</span></span>
<span data-ttu-id="5c5b4-156">С терминала T1 убедитесь, что вы все еще находитесь в системе.</span><span class="sxs-lookup"><span data-stu-id="5c5b4-156">From the T1 shell verify that you are still logged in.</span></span>  <span data-ttu-id="5c5b4-157">Это важно, чтобы не потерять доступ к виртуальной машине, если SSH-ключи окажутся неправильными, поскольку пароли будут отключены.</span><span class="sxs-lookup"><span data-stu-id="5c5b4-157">This is critical so you do not get locked out of your VM if your SSH keys are not correct since passwords are now disabled.</span></span>  <span data-ttu-id="5c5b4-158">Если какие-либо параметры виртуальной машины Linux окажутся неправильными, можно будет воспользоваться терминалом T1, чтобы исправить sshd_config, поскольку у вас сохраняется вход в систему и SSH будет поддерживать соединение во время перезапуска службы SSHD.</span><span class="sxs-lookup"><span data-stu-id="5c5b4-158">If any setting are incorrect on your Linux VM you can use T1 to fix sshd_config as you will still be logged in and SSH will keep the connection alive during the SSHD service restart.</span></span>

<span data-ttu-id="5c5b4-159">С терминала T2 выполните:</span><span class="sxs-lookup"><span data-stu-id="5c5b4-159">From T2 run:</span></span>

##### <a name="on-the-debian-family"></a><span data-ttu-id="5c5b4-160">В семействе Debian</span><span class="sxs-lookup"><span data-stu-id="5c5b4-160">On the Debian Family</span></span>
```bash
sudo service ssh restart
```

##### <a name="on-the-redhat-family"></a><span data-ttu-id="5c5b4-161">В семействе RedHat</span><span class="sxs-lookup"><span data-stu-id="5c5b4-161">On the RedHat Family</span></span>
```bash
sudo service sshd restart
```

<span data-ttu-id="5c5b4-162">Теперь пароли на виртуальной машине отключены, что защищает ее от попыток входа методом подбора пароля.</span><span class="sxs-lookup"><span data-stu-id="5c5b4-162">Passwords are now disabled on your VM protecting it from brute force password login attempts.</span></span>  <span data-ttu-id="5c5b4-163">Благодаря тому, что разрешены только SSH-ключи, вы сможете выполнять вход быстрее и гораздо безопаснее.</span><span class="sxs-lookup"><span data-stu-id="5c5b4-163">With only SSH Keys allowed you will be able to login faster and much more secure.</span></span>

