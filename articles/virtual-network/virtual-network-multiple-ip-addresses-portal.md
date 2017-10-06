---
title: "aaaMultiple IP-адресов для виртуальных машин Azure - портала | Документы Microsoft"
description: "Узнайте, как tooassign несколько IP-адресов tooa виртуальную машину с помощью hello портал Azure | Диспетчер ресурсов."
services: virtual-network
documentationcenter: na
author: anavinahar
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: 3a8cae97-3bed-430d-91b3-274696d91e34
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/30/2016
ms.author: annahar
ms.openlocfilehash: 34075766ac68c8de38c258a4d70e35881f28bb0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="assign-multiple-ip-addresses-toovirtual-machines-using-hello-azure-portal"></a>Присвоить нескольким компьютерам toovirtual адресов IP, используя hello портал Azure

>[!INCLUDE [virtual-network-multiple-ip-addresses-intro.md](../../includes/virtual-network-multiple-ip-addresses-intro.md)]
>
В этой статье объясняется, как toocreate виртуальной машины (VM) с помощью hello Azure Resource Manager развертывания модели с помощью hello портал Azure. Несколько IP-адресов нельзя назначить tooresources, созданные с помощью hello классической модели развертывания. Дополнительные сведения о моделях развертывания Azure, чтение hello toolearn [понять модели развертывания](../resource-manager-deployment-model.md) статьи.

[!INCLUDE [virtual-network-multiple-ip-addresses-template-scenario.md](../../includes/virtual-network-multiple-ip-addresses-scenario.md)]

## <a name = "create"></a>Создание виртуальной машины с несколькими IP-адресами

