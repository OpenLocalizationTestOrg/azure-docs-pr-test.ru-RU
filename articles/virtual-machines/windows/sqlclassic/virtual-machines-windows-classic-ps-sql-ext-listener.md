---
title: "aaaConfigure внешний прослушиватель для группы доступности Always On | Документы Microsoft"
description: "В этом учебника последовательно, можно выполнить с помощью действия по созданию всегда на прослушиватель группы доступности в Azure, доступном с использованием hello общедоступный виртуальный IP-адрес hello связанной облачной службой."
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: a2453032-94ab-4775-b976-c74d24716728
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/31/2017
ms.author: mikeray
ms.openlocfilehash: f8e2110bcc25d9cb7653675cb4ae5c8d717b6902
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-external-listener-for-always-on-availability-groups-in-azure"></a>Настройка внешнего прослушивателя для групп доступности AlwaysOn в Azure
> [!div class="op_single_selector"]
> * [Внутренний прослушиватель](../classic/ps-sql-int-listener.md)
> * [Внешний прослушиватель](../classic/ps-sql-ext-listener.md)
> 
> 

В этом разделе рассказывается, как tooconfigure прослушиватель для группы доступности AlwaysOn, доступном на hello Интернета. Это стало возможным, связав hello облачной службы **открытый виртуальный IP-адресов (VIP)** адрес прослушивателя hello.

> [!IMPORTANT] 
> В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../../../azure-resource-manager/resource-manager-deployment-model.md). В этой статье описан с помощью hello классической модели развертывания. Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов.

В группе доступности могут быть реплики, доступные только локально или только в Azure. В гибридных конфигурациях возможны оба способа доступа одновременно. Реплики в Azure может находиться в пределах hello же регионе или в нескольких регионах с помощью нескольких виртуальных сетей (Vnet). Hello ниже предполагается, что у вас уже есть [группа доступности настроена](../classic/portal-sql-alwayson-availability-groups.md) , но не настроили прослушиватель.

## <a name="guidelines-and-limitations-for-external-listeners"></a>Рекомендации и ограничения для внешних прослушивателей
Обратите внимание, hello следующие рекомендации о hello прослушивателя группы доступности в Azure, при развертывании с помощью hello облачной службы pubic виртуальный IP-адрес:

* прослушиватель группы доступности Hello поддерживается на Windows Server 2008 R2, Windows Server 2012 и Windows Server 2012 R2.
* Hello клиентское приложение должно находиться в облачной службе, отличной hello, которая содержит ВМ группы доступности. Azure не поддерживает прямой сервера возвращаются с клиентом и сервером в hello же облачной службе.
* По умолчанию hello шаги в этой статье показывают, как hello toouse один прослушиватель tooconfigure облако адрес виртуального IP-адресов (VIP) службы. Тем не менее возможно tooreserve и создать несколько виртуальных IP-адресов для облачной службы. Это позволяет toouse hello шаги в этой статье toocreate, несколько прослушивателей, которые они имеют связанные с разных виртуальных IP-адресов. Сведения о toocreate несколько виртуальных IP-адресов. в статье [несколько виртуальных IP-адресов в облачной службе](../../../load-balancer/load-balancer-multivip.md).
* При создании прослушиватель в гибридной среде hello в локальной сети должен иметь toohello подключения общедоступный Интернет в toohello сложения через виртуальную Частную сеть сеть с hello виртуальной сети Azure. В случае hello подсети Azure, hello прослушивателя группы доступности можно подключиться только по hello общедоступный IP-адрес hello соответствующей облачной службы.
* Не поддерживается toocreate внешний прослушиватель в hello же облачной службе, где также имеется внутренний прослушиватель, используя hello внутренняя Подсистема балансировки нагрузки (ILB).

## <a name="determine-hello-accessibility-of-hello-listener"></a>Определить доступность hello hello прослушивателя
[!INCLUDE [ag-listener-accessibility](../../../../includes/virtual-machines-ag-listener-determine-accessibility.md)]

В этой статье рассматривается создание прослушивателя, использующего **внешнюю балансировку нагрузки**. Если требуется, чтобы прослушиватель, который является tooyour частной виртуальной сети, см. hello в этой статье, пошаговые инструкции по настройке [прослушиватель с ILB](../classic/ps-sql-int-listener.md)

## <a name="create-load-balanced-vm-endpoints-with-direct-server-return"></a>Создание конечных точек балансировки нагрузки в ВМ со службой Direct Server Return
Балансировка нагрузки использует hello hello виртуальный открытый виртуальный IP-адрес hello облачной службы, на котором размещены виртуальные машины. Поэтому не требуется toocreate и в этом случае Настройка балансировки нагрузки hello.

