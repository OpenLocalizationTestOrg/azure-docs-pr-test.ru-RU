---
title: "aaaManage Azure зарезервированные IP-адреса (обычная) — PowerShell | Документы Microsoft"
description: "Понимать зарезервированные IP-адреса (классические) и как toomanage их с помощью PowerShell."
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: 34652a55-3ab8-4c2d-8fb2-43684033b191
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/10/2016
ms.author: jdial
ms.openlocfilehash: c0a77b2ab8b1ab9bef6015c903eb735ea4358a35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="reserved-ip-addresses-classic"></a>Зарезервированные IP-адреса (классическая модель)

> [!div class="op_single_selector"]
> * [Портал Azure](virtual-network-deploy-static-pip-arm-portal.md)
> * [PowerShell](virtual-network-deploy-static-pip-arm-ps.md)
> * [Интерфейс командной строки Azure](virtual-network-deploy-static-pip-arm-cli.md)
> * [Шаблон](virtual-network-deploy-static-pip-arm-template.md)
> * [PowerShell (классическая модель)](virtual-networks-reserved-public-ip.md)

IP-адреса в Azure делятся на две категории: динамические и зарезервированные. Общедоступные IP-адреса, управляемые Azure, являются динамическими по умолчанию. Что означает, что hello IP-адрес используется для данной облачной службы (VIP) или tooaccess виртуальной Машины или изменить непосредственно для экземпляра роли (ILPIP) из tootime времени при останове (освобождении) или завершение работы ресурсов.

tooprevent изменять IP-адреса, можно зарезервировать IP-адрес. Зарезервированные IP-адреса можно использовать только в качестве виртуального IP-адреса, обеспечивая этот hello IP-адрес для облачной службы hello останется hello таким же, даже если ресурсы, завершают работу или остановлена (освобождена). Кроме того можно преобразовать существующие динамические IP-адреса, использовать в качестве виртуального IP-адреса tooa зарезервированные IP-адрес.

> [!IMPORTANT]
> В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель Resource Manager и классическая модель](../azure-resource-manager/resource-manager-deployment-model.md). В этой статье описан с помощью hello классической модели развертывания. Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов. Узнайте, как статический открытый IP адрес с помощью tooreserve hello [модели развертывания диспетчера ресурсов](virtual-network-ip-addresses-overview-arm.md).

toolearn более о IP-адреса в Azure, ознакомьтесь со статьей hello [IP-адреса](virtual-network-ip-addresses-overview-classic.md) статьи.

## <a name="when-do-i-need-a-reserved-ip"></a>Когда требуется зарезервированный IP-адрес?
* **Вы хотите tooensure, hello IP, зарезервированным в подписке**. Если нужно tooreserve IP-адрес, не освобождается из вашей подписки ни при каких обстоятельствах следует использовать зарезервированный общедоступный IP-адрес.  
* **Требуется toostay ваш IP в облачной службе даже через остановлена или освобождена состояние (ВМ)**. Если вы хотите toobe вашей службы, обращаться с помощью IP-адрес, который не изменяется, даже в том случае, если облака виртуальных машин в hello службы завершение работы или остановки (освобождена).
* **Вы хотите tooensure, что исходящий трафик из Azure использует предсказуемого IP-адреса**. Возможно, вашей локальной брандмауэром tooallow трафик только от определенных IP-адресов. Резервируя IP-адреса, вы знаете hello исходный IP-адрес адрес и нет необходимости правила брандмауэра из-за изменения IP tooan tooupdate.

## <a name="faq"></a>Часто задаваемые вопросы
1. Можно ли использовать зарезервированный IP-адрес для всех служб Azure? <br>
    Нет. Зарезервированные IP-адреса можно использовать только для виртуальных машин и экземпляров ролей облачных служб, представляемых через виртуальный IP-адрес.
