---
title: "адреса aaaAzure уровне экземпляра общедоступный IP-адрес (классические) | Документы Microsoft"
description: "Понимать экземпляра уровня общедоступных адресов IP (ILPIP) и как toomanage их с помощью PowerShell."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
ms.assetid: 07eef6ec-7dfe-4c4d-a2c2-be0abfb48ec5
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/10/2016
ms.author: jdial
ms.openlocfilehash: 832143ee6fdd80b634e1cebfddc759a8cacda583
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="instance-level-public-ip-classic-overview"></a>Общие сведения об общедоступных IP-адресах уровня экземпляра (классическая модель развертывания)
Экземпляр уровня открытый IP (ILPIP) — общедоступный IP-адрес, который можно назначить непосредственно tooa экземпляра роли виртуальной Машины или облачные службы, а не toohello облачной службы, в котором экземпляр виртуальной Машины или роли. ILPIP не принимает hello вместо hello виртуальный IP-адрес (VIP), назначенный tooyour облачной службы. Скорее, это дополнительный IP-адрес, что можно использовать tooconnect непосредственно tooyour ВМ или экземпляру роли.

> [!IMPORTANT]
> В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель Resource Manager и классическая модель](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json). В этой статье описан с помощью hello классической модели развертывания. Корпорация Майкрософт рекомендует создавать виртуальные машины с помощью Resource Manager. Убедитесь, что вы понимаете как работают в Azure [IP-адреса](virtual-network-ip-addresses-overview-classic.md) .

![Разница между ILPIP-адресом и виртуальным IP-адресом](./media/virtual-networks-instance-level-public-ip/Figure1.png)

Как показано на рисунке 1 hello облачной службе осуществляется с использованием VIP, при hello отдельные виртуальные машины обычно осуществляется с помощью виртуального IP-адреса:&lt;номер порта&gt;. Назначив tooa ILPIP определенную виртуальную Машину, что виртуальная машина может быть доступ непосредственно с помощью этого IP-адреса.

При создании облачной службы в Azure, соответствующие записи DNS создаются автоматически службы toohello tooallow доступа через полное доменное имя (FQDN), вместо использования hello фактических виртуальных IP-адресов. Hello для ILPIP, позволяя доступа toohello ВМ или экземпляру роли по полному доменному ИМЕНИ вместо hello ILPIP может произойти одного процесса. Для экземпляра при создании облачной службы с именем *contosoadservice*, и настройте веб-роль с именем *contosoweb* с двумя экземплярами hello Azure регистрирует следующие A записей для hello экземпляров:

* contosoweb\_IN_0.contosoadservice.cloudapp.net;
* contosoweb\_IN_1.contosoadservice.cloudapp.net. 

> [!NOTE]
> Каждой виртуальной машине или экземпляру роли можно назначить только один ILPIP-адрес. Воспользуйтесь ILPIPs too5 на подписку. ILPIP-адреса не поддерживаются для виртуальных машин с несколькими сетевыми картами.
> 
> 

## <a name="why-would-i-request-an-ilpip"></a>Зачем запрашивать ILPIP-адрес?
Tooyour может tooconnect toobe виртуальной Машины или экземпляра роли по IP-адреса назначаются напрямую tooit, вместо использования hello облачной службы VIP:&lt;номер порта&gt;, запрос ILPIP для виртуальной Машины или экземпляра роли.