Для каждой виртуальной машины с репликой Azure необходимо создать конечную точку с балансировкой нагрузки. Если у вас есть реплики в нескольких регионах, каждая реплика для этого региона должна быть в hello же облачную службу в hello одной виртуальной сети. Чтобы создать реплики группы доступности, охватывающие несколько регионов Azure, необходимо настроить несколько виртуальных сетей. Дополнительные сведения о настройке подключения между VNet см. в разделе [tooVNet виртуальной сети, настройте подключение](../../../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md).

1. В hello портал Azure перейдите tooeach размещение реплики и просмотрите сведения о hello виртуальной Машины.
2. Нажмите кнопку hello **конечные точки** для каждой из виртуальных машин hello.
3. Убедитесь, что hello **имя** и **общий порт** конечная точка прослушивателя hello нужно toouse уже не используется. В следующем примере hello hello имя «MyEndpoint» а hello порт «1433».
4. На локальном клиенте Загрузите и установите [hello последнюю версию модуля PowerShell](https://azure.microsoft.com/downloads/).
5. Запустите **Azure PowerShell**. Новый PowerShell, открытия сеанса с hello загруженными административными модулями Azure.
6. Выполните командлет **Get-AzurePublishSettingsFile**. Этот командлет перенаправит браузер tooa toodownload публикации параметров файла tooa локальный каталог. Может потребоваться ввод учетных данных подписки Azure.
7. Запустите hello **команду Import-AzurePublishSettingsFile** загруженный файл настроек публикации командой hello путь hello:
   
        Import-AzurePublishSettingsFile -PublishSettingsFile <PublishSettingsFilePath>
   
    После публикации hello импорта файла параметров, можно управлять подпиской Azure в сеансе PowerShell hello.
    
1. Скопируйте ниже сценарий PowerShell hello в текстовый редактор и задайте toosuit hello значения переменных среды (по умолчанию были предоставлены для некоторых параметров). Обратите внимание, что если группа доступности охватывает регионы Azure, необходимо выполнить скрипт hello один раз в каждом центре обработки данных для hello облачной службы и узлы, находящиеся в этом центре обработки данных.
   
        # Define variables
        $ServiceName = "<MyCloudService>" # hello name of hello cloud service that contains hello availability group nodes
        $AGNodes = "<VM1>","<VM2>","<VM3>" # all availability group nodes containing replicas in hello same cloud service, separated by commas
   
        # Configure a load balanced endpoint for each node in $AGNodes, with direct server return enabled
        ForEach ($node in $AGNodes)
        {
            Get-AzureVM -ServiceName $ServiceName -Name $node | Add-AzureEndpoint -Name "ListenerEndpoint" -Protocol "TCP" -PublicPort 1433 -LocalPort 1433 -LBSetName "ListenerEndpointLB" -ProbePort 59999 -ProbeProtocol "TCP" -DirectServerReturn $true | Update-AzureVM
        }

2. После задания переменных hello hello Копировать сценарий из hello текстового редактора в вашей toorun сеанс Azure PowerShell его. Если появится запрос hello >>, ввод снова начать выполнение toomake убедиться, что hello скрипта.

## <a name="verify-that-kb2854082-is-installed-if-necessary"></a>Проверка наличия пакета KB2854082
[!INCLUDE [kb2854082](../../../../includes/virtual-machines-ag-listener-kb2854082.md)]

## <a name="open-hello-firewall-ports-in-availability-group-nodes"></a>Открыть порты брандмауэра hello в узлах группы доступности
[!INCLUDE [firewall](../../../../includes/virtual-machines-ag-listener-open-firewall.md)]

## <a name="create-hello-availability-group-listener"></a>Создание прослушивателя группы доступности hello

Создание прослушивателя группы доступности hello в два этапа. Во-первых создайте ресурс кластера точки доступа клиента hello и настроить зависимости. Во-вторых настройте hello ресурсов кластера с помощью PowerShell.

### <a name="create-hello-client-access-point-and-configure-hello-cluster-dependencies"></a>Создать точку доступа клиента hello и настроить зависимости кластера hello
[!INCLUDE [firewall](../../../../includes/virtual-machines-ag-listener-create-listener.md)]

### <a name="configure-hello-cluster-resources-in-powershell"></a>Настройка ресурсов кластера hello в PowerShell
1. Для балансировки нагрузки, необходимо получить hello общедоступный виртуальный IP-адрес hello облачной службы, содержащей реплики. Войдите на hello портал Azure. Перейдите toohello облачная служба, которая содержит ВМ группы доступности. Откройте hello **мониторинга** представления.
2. Запишите адрес hello, показанный в разделе **открытый виртуальный IP-адресов (VIP) адрес**. Если ваше решение располагается в нескольких виртуальных сетях, повторите этот шаг для каждой облачной службы с виртуальной машиной, на которой размещается реплика.
3. На одном из hello виртуальные машины скопируйте hello ниже сценарий PowerShell в текстовый редактор и задайте переменные hello toohello значения, записанные ранее.
   
        # Define variables
        $ClusterNetworkName = "<ClusterNetworkName>" # hello cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name)
        $IPResourceName = "<IPResourceName>" # hello IP Address resource name
        $CloudServiceIP = "<X.X.X.X>" # Public Virtual IP (VIP) address of your cloud service
   
        Import-Module FailoverClusters
   
        # If you are using Windows Server 2012 or higher, use hello Get-Cluster Resource command. If you are using Windows Server 2008 R2, use hello cluster res command. Both commands are commented out. Choose hello one applicable tooyour environment and remove hello # at hello beginning of hello line tooconvert hello comment tooan executable line of code.
   
        # Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$CloudServiceIP";"ProbePort"="59999";"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"OverrideAddressMatch"=1;"EnableDhcp"=0}
        # cluster res $IPResourceName /priv enabledhcp=0 overrideaddressmatch=1 address=$CloudServiceIP probeport=59999  subnetmask=255.255.255.255
4. Один раз вы задали hello переменные, откройте окно Windows PowerShell с повышенными привилегиями, а затем скопируйте hello скрипт из текстового редактора hello и вставьте в вашей toorun сеанс Azure PowerShell его. Если появится запрос hello >>, ввод снова начать выполнение toomake убедиться, что hello скрипта.
5. Повторите эти действия на каждой виртуальной машине. Этот скрипт настраивает ресурс IP-адреса hello с IP-адресом hello hello облачной службы и устанавливает прочие параметры, такие как порт пробы hello. При подключении hello ресурс IP-адреса, он может отвечать toohello опрос на порту пробы hello из hello балансировкой нагрузки конечной точки, созданной ранее в этом учебнике.

## <a name="bring-hello-listener-online"></a>Перевод прослушивателя hello в интерактивном режиме
[!INCLUDE [Bring-Listener-Online](../../../../includes/virtual-machines-ag-listener-bring-online.md)]

## <a name="follow-up-items"></a>Дальнейшие действия
[!INCLUDE [Follow-up](../../../../includes/virtual-machines-ag-listener-follow-up.md)]

## <a name="test-hello-availability-group-listener-within-hello-same-vnet"></a>Прослушиватель группы доступности hello теста (в пределах hello же виртуальной сети)
[!INCLUDE [Test-Listener-Within-VNET](../../../../includes/virtual-machines-ag-listener-test.md)]

## <a name="test-hello-availability-group-listener-over-hello-internet"></a>Прослушиватель группы доступности hello теста (через hello Интернет)
В прослушивателе hello tooaccess заказа из внешней hello виртуальной сети, необходимо использовать балансировку нагрузки внешние/public (как описано в этом разделе) вместо ILB, являющийся доступными только в пределах hello одной виртуальной сети. В строке подключения hello укажите имя облачной службы hello. Например, если имеется облачная служба с именем hello *mycloudservice*, инструкция sqlcmd hello будет выглядеть следующим образом:

    sqlcmd -S "mycloudservice.cloudapp.net,<EndpointPort>" -d "<DatabaseName>" -U "<LoginId>" -P "<Password>"  -Q "select @@servername, db_name()" -l 15

В отличие от предыдущего примера hello, необходимо использовать проверку подлинности SQL, поскольку hello вызывающий объект не может использовать проверку подлинности windows через hello Интернета. Дополнительные сведения см. в публикации блога [AlwaysOn Availability Group in Windows Azure VM: Client Connectivity Scenarios](http://blogs.msdn.com/b/sqlcat/archive/2014/02/03/alwayson-availability-group-in-windows-azure-vm-client-connectivity-scenarios.aspx) (Группы доступности AlwaysOn на виртуальной машине Azure: сценарии клиентских подключений). При использовании проверки подлинности SQL, убедитесь, что создается hello одинаковые учетные данные входа на обоих репликах. Дополнительные сведения об устранении неполадок входа с группами доступности см. в разделе [как имена входа toomap или используйте содержится SQL пользователя tooconnect tooother реплик базы данных и базы данных tooavailability сопоставлений](http://blogs.msdn.com/b/alwaysonpro/archive/2014/02/19/how-to-map-logins-or-use-contained-sql-database-user-to-connect-to-other-replicas-and-map-to-availability-databases.aspx).

Если hello Always On реплики находятся в разных подсетях, клиенты должны задавать **MultisubnetFailover = True** в строке подключения hello. Это приводит к tooreplicas попытки параллельных подключений в разных подсетях hello. Обратите внимание, что этот сценарий включает развертывание межрегиональной группы доступности AlwaysOn.

## <a name="next-steps"></a>Дальнейшие действия
[!INCLUDE [Listener-Next-Steps](../../../../includes/virtual-machines-ag-listener-next-steps.md)]

