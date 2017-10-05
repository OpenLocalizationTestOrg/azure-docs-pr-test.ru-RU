---
title: "Создание пары ключей SSH для виртуальных машин Linux в Azure | Документация Майкрософт"
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
ms.openlocfilehash: 19acd4efca7ef043f31b436b96f9129caee9591b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-ssh-public-and-private-key-pair-for-linux-vms"></a><span data-ttu-id="39c8b-103">Создание пары из открытого и закрытого ключей SSH для виртуальных машин Linux</span><span class="sxs-lookup"><span data-stu-id="39c8b-103">Create an SSH public and private key pair for Linux VMs</span></span>

<span data-ttu-id="39c8b-104">В этой статье показано, как создать пару файлов открытого и закрытого ключей в формате SSH-RSA для виртуальных машин Linux.</span><span class="sxs-lookup"><span data-stu-id="39c8b-104">This article shows you how to generate an SSH protocol version 2 RSA public and private key file pair to use with Linux VMs.</span></span>  <span data-ttu-id="39c8b-105">С помощью пары ключей SSH в Azure можно создавать виртуальные машины, по умолчанию использующие ключи SSH для проверки подлинности, что позволяет обойтись без паролей для входа.</span><span class="sxs-lookup"><span data-stu-id="39c8b-105">With an SSH key pair, you can create Virtual Machines on Azure that default to using SSH keys for authentication, eliminating the need for passwords to log in.</span></span>  <span data-ttu-id="39c8b-106">Так как существует вероятность подбора пароля, ваши виртуальные машины могут подвергаться непрерывным попыткам взлома.</span><span class="sxs-lookup"><span data-stu-id="39c8b-106">Passwords can be guessed, and open your VMs up to relentless brute force attempts to guess your password.</span></span> <span data-ttu-id="39c8b-107">При развертывании виртуальные машины, созданные с помощью шаблонов Azure или `azure-cli`, могут содержать открытый ключ SSH, что устраняет необходимость в настройке после развертывания, а именно в отключении входа с использованием пароля для SSH.</span><span class="sxs-lookup"><span data-stu-id="39c8b-107">VMs created with Azure Templates or the `azure-cli` can include your SSH public key as part of the deployment, removing a post deployment configuration step of disabling password logins for SSH.</span></span>

## <a name="quick-commands"></a><span data-ttu-id="39c8b-108">Быстрые команды</span><span class="sxs-lookup"><span data-stu-id="39c8b-108">Quick Commands</span></span>

<span data-ttu-id="39c8b-109">Выполните следующие команды из оболочки Bash, заменяя примеры собственными значениями.</span><span class="sxs-lookup"><span data-stu-id="39c8b-109">Run the following commands from a Bash shell, replacing the examples with your own choices.</span></span>

<span data-ttu-id="39c8b-110">По умолчанию файл открытого ключа SSH создается в каталоге `~/.ssh/id_rsa.pub`.</span><span class="sxs-lookup"><span data-stu-id="39c8b-110">Your SSH public key file is by default created at `~/.ssh/id_rsa.pub`.</span></span> <span data-ttu-id="39c8b-111">При появлении запроса создайте парольную фразу, необходимую для защиты закрытого ключа, с помощью приведенной ниже команды.</span><span class="sxs-lookup"><span data-stu-id="39c8b-111">When prompted using the following command, you should create a "passphrase" to secure your private key.</span></span> <span data-ttu-id="39c8b-112">(Парольная фраза — это пароль, используемый для шифрования закрытого ключа.)</span><span class="sxs-lookup"><span data-stu-id="39c8b-112">(The passphrase is a password used to encrypt your private key.)</span></span>

```bash
ssh-keygen -t rsa -b 2048 
```

<span data-ttu-id="39c8b-113">Добавьте созданный ключ в `ssh-agent`:</span><span class="sxs-lookup"><span data-stu-id="39c8b-113">Add the newly created key to `ssh-agent`:</span></span>

```bash
ssh-add ~/.ssh/id_rsa
```

