---
title: "aaaConnect виртуальной сети tooyour приложения с помощью PowerShell"
description: "Инструкции о способах tooconnect tooand работы с виртуальными сетями с помощью PowerShell"
services: app-service
documentationcenter: 
author: ccompy
manager: erikre
editor: cephalin
ms.assetid: a5c76e77-972a-431c-b14b-3611dae1631b
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/29/2016
ms.author: ccompy
ms.openlocfilehash: c9d0fa99d02cab7b2c7211a1b2f7b7d0cd27ee8e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-app-tooyour-virtual-network-by-using-powershell"></a>Подключение виртуальной сети tooyour приложения с помощью PowerShell
## <a name="overview"></a>Обзор
В службе приложений Azure, можно подключить ваше приложение (веб, мобильных или API) tooan виртуальной сети (VNet) Azure в вашей подписке. Эта функция называется интеграцией с виртуальной сетью. Функция интеграции виртуальной сети Hello не следует путать с функцией hello среды службы приложений, позволяющую toorun экземпляр службы приложений Azure в виртуальной сети.

Функция интеграции виртуальной сети Hello имеет пользовательский интерфейс (UI) в новый портал hello toointegrate можно использовать с виртуальными сетями, которые развертываются с помощью модели развертывания диспетчера ресурсов Azure hello либо hello классической модели развертывания. Дополнительные сведения о функции hello toolearn см [интегрировать приложения с помощью виртуальной сети Azure](web-sites-integrate-with-vnet.md).

Эта статья является не о как toouse hello пользовательского интерфейса, но вместо о том, как tooenable интеграции с помощью PowerShell. Поскольку отличаются hello команды для каждой модели развертывания, в этой статье имеется раздел для каждой модели развертывания.  

Прежде чем продолжить работу с этой статьей, убедитесь, что:

* Здравствуйте, который установлен последний пакет SDK Azure PowerShell. Это можно установить с hello установщика веб-платформы.
* У вас есть приложение в службе приложений Azure, работающее в системе SKU класса "Стандартный" или "Премиум".

## <a name="classic-virtual-networks"></a>Классические виртуальные сети
В этом разделе объясняется три задачи для виртуальных сетей, использующих hello классической модели развертывания.

1. Подключение приложения tooa ранее существовавших виртуальной сети, шлюз и настроенной для подключения точки сайтами.
2. обновление сведений об интеграции с виртуальной сетью для приложения;
3. отключение приложения от виртуальной сети.

### <a name="connect-an-app-tooa-classic-vnet"></a>Подключение приложения tooa классической виртуальной сети
tooconnect приложения tooa виртуальной сетью, выполните следующие три действия.

1. Объявите toohello веб-приложения, что он будет присоединение к конкретной виртуальной сети. приложение Hello создаст сертификат, который получит toohello виртуальной сети для подключения точки сайтами.
2. Отправка hello web app сертификат toohello виртуальной сети, а затем извлечь hello точка сеть VPN пакет URI.
3. Обновите подключение виртуальной сети hello веб-приложения с URI пакета точки сайтами hello.

Hello первый и третий шаги можно использовать в сценариях, но второй шаг hello требует однократное действие вручную через портал hello или tooperform доступа **ПОМЕСТИТЬ** или **PATCH** действия hello виртуальной сети Конечная точка диспетчера ресурсов Azure. Обратитесь в службу поддержки Azure toohave это включена. Перед выполнением действий убедитесь, что у вас есть классическая виртуальная сеть со включенным подключением типа "точка — сеть" и развернутым шлюзом. toocreate hello шлюза и включить точки сайтами подключения, необходимо toouse hello портала, описанную в [создание VPN-шлюза][createvpngateway].

Hello классической виртуальной сети должен toobe в hello той же подписке, службе приложений план содержит приложение hello, который интегрируется с.

##### <a name="set-up-azure-powershell-sdk"></a>Настройка пакета SDK для Azure PowerShell
Откройте окно PowerShell и настройте учетную запись и подписку Azure, используя следующую команду:

    Login-AzureRmAccount

Этой команды откроется запрос tooget учетные данные Azure. После входа в воспользуйтесь одним из следующих команд tooselect hello подписки, которые должны toouse hello. Убедитесь, что вы используете подписки hello, виртуальную сеть и план служб приложений в.

    Select-AzureRmSubscription –SubscriptionName [WebAppSubscriptionName]

или

    Select-AzureRmSubscription –SubscriptionId [WebAppSubscriptionId]

##### <a name="variables-used-in-this-article"></a>Переменные, используемые в этой статье
команды toosimplify, мы установим **$Configuration** переменной PowerShell с определенной конфигурацией hello.

Задайте переменную следующим образом в PowerShell с hello следующие параметры:

    $Configuration = @{}
    $Configuration.WebAppResourceGroup = "[Your web app resource group]"
    $Configuration.WebAppName = "[Your web app name]"
    $Configuration.VnetSubscriptionId = "[Your vnet subscription id]"
    $Configuration.VnetResourceGroup = "[Your vnet resource group]"
    $Configuration.VnetName = "[Your vnet name]"

