---
title: "пары ключей toocreate действия aaaDetailed SSH для виртуальных машин Linux в Azure | Документы Microsoft"
description: "Узнайте дополнительные шаги toocreate SSH пару открытого и закрытого ключей для виртуальных машин Linux в Azure, вместе с конкретных сертификатов для различных вариантов использования."
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 6/28/2017
ms.author: danlep
ms.openlocfilehash: 9ac52ef4dc87e73b9c07ccc323adc955829e2014
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="detailed-walk-through-toocreate-an-ssh-key-pair-and-additional-certificates-for-a-linux-vm-in-azure"></a><span data-ttu-id="1e7e2-103">Подробные руководства по toocreate пару ключей SSH и дополнительных сертификатов для виртуальной Машины Linux в Azure</span><span class="sxs-lookup"><span data-stu-id="1e7e2-103">Detailed walk through toocreate an SSH key pair and additional certificates for a Linux VM in Azure</span></span>
<span data-ttu-id="1e7e2-104">С пару ключей SSH можно создавать виртуальные машины в Azure, то по умолчанию toousing ключей SSH для проверки подлинности, устраняя необходимость hello toolog пароли в.</span><span class="sxs-lookup"><span data-stu-id="1e7e2-104">With an SSH key pair, you can create Virtual Machines on Azure that default toousing SSH keys for authentication, eliminating hello need for passwords toolog in.</span></span> <span data-ttu-id="1e7e2-105">Пароли можно подобрать и открыть виртуальные машины вверх tooguess попыток toorelentless подбора пароля.</span><span class="sxs-lookup"><span data-stu-id="1e7e2-105">Passwords can be guessed, and open your VMs up toorelentless brute force attempts tooguess your password.</span></span> <span data-ttu-id="1e7e2-106">Виртуальные машины, созданные с помощью шаблонов hello Azure CLI или диспетчер ресурсов может содержать открытый ключ SSH как часть развертывания hello, удаление шаг настройки развертывания post отключения имена входа пароль для SSH.</span><span class="sxs-lookup"><span data-stu-id="1e7e2-106">VMs created with hello Azure CLI or Resource Manager templates can include your SSH public key as part of hello deployment, removing a post deployment configuration step of disabling password logins for SSH.</span></span> <span data-ttu-id="1e7e2-107">В этой статье приведены подробные указания и дополнительные примеры создания сертификатов, используемых, например, на виртуальных машинах Linux.</span><span class="sxs-lookup"><span data-stu-id="1e7e2-107">This article provides detailed steps and additional examples of generating certificates, such as for use with Linux virtual machines.</span></span> <span data-ttu-id="1e7e2-108">Если требуется, чтобы tooquickly создать и использовать пару ключей SSH см. в разделе [как пары toocreate открытого и закрытого ключа SSH для виртуальных машин Linux в Azure](mac-create-ssh-keys.md).</span><span class="sxs-lookup"><span data-stu-id="1e7e2-108">If you want tooquickly create and use an SSH key pair, see [How toocreate an SSH public and private key pair for Linux VMs in Azure](mac-create-ssh-keys.md).</span></span>

## <a name="understanding-ssh-keys"></a><span data-ttu-id="1e7e2-109">Общие сведения о ключах SSH</span><span class="sxs-lookup"><span data-stu-id="1e7e2-109">Understanding SSH keys</span></span>

