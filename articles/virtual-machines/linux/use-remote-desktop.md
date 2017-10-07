---
title: "tooa aaaUse удаленного рабочего стола виртуальной Машины Linux в Azure | Документы Microsoft"
description: "Узнайте, как tooinstall и настроить удаленный рабочий стол (xrdp) tooconnect tooa виртуальных Машин Linux в Azure с помощью графических средств"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: iainfou
ms.openlocfilehash: 64d30be101ceeb49fc05bb10293ad63db358efe3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-remote-desktop-tooconnect-tooa-linux-vm-in-azure"></a><span data-ttu-id="7fa7c-103">Установка и настройка удаленного рабочего стола tooconnect tooa виртуальных Машин Linux в Azure</span><span class="sxs-lookup"><span data-stu-id="7fa7c-103">Install and configure Remote Desktop tooconnect tooa Linux VM in Azure</span></span>
<span data-ttu-id="7fa7c-104">Linux виртуальных машин (ВМ) в Azure обычно осуществляется из командной строки hello, с использованием безопасного shell (SSH) подключения.</span><span class="sxs-lookup"><span data-stu-id="7fa7c-104">Linux virtual machines (VMs) in Azure are usually managed from hello command line using a secure shell (SSH) connection.</span></span> <span data-ttu-id="7fa7c-105">Когда новый tooLinux или быстрого устранения неполадок при использовании hello использование удаленного рабочего стола может оказаться удобнее.</span><span class="sxs-lookup"><span data-stu-id="7fa7c-105">When new tooLinux, or for quick troubleshooting scenarios, hello use of remote desktop may be easier.</span></span> <span data-ttu-id="7fa7c-106">Это статья сведения о том, как tooinstall и настройте рабочего стола ([xfce](https://www.xfce.org)) и удаленного рабочего стола ([xrdp](http://www.xrdp.org)) для ВМ Linux с помощью модели развертывания диспетчера ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="7fa7c-106">This article details how tooinstall and configure a desktop environment ([xfce](https://www.xfce.org)) and remote desktop ([xrdp](http://www.xrdp.org)) for your Linux VM using hello Resource Manager deployment model.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="7fa7c-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="7fa7c-107">Prerequisites</span></span>
<span data-ttu-id="7fa7c-108">Для работы с этой статьей требуется существующая виртуальная машина Linux в Azure.</span><span class="sxs-lookup"><span data-stu-id="7fa7c-108">This article requires an existing Linux VM in Azure.</span></span> <span data-ttu-id="7fa7c-109">Если вам требуется toocreate виртуальной Машины, используйте один из следующих методов hello:</span><span class="sxs-lookup"><span data-stu-id="7fa7c-109">If you need toocreate a VM, use one of hello following methods:</span></span>

- <span data-ttu-id="7fa7c-110">Hello [Azure CLI 2.0](quick-create-cli.md)</span><span class="sxs-lookup"><span data-stu-id="7fa7c-110">hello [Azure CLI 2.0](quick-create-cli.md)</span></span>
- <span data-ttu-id="7fa7c-111">Hello [портал Azure](quick-create-portal.md)</span><span class="sxs-lookup"><span data-stu-id="7fa7c-111">hello [Azure portal](quick-create-portal.md)</span></span>


## <a name="install-a-desktop-environment-on-your-linux-vm"></a><span data-ttu-id="7fa7c-112">Установка среды рабочего стола на виртуальной машине Linux</span><span class="sxs-lookup"><span data-stu-id="7fa7c-112">Install a desktop environment on your Linux VM</span></span>
<span data-ttu-id="7fa7c-113">На большинстве виртуальных машин Linux в Azure по умолчанию не установлена среда рабочего стола.</span><span class="sxs-lookup"><span data-stu-id="7fa7c-113">Most Linux VMs in Azure do not have a desktop environment installed by default.</span></span> <span data-ttu-id="7fa7c-114">Управление виртуальными машинами Linux обычно осуществляется через SSH-подключения, а не с помощью рабочего стола.</span><span class="sxs-lookup"><span data-stu-id="7fa7c-114">Linux VMs are commonly managed using SSH connections rather than a desktop environment.</span></span> <span data-ttu-id="7fa7c-115">В Linux можно использовать различные среды рабочего стола.</span><span class="sxs-lookup"><span data-stu-id="7fa7c-115">There are various desktop environments in Linux that you can choose.</span></span> <span data-ttu-id="7fa7c-116">В зависимости от используемого рабочей среды он может использовать один too2 ГБ места на диске, занять tooinstall минут 5 too10 и настройте все пакеты необходимых hello.</span><span class="sxs-lookup"><span data-stu-id="7fa7c-116">Depending on your choice of desktop environment, it may consume one too2 GB of disk space, and take 5 too10 minutes tooinstall and configure all hello required packages.</span></span>

<span data-ttu-id="7fa7c-117">Hello следующий пример устанавливает облегченного hello [xfce4](https://www.xfce.org/) рабочей среды на Виртуальной машине Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="7fa7c-117">hello following example installs hello lightweight [xfce4](https://www.xfce.org/) desktop environment on an Ubuntu VM.</span></span> <span data-ttu-id="7fa7c-118">Команды для других распределений, незначительно (используйте `yum` tooinstall в Red Hat Enterprise Linux и настроить соответствующие `selinux` правила или используйте `zypper` tooinstall на SUSE, например).</span><span class="sxs-lookup"><span data-stu-id="7fa7c-118">Commands for other distributions vary slightly (use `yum` tooinstall on Red Hat Enterprise Linux and configure appropriate `selinux` rules, or use `zypper` tooinstall on SUSE, for example).</span></span>

<span data-ttu-id="7fa7c-119">Во-первых, tooyour SSH виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="7fa7c-119">First, SSH tooyour VM.</span></span> <span data-ttu-id="7fa7c-120">Hello следующий пример соединяет toohello виртуальной Машины с именем *myvm.westus.cloudapp.azure.com* с именем пользователя hello объекта *azureuser*:</span><span class="sxs-lookup"><span data-stu-id="7fa7c-120">hello following example connects toohello VM named *myvm.westus.cloudapp.azure.com* with hello username of *azureuser*:</span></span>

```bash
ssh azureuser@myvm.westus.cloudapp.azure.com
```

<span data-ttu-id="7fa7c-121">Если вы используете Windows и требуются дополнительные сведения об использовании SSH, см. раздел [как toouse SSH ключей с Windows](ssh-from-windows.md).</span><span class="sxs-lookup"><span data-stu-id="7fa7c-121">If you are using Windows and need more information on using SSH, see [How toouse SSH keys with Windows](ssh-from-windows.md).</span></span>

<span data-ttu-id="7fa7c-122">Затем установите xfce с помощью `apt` следующим образом:</span><span class="sxs-lookup"><span data-stu-id="7fa7c-122">Next, install xfce using `apt` as follows:</span></span>

```bash
sudo apt-get update
sudo apt-get install xfce4
```

## <a name="install-and-configure-a-remote-desktop-server"></a><span data-ttu-id="7fa7c-123">Установка и настройка сервера удаленных рабочих столов</span><span class="sxs-lookup"><span data-stu-id="7fa7c-123">Install and configure a remote desktop server</span></span>
<span data-ttu-id="7fa7c-124">Теперь, когда вы получите доступ к среде установлен, настройте toolisten служб удаленных рабочих столов для входящих подключений.</span><span class="sxs-lookup"><span data-stu-id="7fa7c-124">Now that you have a desktop environment installed, configure a remote desktop service toolisten for incoming connections.</span></span> <span data-ttu-id="7fa7c-125">[xrdp](http://xrdp.org) — это сервер RDP с открытым исходным кодом, доступный в большинстве дистрибутивов Linux и совместимый с xfce.</span><span class="sxs-lookup"><span data-stu-id="7fa7c-125">[xrdp](http://xrdp.org) is an open source Remote Desktop Protocol (RDP) server that is available on most Linux distributions, and works well with xfce.</span></span> <span data-ttu-id="7fa7c-126">Установите xrdp на виртуальной машине Ubuntu следующим образом:</span><span class="sxs-lookup"><span data-stu-id="7fa7c-126">Install xrdp on your Ubuntu VM as follows:</span></span>

```bash
sudo apt-get install xrdp
```

<span data-ttu-id="7fa7c-127">Сообщите xrdp какие toouse рабочей среды при запуске сеанса.</span><span class="sxs-lookup"><span data-stu-id="7fa7c-127">Tell xrdp what desktop environment toouse when you start your session.</span></span> <span data-ttu-id="7fa7c-128">Настройка xrdp toouse xfce в качестве рабочего стола следующим образом:</span><span class="sxs-lookup"><span data-stu-id="7fa7c-128">Configure xrdp toouse xfce as your desktop environment as follows:</span></span>

```bash
echo xfce4-session >~/.xsession
```

<span data-ttu-id="7fa7c-129">Перезапустите службу xrdp hello для эффекта tootake изменения hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="7fa7c-129">Restart hello xrdp service for hello changes tootake effect as follows:</span></span>

```bash
sudo service xrdp restart
```


## <a name="set-a-local-user-account-password"></a><span data-ttu-id="7fa7c-130">Настройка пароля локальной учетной записи пользователя</span><span class="sxs-lookup"><span data-stu-id="7fa7c-130">Set a local user account password</span></span>
<span data-ttu-id="7fa7c-131">Если вы создали пароль для учетной записи пользователя при создании виртуальной машины, пропустите этот шаг.</span><span class="sxs-lookup"><span data-stu-id="7fa7c-131">If you created a password for your user account when you created your VM, skip this step.</span></span> <span data-ttu-id="7fa7c-132">При использовании проверки подлинности SSH с ключом только и не иметь пароль локальной учетной записи задано, укажите пароль, прежде чем использовать xrdp toolog в tooyour виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="7fa7c-132">If you only use SSH key authentication and do not have a local account password set, specify a password before you use xrdp toolog in tooyour VM.</span></span> <span data-ttu-id="7fa7c-133">xrdp не принимает ключи SSH для проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="7fa7c-133">xrdp cannot accept SSH keys for authentication.</span></span> <span data-ttu-id="7fa7c-134">Hello следующий пример указывает пароль для учетной записи пользователя hello *azureuser*:</span><span class="sxs-lookup"><span data-stu-id="7fa7c-134">hello following example specifies a password for hello user account *azureuser*:</span></span>

```bash
sudo passwd azureuser
```

> [!NOTE]
> <span data-ttu-id="7fa7c-135">Указание пароля не обновляет вашей SSHD конфигурации toopermit пароль входа, если он в настоящее время не поддерживает.</span><span class="sxs-lookup"><span data-stu-id="7fa7c-135">Specifying a password does not update your SSHD configuration toopermit password logins if it currently does not.</span></span> <span data-ttu-id="7fa7c-136">С точки зрения безопасности могут обратиться в tooconnect tooyour ВМ с туннель SSH с использованием проверки подлинности на основе ключей, а затем подключите tooxrdp.</span><span class="sxs-lookup"><span data-stu-id="7fa7c-136">From a security perspective, you may wish tooconnect tooyour VM with an SSH tunnel using key-based authentication and then connect tooxrdp.</span></span> <span data-ttu-id="7fa7c-137">Если Да, пропустите следующий шаг по созданию сетевой безопасности группы правил tooallow удаленного рабочего стола трафика hello.</span><span class="sxs-lookup"><span data-stu-id="7fa7c-137">If so, skip hello following step on creating a network security group rule tooallow remote desktop traffic.</span></span>


## <a name="create-a-network-security-group-rule-for-remote-desktop-traffic"></a><span data-ttu-id="7fa7c-138">Создание правила группы безопасности сети, разрешающего трафик с удаленного рабочего стола</span><span class="sxs-lookup"><span data-stu-id="7fa7c-138">Create a Network Security Group rule for Remote Desktop traffic</span></span>
<span data-ttu-id="7fa7c-139">tooreach трафика удаленного рабочего стола tooallow ВМ Linux, правило группы безопасности сети должен создать toobe разрешает TCP на порт 3389 tooreach ВМ.</span><span class="sxs-lookup"><span data-stu-id="7fa7c-139">tooallow Remote Desktop traffic tooreach your Linux VM, a network security group rule needs toobe created that allows TCP on port 3389 tooreach your VM.</span></span> <span data-ttu-id="7fa7c-140">Дополнительные сведения о правилах групп безопасности сети см. в статье [Группа безопасности сети](../../virtual-network/virtual-networks-nsg.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7fa7c-140">For more information about network security group rules, see [What is a Network Security Group?](../../virtual-network/virtual-networks-nsg.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span> <span data-ttu-id="7fa7c-141">Вы также можете [используйте hello Azure портала toocreate правило группы безопасности сети](../windows/nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7fa7c-141">You can also [use hello Azure portal toocreate a network security group rule](../windows/nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="7fa7c-142">Hello следующие примеры создают правило группы безопасности сети с [создать правило nsg сети az](/cli/azure/network/nsg/rule#create) с именем *myNetworkSecurityGroupRule* слишком*Разрешить* трафика на *tcp* порт *3389*.</span><span class="sxs-lookup"><span data-stu-id="7fa7c-142">hello following examples create a network security group rule with [az network nsg rule create](/cli/azure/network/nsg/rule#create) named *myNetworkSecurityGroupRule* too*allow* traffic on *tcp* port *3389*.</span></span>

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --protocol tcp \
    --priority 1010 \
    --destination-port-range 3389
```


## <a name="connect-your-linux-vm-with-a-remote-desktop-client"></a><span data-ttu-id="7fa7c-143">Подключение к виртуальной машине Linux с помощью клиента удаленного рабочего стола</span><span class="sxs-lookup"><span data-stu-id="7fa7c-143">Connect your Linux VM with a Remote Desktop client</span></span>
<span data-ttu-id="7fa7c-144">Откройте ваш локальный клиент удаленного рабочего стола и подключения toohello IP-адрес или DNS-имя виртуальной Машины Linux.</span><span class="sxs-lookup"><span data-stu-id="7fa7c-144">Open your local remote desktop client and connect toohello IP address or DNS name of your Linux VM.</span></span> <span data-ttu-id="7fa7c-145">Введите hello имя пользователя и пароль для учетной записи пользователя hello на ВМ следующим образом:</span><span class="sxs-lookup"><span data-stu-id="7fa7c-145">Enter hello username and password for hello user account on your VM as follows:</span></span>

![Подключение через клиент удаленного рабочего стола tooxrdp](./media/use-remote-desktop/remote-desktop-client.png)

<span data-ttu-id="7fa7c-147">После проверки подлинности рабочего стола xfce hello загрузки и выглядеть аналогично toohello в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="7fa7c-147">After authenticating, hello xfce desktop environment will load and look similar toohello following example:</span></span>

![Среда рабочего стола xfce при подключении через xrdp](./media/use-remote-desktop/xfce-desktop-environment.png)


## <a name="troubleshoot"></a><span data-ttu-id="7fa7c-149">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="7fa7c-149">Troubleshoot</span></span>
<span data-ttu-id="7fa7c-150">Если не удается подключиться tooyour виртуальных Машин Linux с помощью клиента удаленного рабочего стола, используйте `netstat` на вашей виртуальной Машине Linux tooverify, ВМ ожидающей подключений по протоколу RDP следующим образом:</span><span class="sxs-lookup"><span data-stu-id="7fa7c-150">If you cannot connect tooyour Linux VM using a Remote Desktop client, use `netstat` on your Linux VM tooverify that your VM is listening for RDP connections  as follows:</span></span>

```bash
sudo netstat -plnt | grep rdp
```

<span data-ttu-id="7fa7c-151">Следующий пример показывает Hello hello виртуальная машина прослушивает TCP-порт 3389 должным образом:</span><span class="sxs-lookup"><span data-stu-id="7fa7c-151">hello following example shows hello VM listening on TCP port 3389 as expected:</span></span>

```bash
tcp     0     0      127.0.0.1:3350     0.0.0.0:*     LISTEN     53192/xrdp-sesman
tcp     0     0      0.0.0.0:3389       0.0.0.0:*     LISTEN     53188/xrdp
```

<span data-ttu-id="7fa7c-152">Если порт не прослушивается hello xrdp службы, на Виртуальной машине Ubuntu перезапустите службу hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="7fa7c-152">If hello xrdp service is not listening, on an Ubuntu VM restart hello service as follows:</span></span>

```bash
sudo service xrdp restart
```

<span data-ttu-id="7fa7c-153">Просмотрите журналы */var/log*Thug на ВМ для выяснения наличия Ubuntu как toowhy hello служба не отвечает.</span><span class="sxs-lookup"><span data-stu-id="7fa7c-153">Review logs in */var/log*Thug  on your Ubuntu VM for indications as toowhy hello service may not be responding.</span></span> <span data-ttu-id="7fa7c-154">Также можно отслеживать hello syslog во время попытки подключения удаленного рабочего стола tooview ошибок:</span><span class="sxs-lookup"><span data-stu-id="7fa7c-154">You can also monitor hello syslog during a remote desktop connection attempt tooview any errors:</span></span>

```bash
tail -f /var/log/syslog
```

<span data-ttu-id="7fa7c-155">Службы toorestart различными способами и tooreview расположения файла журнала альтернативный, возможно других дистрибутивов Linux, например Red Hat Enterprise Linux и SUSE.</span><span class="sxs-lookup"><span data-stu-id="7fa7c-155">Other Linux distributions such as Red Hat Enterprise Linux and SUSE may have different ways toorestart services and alternate log file locations tooreview.</span></span>

<span data-ttu-id="7fa7c-156">Если не получают ответа в клиенте удаленного рабочего стола и увидеть все события в системном журнале hello, это указывает, что трафика удаленного рабочего стола не может связаться с hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="7fa7c-156">If you do not receive any response in your remote desktop client and do not see any events in hello system log, this behavior indicates that remote desktop traffic cannot reach hello VM.</span></span> <span data-ttu-id="7fa7c-157">Просмотрите tooensure правила сетевой безопасности группы имеется правило toopermit TCP через порт 3389.</span><span class="sxs-lookup"><span data-stu-id="7fa7c-157">Review your network security group rules tooensure that you have a rule toopermit TCP on port 3389.</span></span> <span data-ttu-id="7fa7c-158">Дополнительные сведения см. в статье [Устранение проблем с подключением к приложениям на виртуальных машинах Linux в Azure](../windows/troubleshoot-app-connection.md).</span><span class="sxs-lookup"><span data-stu-id="7fa7c-158">For more information, see [Troubleshoot application connectivity issues](../windows/troubleshoot-app-connection.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="7fa7c-159">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7fa7c-159">Next steps</span></span>
<span data-ttu-id="7fa7c-160">Дополнительные сведения о создании и использовании ключей SSH на виртуальных машинах Linux см. в статье [Создание пары из открытого и закрытого ключей SSH для виртуальных машин Linux](mac-create-ssh-keys.md).</span><span class="sxs-lookup"><span data-stu-id="7fa7c-160">For more information about creating and using SSH keys with Linux VMs, see [Create SSH keys for Linux VMs in Azure](mac-create-ssh-keys.md).</span></span>

<span data-ttu-id="7fa7c-161">Сведения об использовании SSH из Windows см. в разделе [как toouse SSH ключей с Windows](ssh-from-windows.md).</span><span class="sxs-lookup"><span data-stu-id="7fa7c-161">For information on using SSH from Windows, see [How toouse SSH keys with Windows](ssh-from-windows.md).</span></span>