расположение приложения Hello должно быть расположение hello без пробелов. например westus для западной части США.

    $Configuration.WebAppLocation = "[Your web app Location]"

Следующий элемент Hello —, где должен быть записан hello сертификата. Этот путь должен быть доступным для записи на локальном компьютере. Убедитесь, что tooinclude CER-файл в конце hello.

    $Configuration.GeneratedCertificatePath = "[C:\Path\To\Certificate.cer]"

toosee можно задать тип **$Configuration**.

    > $Configuration

    Name                           Value
    ----                           -----
    GeneratedCertificatePath       C:\vnetcert.cer
    VnetSubscriptionId             efc239a4-88f9-2c5e-a9a1-3034c21ad496
    WebAppResourceGroup            vnetdemo-rg
    VnetResourceGroup              testase1-rg
    VnetName                       TestNetwork
    WebAppName                     vnetintdemoapp
    WebAppLocation                 centralus

Hello оставшейся части этого раздела предполагается, что переменная, созданная, как описано выше.

##### <a name="declare-hello-virtual-network-toohello-app"></a>Объявите toohello приложение hello виртуальной сети
Используйте hello следующая команда приложение hello tootell, что он будет использоваться этой конкретной виртуальной сети. Это приведет к toogenerate приложения hello необходимые сертификаты:

    $vnet = New-AzureRmResource -Name "$($Configuration.WebAppName)/$($Configuration.VnetName)" -ResourceGroupName $Configuration.WebAppResourceGroup -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -PropertyObject @{"VnetResourceId" = "/subscriptions/$($Configuration.VnetSubscriptionId)/resourceGroups/$($Configuration.VnetResourceGroup)/providers/Microsoft.ClassicNetwork/virtualNetworks/$($Configuration.VnetName)"} -Location $Configuration.WebAppLocation -ApiVersion 2015-07-01

Если команда выполнится успешно, **$vnet** будет содержать переменную **Properties**. Hello **свойства** переменной должен содержать оба сертификата отпечаток и hello данные сертификата.

##### <a name="upload-hello-web-app-certificate-toohello-virtual-network"></a>Отправка hello web app сертификат toohello виртуальной сети
Для каждого сочетания виртуальной сети и подписки необходимо выполнить однократное действие вручную. То есть при подключении приложения в подписке A tooVirtual сети A необходимо будет toodo этот шаг только один раз, независимо от того, сколько приложений можно настроить. При добавлении новой виртуальной сети tooanother приложения toodo потребуется снова. Hello причиной этого является набор сертификатов, созданный на уровне подписки в службе приложений Azure, что набор hello формируется один раз для каждой виртуальной сети, к которому будут подключаться приложения hello.

Hello сертификаты будут уже заданы Если выполнены эти действия или интегрируется с hello же виртуальной сети с помощью портала hello.

Hello первым шагом является toogenerate hello CER-файл. второй шаг Hello — tooupload hello .cer файл tooyour виртуальной сети. toogenerate hello CER-файл из вызова hello API в hello предыдущих шага, выполните следующие команды hello.

    $certBytes = [System.Convert]::FromBase64String($vnet.Properties.certBlob)
    [System.IO.File]::WriteAllBytes("$($Configuration.GeneratedCertificatePath)", $certBytes)

Hello сертификат будет находится в папке hello, **$Configuration.GeneratedCertificatePath** указывает.

сертификат hello tooupload вручную, используйте hello [портал Azure] [ azureportal] и **Обзор виртуальной сети (классические)** > **VPN-подключений**  >  **Точки сайтами** > **Управление сертификатами**. Здесь можно отправить сертификат.

##### <a name="get-hello-point-to-site-package"></a>Получение пакета hello точка сеть
Hello следующим шагом в настройке подключения к виртуальной сети на веб-приложения является пакетом точки сайтами tooget hello и предоставить ему tooyour веб-приложения.

Сохраните hello следующий файл шаблона tooa вызывается GetNetworkPackageUri.json где-либо на компьютере, например, C:\Azure\Templates\GetNetworkPackageUri.json.

    {
        "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "certData": {
                "type": "string"
            },
            "certThumbprint": {
                "type": "string"
            },
            "networkName": {
                "type": "string"
            }
        },
        "variables": {
            "legacyVnetName": "[concat('Group ', resourceGroup().name, ' ', parameters('networkName'))]"
            },
            "resources": [
            ],
        "outputs" : {
            "PackageUri" :
            {
            "value" : "[listPackage(resourceId('Microsoft.ClassicNetwork/virtualNetworks/gateways/clientRootCertificates', parameters('networkName'), 'primary', parameters('certThumbprint')), '2014-06-01').packageUri]", "type" : "string"
            }
        }
    }


Задайте входные параметры.

    $parameters = @{"certData" = $vnet.Properties.certBlob ;
    certThumbprint = $vnet.Properties.certThumbprint ;
    "networkName" = $Configuration.VnetName }

