---
title: "пары ключей aaaCreate SSH для виртуальных машин Linux в Azure | Документы Microsoft"
description: "Безопасное создание пары из открытого и закрытого ключей SSH для виртуальных машин Linux в Linux."
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: 
ms.assetid: 34ae9482-da3e-4b2d-9d0d-9d672aa42498
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/08/2017
ms.author: rasquill
ms.openlocfilehash: c4c7cec77c9b48295f2a28c8179b30a4dc38a555
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-ssh-public-and-private-key-pair-for-linux-vms"></a><span data-ttu-id="981f1-103">Создание пары из открытого и закрытого ключей SSH для виртуальных машин Linux</span><span class="sxs-lookup"><span data-stu-id="981f1-103">Create an SSH public and private key pair for Linux VMs</span></span>

<span data-ttu-id="981f1-104">В этой статье показано, как toogenerate SSH протокол версии 2 открытый и закрытый ключ RSA файл toouse пары с виртуальных машин Linux.</span><span class="sxs-lookup"><span data-stu-id="981f1-104">This article shows you how toogenerate an SSH protocol version 2 RSA public and private key file pair toouse with Linux VMs.</span></span>  <span data-ttu-id="981f1-105">С пару ключей SSH можно создавать виртуальные машины в Azure, то по умолчанию toousing ключей SSH для проверки подлинности, устраняя необходимость hello toolog пароли в.</span><span class="sxs-lookup"><span data-stu-id="981f1-105">With an SSH key pair, you can create Virtual Machines on Azure that default toousing SSH keys for authentication, eliminating hello need for passwords toolog in.</span></span>  <span data-ttu-id="981f1-106">Пароли можно подобрать и открыть виртуальные машины вверх tooguess попыток toorelentless подбора пароля.</span><span class="sxs-lookup"><span data-stu-id="981f1-106">Passwords can be guessed, and open your VMs up toorelentless brute force attempts tooguess your password.</span></span> <span data-ttu-id="981f1-107">Виртуальные машины, созданные с помощью шаблонов Azure или hello `azure-cli` можно включить свой открытый ключ SSH как часть развертывания hello, удаление шаг настройки развертывания post отключения имена входа пароль для SSH.</span><span class="sxs-lookup"><span data-stu-id="981f1-107">VMs created with Azure Templates or hello `azure-cli` can include your SSH public key as part of hello deployment, removing a post deployment configuration step of disabling password logins for SSH.</span></span>

## <a name="quick-commands"></a><span data-ttu-id="981f1-108">Быстрые команды</span><span class="sxs-lookup"><span data-stu-id="981f1-108">Quick Commands</span></span>

<span data-ttu-id="981f1-109">Следующие команды в оболочке Bash, заменив собственный выбор hello примеры выполнения hello.</span><span class="sxs-lookup"><span data-stu-id="981f1-109">Run hello following commands from a Bash shell, replacing hello examples with your own choices.</span></span>

<span data-ttu-id="981f1-110">По умолчанию файл открытого ключа SSH создается в каталоге `~/.ssh/id_rsa.pub`.</span><span class="sxs-lookup"><span data-stu-id="981f1-110">Your SSH public key file is by default created at `~/.ssh/id_rsa.pub`.</span></span> <span data-ttu-id="981f1-111">При появлении запроса, используя следующую команду hello, следует создать toosecure «парольную фразу» ваш закрытый ключ.</span><span class="sxs-lookup"><span data-stu-id="981f1-111">When prompted using hello following command, you should create a "passphrase" toosecure your private key.</span></span> <span data-ttu-id="981f1-112">(парольная фраза hello есть использовать tooencrypt пароль закрытого ключа.)</span><span class="sxs-lookup"><span data-stu-id="981f1-112">(hello passphrase is a password used tooencrypt your private key.)</span></span>

```bash
ssh-keygen -t rsa -b 2048 
```

<span data-ttu-id="981f1-113">Добавьте hello только что созданный раздел слишком`ssh-agent`:</span><span class="sxs-lookup"><span data-stu-id="981f1-113">Add hello newly created key too`ssh-agent`:</span></span>

