---
title: "aaaCreate виртуальная сеть | Шаблон диспетчера ресурсов Azure | Документы Microsoft"
description: "Узнайте, как toocreate в виртуальной сети с помощью шаблона диспетчера ресурсов Azure."
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 69530861-2f97-4a6e-b336-a7baf2690044
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b9c289433ff2a84bec19eac25fa28ab40d131c7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-using-an-azure-resource-manager-template"></a>Создание виртуальной сети с использованием шаблона Azure Resource Manager

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

Azure предоставляет две модели развертывания: с помощью Azure Resource Manager и классическую. Корпорация Майкрософт рекомендует создать ресурсы с помощью модели развертывания диспетчера ресурсов hello. Дополнительные сведения о toolearn hello различий между моделями hello двух чтения hello [модели развертывания Azure понять](../azure-resource-manager/resource-manager-deployment-model.md) статьи.
 
В этой статье объясняется, как toocreate виртуальной сети путем развертывания диспетчера ресурсов hello модели с помощью шаблона диспетчера ресурсов Azure. Также можно создать виртуальную сеть через диспетчер ресурсов с помощью других средств или создайте виртуальную сеть через hello классической модели развертывания, выбрав другой вариант hello после списка:

> [!div class="op_single_selector"]
- [Портал](virtual-networks-create-vnet-arm-pportal.md)
- [PowerShell](virtual-networks-create-vnet-arm-ps.md)
- [ИНТЕРФЕЙС КОМАНДНОЙ СТРОКИ](virtual-networks-create-vnet-arm-cli.md)
- [Шаблон](virtual-networks-create-vnet-arm-template-click.md)
- [Портал (классический)](virtual-networks-create-vnet-classic-pportal.md)
- [PowerShell (классическая модель)](virtual-networks-create-vnet-classic-netcfg-ps.md)
- [Интерфейс командной строки (классическая модель)](virtual-networks-create-vnet-classic-cli.md)

Вы узнаете, как toodownload и изменить существующий шаблон ARM из GitHub и развертывания шаблона hello из GitHub, PowerShell и hello Azure CLI.