Вызов скрипта hello:

    $output = New-AzureRmResourceGroupDeployment -Name unused -ResourceGroupName $Configuration.VnetResourceGroup -TemplateParameterObject $parameters -TemplateFile C:\PATH\TO\GetNetworkPackageUri.json


переменная приветствия **$output. Outputs.packageUri** теперь будет содержать toobe URI пакета hello, учитывая tooyour веб-приложения.

##### <a name="upload-hello-point-to-site-package-tooyour-app"></a>Отправка tooyour приложения hello пакета точка сеть
последним шагом Hello является приложение hello tooprovide с этим пакетом. Просто выполните hello следующей команды:

    $vnet = New-AzureRmResource -Name "$($Configuration.WebAppName)/$($Configuration.VnetName)/primary" -ResourceGroupName $Configuration.WebAppResourceGroup -ResourceType "Microsoft.Web/sites/virtualNetworkConnections/gateways" -ApiVersion 2015-07-01 -PropertyObject @{"VnetName" = $Configuration.VnetName ; "VpnPackageUri" = $($output.Outputs.packageUri).Value } -Location $Configuration.WebAppLocation

Если сообщение с запросом tooconfirm перезаписи существующего ресурса, убедитесь, что tooallow его.

После успешного выполнения этой команды, приложение должно быть toohello подключенной виртуальной сети. в случае успешного выполнения tooconfirm перейдите tooyour консольного приложения и введите ниже hello:

    SET WEBSITE_

Если переменной среды WEBSITE_VNETNAME со значением, совпадающим с именем hello hello целевой виртуальной сети, все конфигурации успешно выполнено.

### <a name="update-classic-vnet-integration-information"></a>Обновление сведений об интеграции с классической виртуальной сетью
tooupdate или повторной синхронизации информации, просто повторите действия hello, которая использовалась при создании hello интеграции на первом месте hello. К этим действиям относятся:

1. Определение данных конфигурации.
2. Объявите toohello приложение hello виртуальной сети.
3. Получение пакета точки сайтами hello.
4. Отправьте приложение tooyour hello точки сайтами пакета.

### <a name="disconnect-your-app-from-a-classic-vnet"></a>Отключение приложения от классической виртуальной сети
приложение hello toodisconnect, необходимо hello сведения о конфигурации, который был задан во время интеграции виртуальной сети. Используя эту информацию, нет нажмите одну команду toodisconnect приложения из виртуальной сети.

    $vnet = Remove-AzureRmResource -Name "$($Configuration.WebAppName)/$($Configuration.VnetName)" -ResourceGroupName $Configuration.WebAppResourceGroup -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-07-01

## <a name="resource-manager-virtual-networks"></a>Виртуальные сети Resource Manager
У виртуальных сетей Resource Manager есть интерфейсы API Azure Resource Manager, которые упрощают некоторые процессы по сравнению с классическими виртуальными сетями. У нас есть скрипт, который поможет вам выполнить hello следующие задачи:

* создать виртуальную сеть Resource Manager и интегрировать свое приложение с ней;
* создать шлюз, настроить подключение "точка — сеть" в созданной ранее виртуальной сети Resource Manager, а затем интегрировать свое приложение с ней;
* интегрировать свое приложение с созданной ранее виртуальной сетью Resource Manager, у которой есть шлюз и включенное подключение "точка — сеть";
* отключение приложения от виртуальной сети.