2. Сколько зарезервированных IP-адресов можно установить? <br>
    Дополнительные сведения см. в разделе hello [Azure ограничивает](../azure-subscription-service-limits.md#networking-limits) статьи.
3. Взимается ли плата за зарезервированные IP-адреса? <br>
    Иногда. Сведения о ценах см. в разделе hello [зарезервированные IP адрес сведения о ценах на](http://go.microsoft.com/fwlink/?LinkID=398482) страницы.
4. Как зарезервировать IP-адрес? <br>
    Можно использовать PowerShell, hello [API REST управления Azure](https://msdn.microsoft.com/library/azure/dn722420.aspx), или hello [портал Azure](https://portal.azure.com) tooreserve IP-адрес в регионе Azure. Зарезервированный IP-адрес — это связанные tooyour подписка.
5. Можно ли использовать зарезервированный IP-адрес с виртуальными сетями на основе территориальной группы? <br>
    Нет. Зарезервированные IP-адреса поддерживаются только в региональных виртуальных сетях. Зарезервированные IP-адреса не поддерживаются для виртуальных сетей, которые связаны с территориальными группами. Дополнительные сведения о связывании виртуальной сети с регион или территориальная группа см. в разделе hello [о региональных виртуальных сетях и территориальных группах](virtual-networks-migrate-to-regional-vnet.md) статьи.

## <a name="manage-reserved-vips"></a>Управление зарезервированными виртуальными IP-адресами

Убедитесь в наличии установлен и настроен PowerShell, выполнив шаги hello в hello [установить и настроить PowerShell](/powershell/azure/overview) статьи. 

Прежде чем использовать зарезервированные IP-адреса, необходимо добавить его tooyour подписки. toocreate зарезервированный IP-адрес из пула hello общедоступных IP-адресов в hello *центральной части США* расположение, запускать hello следующую команду:

```powershell
New-AzureReservedIP –ReservedIPName MyReservedIP –Location "Central US"
```

Обратите внимание, однако, что нельзя указать, какой IP-адрес будет зарезервирован. tooview какие IP-адреса зарезервированы в вашу подписку, запустите следующую команду PowerShell hello и обратите внимание, hello значения для *ReservedIPName* и *адрес*:

```powershell
Get-AzureReservedIP
```

Ожидаемые выходные данные:

    ReservedIPName       : MyReservedIP
    Address              : 23.101.114.211
    Id                   : d73be9dd-db12-4b5e-98c8-bc62e7c42041
    Label                :
    Location             : Central US
    State                : Created
    InUse                : False
    ServiceName          :
    DeploymentName       :
    OperationDescription : Get-AzureReservedIP
    OperationId          : 55e4f245-82e4-9c66-9bd8-273e815ce30a
    OperationStatus      : Succeeded

>[!NOTE]
>При создании зарезервированный IP-адрес с помощью PowerShell, нельзя указать ресурсов группы toocreate hello зарезервированные IP-адрес в. Azure по умолчанию помещает его в группу ресурсов с именем *Default-Networking*. При создании hello зарезервированные IP с помощью hello [портал Azure](http://portal.azure.com), можно указать любой выбрать группу ресурсов. При создании hello зарезервированные IP в группе ресурсов не *сети по умолчанию* тем не менее, при ссылках на hello зарезервированный IP-адрес с командами, таких как `Get-AzureReservedIP` и `Remove-AzureReservedIP`, необходимо сослаться на имя hello *Зарезервированное имя группы ресурсов — ip имя группы*.  Например, если создать зарезервированный IP-адрес с именем *myReservedIP* в группу ресурсов с именем *myResourceGroup*, должно ссылаться имя hello hello зарезервированные IP-адрес как *myResourceGroup группы myReservedIP*.   

После зарезервированные IP-адреса, она остается tooyour связанные подписки, до момента ее удаления. toodelete зарезервированный IP-адрес выполнения hello следующую команду PowerShell:

```powershell
Remove-AzureReservedIP -ReservedIPName "MyReservedIP"
```

## <a name="reserve-hello-ip-address-of-an-existing-cloud-service"></a>Зарезервировать IP-адрес hello существующей облачной службы
Можно зарезервировать IP-адрес hello существующей облачной службы, добавив hello `-ServiceName` параметра. tooreserve hello IP-адрес облачной службы *TestService* в hello *центральной части США* расположение, запустите следующую команду PowerShell hello:

```powershell
New-AzureReservedIP –ReservedIPName MyReservedIP –Location "Central US" -ServiceName TestService
```

## <a name="associate-a-reserved-ip-tooa-new-cloud-service"></a>Связать зарезервированный IP tooa новой облачной службы
Hello следующий скрипт создает новые зарезервированные IP, а затем связывает его tooa новой облачной службы с именем *TestService*.

```powershell
New-AzureReservedIP –ReservedIPName MyReservedIP –Location "Central US"

$image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"}

New-AzureVMConfig -Name TestVM -InstanceSize Small -ImageName $image.ImageName `
| Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
| New-AzureVM -ServiceName TestService -ReservedIPName MyReservedIP -Location "Central US"
```

> [!NOTE]
> При создании зарезервированные toouse IP для облачной службы, вы по-прежнему ссылаться toohello виртуальной Машины с помощью *виртуального IP-адреса:&lt;номер порта >* для входящих сообщений. Резервирование IP-адреса не означает, что toohello виртуальной Машины можно подключаться напрямую. Hello зарезервированный IP-адрес назначается toohello облачной службы, hello, в которой развернута виртуальная машина. Если требуется напрямую tooconnect tooa ВМ по IP-Адресу tooconfigure имеется открытый IP-адрес уровня экземпляра. Открытый IP-адрес уровня экземпляра — это тип общедоступный IP-адрес (называемых ILPIP), назначенный непосредственно tooyour виртуальной Машины. Его нельзя зарезервировать. Дополнительные сведения см. в статье hello [уровня экземпляра открытый IP (ILPIP)](virtual-networks-instance-level-public-ip.md) статьи.
> 

## <a name="remove-a-reserved-ip-from-a-running-deployment"></a>Удаление зарезервированного IP-адреса из работающей развернутой системы
tooremove зарезервированный IP-адрес добавлен tooa новой облачной службы, запустите следующую команду PowerShell hello:

```powershell
Remove-AzureReservedIPAssociation -ReservedIPName MyReservedIP -ServiceName TestService
```

> [!NOTE]
> Удаление зарезервированного IP-адреса из выполняющегося развертывания не удаляет резервирование hello из подписки. Он просто освобождает hello IP toobe используется другим ресурсом в вашей подписке.
> 

## <a name="associate-a-reserved-ip-tooa-running-deployment"></a>Связать зарезервированный tooa IP выполнение развертывания
Hello следующие команды создают облачная служба с именем *TestService2* с новой виртуальной Машины с именем *TestVM2*. Hello существующий зарезервированный IP-адрес с именем *MyReservedIP* имеет связанный toohello облачной службы.

```powershell
$image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"}

New-AzureVMConfig -Name TestVM2 -InstanceSize Small -ImageName $image.ImageName `
| Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
| New-AzureVM -ServiceName TestService2 -Location "Central US"

Set-AzureReservedIPAssociation -ReservedIPName MyReservedIP -ServiceName TestService2
```

## <a name="associate-a-reserved-ip-tooa-cloud-service-by-using-a-service-configuration-file"></a>Связать зарезервированный IP tooa облачной службы с помощью файла конфигурации службы
Также можно связать зарезервированный IP tooa облачной службы с помощью файла конфигурации (CSCFG) службы. Hello следующий образец xml показано как tooconfigure облачной службы toouse зарезервированного виртуального IP-адреса с именем *MyReservedIP*:

    <?xml version="1.0" encoding="utf-8"?>
    <ServiceConfiguration serviceName="ReservedIPSample" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration" osFamily="4" osVersion="*" schemaVersion="2014-01.2.3">
      <Role name="WebRole1">
        <Instances count="1" />
        <ConfigurationSettings>
          <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="UseDevelopmentStorage=true" />
        </ConfigurationSettings>
      </Role>
      <NetworkConfiguration>
        <AddressAssignments>
          <ReservedIPs>
           <ReservedIP name="MyReservedIP"/>
          </ReservedIPs>
        </AddressAssignments>
      </NetworkConfiguration>
    </ServiceConfiguration>

## <a name="next-steps"></a>Дальнейшие действия
* Понять, как [IP-адресация](virtual-network-ip-addresses-overview-classic.md) работает в hello классической модели развертывания.
* Ознакомьтесь с информацией о [зарезервированных частных IP-адресах](virtual-networks-reserved-private-ip.md).
* Ознакомьтесь с информацией об [общедоступных IP-адресах уровня экземпляра (ILPIP)](virtual-networks-instance-level-public-ip.md).

