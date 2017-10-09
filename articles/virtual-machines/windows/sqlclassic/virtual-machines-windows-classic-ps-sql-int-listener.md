---
title: "aaaConfigure ILB прослушивателя для групп доступности AlwaysOn в Azure | Документы Microsoft"
description: "В этом учебнике используются ресурсы, созданные с помощью hello классической модели развертывания, и создает всегда на прослушиватель группы доступности в Azure, которая использует внутренний балансировщик нагрузки."
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 291288a0-740b-4cfa-af62-053218beba77
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/02/2017
ms.author: mikeray
ms.openlocfilehash: 2ce9b64fea491c945b58f7641e41fd39d90b078a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-ilb-listener-for-always-on-availability-groups-in-azure"></a>Настройка прослушивателя внутреннего балансировщика нагрузки для групп доступности AlwaysOn в Azure
> [!div class="op_single_selector"]
> * [Внутренний прослушиватель](../classic/ps-sql-int-listener.md)
> * [Внешний прослушиватель](../classic/ps-sql-ext-listener.md)
>
>

## <a name="overview"></a>Обзор

> [!IMPORTANT]
> В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель Azure Resource Manager и классическая модель](../../../azure-resource-manager/resource-manager-deployment-model.md). В этой статье описывается использование hello hello классической модели развертывания. Корпорация Майкрософт рекомендует наиболее новые развертывания для использования модели hello диспетчера ресурсов.

tooconfigure прослушивателя для группы доступности Always On, в модели hello диспетчера ресурсов, в разделе [настройки балансировки нагрузки для группы доступности AlwaysOn в Azure](../sql/virtual-machines-windows-portal-sql-alwayson-int-listener.md).

В группе доступности могут быть реплики, доступные только локально или только в Azure. В гибридных конфигурациях возможны оба способа доступа одновременно. Реплики в Azure может находиться в пределах hello же регионе или в нескольких регионах, использующие несколько виртуальных сетей. Hello процедуры, описанные в этой статье предполагается, что вы уже [группа доступности настроена](../classic/portal-sql-alwayson-availability-groups.md) , но еще не настроен прослушиватель.

## <a name="guidelines-and-limitations-for-internal-listeners"></a>Рекомендации и ограничения для внутренних прослушивателей
Hello внутренней подсистемы балансировки нагрузки (ILB) с прослушивателем группы доступности в Azure используется тема toohello рекомендаций:

* прослушиватель группы доступности Hello поддерживается на Windows Server 2008 R2, Windows Server 2012 и Windows Server 2012 R2.
* Только один прослушиватель группы доступности внутренней поддерживается для каждой облачной службы, так как прослушиватель hello настроен toohello ILB, а имеется только один ILB для каждой облачной службы. Однако это возможно toocreate несколько внешних прослушивателей. Дополнительные сведения см. в статье [Настройка внешнего прослушивателя для групп доступности AlwaysOn в Azure](../classic/ps-sql-ext-listener.md).

## <a name="determine-hello-accessibility-of-hello-listener"></a>Определить доступность hello hello прослушивателя
[!INCLUDE [ag-listener-accessibility](../../../../includes/virtual-machines-ag-listener-determine-accessibility.md)]

