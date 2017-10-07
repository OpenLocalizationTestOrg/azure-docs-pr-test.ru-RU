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
# <a name="connect-hdinsight-tooyour-on-premise-network"></a>Подключение к HDInsight tooyour в локальной сети

Узнайте, как tooconnect HDInsight tooyour в локальной сети с помощью виртуальных сетях Azure и VPN-шлюза. В этом документе содержатся следующие сведения о планировании:

* С помощью HDInsight в виртуальной сети Azure, который подключается tooyour локальной сети.

* Настройка разрешения имен DNS между виртуальной сетью hello и в локальной сети.

* Настройка доступа к сети безопасности группы toorestrict internet tooHDInsight.

* Порты, предоставляемые HDInsight hello виртуальной сети.

## <a name="create-hello-virtual-network-configuration"></a>Создать конфигурацию сети виртуальных hello

> [!IMPORTANT]
> Если вы ищете пошаговые инструкции о подключении HDInsight tooyour в локальной сети с помощью виртуальной сети Azure см. в разделе hello [HDInsight подключения tooyour локальной сетью](connect-on-premises-network.md) документа.

Используйте следующие hello документы toolearn как toocreate виртуальной сети Azure, подключенной tooyour в локальной сети:
    
* [С помощью портала Azure hello](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md)

* [Использование Azure PowerShell](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)

* [Использование интерфейса командной строки Azure](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli.md)

## <a name="configure-name-resolution"></a>Настройка разрешения имен

tooallow HDInsight и ресурсы в toocommunicate hello объединить сети по имени, необходимо выполнить следующие действия hello:

* Создание пользовательского DNS-сервера в hello виртуальной сети Azure.

* Настройте hello виртуальной сети toouse hello пользовательские DNS-сервер вместо по умолчанию hello Azure рекурсивного сопоставителя.

* Настройка перенаправления между hello пользовательского DNS-сервера и DNS-сервере в локальной среде.

Такая конфигурация позволяет hello, следуя поведение:

* Запросы на полные доменные имена DNS-суффиксом hello __для виртуальной сети hello__ перенаправляются toohello пользовательского DNS-сервера. Hello пользовательского DNS-сервера, затем перенаправляет эти запросы toohello Azure рекурсивного сопоставителя возвращает hello IP-адрес.

* Все другие запросы перенаправляются toohello локального DNS-сервера. Даже запросы открытый Интернет-ресурсов, таких как microsoft.com, перенаправляются toohello локального DNS-сервера для разрешения имен.

В следующие схемы hello зеленые линии являются запросы на ресурсы, заканчивающиеся на DNS-суффикс hello hello виртуальной сети. Синие линии — это запросы к ресурсам в локальной сети hello или в hello общедоступный Интернет.

![Схема как DNS-запросы разрешаются в конфигурации hello, используемой в этом документе](./media/connect-on-premises-network/on-premises-to-cloud-dns.png)

### <a name="create-a-custom-dns-server"></a>Создание пользовательского DNS-сервера

> [!IMPORTANT]
> Необходимо создать и настроить перед установкой HDInsight в виртуальной сети hello hello DNS-сервера.