* **Активный режим FTP** -назначая ILPIP tooa виртуальной Машины, она может получать трафик через любой порт. Конечные точки не являются обязательными для hello tooreceive трафика виртуальных Машин.  Дополнительные сведения по протоколу hello FTP. в разделе (https://en.wikipedia.org/wiki/File_Transfer_Protocol#Protocol_overview) [Обзор протокола FTP].
* **Исходящий IP-адрес** - исходящий трафик от ВМ hello сопоставлен toohello ILPIP в качестве источника hello и hello ILPIP однозначно определяет объекты tooexternal hello виртуальной Машины.

> [!NOTE]
> В прошлом hello адрес ILPIP была ссылка tooas общедоступному IP (PIP).
> 

## <a name="manage-an-ilpip-for-a-vm"></a>Управление ILPIP-адресом виртуальной машины
следующие задачи Hello позволяют toocreate, назначение и удаление ILPIPs из виртуальных машин:

### <a name="how-toorequest-an-ilpip-during-vm-creation-using-powershell"></a>Как toorequest ILPIP во время создания виртуальной Машины с помощью PowerShell
Следующий сценарий PowerShell Hello создает облачную службу с именем *FTP-Служба\всего*, извлекает изображение из Azure, создает Виртуальную машину с именем *FTPInstance* с помощью образа hello получить задает hello ВМ toouse ILPIP и добавляет новую службу hello ВМ toohello:

```powershell
New-AzureService -ServiceName FTPService -Location "Central US"

$image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"} `
New-AzureVMConfig -Name FTPInstance -InstanceSize Small -ImageName $image.ImageName `
| Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
| Set-AzurePublicIP -PublicIPName ftpip | New-AzureVM -ServiceName FTPService -Location "Central US"
```

### <a name="how-tooretrieve-ilpip-information-for-a-vm"></a>Как tooretrieve ILPIP сведения для виртуальной Машины
hello tooview ILPIP сведения для hello создания ВМ и для предыдущего сценария hello, запустите следующую команду PowerShell hello и просмотрите значения hello *PublicIPAddress* и *PublicIPName*:

```powershell
Get-AzureVM -Name FTPInstance -ServiceName FTPService
```

Ожидаемые выходные данные:
 
    DeploymentName              : FTPService
    Name                        : FTPInstance
    Label                       : 
    VM                          : Microsoft.WindowsAzure.Commands.ServiceManagement.Model.PersistentVM
    InstanceStatus              : ReadyRole
    IpAddress                   : 100.74.118.91
    InstanceStateDetails        : 
    PowerState                  : Started
    InstanceErrorCode           : 
    InstanceFaultDomain         : 0
    InstanceName                : FTPInstance
    InstanceUpgradeDomain       : 0
    InstanceSize                : Small
    HostName                    : FTPInstance
    AvailabilitySetName         : 
    DNSName                     : http://ftpservice888.cloudapp.net/
    Status                      : ReadyRole
    GuestAgentStatus            :   Microsoft.WindowsAzure.Commands.ServiceManagement.Model.GuestAgentStatus
    ResourceExtensionStatusList : {Microsoft.Compute.BGInfo}
    PublicIPAddress             : 104.43.142.188
    PublicIPName                : ftpip
    NetworkInterfaces           : {}
    ServiceName                 : FTPService
    OperationDescription        : Get-AzureVM
    OperationId                 : 568d88d2be7c98f4bbb875e4d823718e
    OperationStatus             : OK

### <a name="how-tooremove-an-ilpip-from-a-vm"></a>Как tooremove ILPIP из виртуальной Машины
в предыдущий сценарий hello, запустите следующую команду PowerShell hello tooremove hello ILPIP добавлены toohello виртуальной Машины:

```powershell
Get-AzureVM -ServiceName FTPService -Name FTPInstance | Remove-AzurePublicIP | Update-AzureVM
```

### <a name="how-tooadd-an-ilpip-tooan-existing-vm"></a>Как tooadd tooan ILPIP существующей виртуальной Машины
tooadd ILPIP toohello виртуальной Машины, созданной с помощью скрипта hello предыдущей, выполните следующую команду hello:

```powershell
Get-AzureVM -ServiceName FTPService -Name FTPInstance | Set-AzurePublicIP -PublicIPName ftpip2 | Update-AzureVM
```

## <a name="manage-an-ilpip-for-a-cloud-services-role-instance"></a>Управление ILPIP-адресом экземпляра роли облачных служб

tooadd экземпляр роли облачных служб ILPIP tooa завершения hello, следующие шаги:

1. Загрузите файл cscfg hello hello облачную службу, выполнив hello шагов в hello [как tooConfigure облачных служб](../cloud-services/cloud-services-how-to-configure-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json#reconfigure-your-cscfg) статьи.
2. Обновление hello cscfg-файле, добавив hello `InstanceAddress` элемента. Hello следующий пример добавляет ILPIP с именем *MyPublicIP* с именем экземпляра роли tooa *WebRole1*: 

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <ServiceConfiguration serviceName="ILPIPSample" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration" osFamily="4" osVersion="*" schemaVersion="2014-01.2.3">
      <Role name="WebRole1">
        <Instances count="1" />
          <ConfigurationSettings>
        <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="UseDevelopmentStorage=true" />
          </ConfigurationSettings>
      </Role>
      <NetworkConfiguration>
        <AddressAssignments>
          <InstanceAddress roleName="WebRole1">
        <PublicIPs>
          <PublicIP name="MyPublicIP" domainNameLabel="MyPublicIP" />
            </PublicIPs>
          </InstanceAddress>
        </AddressAssignments>
      </NetworkConfiguration>
    </ServiceConfiguration>
    ```
3. Отправить файл cscfg hello hello облачную службу, выполнив hello шагов в hello [как tooConfigure облачных служб](../cloud-services/cloud-services-how-to-configure-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json#reconfigure-your-cscfg) статьи.

## <a name="next-steps"></a>Дальнейшие действия
* Понять, как [IP-адресация](virtual-network-ip-addresses-overview-classic.md) работает в hello классической модели развертывания.
* Общие сведения о зарезервированных IP-адресах см. в [этой статье](virtual-networks-reserved-public-ip.md).
