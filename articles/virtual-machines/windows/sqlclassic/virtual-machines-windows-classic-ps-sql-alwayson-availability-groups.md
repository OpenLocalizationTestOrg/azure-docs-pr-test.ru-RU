---
title: "aaaConfigure hello группы доступности AlwaysOn на Виртуальной машине Azure с помощью PowerShell | Документы Microsoft"
description: "В этом учебнике используется ресурсов, которые были созданы с помощью hello классической модели развертывания. Используйте PowerShell toocreate группы доступности AlwaysOn в Azure."
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: a4e2f175-fe56-4218-86c7-a43fb916cc64
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 03/17/2017
ms.author: mikeray
ms.openlocfilehash: d4a27e203b2ff299adebec2b010c03422459b3c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hello-always-on-availability-group-on-an-azure-vm-with-powershell"></a>Настройка группы доступности Always On для hello на Виртуальной машине Azure с помощью PowerShell
> [!div class="op_single_selector"]
> * [Классическая модель: пользовательский интерфейс](../classic/portal-sql-alwayson-availability-groups.md)
> * [Классическая модель: PowerShell](../classic/ps-sql-alwayson-availability-groups.md)
<br/>

Прежде чем начать, учтите, что теперь можно выполнить эту задачу в модели Azure Resource Manager. Для новых развертываний мы советуем использовать модель Azure Resource Manager. См. сведения в статье [Введение в группы доступности Always On SQL Server на виртуальных машинах Azure](../sql/virtual-machines-windows-portal-sql-availability-group-overview.md).

> [!IMPORTANT]
> Корпорация Майкрософт рекомендует наиболее новые развертывания для использования модели hello диспетчера ресурсов. В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../../../azure-resource-manager/resource-manager-deployment-model.md). В этой статье описан с помощью hello классической модели развертывания.

Виртуальные машины (VM) Azure может помочь стоимости hello toolower администраторы базы данных системы SQL Server высокой доступности. Этот учебник показывает, как группировать tooimplement доступности с помощью SQL Server Always On end-to-end среде Azure. В конце учебника hello hello решения AlwaysOn в SQL Server в Azure будет состоять из hello следующие элементы:

* Виртуальной сети, которая содержит множество подсетей, в том числе внешнюю и внутреннюю подсети;
* контроллера домена с доменом Active Directory;
* Две виртуальные машины SQL Server, развернутые toohello внутренней подсети и присоединены к домену toohello домена Active Directory.
* Отказоустойчивый кластер Windows трех узлов с моделью кворума большинства узлов hello.
* группы доступности с двумя репликами с синхронной фиксацией базы данных доступности.

Этот сценарий — хороший выбор из-за его простоты на Azure, а не из-за его экономичности или других факторов. Например можно свести к минимуму hello число виртуальных машин для группы доступности с двумя репликами toosave часы вычислительных операций в Azure, используя hello контроллер домена как следящую общую папку hello кворума в кластере отработки отказа двух узлов. Этот метод уменьшает число виртуальных Машин hello из hello выше конфигурации.

Этот учебник предназначен, что tooshow hello шаги, необходимые tooset копирование hello описано решение выше, не приводятся подробные сведения каждого этапа hello. Таким образом вместо обеспечивает действия по настройке hello графического пользовательского интерфейса, он использует tootake сценариев PowerShell можно быстро через каждый шаг. В этом учебнике предполагается hello следующее:

