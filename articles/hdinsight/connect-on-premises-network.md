---
title: "aaaConnect HDInsight tooyour в локальной сети — Azure HDInsight | Документы Microsoft"
description: "Узнайте, как toocreate HDInsight кластер в виртуальной сети Azure и подключите его tooyour локальной сети. Узнайте, как tooconfigure имен между HDInsight и в локальной сети с помощью пользовательского DNS-сервера."
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/21/2017
ms.author: larryfr
ms.openlocfilehash: 8a3adf0e3df7726d8e6566d723700506baaf89a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-hdinsight-tooyour-on-premise-network"></a><span data-ttu-id="6bdd2-104">Подключение к HDInsight tooyour в локальной сети</span><span class="sxs-lookup"><span data-stu-id="6bdd2-104">Connect HDInsight tooyour on-premise network</span></span>

<span data-ttu-id="6bdd2-105">Узнайте, как tooconnect HDInsight tooyour в локальной сети с помощью виртуальных сетях Azure и VPN-шлюза.</span><span class="sxs-lookup"><span data-stu-id="6bdd2-105">Learn how tooconnect HDInsight tooyour on-premises network by using Azure Virtual Networks and a VPN gateway.</span></span> <span data-ttu-id="6bdd2-106">В этом документе содержатся следующие сведения о планировании:</span><span class="sxs-lookup"><span data-stu-id="6bdd2-106">This document provides planning information on:</span></span>

* <span data-ttu-id="6bdd2-107">С помощью HDInsight в виртуальной сети Azure, который подключается tooyour локальной сети.</span><span class="sxs-lookup"><span data-stu-id="6bdd2-107">Using HDInsight in an Azure Virtual Network that connects tooyour on-premises network.</span></span>

* <span data-ttu-id="6bdd2-108">Настройка разрешения имен DNS между виртуальной сетью hello и в локальной сети.</span><span class="sxs-lookup"><span data-stu-id="6bdd2-108">Configuring DNS name resolution between hello virtual network and your on-premises network.</span></span>

* <span data-ttu-id="6bdd2-109">Настройка доступа к сети безопасности группы toorestrict internet tooHDInsight.</span><span class="sxs-lookup"><span data-stu-id="6bdd2-109">Configuring network security groups toorestrict internet access tooHDInsight.</span></span>

* <span data-ttu-id="6bdd2-110">Порты, предоставляемые HDInsight hello виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="6bdd2-110">Ports provided by HDInsight on hello virtual network.</span></span>

## <a name="create-hello-virtual-network-configuration"></a><span data-ttu-id="6bdd2-111">Создать конфигурацию сети виртуальных hello</span><span class="sxs-lookup"><span data-stu-id="6bdd2-111">Create hello Virtual network configuration</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6bdd2-112">Если вы ищете пошаговые инструкции о подключении HDInsight tooyour в локальной сети с помощью виртуальной сети Azure см. в разделе hello [HDInsight подключения tooyour локальной сетью](connect-on-premises-network.md) документа.</span><span class="sxs-lookup"><span data-stu-id="6bdd2-112">If you are looking for step by step guidance on connecting HDInsight tooyour on-premises network using an Azure Virtual Network, see hello [Connect HDInsight tooyour on-premise network](connect-on-premises-network.md) document.</span></span>

<span data-ttu-id="6bdd2-113">Используйте следующие hello документы toolearn как toocreate виртуальной сети Azure, подключенной tooyour в локальной сети:</span><span class="sxs-lookup"><span data-stu-id="6bdd2-113">Use hello following documents toolearn how toocreate an Azure Virtual Network that is connected tooyour on-premises network:</span></span>
    
* [<span data-ttu-id="6bdd2-114">С помощью портала Azure hello</span><span class="sxs-lookup"><span data-stu-id="6bdd2-114">Using hello Azure portal</span></span>](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md)

* [<span data-ttu-id="6bdd2-115">Использование Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="6bdd2-115">Using Azure PowerShell</span></span>](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)

* [<span data-ttu-id="6bdd2-116">Использование интерфейса командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="6bdd2-116">Using Azure CLI</span></span>](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli.md)

## <a name="configure-name-resolution"></a><span data-ttu-id="6bdd2-117">Настройка разрешения имен</span><span class="sxs-lookup"><span data-stu-id="6bdd2-117">Configure name resolution</span></span>

<span data-ttu-id="6bdd2-118">tooallow HDInsight и ресурсы в toocommunicate hello объединить сети по имени, необходимо выполнить следующие действия hello:</span><span class="sxs-lookup"><span data-stu-id="6bdd2-118">tooallow HDInsight and resources in hello joined network toocommunicate by name, you must perform hello following actions:</span></span>

* <span data-ttu-id="6bdd2-119">Создание пользовательского DNS-сервера в hello виртуальной сети Azure.</span><span class="sxs-lookup"><span data-stu-id="6bdd2-119">Create a custom DNS server in hello Azure Virtual Network.</span></span>

* <span data-ttu-id="6bdd2-120">Настройте hello виртуальной сети toouse hello пользовательские DNS-сервер вместо по умолчанию hello Azure рекурсивного сопоставителя.</span><span class="sxs-lookup"><span data-stu-id="6bdd2-120">Configure hello virtual network toouse hello custom DNS server instead of hello default Azure Recursive Resolver.</span></span>

* <span data-ttu-id="6bdd2-121">Настройка перенаправления между hello пользовательского DNS-сервера и DNS-сервере в локальной среде.</span><span class="sxs-lookup"><span data-stu-id="6bdd2-121">Configure forwarding between hello custom DNS server and your on-premises DNS server.</span></span>

