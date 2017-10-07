---
title: "пароли aaaDisable SSH для ВМ Linux, настроив SSHD | Документы Microsoft"
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
ms.openlocfilehash: fb67b2f5b8b3bf2ba214858940b04f2ea9013fb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="disable-ssh-passwords-on-your-linux-vm-by-configuring-sshd"></a><span data-ttu-id="c2dcd-103">Отключение паролей SSH в виртуальной машине Linux в настройках SSHD</span><span class="sxs-lookup"><span data-stu-id="c2dcd-103">Disable SSH passwords on your Linux VM by configuring SSHD</span></span>
<span data-ttu-id="c2dcd-104">В этой статье основное внимание уделено toolock вниз hello безопасности входа в систему виртуальной машины Linux.</span><span class="sxs-lookup"><span data-stu-id="c2dcd-104">This article focuses on how toolock down hello login security of your Linux VM.</span></span>  <span data-ttu-id="c2dcd-105">По мере открытия hello SSH-порт 22 программы-роботы world toohello запустите попытки toologin путем подбора паролей.</span><span class="sxs-lookup"><span data-stu-id="c2dcd-105">As soon as hello SSH port 22 is opened toohello world bots start trying toologin by guessing passwords.</span></span>  <span data-ttu-id="c2dcd-106">В этой статье мы отключим вход в систему с паролем по протоколу SSH.</span><span class="sxs-lookup"><span data-stu-id="c2dcd-106">What we will do in this article is disable password logins over SSH.</span></span>  <span data-ttu-id="c2dcd-107">Удалив hello возможность полностью toouse пароли защищен hello виртуальной Машине Linux из этого типа атаки методом принудительно атаки.</span><span class="sxs-lookup"><span data-stu-id="c2dcd-107">By completely removing hello ability toouse passwords we protect hello Linux VM from this type of brute force attack.</span></span>  <span data-ttu-id="c2dcd-108">Hello добавлены премия — Linux SSHD tooonly позволяют настроить имена входа через открытый и закрытый ключи SSH, пока hello tooLinux toologin наиболее безопасным способом.</span><span class="sxs-lookup"><span data-stu-id="c2dcd-108">hello added bonus is we will configure Linux SSHD tooonly allow logins via SSH public & private keys, by far hello most secure way toologin tooLinux.</span></span>  <span data-ttu-id="c2dcd-109">Hello возможных сочетаний, его потребуется закрытый ключ hello tooguess весьма велик и таким образом не рекомендует программы-роботы из даже беспокоить ключи SSH tootry toobrute force.</span><span class="sxs-lookup"><span data-stu-id="c2dcd-109">hello possible combinations of it would require tooguess hello private key is immense and therefore discourages bots from even bothering tootry toobrute force SSH keys.</span></span>

## <a name="goals"></a><span data-ttu-id="c2dcd-110">Цели</span><span class="sxs-lookup"><span data-stu-id="c2dcd-110">Goals</span></span>
* <span data-ttu-id="c2dcd-111">Настройте SSHD toodisallow.</span><span class="sxs-lookup"><span data-stu-id="c2dcd-111">Configure SSHD toodisallow:</span></span>
  * <span data-ttu-id="c2dcd-112">Вход с использованием пароля</span><span class="sxs-lookup"><span data-stu-id="c2dcd-112">Password logins</span></span>
  * <span data-ttu-id="c2dcd-113">Вход привилегированного пользователя</span><span class="sxs-lookup"><span data-stu-id="c2dcd-113">Root user login</span></span>
  * <span data-ttu-id="c2dcd-114">Проверку подлинности через запрос и ответ</span><span class="sxs-lookup"><span data-stu-id="c2dcd-114">Challenge-response authentication</span></span>
* <span data-ttu-id="c2dcd-115">Настройте SSHD tooallow.</span><span class="sxs-lookup"><span data-stu-id="c2dcd-115">Configure SSHD tooallow:</span></span>
  * <span data-ttu-id="c2dcd-116">Вход только с использованием SSH-ключей</span><span class="sxs-lookup"><span data-stu-id="c2dcd-116">only SSH key logins</span></span>
* <span data-ttu-id="c2dcd-117">Перезапустите SSHD, не выходя из системы</span><span class="sxs-lookup"><span data-stu-id="c2dcd-117">Restart SSHD while still logged in</span></span>
* <span data-ttu-id="c2dcd-118">Новая конфигурация SSHD теста hello</span><span class="sxs-lookup"><span data-stu-id="c2dcd-118">Test hello new SSHD configuration</span></span>