> [!IMPORTANT] 
> <span data-ttu-id="39c8b-114">Приведенные выше команды работают в операционных системах Linux на основе практически всех дистрибутивов, но не обязательно будут работать в контейнерах, так как среда может быть сильно ограничена.</span><span class="sxs-lookup"><span data-stu-id="39c8b-114">The above commands work on Linux operating systems of almost all distributions, but do not necessarily work in containers, as the environment can be radically constrained.</span></span> 

## <a name="detailed-walkthrough"></a><span data-ttu-id="39c8b-115">Подробное пошаговое руководство</span><span class="sxs-lookup"><span data-stu-id="39c8b-115">Detailed Walkthrough</span></span>

<span data-ttu-id="39c8b-116">Использование открытого и закрытого ключей SSH — это самый простой способ войти на серверы Linux.</span><span class="sxs-lookup"><span data-stu-id="39c8b-116">Using SSH public and private keys is the easiest way to log in to your Linux servers.</span></span> <span data-ttu-id="39c8b-117">[Шифрование с открытым ключом](https://en.wikipedia.org/wiki/Public-key_cryptography) обеспечивает большую безопасность при входе на виртуальные машины Linux или BSD в Azure, чем использование паролей, которые довольно легко получить методом подбора.</span><span class="sxs-lookup"><span data-stu-id="39c8b-117">[Public-key cryptography](https://en.wikipedia.org/wiki/Public-key_cryptography) provides a much more secure way to log in to your Linux or BSD VM in Azure than passwords, which can be brute-forced far more easily.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="39c8b-118">Открытый ключ можно предоставить любому пользователю, тогда как закрытый ключ принадлежит только вам (или локальной инфраструктуре безопасности).</span><span class="sxs-lookup"><span data-stu-id="39c8b-118">Your public key can be shared with anyone; but only you (or your local security infrastructure) possess your private key.</span></span>  <span data-ttu-id="39c8b-119">Закрытый ключ SSH должен быть защищен [очень надежным паролем](https://www.xkcd.com/936/) (источник: [xkcd.com](https://xkcd.com)).</span><span class="sxs-lookup"><span data-stu-id="39c8b-119">The SSH private key should have a [very secure password](https://www.xkcd.com/936/) (source:[xkcd.com](https://xkcd.com)) to safeguard it.</span></span>  <span data-ttu-id="39c8b-120">Это пароль для доступа к закрытому ключу SSH, а **не** пароль к учетной записи пользователя.</span><span class="sxs-lookup"><span data-stu-id="39c8b-120">This password is just to access the private SSH key and **is not** the user account password.</span></span>  <span data-ttu-id="39c8b-121">Когда вы добавите к ключу SSH пароль, закрытый ключ будет зашифрован с помощью 128-разрядного ключа AES. После этого закрытый ключ нельзя будет использовать без пароля для разблокировки.</span><span class="sxs-lookup"><span data-stu-id="39c8b-121">When you add a password to your SSH key, it encrypts the private key using 128-bit AES, so that the private key is useless without the password to decrypt it.</span></span>  <span data-ttu-id="39c8b-122">Если злоумышленник украдет ваш закрытый ключ, не защищенный паролем, он сможет воспользоваться этим ключом для входа на серверы, на которых установлен соответствующий открытый ключ.</span><span class="sxs-lookup"><span data-stu-id="39c8b-122">If an attacker stole your private key and that key did not have a password, they would be able to use that private key to log in to any servers that have the corresponding public key.</span></span>  <span data-ttu-id="39c8b-123">Если закрытый ключ защищен паролем, злоумышленник не сможет использовать его. Такой подход обеспечивает дополнительный уровень безопасности инфраструктуры в Azure.</span><span class="sxs-lookup"><span data-stu-id="39c8b-123">If a private key is password protected it cannot be used by that attacker, providing an additional layer of security for your infrastructure on Azure.</span></span>

<span data-ttu-id="39c8b-124">В этой статье рассматривается создание файлов открытого и закрытого ключей в формате SSH-RSA. Мы рекомендуем использовать именно их при развертывании с помощью Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="39c8b-124">This article creates SSH protocol version 2 RSA public and private key files, which are recommended for deployments on the Resource Manager.</span></span>  <span data-ttu-id="39c8b-125">Ключи *ssh-rsa* являются обязательными при развертываниях на [портале](https://portal.azure.com) (как в классической модели, так и в модели развертывания с помощью Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="39c8b-125">*ssh-rsa* keys are required on the [portal](https://portal.azure.com) for both classic and Resource Manager deployments.</span></span>

## <a name="disable-ssh-passwords-by-using-ssh-keys"></a><span data-ttu-id="39c8b-126">Отключение паролей SSH за счет использования ключей SSH</span><span class="sxs-lookup"><span data-stu-id="39c8b-126">Disable SSH passwords by using SSH keys</span></span>

<span data-ttu-id="39c8b-127">В Azure необходимо использовать по крайней 2048-разрядные открытые и закрытые ключи в формате ssh-rsa.</span><span class="sxs-lookup"><span data-stu-id="39c8b-127">Azure requires at least 2048-bit, ssh-rsa format public and private keys.</span></span> <span data-ttu-id="39c8b-128">Чтобы создать ключи, выполните команду `ssh-keygen`, которая задаст несколько вопросов, а затем запишет закрытый ключ и соответствующий открытый ключ.</span><span class="sxs-lookup"><span data-stu-id="39c8b-128">To create the keys use `ssh-keygen`, which asks a series of questions and then writes a private key and a matching public key.</span></span> <span data-ttu-id="39c8b-129">При создании виртуальной машины Azure открытый ключ копируется в `~/.ssh/authorized_keys`.</span><span class="sxs-lookup"><span data-stu-id="39c8b-129">When an Azure VM is created, the public key is copied to `~/.ssh/authorized_keys`.</span></span>  <span data-ttu-id="39c8b-130">Ключи SSH в `~/.ssh/authorized_keys` используются для запросов к клиенту, который должен подобрать соответствующий закрытый ключ при SSH-подключении для входа.</span><span class="sxs-lookup"><span data-stu-id="39c8b-130">SSH keys in `~/.ssh/authorized_keys` are used to challenge the client to match the corresponding private key on an SSH login connection.</span></span>  <span data-ttu-id="39c8b-131">При создании виртуальной машины Linux в Azure с использованием ключей SSH для проверки подлинности Azure настраивает сервер SSHD таким образом, чтобы для входа можно было использовать только ключи SSH.</span><span class="sxs-lookup"><span data-stu-id="39c8b-131">When an Azure Linux VM is created using SSH keys for authentication, Azure configures the SSHD server to not allow password logins, only SSH keys.</span></span>  <span data-ttu-id="39c8b-132">Таким образом, создавая виртуальные машины Azure Linux с использованием ключей SSH, вы защищаете это развертывание и выполняете стандартный шаг настройки после развертывания — отключаете пароли в файле конфигурации sshd_config.</span><span class="sxs-lookup"><span data-stu-id="39c8b-132">Therefore, by creating Azure Linux VMs with SSH keys, you can help secure the VM deployment and save yourself the typical post-deployment configuration step of disabling passwords in the sshd_config config file.</span></span>

## <a name="using-ssh-keygen"></a><span data-ttu-id="39c8b-133">Использование команды ssh-keygen</span><span class="sxs-lookup"><span data-stu-id="39c8b-133">Using ssh-keygen</span></span>

<span data-ttu-id="39c8b-134">Эта команда создает пару защищенных паролем (зашифрованных) ключей SSH, используя 2048-разрядный RSA. К этой паре можно добавить комментарий, чтобы ее потом можно было легко определить.</span><span class="sxs-lookup"><span data-stu-id="39c8b-134">This command creates a password secured (encrypted) SSH key pair using 2048-bit RSA and it is commented to easily identify it.</span></span>  

<span data-ttu-id="39c8b-135">Ключи SSH по умолчанию хранятся в каталоге `~/.ssh`.</span><span class="sxs-lookup"><span data-stu-id="39c8b-135">SSH keys are by default kept in the `~/.ssh` directory.</span></span>  <span data-ttu-id="39c8b-136">Если у вас нет каталога `~/.ssh`, создайте его с правильными разрешениями с помощью команды `ssh-keygen`.</span><span class="sxs-lookup"><span data-stu-id="39c8b-136">If you do not have a `~/.ssh` directory, the `ssh-keygen` command creates it for you with the correct permissions.</span></span>

```bash
ssh-keygen \
-t rsa \
-b 2048 
```

<span data-ttu-id="39c8b-137">*Описание команды*</span><span class="sxs-lookup"><span data-stu-id="39c8b-137">*Command explained*</span></span>

<span data-ttu-id="39c8b-138">`ssh-keygen` — программа, с помощью которой создаются ключи.</span><span class="sxs-lookup"><span data-stu-id="39c8b-138">`ssh-keygen` = the program used to create the keys</span></span>

<span data-ttu-id="39c8b-139">`-t rsa` — тип ключа, который создается в формате RSA [wikipedia](https://ru.wikipedia.org/wiki/RSA).</span><span class="sxs-lookup"><span data-stu-id="39c8b-139">`-t rsa` = type of key to create which is the RSA format [wikipedia](https://en.wikipedia.org/wiki/RSA_(cryptosystem)</span></span>

<span data-ttu-id="39c8b-140">`-b 2048` — число битов в ключе.</span><span class="sxs-lookup"><span data-stu-id="39c8b-140">`-b 2048` = bits of the key</span></span>


## <a name="classic-portal-and-x509-certs"></a><span data-ttu-id="39c8b-141">Классический портал и сертификаты X.509</span><span class="sxs-lookup"><span data-stu-id="39c8b-141">Classic portal and X.509 certs</span></span>

<span data-ttu-id="39c8b-142">Если вы используете [классический портал](https://manage.windowsazure.com/) Azure, вам понадобятся сертификаты X.509 для ключей SSH.</span><span class="sxs-lookup"><span data-stu-id="39c8b-142">If you are using the Azure [classic portal](https://manage.windowsazure.com/), it requires X.509 certs for the SSH keys.</span></span>  <span data-ttu-id="39c8b-143">Другие типы открытых ключей SSH не используются. *Требуются* только сертификаты X.509.</span><span class="sxs-lookup"><span data-stu-id="39c8b-143">No other types of SSH public keys are allowed, they *must* be X.509 certs.</span></span>

<span data-ttu-id="39c8b-144">Чтобы создать сертификат X.509 из существующего закрытого ключа SSH RSA, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="39c8b-144">To create an X.509 cert from your existing SSH-RSA private key:</span></span>

```bash
openssl req -x509 \
-key ~/.ssh/id_rsa \
-nodes \
-days 365 \
-newkey rsa:2048 \
-out ~/.ssh/id_rsa.pem
```

## <a name="classic-deploy-using-asm"></a><span data-ttu-id="39c8b-145">Классическое развертывание с помощью `asm`</span><span class="sxs-lookup"><span data-stu-id="39c8b-145">Classic deploy using `asm`</span></span>

<span data-ttu-id="39c8b-146">При использовании классической модели развертывания (интерфейс командной строки `asm` управления службами Azure) вы можете использовать открытый ключ SSH-RSA или ключ в формате RFC4716 в контейнере **PEM**.</span><span class="sxs-lookup"><span data-stu-id="39c8b-146">If you are using the classic deploy model (Azure service management CLI `asm`), you can use an SSH-RSA public key or an RFC4716 formatted key in a **.pem** container.</span></span>  <span data-ttu-id="39c8b-147">Открытый ключ SSH-RSA вы создали ранее в рамках этого руководства с помощью `ssh-keygen`.</span><span class="sxs-lookup"><span data-stu-id="39c8b-147">The SSH-RSA public key is what was created earlier in this article using `ssh-keygen`.</span></span>

<span data-ttu-id="39c8b-148">Чтобы создать ключ в формате RFC4716 из существующего открытого ключа SSH, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="39c8b-148">To create a RFC4716 formatted key from an existing SSH public key:</span></span>

```bash
ssh-keygen \
-f ~/.ssh/id_rsa.pub \
-e \
-m RFC4716 > ~/.ssh/id_ssh2.pem
```

## <a name="example-of-ssh-keygen"></a><span data-ttu-id="39c8b-149">Пример с ssh-keygen</span><span class="sxs-lookup"><span data-stu-id="39c8b-149">Example of ssh-keygen</span></span>

```bash
ssh-keygen -t rsa -b 2048 -C "ahmet@myserver"
Generating public/private rsa key pair.
Enter file in which to save the key (/home/ahmet/.ssh/id_rsa): 
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/ahmet/.ssh/id_rsa.
Your public key has been saved in /home/ahmet/.ssh/id_rsa.pub.
The key fingerprint is:
14:a3:cb:3e:78:ad:25:cc:55:e9:0c:08:e5:d1:a9:08 ahmet@myserver
The keys randomart image is:
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

<span data-ttu-id="39c8b-150">Сохраненные файлы ключей:</span><span class="sxs-lookup"><span data-stu-id="39c8b-150">Saved key files:</span></span>

`Enter file in which to save the key (/home/ahmet/.ssh/id_rsa): ~/.ssh/id_rsa`

<span data-ttu-id="39c8b-151">Имя пары ключей, используемое в этой статье.</span><span class="sxs-lookup"><span data-stu-id="39c8b-151">The key pair name for this article.</span></span>  <span data-ttu-id="39c8b-152">По умолчанию пара ключей называется **id_rsa**. Так как некоторые средства ожидаемо ищут закрытый ключ в файле с именем **id_rsa**, есть смысл создать такой файл.</span><span class="sxs-lookup"><span data-stu-id="39c8b-152">Having a key pair named **id_rsa** is the default and some tools might expect the **id_rsa** private key file name so having one is a good idea.</span></span> <span data-ttu-id="39c8b-153">Пары ключей SSH и файл конфигурации SSH по умолчанию располагаются в каталоге `~/.ssh/`.</span><span class="sxs-lookup"><span data-stu-id="39c8b-153">The directory `~/.ssh/` is the default location for SSH key pairs and the SSH config file.</span></span>  <span data-ttu-id="39c8b-154">Если не указать полный путь, с помощью `ssh-keygen` будут созданы ключи в текущем рабочем каталоге, а не в стандартном каталоге `~/.ssh`.</span><span class="sxs-lookup"><span data-stu-id="39c8b-154">If not specified with a full path, `ssh-keygen` will create the keys in the current working directory, not the default `~/.ssh`.</span></span>

<span data-ttu-id="39c8b-155">Описание каталога `~/.ssh`.</span><span class="sxs-lookup"><span data-stu-id="39c8b-155">A listing of the `~/.ssh` directory.</span></span>

```bash
ls -al ~/.ssh
-rw------- 1 ahmet staff  1675 Aug 25 18:04 id_rsa
-rw-r--r-- 1 ahmet staff   410 Aug 25 18:04 rsa.pub
```

<span data-ttu-id="39c8b-156">Пароль ключа:</span><span class="sxs-lookup"><span data-stu-id="39c8b-156">Key Password:</span></span>

`Enter passphrase (empty for no passphrase):`

<span data-ttu-id="39c8b-157">В качестве парольной фразы `ssh-keygen` ссылается на пароль, используемый для шифрования закрытого ключа.</span><span class="sxs-lookup"><span data-stu-id="39c8b-157">`ssh-keygen` refers to a password used to encrypt the private key as "a passphrase."</span></span>  <span data-ttu-id="39c8b-158">Мы *настоятельно* рекомендуем добавить парольную фразу к своей паре ключей.</span><span class="sxs-lookup"><span data-stu-id="39c8b-158">It is *strongly* recommended to add a passphrase to your key pairs.</span></span> <span data-ttu-id="39c8b-159">Если не защитить закрытый ключ парольной фразой, любой пользователь, у которого есть файл ключа, сможет использовать его, чтобы войти на любой из серверов, для которого предусмотрен соответствующий открытый ключ.</span><span class="sxs-lookup"><span data-stu-id="39c8b-159">Without a passphrase protecting the private key, anyone with the key file can use it to log in to any server that has the corresponding public key.</span></span> <span data-ttu-id="39c8b-160">Добавив парольную фразу, вы усилите защиту на случай, если другой пользователь получит доступ к файлу закрытого ключа. Это даст вам время, чтобы изменить ключи для проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="39c8b-160">Adding a passphrase offers more protection in case someone is able to gain access to your private key file, giving you time to change the keys used to authenticate you.</span></span>

## <a name="using-ssh-agent-to-store-your-private-key-password"></a><span data-ttu-id="39c8b-161">Использование ssh-agent для хранения пароля закрытого ключа</span><span class="sxs-lookup"><span data-stu-id="39c8b-161">Using ssh-agent to store your private key password</span></span>

<span data-ttu-id="39c8b-162">Чтобы не вводить парольную фразу файла закрытого ключа при каждом входе с использованием SSH, вы можете создать кэш пароля от файла закрытого ключа с помощью команды `ssh-agent`.</span><span class="sxs-lookup"><span data-stu-id="39c8b-162">To avoid typing your private key file passphrase with every SSH login, you can use `ssh-agent` to cache your private key file password.</span></span> <span data-ttu-id="39c8b-163">Если вы используете компьютер Mac, при вызове `ssh-agent`пароли закрытых ключей будут надежно сохранены в цепочке ключей OS X.</span><span class="sxs-lookup"><span data-stu-id="39c8b-163">If you are using a Mac, the OSX Keychain securely stores the private key passwords when you invoke `ssh-agent`.</span></span>

<span data-ttu-id="39c8b-164">С помощью `ssh-agent` и `ssh-add` определите для системы SSH файлы ключей, чтобы вам не нужно было использовать парольную фразу в интерактивном режиме.</span><span class="sxs-lookup"><span data-stu-id="39c8b-164">Verify and use `ssh-agent` and `ssh-add` to inform the SSH system about the key files so that the passphrase will not need to be used interactively.</span></span>

```bash
eval "$(ssh-agent -s)"
```

<span data-ttu-id="39c8b-165">Затем добавьте закрытый ключ к `ssh-agent` с помощью команды `ssh-add`.</span><span class="sxs-lookup"><span data-stu-id="39c8b-165">Now add the private key to `ssh-agent` using the command `ssh-add`.</span></span>

```bash
ssh-add ~/.ssh/id_rsa
```

<span data-ttu-id="39c8b-166">Теперь пароль закрытого ключа хранится в `ssh-agent`.</span><span class="sxs-lookup"><span data-stu-id="39c8b-166">The private key password is now stored in `ssh-agent`.</span></span>

## <a name="using-ssh-copy-id-to-install-the-new-key"></a><span data-ttu-id="39c8b-167">Использование `ssh-copy-id` для установки нового ключа</span><span class="sxs-lookup"><span data-stu-id="39c8b-167">Using `ssh-copy-id` to install the new key</span></span>
<span data-ttu-id="39c8b-168">Если виртуальная машина Linux уже создана, вы можете установить для нее новый открытый ключ SSH с помощью приведенной ниже команды, заменив имя пользователя виртуальной машины и адрес сервера собственными значениями.</span><span class="sxs-lookup"><span data-stu-id="39c8b-168">If you have already created a VM you can install the new SSH public key to your Linux VM with the following command, replacing the VM username and the server address with your own values:</span></span>

```bash
ssh-copy-id -i ~/.ssh/id_rsa.pub ahmet@myserver
```

## <a name="create-and-configure-an-ssh-config-file"></a><span data-ttu-id="39c8b-169">Создание и настройка файла конфигурации SSH</span><span class="sxs-lookup"><span data-stu-id="39c8b-169">Create and configure an SSH config file</span></span>

<span data-ttu-id="39c8b-170">Чтобы ускорить процесс входа и оптимизировать поведение клиента SSH, мы рекомендуем создать и настроить файл `~/.ssh/config`.</span><span class="sxs-lookup"><span data-stu-id="39c8b-170">It is a best practice to create and configure an `~/.ssh/config` file to speed up log ins and for optimizing your SSH client behavior.</span></span>

<span data-ttu-id="39c8b-171">Ниже приведены шаги для выполнения стандартной конфигурации.</span><span class="sxs-lookup"><span data-stu-id="39c8b-171">The following example shows a standard configuration.</span></span>

### <a name="create-the-file"></a><span data-ttu-id="39c8b-172">Создание файла</span><span class="sxs-lookup"><span data-stu-id="39c8b-172">Create the file</span></span>

```bash
touch ~/.ssh/config
```

### <a name="edit-the-file-to-add-the-new-ssh-configuration"></a><span data-ttu-id="39c8b-173">Изменение файла путем добавления новой конфигурации SSH</span><span class="sxs-lookup"><span data-stu-id="39c8b-173">Edit the file to add the new SSH configuration:</span></span>

```bash
vim ~/.ssh/config
```

### <a name="example-sshconfig-file"></a><span data-ttu-id="39c8b-174">Пример файла `~/.ssh/config`:</span><span class="sxs-lookup"><span data-stu-id="39c8b-174">Example `~/.ssh/config` file:</span></span>

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

<span data-ttu-id="39c8b-175">Эта конфигурация SSH предусматривает отдельные разделы для серверов, чтобы каждый из них мог использовать выделенную ему пару ключей.</span><span class="sxs-lookup"><span data-stu-id="39c8b-175">This SSH config gives you sections for each server to enable each to have its own dedicated key pair.</span></span> <span data-ttu-id="39c8b-176">Параметры по умолчанию (`Host *`) используются для всех узлов, которые отличаются от конкретных узлов, указанных выше в файле конфигурации.</span><span class="sxs-lookup"><span data-stu-id="39c8b-176">The default settings (`Host *`) are for any hosts that do not match any of the specific hosts higher up in the config file.</span></span>

### <a name="config-file-explained"></a><span data-ttu-id="39c8b-177">Описание файла конфигурации</span><span class="sxs-lookup"><span data-stu-id="39c8b-177">Config file explained</span></span>

<span data-ttu-id="39c8b-178">`Host` — имя узла, вызываемого в терминале.</span><span class="sxs-lookup"><span data-stu-id="39c8b-178">`Host` = the name of the host being called on the terminal.</span></span>  <span data-ttu-id="39c8b-179">Команда `ssh fedora22` сообщает `SSH`, что нужно использовать значения из блока параметров с меткой `Host fedora22`. Примечание. В качестве узла можно использовать любую удобную для вас метку, не обязательно связанную с именем узла любого из серверов.</span><span class="sxs-lookup"><span data-stu-id="39c8b-179">`ssh fedora22` tells `SSH` to use the values in the settings block labeled `Host fedora22`  NOTE: Host can be any label that is logical for your usage and does not represent the actual hostname of any server.</span></span>

<span data-ttu-id="39c8b-180">`Hostname 102.160.203.241` — IP-адрес или DNS-имя сервера, к которому осуществляется доступ.</span><span class="sxs-lookup"><span data-stu-id="39c8b-180">`Hostname 102.160.203.241` = the IP address or DNS name for the server being accessed.</span></span>

<span data-ttu-id="39c8b-181">`User ahmet` — удаленная учетная запись пользователя, которую нужно использовать для входа на сервер.</span><span class="sxs-lookup"><span data-stu-id="39c8b-181">`User ahmet` = the remote user account to use when logging in to the server.</span></span>

<span data-ttu-id="39c8b-182">`PubKeyAuthentication yes` — таким образом SSH сообщается, что для входа используется ключ SSH.</span><span class="sxs-lookup"><span data-stu-id="39c8b-182">`PubKeyAuthentication yes` = tells SSH you want to use an SSH key to log in.</span></span>

<span data-ttu-id="39c8b-183">`IdentityFile /home/ahmet/.ssh/id_id_rsa` — закрытый ключ SSH и соответствующий открытый ключ для проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="39c8b-183">`IdentityFile /home/ahmet/.ssh/id_id_rsa` = the SSH private key and corresponding public key to use for authentication.</span></span>

## <a name="ssh-into-linux-without-a-password"></a><span data-ttu-id="39c8b-184">Вход в Linux с использованием SSH без пароля</span><span class="sxs-lookup"><span data-stu-id="39c8b-184">SSH into Linux without a password</span></span>

<span data-ttu-id="39c8b-185">Теперь, когда у вас есть пара ключей SSH и настроенный файл конфигурации SSH, вы можете быстро и безопасно входить на виртуальную машину Linux.</span><span class="sxs-lookup"><span data-stu-id="39c8b-185">Now that you have an SSH key pair and a configured SSH config file, you are able to log in to your Linux VM quickly and securely.</span></span> <span data-ttu-id="39c8b-186">При первом входе на сервер с использованием ключа SSH команда запрашивает парольную фразу для этого файла ключа.</span><span class="sxs-lookup"><span data-stu-id="39c8b-186">The first time you log in to a server using an SSH key the command prompts you for the passphrase for that key file.</span></span>

```bash
ssh fedora22
```

### <a name="command-explained"></a><span data-ttu-id="39c8b-187">Описание команды</span><span class="sxs-lookup"><span data-stu-id="39c8b-187">Command explained</span></span>

<span data-ttu-id="39c8b-188">При выполнении команды `ssh fedora22` SSH сначала находит и загружает все параметры из блока `Host fedora22`, а затем загружает все остальные параметры из последнего блока (`Host *`).</span><span class="sxs-lookup"><span data-stu-id="39c8b-188">When `ssh fedora22` is executed SSH first locates and loads any settings from the `Host fedora22` block, and then loads all the remaining settings from the last block, `Host *`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="39c8b-189">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="39c8b-189">Next Steps</span></span>

<span data-ttu-id="39c8b-190">Следующий шаг — создание виртуальных машин Linux Azure с помощью нового открытого ключа SSH.</span><span class="sxs-lookup"><span data-stu-id="39c8b-190">Next up is to create Azure Linux VMs using the new SSH public key.</span></span>  <span data-ttu-id="39c8b-191">Виртуальные машины Azure, созданные с использованием открытого ключа SSH в качестве данных для входа, защищены лучше, чем виртуальные машины, созданные с помощью метода по умолчанию, предусматривающего использование паролей.</span><span class="sxs-lookup"><span data-stu-id="39c8b-191">Azure VMs that are created with an SSH public key as the login are better secured than VMs created with the default login method, passwords.</span></span>  <span data-ttu-id="39c8b-192">В настройках виртуальных машин Azure, созданных с помощью ключей SSH, пароли отключены по умолчанию для защиты от атак методом подбора.</span><span class="sxs-lookup"><span data-stu-id="39c8b-192">Azure VMs created using SSH keys are by default configured with passwords disabled, avoiding brute-forced guessing attempts.</span></span> <span data-ttu-id="39c8b-193">Дополнительные сведения о создании пары ключей SSH или дополнительных сертификатов, используемых на классическом портале, см. в [этом руководстве](create-ssh-keys-detailed.md).</span><span class="sxs-lookup"><span data-stu-id="39c8b-193">If you need more assistance in creating your SSH key pair or require additional certificates, such as for use with the classic portal, see [Detailed steps to create SSH key pairs and certificates](create-ssh-keys-detailed.md).</span></span>

* [<span data-ttu-id="39c8b-194">Создание защищенной виртуальной машины Linux с помощью шаблона Azure</span><span class="sxs-lookup"><span data-stu-id="39c8b-194">Create a secure Linux VM using an Azure template</span></span>](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="39c8b-195">Создание виртуальной машины Linux в Azure с помощью портала</span><span class="sxs-lookup"><span data-stu-id="39c8b-195">Create a secure Linux VM using the Azure portal</span></span>](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="39c8b-196">Создание защищенной виртуальной машины Linux с помощью интерфейса командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="39c8b-196">Create a secure Linux VM using the Azure CLI</span></span>](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