### <a name="resource-manager-vnet-app-service-integration-script"></a>Скрипт для интеграции службы приложений для виртуальной сети Resource Manager
Скопируйте hello следующий скрипт и сохраните его файл tooa. Если вы не хотите toouse hello скрипт, вы свободного toolearn от него toosee как tooset всех компонентов с помощью диспетчера ресурсов для виртуальной сети.

    function ReadHostWithDefault($message, $default)
    {
        $result = Read-Host "$message [$default]"
        if($result -eq "")
        {
            $result = $default
        }
            return $result
        }

    function PromptCustom($title, $optionValues, $optionDescriptions)
    {
        Write-Host $title
        Write-Host
        $a = @()
        for($i = 0; $i -lt $optionValues.Length; $i++){
            Write-Host "$($i+1))" $optionDescriptions[$i]
        }
        Write-Host

        while($true)
        {
            Write-Host "Choose an option: "
            $option = Read-Host
            $option = $option -as [int]

            if($option -ge 1 -and $option -le $optionValues.Length)
            {
                return $optionValues[$option-1]
            }
        }
    }

    function PromptYesNo($title, $message, $default = 0)
    {
        $yes = New-Object System.Management.Automation.Host.ChoiceDescription "&Yes", ""
        $no = New-Object System.Management.Automation.Host.ChoiceDescription "&No", ""
        $options = [System.Management.Automation.Host.ChoiceDescription[]]($yes, $no)
        $result = $host.ui.PromptForChoice($title, $message, $options, $default)
        return $result
    }

    function CreateVnet($resourceGroupName, $vnetName, $vnetAddressSpace, $vnetGatewayAddressSpace, $location)
    {
        Write-Host "Creating a new VNET"
        $gatewaySubnet = New-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix $vnetGatewayAddressSpace
        New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $resourceGroupName -Location $location -AddressPrefix $vnetAddressSpace -Subnet $gatewaySubnet
    }

    function CreateVnetGateway($resourceGroupName, $vnetName, $vnetIpName, $location, $vnetIpConfigName, $vnetGatewayName, $certificateData, $vnetPointToSiteAddressSpace)
    {
        $vnet = Get-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $resourceGroupName
        $subnet=Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet

        Write-Host "Creating a public IP address for this VNET"
        $pip = New-AzureRmPublicIpAddress -Name $vnetIpName -ResourceGroupName $resourceGroupName -Location $location -AllocationMethod Dynamic
        $ipconf = New-AzureRmVirtualNetworkGatewayIpConfig -Name $vnetIpConfigName -Subnet $subnet -PublicIpAddress $pip

        Write-Host "Adding a root certificate toothis VNET"
        $root = New-AzureRmVpnClientRootCertificate -Name "AppServiceCertificate.cer" -PublicCertData $certificateData

        Write-Host "Creating Azure VNET Gateway. This may take up tooan hour."
        New-AzureRmVirtualNetworkGateway -Name $vnetGatewayName -ResourceGroupName $resourceGroupName -Location $location -IpConfigurations $ipconf -GatewayType Vpn -VpnType RouteBased -EnableBgp $false -GatewaySku Basic -VpnClientAddressPool $vnetPointToSiteAddressSpace -VpnClientRootCertificates $root
    }

    function AddNewVnet($subscriptionId, $webAppResourceGroup, $webAppName)
    {
        Write-Host "Adding a new Vnet"
        Write-Host
        $vnetName = Read-Host "Specify a name for this Virtual Network"

        $vnetGatewayName="$($vnetName)-gateway"
        $vnetIpName="$($vnetName)-ip"
        $vnetIpConfigName="$($vnetName)-ipconf"

        # Virtual Network settings
        $vnetAddressSpace="10.0.0.0/8"
        $vnetGatewayAddressSpace="10.5.0.0/16"
        $vnetPointToSiteAddressSpace="172.16.0.0/16"

        $changeRequested = 0
        $resourceGroupName = $webAppResourceGroup

        while($changeRequested -eq 0)
        {
            Write-Host
            Write-Host "Currently, I will create a VNET with hello following settings:"
            Write-Host
            Write-Host "Virtual Network Name: $vnetName"
            Write-Host "Resource Group Name:  $resourceGroupName"
            Write-Host "Gateway Name: $vnetGatewayName"
            Write-Host "Vnet IP name: $vnetIpName"
            Write-Host "Vnet IP config name:  $vnetIpConfigName"
            Write-Host "Address Space:$vnetAddressSpace"
            Write-Host "Gateway Address Space:$vnetGatewayAddressSpace"
            Write-Host "Point-To-Site Address Space:  $vnetPointToSiteAddressSpace"
            Write-Host
            $changeRequested = PromptYesNo "" "Do you wish toochange these settings?" 1

            if($changeRequested -eq 0)
            {
                $vnetName = ReadHostWithDefault "Virtual Network Name" $vnetName
                $resourceGroupName = ReadHostWithDefault "Resource Group Name" $resourceGroupName
                $vnetGatewayName = ReadHostWithDefault "Vnet Gateway Name" $vnetGatewayName
                $vnetIpName = ReadHostWithDefault "Vnet IP name" $vnetIpName
                $vnetIpConfigName = ReadHostWithDefault "Vnet IP configuration name" $vnetIpConfigName
                $vnetAddressSpace = ReadHostWithDefault "Vnet Address Space" $vnetAddressSpace
                $vnetGatewayAddressSpace = ReadHostWithDefault "Vnet Gateway Address Space" $vnetGatewayAddressSpace
                $vnetPointToSiteAddressSpace = ReadHostWithDefault "Vnet Point-to-site Address Space" $vnetPointToSiteAddressSpace
            }
        }

        $ErrorActionPreference = "Stop";

        # We create hello virtual network and add it here. hello way this works is:
        # 1) Add hello VNET association toohello App. This allows hello App toogenerate certificates, etc. for hello VNET.
        # 2) Create hello VNET and VNET gateway, add hello certificates, create hello public IP, etc., required for hello gateway
        # 3) Get hello VPN package from hello gateway and pass it back toohello App.

        $webApp = Get-AzureRmResource -ResourceName $webAppName -ResourceType "Microsoft.Web/sites" -ApiVersion 2015-08-01 -ResourceGroupName $webAppResourceGroup
        $location = $webApp.Location

        Write-Host "Creating App association tooVNET"
        $propertiesObject = @{
         "vnetResourceId" = "/subscriptions/$($subscriptionId)/resourceGroups/$($resourceGroupName)/providers/Microsoft.Network/virtualNetworks/$($vnetName)"
        }
        $virtualNetwork = New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnetName)" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-08-01 -ResourceGroupName $webAppResourceGroup -Force

        CreateVnet $resourceGroupName $vnetName $vnetAddressSpace $vnetGatewayAddressSpace $location

        CreateVnetGateway $resourceGroupName $vnetName $vnetIpName $location $vnetIpConfigName $vnetGatewayName $virtualNetwork.Properties.CertBlob $vnetPointToSiteAddressSpace

        Write-Host "Retrieving VPN Package and supplying tooApp"
        $packageUri = Get-AzureRmVpnClientPackage -ResourceGroupName $resourceGroupName -VirtualNetworkGatewayName $vnetGatewayName -ProcessorArchitecture Amd64
        
        # $packageUri may contain literal double-quotes at hello start and hello end of hello URL
        if($packageUri.Length -gt 0 -and $packageUri.Substring(0, 1) -eq '"' -and $packageUri.Substring($packageUri.Length - 1, 1) -eq '"')
        {
            $packageUri = $packageUri.Substring(1, $packageUri.Length - 2)
        }

        # Put hello VPN client configuration package onto hello App
        $PropertiesObject = @{
        "vnetName" = $VirtualNetworkName; "vpnPackageUri" = $packageUri
        }

        New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnetName)/primary" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections/gateways" -ApiVersion 2015-08-01 -ResourceGroupName $webAppResourceGroup -Force

        Write-Host "Finished!"
    }

    function AddExistingVnet($subscriptionId, $resourceGroupName, $webAppName)
    {
        $ErrorActionPreference = "Stop";

        # At this point, hello gateway should be able toobe joined tooan App, but may require some minor tweaking. We will declare toohello App now toouse this VNET
        Write-Host "Getting App information"
        $webApp = Get-AzureRmResource -ResourceName $webAppName -ResourceType "Microsoft.Web/sites" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName
        $location = $webApp.Location

        $webAppConfig = Get-AzureRmResource -ResourceName "$($webAppName)/web" -ResourceType "Microsoft.Web/sites/config" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName
        $currentVnet = $webAppConfig.Properties.VnetName
        if($currentVnet -ne $null -and $currentVnet -ne "")
        {
            Write-Host "Currently connected tooVNET $currentVnet"
        }

        # Display existing vnets
        $vnets = Get-AzureRmVirtualNetwork
        $vnetNames = @()
        foreach($vnet in $vnets)
        {
            $vnetNames += $vnet.Name
        }

        Write-Host
        $vnet = PromptCustom "Select a VNET toointegrate with" $vnets $vnetNames

        # We need toocheck if this VNET is able toobe joined tooa App, based on following criteria
            # If there is no gateway, we can create one.
            # If there is a gateway:
                # It must be of type Vpn
                # It must be of VpnType RouteBased
                # If it doesn't have hello right certificate, we will need tooadd it.
                # If it doesn't have a point-to-site range, we will need tooadd it.

        $gatewaySubnet = $vnet.Subnets | Where-Object { $_.Name -eq "GatewaySubnet" }

        if($gatewaySubnet -eq $null -or $gatewaySubnet.IpConfigurations -eq $null -or $gatewaySubnet.IpConfigurations.Count -eq 0)
        {
            $ErrorActionPreference = "Continue";
            # There is no gateway. We need toocreate one.
            Write-Host "This Virtual Network has no gateway. I will need toocreate one."

            $vnetName = $vnet.Name
            $vnetGatewayName="$($vnetName)-gateway"
            $vnetIpName="$($vnetName)-ip"
            $vnetIpConfigName="$($vnetName)-ipconf"

            # Virtual Network settings
            $vnetAddressSpace="10.0.0.0/8"
            $vnetGatewayAddressSpace="10.5.0.0/16"
            $vnetPointToSiteAddressSpace="172.16.0.0/16"

            $changeRequested = 0

            Write-Host "Your VNET is in hello address space $($vnet.AddressSpace.AddressPrefixes), with hello following Subnets:"
            foreach($subnet in $vnet.Subnets)
            {
                Write-Host "$($subnet.Name): $($subnet.AddressPrefix)"
            }

            $vnetGatewayAddressSpace = Read-Host "Please choose a GatewaySubnet address space"

            while($changeRequested -eq 0)
            {
                Write-Host
                Write-Host "Currently, I will create a VNET gateway with hello following settings:"
                Write-Host
                Write-Host "Virtual Network Name: $vnetName"
                Write-Host "Resource Group Name:  $($vnet.ResourceGroupName)"
                Write-Host "Gateway Name: $vnetGatewayName"
                Write-Host "Vnet IP name: $vnetIpName"
                Write-Host "Vnet IP config name:  $vnetIpConfigName"
                Write-Host "Address Space:$($vnet.AddressSpace.AddressPrefixes)"
                Write-Host "Gateway Address Space:$vnetGatewayAddressSpace"
                Write-Host "Point-To-Site Address Space:  $vnetPointToSiteAddressSpace"
                Write-Host
                $changeRequested = PromptYesNo "" "Do you wish toochange these settings?" 1

                if($changeRequested -eq 0)
                {
                    $vnetGatewayName = ReadHostWithDefault "Vnet Gateway Name" $vnetGatewayName
                    $vnetIpName = ReadHostWithDefault "Vnet IP name" $vnetIpName
                    $vnetIpConfigName = ReadHostWithDefault "Vnet IP configuration name" $vnetIpConfigName
                    $vnetGatewayAddressSpace = ReadHostWithDefault "Vnet Gateway Address Space" $vnetGatewayAddressSpace
                    $vnetPointToSiteAddressSpace = ReadHostWithDefault "Vnet Point-to-site Address Space" $vnetPointToSiteAddressSpace
                }
            }

            $ErrorActionPreference = "Stop";

            Write-Host "Creating App association tooVNET"
            $propertiesObject = @{
             "vnetResourceId" = "/subscriptions/$($subscriptionId)/resourceGroups/$($vnet.ResourceGroupName)/providers/Microsoft.Network/virtualNetworks/$($vnetName)"
            }

            $virtualNetwork = New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnet.Name)" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName -Force

            # If there is no gateway subnet, we need toocreate one.
            if($gatewaySubnet -eq $null)
            {
                $gatewaySubnet = New-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix $vnetGatewayAddressSpace
                $vnet.Subnets.Add($gatewaySubnet);
                Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
            }

            CreateVnetGateway $vnet.ResourceGroupName $vnetName $vnetIpName $location $vnetIpConfigName $vnetGatewayName $virtualNetwork.Properties.CertBlob $vnetPointToSiteAddressSpace

            $gateway = Get-AzureRmVirtualNetworkGateway -ResourceGroupName $vnet.ResourceGroupName -Name $vnetGatewayName
        }
        else
        {
            $uriParts = $gatewaySubnet.IpConfigurations[0].Id.Split('/')
            $gatewayResourceGroup = $uriParts[4]
            $gatewayName = $uriParts[8]

            $gateway = Get-AzureRmVirtualNetworkGateway -ResourceGroupName $vnet.ResourceGroupName -Name $gatewayName

            # validate gateway types, etc.
            if($gateway.GatewayType -ne "Vpn")
            {
                Write-Error "This gateway is not of hello Vpn type. It cannot be joined tooan App."
                return
            }

            if($gateway.VpnType -ne "RouteBased")
            {
                Write-Error "This gateways Vpn type is not RouteBased. It cannot be joined tooan App."
                return
            }

            if($gateway.VpnClientConfiguration -eq $null -or $gateway.VpnClientConfiguration.VpnClientAddressPool -eq $null)
            {
                Write-Host "This gateway does not have a Point-to-site Address Range. Please specify one in CIDR notation, e.g. 10.0.0.0/8"
                $pointToSiteAddress = Read-Host "Point-To-Site Address Space"
                Set-AzureRmVirtualNetworkGatewayVpnClientConfig -VirtualNetworkGateway $gateway.Name -VpnClientAddressPool $pointToSiteAddress
            }

            Write-Host "Creating App association tooVNET"
            $propertiesObject = @{
             "vnetResourceId" = "/subscriptions/$($subscriptionId)/resourceGroups/$($vnet.ResourceGroupName)/providers/Microsoft.Network/virtualNetworks/$($vnet.Name)"
            }

            $virtualNetwork = New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnet.Name)" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName -Force

            # We need toocheck if hello certificate here exists in hello gateway.
            $certificates = $gateway.VpnClientConfiguration.VpnClientRootCertificates

            $certFound = $false
            foreach($certificate in $certificates)
            {
                if($certificate.PublicCertData -eq $virtualNetwork.Properties.CertBlob)
                {
                    $certFound = $true
                    break
                }
            }

            if(-not $certFound)
            {
                Write-Host "Adding certificate"
                Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName "AppServiceCertificate.cer" -PublicCertData $virtualNetwork.Properties.CertBlob -VirtualNetworkGatewayName $gateway.Name
            }
        }

        # Now finish joining by getting hello VPN package and giving it toohello App
        Write-Host "Retrieving VPN Package and supplying tooApp"
        $packageUri = Get-AzureRmVpnClientPackage -ResourceGroupName $vnet.ResourceGroupName -VirtualNetworkGatewayName $gateway.Name -ProcessorArchitecture Amd64
        
        # $packageUri may contain literal double-quotes at hello start and hello end of hello URL
        if($packageUri.Length -gt 0 -and $packageUri.Substring(0, 1) -eq '"' -and $packageUri.Substring($packageUri.Length - 1, 1) -eq '"')
        {
            $packageUri = $packageUri.Substring(1, $packageUri.Length - 2)
        }

        # Put hello VPN client configuration package onto hello App
        $PropertiesObject = @{
        "vnetName" = $vnet.Name; "vpnPackageUri" = $packageUri
        }

        New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnet.Name)/primary" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections/gateways" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName -Force

        Write-Host "Finished!"
    }

    function RemoveVnet($subscriptionId, $resourceGroupName, $webAppName)
    {
        $webAppConfig = Get-AzureRmResource -ResourceName "$($webAppName)/web" -ResourceType "Microsoft.Web/sites/config" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName
        $currentVnet = $webAppConfig.Properties.VnetName
        if($currentVnet -ne $null -and $currentVnet -ne "")
        {
            Write-Host "Currently connected tooVNET $currentVnet"

            Remove-AzureRmResource -ResourceName "$($webAppName)/$($currentVnet)" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName
        }
            else
        {
            Write-Host "Not connected tooa VNET."
        }
    }

    Write-Host "Please Login"
    Login-AzureRmAccount

    # Choose subscription. If there's only one we will choose automatically

    $subs = Get-AzureRmSubscription
    $subscriptionId = ""

    if($subs.Length -eq 0)
    {
        Write-Error "No subscriptions bound toothis account."
        return
    }

    if($subs.Length -eq 1)
    {
        $subscriptionId = $subs[0].SubscriptionId
    }
    else
    {
        $subscriptionChoices = @()
        $subscriptionValues = @()

        foreach($subscription in $subs){
        $subscriptionChoices += "$($subscription.SubscriptionName) ($($subscription.SubscriptionId))";
        $subscriptionValues += ($subscription.SubscriptionId);
        }

        $subscriptionId = PromptCustom "Choose a subscription" $subscriptionValues $subscriptionChoices
    }

    Select-AzureRmSubscription -SubscriptionId $subscriptionId

    $resourceGroup = Read-Host "Please enter hello Resource Group of your App"

    $appName = Read-Host "Please enter hello Name of your App"

    $options = @("Add a NEW Virtual Network tooan App", "Add an EXISTING Virtual Network tooan App", "Remove a Virtual Network from an App");
    $optionValues = @(0, 1, 2)
    $option = PromptCustom "What do you want toodo?" $optionValues $options

    if($option -eq 0)
    {
        AddNewVnet $subscriptionId $resourceGroup $appName
    }
    if($option -eq 1)
    {
        AddExistingVnet $subscriptionId $resourceGroup $appName
    }
    if($option -eq 2)
    {
        RemoveVnet $subscriptionId $resourceGroup $appName
    }