## <a name="introduction"></a><span data-ttu-id="c2dcd-119">Введение</span><span class="sxs-lookup"><span data-stu-id="c2dcd-119">Introduction</span></span>
[<span data-ttu-id="c2dcd-120">Определение SSH</span><span class="sxs-lookup"><span data-stu-id="c2dcd-120">SSH defined</span></span>](https://en.wikipedia.org/wiki/Secure_Shell)

<span data-ttu-id="c2dcd-121">SSHD — hello SSH сервера, работающего на виртуальной Машине Linux hello.</span><span class="sxs-lookup"><span data-stu-id="c2dcd-121">SSHD is hello SSH Server that runs on hello Linux VM.</span></span>  <span data-ttu-id="c2dcd-122">SSH — это клиент, который запускается из оболочки на рабочей станции MacBook или Linux.</span><span class="sxs-lookup"><span data-stu-id="c2dcd-122">SSH is a client that runs from a shell on your MacBook or Linux workstation.</span></span>  <span data-ttu-id="c2dcd-123">SSH также является протокол hello используется toosecure и шифрования hello обмена данными между рабочей станцией и hello виртуальной Машины с Linux.</span><span class="sxs-lookup"><span data-stu-id="c2dcd-123">SSH is also hello protocol used toosecure and encrypt hello communication between your workstation and hello Linux VM.</span></span>

<span data-ttu-id="c2dcd-124">В этой статье это очень важно tookeep перемещайтесь открыт для hello всей виртуальной Машины Linux один tooyour входа.</span><span class="sxs-lookup"><span data-stu-id="c2dcd-124">For this article it is very important tookeep one login tooyour Linux VM open for hello entire walk through.</span></span>  <span data-ttu-id="c2dcd-125">По этой причине их откроется два терминалы и SSH toohello виртуальной Машины с Linux.</span><span class="sxs-lookup"><span data-stu-id="c2dcd-125">For this reason we will open two terminals and SSH toohello Linux VM from both of them.</span></span>  <span data-ttu-id="c2dcd-126">Мы будет использовать hello первый терминалов toomake hello изменения tooSSHDs файл конфигурации и перезапустите службу SSHD hello.</span><span class="sxs-lookup"><span data-stu-id="c2dcd-126">We will use hello first terminal toomake hello changes tooSSHDs configuration file and restart hello SSHD service.</span></span>  <span data-ttu-id="c2dcd-127">Мы будем использовать терминалов tootest с второй hello эти изменения, после перезапуска службы hello.</span><span class="sxs-lookup"><span data-stu-id="c2dcd-127">We will use hello second terminal tootest those changes once hello service is restarted.</span></span>  <span data-ttu-id="c2dcd-128">Так как мы выполняется отключение SSH пароли и полагаться исключительно на ключи SSH, если ключи SSH неверны и закрыть toohello hello подключения виртуальной Машины, hello виртуальной Машины будут окончательно заблокирован и никто будут tooit toologin может запрашивать ее toobe удалена и создана заново.</span><span class="sxs-lookup"><span data-stu-id="c2dcd-128">Because we are disabling SSH passwords and relying strictly on SSH keys, if your SSH keys are not correct and you close hello connection toohello VM, hello VM will be permanently locked and no one will be able toologin tooit requiring it toobe deleted and recreated.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c2dcd-129">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="c2dcd-129">Prerequisites</span></span>
* [<span data-ttu-id="c2dcd-130">Создание ключей SSH для виртуальных машин Linux в ОС Linux и Mac в Azure</span><span class="sxs-lookup"><span data-stu-id="c2dcd-130">Create SSH keys on Linux and Mac for Linux VMs in Azure</span></span>](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* <span data-ttu-id="c2dcd-131">Учетная запись Azure</span><span class="sxs-lookup"><span data-stu-id="c2dcd-131">Azure account</span></span>
  * [<span data-ttu-id="c2dcd-132">Бесплатная пробная версия подписки</span><span class="sxs-lookup"><span data-stu-id="c2dcd-132">free trial signup</span></span>](https://azure.microsoft.com/pricing/free-trial/)
  * [<span data-ttu-id="c2dcd-133">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="c2dcd-133">Azure portal</span></span>](http://portal.azure.com)
* <span data-ttu-id="c2dcd-134">Виртуальная машина Linux в Azure</span><span class="sxs-lookup"><span data-stu-id="c2dcd-134">Linux VM running on azure</span></span>
* <span data-ttu-id="c2dcd-135">Открытый и закрытый SSH-ключ в `~/.ssh/`</span><span class="sxs-lookup"><span data-stu-id="c2dcd-135">SSH public & private key pair in `~/.ssh/`</span></span>
* <span data-ttu-id="c2dcd-136">Открытый ключ SSH в `~/.ssh/authorized_keys` на виртуальной Машине Linux hello</span><span class="sxs-lookup"><span data-stu-id="c2dcd-136">SSH public key in `~/.ssh/authorized_keys` on hello Linux VM</span></span>
* <span data-ttu-id="c2dcd-137">Прав sudo на hello виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="c2dcd-137">Sudo rights on hello VM</span></span>
* <span data-ttu-id="c2dcd-138">Открытый порт 22</span><span class="sxs-lookup"><span data-stu-id="c2dcd-138">Port 22 open</span></span>

## <a name="quick-commands"></a><span data-ttu-id="c2dcd-139">Быстрые команды</span><span class="sxs-lookup"><span data-stu-id="c2dcd-139">Quick Commands</span></span>
<span data-ttu-id="c2dcd-140">*Начните здесь наемных Linux администраторов, желающих только версии TLDR hello.  Для всех остальных случаях, если оно hello подробное описание и пошагового пропустите этот раздел.*</span><span class="sxs-lookup"><span data-stu-id="c2dcd-140">*Seasoned Linux Admins who just want hello TLDR version start here.  For everyone else that wants hello detailed explanation and walk through skip this section.*</span></span>

```bash
sudo vim /etc/ssh/sshd_config
```

<span data-ttu-id="c2dcd-141">Измените файл конфигурации hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="c2dcd-141">Edit hello config file as follows:</span></span>

```sh
# Change PasswordAuthentication toothis:
PasswordAuthentication no

# Change PubkeyAuthentication toothis:
PubkeyAuthentication yes

# Change PermitRootLogin toothis:
PermitRootLogin no

# Change ChallengeResponseAuthentication toothis:
ChallengeResponseAuthentication no
```

<span data-ttu-id="c2dcd-142">Перезапустите службу SSHD hello.</span><span class="sxs-lookup"><span data-stu-id="c2dcd-142">Restart hello SSHD service.</span></span> <span data-ttu-id="c2dcd-143">На основе дистрибутивов Debian:</span><span class="sxs-lookup"><span data-stu-id="c2dcd-143">On Debian-based distros:</span></span>

```bash
sudo service ssh restart
```

<span data-ttu-id="c2dcd-144">На основе дистрибутивов Red Hat:</span><span class="sxs-lookup"><span data-stu-id="c2dcd-144">On Red Hat-based distros:</span></span>

```bash
sudo service sshd restart
```

## <a name="detailed-walk-through"></a><span data-ttu-id="c2dcd-145">Подробные пошаговые инструкции</span><span class="sxs-lookup"><span data-stu-id="c2dcd-145">Detailed Walk Through</span></span>
<span data-ttu-id="c2dcd-146">Toohello входа в систему виртуальной Машины с Linux на сервере терминалов 1 (T1).</span><span class="sxs-lookup"><span data-stu-id="c2dcd-146">Login toohello Linux VM on terminal 1 (T1).</span></span>  <span data-ttu-id="c2dcd-147">Toohello входа в систему виртуальной Машины с Linux для терминалов 2 (T2).</span><span class="sxs-lookup"><span data-stu-id="c2dcd-147">Login toohello Linux VM on terminal 2 (T2).</span></span>

<span data-ttu-id="c2dcd-148">Файл конфигурации SSHD hello tooedit мы будем в таблицу T2.</span><span class="sxs-lookup"><span data-stu-id="c2dcd-148">On T2 we are going tooedit hello SSHD configuration file.</span></span>  

```bash
sudo vim /etc/ssh/sshd_config
```

<span data-ttu-id="c2dcd-149">Здесь мы изменить только пароли toodisable параметры hello и включить учетные записи ключа SSH.</span><span class="sxs-lookup"><span data-stu-id="c2dcd-149">From here we will edit just hello settings toodisable passwords and enable SSH key logins.</span></span>  <span data-ttu-id="c2dcd-150">Существует множество параметров в этот файл следует изучить и Смена toomake Linux SSH, как безопасные, сколько требуется.</span><span class="sxs-lookup"><span data-stu-id="c2dcd-150">There are many settings in this file that you should research and change toomake Linux & SSH as secure as you need.</span></span>

#### <a name="disable-password-logins"></a><span data-ttu-id="c2dcd-151">Отключение входа с использованием пароля</span><span class="sxs-lookup"><span data-stu-id="c2dcd-151">Disable Password logins</span></span>

```sh
# Change PasswordAuthentication toothis:
PasswordAuthentication no
```

#### <a name="enable-public-key-authentication"></a><span data-ttu-id="c2dcd-152">Включение проверки подлинности с использованием открытого ключа</span><span class="sxs-lookup"><span data-stu-id="c2dcd-152">Enable Public Key Authentication</span></span>

```sh
# Change PubkeyAuthentication toothis:
PubkeyAuthentication yes
```

#### <a name="disable-root-login"></a><span data-ttu-id="c2dcd-153">Отключение корневого входа</span><span class="sxs-lookup"><span data-stu-id="c2dcd-153">Disable Root Login</span></span>

```sh
# Change PermitRootLogin toothis:
PermitRootLogin no
```

#### <a name="disable-challenge-response-authentication"></a><span data-ttu-id="c2dcd-154">Отключение проверки подлинности через запрос и ответ</span><span class="sxs-lookup"><span data-stu-id="c2dcd-154">Disable Challenge-response Authentication</span></span>
```sh
# Change ChallengeResponseAuthentication toothis:
ChallengeResponseAuthentication no
```

### <a name="restart-sshd"></a><span data-ttu-id="c2dcd-155">Перезапуск SSHD</span><span class="sxs-lookup"><span data-stu-id="c2dcd-155">Restart SSHD</span></span>
<span data-ttu-id="c2dcd-156">Убедитесь, что по-прежнему вы вошли из оболочки hello T1.</span><span class="sxs-lookup"><span data-stu-id="c2dcd-156">From hello T1 shell verify that you are still logged in.</span></span>  <span data-ttu-id="c2dcd-157">Это важно, чтобы не потерять доступ к виртуальной машине, если SSH-ключи окажутся неправильными, поскольку пароли будут отключены.</span><span class="sxs-lookup"><span data-stu-id="c2dcd-157">This is critical so you do not get locked out of your VM if your SSH keys are not correct since passwords are now disabled.</span></span>  <span data-ttu-id="c2dcd-158">Если ни один параметр неверны на вашей виртуальной Машине Linux, можно использовать T1 toofix sshd_config, а вы по-прежнему заносятся SSH будет активности hello подключения во время hello SSHD service перезапустите.</span><span class="sxs-lookup"><span data-stu-id="c2dcd-158">If any setting are incorrect on your Linux VM you can use T1 toofix sshd_config as you will still be logged in and SSH will keep hello connection alive during hello SSHD service restart.</span></span>

<span data-ttu-id="c2dcd-159">С терминала T2 выполните:</span><span class="sxs-lookup"><span data-stu-id="c2dcd-159">From T2 run:</span></span>

##### <a name="on-hello-debian-family"></a><span data-ttu-id="c2dcd-160">В Debian семейства hello</span><span class="sxs-lookup"><span data-stu-id="c2dcd-160">On hello Debian Family</span></span>
```bash
sudo service ssh restart
```

##### <a name="on-hello-redhat-family"></a><span data-ttu-id="c2dcd-161">На семейство RedHat hello</span><span class="sxs-lookup"><span data-stu-id="c2dcd-161">On hello RedHat Family</span></span>
```bash
sudo service sshd restart
```

<span data-ttu-id="c2dcd-162">Теперь пароли на виртуальной машине отключены, что защищает ее от попыток входа методом подбора пароля.</span><span class="sxs-lookup"><span data-stu-id="c2dcd-162">Passwords are now disabled on your VM protecting it from brute force password login attempts.</span></span>  <span data-ttu-id="c2dcd-163">Только SSH ключи допускается будет toologin может быстрее и безопаснее.</span><span class="sxs-lookup"><span data-stu-id="c2dcd-163">With only SSH Keys allowed you will be able toologin faster and much more secure.</span></span>