<span data-ttu-id="1e7e2-110">Использование открытый и закрытый ключи SSH — toolog простым способом hello в tooyour серверы Linux.</span><span class="sxs-lookup"><span data-stu-id="1e7e2-110">Using SSH public and private keys is hello easiest way toolog in tooyour Linux servers.</span></span> <span data-ttu-id="1e7e2-111">[Шифрование с открытым ключом](https://en.wikipedia.org/wiki/Public-key_cryptography) предоставляет гораздо более безопасный способ toolog в tooyour Linux или BSD виртуальную Машину в Azure чем пароль, который может быть принудительно применен гораздо проще.</span><span class="sxs-lookup"><span data-stu-id="1e7e2-111">[Public-key cryptography](https://en.wikipedia.org/wiki/Public-key_cryptography) provides a much more secure way toolog in tooyour Linux or BSD VM in Azure than passwords, which can be brute-forced far more easily.</span></span>

<span data-ttu-id="1e7e2-112">Открытый ключ можно предоставить любому пользователю, тогда как закрытый ключ принадлежит только вам (или локальной инфраструктуре безопасности).</span><span class="sxs-lookup"><span data-stu-id="1e7e2-112">Your public key can be shared with anyone; but only you (or your local security infrastructure) possess your private key.</span></span>  <span data-ttu-id="1e7e2-113">должен иметь закрытый ключ SSH Hello [высокий уровень безопасности пароля](https://www.xkcd.com/936/) (источник:[xkcd.com](https://xkcd.com)) toosafeguard его.</span><span class="sxs-lookup"><span data-stu-id="1e7e2-113">hello SSH private key should have a [very secure password](https://www.xkcd.com/936/) (source:[xkcd.com](https://xkcd.com)) toosafeguard it.</span></span>  <span data-ttu-id="1e7e2-114">Этот пароль будет просто tooaccess hello SSH файл закрытого ключа и **не** hello пароль учетной записи пользователя.</span><span class="sxs-lookup"><span data-stu-id="1e7e2-114">This password is just tooaccess hello private SSH key file and **is not** hello user account password.</span></span>  <span data-ttu-id="1e7e2-115">При добавлении пароль tooyour SSH-ключ, шифрует hello закрытый ключ с помощью 128-разрядный AES, чтобы hello закрытый ключ не имеет смысла без пароля toodecrypt hello его.</span><span class="sxs-lookup"><span data-stu-id="1e7e2-115">When you add a password tooyour SSH key, it encrypts hello private key using 128-bit AES, so that hello private key is useless without hello password toodecrypt it.</span></span>  <span data-ttu-id="1e7e2-116">Если злоумышленник украсть ваш закрытый ключ и пароль не был ключ, они будут иметь доступ toouse, закрытый ключ toolog в tooany серверов, которые имеют hello соответствующего открытого ключа.</span><span class="sxs-lookup"><span data-stu-id="1e7e2-116">If an attacker stole your private key and that key did not have a password, they would be able toouse that private key toolog in tooany servers that have hello corresponding public key.</span></span>  <span data-ttu-id="1e7e2-117">Если закрытый ключ защищен паролем, злоумышленник не сможет использовать его. Такой подход обеспечивает дополнительный уровень безопасности инфраструктуры в Azure.</span><span class="sxs-lookup"><span data-stu-id="1e7e2-117">If a private key is password protected it cannot be used by that attacker, providing an additional layer of security for your infrastructure on Azure.</span></span>

<span data-ttu-id="1e7e2-118">В этой статье создается с использованием протокола SSH версии 2 RSA открытого и закрытого ключа пара файлов (также назывались tooas «ssh-rsa» ключей), которые рекомендуются для развертываний с помощью диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="1e7e2-118">This article creates an SSH protocol version 2 RSA public and private key file pair (also referred tooas "ssh-rsa" keys), which are recommended for deployments with Azure Resource Manager.</span></span> <span data-ttu-id="1e7e2-119">*SSH-rsa* в hello необходимы ключи [портала](https://portal.azure.com) классический и развертывания диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="1e7e2-119">*ssh-rsa* keys are required on hello [portal](https://portal.azure.com) for both classic and Resource Manager deployments.</span></span>

## <a name="ssh-keys-use-and-benefits"></a><span data-ttu-id="1e7e2-120">Использование ключей SSH и их преимущества</span><span class="sxs-lookup"><span data-stu-id="1e7e2-120">SSH keys use and benefits</span></span>

<span data-ttu-id="1e7e2-121">Azure требует по крайней мере 2048-разрядный процессор, протокол SSH версии 2 формата открытого и закрытого ключей RSA; файл открытого ключа Hello имеет hello `.pub` формат контейнера.</span><span class="sxs-lookup"><span data-stu-id="1e7e2-121">Azure requires at least 2048-bit, SSH protocol version 2 RSA format public and private keys; hello public key file has hello `.pub` container format.</span></span> <span data-ttu-id="1e7e2-122">Используйте ключи toocreate hello `ssh-keygen`, который задает ряд вопросов, а затем записывает закрытого ключа и соответствующего открытого ключа.</span><span class="sxs-lookup"><span data-stu-id="1e7e2-122">toocreate hello keys use `ssh-keygen`, which asks a series of questions and then writes a private key and a matching public key.</span></span> <span data-ttu-id="1e7e2-123">При создании виртуальной Машины Azure, Azure копирует hello открытого ключа toohello `~/.ssh/authorized_keys` папку на hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="1e7e2-123">When an Azure VM is created, Azure copies hello public key toohello `~/.ssh/authorized_keys` folder on hello VM.</span></span> <span data-ttu-id="1e7e2-124">Ключи SSH в `~/.ssh/authorized_keys` , используемые toochallenge hello клиента toomatch hello соответствующий закрытый ключ для имени входа SSH-подключения.</span><span class="sxs-lookup"><span data-stu-id="1e7e2-124">SSH keys in `~/.ssh/authorized_keys` are used toochallenge hello client toomatch hello corresponding private key on an SSH login connection.</span></span>  <span data-ttu-id="1e7e2-125">При создании ВМ Linux Azure с помощью ключей SSH для проверки подлинности, Azure настраивает hello SSHD toonot сервера разрешить имен входа, пароль, только ключи SSH.</span><span class="sxs-lookup"><span data-stu-id="1e7e2-125">When an Azure Linux VM is created using SSH keys for authentication, Azure configures hello SSHD server toonot allow password logins, only SSH keys.</span></span>  <span data-ttu-id="1e7e2-126">Таким образом, путем создания виртуальных машин Linux в Azure с ключи SSH, вы можете помочь безопасное развертывание виртуальной Машины hello и сэкономить шаг стандартной конфигурации после развертывания hello отключения пароли в hello **sshd_config** файла.</span><span class="sxs-lookup"><span data-stu-id="1e7e2-126">Therefore, by creating Azure Linux VMs with SSH keys, you can help secure hello VM deployment and save yourself hello typical post-deployment configuration step of disabling passwords in hello **sshd_config** file.</span></span>

## <a name="using-ssh-keygen"></a><span data-ttu-id="1e7e2-127">Использование команды ssh-keygen</span><span class="sxs-lookup"><span data-stu-id="1e7e2-127">Using ssh-keygen</span></span>

<span data-ttu-id="1e7e2-128">Эта команда создает пароль, защищенным (зашифрованное) пару ключей SSH, с помощью RSA 2048 бит и его закомментирована tooeasily идентифицировать его.</span><span class="sxs-lookup"><span data-stu-id="1e7e2-128">This command creates a password secured (encrypted) SSH key pair using 2048-bit RSA and it is commented tooeasily identify it.</span></span>  

<span data-ttu-id="1e7e2-129">SSH ключи, по умолчанию хранится в hello `~/.ssh` каталога.</span><span class="sxs-lookup"><span data-stu-id="1e7e2-129">SSH keys are by default kept in hello `~/.ssh` directory.</span></span>  <span data-ttu-id="1e7e2-130">Если у вас `~/.ssh` каталог, hello `ssh-keygen` команда создает его с hello правильные разрешения.</span><span class="sxs-lookup"><span data-stu-id="1e7e2-130">If you do not have a `~/.ssh` directory, hello `ssh-keygen` command creates it for you with hello correct permissions.</span></span>

```bash
ssh-keygen \
    -t rsa \
    -b 2048 \
    -C "azureuser@myserver" \
    -f ~/.ssh/id_rsa \
    -N mypassword
```

<span data-ttu-id="1e7e2-131">*Описание команды*</span><span class="sxs-lookup"><span data-stu-id="1e7e2-131">*Command explained*</span></span>

<span data-ttu-id="1e7e2-132">`ssh-keygen`= hello программа, используемая toocreate hello ключи</span><span class="sxs-lookup"><span data-stu-id="1e7e2-132">`ssh-keygen` = hello program used toocreate hello keys</span></span>

<span data-ttu-id="1e7e2-133">`-t rsa`Тип ключа toocreate, который имеет формат RSA hello [Википедии] =[эти скобки в конце](`https://en.wikipedia.org/wiki/RSA_(cryptosystem) `) 
 `-b 2048` = bits hello ключа</span><span class="sxs-lookup"><span data-stu-id="1e7e2-133">`-t rsa` = type of key toocreate which is hello RSA format [wikipedia][parens at end](`https://en.wikipedia.org/wiki/RSA_(cryptosystem) `)
`-b 2048` = bits of hello key</span></span>

<span data-ttu-id="1e7e2-134">`-C "azureuser@myserver"`= комментарий присоединенных toohello конца файла открытого ключа tooeasily hello идентифицировать его.</span><span class="sxs-lookup"><span data-stu-id="1e7e2-134">`-C "azureuser@myserver"` = a comment appended toohello end of hello public key file tooeasily identify it.</span></span>  <span data-ttu-id="1e7e2-135">Обычно сообщения электронной почты используется как hello комментария, но можно использовать любые имена оптимально подходит для вашей инфраструктуры.</span><span class="sxs-lookup"><span data-stu-id="1e7e2-135">Normally an email is used as hello comment but you can use whatever works best for your infrastructure.</span></span>

## <a name="classic-deploy-using-asm"></a><span data-ttu-id="1e7e2-136">Классическое развертывание с помощью `asm`</span><span class="sxs-lookup"><span data-stu-id="1e7e2-136">Classic deploy using `asm`</span></span>

<span data-ttu-id="1e7e2-137">Если вы используете hello классической модели развертывания (`asm` режим в hello CLI), можно использовать открытый ключ SSH-RSA или RFC4716 в формате ключа в контейнере pem.</span><span class="sxs-lookup"><span data-stu-id="1e7e2-137">If you are using hello classic deployment model (`asm` mode in hello CLI), you can use an SSH-RSA public key or an RFC4716 formatted key in a pem container.</span></span>  <span data-ttu-id="1e7e2-138">открытый ключ SSH-RSA Hello является то, что был создан ранее в этой статье с помощью `ssh-keygen`.</span><span class="sxs-lookup"><span data-stu-id="1e7e2-138">hello SSH-RSA public key is what was created earlier in this article using `ssh-keygen`.</span></span>

<span data-ttu-id="1e7e2-139">toocreate RFC4716 формат ключа из существующих открытый ключ SSH:</span><span class="sxs-lookup"><span data-stu-id="1e7e2-139">toocreate a RFC4716 formatted key from an existing SSH public key:</span></span>

```bash
ssh-keygen \
-f ~/.ssh/id_rsa.pub \
-e \
-m RFC4716 > ~/.ssh/id_ssh2.pem
```

## <a name="example-of-ssh-keygen"></a><span data-ttu-id="1e7e2-140">Пример с ssh-keygen</span><span class="sxs-lookup"><span data-stu-id="1e7e2-140">Example of ssh-keygen</span></span>

```bash
ssh-keygen -t rsa -b 2048 -C "azureuser@myserver"
Generating public/private rsa key pair.
Enter file in which toosave hello key (/home/azureuser/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/azureuser/.ssh/id_rsa.
Your public key has been saved in /home/azureuser/.ssh/id_rsa.pub.
hello key fingerprint is:
14:a3:cb:3e:78:ad:25:cc:55:e9:0c:08:e5:d1:a9:08 azureuser@myserver
hello keys randomart image is:
+--[ RSA 2048]----+
|        o o. .   |
|      E. = .o    |
|      ..o...     |
|     . o....     |
|      o S =      |
|     . + O       |
|      + = =      |
|       o +       |
|        .        |
+-----------------+
```

<span data-ttu-id="1e7e2-141">Сохраненные файлы ключей:</span><span class="sxs-lookup"><span data-stu-id="1e7e2-141">Saved key files:</span></span>

`Enter file in which toosave hello key (/home/azureuser/.ssh/id_rsa): ~/.ssh/id_rsa`

<span data-ttu-id="1e7e2-142">Имя Hello пару ключей для данной статьи.</span><span class="sxs-lookup"><span data-stu-id="1e7e2-142">hello key pair name for this article.</span></span>  <span data-ttu-id="1e7e2-143">Наличие пару ключей с именем **id_rsa** значения по умолчанию hello и ожидать, некоторые средства hello **id_rsa** имени файла закрытого ключа, имеющая одно имеет смысл.</span><span class="sxs-lookup"><span data-stu-id="1e7e2-143">Having a key pair named **id_rsa** is hello default and some tools might expect hello **id_rsa** private key file name so having one is a good idea.</span></span> <span data-ttu-id="1e7e2-144">каталог Hello `~/.ssh/` hello расположение по умолчанию для пар ключей SSH и файл конфигурации SSH hello.</span><span class="sxs-lookup"><span data-stu-id="1e7e2-144">hello directory `~/.ssh/` is hello default location for SSH key pairs and hello SSH config file.</span></span>  <span data-ttu-id="1e7e2-145">Если не указано с указанием полного пути `ssh-keygen` создает ключи hello в текущем рабочем каталоге hello, по умолчанию hello не `~/.ssh`.</span><span class="sxs-lookup"><span data-stu-id="1e7e2-145">If not specified with a full path, `ssh-keygen` creates hello keys in hello current working directory, not hello default `~/.ssh`.</span></span>

<span data-ttu-id="1e7e2-146">Перечень hello `~/.ssh` каталога.</span><span class="sxs-lookup"><span data-stu-id="1e7e2-146">A listing of hello `~/.ssh` directory.</span></span>

```bash
ls -al ~/.ssh
-rw------- 1 azureuser staff  1675 Aug 25 18:04 id_rsa
-rw-r--r-- 1 azureuser staff   410 Aug 25 18:04 id_rsa.pub
```

<span data-ttu-id="1e7e2-147">Пароль ключа:</span><span class="sxs-lookup"><span data-stu-id="1e7e2-147">Key Password:</span></span>

`Enter passphrase (empty for no passphrase):`

<span data-ttu-id="1e7e2-148">`ssh-keygen`означает tooa пароль для файла закрытого ключа hello как «парольную фразу.»</span><span class="sxs-lookup"><span data-stu-id="1e7e2-148">`ssh-keygen` refers tooa password for hello private key file as "a passphrase."</span></span>  <span data-ttu-id="1e7e2-149">Это *строго* рекомендуется tooadd tooyour пароль закрытого ключа.</span><span class="sxs-lookup"><span data-stu-id="1e7e2-149">It is *strongly* recommended tooadd a password tooyour private key.</span></span> <span data-ttu-id="1e7e2-150">Без пароля защиту hello файл ключа имеющему hello файла можно использовать toolog в tooany сервер, имеющий hello соответствующего открытого ключа.</span><span class="sxs-lookup"><span data-stu-id="1e7e2-150">Without a password protecting hello key file, anyone with hello file can use it toolog in tooany server that has hello corresponding public key.</span></span> <span data-ttu-id="1e7e2-151">Добавление пароля (парольную фразу) предлагает несколько защиты в случае, если кто-то — может toogain доступа tooyour файла закрытого ключа, вы получили время toochange hello ключи, используемые tooauthenticate вы.</span><span class="sxs-lookup"><span data-stu-id="1e7e2-151">Adding a password (passphrase) offers more protection in case someone is able toogain access tooyour private key file, given you time toochange hello keys used tooauthenticate you.</span></span>

## <a name="using-ssh-agent-toostore-your-private-key-password"></a><span data-ttu-id="1e7e2-152">С помощью ssh агента toostore пароль закрытого ключа</span><span class="sxs-lookup"><span data-stu-id="1e7e2-152">Using ssh-agent toostore your private key password</span></span>

<span data-ttu-id="1e7e2-153">Введите пароль файла закрытого ключа с помощью все имена входа по SSH tooavoid можно использовать `ssh-agent` toocache пароль файла закрытого ключа.</span><span class="sxs-lookup"><span data-stu-id="1e7e2-153">tooavoid typing your private key file password with every SSH login, you can use `ssh-agent` toocache your private key file password.</span></span> <span data-ttu-id="1e7e2-154">При использовании Mac OSX цепочки ключей hello надежно сохраняет пароли закрытых ключей hello при вызове `ssh-agent`.</span><span class="sxs-lookup"><span data-stu-id="1e7e2-154">If you are using a Mac, hello OSX Keychain securely stores hello private key passwords when you invoke `ssh-agent`.</span></span>

<span data-ttu-id="1e7e2-155">Проверить и использовать ssh агента и ssh добавить tooinform hello SSH системы о hello ключевых файлов, чтобы hello парольная фраза не нужно использовать в интерактивном режиме toobe.</span><span class="sxs-lookup"><span data-stu-id="1e7e2-155">Verify and use ssh-agent and ssh-add tooinform hello SSH system about hello key files so that hello passphrase will not need toobe used interactively.</span></span>

```bash
eval "$(ssh-agent -s)"
```

<span data-ttu-id="1e7e2-156">Теперь добавьте закрытый ключ hello слишком`ssh-agent` с помощью команды hello `ssh-add`.</span><span class="sxs-lookup"><span data-stu-id="1e7e2-156">Now add hello private key too`ssh-agent` using hello command `ssh-add`.</span></span>

```bash
ssh-add ~/.ssh/id_rsa
```

<span data-ttu-id="1e7e2-157">Hello пароль закрытого ключа сохраняется в `ssh-agent`.</span><span class="sxs-lookup"><span data-stu-id="1e7e2-157">hello private key password is now stored in `ssh-agent`.</span></span>

## <a name="using-ssh-copy-id-toocopy-hello-key-tooan-existing-vm"></a><span data-ttu-id="1e7e2-158">С помощью `ssh-copy-id` ключа tooan toocopy hello существующей виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="1e7e2-158">Using `ssh-copy-id` toocopy hello key tooan existing VM</span></span>
<span data-ttu-id="1e7e2-159">При создании виртуальной Машины можно установить hello новый SSH открытого ключа tooyour виртуальных Машин Linux с помощью:</span><span class="sxs-lookup"><span data-stu-id="1e7e2-159">If you have already created a VM you can install hello new SSH public key tooyour Linux VM with:</span></span>

```bash
ssh-copy-id -i ~/.ssh/id_rsa.pub ahmet@myserver
```

## <a name="create-and-configure-an-ssh-config-file"></a><span data-ttu-id="1e7e2-160">Создание и настройка файла конфигурации SSH</span><span class="sxs-lookup"><span data-stu-id="1e7e2-160">Create and configure an SSH config file</span></span>

<span data-ttu-id="1e7e2-161">Его рекомендуется наиболее toocreate рекомендаций и настроить `~/.ssh/config` toospeed файл вверх имена входа и оптимизации поведение клиента SSH.</span><span class="sxs-lookup"><span data-stu-id="1e7e2-161">It is a recommended best practice toocreate and configure an `~/.ssh/config` file toospeed up log ins and for optimizing your SSH client behavior.</span></span>

<span data-ttu-id="1e7e2-162">Следующий пример Hello показывает стандартной конфигурации.</span><span class="sxs-lookup"><span data-stu-id="1e7e2-162">hello following example shows a standard configuration.</span></span>

### <a name="create-hello-file"></a><span data-ttu-id="1e7e2-163">Создайте файл hello</span><span class="sxs-lookup"><span data-stu-id="1e7e2-163">Create hello file</span></span>

```bash
touch ~/.ssh/config
```

### <a name="edit-hello-file-tooadd-hello-new-ssh-configuration"></a><span data-ttu-id="1e7e2-164">Изменение hello файл tooadd hello новой конфигурации SSH:</span><span class="sxs-lookup"><span data-stu-id="1e7e2-164">Edit hello file tooadd hello new SSH configuration:</span></span>

```bash
vim ~/.ssh/config
```

### <a name="example-sshconfig-file"></a><span data-ttu-id="1e7e2-165">Пример файла `~/.ssh/config`:</span><span class="sxs-lookup"><span data-stu-id="1e7e2-165">Example `~/.ssh/config` file:</span></span>

```bash
# Azure Keys
Host fedora22
  Hostname 102.160.203.241
  User ahmet
# ./Azure Keys
# Default Settings
Host *
  PubkeyAuthentication=yes
  IdentitiesOnly=yes
  ServerAliveInterval=60
  ServerAliveCountMax=30
  ControlMaster auto
  ControlPath ~/.ssh/SSHConnections/ssh-%r@%h:%p
  ControlPersist 4h
  IdentityFile ~/.ssh/id_rsa
```

<span data-ttu-id="1e7e2-166">Это дает конфигурации SSH, вы разделы для каждого сервера tooenable каждого toohave свой собственный выделенный пару ключей.</span><span class="sxs-lookup"><span data-stu-id="1e7e2-166">This SSH config gives you sections for each server tooenable each toohave its own dedicated key pair.</span></span> <span data-ttu-id="1e7e2-167">Здравствуйте, параметры по умолчанию (`Host *`) предназначены для тех узлах, которые не соответствует ни одному из hello конкретных узлов, чем в файле конфигурации hello.</span><span class="sxs-lookup"><span data-stu-id="1e7e2-167">hello default settings (`Host *`) are for any hosts that do not match any of hello specific hosts higher up in hello config file.</span></span>

### <a name="config-file-explained"></a><span data-ttu-id="1e7e2-168">Описание файла конфигурации</span><span class="sxs-lookup"><span data-stu-id="1e7e2-168">Config file explained</span></span>

<span data-ttu-id="1e7e2-169">`Host`= hello имя узла hello, вызываемый на hello терминалов.</span><span class="sxs-lookup"><span data-stu-id="1e7e2-169">`Host` = hello name of hello host being called on hello terminal.</span></span>  <span data-ttu-id="1e7e2-170">`ssh fedora22`сообщает `SSH` toouse значения hello в блоке settings hello с меткой `Host fedora22` Примечание: для узла можно указать любую метку, для использования логического и не представляют Привет фактическое имя узла любого сервера.</span><span class="sxs-lookup"><span data-stu-id="1e7e2-170">`ssh fedora22` tells `SSH` toouse hello values in hello settings block labeled `Host fedora22`  NOTE: Host can be any label that is logical for your usage and does not represent hello actual hostname of any server.</span></span>

<span data-ttu-id="1e7e2-171">`Hostname 102.160.203.241`= hello IP-адрес или DNS-имя сервера hello к которому выполняется доступ.</span><span class="sxs-lookup"><span data-stu-id="1e7e2-171">`Hostname 102.160.203.241` = hello IP address or DNS name for hello server being accessed.</span></span>

<span data-ttu-id="1e7e2-172">`User ahmet`= toouse учетную запись удаленного пользователя hello при входе toohello сервера.</span><span class="sxs-lookup"><span data-stu-id="1e7e2-172">`User ahmet` = hello remote user account toouse when logging in toohello server.</span></span>

<span data-ttu-id="1e7e2-173">`PubKeyAuthentication yes`= сообщает SSH требуется toouse toolog ключа SSH.</span><span class="sxs-lookup"><span data-stu-id="1e7e2-173">`PubKeyAuthentication yes` = tells SSH you want toouse an SSH key toolog in.</span></span>

<span data-ttu-id="1e7e2-174">`IdentityFile /home/ahmet/.ssh/id_id_rsa`= hello SSH закрытого ключа и соответствующего открытого ключа toouse для проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="1e7e2-174">`IdentityFile /home/ahmet/.ssh/id_id_rsa` = hello SSH private key and corresponding public key toouse for authentication.</span></span>

## <a name="ssh-into-linux-without-a-password"></a><span data-ttu-id="1e7e2-175">Вход в Linux с использованием SSH без пароля</span><span class="sxs-lookup"><span data-stu-id="1e7e2-175">SSH into Linux without a password</span></span>

<span data-ttu-id="1e7e2-176">Теперь, когда у вас есть пару ключей SSH и настроенный файл конфигурации SSH, быстро и надежно являются может toolog в tooyour виртуальной Машины с Linux.</span><span class="sxs-lookup"><span data-stu-id="1e7e2-176">Now that you have an SSH key pair and a configured SSH config file, you are able toolog in tooyour Linux VM quickly and securely.</span></span> <span data-ttu-id="1e7e2-177">Здравствуйте, во время первого входа в tooa сервера, с помощью SSH ключа hello командные строки можно для hello парольную фразу для этого файла ключа.</span><span class="sxs-lookup"><span data-stu-id="1e7e2-177">hello first time you log in tooa server using an SSH key hello command prompts you for hello passphrase for that key file.</span></span>

```bash
ssh fedora22
```

### <a name="command-explained"></a><span data-ttu-id="1e7e2-178">Описание команды</span><span class="sxs-lookup"><span data-stu-id="1e7e2-178">Command explained</span></span>

<span data-ttu-id="1e7e2-179">Когда `ssh fedora22` выполнении SSH сначала находит и загружает все параметры из hello `Host fedora22` блока, а затем загружает все hello оставшиеся параметры из hello последний блок `Host *`.</span><span class="sxs-lookup"><span data-stu-id="1e7e2-179">When `ssh fedora22` is executed SSH first locates and loads any settings from hello `Host fedora22` block, and then loads all hello remaining settings from hello last block, `Host *`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1e7e2-180">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1e7e2-180">Next Steps</span></span>

<span data-ttu-id="1e7e2-181">Далее вверх toocreate виртуальных машин Linux Azure использует hello новый SSH открытый ключ.</span><span class="sxs-lookup"><span data-stu-id="1e7e2-181">Next up is toocreate Azure Linux VMs using hello new SSH public key.</span></span>  <span data-ttu-id="1e7e2-182">Виртуальные машины Azure, созданных с помощью открытого ключа SSH от имени для входа hello, лучше защищенным, чем виртуальные машины, созданные с помощью метода входа по умолчанию hello, пароли.</span><span class="sxs-lookup"><span data-stu-id="1e7e2-182">Azure VMs that are created with an SSH public key as hello login are better secured than VMs created with hello default login method, passwords.</span></span>  <span data-ttu-id="1e7e2-183">В настройках виртуальных машин Azure, созданных с помощью ключей SSH, пароли отключены по умолчанию для защиты от атак методом подбора.</span><span class="sxs-lookup"><span data-stu-id="1e7e2-183">Azure VMs created using SSH keys are by default configured with passwords disabled, avoiding brute-forced guessing attempts.</span></span>

* [<span data-ttu-id="1e7e2-184">Создание защищенной виртуальной машины Linux с помощью шаблона Azure</span><span class="sxs-lookup"><span data-stu-id="1e7e2-184">Create a secure Linux VM using an Azure template</span></span>](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="1e7e2-185">Создание безопасного ВМ Linux с помощью hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="1e7e2-185">Create a secure Linux VM using hello Azure portal</span></span>](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="1e7e2-186">Создание безопасного ВМ Linux с помощью hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="1e7e2-186">Create a secure Linux VM using hello Azure CLI</span></span>](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