Если вы хотите toocreate виртуальной Машины с несколькими IP-адресами или статический частный IP-адрес, необходимо создать его с помощью PowerShell или Azure CLI hello. Щелкните hello PowerShell или параметры CLI hello верхней части этой статьи toolearn как. Можно создать виртуальную Машину с одного динамического частный IP-адрес и (необязательно) с помощью портала hello, следуя указаниям hello hello один общий IP-адрес [создания виртуальной Машины Windows](../virtual-machines/virtual-machines-windows-hero-tutorial.md) или [создания виртуальной Машины Linux](../virtual-machines/linux/quick-create-portal.md) статьи. После создания hello виртуальной Машины, можно изменить тип hello IP-адреса из динамического toostatic и добавить дополнительные IP-адреса, с помощью портала hello, выполните шаги в hello [добавить IP-адреса виртуальной Машины tooa](#add) этой статьи.

## <a name="add"></a>Добавьте IP адресов tooa виртуальной Машины

Можно добавить открытые и закрытые tooa адресов IP сетевого Адаптера, выполнив hello, описанных ниже. Hello примеры в следующих разделах hello предполагается, что вы уже виртуальной Машины с hello трех IP-конфигурации, описанной в hello [сценарий](#Scenario) в этой статье, но он не обязательно должен выполнить.

### <a name="coreadd"></a>Основные шаги

1. Обзор toohello портал Azure по адресу https://portal.azure.com и войдите в нее, при необходимости.
2. Hello портале щелкните **дополнительные службы** > тип *виртуальные машины* в hello поля фильтра и нажмите кнопку **виртуальные машины**.
3. В hello **виртуальные машины** колонка, щелкните hello виртуальной Машины требуется tooadd IP-адресов. Нажмите кнопку **сетевых интерфейсов** в колонку hello виртуальной машины, которая появляется и hello, а затем выберите сетевой интерфейс, будет tooadd hello IP-адресов. В примере hello hello следующий рисунок, hello сетевого Адаптера с именем *myNIC* из виртуальной Машины с именем hello *myVM* установлен:

    ![Сетевой интерфейс](./media/virtual-network-multiple-ip-addresses-portal/figure1.png)

4. В hello колонку, которая появится для hello выбранного сетевого Адаптера, нажмите кнопку **IP-конфигурации**.

Hello завершения шагов в одном из последующих разделах hello, исходя из IP-адрес типа hello нужный tooadd.

### <a name="add-a-private-ip-address"></a>**Добавление частного IP-адреса**

Выполните следующие шаги tooadd новый частный IP-адрес hello.

1. Hello завершения шагов в hello [основные шаги](#coreadd) этой статьи.
2. Щелкните **Добавить**. В hello **добавить IP-конфигурации** колонки, отображается, создайте IP-адрес с именем *IPConfig 4* с *10.0.0.7* как *статических* закрытый IP адрес, а затем нажмите кнопку **ОК**.

    > [!NOTE]
    > При добавлении статического IP-адреса, необходимо указать неиспользуемые допустимый адрес на сетевой Адаптер подключен к подсети приветствия hello. Если адрес hello, при выборе недоступен, hello портала будут показаны X для hello IP-адреса и вам потребуется tooselect его.

3. После нажатия кнопки ОК колонке hello закроется, и вы увидите hello в списке Новая конфигурация IP. Нажмите кнопку **ОК** tooclose hello **добавить IP-конфигурации** колонку.
4. Можно щелкнуть **добавить** tooadd дополнительные IP-конфигурации, или закройте все открытые колонках toofinish Добавление IP-адреса.
5. Добавить hello частного IP адресов toohello ВМ операционной системы, выполнив шаги hello для вашей операционной системы в hello [добавить IP-адресов операционной системы виртуальной Машины tooa](#os-config) этой статьи.

### <a name="add-a-public-ip-address"></a>Добавление общедоступного IP-адреса

Общедоступный IP-адрес будет добавлен, связав общих ресурсов tooeither IP-адрес новой конфигурации IP или существующей конфигурации IP.

> [!NOTE]
> За общедоступные IP-адреса взимается номинальная плата. Дополнительные сведения о IP-адресов цен, toolearn чтения hello [цены IP адрес](https://azure.microsoft.com/pricing/details/ip-addresses) страницы. Нет toohello предельное число общих IP-адресов, которые могут использоваться в подписке. Дополнительные об ограничениях hello, чтение hello toolearn [Azure ограничивает](../azure-subscription-service-limits.md#networking-limits) статьи.
> 

### <a name="create-public-ip"></a>Создание ресурса общедоступного IP-адреса

Общедоступный IP-адрес является параметром ресурса частного IP-адреса. При наличии открытого ресурса IP-адреса, не связанную tooan IP-конфигурации, вы должны tooassociate tooan IP-конфигурации, пропустите следующие шаги hello и этапы hello в одном hello следующих разделах, сколько требуется. Если у вас нет доступных общих IP-адрес, выполните следующие шаги toocreate один hello.

1. Обзор toohello портал Azure по адресу https://portal.azure.com и войдите в нее, при необходимости.
3. На портале hello щелкните **New** > **сети** > **общедоступный IP-адрес**.
4. В hello **создать общедоступный IP-адрес** колонки, которое откроется, введите **имя**выберите **назначения IP-адресов** типа, **подписки**, **Группы ресурсов**и **расположение**, нажмите кнопку **создать**, как показано в следующий рисунок hello:

    ![Создание ресурса общедоступного IP-адреса](./media/virtual-network-multiple-ip-addresses-portal/figure5.png)

5. Полный hello шаги в одном из следующих разделах hello tooassociate hello общей конфигурации IP-адреса ресурса tooan IP.

#### <a name="associate-hello-public-ip-address-resource-tooa-new-ip-configuration"></a>Связать hello открытый конфигурацию IP-адреса ресурса tooa новый IP

1. Hello завершения шагов в hello [основные шаги](#coreadd) этой статьи.
2. Щелкните **Добавить**. В hello **добавить IP-конфигурации** колонки, отображается, создайте IP-адрес с именем *IPConfig 4*. Включить hello **общедоступный IP-адрес** и выберите существующий, которые доступны открытый ресурс IP-адреса из hello **выберите общедоступный IP-адрес** колонки, отображается.

    После выбора hello открытого ресурса IP-адреса, нажмите кнопку **ОК** и колонки hello закроется. Если у вас нет существующих общедоступный IP-адрес, можно создать, выполнив шаги hello в hello [создать открытый ресурс IP-адреса](#create-public-ip) этой статьи. 

3. Просмотрите hello новая настройка IP. Несмотря на то, что частный IP-адрес не был явно назначен, один автоматически назначается toohello IP-конфигурации, так как все IP-конфигурации должны иметь частный IP-адрес.
4. Можно щелкнуть **добавить** tooadd дополнительные IP-конфигурации, или закройте все открытые колонках toofinish Добавление IP-адреса.
5. Добавьте hello частного IP адрес toohello операционной системы ВМ, выполнив действия hello для вашей операционной системы в hello [добавить IP-адресов операционной системы виртуальной Машины tooa](#os-config) этой статьи. Не добавляйте hello открытый IP адрес toohello операционной системы.

#### <a name="associate-hello-public-ip-address-resource-tooan-existing-ip-configuration"></a>Связать hello открытый конфигурацию IP-адреса ресурса tooan существующие IP

1. Hello завершения шагов в hello [основные шаги](#coreadd) этой статьи.
2. Щелкните IP-конфигурации hello нужные tooadd hello открытого ресурса IP-адреса для.
3. В колонке IPConfig hello, которое отображается, нажмите кнопку **IP-адрес**.
4. В hello **выберите общедоступный IP-адрес** колонки, отображается, выберите общедоступный IP-адрес.
5. Нажмите кнопку **Сохранить** и колонок hello закроется. Если у вас нет существующих общедоступный IP-адрес, можно создать, выполнив шаги hello в hello [создать открытый ресурс IP-адреса](#create-public-ip) этой статьи.
3. Просмотрите hello новая настройка IP.
4. Можно щелкнуть **добавить** tooadd дополнительные IP-конфигурации, или закройте все открытые колонках toofinish Добавление IP-адреса. Не добавляйте hello открытый IP адрес toohello операционной системы.


[!INCLUDE [virtual-network-multiple-ip-addresses-os-config.md](../../includes/virtual-network-multiple-ip-addresses-os-config.md)]