Сохраните копию скрипта hello. В этой статье он называется V2VnetAllinOne.ps1, но можно использовать другое имя. Для этого сценария не нужно указывать никаких аргументов. Просто запустите его. Hello первое, что скрипт hello будет выполнять является toosign в запрос. После входа в скрипт hello получает сведения о вашей учетной записи и возвращает список подписок. Не считая hello запрос учетных данных, выполнения начального сценария hello выглядит следующим образом:

    PS C:\Users\ccompy\Documents\VNET> .\V2VnetAllInOne.ps1
    Please Login

    Environment           : AzureCloud
    Account               : ccompy@microsoft.com
    TenantId              : 722278f-fef1-499f-91ab-2323d011db47
    SubscriptionId        : af5358e1-acac-2c90-a9eb-722190abf47a
    CurrentStorageAccount :

    Choose a subscription

    1) Demo Subscription (af5358e1-acac-2c90-a9eb-722190abf47a)
    2) MS Test (a5350f55-dd5a-41ec-2ddb-ff7b911bb2ef)
    3) Purple Demo Subscription (2d4c99a4-57f9-4d5e-a0a1-0034c52db59d)

    Выберите вариант: 3

    Учетная запись      : ccompy@microsoft.com Среда  : AzureCloud Подписка : 2d4c99a4-57f9-4d5e-a0a1-0034c52db59d Клиент       : 722278f-fef1-499f-91ab-2323d011db47

    Введите группу ресурсов приложения hello: hcdemo rg введите имя приложения hello: v2vnetpowershell что вам требуется toodo?

    1) Добавить новую виртуальную сеть tooan приложения
    2) Добавление СУЩЕСТВУЮЩЕЙ виртуальной сети tooan приложения
    3) Удаление виртуальной сети из приложения

