---
title: "Руководство по созданию пары ключей SSH для виртуальных машин Linux в Azure | Документация Майкрософт"
description: "Указания по созданию пары из открытого и закрытого ключей SSH для виртуальных машин Linux в Azure, а также сведения о разных вариантах использования определенных сертификатов."
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
ms.openlocfilehash: d4548c6f21d04effd57ea36e4fc0d15f77568903
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="detailed-walk-through-to-create-an-ssh-key-pair-and-additional-certificates-for-a-linux-vm-in-azure"></a><span data-ttu-id="5d58b-103">Подробное руководство по созданию пары ключей SSH и дополнительных сертификатов для виртуальной машины Linux в Azure</span><span class="sxs-lookup"><span data-stu-id="5d58b-103">Detailed walk through to create an SSH key pair and additional certificates for a Linux VM in Azure</span></span>
<span data-ttu-id="5d58b-104">С помощью пары ключей SSH в Azure можно создавать виртуальные машины, по умолчанию использующие ключи SSH для проверки подлинности, что позволяет обойтись без паролей для входа.</span><span class="sxs-lookup"><span data-stu-id="5d58b-104">With an SSH key pair, you can create Virtual Machines on Azure that default to using SSH keys for authentication, eliminating the need for passwords to log in.</span></span> <span data-ttu-id="5d58b-105">Так как существует вероятность подбора пароля, ваши виртуальные машины могут подвергаться непрерывным попыткам взлома.</span><span class="sxs-lookup"><span data-stu-id="5d58b-105">Passwords can be guessed, and open your VMs up to relentless brute force attempts to guess your password.</span></span> <span data-ttu-id="5d58b-106">Виртуальные машины, созданные с помощью интерфейса командной строки Azure или шаблонов Resource Manager, могут содержать открытый ключ SSH, что устраняет необходимость в настройке после их развертывания, а именно в отключении входа с использованием пароля для SSH.</span><span class="sxs-lookup"><span data-stu-id="5d58b-106">VMs created with the Azure CLI or Resource Manager templates can include your SSH public key as part of the deployment, removing a post deployment configuration step of disabling password logins for SSH.</span></span> <span data-ttu-id="5d58b-107">В этой статье приведены подробные указания и дополнительные примеры создания сертификатов, используемых, например, на виртуальных машинах Linux.</span><span class="sxs-lookup"><span data-stu-id="5d58b-107">This article provides detailed steps and additional examples of generating certificates, such as for use with Linux virtual machines.</span></span> <span data-ttu-id="5d58b-108">Если вы хотите быстро создать и использовать пару ключей SSH, см. сведения в [этой статье](mac-create-ssh-keys.md).</span><span class="sxs-lookup"><span data-stu-id="5d58b-108">If you want to quickly create and use an SSH key pair, see [How to create an SSH public and private key pair for Linux VMs in Azure](mac-create-ssh-keys.md).</span></span>

## <a name="understanding-ssh-keys"></a><span data-ttu-id="5d58b-109">Общие сведения о ключах SSH</span><span class="sxs-lookup"><span data-stu-id="5d58b-109">Understanding SSH keys</span></span>