При развертывании шаблона hello ARM непосредственно из GitHub, без изменений, просто пропустите слишком[развертывания шаблона из github](#deploy-the-arm-template-by-using-click-to-deploy).

[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]

## <a name="download-and-understand-hello-azure-resource-manager-template"></a>Загрузите и понять hello шаблона диспетчера ресурсов Azure
Можно загрузить hello существующего шаблона для создания виртуальной сети и две подсети из GitHub, внесите изменения можно будет и использовать его. toodo таким образом, выполните следующие шаги hello.

1. Перейдите в слишком[страницы шаблона образец hello](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets).
2. Щелкните **azuredeploy.json** и нажмите кнопку **RAW**.
3. Сохраните файл tooa hello локальную папку на локальном компьютере.
4. Если вы знакомы с шаблонами, пропустите toostep 7.
5. Откройте только что сохраненный файл hello и просмотрите содержимое hello под **параметры** в строке 5. Параметры шаблона ARM предоставляют заполнитель для значений, которые могут заполняться во время развертывания.
   
   | Параметр | Описание |
   | --- | --- |
   | **расположение** |Регион Azure, где будут создаваться hello виртуальной сети |
   | **vnetName** |Имя для hello новой виртуальной сети |
   | **addressPrefix** |Адресное пространство для hello виртуальной сети, в формате CIDR |
   | **subnet1Name** |Имя для hello первой виртуальной сети |
   | **subnet1Prefix** |Блок CIDR для hello первая подсеть |
   | **subnet2Name** |Имя для hello второй виртуальной сети |
   | **subnet2Prefix** |Блок CIDR для второй подсети hello |
   
   > [!IMPORTANT]
   > Шаблоны ARM, хранящиеся в GitHub, со временем могут изменяться. Убедитесь, что проверка hello шаблона перед его использованием.
   > 
   > 
6. Проверьте содержимое hello в **ресурсов** и обратите внимание, hello следующее:
   
   * **type**. Тип ресурса, создаваемого шаблоном hello. В данном случае это тип **Microsoft.Network/virtualNetworks**, который представляют виртуальную сеть.
   * **name**. Имя ресурса hello. Использование уведомления hello **[parameters('vnetName')]**, который означает hello имя будут указаны во входных данных hello пользователем или в файле параметров во время развертывания.
   * **properties**. Список свойств для ресурса hello. Этот шаблон использует свойства пространства и подсети адреса hello во время создания виртуальной сети.
7. Переход назад слишком[страницы шаблона образец hello](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets).
8. Щелкните **azuredeploy paremeters.json** и нажмите кнопку **RAW**.
9. Сохраните файл tooa hello локальную папку на локальном компьютере.
10. Откройте только что сохраненный файл hello и отредактируйте hello значения для параметров hello. Используйте следующие значения ниже toodeploy hello виртуальной сети в сценарии hello hello.

    ```json
        {
          "location": {
            "value": "Central US"
          },
          "vnetName": {
              "value": "TestVNet"
          },
          "addressPrefix": {
              "value": "192.168.0.0/16"
          },
          "subnet1Name": {
              "value": "FrontEnd"
          },
          "subnet1Prefix": {
            "value": "192.168.1.0/24"
          },
          "subnet2Name": {
              "value": "BackEnd"
          },
          "subnet2Prefix": {
              "value": "192.168.2.0/24"
          }
        }
    ```

11. Сохраните файл hello.


## <a name="deploy-hello-template-using-powershell"></a>Развертывание шаблона hello, с помощью PowerShell

Выполните следующие шаги toodeploy hello загруженный шаблон с помощью PowerShell hello.

1. Установка и настройка Azure PowerShell, выполнив шаги hello в hello [как tooInstall и настройка Azure PowerShell](/powershell/azure/overview) статьи.
2. Выполните следующие команды toocreate hello новой группы ресурсов:

    ```powershell
    New-AzureRmResourceGroup -Name TestRG -Location centralus
    ```

    Команда Hello создает группу ресурсов с именем *TestRG* в hello *центральной части США* регион azure. Дополнительные сведения о группах ресурсов см. в разделе "Группы ресурсов" [обзора Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).

    Ожидаемые выходные данные:

        ResourceGroupName : TestRG
        Location          : centralus
        ProvisioningState : Succeeded
        Tags              :
        Permissions       :
                            Actions  NotActions
                            =======  ==========
                            *
        ResourceId        : /subscriptions/[Id]/resourceGroups/TestRG

3. Выполните следующую команду, toodeploy hello новой виртуальной сети с помощью hello файлы шаблонов и параметров загрузки и изменения выше hello.

    ```powershell
    New-AzureRmResourceGroupDeployment -Name TestVNetDeployment -ResourceGroupName TestRG `
    -TemplateFile C:\ARM\azuredeploy.json -TemplateParameterFile C:\ARM\azuredeploy-parameters.json
    ```

    Ожидаемые выходные данные:
   
        DeploymentName    : TestVNetDeployment
        ResourceGroupName : TestRG
        ProvisioningState : Succeeded
        Timestamp         : [Date and time]
        Mode              : Incremental
        TemplateLink      :
        Parameters        :
                            Name             Type                       Value
                            ===============  =========================  ==========
                            location         String                     Central US
                            vnetName         String                     TestVNet
                            addressPrefix    String                     192.168.0.0/16
                            subnet1Prefix    String                     192.168.1.0/24
                            subnet1Name      String                     FrontEnd
                            subnet2Prefix    String                     192.168.2.0/24
                            subnet2Name      String                     BackEnd
   
        Outputs           :
4. Выполнения hello следующая команда свойства hello tooview hello новой виртуальной сети:

    ```powershell
    Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
    ```

    Ожидаемые выходные данные:

        Name              : TestVNet
        ResourceGroupName : TestRG
        Location          : centralus
        Id                : /subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet
        Etag              : W/"[Id]"
        ProvisioningState : Succeeded
        Tags              :
        AddressSpace      : {
                              "AddressPrefixes": [
                                "192.168.0.0/16"
                              ]
                            }
        DhcpOptions       : {
                              "DnsServers": null
                            }
        NetworkInterfaces : null
        Subnets           : [
                              {
                                "Name": "FrontEnd",
                                "Etag": "W/\"[Id]\"",
                                "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                                "AddressPrefix": "192.168.1.0/24",
                                "IpConfigurations": [],
                                "NetworkSecurityGroup": null,
                                "RouteTable": null,
                                "ProvisioningState": "Succeeded"
                              },
                              {
                                "Name": "BackEnd",
                                "Etag": "W/\"[Id]\"",
                                "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/BackEnd",
                                "AddressPrefix": "192.168.2.0/24",
                                "IpConfigurations": [],
                                "NetworkSecurityGroup": null,
                                "RouteTable": null,
                                "ProvisioningState": "Succeeded"
                              }
                            ]

## <a name="deploy-hello-template-using-click-to-deploy"></a>Развертывание с помощью нажмите кнопку развертывания шаблона hello

Можно повторно использовать поддерживается корпорацией Майкрософт и сообщества откройте toohello репозитории отправленного tooa GitHub предварительно определенных диспетчера ресурсов Azure шаблонов. Эти шаблоны можно развертывать из GitHub, или загружаются и изменить toofit вашим потребностям. toodeploy шаблон, который создает виртуальную сеть с двумя подсетями завершения hello, следующие шаги:

1. В браузере перейдите слишком[https://github.com/Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates).
2. Прокрутите вниз список шаблонов hello и нажмите **101 виртуальной сети 2 подсети**. Проверьте hello **README.md** файла, как показано ниже.

    ![Файл README.md в Github](./media/virtual-networks-create-vnet-arm-template-click-include/figure1.png)

3. Нажмите кнопку **развертывание tooAzure**. При необходимости введите учетные данные для входа в Azure. 
4. В hello **параметры** колонки, введите значения hello вы toouse toocreate в новую виртуальную сеть и нажмите кнопку **ОК**. Hello на этом рисунке показаны значения hello для hello сценария:
   
    ![Параметры шаблона ARM](./media/virtual-networks-create-vnet-arm-template-click-include/figure2.png)

5. Нажмите кнопку **группы ресурсов** и выберите tooadd группы ресурсов виртуальной сети для hello, или нажмите кнопку **создать новый** tooadd hello виртуальной сети tooa новую группу ресурсов. Hello на этом рисунке показан hello ресурс группы параметры для новой группы ресурсов с именем **TestRG**:

    ![Группа ресурсов](./media/virtual-networks-create-vnet-arm-template-click-include/figure3.png)

6. При необходимости измените hello **подписки** и **расположение** параметры для виртуальной сети.
7. Если требуется запретить toosee hello виртуальной сети в качестве плитки в hello **начальной панели**, отключите **tooStartboard ПИН-кода**.
8. Нажмите кнопку **условия**, ознакомьтесь с условиями hello и нажмите кнопку **купить** tooagree. 
9. Нажмите кнопку **создать** toocreate hello виртуальной сети.
   
    ![Отправка элемента развертывания в портал предварительной версии](./media/virtual-networks-create-vnet-arm-template-click-include/figure4.png)

10. После завершения развертывания hello в hello портал Azure нажмите кнопку **дополнительные службы**, тип *виртуальных сетей* hello поле фильтра, которое появляется, а затем нажмите кнопку виртуальных сетей toosee hello виртуальных сетей колонку. В колонке hello щелкните *TestVNet*. В hello *TestVNet* колонка, щелкните **подсетей** toosee hello создан подсетях, как показано в следующий рисунок hello:
    
     ![Создание виртуальной сети в портале предварительной версии](./media/virtual-networks-create-vnet-arm-template-click-include/figure5.png)

## <a name="next-steps"></a>Дальнейшие действия

Узнайте, как tooconnect:

- Виртуальная сеть виртуальной машины (VM) tooa путем чтения hello [создания виртуальной Машины Windows](../virtual-machines/virtual-machines-windows-hero-tutorial.md) или [создания виртуальной Машины Linux](../virtual-machines/linux/quick-create-portal.md) статей. Вместо создания виртуальной сети и подсети в шагах hello hello статей, можно выбрать существующей виртуальной сети и подсети tooconnect для виртуальной Машины.
- Здравствуйте, считывая hello виртуальных сетей в виртуальной сети tooother [подключение виртуальных сетей](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md) статьи.
- tooan Hello виртуальной сети в локальной сети с помощью виртуальной частной сети сеть сеть (VPN) или канал ExpressRoute. Дополнительные сведения в разделе hello [подключения локальной сети tooan виртуальной сети с помощью VPN сайтами](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) и [связывание виртуальной сети tooan канал ExpressRoute](../expressroute/expressroute-howto-linkvnet-arm.md) статей.