* Уже имеется учетная запись Azure с подпиской для виртуальных машин hello.
* После установки hello [командлетов Azure PowerShell](/powershell/azure/overview).
* Вы хорошо понимаете принцип работы групп доступности Always On в локальных решениях. Дополнительные сведения см. в разделе [Группы доступности AlwaysOn (SQL Server)](https://msdn.microsoft.com/library/hh510230.aspx).

## <a name="connect-tooyour-azure-subscription-and-create-hello-virtual-network"></a>Подключение tooyour подписки Azure и создать виртуальную сеть hello
1. В окне PowerShell на локальном компьютере импортируйте модуль Azure hello, загрузите hello машины tooyour файл параметров публикации и подключения к tooyour сеанса PowerShell подписки Azure путем импорта hello загрузки параметров публикации.

        Import-Module "C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\Azure\Azure.psd1"
        Get-AzurePublishSettingsFile
        Import-AzurePublishSettingsFile <publishsettingsfilepath>

    Hello **Get-AzurePublishSettingsFile** команда автоматически создает сертификат управления с помощью Azure и загружает его tooyour машины. Автоматически откроется браузер, и все данные учетной записи Майкрософт запрос tooenter hello для подписки Azure. загружаются Hello **.publishsettings** файле содержится вся информация hello требуется toomanage подписки Azure. После сохранения этого файла tooa локальный каталог, импортировать его, используя hello **команду Import-AzurePublishSettingsFile** команды.

   > [!NOTE]
   > файл PUBLISHSETTINGS Hello содержит учетные данные (Незакодированные), используемые tooadminister подписки Azure и служб. Hello рекомендации по безопасности для этого файла является toostore он временно за пределами исходных каталогов (например, в папке Libraries\Documents hello), а затем удалите его после завершения импорта hello. Злоумышленник, получивший доступ toohello PUBLISHSETTINGS-файл можно изменять, создавать и удалять служб Azure.

2. Определите ряд переменных, вы сможете использовать toocreate облачной ИТ-инфраструктуры.

        $location = "West US"
        $affinityGroupName = "ContosoAG"
        $affinityGroupDescription = "Contoso SQL HADR Affinity Group"
        $affinityGroupLabel = "IaaS BI Affinity Group"
        $networkConfigPath = "C:\scripts\Network.netcfg"
        $virtualNetworkName = "ContosoNET"
        $storageAccountName = "<uniquestorageaccountname>"
        $storageAccountLabel = "Contoso SQL HADR Storage Account"
        $storageAccountContainer = "https://" + $storageAccountName + ".blob.core.windows.net/vhds/"
        $winImageName = (Get-AzureVMImage | where {$_.Label -like "Windows Server 2008 R2 SP1*"} | sort PublishedDate -Descending)[0].ImageName
        $sqlImageName = (Get-AzureVMImage | where {$_.Label -like "SQL Server 2012 SP1 Enterprise*"} | sort PublishedDate -Descending)[0].ImageName
        $dcServerName = "ContosoDC"
        $dcServiceName = "<uniqueservicename>"
        $availabilitySetName = "SQLHADR"
        $vmAdminUser = "AzureAdmin"
        $vmAdminPassword = "Contoso!000"
        $workingDir = "c:\scripts\"

    Обратите внимания toohello после tooensure, который позднее будет успешным команды:

   * Переменные **$storageAccountName** и **$dcServiceName** должно быть уникальным, так как они используются tooidentify вашей учетная запись облачного хранилища и облачного сервера соответственно на hello Интернет.
   * Здравствуйте, имена, указанные для переменных **$affinityGroupName** и **$virtualNetworkName** настраиваются в документе конфигурации hello виртуальной сети, которые будут использоваться позже.
   * **$sqlImageName** указывает hello обновить имя образа виртуальной Машины hello, который содержит SQL Server 2012 Service Pack 1 Enterprise Edition.
   * Для простоты **Contoso! 000** Здравствуйте, же пароль, который используется на протяжении всего учебника hello.

3. Создайте территориальную группу

        New-AzureAffinityGroup `
            -Name $affinityGroupName `
            -Location $location `
            -Description $affinityGroupDescription `
            -Label $affinityGroupLabel

4. Создайте виртуальную сеть, импортировав файл конфигурации.

        Set-AzureVNetConfig `
            -ConfigurationPath $networkConfigPath

    файл конфигурации Hello содержит следующие XML-документ hello. Вкратце, он указывает виртуальную сеть с именем **ContosoNET** в территориальной группе hello вызывается **ContosoAG**. Он имеет hello адресное пространство **10.10.0.0/16** и две подсети **10.10.1.0/24** и **10.10.2.0/24**, являющиеся интерфейсной подсети hello и задней подсеть соответственно. Hello интерфейсной подсети — расположения клиентские приложения, например Microsoft SharePoint. Hello конечной подсети является расположения hello виртуальные машины SQL Server. При изменении hello **$affinityGroupName** и **$virtualNetworkName** переменных ранее, необходимо также изменить соответствующие имена ниже hello.

        <NetworkConfiguration xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns="http://schemas.microsoft.com/ServiceHosting/2011/07/NetworkConfiguration">
          <VirtualNetworkConfiguration>
            <Dns />
            <VirtualNetworkSites>
              <VirtualNetworkSite name="ContosoNET" AffinityGroup="ContosoAG">
                <AddressSpace>
                  <AddressPrefix>10.10.0.0/16</AddressPrefix>
                </AddressSpace>
                <Subnets>
                  <Subnet name="Front">
                    <AddressPrefix>10.10.1.0/24</AddressPrefix>
                  </Subnet>
                  <Subnet name="Back">
                    <AddressPrefix>10.10.2.0/24</AddressPrefix>
                  </Subnet>
                </Subnets>
              </VirtualNetworkSite>
            </VirtualNetworkSites>
          </VirtualNetworkConfiguration>
        </NetworkConfiguration>

5. Создайте учетную запись хранилища, связанной с hello территориальная группа создана и задать его в качестве текущей учетной записи хранилища hello в вашей подписке.

        New-AzureStorageAccount `
            -StorageAccountName $storageAccountName `
            -Label $storageAccountLabel `
            -AffinityGroup $affinityGroupName
        Set-AzureSubscription `
            -SubscriptionName (Get-AzureSubscription).SubscriptionName `
            -CurrentStorageAccount $storageAccountName

6. Создайте сервер контроллера домена hello в hello новой облачной службе и группе доступности.

        New-AzureVMConfig `
            -Name $dcServerName `
            -InstanceSize Medium `
            -ImageName $winImageName `
            -MediaLocation "$storageAccountContainer$dcServerName.vhd" `
            -DiskLabel "OS" |
            Add-AzureProvisioningConfig `
                -Windows `
                -DisableAutomaticUpdates `
                -AdminUserName $vmAdminUser `
                -Password $vmAdminPassword |
                New-AzureVM `
                    -ServiceName $dcServiceName `
                    –AffinityGroup $affinityGroupName `
                    -VNetName $virtualNetworkName

    Эти перенаправленные команды hello следующие действия:

   * **New-AzureVMConfig** создает конфигурацию виртуальной машины.
   * **-AzureProvisioningConfig** дает hello параметры конфигурации изолированного сервера Windows.
   * **-AzureDataDisk** добавляет диск данных hello, который будет использоваться для хранения данных Active Directory с кэширование параметр set tooNone hello.
   * **Новый-AzureVM** создает новую облачную службу, а hello новой виртуальной Машины Azure в новой облачной службе hello.

7. Дождитесь hello toobe новой виртуальной Машины полностью подготовлены и загрузить hello файл удаленного рабочего стола tooyour рабочий каталог. Здравствуйте, так как hello новой виртуальной Машины Azure использует tooprovision много времени, `while` цикл продолжает toopoll hello новой виртуальной Машины, пока он не готов к использованию.

        $VMStatus = Get-AzureVM -ServiceName $dcServiceName -Name $dcServerName

        While ($VMStatus.InstanceStatus -ne "ReadyRole")
        {
            write-host "Waiting for " $VMStatus.Name "... Current Status = " $VMStatus.InstanceStatus
            Start-Sleep -Seconds 15
            $VMStatus = Get-AzureVM -ServiceName $dcServiceName -Name $dcServerName
        }

        Get-AzureRemoteDesktopFile `
            -ServiceName $dcServiceName `
            -Name $dcServerName `
            -LocalPath "$workingDir$dcServerName.rdp"

Hello сервера контроллера домена успешно подготовлен. Далее следует настроить hello домена Active Directory на этом сервере контроллера домена. Не закрывайте окно hello PowerShell на локальном компьютере. Оно будет использоваться снова далее toocreate hello две виртуальные машины SQL Server.

## <a name="configure-hello-domain-controller"></a>Настройка контроллера домена hello
1. Подключитесь toohello сервера контроллера домена, запустив файл удаленного рабочего стола hello. Использовать AzureAdmin имя пользователя и пароль администратора машины hello **Contoso! 000**, который был указан при создании hello новой виртуальной Машины.
2. Откройте окно PowerShell с правами администратора.
3. Запустите следующие hello **DCPROMO. EXE** tooset команду копирования hello **corp.contoso.com** домен с hello каталоги данных на диск M.

        dcpromo.exe `
            /unattend `
            /ReplicaOrNewDomain:Domain `
            /NewDomain:Forest `
            /NewDomainDNSName:corp.contoso.com `
            /ForestLevel:4 `
            /DomainNetbiosName:CORP `
            /DomainLevel:4 `
            /InstallDNS:Yes `
            /ConfirmGc:Yes `
            /CreateDNSDelegation:No `
            /DatabasePath:"C:\Windows\NTDS" `
            /LogPath:"C:\Windows\NTDS" `
            /SYSVOLPath:"C:\Windows\SYSVOL" `
            /SafeModeAdminPassword:"Contoso!000"

    После завершения выполнения команды hello hello виртуальная машина автоматически перезапустится.

4. Повторное подключение toohello сервера контроллера домена, запустив файл удаленного рабочего стола hello. На этот раз войдите с именем **CORP\Administrator**.
5. Откройте окно PowerShell с правами администратора и импортируйте модуль Active Directory PowerShell hello с помощью hello следующую команду:

        Import-Module ActiveDirectory

6. Выполните следующие команды tooadd трех пользователей toohello домена hello.

        $pwd = ConvertTo-SecureString "Contoso!000" -AsPlainText -Force
        New-ADUser `
            -Name 'Install' `
            -AccountPassword  $pwd `
            -PasswordNeverExpires $true `
            -ChangePasswordAtLogon $false `
            -Enabled $true
        New-ADUser `
            -Name 'SQLSvc1' `
            -AccountPassword  $pwd `
            -PasswordNeverExpires $true `
            -ChangePasswordAtLogon $false `
            -Enabled $true
        New-ADUser `
            -Name 'SQLSvc2' `
            -AccountPassword  $pwd `
            -PasswordNeverExpires $true `
            -ChangePasswordAtLogon $false `
            -Enabled $true

    **CORP\Install** является используется tooconfigure все данные, связанные с экземплярами службы SQL Server toohello, hello отказоустойчивого кластера группы доступности hello. **CORP\SQLSvc1** и **CORP\SQLSvc2** , используются в качестве учетных записей служб SQL Server hello hello двух виртуальных машин SQL Server.
7. Hello Далее, выполните следующие команды toogive **CORP\Install** hello разрешения toocreate объектов-компьютеров в домене hello.

        Cd ad:
        $sid = new-object System.Security.Principal.SecurityIdentifier (Get-ADUser "Install").SID
        $guid = new-object Guid bf967a86-0de6-11d0-a285-00aa003049e2
        $ace1 = new-object System.DirectoryServices.ActiveDirectoryAccessRule $sid,"CreateChild","Allow",$guid,"All"
        $corp = Get-ADObject -Identity "DC=corp,DC=contoso,DC=com"
        $acl = Get-Acl $corp
        $acl.AddAccessRule($ace1)
        Set-Acl -Path "DC=corp,DC=contoso,DC=com" -AclObject $acl

    Hello GUID, указанный выше — hello GUID для типа объекта компьютера hello. Hello **CORP\Install** учетная запись должна hello **чтение всех свойств** и **создание объектов-компьютеров** Active Direct hello toocreate разрешение объектов для отработки отказа hello кластер. Hello **чтение всех свойств** разрешение уже предоставлено tooCORP\Install по умолчанию, поэтому не требуется toogrant его явным образом. Дополнительные сведения о разрешениях, необходимых toocreate hello отказоустойчивого кластера, см. в разделе [Пошаговое руководство по отказоустойчивому кластеру: Настройка учетных записей в Active Directory](https://technet.microsoft.com/library/cc731002%28v=WS.10%29.aspx).

    Теперь, после завершения настройки Active Directory и объектов пользователей hello, вы создадите двух виртуальных машин SQL Server и присоединить их toothis домена.

## <a name="create-hello-sql-server-vms"></a>Создание виртуальных машин SQL Server hello
1. По-прежнему toouse окно hello PowerShell, открытое на локальном компьютере. Определите следующие дополнительные переменные hello:

        $domainName= "corp"
        $FQDN = "corp.contoso.com"
        $subnetName = "Back"
        $sqlServiceName = "<uniqueservicename>"
        $quorumServerName = "ContosoQuorum"
        $sql1ServerName = "ContosoSQL1"
        $sql2ServerName = "ContosoSQL2"
        $availabilitySetName = "SQLHADR"
        $dataDiskSize = 100
        $dnsSettings = New-AzureDns -Name "ContosoBackDNS" -IPAddress "10.10.0.4"

    Здравствуйте, IP-адрес **10.10.0.4** toohello обычно назначается первой виртуальной Машины, созданной в hello **10.10.0.0/16** подсети виртуальной сети Azure. Следует убедиться, что это hello адрес сервера контроллера домена, запустив **IPCONFIG**.
2. С именем виртуальной Машины в отказоустойчивом кластере hello, выполнения hello следующий набор команд toocreate hello сначала **ContosoQuorum**:

        New-AzureVMConfig `
            -Name $quorumServerName `
            -InstanceSize Medium `
            -ImageName $winImageName `
            -MediaLocation "$storageAccountContainer$quorumServerName.vhd" `
            -AvailabilitySetName $availabilitySetName `
            -DiskLabel "OS" |
            Add-AzureProvisioningConfig `
                -WindowsDomain `
                -AdminUserName $vmAdminUser `
                -Password $vmAdminPassword `
                -DisableAutomaticUpdates `
                -Domain $domainName `
                -JoinDomain $FQDN `
                -DomainUserName $vmAdminUser `
                -DomainPassword $vmAdminPassword |
                Set-AzureSubnet `
                    -SubnetNames $subnetName |
                    New-AzureVM `
                        -ServiceName $sqlServiceName `
                        –AffinityGroup $affinityGroupName `
                        -VNetName $virtualNetworkName `
                        -DnsSettings $dnsSettings

    Обратите внимание hello следующее относительно приведенных выше команд hello.

   * **Новый AzureVMConfig** создает конфигурацию виртуальной Машины с hello заданным именем группы доступности. Hello последующие виртуальные машины будут созданы со hello же имя набора доступности, чтобы все они присоединены toohello одной группе доступности.
   * **-AzureProvisioningConfig** соединения hello домена Active Directory toohello виртуальной Машины, созданной.
   * **SET-AzureSubnet** местах hello виртуальной Машины в конечной подсети hello.
   * **Новый-AzureVM** создает новую облачную службу, а hello новой виртуальной Машины Azure в новой облачной службе hello. Hello **DnsSettings** для hello серверов в новой облачной службе hello имеет hello IP-адрес указывает этот DNS-сервер hello **10.10.0.4**. Это IP-адрес сервера контроллера домена hello hello. Этот параметр необходим tooenable hello новых виртуальных машин в домене Active Directory для службы toojoin hello облака toohello успешно. Без этого параметра необходимо вручную задать параметры IPv4 hello в вашей виртуальной Машины toouse hello контроллер домена как основной DNS-сервер hello после подготовки hello виртуальной Машины и затем присоединить домену Active Directory toohello hello виртуальной Машины.
3. Выполнения hello следующие выведенной команды toocreate hello виртуальные машины SQL Server с именем **ContosoSQL1** и **ContosoSQL2**.

        # Create ContosoSQL1...
        New-AzureVMConfig `
            -Name $sql1ServerName `
            -InstanceSize Large `
            -ImageName $sqlImageName `
            -MediaLocation "$storageAccountContainer$sql1ServerName.vhd" `
            -AvailabilitySetName $availabilitySetName `
            -HostCaching "ReadOnly" `
            -DiskLabel "OS" |
            Add-AzureProvisioningConfig `
                -WindowsDomain `
                -AdminUserName $vmAdminUser `
                -Password $vmAdminPassword `
                -DisableAutomaticUpdates `
                -Domain $domainName `
                -JoinDomain $FQDN `
                -DomainUserName $vmAdminUser `
                -DomainPassword $vmAdminPassword |
                Set-AzureSubnet `
                    -SubnetNames $subnetName |
                    Add-AzureEndpoint `
                        -Name "SQL" `
                        -Protocol "tcp" `
                        -PublicPort 1 `
                        -LocalPort 1433 |
                        New-AzureVM `
                            -ServiceName $sqlServiceName

        # Create ContosoSQL2...
        New-AzureVMConfig `
            -Name $sql2ServerName `
            -InstanceSize Large `
            -ImageName $sqlImageName `
            -MediaLocation "$storageAccountContainer$sql2ServerName.vhd" `
            -AvailabilitySetName $availabilitySetName `
            -HostCaching "ReadOnly" `
            -DiskLabel "OS" |
            Add-AzureProvisioningConfig `
                -WindowsDomain `
                -AdminUserName $vmAdminUser `
                -Password $vmAdminPassword `
                -DisableAutomaticUpdates `
                -Domain $domainName `
                -JoinDomain $FQDN `
                -DomainUserName $vmAdminUser `
                -DomainPassword $vmAdminPassword |
                Set-AzureSubnet `
                    -SubnetNames $subnetName |
                    Add-AzureEndpoint `
                        -Name "SQL" `
                        -Protocol "tcp" `
                        -PublicPort 2 `
                        -LocalPort 1433 |
                        New-AzureVM `
                            -ServiceName $sqlServiceName

    Обратите внимание hello следующее относительно hello показанные выше команды.

   * **Новый AzureVMConfig** использует hello же имя набора доступности как контроллер домена hello и использует hello образа SQL Server 2012 Service Pack 1 Enterprise Edition в коллекции виртуальных машин hello. Он также устанавливает hello операционной системы диска tooread кэша (запрет записи в кэш). Мы рекомендуем hello базы данных файлы tooa отдельный диск с данными присоединения toohello виртуальной Машины и настроить в нем нет чтение или кэширование записи. Однако Наилучшая альтернатива hello это tooremove кэширование записи на диск операционной системы hello, так как не удается удалить кэширование на диске операционной системы hello.
   * **-AzureProvisioningConfig** соединения hello домена Active Directory toohello виртуальной Машины, созданной.
   * **SET-AzureSubnet** местах hello виртуальной Машины в конечной подсети hello.
   * **-AzureEndpoint** добавляет конечные точки доступа, чтобы клиентские приложения могут обращаться к эти экземпляры служб SQL Server на hello Интернета. Другие порты, получают tooContosoSQL1 и ContosoSQL2.
   * **Новый-AzureVM** создает hello новую виртуальную Машину SQL Server в hello же облачную службу как ContosoQuorum. Виртуальные машины hello необходимо поместить в hello же облачную службу при необходимости toobe в одной группе доступности hello.
4. Дождитесь каждого toobe ВМ полностью подготовлены, а для каждой виртуальной Машины toodownload его файл удаленного рабочего стола tooyour рабочий каталог. Hello `for` цикла циклически hello трем новым виртуальным машинам и выполняет команды hello в фигурных скобках верхнего уровня hello для каждого из них.

        Foreach ($VM in $VMs = Get-AzureVM -ServiceName $sqlServiceName)
        {
            write-host "Waiting for " $VM.Name "..."

            # Loop until hello VM status is "ReadyRole"
            While ($VM.InstanceStatus -ne "ReadyRole")
            {
                write-host "  Current Status = " $VM.InstanceStatus
                Start-Sleep -Seconds 15
                $VM = Get-AzureVM -ServiceName $VM.ServiceName -Name $VM.InstanceName
            }

            write-host "  Current Status = " $VM.InstanceStatus

            # Download remote desktop file
            Get-AzureRemoteDesktopFile -ServiceName $VM.ServiceName -Name $VM.InstanceName -LocalPath "$workingDir$($VM.InstanceName).rdp"
        }

    виртуальные машины Hello SQL Server настроены и запущены, но они установлены с помощью SQL Server с параметрами по умолчанию.

## <a name="initialize-hello-failover-cluster-vms"></a>Инициализировать hello отказоустойчивого кластера виртуальные машины
В этом разделе требуется три серверов hello toomodify, которые будут использоваться в отказоустойчивом кластере hello и hello установки SQL Server. В частности:

* Все серверы: требуется tooinstall hello **отказоустойчивой кластеризации** компонентов.
* Все серверы: требуется tooadd **CORP\Install** как hello машина **администратора**.
* Только ContosoSQL1 и ContosoSQL2: требуется tooadd **CORP\Install** как **sysadmin** роли в базе данных по умолчанию hello.
* Только ContosoSQL1 и ContosoSQL2: требуется tooadd **NT AUTHORITY\System** как вход с hello следующие разрешения:

  * Изменение любой группы доступности
  * Соединение SQL
  * Просмотр состояния сервера
* Только ContosoSQL1 и ContosoSQL2: hello **TCP** протокол уже включен на виртуальной Машине SQL Server hello. Однако по-прежнему требуются tooopen hello брандмауэра для удаленного доступа к SQL Server.

Теперь вы готовы toostart. Начиная с версии **ContosoQuorum**, выполните следующие шаги hello:

1. Подключение слишком**ContosoQuorum** путем запуска файлов удаленного рабочего стола hello. Используйте имя пользователя администратора машины hello **AzureAdmin** и пароль **Contoso! 000**, указанные при создании виртуальных машин hello.
2. Убедитесь, что компьютеры hello была успешно присоединена слишком**corp.contoso.com**.
3. Дождитесь hello toofinish установки на SQL Server под управлением hello автоматизировать задачи инициализации, прежде чем продолжить.
4. Откройте окно PowerShell с правами администратора.
5. Установите компонент отказоустойчивой кластеризации Windows hello.

        Import-Module ServerManager
        Add-WindowsFeature Failover-Clustering
6. Добавьте **CORP\Install** в качестве локального администратора.

        net localgroup administrators "CORP\Install" /Add
7. Выйдите из ContosoQuorum. Теперь работа с этим сервером завершена.

        logoff.exe

Затем инициализируйте виртуальные машины **ContosoSQL1** и **ContosoSQL2**. Выполните hello шаги, которые идентичны для обеих виртуальных машин SQL Server.

1. Подключитесь toohello двух виртуальных машин SQL Server, запустив файлы удаленного рабочего стола hello. Используйте имя пользователя администратора машины hello **AzureAdmin** и пароль **Contoso! 000**, указанные при создании виртуальных машин hello.
2. Убедитесь, что компьютеры hello была успешно присоединена слишком**corp.contoso.com**.
3. Дождитесь hello toofinish установки на SQL Server под управлением hello автоматизировать задачи инициализации, прежде чем продолжить.
4. Откройте окно PowerShell с правами администратора.
5. Установите компонент отказоустойчивой кластеризации Windows hello.

        Import-Module ServerManager
        Add-WindowsFeature Failover-Clustering
6. Добавьте **CORP\Install** в качестве локального администратора.

        net localgroup administrators "CORP\Install" /Add
7. Импортируйте поставщик SQL Server PowerShell hello.

        Set-ExecutionPolicy -Execution RemoteSigned -Force
        Import-Module -Name "sqlps" -DisableNameChecking
8. Добавить **CORP\Install** как hello роли sysadmin для экземпляра SQL Server по умолчанию hello.

        net localgroup administrators "CORP\Install" /Add
        Invoke-SqlCmd -Query "EXEC sp_addsrvrolemember 'CORP\Install', 'sysadmin'" -ServerInstance "."
9. Добавить **NT AUTHORITY\System** как вход с описанными выше разрешениями hello трех.

        Invoke-SqlCmd -Query "CREATE LOGIN [NT AUTHORITY\SYSTEM] FROM WINDOWS" -ServerInstance "."
        Invoke-SqlCmd -Query "GRANT ALTER ANY AVAILABILITY GROUP too[NT AUTHORITY\SYSTEM] AS SA" -ServerInstance "."
        Invoke-SqlCmd -Query "GRANT CONNECT SQL too[NT AUTHORITY\SYSTEM] AS SA" -ServerInstance "."
        Invoke-SqlCmd -Query "GRANT VIEW SERVER STATE too[NT AUTHORITY\SYSTEM] AS SA" -ServerInstance "."
10. Откройте брандмауэр Windows hello для удаленного доступа к SQL Server.

         netsh advfirewall firewall add rule name='SQL Server (TCP-In)' program='C:\Program Files\Microsoft SQL Server\MSSQL11.MSSQLSERVER\MSSQL\Binn\sqlservr.exe' dir=in action=allow protocol=TCP
11. Выйдите из обеих виртуальных машин.

         logoff.exe

Наконец вы готовы tooconfigure группы доступности hello. Вы воспользуетесь tooperform hello поставщик SQL Server PowerShell, работающие hello со **ContosoSQL1**.

## <a name="configure-hello-availability-group"></a>Настройка группы доступности hello
1. Подключение слишком**ContosoSQL1** еще раз путем запуска файлов удаленного рабочего стола hello. Вместо вход с помощью учетной записи компьютера hello, войдите в систему с **CORP\Install**.
2. Откройте окно PowerShell с правами администратора.
3. Определите следующие переменные hello:

        $server1 = "ContosoSQL1"
        $server2 = "ContosoSQL2"
        $serverQuorum = "ContosoQuorum"
        $acct1 = "CORP\SQLSvc1"
        $acct2 = "CORP\SQLSvc2"
        $password = "Contoso!000"
        $clusterName = "Cluster1"
        $timeout = New-Object System.TimeSpan -ArgumentList 0, 0, 30
        $db = "MyDB1"
        $backupShare = "\\$server1\backup"
        $quorumShare = "\\$server1\quorum"
        $ag = "AG1"
4. Импортируйте поставщик SQL Server PowerShell hello.

        Set-ExecutionPolicy RemoteSigned -Force
        Import-Module "sqlps" -DisableNameChecking
5. Изменение учетной записи службы SQL Server hello для ContosoSQL1 tooCORP\SQLSvc1.

        $wmi1 = new-object ("Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer") $server1
        $wmi1.services | where {$_.Type -eq 'SqlServer'} | foreach{$_.SetServiceAccount($acct1,$password)}
        $svc1 = Get-Service -ComputerName $server1 -Name 'MSSQLSERVER'
        $svc1.Stop()
        $svc1.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Stopped,$timeout)
        $svc1.Start();
        $svc1.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Running,$timeout)
6. Изменение учетной записи службы SQL Server hello для ContosoSQL2 tooCORP\SQLSvc2.

        $wmi2 = new-object ("Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer") $server2
        $wmi2.services | where {$_.Type -eq 'SqlServer'} | foreach{$_.SetServiceAccount($acct2,$password)}
        $svc2 = Get-Service -ComputerName $server2 -Name 'MSSQLSERVER'
        $svc2.Stop()
        $svc2.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Stopped,$timeout)
        $svc2.Start();
        $svc2.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Running,$timeout)
7. Загрузить **CreateAzureFailoverCluster.ps1** из [Создание отказоустойчивого кластера для группы доступности AlwaysOn в виртуальной Машине Azure](http://gallery.technet.microsoft.com/scriptcenter/Create-WSFC-Cluster-for-7c207d3a) toohello локальный рабочий каталог. Вы будете использовать этот сценарий toohelp, Создание функциональной отказоустойчивого кластера. Важная информация по отказоустойчивой кластеризации Windows взаимодействие с hello Azure сети см. в разделе [высокий уровень доступности и аварийного восстановления SQL Server в виртуальных машинах Azure](../sql/virtual-machines-windows-sql-high-availability-dr.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).
8. Изменить tooyour рабочий каталог и создайте hello отказоустойчивого кластера с помощью сценария загружаются hello.

        Set-ExecutionPolicy Unrestricted -Force
        .\CreateAzureFailoverCluster.ps1 -ClusterName "$clusterName" -ClusterNode "$server1","$server2","$serverQuorum"
9. Включение групп доступности AlwaysOn для экземпляров SQL Server по умолчанию hello **ContosoSQL1** и **ContosoSQL2**.

        Enable-SqlAlwaysOn `
            -Path SQLSERVER:\SQL\$server1\Default `
            -Force
        Enable-SqlAlwaysOn `
            -Path SQLSERVER:\SQL\$server2\Default `
            -NoServiceRestart
        $svc2.Stop()
        $svc2.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Stopped,$timeout)
        $svc2.Start();
        $svc2.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Running,$timeout)
10. Создать каталог резервных копий и предоставьте разрешения для учетных записей служб SQL Server hello. Вы используете tooprepare directory hello баз данных доступности на вторичной реплике hello.

         $backup = "C:\backup"
         New-Item $backup -ItemType directory
         net share backup=$backup "/grant:$acct1,FULL" "/grant:$acct2,FULL"
         icacls.exe "$backup" /grant:r ("$acct1" + ":(OI)(CI)F") ("$acct2" + ":(OI)(CI)F")
11. Создание базы данных на **ContosoSQL1** вызывается **MyDB1**, выполните полную резервную копию и резервную копию журнала и восстановить их на **ContosoSQL2** с hello **WITH Параметр NORECOVERY** параметр.

         Invoke-SqlCmd -Query "CREATE database $db"
         Backup-SqlDatabase -Database $db -BackupFile "$backupShare\db.bak" -ServerInstance $server1
         Backup-SqlDatabase -Database $db -BackupFile "$backupShare\db.log" -ServerInstance $server1 -BackupAction Log
         Restore-SqlDatabase -Database $db -BackupFile "$backupShare\db.bak" -ServerInstance $server2 -NoRecovery
         Restore-SqlDatabase -Database $db -BackupFile "$backupShare\db.log" -ServerInstance $server2 -RestoreAction Log -NoRecovery
12. Создайте конечные точки группы доступности hello на hello виртуальные машины SQL Server и задайте соответствующие разрешения hello в конечных точках hello.

         $endpoint =
             New-SqlHadrEndpoint MyMirroringEndpoint `
             -Port 5022 `
             -Path "SQLSERVER:\SQL\$server1\Default"
         Set-SqlHadrEndpoint `
             -InputObject $endpoint `
             -State "Started"
         $endpoint =
             New-SqlHadrEndpoint MyMirroringEndpoint `
             -Port 5022 `
             -Path "SQLSERVER:\SQL\$server2\Default"
         Set-SqlHadrEndpoint `
             -InputObject $endpoint `
             -State "Started"

         Invoke-SqlCmd -Query "CREATE LOGIN [$acct2] FROM WINDOWS" -ServerInstance $server1
         Invoke-SqlCmd -Query "GRANT CONNECT ON ENDPOINT::[MyMirroringEndpoint] too[$acct2]" -ServerInstance $server1
         Invoke-SqlCmd -Query "CREATE LOGIN [$acct1] FROM WINDOWS" -ServerInstance $server2
         Invoke-SqlCmd -Query "GRANT CONNECT ON ENDPOINT::[MyMirroringEndpoint] too[$acct1]" -ServerInstance $server2
13. Создание реплики доступности hello.

         $primaryReplica =
             New-SqlAvailabilityReplica `
             -Name $server1 `
             -EndpointURL "TCP://$server1.corp.contoso.com:5022" `
             -AvailabilityMode "SynchronousCommit" `
             -FailoverMode "Automatic" `
             -Version 11 `
             -AsTemplate
         $secondaryReplica =
             New-SqlAvailabilityReplica `
             -Name $server2 `
             -EndpointURL "TCP://$server2.corp.contoso.com:5022" `
             -AvailabilityMode "SynchronousCommit" `
             -FailoverMode "Automatic" `
             -Version 11 `
             -AsTemplate
14. Наконец создайте группу доступности hello и группы доступности toohello вторичная реплика hello соединения.

         New-SqlAvailabilityGroup `
             -Name $ag `
             -Path "SQLSERVER:\SQL\$server1\Default" `
             -AvailabilityReplica @($primaryReplica,$secondaryReplica) `
             -Database $db
         Join-SqlAvailabilityGroup `
             -Path "SQLSERVER:\SQL\$server2\Default" `
             -Name $ag
         Add-SqlAvailabilityDatabase `
             -Path "SQLSERVER:\SQL\$server2\Default\AvailabilityGroups\$ag" `
             -Database $db

## <a name="next-steps"></a>Дальнейшие действия
Решение SQL Server Always On на основе группы доступности в Azure успешно создано. tooconfigure прослушивателя для этой группы доступности. в разделе [настроить прослушиватель ILB для групп доступности AlwaysOn в Azure](../classic/ps-sql-int-listener.md).

Дополнительные сведения об использовании SQL Server в Azure см. в статье [Общие сведения об SQL Server на виртуальных машинах Azure](../sql/virtual-machines-windows-sql-server-iaas-overview.md).