<span data-ttu-id="5d58b-110">Использование открытого и закрытого ключей SSH — это самый простой способ войти на серверы Linux.</span><span class="sxs-lookup"><span data-stu-id="5d58b-110">Using SSH public and private keys is the easiest way to log in to your Linux servers.</span></span> <span data-ttu-id="5d58b-111">[Шифрование с открытым ключом](https://en.wikipedia.org/wiki/Public-key_cryptography) обеспечивает большую безопасность при входе на виртуальные машины Linux или BSD в Azure, чем использование паролей, которые довольно легко получить методом подбора.</span><span class="sxs-lookup"><span data-stu-id="5d58b-111">[Public-key cryptography](https://en.wikipedia.org/wiki/Public-key_cryptography) provides a much more secure way to log in to your Linux or BSD VM in Azure than passwords, which can be brute-forced far more easily.</span></span>

<span data-ttu-id="5d58b-112">Открытый ключ можно предоставить любому пользователю, тогда как закрытый ключ принадлежит только вам (или локальной инфраструктуре безопасности).</span><span class="sxs-lookup"><span data-stu-id="5d58b-112">Your public key can be shared with anyone; but only you (or your local security infrastructure) possess your private key.</span></span>  <span data-ttu-id="5d58b-113">Закрытый ключ SSH должен быть защищен [очень надежным паролем](https://www.xkcd.com/936/) (источник: [xkcd.com](https://xkcd.com)).</span><span class="sxs-lookup"><span data-stu-id="5d58b-113">The SSH private key should have a [very secure password](https://www.xkcd.com/936/) (source:[xkcd.com](https://xkcd.com)) to safeguard it.</span></span>  <span data-ttu-id="5d58b-114">Это пароль для доступа к файлу закрытого ключа SSH, а **не** пароль к учетной записи пользователя.</span><span class="sxs-lookup"><span data-stu-id="5d58b-114">This password is just to access the private SSH key file and **is not** the user account password.</span></span>  <span data-ttu-id="5d58b-115">Когда вы добавите к ключу SSH пароль, закрытый ключ будет зашифрован с помощью 128-разрядного ключа AES. После этого закрытый ключ нельзя будет использовать без пароля для разблокировки.</span><span class="sxs-lookup"><span data-stu-id="5d58b-115">When you add a password to your SSH key, it encrypts the private key using 128-bit AES, so that the private key is useless without the password to decrypt it.</span></span>  <span data-ttu-id="5d58b-116">Если злоумышленник украдет ваш закрытый ключ, не защищенный паролем, он сможет воспользоваться этим ключом для входа на серверы, на которых установлен соответствующий открытый ключ.</span><span class="sxs-lookup"><span data-stu-id="5d58b-116">If an attacker stole your private key and that key did not have a password, they would be able to use that private key to log in to any servers that have the corresponding public key.</span></span>  <span data-ttu-id="5d58b-117">Если закрытый ключ защищен паролем, злоумышленник не сможет использовать его. Такой подход обеспечивает дополнительный уровень безопасности инфраструктуры в Azure.</span><span class="sxs-lookup"><span data-stu-id="5d58b-117">If a private key is password protected it cannot be used by that attacker, providing an additional layer of security for your infrastructure on Azure.</span></span>

<span data-ttu-id="5d58b-118">В этой статье рассматривается создание пары файлов открытого и закрытого ключей в формате SSH-RSA. Мы рекомендуем использовать именно их при развертывании с помощью Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="5d58b-118">This article creates an SSH protocol version 2 RSA public and private key file pair (also referred to as "ssh-rsa" keys), which are recommended for deployments with Azure Resource Manager.</span></span> <span data-ttu-id="5d58b-119">Ключи *ssh-rsa* являются обязательными при развертываниях на [портале](https://portal.azure.com) (как в классической модели, так и в модели развертывания с помощью Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="5d58b-119">*ssh-rsa* keys are required on the [portal](https://portal.azure.com) for both classic and Resource Manager deployments.</span></span>

## <a name="ssh-keys-use-and-benefits"></a><span data-ttu-id="5d58b-120">Использование ключей SSH и их преимущества</span><span class="sxs-lookup"><span data-stu-id="5d58b-120">SSH keys use and benefits</span></span>

<span data-ttu-id="5d58b-121">В Azure необходимо использовать по крайней мере 2048-разрядные открытые и закрытые ключи в формате SSH-RSA. Файл открытого ключа имеет формат контейнера `.pub`.</span><span class="sxs-lookup"><span data-stu-id="5d58b-121">Azure requires at least 2048-bit, SSH protocol version 2 RSA format public and private keys; the public key file has the `.pub` container format.</span></span> <span data-ttu-id="5d58b-122">Чтобы создать ключи, выполните команду `ssh-keygen`, которая задаст несколько вопросов, а затем запишет закрытый ключ и соответствующий открытый ключ.</span><span class="sxs-lookup"><span data-stu-id="5d58b-122">To create the keys use `ssh-keygen`, which asks a series of questions and then writes a private key and a matching public key.</span></span> <span data-ttu-id="5d58b-123">При создании виртуальной машины Azure копирует открытый ключ в папку `~/.ssh/authorized_keys` на виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="5d58b-123">When an Azure VM is created, Azure copies the public key to the `~/.ssh/authorized_keys` folder on the VM.</span></span> <span data-ttu-id="5d58b-124">Ключи SSH в `~/.ssh/authorized_keys` используются для запросов к клиенту, который должен подобрать соответствующий закрытый ключ при SSH-подключении для входа.</span><span class="sxs-lookup"><span data-stu-id="5d58b-124">SSH keys in `~/.ssh/authorized_keys` are used to challenge the client to match the corresponding private key on an SSH login connection.</span></span>  <span data-ttu-id="5d58b-125">При создании виртуальной машины Linux в Azure с использованием ключей SSH для проверки подлинности Azure настраивает сервер SSHD таким образом, чтобы для входа можно было использовать только ключи SSH.</span><span class="sxs-lookup"><span data-stu-id="5d58b-125">When an Azure Linux VM is created using SSH keys for authentication, Azure configures the SSHD server to not allow password logins, only SSH keys.</span></span>  <span data-ttu-id="5d58b-126">Таким образом, создавая виртуальные машины Azure Linux с использованием ключей SSH, вы защищаете это развертывание и выполняете стандартный шаг настройки после развертывания — отключаете пароли в файле **sshd_config**.</span><span class="sxs-lookup"><span data-stu-id="5d58b-126">Therefore, by creating Azure Linux VMs with SSH keys, you can help secure the VM deployment and save yourself the typical post-deployment configuration step of disabling passwords in the **sshd_config** file.</span></span>

## <a name="using-ssh-keygen"></a><span data-ttu-id="5d58b-127">Использование команды ssh-keygen</span><span class="sxs-lookup"><span data-stu-id="5d58b-127">Using ssh-keygen</span></span>

<span data-ttu-id="5d58b-128">Эта команда создает пару защищенных паролем (зашифрованных) ключей SSH, используя 2048-разрядный RSA. К этой паре можно добавить комментарий, чтобы ее потом можно было легко определить.</span><span class="sxs-lookup"><span data-stu-id="5d58b-128">This command creates a password secured (encrypted) SSH key pair using 2048-bit RSA and it is commented to easily identify it.</span></span>  

<span data-ttu-id="5d58b-129">Ключи SSH по умолчанию хранятся в каталоге `~/.ssh`.</span><span class="sxs-lookup"><span data-stu-id="5d58b-129">SSH keys are by default kept in the `~/.ssh` directory.</span></span>  <span data-ttu-id="5d58b-130">Если у вас нет каталога `~/.ssh`, создайте его с правильными разрешениями с помощью команды `ssh-keygen`.</span><span class="sxs-lookup"><span data-stu-id="5d58b-130">If you do not have a `~/.ssh` directory, the `ssh-keygen` command creates it for you with the correct permissions.</span></span>

```bash
ssh-keygen \
    -t rsa \
    -b 2048 \
    -C "azureuser@myserver" \
    -f ~/.ssh/id_rsa \
    -N mypassword
```

<span data-ttu-id="5d58b-131">*Описание команды*</span><span class="sxs-lookup"><span data-stu-id="5d58b-131">*Command explained*</span></span>

<span data-ttu-id="5d58b-132">`ssh-keygen` — программа, с помощью которой создаются ключи.</span><span class="sxs-lookup"><span data-stu-id="5d58b-132">`ssh-keygen` = the program used to create the keys</span></span>

<span data-ttu-id="5d58b-133">`-t rsa` — тип создаваемого ключа, который является форматом RSA [статья в Википедии] [со скобками в конце](`https://en.wikipedia.org/wiki/RSA_(cryptosystem) `); 
`-b 2048` — биты ключа.</span><span class="sxs-lookup"><span data-stu-id="5d58b-133">`-t rsa` = type of key to create which is the RSA format [wikipedia][parens at end](`https://en.wikipedia.org/wiki/RSA_(cryptosystem) `)
`-b 2048` = bits of the key</span></span>

<span data-ttu-id="5d58b-134">`-C "azureuser@myserver"` — комментарий, который будет добавлен в конец файла открытого ключа для идентификации.</span><span class="sxs-lookup"><span data-stu-id="5d58b-134">`-C "azureuser@myserver"` = a comment appended to the end of the public key file to easily identify it.</span></span>  <span data-ttu-id="5d58b-135">Обычно в качестве комментария используется адрес электронной почты, но вы можете выбрать для своей инфраструктуры любой удобный метод идентификации.</span><span class="sxs-lookup"><span data-stu-id="5d58b-135">Normally an email is used as the comment but you can use whatever works best for your infrastructure.</span></span>

## <a name="classic-deploy-using-asm"></a><span data-ttu-id="5d58b-136">Классическое развертывание с помощью `asm`</span><span class="sxs-lookup"><span data-stu-id="5d58b-136">Classic deploy using `asm`</span></span>

<span data-ttu-id="5d58b-137">При использовании классической модели развертывания (режим `asm` в интерфейсе командной строки) вы можете использовать открытый ключ SSH-RSA или ключ в формате RFC4716 в контейнере PEM.</span><span class="sxs-lookup"><span data-stu-id="5d58b-137">If you are using the classic deployment model (`asm` mode in the CLI), you can use an SSH-RSA public key or an RFC4716 formatted key in a pem container.</span></span>  <span data-ttu-id="5d58b-138">Открытый ключ SSH-RSA вы создали ранее в рамках этого руководства с помощью `ssh-keygen`.</span><span class="sxs-lookup"><span data-stu-id="5d58b-138">The SSH-RSA public key is what was created earlier in this article using `ssh-keygen`.</span></span>

<span data-ttu-id="5d58b-139">Чтобы создать ключ в формате RFC4716 из существующего открытого ключа SSH, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="5d58b-139">To create a RFC4716 formatted key from an existing SSH public key:</span></span>

```bash
ssh-keygen \
-f ~/.ssh/id_rsa.pub \
-e \
-m RFC4716 > ~/.ssh/id_ssh2.pem
```

## <a name="example-of-ssh-keygen"></a><span data-ttu-id="5d58b-140">Пример с ssh-keygen</span><span class="sxs-lookup"><span data-stu-id="5d58b-140">Example of ssh-keygen</span></span>

```bash
ssh-keygen -t rsa -b 2048 -C "azureuser@myserver"
Generating public/private rsa key pair.
Enter file in which to save the key (/home/azureuser/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/azureuser/.ssh/id_rsa.
Your public key has been saved in /home/azureuser/.ssh/id_rsa.pub.
The key fingerprint is:
14:a3:cb:3e:78:ad:25:cc:55:e9:0c:08:e5:d1:a9:08 azureuser@myserver
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

<span data-ttu-id="5d58b-141">Сохраненные файлы ключей:</span><span class="sxs-lookup"><span data-stu-id="5d58b-141">Saved key files:</span></span>

`Enter file in which to save the key (/home/azureuser/.ssh/id_rsa): ~/.ssh/id_rsa`

<span data-ttu-id="5d58b-142">Имя пары ключей, используемое в этой статье.</span><span class="sxs-lookup"><span data-stu-id="5d58b-142">The key pair name for this article.</span></span>  <span data-ttu-id="5d58b-143">По умолчанию пара ключей называется **id_rsa**. Так как некоторые средства ожидаемо ищут закрытый ключ в файле с именем **id_rsa**, есть смысл создать такой файл.</span><span class="sxs-lookup"><span data-stu-id="5d58b-143">Having a key pair named **id_rsa** is the default and some tools might expect the **id_rsa** private key file name so having one is a good idea.</span></span> <span data-ttu-id="5d58b-144">Пары ключей SSH и файл конфигурации SSH по умолчанию располагаются в каталоге `~/.ssh/`.</span><span class="sxs-lookup"><span data-stu-id="5d58b-144">The directory `~/.ssh/` is the default location for SSH key pairs and the SSH config file.</span></span>  <span data-ttu-id="5d58b-145">Если не указать полный путь, `ssh-keygen` создаст ключи в текущем рабочем каталоге, а не в стандартном каталоге `~/.ssh`.</span><span class="sxs-lookup"><span data-stu-id="5d58b-145">If not specified with a full path, `ssh-keygen` creates the keys in the current working directory, not the default `~/.ssh`.</span></span>

<span data-ttu-id="5d58b-146">Описание каталога `~/.ssh`.</span><span class="sxs-lookup"><span data-stu-id="5d58b-146">A listing of the `~/.ssh` directory.</span></span>

```bash
ls -al ~/.ssh
-rw------- 1 azureuser staff  1675 Aug 25 18:04 id_rsa
-rw-r--r-- 1 azureuser staff   410 Aug 25 18:04 id_rsa.pub
```

<span data-ttu-id="5d58b-147">Пароль ключа:</span><span class="sxs-lookup"><span data-stu-id="5d58b-147">Key Password:</span></span>

`Enter passphrase (empty for no passphrase):`

<span data-ttu-id="5d58b-148">В качестве парольной фразы `ssh-keygen` использует пароль к файлу закрытого ключа.</span><span class="sxs-lookup"><span data-stu-id="5d58b-148">`ssh-keygen` refers to a password for the private key file as "a passphrase."</span></span>  <span data-ttu-id="5d58b-149">Мы *настоятельно* рекомендуем добавить пароль к своему закрытому ключу.</span><span class="sxs-lookup"><span data-stu-id="5d58b-149">It is *strongly* recommended to add a password to your private key.</span></span> <span data-ttu-id="5d58b-150">Если не защитить файл ключа паролем, любой пользователь, у которого есть этот файл, сможет использовать его, чтобы войти на любой из серверов, для которого предусмотрен соответствующий открытый ключ.</span><span class="sxs-lookup"><span data-stu-id="5d58b-150">Without a password protecting the key file, anyone with the file can use it to log in to any server that has the corresponding public key.</span></span> <span data-ttu-id="5d58b-151">Следовательно, добавив пароль (парольную фразу), вы усилите защиту на случай, если другой пользователь получит доступ к файлу закрытого ключа. Это даст вам время, чтобы изменить ключи для проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="5d58b-151">Adding a password (passphrase) offers more protection in case someone is able to gain access to your private key file, given you time to change the keys used to authenticate you.</span></span>

## <a name="using-ssh-agent-to-store-your-private-key-password"></a><span data-ttu-id="5d58b-152">Использование ssh-agent для хранения пароля закрытого ключа</span><span class="sxs-lookup"><span data-stu-id="5d58b-152">Using ssh-agent to store your private key password</span></span>

<span data-ttu-id="5d58b-153">Чтобы не вводить пароль файла закрытого ключа при каждом входе с использованием SSH, вы можете создать кэш пароля от файла закрытого ключа с помощью команды `ssh-agent` .</span><span class="sxs-lookup"><span data-stu-id="5d58b-153">To avoid typing your private key file password with every SSH login, you can use `ssh-agent` to cache your private key file password.</span></span> <span data-ttu-id="5d58b-154">Если вы используете компьютер Mac, при вызове `ssh-agent`пароли закрытых ключей будут надежно сохранены в цепочке ключей OS X.</span><span class="sxs-lookup"><span data-stu-id="5d58b-154">If you are using a Mac, the OSX Keychain securely stores the private key passwords when you invoke `ssh-agent`.</span></span>

<span data-ttu-id="5d58b-155">С помощью ssh-agent и ssh-add определите для системы SSH файлы ключей, чтобы вам не нужно было использовать парольную фразу в интерактивном режиме.</span><span class="sxs-lookup"><span data-stu-id="5d58b-155">Verify and use ssh-agent and ssh-add to inform the SSH system about the key files so that the passphrase will not need to be used interactively.</span></span>

```bash
eval "$(ssh-agent -s)"
```

<span data-ttu-id="5d58b-156">Затем добавьте закрытый ключ к `ssh-agent` с помощью команды `ssh-add`.</span><span class="sxs-lookup"><span data-stu-id="5d58b-156">Now add the private key to `ssh-agent` using the command `ssh-add`.</span></span>

```bash
ssh-add ~/.ssh/id_rsa
```

<span data-ttu-id="5d58b-157">Теперь пароль закрытого ключа хранится в `ssh-agent`.</span><span class="sxs-lookup"><span data-stu-id="5d58b-157">The private key password is now stored in `ssh-agent`.</span></span>

## <a name="using-ssh-copy-id-to-copy-the-key-to-an-existing-vm"></a><span data-ttu-id="5d58b-158">Копирование ключа на имеющуюся виртуальную машину с помощью `ssh-copy-id`</span><span class="sxs-lookup"><span data-stu-id="5d58b-158">Using `ssh-copy-id` to copy the key to an existing VM</span></span>
<span data-ttu-id="5d58b-159">Если виртуальная машина Linux уже создана, вы можете установить для нее новый открытый ключ SSH с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="5d58b-159">If you have already created a VM you can install the new SSH public key to your Linux VM with:</span></span>

```bash
ssh-copy-id -i ~/.ssh/id_rsa.pub ahmet@myserver
```

## <a name="create-and-configure-an-ssh-config-file"></a><span data-ttu-id="5d58b-160">Создание и настройка файла конфигурации SSH</span><span class="sxs-lookup"><span data-stu-id="5d58b-160">Create and configure an SSH config file</span></span>

<span data-ttu-id="5d58b-161">Чтобы ускорить процесс входа и оптимизировать поведение клиента SSH, рекомендуется создать и настроить файл `~/.ssh/config`.</span><span class="sxs-lookup"><span data-stu-id="5d58b-161">It is a recommended best practice to create and configure an `~/.ssh/config` file to speed up log ins and for optimizing your SSH client behavior.</span></span>

<span data-ttu-id="5d58b-162">Ниже приведены шаги для выполнения стандартной конфигурации.</span><span class="sxs-lookup"><span data-stu-id="5d58b-162">The following example shows a standard configuration.</span></span>

### <a name="create-the-file"></a><span data-ttu-id="5d58b-163">Создание файла</span><span class="sxs-lookup"><span data-stu-id="5d58b-163">Create the file</span></span>

```bash
touch ~/.ssh/config
```

### <a name="edit-the-file-to-add-the-new-ssh-configuration"></a><span data-ttu-id="5d58b-164">Изменение файла путем добавления новой конфигурации SSH</span><span class="sxs-lookup"><span data-stu-id="5d58b-164">Edit the file to add the new SSH configuration:</span></span>

```bash
vim ~/.ssh/config
```

### <a name="example-sshconfig-file"></a><span data-ttu-id="5d58b-165">Пример файла `~/.ssh/config`:</span><span class="sxs-lookup"><span data-stu-id="5d58b-165">Example `~/.ssh/config` file:</span></span>

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

<span data-ttu-id="5d58b-166">Эта конфигурация SSH предусматривает отдельные разделы для серверов, чтобы каждый из них мог использовать выделенную ему пару ключей.</span><span class="sxs-lookup"><span data-stu-id="5d58b-166">This SSH config gives you sections for each server to enable each to have its own dedicated key pair.</span></span> <span data-ttu-id="5d58b-167">Параметры по умолчанию (`Host *`) используются для всех узлов, которые отличаются от конкретных узлов, указанных выше в файле конфигурации.</span><span class="sxs-lookup"><span data-stu-id="5d58b-167">The default settings (`Host *`) are for any hosts that do not match any of the specific hosts higher up in the config file.</span></span>

### <a name="config-file-explained"></a><span data-ttu-id="5d58b-168">Описание файла конфигурации</span><span class="sxs-lookup"><span data-stu-id="5d58b-168">Config file explained</span></span>

<span data-ttu-id="5d58b-169">`Host` — имя узла, вызываемого в терминале.</span><span class="sxs-lookup"><span data-stu-id="5d58b-169">`Host` = the name of the host being called on the terminal.</span></span>  <span data-ttu-id="5d58b-170">Команда `ssh fedora22` сообщает `SSH`, что нужно использовать значения из блока параметров с меткой `Host fedora22`. Примечание. В качестве узла можно использовать любую удобную для вас метку, не обязательно связанную с именем узла любого из серверов.</span><span class="sxs-lookup"><span data-stu-id="5d58b-170">`ssh fedora22` tells `SSH` to use the values in the settings block labeled `Host fedora22`  NOTE: Host can be any label that is logical for your usage and does not represent the actual hostname of any server.</span></span>

<span data-ttu-id="5d58b-171">`Hostname 102.160.203.241` — IP-адрес или DNS-имя сервера, к которому осуществляется доступ.</span><span class="sxs-lookup"><span data-stu-id="5d58b-171">`Hostname 102.160.203.241` = the IP address or DNS name for the server being accessed.</span></span>

<span data-ttu-id="5d58b-172">`User ahmet` — удаленная учетная запись пользователя, которую нужно использовать для входа на сервер.</span><span class="sxs-lookup"><span data-stu-id="5d58b-172">`User ahmet` = the remote user account to use when logging in to the server.</span></span>

<span data-ttu-id="5d58b-173">`PubKeyAuthentication yes` — таким образом SSH сообщается, что для входа используется ключ SSH.</span><span class="sxs-lookup"><span data-stu-id="5d58b-173">`PubKeyAuthentication yes` = tells SSH you want to use an SSH key to log in.</span></span>

<span data-ttu-id="5d58b-174">`IdentityFile /home/ahmet/.ssh/id_id_rsa` — закрытый ключ SSH и соответствующий открытый ключ для проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="5d58b-174">`IdentityFile /home/ahmet/.ssh/id_id_rsa` = the SSH private key and corresponding public key to use for authentication.</span></span>

## <a name="ssh-into-linux-without-a-password"></a><span data-ttu-id="5d58b-175">Вход в Linux с использованием SSH без пароля</span><span class="sxs-lookup"><span data-stu-id="5d58b-175">SSH into Linux without a password</span></span>

<span data-ttu-id="5d58b-176">Теперь, когда у вас есть пара ключей SSH и настроенный файл конфигурации SSH, вы можете быстро и безопасно входить на виртуальную машину Linux.</span><span class="sxs-lookup"><span data-stu-id="5d58b-176">Now that you have an SSH key pair and a configured SSH config file, you are able to log in to your Linux VM quickly and securely.</span></span> <span data-ttu-id="5d58b-177">При первом входе на сервер с использованием ключа SSH команда запрашивает парольную фразу для этого файла ключа.</span><span class="sxs-lookup"><span data-stu-id="5d58b-177">The first time you log in to a server using an SSH key the command prompts you for the passphrase for that key file.</span></span>

```bash
ssh fedora22
```

### <a name="command-explained"></a><span data-ttu-id="5d58b-178">Описание команды</span><span class="sxs-lookup"><span data-stu-id="5d58b-178">Command explained</span></span>

<span data-ttu-id="5d58b-179">При выполнении команды `ssh fedora22` SSH сначала находит и загружает все параметры из блока `Host fedora22`, а затем загружает все остальные параметры из последнего блока (`Host *`).</span><span class="sxs-lookup"><span data-stu-id="5d58b-179">When `ssh fedora22` is executed SSH first locates and loads any settings from the `Host fedora22` block, and then loads all the remaining settings from the last block, `Host *`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5d58b-180">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5d58b-180">Next Steps</span></span>

<span data-ttu-id="5d58b-181">Следующий шаг — создание виртуальных машин Linux Azure с помощью нового открытого ключа SSH.</span><span class="sxs-lookup"><span data-stu-id="5d58b-181">Next up is to create Azure Linux VMs using the new SSH public key.</span></span>  <span data-ttu-id="5d58b-182">Виртуальные машины Azure, созданные с использованием открытого ключа SSH в качестве данных для входа, защищены лучше, чем виртуальные машины, созданные с помощью метода по умолчанию, предусматривающего использование паролей.</span><span class="sxs-lookup"><span data-stu-id="5d58b-182">Azure VMs that are created with an SSH public key as the login are better secured than VMs created with the default login method, passwords.</span></span>  <span data-ttu-id="5d58b-183">В настройках виртуальных машин Azure, созданных с помощью ключей SSH, пароли отключены по умолчанию для защиты от атак методом подбора.</span><span class="sxs-lookup"><span data-stu-id="5d58b-183">Azure VMs created using SSH keys are by default configured with passwords disabled, avoiding brute-forced guessing attempts.</span></span>

* [<span data-ttu-id="5d58b-184">Создание защищенной виртуальной машины Linux с помощью шаблона Azure</span><span class="sxs-lookup"><span data-stu-id="5d58b-184">Create a secure Linux VM using an Azure template</span></span>](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="5d58b-185">Создание виртуальной машины Linux в Azure с помощью портала</span><span class="sxs-lookup"><span data-stu-id="5d58b-185">Create a secure Linux VM using the Azure portal</span></span>](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="5d58b-186">Создание защищенной виртуальной машины Linux с помощью интерфейса командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="5d58b-186">Create a secure Linux VM using the Azure CLI</span></span>](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