ВМ Linux, который использует hello toocreate [привязки](https://www.isc.org/downloads/bind/) программное обеспечение DNS, hello используйте следующие шаги:

> [!NOTE]
> Hello Далее используется hello [портал Azure](https://portal.azure.com) toocreate виртуальной машине Azure. Другие способы toocreate виртуальной машины в разделе hello [создания виртуальной Машины — Azure CLI](../virtual-machines/linux/quick-create-cli.md) и [создания виртуальной Машины — Azure PowerShell](../virtual-machines/linux/quick-create-portal.md) документов.

1. Из hello [портал Azure](https://portal.azure.com)выберите  __+__ , __вычислений__, и __Ubuntu Server 16.04 LTS__.

    ![Создание виртуальной машины Ubuntu](./media/connect-on-premises-network/create-ubuntu-vm.png)

2. Из hello __основы__ введите hello следующую информацию:

    * __Имя.__ Понятное имя, идентифицирующее виртуальную машину. Например, __DNSProxy__.
    * __Имя пользователя__: hello имя hello SSH учетной записи.
    * __Открытый ключ SSH__ или __пароль__: hello метод проверки подлинности для учетной записи SSH hello. Мы рекомендуем использовать открытые ключи, так как они обеспечивают повышенную безопасность. Дополнительные сведения см. в разделе hello [Создание и использование ключей SSH для виртуальных машин Linux](../virtual-machines/linux/mac-create-ssh-keys.md) документа.
    * __Группа ресурсов__: выберите __использовать существующие__, а затем выберите группу ресурсов hello, содержащий hello виртуальную сеть, созданную ранее.
    * __Расположение__: выберите hello местоположения hello виртуальной сети.

    ![Базовая конфигурация виртуальной машины](./media/connect-on-premises-network/vm-basics.png)

    Оставьте значения по умолчанию другие записи в hello, а затем выберите __ОК__.

3. Из hello __выберите размер__ статьи hello выберите размер виртуальной Машины. В этом учебнике выберите наименьшее hello и дешевый параметр. toocontinue hello используйте __выберите__ кнопки.

4. Из hello __параметры__ введите hello следующую информацию:

    * __Виртуальная сеть__: выберите hello виртуальной сети, которое было создано ранее.

    * __Подсети__: выберите подсеть по умолчанию hello для hello виртуальной сети. Сделать __не__ выберите hello подсети, используемый шлюзом VPN hello.

    * __Учетная запись хранения диагностики.__Создайте учетную запись хранения или выберите имеющуюся.

    ![Параметры виртуальной сети](./media/connect-on-premises-network/virtual-network-settings.png)

    Оставьте hello другие записи в значение по умолчанию hello, а затем выберите __ОК__ toocontinue.

5. Из hello __покупки__ раздел, выберите hello __покупки__ кнопку toocreate hello виртуальной машины.

6. После создания виртуальной машины hello его __Обзор__ отображается раздел. Выберите из списка hello слева hello __свойства__. Сохранить hello __общедоступный IP-адрес__ и __частный IP-адрес__ значения. Он будет использоваться в следующем разделе hello.

    ![Общедоступные и частные IP-адреса](./media/connect-on-premises-network/vm-ip-addresses.png)

### <a name="install-and-configure-bind-dns-software"></a>Установка и настройка Bind (программное обеспечение DNS)

1. Использовать SSH tooconnect toohello __общедоступный IP-адрес__ hello виртуальной машины. Следующий пример Hello подключается виртуальная машина tooa 40.68.254.142:

    ```bash
    ssh sshuser@40.68.254.142
    ```

    Замените `sshuser` with hello учетной записи пользователя SSH указан при создании кластера hello.

    > [!NOTE]
    > Существует множество способов tooobtain hello `ssh` программы. В Linux, Unix и macOS предоставляется как часть операционной системы hello. Если вы используете Windows, рассмотрите одну из hello следующие параметры:
    >
    > * [Azure Cloud Shell](../cloud-shell/quickstart.md);
    > * [Bash на платформе Ubuntu в Windows 10](https://msdn.microsoft.com/commandline/wsl/about);
    > * [Git (https://git-scm.com/)](https://git-scm.com/);
    > * [OpenSSH (https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)](https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH).

2. tooinstall Bind, используйте следующие команды из сеанса SSH hello hello:

    ```bash
    sudo apt-get update -y
    sudo apt-get install bind9 -y
    ```

3. tooconfigure привязки tooforward имя разрешения запросов tooyour локального DNS-сервера, используйте hello после текста как содержимое hello hello `/etc/bind/named.conf.options` файла:

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
    > Замените значения hello hello `goodclients` раздел с hello диапазон IP-адресов виртуальной сети hello и локальной сетью. В этом разделе определяет hello адреса, которые этот DNS-сервер принимает запросы от.
    >
    > Замените hello `192.168.0.1` запись в hello `forwarders` раздел с hello IP-адрес локального DNS-сервера. Это tooyour запросы записи DNS маршруты локального DNS-сервера для разрешения.

    tooedit этот файл hello используйте следующую команду:

    ```bash
    sudo nano /etc/bind/named.conf.options
    ```

    toosave hello файла, используйте __Ctrl + X__, __Y__, а затем __ввод__.

4. В сеансе SSH hello используйте hello следующую команду:

    ```bash
    hostname -f
    ```

    Эта команда возвращает аналогичные toohello значение, следующий текст:

        dnsproxy.icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net

    Hello `icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net` — текст hello __DNS-суффикс__ для этой виртуальной сети. Сохраните это значение, так как оно будет использовано позже.

5. tooconfigure привязки tooresolve DNS-имена для ресурсов в пределах hello виртуальной сети, используйте hello после текста как содержимое hello hello `/etc/bind/named.conf.local` файла:

        // Replace hello following with hello DNS suffix for your virtual network
        zone "icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net" {
            type forward;
            forwarders {168.63.129.16;}; # hello Azure recursive resolver
        };

    > [!IMPORTANT]
    > Необходимо заменить hello `icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net` с DNS-суффиксом hello, извлеченного ранее.

    tooedit этот файл hello используйте следующую команду:

    ```bash
    sudo nano /etc/bind/named.conf.local
    ```

    toosave hello файла, используйте __Ctrl + X__, __Y__, а затем __ввод__.

6. toostart привязки hello используйте следующую команду:

    ```bash
    sudo service bind9 restart
    ```

7. tooverify, к которой привязана может разрешать имена hello ресурсам в локальной сети, hello используйте следующие команды:

    ```bash
    sudo apt install dnsutils
    nslookup dns.mynetwork.net 10.0.0.4
    ```

    > [!IMPORTANT]
    > Замените `dns.mynetwork.net` с hello полное доменное имя (FQDN) ресурса в локальной сети.
    >
    > Замените `10.0.0.4` с hello __внутренний IP-адрес__ пользовательские DNS-сервера в виртуальной сети hello.

    Появится ответ Hello аналогичные toohello следующий текст:

        Server:         10.0.0.4
        Address:        10.0.0.4#53

        Non-authoritative answer:
        Name:   dns.mynetwork.net
        Address: 192.168.0.4

### <a name="configure-hello-virtual-network-toouse-hello-custom-dns-server"></a>Настройка hello виртуальной сети toouse hello пользовательского DNS-сервера

tooconfigure hello виртуальной сети toouse hello пользовательские DNS-сервер вместо hello Azure рекурсивного сопоставителя, использовать hello следующие шаги:

1. В hello [портал Azure](https://portal.azure.com), выберите hello виртуальной сети, а затем выберите __DNS-серверы__.

2. Выберите __пользовательские__и введите hello __внутренний IP-адрес__ hello пользовательские DNS-сервера. Наконец, щелкните __Сохранить__.

    ![Набор hello пользовательского DNS-сервера для сети hello](./media/connect-on-premises-network/configure-custom-dns.png)

### <a name="configure-hello-on-premises-dns-server"></a>Настройка hello локального DNS-сервера

В предыдущем разделе hello вы настроили hello пользовательского DNS server tooforward запросов toohello локального DNS-сервера. Далее необходимо настроить hello локальных DNS server tooforward запросов toohello пользовательского DNS-сервера.

Конкретные действия по tooconfigure DNS-сервере, см. в документации hello для программного обеспечения сервера DNS. Поиск hello инструкций о том, как tooconfigure __условной пересылки__.

Сервер условной пересылки только переадресовывает запросы по определенным DNS-суффиксам. В этом случае необходимо настроить пересылки DNS-суффикс hello hello виртуальной сети. IP-адрес toohello hello пользовательского DNS-сервера следует перенаправить запросы для этого суффикса. 

Hello следующий текст является примером конфигурацию условной пересылки для hello **привязки** программное обеспечение DNS:

    zone "icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net" {
        type forward;
        forwarders {10.0.0.4;}; # hello custom DNS server's internal IP address
    };

Дополнительные сведения об использовании DNS на **Windows Server 2016**, разделе hello [DnsServerConditionalForwarderZone добавить](https://technet.microsoft.com/itpro/powershell/windows/dnsserver/add-dnsserverconditionalforwarderzone) документации...

Настроив hello локального DNS-сервера, можно использовать `nslookup` hello в локальной сети tooverify, может разрешать имена в виртуальной сети hello. Следующий пример Hello 

```bash
nslookup dnsproxy.icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net 196.168.0.4
```

В этом примере локальный DNS-сервер на 196.168.0.4 hello использует имя hello tooresolve hello пользовательского DNS-сервера. Замените hello IP-адрес hello, один для hello локального DNS-сервера. Замените hello `dnsproxy` адрес с hello полное доменное имя DNS-сервера, настраиваемые приветствия.

## <a name="optional-control-network-traffic"></a>Управление сетевым трафиком (необязательно)

Можно использовать группы безопасности сети (NSG) или определяемых пользователем маршрутов (UDR) toocontrol сетевого трафика. Группы Nsg позволяют toofilter входящий и исходящий трафик и разрешить или запретить трафик hello. UDRs позволяют toocontrol потоки трафика между ресурсами в виртуальной сети hello и hello Интернет hello в локальной сети.

> [!WARNING]
> Для HDInsight требуется входящий доступ с определенных IP-адресов в облако Azure hello и исходящий неограниченный доступ. При использовании Nsg или UDRs toocontrol трафика, необходимо выполнить следующие шаги hello:
>
> 1. Найти hello IP-адресов для hello расположение, которое содержит виртуальной сети. Список требуемых IP-адресов по расположениям см. в [этом разделе](./hdinsight-extend-hadoop-virtual-network.md#hdinsight-ip).
>
> 2. Разрешать входящий трафик от hello IP-адресов.
>
>    * __NSG__: Разрешить __входящий__ трафик через порт __443__ из hello __Internet__.
>    * __UDR__: hello набор __следующего прыжка__ тип too__Internet__ hello маршрута.

Пример использования Azure PowerShell или Azure CLI hello toocreate Nsg см. в разделе hello [расширить HDInsight с виртуальными сетями Azure](./hdinsight-extend-hadoop-virtual-network.md#hdinsight-nsg) документа.

## <a name="create-hello-hdinsight-cluster"></a>Создание кластера HDInsight hello

> [!WARNING]
> Hello пользовательского DNS-сервера необходимо настроить перед установкой HDInsight в виртуальной сети hello.

Используйте hello шагов в hello [создание кластера HDInsight с помощью портала Azure hello](./hdinsight-hadoop-create-linux-clusters-portal.md) toocreate документ кластера HDInsight.

> [!WARNING]
> * Во время создания кластера необходимо выбрать расположение hello, которое содержит виртуальной сети.
>
> * В hello __Дополнительные параметры__ часть конфигурации, необходимо выбрать hello виртуальной сети и подсети, созданной ранее.

## <a name="connecting-toohdinsight"></a>Подключение tooHDInsight

Большая часть документации по HDInsight предполагается, что кластер toohello доступ через hello Интернета. Например, возможность подключения кластера toohello в https://CLUSTERNAME.azurehdinsight.net. Этот адрес используется hello открытый шлюз, который недоступен, если вы использовали Nsg или Здравствуйте, UDRs toorestrict доступ из Интернета.

toodirectly подключение tooHDInsight через hello виртуальную сеть, использовать hello следующие шаги:

1. toodiscover hello внутренней полные доменные имена узлов кластера HDInsight hello, используйте один из следующих методов hello:

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

2. toodetermine hello доступный порт, службы, в разделе hello [порты, используемые службами Hadoop в HDInsight](./hdinsight-hadoop-port-settings-for-services.md) документа.

    > [!IMPORTANT]
    > Некоторые службы, размещенной на hello головного узла активны только на одном узле одновременно. При попытке доступа к службе на один головной узел и происходит сбой, переключитесь toohello других головного узла.
    >
    > Например, Ambari одновременно активен только на одном головном узле. Если при доступе к Ambari на один головной узел, он возвращает ошибку 404, то она работает на hello других головного узла.

## <a name="next-steps"></a>Дальнейшие действия

* Дополнительные сведения об использовании HDInsight в виртуальной сети см. в статье [Расширение возможностей HDInsight с помощью виртуальной сети Azure](./hdinsight-extend-hadoop-virtual-network.md).

* Дополнительные сведения о виртуальных сетях Azure см. в разделе hello [Обзор виртуальной сети Azure](../virtual-network/virtual-networks-overview.md).

* Дополнительные сведения о группах безопасности сети см. в статье [Фильтрация сетевого трафика с помощью групп безопасности сети](../virtual-network/virtual-networks-nsg.md).

* Дополнительные сведения о пользовательских маршрутах см. в статье [Определяемые пользователем маршруты и IP-пересылка](../virtual-network/virtual-networks-udr-overview.md).