```bash
ssh-add ~/.ssh/id_rsa
```

> [!IMPORTANT] 
> <span data-ttu-id="981f1-114">Здравствуйте выше команды на операционные системы Linux, почти все распределения, но не всегда работают в контейнерах, как hello среды радикально могут быть ограничены.</span><span class="sxs-lookup"><span data-stu-id="981f1-114">hello above commands work on Linux operating systems of almost all distributions, but do not necessarily work in containers, as hello environment can be radically constrained.</span></span> 

## <a name="detailed-walkthrough"></a><span data-ttu-id="981f1-115">Подробное пошаговое руководство</span><span class="sxs-lookup"><span data-stu-id="981f1-115">Detailed Walkthrough</span></span>

<span data-ttu-id="981f1-116">Использование открытый и закрытый ключи SSH — toolog простым способом hello в tooyour серверы Linux.</span><span class="sxs-lookup"><span data-stu-id="981f1-116">Using SSH public and private keys is hello easiest way toolog in tooyour Linux servers.</span></span> <span data-ttu-id="981f1-117">[Шифрование с открытым ключом](https://en.wikipedia.org/wiki/Public-key_cryptography) предоставляет гораздо более безопасный способ toolog в tooyour Linux или BSD виртуальную Машину в Azure чем пароль, который может быть принудительно применен гораздо проще.</span><span class="sxs-lookup"><span data-stu-id="981f1-117">[Public-key cryptography](https://en.wikipedia.org/wiki/Public-key_cryptography) provides a much more secure way toolog in tooyour Linux or BSD VM in Azure than passwords, which can be brute-forced far more easily.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="981f1-118">Открытый ключ можно предоставить любому пользователю, тогда как закрытый ключ принадлежит только вам (или локальной инфраструктуре безопасности).</span><span class="sxs-lookup"><span data-stu-id="981f1-118">Your public key can be shared with anyone; but only you (or your local security infrastructure) possess your private key.</span></span>  <span data-ttu-id="981f1-119">должен иметь закрытый ключ SSH Hello [высокий уровень безопасности пароля](https://www.xkcd.com/936/) (источник:[xkcd.com](https://xkcd.com)) toosafeguard его.</span><span class="sxs-lookup"><span data-stu-id="981f1-119">hello SSH private key should have a [very secure password](https://www.xkcd.com/936/) (source:[xkcd.com](https://xkcd.com)) toosafeguard it.</span></span>  <span data-ttu-id="981f1-120">Этот пароль должен быть закрытый ключ SSH просто tooaccess hello и **не** hello пароль учетной записи пользователя.</span><span class="sxs-lookup"><span data-stu-id="981f1-120">This password is just tooaccess hello private SSH key and **is not** hello user account password.</span></span>  <span data-ttu-id="981f1-121">При добавлении пароль tooyour SSH-ключ, шифрует hello закрытый ключ с помощью 128-разрядный AES, чтобы hello закрытый ключ не имеет смысла без пароля toodecrypt hello его.</span><span class="sxs-lookup"><span data-stu-id="981f1-121">When you add a password tooyour SSH key, it encrypts hello private key using 128-bit AES, so that hello private key is useless without hello password toodecrypt it.</span></span>  <span data-ttu-id="981f1-122">Если злоумышленник украсть ваш закрытый ключ и пароль не был ключ, они будут иметь доступ toouse, закрытый ключ toolog в tooany серверов, которые имеют hello соответствующего открытого ключа.</span><span class="sxs-lookup"><span data-stu-id="981f1-122">If an attacker stole your private key and that key did not have a password, they would be able toouse that private key toolog in tooany servers that have hello corresponding public key.</span></span>  <span data-ttu-id="981f1-123">Если закрытый ключ защищен паролем, злоумышленник не сможет использовать его. Такой подход обеспечивает дополнительный уровень безопасности инфраструктуры в Azure.</span><span class="sxs-lookup"><span data-stu-id="981f1-123">If a private key is password protected it cannot be used by that attacker, providing an additional layer of security for your infrastructure on Azure.</span></span>

<span data-ttu-id="981f1-124">В этой статье создает протокол SSH версии 2 RSA открытого и закрытого ключей файлы, которые рекомендуются для развертывания на hello диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="981f1-124">This article creates SSH protocol version 2 RSA public and private key files, which are recommended for deployments on hello Resource Manager.</span></span>  <span data-ttu-id="981f1-125">*SSH-rsa* в hello необходимы ключи [портала](https://portal.azure.com) классический и развертывания диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="981f1-125">*ssh-rsa* keys are required on hello [portal](https://portal.azure.com) for both classic and Resource Manager deployments.</span></span>

## <a name="disable-ssh-passwords-by-using-ssh-keys"></a><span data-ttu-id="981f1-126">Отключение паролей SSH за счет использования ключей SSH</span><span class="sxs-lookup"><span data-stu-id="981f1-126">Disable SSH passwords by using SSH keys</span></span>

<span data-ttu-id="981f1-127">В Azure необходимо использовать по крайней 2048-разрядные открытые и закрытые ключи в формате ssh-rsa.</span><span class="sxs-lookup"><span data-stu-id="981f1-127">Azure requires at least 2048-bit, ssh-rsa format public and private keys.</span></span> <span data-ttu-id="981f1-128">Используйте ключи toocreate hello `ssh-keygen`, который задает ряд вопросов, а затем записывает закрытого ключа и соответствующего открытого ключа.</span><span class="sxs-lookup"><span data-stu-id="981f1-128">toocreate hello keys use `ssh-keygen`, which asks a series of questions and then writes a private key and a matching public key.</span></span> <span data-ttu-id="981f1-129">При создании виртуальной Машины Azure открытый ключ hello копируется слишком`~/.ssh/authorized_keys`.</span><span class="sxs-lookup"><span data-stu-id="981f1-129">When an Azure VM is created, hello public key is copied too`~/.ssh/authorized_keys`.</span></span>  <span data-ttu-id="981f1-130">Ключи SSH в `~/.ssh/authorized_keys` , используемые toochallenge hello клиента toomatch hello соответствующий закрытый ключ для имени входа SSH-подключения.</span><span class="sxs-lookup"><span data-stu-id="981f1-130">SSH keys in `~/.ssh/authorized_keys` are used toochallenge hello client toomatch hello corresponding private key on an SSH login connection.</span></span>  <span data-ttu-id="981f1-131">При создании ВМ Linux Azure с помощью ключей SSH для проверки подлинности, Azure настраивает hello SSHD toonot сервера разрешить имен входа, пароль, только ключи SSH.</span><span class="sxs-lookup"><span data-stu-id="981f1-131">When an Azure Linux VM is created using SSH keys for authentication, Azure configures hello SSHD server toonot allow password logins, only SSH keys.</span></span>  <span data-ttu-id="981f1-132">Таким образом путем создания виртуальных машин Linux в Azure с ключи SSH, можно помочь hello безопасного развертывания виртуальной Машины и сохранить самостоятельно шаг стандартной конфигурации после развертывания hello отключения пароли в файле конфигурации sshd_config hello.</span><span class="sxs-lookup"><span data-stu-id="981f1-132">Therefore, by creating Azure Linux VMs with SSH keys, you can help secure hello VM deployment and save yourself hello typical post-deployment configuration step of disabling passwords in hello sshd_config config file.</span></span>

## <a name="using-ssh-keygen"></a><span data-ttu-id="981f1-133">Использование команды ssh-keygen</span><span class="sxs-lookup"><span data-stu-id="981f1-133">Using ssh-keygen</span></span>

<span data-ttu-id="981f1-134">Эта команда создает пароль, защищенным (зашифрованное) пару ключей SSH, с помощью RSA 2048 бит и его закомментирована tooeasily идентифицировать его.</span><span class="sxs-lookup"><span data-stu-id="981f1-134">This command creates a password secured (encrypted) SSH key pair using 2048-bit RSA and it is commented tooeasily identify it.</span></span>  

<span data-ttu-id="981f1-135">SSH ключи, по умолчанию хранится в hello `~/.ssh` каталога.</span><span class="sxs-lookup"><span data-stu-id="981f1-135">SSH keys are by default kept in hello `~/.ssh` directory.</span></span>  <span data-ttu-id="981f1-136">Если у вас `~/.ssh` каталог, hello `ssh-keygen` команда создает его с hello правильные разрешения.</span><span class="sxs-lookup"><span data-stu-id="981f1-136">If you do not have a `~/.ssh` directory, hello `ssh-keygen` command creates it for you with hello correct permissions.</span></span>

```bash
ssh-keygen \
-t rsa \
-b 2048 
```

<span data-ttu-id="981f1-137">*Описание команды*</span><span class="sxs-lookup"><span data-stu-id="981f1-137">*Command explained*</span></span>

<span data-ttu-id="981f1-138">`ssh-keygen`= hello программа, используемая toocreate hello ключи</span><span class="sxs-lookup"><span data-stu-id="981f1-138">`ssh-keygen` = hello program used toocreate hello keys</span></span>

<span data-ttu-id="981f1-139">`-t rsa`Тип ключа toocreate, который имеет формат RSA hello = [](https://en.wikipedia.org/wiki/RSA_(cryptosystem) Википедии</span><span class="sxs-lookup"><span data-stu-id="981f1-139">`-t rsa` = type of key toocreate which is hello RSA format [wikipedia](https://en.wikipedia.org/wiki/RSA_(cryptosystem)</span></span>

<span data-ttu-id="981f1-140">`-b 2048`= bits hello ключа</span><span class="sxs-lookup"><span data-stu-id="981f1-140">`-b 2048` = bits of hello key</span></span>


## <a name="classic-portal-and-x509-certs"></a><span data-ttu-id="981f1-141">Классический портал и сертификаты X.509</span><span class="sxs-lookup"><span data-stu-id="981f1-141">Classic portal and X.509 certs</span></span>

<span data-ttu-id="981f1-142">Если вы используете hello Azure [классический портал](https://manage.windowsazure.com/), это требует сертификаты X.509 для hello ключей SSH.</span><span class="sxs-lookup"><span data-stu-id="981f1-142">If you are using hello Azure [classic portal](https://manage.windowsazure.com/), it requires X.509 certs for hello SSH keys.</span></span>  <span data-ttu-id="981f1-143">Другие типы открытых ключей SSH не используются. *Требуются* только сертификаты X.509.</span><span class="sxs-lookup"><span data-stu-id="981f1-143">No other types of SSH public keys are allowed, they *must* be X.509 certs.</span></span>

<span data-ttu-id="981f1-144">toocreate сертификат X.509 с существующие закрытый ключ SSH-RSA:</span><span class="sxs-lookup"><span data-stu-id="981f1-144">toocreate an X.509 cert from your existing SSH-RSA private key:</span></span>

```bash
openssl req -x509 \
-key ~/.ssh/id_rsa \
-nodes \
-days 365 \
-newkey rsa:2048 \
-out ~/.ssh/id_rsa.pem
```

## <a name="classic-deploy-using-asm"></a><span data-ttu-id="981f1-145">Классическое развертывание с помощью `asm`</span><span class="sxs-lookup"><span data-stu-id="981f1-145">Classic deploy using `asm`</span></span>

<span data-ttu-id="981f1-146">Если используется классический hello развертывания модели (управления службами Azure CLI `asm`), можно использовать открытый ключ SSH-RSA или RFC4716 в формате ключа в **.pem** контейнера.</span><span class="sxs-lookup"><span data-stu-id="981f1-146">If you are using hello classic deploy model (Azure service management CLI `asm`), you can use an SSH-RSA public key or an RFC4716 formatted key in a **.pem** container.</span></span>  <span data-ttu-id="981f1-147">открытый ключ SSH-RSA Hello является то, что был создан ранее в этой статье с помощью `ssh-keygen`.</span><span class="sxs-lookup"><span data-stu-id="981f1-147">hello SSH-RSA public key is what was created earlier in this article using `ssh-keygen`.</span></span>

<span data-ttu-id="981f1-148">toocreate RFC4716 формат ключа из существующих открытый ключ SSH:</span><span class="sxs-lookup"><span data-stu-id="981f1-148">toocreate a RFC4716 formatted key from an existing SSH public key:</span></span>

```bash
ssh-keygen \
-f ~/.ssh/id_rsa.pub \
-e \
-m RFC4716 > ~/.ssh/id_ssh2.pem
```

## <a name="example-of-ssh-keygen"></a><span data-ttu-id="981f1-149">Пример с ssh-keygen</span><span class="sxs-lookup"><span data-stu-id="981f1-149">Example of ssh-keygen</span></span>

```bash
ssh-keygen -t rsa -b 2048 -C "ahmet@myserver"
Generating public/private rsa key pair.
Enter file in which toosave hello key (/home/ahmet/.ssh/id_rsa): 
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/ahmet/.ssh/id_rsa.
Your public key has been saved in /home/ahmet/.ssh/id_rsa.pub.
hello key fingerprint is:
14:a3:cb:3e:78:ad:25:cc:55:e9:0c:08:e5:d1:a9:08 ahmet@myserver
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

<span data-ttu-id="981f1-150">Сохраненные файлы ключей:</span><span class="sxs-lookup"><span data-stu-id="981f1-150">Saved key files:</span></span>

`Enter file in which toosave hello key (/home/ahmet/.ssh/id_rsa): ~/.ssh/id_rsa`

<span data-ttu-id="981f1-151">Имя Hello пару ключей для данной статьи.</span><span class="sxs-lookup"><span data-stu-id="981f1-151">hello key pair name for this article.</span></span>  <span data-ttu-id="981f1-152">Наличие пару ключей с именем **id_rsa** значения по умолчанию hello и ожидать, некоторые средства hello **id_rsa** имени файла закрытого ключа, имеющая одно имеет смысл.</span><span class="sxs-lookup"><span data-stu-id="981f1-152">Having a key pair named **id_rsa** is hello default and some tools might expect hello **id_rsa** private key file name so having one is a good idea.</span></span> <span data-ttu-id="981f1-153">каталог Hello `~/.ssh/` hello расположение по умолчанию для пар ключей SSH и файл конфигурации SSH hello.</span><span class="sxs-lookup"><span data-stu-id="981f1-153">hello directory `~/.ssh/` is hello default location for SSH key pairs and hello SSH config file.</span></span>  <span data-ttu-id="981f1-154">Если не указано с указанием полного пути `ssh-keygen` будет создавать ключи hello в текущем рабочем каталоге hello, не hello по умолчанию `~/.ssh`.</span><span class="sxs-lookup"><span data-stu-id="981f1-154">If not specified with a full path, `ssh-keygen` will create hello keys in hello current working directory, not hello default `~/.ssh`.</span></span>

<span data-ttu-id="981f1-155">Перечень hello `~/.ssh` каталога.</span><span class="sxs-lookup"><span data-stu-id="981f1-155">A listing of hello `~/.ssh` directory.</span></span>

```bash
ls -al ~/.ssh
-rw------- 1 ahmet staff  1675 Aug 25 18:04 id_rsa
-rw-r--r-- 1 ahmet staff   410 Aug 25 18:04 rsa.pub
```

<span data-ttu-id="981f1-156">Пароль ключа:</span><span class="sxs-lookup"><span data-stu-id="981f1-156">Key Password:</span></span>

`Enter passphrase (empty for no passphrase):`

<span data-ttu-id="981f1-157">`ssh-keygen`закрытый ключ hello tooencrypt tooa пароль, используемый диск называется «парольную фразу.»</span><span class="sxs-lookup"><span data-stu-id="981f1-157">`ssh-keygen` refers tooa password used tooencrypt hello private key as "a passphrase."</span></span>  <span data-ttu-id="981f1-158">Это *строго* рекомендуется tooadd пары ключей tooyour парольную фразу.</span><span class="sxs-lookup"><span data-stu-id="981f1-158">It is *strongly* recommended tooadd a passphrase tooyour key pairs.</span></span> <span data-ttu-id="981f1-159">Без парольную фразу защищающее hello закрытого ключа имеющему hello файла ключа можно использовать toolog в tooany сервер, имеющий hello соответствующего открытого ключа.</span><span class="sxs-lookup"><span data-stu-id="981f1-159">Without a passphrase protecting hello private key, anyone with hello key file can use it toolog in tooany server that has hello corresponding public key.</span></span> <span data-ttu-id="981f1-160">Добавление парольную фразу предлагает дополнительные защиты в случае, если кто-то — может toogain доступа tooyour файла закрытого ключа, что дает время toochange hello ключи, используемые tooauthenticate вы.</span><span class="sxs-lookup"><span data-stu-id="981f1-160">Adding a passphrase offers more protection in case someone is able toogain access tooyour private key file, giving you time toochange hello keys used tooauthenticate you.</span></span>

## <a name="using-ssh-agent-toostore-your-private-key-password"></a><span data-ttu-id="981f1-161">С помощью ssh агента toostore пароль закрытого ключа</span><span class="sxs-lookup"><span data-stu-id="981f1-161">Using ssh-agent toostore your private key password</span></span>

<span data-ttu-id="981f1-162">Введите ваш закрытый ключ tooavoid файл парольную фразу все имена входа SSH, можно использовать `ssh-agent` toocache пароль файла закрытого ключа.</span><span class="sxs-lookup"><span data-stu-id="981f1-162">tooavoid typing your private key file passphrase with every SSH login, you can use `ssh-agent` toocache your private key file password.</span></span> <span data-ttu-id="981f1-163">При использовании Mac OSX цепочки ключей hello надежно сохраняет пароли закрытых ключей hello при вызове `ssh-agent`.</span><span class="sxs-lookup"><span data-stu-id="981f1-163">If you are using a Mac, hello OSX Keychain securely stores hello private key passwords when you invoke `ssh-agent`.</span></span>

<span data-ttu-id="981f1-164">Проверить и использовать `ssh-agent` и `ssh-add` tooinform hello SSH системы о hello ключевых файлов, чтобы hello парольная фраза не нужно использовать в интерактивном режиме toobe.</span><span class="sxs-lookup"><span data-stu-id="981f1-164">Verify and use `ssh-agent` and `ssh-add` tooinform hello SSH system about hello key files so that hello passphrase will not need toobe used interactively.</span></span>

```bash
eval "$(ssh-agent -s)"
```

<span data-ttu-id="981f1-165">Теперь добавьте закрытый ключ hello слишком`ssh-agent` с помощью команды hello `ssh-add`.</span><span class="sxs-lookup"><span data-stu-id="981f1-165">Now add hello private key too`ssh-agent` using hello command `ssh-add`.</span></span>

```bash
ssh-add ~/.ssh/id_rsa
```

<span data-ttu-id="981f1-166">Hello пароль закрытого ключа сохраняется в `ssh-agent`.</span><span class="sxs-lookup"><span data-stu-id="981f1-166">hello private key password is now stored in `ssh-agent`.</span></span>

## <a name="using-ssh-copy-id-tooinstall-hello-new-key"></a><span data-ttu-id="981f1-167">С помощью `ssh-copy-id` tooinstall hello новый ключ</span><span class="sxs-lookup"><span data-stu-id="981f1-167">Using `ssh-copy-id` tooinstall hello new key</span></span>
<span data-ttu-id="981f1-168">При создании виртуальной Машины можно установить hello новый SSH открытого ключа tooyour виртуальной Машины Linux при hello следующую команду, заменив имя пользователя виртуальной Машины hello и адрес сервера hello собственные значения.</span><span class="sxs-lookup"><span data-stu-id="981f1-168">If you have already created a VM you can install hello new SSH public key tooyour Linux VM with hello following command, replacing hello VM username and hello server address with your own values:</span></span>

```bash
ssh-copy-id -i ~/.ssh/id_rsa.pub ahmet@myserver
```

## <a name="create-and-configure-an-ssh-config-file"></a><span data-ttu-id="981f1-169">Создание и настройка файла конфигурации SSH</span><span class="sxs-lookup"><span data-stu-id="981f1-169">Create and configure an SSH config file</span></span>

<span data-ttu-id="981f1-170">Он является наиболее toocreate рекомендаций и настроить `~/.ssh/config` toospeed файл вверх имена входа и оптимизации поведение клиента SSH.</span><span class="sxs-lookup"><span data-stu-id="981f1-170">It is a best practice toocreate and configure an `~/.ssh/config` file toospeed up log ins and for optimizing your SSH client behavior.</span></span>

<span data-ttu-id="981f1-171">Следующий пример Hello показывает стандартной конфигурации.</span><span class="sxs-lookup"><span data-stu-id="981f1-171">hello following example shows a standard configuration.</span></span>

### <a name="create-hello-file"></a><span data-ttu-id="981f1-172">Создайте файл hello</span><span class="sxs-lookup"><span data-stu-id="981f1-172">Create hello file</span></span>

```bash
touch ~/.ssh/config
```

### <a name="edit-hello-file-tooadd-hello-new-ssh-configuration"></a><span data-ttu-id="981f1-173">Изменение hello файл tooadd hello новой конфигурации SSH:</span><span class="sxs-lookup"><span data-stu-id="981f1-173">Edit hello file tooadd hello new SSH configuration:</span></span>

```bash
vim ~/.ssh/config
```

### <a name="example-sshconfig-file"></a><span data-ttu-id="981f1-174">Пример файла `~/.ssh/config`:</span><span class="sxs-lookup"><span data-stu-id="981f1-174">Example `~/.ssh/config` file:</span></span>

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

<span data-ttu-id="981f1-175">Это дает конфигурации SSH, вы разделы для каждого сервера tooenable каждого toohave свой собственный выделенный пару ключей.</span><span class="sxs-lookup"><span data-stu-id="981f1-175">This SSH config gives you sections for each server tooenable each toohave its own dedicated key pair.</span></span> <span data-ttu-id="981f1-176">Здравствуйте, параметры по умолчанию (`Host *`) предназначены для тех узлах, которые не соответствует ни одному из hello конкретных узлов, чем в файле конфигурации hello.</span><span class="sxs-lookup"><span data-stu-id="981f1-176">hello default settings (`Host *`) are for any hosts that do not match any of hello specific hosts higher up in hello config file.</span></span>

### <a name="config-file-explained"></a><span data-ttu-id="981f1-177">Описание файла конфигурации</span><span class="sxs-lookup"><span data-stu-id="981f1-177">Config file explained</span></span>

<span data-ttu-id="981f1-178">`Host`= hello имя узла hello, вызываемый на hello терминалов.</span><span class="sxs-lookup"><span data-stu-id="981f1-178">`Host` = hello name of hello host being called on hello terminal.</span></span>  <span data-ttu-id="981f1-179">`ssh fedora22`сообщает `SSH` toouse значения hello в блоке settings hello с меткой `Host fedora22` Примечание: для узла можно указать любую метку, для использования логического и не представляют Привет фактическое имя узла любого сервера.</span><span class="sxs-lookup"><span data-stu-id="981f1-179">`ssh fedora22` tells `SSH` toouse hello values in hello settings block labeled `Host fedora22`  NOTE: Host can be any label that is logical for your usage and does not represent hello actual hostname of any server.</span></span>

<span data-ttu-id="981f1-180">`Hostname 102.160.203.241`= hello IP-адрес или DNS-имя сервера hello к которому выполняется доступ.</span><span class="sxs-lookup"><span data-stu-id="981f1-180">`Hostname 102.160.203.241` = hello IP address or DNS name for hello server being accessed.</span></span>

<span data-ttu-id="981f1-181">`User ahmet`= toouse учетную запись удаленного пользователя hello при входе toohello сервера.</span><span class="sxs-lookup"><span data-stu-id="981f1-181">`User ahmet` = hello remote user account toouse when logging in toohello server.</span></span>

<span data-ttu-id="981f1-182">`PubKeyAuthentication yes`= сообщает SSH требуется toouse toolog ключа SSH.</span><span class="sxs-lookup"><span data-stu-id="981f1-182">`PubKeyAuthentication yes` = tells SSH you want toouse an SSH key toolog in.</span></span>

<span data-ttu-id="981f1-183">`IdentityFile /home/ahmet/.ssh/id_id_rsa`= hello SSH закрытого ключа и соответствующего открытого ключа toouse для проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="981f1-183">`IdentityFile /home/ahmet/.ssh/id_id_rsa` = hello SSH private key and corresponding public key toouse for authentication.</span></span>

## <a name="ssh-into-linux-without-a-password"></a><span data-ttu-id="981f1-184">Вход в Linux с использованием SSH без пароля</span><span class="sxs-lookup"><span data-stu-id="981f1-184">SSH into Linux without a password</span></span>

<span data-ttu-id="981f1-185">Теперь, когда у вас есть пару ключей SSH и настроенный файл конфигурации SSH, быстро и надежно являются может toolog в tooyour виртуальной Машины с Linux.</span><span class="sxs-lookup"><span data-stu-id="981f1-185">Now that you have an SSH key pair and a configured SSH config file, you are able toolog in tooyour Linux VM quickly and securely.</span></span> <span data-ttu-id="981f1-186">Здравствуйте, во время первого входа в tooa сервера, с помощью SSH ключа hello командные строки можно для hello парольную фразу для этого файла ключа.</span><span class="sxs-lookup"><span data-stu-id="981f1-186">hello first time you log in tooa server using an SSH key hello command prompts you for hello passphrase for that key file.</span></span>

```bash
ssh fedora22
```

### <a name="command-explained"></a><span data-ttu-id="981f1-187">Описание команды</span><span class="sxs-lookup"><span data-stu-id="981f1-187">Command explained</span></span>

<span data-ttu-id="981f1-188">Когда `ssh fedora22` выполнении SSH сначала находит и загружает все параметры из hello `Host fedora22` блока, а затем загружает все hello оставшиеся параметры из hello последний блок `Host *`.</span><span class="sxs-lookup"><span data-stu-id="981f1-188">When `ssh fedora22` is executed SSH first locates and loads any settings from hello `Host fedora22` block, and then loads all hello remaining settings from hello last block, `Host *`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="981f1-189">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="981f1-189">Next Steps</span></span>

<span data-ttu-id="981f1-190">Далее вверх toocreate виртуальных машин Linux Azure использует hello новый SSH открытый ключ.</span><span class="sxs-lookup"><span data-stu-id="981f1-190">Next up is toocreate Azure Linux VMs using hello new SSH public key.</span></span>  <span data-ttu-id="981f1-191">Виртуальные машины Azure, созданных с помощью открытого ключа SSH от имени для входа hello, лучше защищенным, чем виртуальные машины, созданные с помощью метода входа по умолчанию hello, пароли.</span><span class="sxs-lookup"><span data-stu-id="981f1-191">Azure VMs that are created with an SSH public key as hello login are better secured than VMs created with hello default login method, passwords.</span></span>  <span data-ttu-id="981f1-192">В настройках виртуальных машин Azure, созданных с помощью ключей SSH, пароли отключены по умолчанию для защиты от атак методом подбора.</span><span class="sxs-lookup"><span data-stu-id="981f1-192">Azure VMs created using SSH keys are by default configured with passwords disabled, avoiding brute-forced guessing attempts.</span></span> <span data-ttu-id="981f1-193">Если необходима дополнительная помощь при создании вашего пару ключей SSH или требуются дополнительные сертификаты, например, для использования с классического портала hello, см. раздел [подробные пар ключей SSH toocreate действия и сертификаты](create-ssh-keys-detailed.md).</span><span class="sxs-lookup"><span data-stu-id="981f1-193">If you need more assistance in creating your SSH key pair or require additional certificates, such as for use with hello classic portal, see [Detailed steps toocreate SSH key pairs and certificates](create-ssh-keys-detailed.md).</span></span>

* [<span data-ttu-id="981f1-194">Создание защищенной виртуальной машины Linux с помощью шаблона Azure</span><span class="sxs-lookup"><span data-stu-id="981f1-194">Create a secure Linux VM using an Azure template</span></span>](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="981f1-195">Создание безопасного ВМ Linux с помощью hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="981f1-195">Create a secure Linux VM using hello Azure portal</span></span>](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="981f1-196">Создание безопасного ВМ Linux с помощью hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="981f1-196">Create a secure Linux VM using hello Azure CLI</span></span>](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