<span data-ttu-id="6bdd2-122">Такая конфигурация позволяет hello, следуя поведение:</span><span class="sxs-lookup"><span data-stu-id="6bdd2-122">This configuration enables hello following behavior:</span></span>

* <span data-ttu-id="6bdd2-123">Запросы на полные доменные имена DNS-суффиксом hello __для виртуальной сети hello__ перенаправляются toohello пользовательского DNS-сервера.</span><span class="sxs-lookup"><span data-stu-id="6bdd2-123">Requests for fully qualified domain names that have hello DNS suffix __for hello virtual network__ are forwarded toohello custom DNS server.</span></span> <span data-ttu-id="6bdd2-124">Hello пользовательского DNS-сервера, затем перенаправляет эти запросы toohello Azure рекурсивного сопоставителя возвращает hello IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="6bdd2-124">hello custom DNS server then forwards these requests toohello Azure Recursive Resolver, which returns hello IP address.</span></span>

* <span data-ttu-id="6bdd2-125">Все другие запросы перенаправляются toohello локального DNS-сервера.</span><span class="sxs-lookup"><span data-stu-id="6bdd2-125">All other requests are forwarded toohello on-premises DNS server.</span></span> <span data-ttu-id="6bdd2-126">Даже запросы открытый Интернет-ресурсов, таких как microsoft.com, перенаправляются toohello локального DNS-сервера для разрешения имен.</span><span class="sxs-lookup"><span data-stu-id="6bdd2-126">Even requests for public internet resources such as microsoft.com are forwarded toohello on-premises DNS server for name resolution.</span></span>

<span data-ttu-id="6bdd2-127">В следующие схемы hello зеленые линии являются запросы на ресурсы, заканчивающиеся на DNS-суффикс hello hello виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="6bdd2-127">In hello following diagram, green lines are requests for resources that end in hello DNS suffix of hello virtual network.</span></span> <span data-ttu-id="6bdd2-128">Синие линии — это запросы к ресурсам в локальной сети hello или в hello общедоступный Интернет.</span><span class="sxs-lookup"><span data-stu-id="6bdd2-128">Blue lines are requests for resources in hello on-premises network or on hello public internet.</span></span>

![Схема как DNS-запросы разрешаются в конфигурации hello, используемой в этом документе](./media/connect-on-premises-network/on-premises-to-cloud-dns.png)

### <a name="create-a-custom-dns-server"></a><span data-ttu-id="6bdd2-130">Создание пользовательского DNS-сервера</span><span class="sxs-lookup"><span data-stu-id="6bdd2-130">Create a custom DNS server</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6bdd2-131">Необходимо создать и настроить перед установкой HDInsight в виртуальной сети hello hello DNS-сервера.</span><span class="sxs-lookup"><span data-stu-id="6bdd2-131">You must create and configure hello DNS server before installing HDInsight into hello virtual network.</span></span>