В этой статье рассматривается создание прослушивателя, использующего внутренний балансировщик нагрузки. Если вам требуется прослушивателя открытого или внешними, см. hello в этой статье, посвященной параметр вверх [внешний прослушиватель](../classic/ps-sql-ext-listener.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

## <a name="create-load-balanced-vm-endpoints-with-direct-server-return"></a>Создание конечных точек балансировки нагрузки в ВМ со службой Direct Server Return
Сначала создать ILB, запустив сценарий hello позже в этом разделе.

Создайте конечную точку с балансировкой нагрузки для каждой виртуальной машины с репликой Azure. Если у вас есть реплики в нескольких регионах, каждая реплика для этого региона должна быть в hello же облачную службу в hello же виртуальной сети Azure. Чтобы создать реплики группы доступности, охватывающие несколько регионов Azure, необходимо настроить несколько виртуальных сетей. Дополнительные сведения о настройке кросс-подключения к виртуальной сети см. в разделе [настройки сетевых подключений виртуальной сети toovirtual](../../../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md).

1. В hello портал Azure перейдите tooeach виртуальной Машины, на котором размещена подробные сведения о реплике tooview hello.

2. Нажмите кнопку hello **конечные точки** вкладки для каждой виртуальной Машины.

3. Убедитесь, что hello **имя** и **общий порт** hello прослушиватель конечной точки требуется toouse уже не используются. В примере hello в этом разделе, имеет имя hello *MyEndpoint*, а порт hello *1433*.

4. На локальном клиенте Загрузите и установите hello последней [модуль PowerShell](https://azure.microsoft.com/downloads/).

5. Запустите Azure PowerShell.  
    Открывает новый сеанс PowerShell с hello Azure загруженными административными модулями.

6. Запустите `Get-AzurePublishSettingsFile`. Этот командлет перенаправит браузер tooa toodownload публикации параметров файла tooa локальный каталог. Может потребоваться ввод учетных данных для входа в подписку Azure.

7. Запустите следующие hello `Import-AzurePublishSettingsFile` загруженный файл настроек публикации командой hello путь hello:

        Import-AzurePublishSettingsFile -PublishSettingsFile <PublishSettingsFilePath>

    После публикации hello импорта файла параметров, можно управлять подпиской Azure в сеансе PowerShell hello.

8. Для *балансировщика нагрузки* вам потребуется назначить статический IP-адрес. Проверьте текущую конфигурацию виртуальной сети hello, выполнив следующую команду hello:

        (Get-AzureVNetConfig).XMLConfiguration
9. Примечание hello *подсети* имя для подсети hello, содержащей hello ВМ, на которых размещены реплики hello. Это имя используется в параметре hello $SubnetName в скрипте hello.

10. Примечание hello *VirtualNetworkSite* имя и hello начиная *AddressPrefix* для hello подсети, содержащей hello ВМ, на которых размещены реплики hello. Найдите доступные IP-адреса, передав оба значения toohello `Test-AzureStaticVNetIP` команду и просмотрев hello *AvailableAddresses*. Например, если hello виртуальной сети называется *MyVNet* и имеет диапазон адресов подсети, который начинается с позиции *172.16.0.128*, hello следующая команда, будет выведен список доступных адресов:

        (Test-AzureStaticVNetIP -VNetName "MyVNet"-IPAddress 172.16.0.128).AvailableAddresses
11. Выберите один из доступных адресов hello и использовать его в параметре hello $ILBStaticIP hello скрипт на следующем шаге hello.

12. Скопируйте hello, следуя PowerShell скрипт tooa текстовый редактор и задайте toosuit hello значения переменных среды. Для некоторых параметров указаны значения по умолчанию.  

    Вы не сможете добавить внутренний балансировщик нагрузки к имеющимся развернутым службам, использующим территориальные группы. Дополнительные сведения о требованиях внутреннего балансировщика нагрузки см. в статье [Обзор внутренней подсистемы балансировки нагрузки](../../../load-balancer/load-balancer-internal-overview.md).

    Кроме того Если группа доступности охватывает регионы Azure, необходимо запустить скрипт hello один раз в каждом центре обработки данных для hello облачной службы и узлы, находящиеся в этом центре обработки данных.

        # Define variables
        $ServiceName = "<MyCloudService>" # hello name of hello cloud service that contains hello availability group nodes
        $AGNodes = "<VM1>","<VM2>","<VM3>" # all availability group nodes containing replicas in hello same cloud service, separated by commas
        $SubnetName = "<MySubnetName>" # subnet name that hello replicas use in hello virtual network
        $ILBStaticIP = "<MyILBStaticIPAddress>" # static IP address for hello ILB in hello subnet
        $ILBName = "AGListenerLB" # customize hello ILB name or use this default value

        # Create hello ILB
        Add-AzureInternalLoadBalancer -InternalLoadBalancerName $ILBName -SubnetName $SubnetName -ServiceName $ServiceName -StaticVNetIPAddress $ILBStaticIP

        # Configure a load-balanced endpoint for each node in $AGNodes by using ILB
        ForEach ($node in $AGNodes)
        {
            Get-AzureVM -ServiceName $ServiceName -Name $node | Add-AzureEndpoint -Name "ListenerEndpoint" -LBSetName "ListenerEndpointLB" -Protocol tcp -LocalPort 1433 -PublicPort 1433 -ProbePort 59999 -ProbeProtocol tcp -ProbeIntervalInSeconds 10 -InternalLoadBalancerName $ILBName -DirectServerReturn $true | Update-AzureVM
        }

13. После установки переменных hello hello Копировать сценарий из сеанса hello текстового редактора tooyour PowerShell toorun его. Если появится запрос hello  **>>** , нажмите клавишу ВВОД еще раз убедиться, что скрипт hello toomake запуска.

## <a name="verify-that-kb2854082-is-installed-if-necessary"></a>Проверка наличия пакета KB2854082
[!INCLUDE [kb2854082](../../../../includes/virtual-machines-ag-listener-kb2854082.md)]

## <a name="open-hello-firewall-ports-in-availability-group-nodes"></a>Открыть порты брандмауэра hello в узлах группы доступности
[!INCLUDE [firewall](../../../../includes/virtual-machines-ag-listener-open-firewall.md)]

## <a name="create-hello-availability-group-listener"></a>Создание прослушивателя группы доступности hello

Создание прослушивателя группы доступности hello в два этапа. Во-первых создайте ресурс кластера точки доступа клиента hello и настроить зависимости. Во-вторых настройте ресурсы кластера hello в PowerShell.

### <a name="create-hello-client-access-point-and-configure-hello-cluster-dependencies"></a>Создать точку доступа клиента hello и настроить зависимости кластера hello
[!INCLUDE [firewall](../../../../includes/virtual-machines-ag-listener-create-listener.md)]

### <a name="configure-hello-cluster-resources-in-powershell"></a>Настройка ресурсов кластера hello в PowerShell
1. Для ILB необходимо использовать IP-адрес hello hello ILB, который был создан ранее. tooobtain этот IP-адрес в PowerShell hello используйте следующий сценарий:

        # Define variables
        $ServiceName="<MyServiceName>" # hello name of hello cloud service that contains hello AG nodes
        (Get-AzureInternalLoadBalancer -ServiceName $ServiceName).IPAddress

2. На одном из hello виртуальные машины скопируйте сценарий PowerShell hello для текстового редактора tooa операционной системы и установка переменных hello toohello записанные ранее значения.

    Для Windows Server 2012 или более поздней версии используйте следующий сценарий hello:

        # Define variables
        $ClusterNetworkName = "<MyClusterNetworkName>" # hello cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name)
        $IPResourceName = "<IPResourceName>" # hello IP address resource name
        $ILBIP = “<X.X.X.X>” # hello IP address of hello ILB

        Import-Module FailoverClusters

        Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"="59999";"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}

    Для Windows Server 2008 R2 используйте следующий сценарий hello:

        # Define variables
        $ClusterNetworkName = "<MyClusterNetworkName>" # hello cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name)
        $IPResourceName = "<IPResourceName>" # hello IP address resource name
        $ILBIP = “<X.X.X.X>” # hello IP address of hello ILB

        Import-Module FailoverClusters

        cluster res $IPResourceName /priv enabledhcp=0 address=$ILBIP probeport=59999  subnetmask=255.255.255.255

3. После того как вы hello заданные переменные, откройте окно Windows PowerShell с повышенными привилегиями, вставить hello сценарий из hello текстового редактора в вашей toorun сеанса PowerShell его. Если появится запрос hello  **>>** , нажмите клавишу ВВОД еще раз убедиться, что начать выполнение скрипта hello toomake.

4. Повторите hello в предыдущих шагах, для каждой виртуальной Машины.  
    Этот скрипт настраивает ресурс IP-адреса hello с IP-адресом hello hello облачной службы и устанавливает прочие параметры, такие как порт пробы hello. При подключении hello ресурс IP-адреса, он может отвечать toohello опрос на порту пробы hello из hello балансировкой нагрузки конечной точки, созданной ранее.

## <a name="bring-hello-listener-online"></a>Перевод прослушивателя hello в интерактивном режиме
[!INCLUDE [Bring-Listener-Online](../../../../includes/virtual-machines-ag-listener-bring-online.md)]

## <a name="follow-up-items"></a>Дальнейшие действия
[!INCLUDE [Follow-up](../../../../includes/virtual-machines-ag-listener-follow-up.md)]

## <a name="test-hello-availability-group-listener-within-hello-same-virtual-network"></a>Прослушиватель группы доступности hello теста (в пределах hello же виртуальной сети)
[!INCLUDE [Test-Listener-Within-VNET](../../../../includes/virtual-machines-ag-listener-test.md)]

## <a name="next-steps"></a>Дальнейшие действия
[!INCLUDE [Listener-Next-Steps](../../../../includes/virtual-machines-ag-listener-next-steps.md)]