Hello оставшейся части этого раздела описана каждая из этих трех параметров.

### <a name="create-a-resource-manager-vnet-and-integrate-with-it"></a>Создание виртуальной сети Resource Manager и интеграция с ней
Выберите новую виртуальную сеть, использует hello модели развертывания диспетчера ресурсов и интегрировать его с вашим приложением toocreate **1) добавьте новую виртуальную сеть tooan приложения**. Это предложит ввести имя hello hello виртуальной сети. В моем случае как видно в hello следующие параметры, я использовал имя hello, v2pshell.

сценарий Hello подробно описывает hello hello виртуальной сети, которая находится в процессе создания. Если я хочу ли изменения любых значений hello. При выполнении этого примера я создал виртуальной сети, которая имеет hello следующие параметры:

    Virtual Network Name:         v2pshell
    Resource Group Name:          hcdemo-rg
    Gateway Name:                 v2pshell-gateway
    Vnet IP name:                 v2pshell-ip
    Vnet IP config name:          v2pshell-ipconf
    Address Space:                10.0.0.0/8
    Gateway Address Space:        10.5.0.0/16
    Point-To-Site Address Space:  172.16.0.0/12

    Do you wish toochange these settings?
    [Y] Yes  [N] No  [?] Help (default is "N"):

Toochange любых значений hello, введите **Y** и внесите изменения hello. Когда будет удовлетворен hello параметры виртуальной сети, введите **N** или просто нажмите клавишу ВВОД, ответ на запрос об изменении параметров hello. Отсюда до ее завершения, скрипт hello сообщает некоторые ею "буквами" i ", выполнив до начала шлюз виртуальной сети toocreate hello. Этот шаг может занять час tooan. Отсутствует на этом этапе не индикатор хода выполнения, но сценарий hello позволит узнать, был ли создан шлюз hello.