<span data-ttu-id="6bdd2-132">ВМ Linux, который использует hello toocreate [привязки](https://www.isc.org/downloads/bind/) программное обеспечение DNS, hello используйте следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="6bdd2-132">toocreate a Linux VM that uses hello [Bind](https://www.isc.org/downloads/bind/) DNS software, use hello following steps:</span></span>

> [!NOTE]
> <span data-ttu-id="6bdd2-133">Hello Далее используется hello [портал Azure](https://portal.azure.com) toocreate виртуальной машине Azure.</span><span class="sxs-lookup"><span data-stu-id="6bdd2-133">hello following steps use hello [Azure portal](https://portal.azure.com) toocreate an Azure Virtual Machine.</span></span> <span data-ttu-id="6bdd2-134">Другие способы toocreate виртуальной машины в разделе hello [создания виртуальной Машины — Azure CLI](../virtual-machines/linux/quick-create-cli.md) и [создания виртуальной Машины — Azure PowerShell](../virtual-machines/linux/quick-create-portal.md) документов.</span><span class="sxs-lookup"><span data-stu-id="6bdd2-134">For other ways toocreate a virtual machine, see hello [Create VM - Azure CLI](../virtual-machines/linux/quick-create-cli.md) and [Create VM - Azure PowerShell](../virtual-machines/linux/quick-create-portal.md) documents.</span></span>

1. <span data-ttu-id="6bdd2-135">Из hello [портал Azure](https://portal.azure.com)выберите  __+__ , __вычислений__, и __Ubuntu Server 16.04 LTS__.</span><span class="sxs-lookup"><span data-stu-id="6bdd2-135">From hello [Azure portal](https://portal.azure.com), select __+__, __Compute__, and __Ubuntu Server 16.04 LTS__.</span></span>

    ![Создание виртуальной машины Ubuntu](./media/connect-on-premises-network/create-ubuntu-vm.png)

2. <span data-ttu-id="6bdd2-137">Из hello __основы__ введите hello следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="6bdd2-137">From hello __Basics__ section, enter hello following information:</span></span>

    * <span data-ttu-id="6bdd2-138">__Имя.__ Понятное имя, идентифицирующее виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="6bdd2-138">__Name__: A friendly name that identifies this virtual machine.</span></span> <span data-ttu-id="6bdd2-139">Например, __DNSProxy__.</span><span class="sxs-lookup"><span data-stu-id="6bdd2-139">For example, __DNSProxy__.</span></span>
    * <span data-ttu-id="6bdd2-140">__Имя пользователя__: hello имя hello SSH учетной записи.</span><span class="sxs-lookup"><span data-stu-id="6bdd2-140">__User name__: hello name of hello SSH account.</span></span>
    * <span data-ttu-id="6bdd2-141">__Открытый ключ SSH__ или __пароль__: hello метод проверки подлинности для учетной записи SSH hello.</span><span class="sxs-lookup"><span data-stu-id="6bdd2-141">__SSH public key__ or __Password__: hello authentication method for hello SSH account.</span></span> <span data-ttu-id="6bdd2-142">Мы рекомендуем использовать открытые ключи, так как они обеспечивают повышенную безопасность.</span><span class="sxs-lookup"><span data-stu-id="6bdd2-142">We recommend using public keys, as they are more secure.</span></span> <span data-ttu-id="6bdd2-143">Дополнительные сведения см. в разделе hello [Создание и использование ключей SSH для виртуальных машин Linux](../virtual-machines/linux/mac-create-ssh-keys.md) документа.</span><span class="sxs-lookup"><span data-stu-id="6bdd2-143">For more information, see hello [Create and use SSH keys for Linux VMs](../virtual-machines/linux/mac-create-ssh-keys.md) document.</span></span>
    * <span data-ttu-id="6bdd2-144">__Группа ресурсов__: выберите __использовать существующие__, а затем выберите группу ресурсов hello, содержащий hello виртуальную сеть, созданную ранее.</span><span class="sxs-lookup"><span data-stu-id="6bdd2-144">__Resource group__: Select __Use existing__, and then select hello resource group that contains hello virtual network created earlier.</span></span>
    * <span data-ttu-id="6bdd2-145">__Расположение__: выберите hello местоположения hello виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="6bdd2-145">__Location__: Select hello same location as hello virtual network.</span></span>

    ![Базовая конфигурация виртуальной машины](./media/connect-on-premises-network/vm-basics.png)

    <span data-ttu-id="6bdd2-147">Оставьте значения по умолчанию другие записи в hello, а затем выберите __ОК__.</span><span class="sxs-lookup"><span data-stu-id="6bdd2-147">Leave other entries at hello default values and then select __OK__.</span></span>

3. <span data-ttu-id="6bdd2-148">Из hello __выберите размер__ статьи hello выберите размер виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="6bdd2-148">From hello __Choose a size__ section, select hello VM size.</span></span> <span data-ttu-id="6bdd2-149">В этом учебнике выберите наименьшее hello и дешевый параметр.</span><span class="sxs-lookup"><span data-stu-id="6bdd2-149">For this tutorial, select hello smallest and lowest cost option.</span></span> <span data-ttu-id="6bdd2-150">toocontinue hello используйте __выберите__ кнопки.</span><span class="sxs-lookup"><span data-stu-id="6bdd2-150">toocontinue, use hello __Select__ button.</span></span>

4. <span data-ttu-id="6bdd2-151">Из hello __параметры__ введите hello следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="6bdd2-151">From hello __Settings__ section, enter hello following information:</span></span>

    * <span data-ttu-id="6bdd2-152">__Виртуальная сеть__: выберите hello виртуальной сети, которое было создано ранее.</span><span class="sxs-lookup"><span data-stu-id="6bdd2-152">__Virtual network__: Select hello virtual network that you created earlier.</span></span>

    * <span data-ttu-id="6bdd2-153">__Подсети__: выберите подсеть по умолчанию hello для hello виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="6bdd2-153">__Subnet__: Select hello default subnet for hello virtual network.</span></span> <span data-ttu-id="6bdd2-154">Сделать __не__ выберите hello подсети, используемый шлюзом VPN hello.</span><span class="sxs-lookup"><span data-stu-id="6bdd2-154">Do __not__ select hello subnet used by hello VPN gateway.</span></span>

    * <span data-ttu-id="6bdd2-155">__Учетная запись хранения диагностики.__Создайте учетную запись хранения или выберите имеющуюся.</span><span class="sxs-lookup"><span data-stu-id="6bdd2-155">__Diagnostics storage account__: Either select an existing storage account or create a new one.</span></span>

    ![Параметры виртуальной сети](./media/connect-on-premises-network/virtual-network-settings.png)

    <span data-ttu-id="6bdd2-157">Оставьте hello другие записи в значение по умолчанию hello, а затем выберите __ОК__ toocontinue.</span><span class="sxs-lookup"><span data-stu-id="6bdd2-157">Leave hello other entries at hello default value, then select __OK__ toocontinue.</span></span>

5. <span data-ttu-id="6bdd2-158">Из hello __покупки__ раздел, выберите hello __покупки__ кнопку toocreate hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="6bdd2-158">From hello __Purchase__ section, select hello __Purchase__ button toocreate hello virtual machine.</span></span>

6. <span data-ttu-id="6bdd2-159">После создания виртуальной машины hello его __Обзор__ отображается раздел.</span><span class="sxs-lookup"><span data-stu-id="6bdd2-159">Once hello virtual machine has been created, its __Overview__ section is displayed.</span></span> <span data-ttu-id="6bdd2-160">Выберите из списка hello слева hello __свойства__.</span><span class="sxs-lookup"><span data-stu-id="6bdd2-160">From hello list on hello left, select __Properties__.</span></span> <span data-ttu-id="6bdd2-161">Сохранить hello __общедоступный IP-адрес__ и __частный IP-адрес__ значения.</span><span class="sxs-lookup"><span data-stu-id="6bdd2-161">Save hello __Public IP address__ and __Private IP address__ values.</span></span> <span data-ttu-id="6bdd2-162">Он будет использоваться в следующем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="6bdd2-162">It will be used in hello next section.</span></span>

    ![Общедоступные и частные IP-адреса](./media/connect-on-premises-network/vm-ip-addresses.png)

### <a name="install-and-configure-bind-dns-software"></a><span data-ttu-id="6bdd2-164">Установка и настройка Bind (программное обеспечение DNS)</span><span class="sxs-lookup"><span data-stu-id="6bdd2-164">Install and configure Bind (DNS software)</span></span>

1. <span data-ttu-id="6bdd2-165">Использовать SSH tooconnect toohello __общедоступный IP-адрес__ hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="6bdd2-165">Use SSH tooconnect toohello __public IP address__ of hello virtual machine.</span></span> <span data-ttu-id="6bdd2-166">Следующий пример Hello подключается виртуальная машина tooa 40.68.254.142:</span><span class="sxs-lookup"><span data-stu-id="6bdd2-166">hello following example connects tooa virtual machine at 40.68.254.142:</span></span>

    ```bash
    ssh sshuser@40.68.254.142
    ```

    <span data-ttu-id="6bdd2-167">Замените `sshuser` with hello учетной записи пользователя SSH указан при создании кластера hello.</span><span class="sxs-lookup"><span data-stu-id="6bdd2-167">Replace `sshuser` with hello SSH user account you specified when creating hello cluster.</span></span>

    > [!NOTE]
    > <span data-ttu-id="6bdd2-168">Существует множество способов tooobtain hello `ssh` программы.</span><span class="sxs-lookup"><span data-stu-id="6bdd2-168">There are a variety of ways tooobtain hello `ssh` utility.</span></span> <span data-ttu-id="6bdd2-169">В Linux, Unix и macOS предоставляется как часть операционной системы hello.</span><span class="sxs-lookup"><span data-stu-id="6bdd2-169">On Linux, Unix, and macOS, it is provided as part of hello operating system.</span></span> <span data-ttu-id="6bdd2-170">Если вы используете Windows, рассмотрите одну из hello следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="6bdd2-170">If you are using Windows, consider one of hello following options:</span></span>
    >
    > * <span data-ttu-id="6bdd2-171">[Azure Cloud Shell](../cloud-shell/quickstart.md);</span><span class="sxs-lookup"><span data-stu-id="6bdd2-171">[Azure Cloud Shell](../cloud-shell/quickstart.md)</span></span>
    > * <span data-ttu-id="6bdd2-172">[Bash на платформе Ubuntu в Windows 10](https://msdn.microsoft.com/commandline/wsl/about);</span><span class="sxs-lookup"><span data-stu-id="6bdd2-172">[Bash on Ubuntu on Windows 10](https://msdn.microsoft.com/commandline/wsl/about)</span></span>
    > * <span data-ttu-id="6bdd2-173">[Git (https://git-scm.com/)](https://git-scm.com/);</span><span class="sxs-lookup"><span data-stu-id="6bdd2-173">[Git (https://git-scm.com/)](https://git-scm.com/)</span></span>
    > * <span data-ttu-id="6bdd2-174">[OpenSSH (https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)](https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH).</span><span class="sxs-lookup"><span data-stu-id="6bdd2-174">[OpenSSH (https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)](https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)</span></span>

2. <span data-ttu-id="6bdd2-175">tooinstall Bind, используйте следующие команды из сеанса SSH hello hello:</span><span class="sxs-lookup"><span data-stu-id="6bdd2-175">tooinstall Bind, use hello following commands from hello SSH session:</span></span>

    ```bash
    sudo apt-get update -y
    sudo apt-get install bind9 -y
    ```

3. <span data-ttu-id="6bdd2-176">tooconfigure привязки tooforward имя разрешения запросов tooyour локального DNS-сервера, используйте hello после текста как содержимое hello hello `/etc/bind/named.conf.options` файла:</span><span class="sxs-lookup"><span data-stu-id="6bdd2-176">tooconfigure Bind tooforward name resolution requests tooyour on-prem DNS server, use hello following text as hello contents of hello `/etc/bind/named.conf.options` file:</span></span>

        acl goodclients {
            10.0.0.0/16; # Replace with hello IP address range of hello virtual network
            10.1.0.0/16; # Replace with hello IP address range of hello on-premises network
            localhost;
            localnets;
        };

        options {
                directory "/var/cache/bind";

                recursion yes;

                allow-query { goodclients; };

                forwarders {
                192.168.0.1; # Replace with hello IP address of hello on-premises DNS server
                };

                dnssec-validation auto;

                auth-nxdomain no;    # conform tooRFC1035
                listen-on { any; };
        };

    > [!IMPORTANT]
    > <span data-ttu-id="6bdd2-177">Замените значения hello hello `goodclients` раздел с hello диапазон IP-адресов виртуальной сети hello и локальной сетью.</span><span class="sxs-lookup"><span data-stu-id="6bdd2-177">Replace hello values in hello `goodclients` section with hello IP address range of hello virtual network and on-premises network.</span></span> <span data-ttu-id="6bdd2-178">В этом разделе определяет hello адреса, которые этот DNS-сервер принимает запросы от.</span><span class="sxs-lookup"><span data-stu-id="6bdd2-178">This section defines hello addresses that this DNS server accepts requests from.</span></span>
    >
    > <span data-ttu-id="6bdd2-179">Замените hello `192.168.0.1` запись в hello `forwarders` раздел с hello IP-адрес локального DNS-сервера.</span><span class="sxs-lookup"><span data-stu-id="6bdd2-179">Replace hello `192.168.0.1` entry in hello `forwarders` section with hello IP address of your on-premises DNS server.</span></span> <span data-ttu-id="6bdd2-180">Это tooyour запросы записи DNS маршруты локального DNS-сервера для разрешения.</span><span class="sxs-lookup"><span data-stu-id="6bdd2-180">This entry routes DNS requests tooyour on-premises DNS server for resolution.</span></span>

    <span data-ttu-id="6bdd2-181">tooedit этот файл hello используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="6bdd2-181">tooedit this file, use hello following command:</span></span>

    ```bash
    sudo nano /etc/bind/named.conf.options
    ```

    <span data-ttu-id="6bdd2-182">toosave hello файла, используйте __Ctrl + X__, __Y__, а затем __ввод__.</span><span class="sxs-lookup"><span data-stu-id="6bdd2-182">toosave hello file, use __Ctrl+X__, __Y__, and then __Enter__.</span></span>

4. <span data-ttu-id="6bdd2-183">В сеансе SSH hello используйте hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="6bdd2-183">From hello SSH session, use hello following command:</span></span>

    ```bash
    hostname -f
    ```

    <span data-ttu-id="6bdd2-184">Эта команда возвращает аналогичные toohello значение, следующий текст:</span><span class="sxs-lookup"><span data-stu-id="6bdd2-184">This command returns a value similar toohello following text:</span></span>

        dnsproxy.icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net

    <span data-ttu-id="6bdd2-185">Hello `icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net` — текст hello __DNS-суффикс__ для этой виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="6bdd2-185">hello `icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net` text is hello __DNS suffix__ for this virtual network.</span></span> <span data-ttu-id="6bdd2-186">Сохраните это значение, так как оно будет использовано позже.</span><span class="sxs-lookup"><span data-stu-id="6bdd2-186">Save this value, as it is used later.</span></span>

5. <span data-ttu-id="6bdd2-187">tooconfigure привязки tooresolve DNS-имена для ресурсов в пределах hello виртуальной сети, используйте hello после текста как содержимое hello hello `/etc/bind/named.conf.local` файла:</span><span class="sxs-lookup"><span data-stu-id="6bdd2-187">tooconfigure Bind tooresolve DNS names for resources within hello virtual network, use hello following text as hello contents of hello `/etc/bind/named.conf.local` file:</span></span>

        // Replace hello following with hello DNS suffix for your virtual network
        zone "icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net" {
            type forward;
            forwarders {168.63.129.16;}; # hello Azure recursive resolver
        };

    > [!IMPORTANT]
    > <span data-ttu-id="6bdd2-188">Необходимо заменить hello `icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net` с DNS-суффиксом hello, извлеченного ранее.</span><span class="sxs-lookup"><span data-stu-id="6bdd2-188">You must replace hello `icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net` with hello DNS suffix you retrieved earlier.</span></span>

    <span data-ttu-id="6bdd2-189">tooedit этот файл hello используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="6bdd2-189">tooedit this file, use hello following command:</span></span>

    ```bash
    sudo nano /etc/bind/named.conf.local
    ```

    <span data-ttu-id="6bdd2-190">toosave hello файла, используйте __Ctrl + X__, __Y__, а затем __ввод__.</span><span class="sxs-lookup"><span data-stu-id="6bdd2-190">toosave hello file, use __Ctrl+X__, __Y__, and then __Enter__.</span></span>

6. <span data-ttu-id="6bdd2-191">toostart привязки hello используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="6bdd2-191">toostart Bind, use hello following command:</span></span>

    ```bash
    sudo service bind9 restart
    ```

7. <span data-ttu-id="6bdd2-192">tooverify, к которой привязана может разрешать имена hello ресурсам в локальной сети, hello используйте следующие команды:</span><span class="sxs-lookup"><span data-stu-id="6bdd2-192">tooverify that bind can resolve hello names of resources in your on-premises network, use hello following commands:</span></span>

    ```bash
    sudo apt install dnsutils
    nslookup dns.mynetwork.net 10.0.0.4
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="6bdd2-193">Замените `dns.mynetwork.net` с hello полное доменное имя (FQDN) ресурса в локальной сети.</span><span class="sxs-lookup"><span data-stu-id="6bdd2-193">Replace `dns.mynetwork.net` with hello fully qualified domain name (FQDN) of a resource in your on-premises network.</span></span>
    >
    > <span data-ttu-id="6bdd2-194">Замените `10.0.0.4` с hello __внутренний IP-адрес__ пользовательские DNS-сервера в виртуальной сети hello.</span><span class="sxs-lookup"><span data-stu-id="6bdd2-194">Replace `10.0.0.4` with hello __internal IP address__ of your custom DNS server in hello virtual network.</span></span>

    <span data-ttu-id="6bdd2-195">Появится ответ Hello аналогичные toohello следующий текст:</span><span class="sxs-lookup"><span data-stu-id="6bdd2-195">hello response appears similar toohello following text:</span></span>

        Server:         10.0.0.4
        Address:        10.0.0.4#53

        Non-authoritative answer:
        Name:   dns.mynetwork.net
        Address: 192.168.0.4

### <a name="configure-hello-virtual-network-toouse-hello-custom-dns-server"></a><span data-ttu-id="6bdd2-196">Настройка hello виртуальной сети toouse hello пользовательского DNS-сервера</span><span class="sxs-lookup"><span data-stu-id="6bdd2-196">Configure hello virtual network toouse hello custom DNS server</span></span>

<span data-ttu-id="6bdd2-197">tooconfigure hello виртуальной сети toouse hello пользовательские DNS-сервер вместо hello Azure рекурсивного сопоставителя, использовать hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="6bdd2-197">tooconfigure hello virtual network toouse hello custom DNS server instead of hello Azure recursive resolver, use hello following steps:</span></span>

1. <span data-ttu-id="6bdd2-198">В hello [портал Azure](https://portal.azure.com), выберите hello виртуальной сети, а затем выберите __DNS-серверы__.</span><span class="sxs-lookup"><span data-stu-id="6bdd2-198">In hello [Azure portal](https://portal.azure.com), select hello virtual network, and then select __DNS Servers__.</span></span>

2. <span data-ttu-id="6bdd2-199">Выберите __пользовательские__и введите hello __внутренний IP-адрес__ hello пользовательские DNS-сервера.</span><span class="sxs-lookup"><span data-stu-id="6bdd2-199">Select __Custom__, and enter hello __internal IP address__ of hello custom DNS server.</span></span> <span data-ttu-id="6bdd2-200">Наконец, щелкните __Сохранить__.</span><span class="sxs-lookup"><span data-stu-id="6bdd2-200">Finally, select __Save__.</span></span>

    ![Набор hello пользовательского DNS-сервера для сети hello](./media/connect-on-premises-network/configure-custom-dns.png)

### <a name="configure-hello-on-premises-dns-server"></a><span data-ttu-id="6bdd2-202">Настройка hello локального DNS-сервера</span><span class="sxs-lookup"><span data-stu-id="6bdd2-202">Configure hello on-premises DNS server</span></span>

<span data-ttu-id="6bdd2-203">В предыдущем разделе hello вы настроили hello пользовательского DNS server tooforward запросов toohello локального DNS-сервера.</span><span class="sxs-lookup"><span data-stu-id="6bdd2-203">In hello previous section, you configured hello custom DNS server tooforward requests toohello on-premises DNS server.</span></span> <span data-ttu-id="6bdd2-204">Далее необходимо настроить hello локальных DNS server tooforward запросов toohello пользовательского DNS-сервера.</span><span class="sxs-lookup"><span data-stu-id="6bdd2-204">Next, you must configure hello on-premises DNS server tooforward requests toohello custom DNS server.</span></span>

<span data-ttu-id="6bdd2-205">Конкретные действия по tooconfigure DNS-сервере, см. в документации hello для программного обеспечения сервера DNS.</span><span class="sxs-lookup"><span data-stu-id="6bdd2-205">For specific steps on how tooconfigure your DNS server, consult hello documentation for your DNS server software.</span></span> <span data-ttu-id="6bdd2-206">Поиск hello инструкций о том, как tooconfigure __условной пересылки__.</span><span class="sxs-lookup"><span data-stu-id="6bdd2-206">Look for hello steps on how tooconfigure a __conditional forwarder__.</span></span>

<span data-ttu-id="6bdd2-207">Сервер условной пересылки только переадресовывает запросы по определенным DNS-суффиксам.</span><span class="sxs-lookup"><span data-stu-id="6bdd2-207">A conditional forward only forwards requests for a specific DNS suffix.</span></span> <span data-ttu-id="6bdd2-208">В этом случае необходимо настроить пересылки DNS-суффикс hello hello виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="6bdd2-208">In this case, you must configure a forwarder for hello DNS suffix of hello virtual network.</span></span> <span data-ttu-id="6bdd2-209">IP-адрес toohello hello пользовательского DNS-сервера следует перенаправить запросы для этого суффикса.</span><span class="sxs-lookup"><span data-stu-id="6bdd2-209">Requests for this suffix should be forwarded toohello IP address of hello custom DNS server.</span></span> 

<span data-ttu-id="6bdd2-210">Hello следующий текст является примером конфигурацию условной пересылки для hello **привязки** программное обеспечение DNS:</span><span class="sxs-lookup"><span data-stu-id="6bdd2-210">hello following text is an example of a conditional forwarder configuration for hello **Bind** DNS software:</span></span>

    zone "icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net" {
        type forward;
        forwarders {10.0.0.4;}; # hello custom DNS server's internal IP address
    };

<span data-ttu-id="6bdd2-211">Дополнительные сведения об использовании DNS на **Windows Server 2016**, разделе hello [DnsServerConditionalForwarderZone добавить](https://technet.microsoft.com/itpro/powershell/windows/dnsserver/add-dnsserverconditionalforwarderzone) документации...</span><span class="sxs-lookup"><span data-stu-id="6bdd2-211">For information on using DNS on **Windows Server 2016**, see hello [Add-DnsServerConditionalForwarderZone](https://technet.microsoft.com/itpro/powershell/windows/dnsserver/add-dnsserverconditionalforwarderzone) documentation...</span></span>

<span data-ttu-id="6bdd2-212">Настроив hello локального DNS-сервера, можно использовать `nslookup` hello в локальной сети tooverify, может разрешать имена в виртуальной сети hello.</span><span class="sxs-lookup"><span data-stu-id="6bdd2-212">Once you have configured hello on-premises DNS server, you can use `nslookup` from hello on-premises network tooverify that you can resolve names in hello virtual network.</span></span> <span data-ttu-id="6bdd2-213">Следующий пример Hello</span><span class="sxs-lookup"><span data-stu-id="6bdd2-213">hello following example</span></span> 

```bash
nslookup dnsproxy.icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net 196.168.0.4
```

<span data-ttu-id="6bdd2-214">В этом примере локальный DNS-сервер на 196.168.0.4 hello использует имя hello tooresolve hello пользовательского DNS-сервера.</span><span class="sxs-lookup"><span data-stu-id="6bdd2-214">This example uses hello on-premises DNS server at 196.168.0.4 tooresolve hello name of hello custom DNS server.</span></span> <span data-ttu-id="6bdd2-215">Замените hello IP-адрес hello, один для hello локального DNS-сервера.</span><span class="sxs-lookup"><span data-stu-id="6bdd2-215">Replace hello IP address with hello one for hello on-premises DNS server.</span></span> <span data-ttu-id="6bdd2-216">Замените hello `dnsproxy` адрес с hello полное доменное имя DNS-сервера, настраиваемые приветствия.</span><span class="sxs-lookup"><span data-stu-id="6bdd2-216">Replace hello `dnsproxy` address with hello fully qualified domain name of hello custom DNS server.</span></span>

## <a name="optional-control-network-traffic"></a><span data-ttu-id="6bdd2-217">Управление сетевым трафиком (необязательно)</span><span class="sxs-lookup"><span data-stu-id="6bdd2-217">Optional: Control network traffic</span></span>

<span data-ttu-id="6bdd2-218">Можно использовать группы безопасности сети (NSG) или определяемых пользователем маршрутов (UDR) toocontrol сетевого трафика.</span><span class="sxs-lookup"><span data-stu-id="6bdd2-218">You can use network security groups (NSG) or user-defined routes (UDR) toocontrol network traffic.</span></span> <span data-ttu-id="6bdd2-219">Группы Nsg позволяют toofilter входящий и исходящий трафик и разрешить или запретить трафик hello.</span><span class="sxs-lookup"><span data-stu-id="6bdd2-219">NSGs allow you toofilter inbound and outbound traffic, and allow or deny hello traffic.</span></span> <span data-ttu-id="6bdd2-220">UDRs позволяют toocontrol потоки трафика между ресурсами в виртуальной сети hello и hello Интернет hello в локальной сети.</span><span class="sxs-lookup"><span data-stu-id="6bdd2-220">UDRs allow you toocontrol how traffic flows between resources in hello virtual network, hello internet, and hello on-premises network.</span></span>

> [!WARNING]
> <span data-ttu-id="6bdd2-221">Для HDInsight требуется входящий доступ с определенных IP-адресов в облако Azure hello и исходящий неограниченный доступ.</span><span class="sxs-lookup"><span data-stu-id="6bdd2-221">HDInsight requires inbound access from specific IP addresses in hello Azure cloud, and unrestricted outbound access.</span></span> <span data-ttu-id="6bdd2-222">При использовании Nsg или UDRs toocontrol трафика, необходимо выполнить следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="6bdd2-222">When using NSGs or UDRs toocontrol traffic, you must perform hello following steps:</span></span>
>
> 1. <span data-ttu-id="6bdd2-223">Найти hello IP-адресов для hello расположение, которое содержит виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="6bdd2-223">Find hello IP addresses for hello location that contains your virtual network.</span></span> <span data-ttu-id="6bdd2-224">Список требуемых IP-адресов по расположениям см. в [этом разделе](./hdinsight-extend-hadoop-virtual-network.md#hdinsight-ip).</span><span class="sxs-lookup"><span data-stu-id="6bdd2-224">For a list of required IPs by location, see [Required IP addresses](./hdinsight-extend-hadoop-virtual-network.md#hdinsight-ip).</span></span>
>
> 2. <span data-ttu-id="6bdd2-225">Разрешать входящий трафик от hello IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="6bdd2-225">Allow inbound traffic from hello IP addresses.</span></span>
>
>    * <span data-ttu-id="6bdd2-226">__NSG__: Разрешить __входящий__ трафик через порт __443__ из hello __Internet__.</span><span class="sxs-lookup"><span data-stu-id="6bdd2-226">__NSG__: Allow __inbound__ traffic on port __443__ from hello __Internet__.</span></span>
>    * <span data-ttu-id="6bdd2-227">__UDR__: hello набор __следующего прыжка__ тип too__Internet__ hello маршрута.</span><span class="sxs-lookup"><span data-stu-id="6bdd2-227">__UDR__: Set hello __Next Hop__ type of hello route too__Internet__.</span></span>

<span data-ttu-id="6bdd2-228">Пример использования Azure PowerShell или Azure CLI hello toocreate Nsg см. в разделе hello [расширить HDInsight с виртуальными сетями Azure](./hdinsight-extend-hadoop-virtual-network.md#hdinsight-nsg) документа.</span><span class="sxs-lookup"><span data-stu-id="6bdd2-228">For an example of using Azure PowerShell or hello Azure CLI toocreate NSGs, see hello [Extend HDInsight with Azure Virtual Networks](./hdinsight-extend-hadoop-virtual-network.md#hdinsight-nsg) document.</span></span>

## <a name="create-hello-hdinsight-cluster"></a><span data-ttu-id="6bdd2-229">Создание кластера HDInsight hello</span><span class="sxs-lookup"><span data-stu-id="6bdd2-229">Create hello HDInsight cluster</span></span>

> [!WARNING]
> <span data-ttu-id="6bdd2-230">Hello пользовательского DNS-сервера необходимо настроить перед установкой HDInsight в виртуальной сети hello.</span><span class="sxs-lookup"><span data-stu-id="6bdd2-230">You must configure hello custom DNS server before installing HDInsight in hello virtual network.</span></span>

<span data-ttu-id="6bdd2-231">Используйте hello шагов в hello [создание кластера HDInsight с помощью портала Azure hello](./hdinsight-hadoop-create-linux-clusters-portal.md) toocreate документ кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="6bdd2-231">Use hello steps in hello [Create an HDInsight cluster using hello Azure portal](./hdinsight-hadoop-create-linux-clusters-portal.md) document toocreate an HDInsight cluster.</span></span>

> [!WARNING]
> * <span data-ttu-id="6bdd2-232">Во время создания кластера необходимо выбрать расположение hello, которое содержит виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="6bdd2-232">During cluster creation, you must choose hello location that contains your virtual network.</span></span>
>
> * <span data-ttu-id="6bdd2-233">В hello __Дополнительные параметры__ часть конфигурации, необходимо выбрать hello виртуальной сети и подсети, созданной ранее.</span><span class="sxs-lookup"><span data-stu-id="6bdd2-233">In hello __Advanced settings__ part of configuration, you must select hello virtual network and subnet that you created earlier.</span></span>

## <a name="connecting-toohdinsight"></a><span data-ttu-id="6bdd2-234">Подключение tooHDInsight</span><span class="sxs-lookup"><span data-stu-id="6bdd2-234">Connecting tooHDInsight</span></span>

<span data-ttu-id="6bdd2-235">Большая часть документации по HDInsight предполагается, что кластер toohello доступ через hello Интернета.</span><span class="sxs-lookup"><span data-stu-id="6bdd2-235">Most documentation on HDInsight assumes that you have access toohello cluster over hello internet.</span></span> <span data-ttu-id="6bdd2-236">Например, возможность подключения кластера toohello в https://CLUSTERNAME.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="6bdd2-236">For example, that you can connect toohello cluster at https://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="6bdd2-237">Этот адрес используется hello открытый шлюз, который недоступен, если вы использовали Nsg или Здравствуйте, UDRs toorestrict доступ из Интернета.</span><span class="sxs-lookup"><span data-stu-id="6bdd2-237">This address uses hello public gateway, which is not available if you have used NSGs or UDRs toorestrict access from hello internet.</span></span>

<span data-ttu-id="6bdd2-238">toodirectly подключение tooHDInsight через hello виртуальную сеть, использовать hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="6bdd2-238">toodirectly connect tooHDInsight through hello virtual network, use hello following steps:</span></span>

1. <span data-ttu-id="6bdd2-239">toodiscover hello внутренней полные доменные имена узлов кластера HDInsight hello, используйте один из следующих методов hello:</span><span class="sxs-lookup"><span data-stu-id="6bdd2-239">toodiscover hello internal fully qualified domain names of hello HDInsight cluster nodes, use one of hello following methods:</span></span>

    ```powershell
    $resourceGroupName = "hello resource group that contains hello virtual network used with HDInsight"

    $clusterNICs = Get-AzureRmNetworkInterface -ResourceGroupName $resourceGroupName | where-object {$_.Name -like "*node*"}

    $nodes = @()
    foreach($nic in $clusterNICs) {
        $node = new-object System.Object
        $node | add-member -MemberType NoteProperty -name "Type" -value $nic.Name.Split('-')[1]
        $node | add-member -MemberType NoteProperty -name "InternalIP" -value $nic.IpConfigurations.PrivateIpAddress
        $node | add-member -MemberType NoteProperty -name "InternalFQDN" -value $nic.DnsSettings.InternalFqdn
        $nodes += $node
    }
    $nodes | sort-object Type
    ```

    ```azurecli
    az network nic list --resource-group <resourcegroupname> --output table --query "[?contains(name,'node')].{NICname:name,InternalIP:ipConfigurations[0].privateIpAddress,InternalFQDN:dnsSettings.internalFqdn}"
    ```

2. <span data-ttu-id="6bdd2-240">toodetermine hello доступный порт, службы, в разделе hello [порты, используемые службами Hadoop в HDInsight](./hdinsight-hadoop-port-settings-for-services.md) документа.</span><span class="sxs-lookup"><span data-stu-id="6bdd2-240">toodetermine hello port that a service is available on, see hello [Ports used by Hadoop services on HDInsight](./hdinsight-hadoop-port-settings-for-services.md) document.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="6bdd2-241">Некоторые службы, размещенной на hello головного узла активны только на одном узле одновременно.</span><span class="sxs-lookup"><span data-stu-id="6bdd2-241">Some services hosted on hello head nodes are only active on one node at a time.</span></span> <span data-ttu-id="6bdd2-242">При попытке доступа к службе на один головной узел и происходит сбой, переключитесь toohello других головного узла.</span><span class="sxs-lookup"><span data-stu-id="6bdd2-242">If you try accessing a service on one head node and it fails, switch toohello other head node.</span></span>
    >
    > <span data-ttu-id="6bdd2-243">Например, Ambari одновременно активен только на одном головном узле.</span><span class="sxs-lookup"><span data-stu-id="6bdd2-243">For example, Ambari is only active on one head node at a time.</span></span> <span data-ttu-id="6bdd2-244">Если при доступе к Ambari на один головной узел, он возвращает ошибку 404, то она работает на hello других головного узла.</span><span class="sxs-lookup"><span data-stu-id="6bdd2-244">If you try accessing Ambari on one head node and it returns a 404 error, then it is running on hello other head node.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6bdd2-245">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6bdd2-245">Next steps</span></span>

* <span data-ttu-id="6bdd2-246">Дополнительные сведения об использовании HDInsight в виртуальной сети см. в статье [Расширение возможностей HDInsight с помощью виртуальной сети Azure](./hdinsight-extend-hadoop-virtual-network.md).</span><span class="sxs-lookup"><span data-stu-id="6bdd2-246">For more information on using HDInsight in a virtual network, see [Extend HDInsight by using Azure Virtual Networks](./hdinsight-extend-hadoop-virtual-network.md).</span></span>

* <span data-ttu-id="6bdd2-247">Дополнительные сведения о виртуальных сетях Azure см. в разделе hello [Обзор виртуальной сети Azure](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6bdd2-247">For more information on Azure virtual networks, see hello [Azure Virtual Network overview](../virtual-network/virtual-networks-overview.md).</span></span>

* <span data-ttu-id="6bdd2-248">Дополнительные сведения о группах безопасности сети см. в статье [Фильтрация сетевого трафика с помощью групп безопасности сети](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="6bdd2-248">For more information on network security groups, see [Network security groups](../virtual-network/virtual-networks-nsg.md).</span></span>

* <span data-ttu-id="6bdd2-249">Дополнительные сведения о пользовательских маршрутах см. в статье [Определяемые пользователем маршруты и IP-пересылка](../virtual-network/virtual-networks-udr-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6bdd2-249">For more information on user-defined routes, see [USer-defined routes and IP forwarding](../virtual-network/virtual-networks-udr-overview.md).</span></span>