По завершении сценария hello укажет **завершен**. На этом этапе будет создана диспетчера ресурсов виртуальной сети, которая имеет имя hello и выбранные параметры. Эта новая виртуальная сеть также будет интегрирована с приложением.

### <a name="integrate-your-app-with-a-preexisting-resource-manager-vnet"></a>Интеграция приложения с созданной ранее виртуальной сетью Resource Manager
При интегрируете с существующие ранее виртуальной сети, если диспетчер ресурсов виртуальной сети, у которого нет шлюза или подключение точка сеть, hello скрипт будет настроить это подключение. Если hello виртуальная сеть уже тем элементам, Настройка, скрипт hello переходит toohello прямой интеграцией приложений. toostart этот процесс, просто выберите **2) добавьте СУЩЕСТВУЮЩУЮ виртуальную сеть tooan приложения**.

Этот параметр работает только в том случае, если имеется уже существующий диспетчер ресурсов виртуальной сети, которая находится в hello той же подписке, ваше приложение. После выбора параметра hello, появится список виртуальных сетей диспетчера ресурсов.   

    Select a VNET toointegrate with

    1) v2demonetwork
    2) v2pshell
    3) v2vnetintdemo
    4) v2asenetwork
    5) v2pshell2

    Выберите вариант: 5

Просто выберите hello виртуальную сеть, которую вы хотите toointegrate с. При наличии шлюза с подключением точки сайтами включена hello скрипт просто интегрировать приложения виртуальной сети. Если у вас шлюз, необходимо будет подсеть шлюза toospecify hello. Подсеть шлюза должна находиться в адресном пространстве виртуальной сети и не может находиться ни в какой другой подсети. При выполнении этого шага для виртуальной сети без шлюза вы получите следующий результат:

    This Virtual Network has no gateway. I will need toocreate one.
    Your VNET is in hello address space 172.16.0.0/16, with hello following Subnets:
    default: 172.16.0.0/24
    Please choose a GatewaySubnet address space: 172.16.1.0/26

В этом примере создан шлюз виртуальной сети, имеющий hello следующие параметры:

    Virtual Network Name:         v2pshell2
    Resource Group Name:          vnetdemo-rg
    Gateway Name:                 v2pshell2-gateway
    Vnet IP name:                 v2pshell2-ip
    Vnet IP config name:          v2pshell2-ipconf
    Address Space:                172.16.0.0/16
    Gateway Address Space:        172.16.1.0/26
    Point-To-Site Address Space:  172.16.0.0/12

    Do you wish toochange these settings?
    [Y] Yes  [N] No  [?] Help (default is "N"):
    Creating App association tooVNET

Если требуется toochange любой из этих параметров, это можно сделать. В противном случае нажмите клавишу ВВОД и создаст шлюза и присоединить виртуальную сеть tooyour приложения hello скрипта. время создания шлюза Hello по-прежнему один час, однако, поэтому убедитесь, что, следует учитывать. По окончании все, что скрипт hello укажет **завершен**.

### <a name="disconnect-your-app-from-a-resource-manager-vnet"></a>Отключение приложения от виртуальной сети Resource Manager
Отключение приложение от виртуальной сети не остановить работу шлюза hello и отключить подключение точка сеть. В конце концов, их можно использовать и для других целей. Он также не отключить его от других приложений, отличный от hello, который вы указали. tooperform это действие, выберите **3) удалить виртуальную сеть из приложения**. При выборе этого варианта вы увидите следующее:

    Currently connected tooVNET v2pshell

    Confirm
    Are you sure you want toodelete hello following resource:
    /subscriptions/edcc99a4-b7f9-4b5e-a9a1-3034c51db496/resourceGroups/hcdemo-rg/providers/Microsoft.Web/sites/v2vnetpowers
    hell/virtualNetworkConnections/v2pshell
    [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"):

Несмотря на то, что скрипт hello говорит delete, не удаляя hello виртуальной сети. Он лишь удаляет hello интеграции. Убедившись, что это желаемый toodo, команда hello обрабатывается довольно быстро и сообщает, **True** после его завершения.

<!--Links-->
[createvpngateway]: http://azure.microsoft.com/documentation/articles/vpn-gateway-point-to-site-create/
[azureportal]: http://portal.azure.com
