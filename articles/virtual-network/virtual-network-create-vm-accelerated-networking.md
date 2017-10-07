---
title: "виртуальной машине Azure с помощью Accelerated сетевых aaaCreate | Документы Microsoft"
description: "Узнайте, как toocreate виртуальную машину с Accelerated работа по сети."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/10/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 241362891bfe083ab32c2f558be54f63f87c0693
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-with-accelerated-networking"></a>Создание виртуальной машины с ускоренной сетью

В этом учебнике вы узнаете, как toocreate виртуальной машины (ВМ) Azure с Accelerated работа по сети. Ускорение работы в сети — общедоступно для Windows и для определенных дистрибутивов Linux (общедоступная предварительная версия). Ускорение сеть позволяет tooa виртуализацию SR-IOV один корневой ввода-вывода виртуальной Машины, значительно повышает его производительность сети. Этот путь высокой производительности обходит hello узла из пути к данным hello, уменьшение задержки, флуктуации и использования ЦП, для использования с hello наиболее ресурсоемких рабочих нагрузок сети на поддерживаемых типов ВМ. Следующий рисунок показывает связи между две виртуальные машины (VM) с и без поддержки сети ускорителем Hello:

![Сравнение](./media/virtual-network-create-vm-accelerated-networking/image1.png)

Без поддержки ускорителем сети все сетевого трафика и из него hello ВМ необходимо проходить по hello узла и виртуального коммутатора hello. Hello виртуальный коммутатор предоставляет все применение политики, такой как сетевых групп безопасности, доступ к данным списков управления, изоляции и другой трафик toonetwork службы виртуальной сети. Дополнительные сведения о виртуальных коммутаторов, чтение hello toolearn [виртуализации сети Hyper-V и виртуального коммутатора](https://technet.microsoft.com/library/jj945275.aspx) статьи.

С ускорителем сетями сетевой трафик поступает на виртуальной Машине hello сетевого интерфейса (NIC) и пересылаются toohello виртуальной Машины. Все сетевые политики, которые hello виртуального коммутатора применяется без ускорителем сети являются прямой и применяется в оборудовании. Применение политики в оборудования позволяет hello Сетевых tooforward сетевой трафик непосредственно toohello ВМ, минуя hello узла и виртуального коммутатора hello, сохраняя все hello политику, которую он применяется в узле hello.

Hello преимущества ускорителем сети применяются только toohello виртуальной Машине, которая была включена. Для получения наилучших результатов hello это идеальный tooenable этой функции для по крайней мере две виртуальные машины подключены toohello одной виртуальной сети Azure (VNet). При обмене данными между виртуальными сетями или подключении в локальной, эта функция имеет минимальное влияние toooverall задержку.

> [!WARNING]
> Это Linux общедоступной предварительной версии не может иметь одинаковый уровень доступности и надежности, как и в случае функций, которые hello в целом общедоступный выпуск. функция Hello не поддерживается, могут ограничены возможности и могут быть доступны не во всех расположений в Azure. Hello последних уведомлений на доступность и состояние этой функцией проверьте страницу обновления виртуальной сети Azure hello.

## <a name="benefits"></a>Преимущества
* **Более низкая задержка или более поздней версии пакетов в секунду (pps):** удаление hello виртуальный коммутатор из пути к данным hello удаляет hello время, затрачиваемое пакетов в узле hello для обработки политики и увеличения hello число пакетов, которые могут быть обработаны внутри hello виртуальной Машины.
* **Сокращение флуктуации:** виртуальный коммутатор обработки зависит от hello объем политики, которая требует применения toobe и hello нагрузки hello ЦП, осуществляющего hello обработки. Разгрузки оборудования toohello принудительного применения политики hello устраняет этой изменчивостью, доставку пакетов напрямую toohello ВМ, удаление связи с узлом tooVM hello и все программное обеспечение прерываний и контекст переключается.
* **Уменьшается загрузка ЦП:** обход hello виртуальный коммутатор в узле hello ведет сборки ЦП для обработки сетевого трафика.

## <a name="Limitations"></a>Ограничения
При использовании этой возможности действуют следующие ограничения Hello.

* **Создание сетевого интерфейса.** Функцию ускорения сети можно включить только в новом сетевом интерфейсе. Ее нельзя включить в имеющемся сетевом интерфейсе.
* **Создание виртуальной Машины:** сетевого Адаптера с ускорителем сеть включенная может только вложенные tooa виртуальной Машины при hello виртуальной Машины создать. Hello сетевого Адаптера не может быть вложенного tooan существующей виртуальной Машины.
* **Регионы.** Виртуальные машины Windows с ускоренной сетью доступны в большинстве регионов Azure, Виртуальные машины Linux с ускоренной сетью доступны в нескольких регионах. Hello областей, которые эта возможность доступна в расширение. См. в разделе блога обновления виртуальной сети Azure hello ниже для получения последних сведений hello.   
* **Поддерживаемые операционные системы.** Windows: Microsoft Windows Server 2012 R2 Datacenter и Windows Server 2016. Linux: Ubuntu Server 16.04 LTS с ядром 4.4.0-77 или более поздней версии, SLES 12 SP2, RHEL 7.3 и CentOS 7.3 (опубликована Rogue Wave Software).
* **Размер виртуальной машины.** Экземпляры общего назначения и оптимизированные для вычислений экземпляры с минимум восемью ядрами. Дополнительные сведения см. в разделе hello [Windows](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) и [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) статьи размеров виртуальной Машины. Hello набор поддерживаемых размеров экземпляр виртуальной Машины будет расширяться в будущем hello.
* **Развертывание только с помощью Azure Resource Manager (ARM).** Ускоренная сеть недоступна для развертывания с помощью ASM/RDFE.

Изменения ограничения toothese объявляются через hello [виртуальную сеть Azure обновляет](https://azure.microsoft.com/updates/accelerated-networking-in-preview) страницы.

## <a name="create-a-windows-vm"></a>Создание виртуальной машины Windows
Вы можете использовать hello портал Azure или Azure [PowerShell](#windows-powershell) toocreate hello виртуальной Машины.

### <a name="windows-portal"></a>Портал

1. Откройте веб-браузер, hello Azure [портала](https://portal.azure.com) и выполните вход с помощью Azure [учетной записи](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account). Если у вас нет учетной записи, вы можете зарегистрироваться для получения [бесплатной пробной версии](https://azure.microsoft.com/offers/ms-azr-0044p).
2. На портале hello щелкните **+ создать** > **вычислений** > **Windows Server 2016 Datacenter**. 
3. В hello **Windows Server 2016 Datacenter** колонки, отображается, оставьте *диспетчера ресурсов* выбранных в разделе **выберите модель развертывания**и нажмите кнопку **создать** .
4. В hello **основы** колонки, отображается, введите следующие значения hello оставьте hello оставшиеся параметры по умолчанию или выбрать или ввести собственные значения и щелкните hello **ОК** кнопки:

    |Настройка|Значение|
    |---|---|
    |Имя|MyVm|
    |Группа ресурсов|Выберите **Создать** и введите *MyResourceGroup*.|
    |Расположение|Западная часть США 2|

    Если вы новый tooAzure, Дополнительные сведения о [групп ресурсов](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group), [подписки](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription), и [расположения](https://azure.microsoft.com/regions) (они также называется tooas областей).
5. В hello **выберите размер** колонки, которое откроется, введите *8* в hello **ядер менее** , а затем нажмите кнопку **просмотреть все**.
6. Нажмите кнопку **DS4_V2 Стандартная**, или любой поддерживаемый виртуальной Машины, нажмите кнопку hello **выберите** кнопки.
7. В hello **параметры** колонки, отображается, оставьте все параметры, как-является, за исключением того, щелкните **включено** под **Accelerated сети**, нажмите кнопку hello **ОК** кнопки. **Примечание:** , если в предыдущих шагах был выбран значения для размера виртуальной Машины, операционной системы или расположение, не перечисленным в hello [ограничения](#Limitations) данной статьи **сети Accelerated**не отображается.
8. В hello **Сводка** колонки, отображается, щелкните hello **ОК** кнопки. Azure запускает создание hello виртуальной Машины. Этот процесс займет несколько минут.
9. tooinstall hello ускорением сетевой драйвер для Windows, hello завершения шагов в hello [настроить Windows](#configure-windows) этой статьи.

### <a name="windows-powershell"></a>PowerShell
1. Установите последнюю версию Azure PowerShell hello hello [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) модуля. Если вы новый tooAzure PowerShell чтения hello [Обзор Azure PowerShell](/powershell/azure/get-started-azureps?toc=%2fazure%2fvirtual-network%2ftoc.json) статьи.
2. Запустите сеанс PowerShell, нажав кнопку Пуск Windows hello, введя **powershell**, выбрав **PowerShell** из результатов поиска hello.
3. В окне PowerShell, введите hello `login-azurermaccount` toosign команда с помощью Azure [учетной записи](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account). Если у вас нет учетной записи, вы можете зарегистрироваться для получения [бесплатной пробной версии](https://azure.microsoft.com/offers/ms-azr-0044p).
4. В браузере скопируйте hello следующий скрипт:
    ```powershell
    $RgName="MyResourceGroup"
    $Location="westus2"
    
    # Create a resource group
    New-AzureRmResourceGroup `
      -Name $RgName `
      -Location $Location
    
    # Create a subnet
    $Subnet = New-AzureRmVirtualNetworkSubnetConfig `
      -Name MySubnet `
      -AddressPrefix 10.0.0.0/24
    
    # Create a virtual network
    $Vnet=New-AzureRmVirtualNetwork `
      -ResourceGroupName $RgName `
      -Location $Location `
      -Name MyVnet `
      -AddressPrefix 10.0.0.0/16 `
      -Subnet $Subnet

    # Create a public IP address
    $Pip = New-AzureRmPublicIpAddress `
      -Name MyPublicIp `
      -ResourceGroupName $RgName `
      -Location $Location `
      -AllocationMethod Static

    # Create a virtual network interface and associate hello public IP address tooit
    $Nic = New-AzureRmNetworkInterface `
      -Name MyNic `
      -ResourceGroupName $RgName `
      -Location $Location `
      -SubnetId $Vnet.Subnets[0].Id `
      -PublicIpAddressId $Pip.Id `
      -EnableAcceleratedNetworking
     
    # Define a credential object for hello VM. PowerShell prompts you for a username and password.
    $Cred = Get-Credential

    # Create a virtual machine configuration
    $VmConfig = New-AzureRmVMConfig `
      -VMName MyVM -VMSize Standard_DS4_v2 | `
      Set-AzureRmVMOperatingSystem `
      -Windows `
      -ComputerName myVM `
      -Credential $Cred | `
    Set-AzureRmVMSourceImage `
      -PublisherName MicrosoftWindowsServer `
      -Offer WindowsServer `
      -Skus 2016-Datacenter `
      -Version latest | `
    Add-AzureRmVMNetworkInterface -Id $Nic.Id 

    # Create hello virtual machine.    
    New-AzureRmVM `
      -ResourceGroupName $RgName `
      -Location $Location `
      -VM $VmConfig
    #
    ```
5. В окне PowerShell щелкните правой кнопкой мыши сценарий toopaste hello и запустить его выполнения. Появится запрос на ввод имени пользователя и пароль. Используйте эти учетные данные toolog в toohello виртуальной Машины при подключении tooit в следующем шаге hello. Если вы изменили значения в сценарии hello перед его выполнением сбоя сценария hello, подтвердите hello значения используются для размера виртуальной Машины, операционной системы и расположение, перечислены в hello [ограничения](#Limitations) этой статьи.
6. tooinstall hello ускорением сетевой драйвер для Windows, hello завершения шагов в hello [настроить Windows](#configure-windows) этой статьи.

### <a name="configure-windows"></a>Настройка виртуальных машин Windows
После создания hello ВМ в Azure, необходимо установить hello ускорителем сетевой драйвер для Windows. Перед завершением hello, выполнив действия, необходимо создать виртуальную Машину Windows с ускорителем сети, с помощью либо hello [портала](#windows-portal) или [PowerShell](#windows-powershell) шаги в этой статье. 

1. Откройте веб-браузер, hello Azure [портала](https://portal.azure.com) и выполните вход с помощью Azure [учетной записи](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account). Если у вас нет учетной записи, вы можете зарегистрироваться для получения [бесплатной пробной версии](https://azure.microsoft.com/offers/ms-azr-0044p).
2. В поле hello, содержащее текст hello *Найдите ресурсы* вверху hello hello портал Azure, введите *MyVm*. Когда **MyVm** появится в результатах поиска hello, щелкните его.
3. В hello **MyVm** колонки, отображается, щелкните hello **Connect** кнопка в верхнем левом углу hello колонка hello. **Примечание:** Если **создание** отображается в группе hello **Connect** кнопки, Azure не завершено создание hello виртуальной Машины. Нажмите кнопку **Connect** только в том случае, если больше нет **создание** под hello **Connect** кнопки.
4. Разрешить hello toodownload ваш браузер **MyVm.rdp** файла.  После загрузки, выберите файл tooopen hello его. 
5. Нажмите кнопку hello **Connect** кнопку в hello **удаленный рабочий стол** поле, которое появляется уведомление о том, что hello не удается определить издателя удаленного подключения hello.
6. В hello **безопасности Windows** щелкните поле, которое появляется, **Дополнительные варианты**, нажмите кнопку **использовать другую учетную запись**. Введите hello имя пользователя и пароль, указанный на шаге 4, а затем нажмите кнопку hello **ОК** кнопки.
7. Нажмите кнопку hello **Да** кнопку в поле удаленный рабочий стол hello, появится уведомление о невозможности проверки удостоверения hello hello удаленного компьютера.
8. Щелкните правой кнопкой мыши кнопку Пуск Windows hello и нажмите кнопку **устройства**. Разверните hello **сетевые адаптеры** узла. Убедитесь, что hello **Mellanox ConnectX-3 виртуальный адаптер Ethernet функция** появляется, как показано в следующий рисунок hello:
   
    ![Диспетчер устройств](./media/virtual-network-create-vm-accelerated-networking/image2.png)

9. Ускорение работы в сети теперь включено на вашей виртуальной машине.

## <a name="create-a-linux-vm"></a>Создание виртуальной машины Linux
Вы можете использовать hello портал Azure или Azure [PowerShell](#linux-powershell) toocreate Ubuntu или SLES виртуальной Машины. У виртуальных машин RHEL и CentOS другой рабочий процесс.  См. в разделе hello приведенным ниже инструкциям.

### <a name="linux-portal"></a>Портал
1. Регистрация для hello accelerated сети для предварительной версии Linux, выполнив шаги 1 – 5 hello [создайте виртуальную Машину Linux — PowerShell](#linux-powershell) этой статьи.  Не удается зарегистрировать hello предварительную версию портала hello.
2. Выполните действия 1 – 8 в hello [создания виртуальной Машины Windows - портал](#windows-portal) этой статьи. На шаге 2 выберите **Ubuntu Server 16.04 LTS**, а не **Windows Server 2016 Datacenter**. В этом учебнике выберите toouse пароль, а не ключ SSH на то, что для рабочих развертываний можно использовать. Если **Accelerated сети** не отображается, когда шаги 7 hello [создания виртуальной Машины Windows - портал](#windows-portal) разделе данной статьи, вполне вероятно, по одной из следующих причин hello:
    - Вы еще не зарегистрированы для предварительного просмотра hello. Убедитесь, что состояние регистрации **зарегистрированные**, как описано в шаге 4 hello [создайте виртуальную Машину Linux — Powershell](#linux-powershell) этой статьи. **Примечание:** Если участвовали в hello Accelerated сети для виртуальных машин Windows preview (его нет больше необходимости tooregister toouse Accelerated сети для виртуальных машин Windows), вы не зарегистрированы автоматически hello Accelerated сети для Просмотр виртуальных машин Linux. Необходимо зарегистрировать для hello Accelerated сети для виртуальных машин Linux предварительного просмотра tooparticipate в нем.
    - Вы не выбрали размер виртуальной Машины, операционной системы или папке, заданной в hello [ограничения](#limitations) этой статьи.
3. tooinstall hello ускорением сетевой драйвер для Linux, hello завершения шагов в hello [Настройка Linux](#configure-linux) этой статьи.

### <a name="linux-powershell"></a>PowerShell

>[!WARNING]
>При создании виртуальных машин Linux с ускорителем сетями в подписке и повторить попытку toocreate виртуальной Машины Windows с ускорителем сетевых технологий в hello одной подписке, hello Создание виртуальной Машины Windows может завершиться ошибкой. Во время действия предварительной версии мы советуем создавать виртуальные машины Windows и Linux с функцией ускорения сети в отдельных подписках.
>

1. Установите последнюю версию Azure PowerShell hello hello [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) модуля. Если вы новый tooAzure PowerShell чтения hello [Обзор Azure PowerShell](/powershell/azure/get-started-azureps?toc=%2fazure%2fvirtual-network%2ftoc.json) статьи.
2. Запустите сеанс PowerShell, нажав кнопку Пуск Windows hello, введя **powershell**, выбрав **PowerShell** из результатов поиска hello.
3. В окне PowerShell, введите hello `login-azurermaccount` toosign команда с помощью Azure [учетной записи](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account). Если у вас нет учетной записи, вы можете зарегистрироваться для получения [бесплатной пробной версии](https://azure.microsoft.com/offers/ms-azr-0044p).
4. Регистрация для hello accelerated сети для Azure preview, выполнив следующие шаги hello:
    - Отправить сообщение электронной почты слишком[ axnpreview@microsoft.com ](mailto:axnpreview@microsoft.com?subject=Request%20to%20enable%20subscription%20%3csubscription%20id%3e) своим Идентификатором подписки Azure, а предполагаемого использования. Дождитесь, пока придет письмо с подтверждением от корпорации Майкрософт о том, что ваша подписка включена.
    - Введите следующие команды tooconfirm зарегистрированы для предварительного просмотра hello hello:
    
        ```powershell
        Get-AzureRmProviderFeature -FeatureName AllowAcceleratedNetworkingForLinux -ProviderNamespace Microsoft.Network
        ```

        Не нужно выполнять шаг 5 до **зарегистрированные** отображается в выходных данных после выполнения предыдущей команды hello hello. Выходные данные должны выглядеть следующие hello, выходные данные перед продолжением:
    
        ```powershell
        FeatureName                        ProviderName      RegistrationState
        -----------                        ------------      -----------------
        AllowAcceleratedNetworkingForLinux Microsoft.Network Registered
        ```
        
      >[!NOTE]
      >Если вы участвовали в hello Accelerated сети для виртуальных машин Windows preview (it's нет больше необходимости tooregister toouse Accelerated сети для виртуальных машин Windows) вы не зарегистрированы автоматически hello Accelerated сети для виртуальных машин Linux предварительной версии. Необходимо зарегистрировать для hello Accelerated сети для виртуальных машин Linux предварительного просмотра tooparticipate в нем.
      >
5. В браузере скопируйте следующий скрипт, заменив нужным Ubuntu или SLES hello.  Опять же, рабочий процесс для Redhat и CentOS разный. Он приведен ниже.

    ```powershell
    $RgName="MyResourceGroup"
    $Location="westus2"
    
    # Create a resource group
    New-AzureRmResourceGroup `
      -Name $RgName `
      -Location $Location
    
    # Create a subnet
    $Subnet = New-AzureRmVirtualNetworkSubnetConfig `
      -Name MySubnet `
      -AddressPrefix 10.0.0.0/24
    
    # Create a virtual network
    $Vnet=New-AzureRmVirtualNetwork `
      -ResourceGroupName $RgName `
      -Location $Location `
      -Name MyVnet `
      -AddressPrefix 10.0.0.0/16 `
      -Subnet $Subnet

    # Create a public IP address
    $Pip = New-AzureRmPublicIpAddress `
      -Name MyPublicIp `
      -ResourceGroupName $RgName `
      -Location $Location `
      -AllocationMethod Static

    # Create a virtual network interface and associate hello public IP address tooit
    $Nic = New-AzureRmNetworkInterface `
      -Name MyNic `
      -ResourceGroupName $RgName `
      -Location $Location `
      -SubnetId $Vnet.Subnets[0].Id `
      -PublicIpAddressId $Pip.Id `
      -EnableAcceleratedNetworking
     
    # Create a new Storage account and define hello new VM’s OSDisk name and its URI
    # Must end with ".vhd" extension
    $OSDiskName = "MyOsDiskName.vhd"
    # Storage account name must be between 3 and 24 characters in length and use numbers and lower-case letters only.
    $OSDiskSAName = "thestorageaccountname"  
    $StorageAccount = New-AzureRmStorageAccount -ResourceGroupName $RgName -Name $OSDiskSAName -Type "Standard_GRS" -Location $Location
    $OSDiskUri = $StorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $OSDiskName
 
    # Define a credential object for hello VM. PowerShell prompts you for a username and password.
    $Cred = Get-Credential

    # Create a virtual machine configuration
    $VmConfig = New-AzureRmVMConfig `
      -VMName MyVM -VMSize Standard_DS4_v2 | `
      Set-AzureRmVMOperatingSystem `
      -Linux `
      -ComputerName myVM `
      -Credential $Cred | `
    Set-AzureRmVMSourceImage `
      -PublisherName Canonical `
      -Offer UbuntuServer `
      -Skus 16.04-LTS `
      -Version latest | `
    Add-AzureRmVMNetworkInterface -Id $Nic.Id | `
    Set-AzureRmVMOSDisk -Name $OSDiskName `
      -VhdUri $OSDiskUri `
      -CreateOption FromImage 

    # Create hello virtual machine.    
    New-AzureRmVM `
      -ResourceGroupName $RgName `
      -Location $Location `
      -VM $VmConfig
    ```
    
6. В окне PowerShell щелкните правой кнопкой мыши сценарий toopaste hello и запустить его выполнения. Появится запрос на ввод имени пользователя и пароль. Используйте эти учетные данные toolog в toohello виртуальной Машины при подключении tooit в следующем шаге hello. При сбое скрипта hello, убедитесь, что:
    - Вы зарегистрированы для предварительного просмотра hello, как описано в шаге 4
    - Если вы изменили размер виртуальной Машины, тип операционной системы или расположение значений в скрипт hello перед его выполнением, что hello значения перечислены в hello [ограничения](#Limitations) этой статьи.
7. tooinstall hello ускорением сетевой драйвер для Linux, hello завершения шагов в hello [Настройка Linux](#configure-linux) этой статьи.

### <a name="configure-linux"></a>Настройка виртуальных машин Linux

После создания hello ВМ в Azure, необходимо установить сетевой драйвер hello для Linux. Перед завершением hello, выполнив действия, необходимо создать виртуальную Машину Linux с ускорителем сети, с помощью либо hello [портала](#linux-portal) или [PowerShell](#linux-powershell) шаги в этой статье. 

1. Откройте веб-браузер, hello Azure [портала](https://portal.azure.com) и выполните вход с помощью Azure [учетной записи](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account). Если у вас нет учетной записи, вы можете зарегистрироваться для получения [бесплатной пробной версии](https://azure.microsoft.com/offers/ms-azr-0044p).
2. Вверху hello hello портала, toohello справа от приветствия *Найдите ресурсы* панели, щелкните hello **> _** toostart значок оболочке Bash облака (Предварительная версия). Hello Bash облака оболочки появится область внизу hello hello портала и через несколько секунд представляется  **username@Azure:~ $** строки. На то, что вы можете toohello SSH виртуальной Машины с вашего компьютера, а не оболочки облака hello, hello инструкции в этом учебнике предполагается, что вы используете hello облака оболочки.
3. Вверху hello портала hello в hello поле, содержащее текст hello *Найдите ресурсы*, тип *MyVm*. Когда **MyVm** появится в результатах поиска hello, щелкните его.
4. В hello **MyVm** колонки, отображается, щелкните hello **Connect** кнопка в верхнем левом углу hello колонка hello. **Примечание:** Если **создание** отображается в группе hello **Connect** кнопки, Azure не завершено создание hello виртуальной Машины. Нажмите кнопку **Connect** только в том случае, если больше нет **создание** под hello **Connect** кнопки.
5. Azure открывает окно, предлагающее tooenter hello `ssh adminuser@<ipaddress>`. Введите эту команду в hello облака оболочки (или копировать его из поля hello, указанную в шаг 4 и вставьте его в toohello облаке оболочки), затем нажмите клавишу ВВОД.
6. Ввод **Да** вопрос toohello запросом вы toocontinue подключения, затем нажмите клавишу ВВОД.
7. Введите пароль hello, введенное при создании hello виртуальной Машины. Один раз успешно выполнил вход toohello ВМ, вы видите adminuser@MyVm:~ $ запрос. Вы вошли в toohello виртуальной Машине через сеанс оболочки hello облака. **Примечание.** Срок действия сеанса Cloud Shell истекает после 10 минут бездействия.

На этом этапе инструкции hello различаются в зависимости от hello распространения, которую вы используете. 

#### <a name="ubuntusles"></a>Ubuntu и SLES

1. В строке приветствия введите `uname -r` и проверить версию hello для:

    * Ubuntu — это версия 4.4.0-77-generic или более поздняя.
    * SLES — это версия 4.4.59-92.20-default или более поздняя.

2. Создайте связь между hello стандартной сети виртуального сетевого адаптера и сетевой hello accelerated виртуального сетевого адаптера с выполнением команд hello, следующие. Трафик сети использует hello выше, выполняя ускорителем сети виртуального сетевого адаптера, когда связь hello гарантирует, что сетевой трафик не будет прервано по некоторые изменения в конфигурации.
          
     ```bash
     wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/configure_hv_sriov.sh
     chmod +x ./configure_hv_sriov.sh
     sudo ./configure_hv_sriov.sh
     ```
3. После выполнения скрипта hello hello виртуальная машина будет перезапущена после приостановки 60 секунд.
4. Один раз hello перезапуске ВМ повторно подключиться tooit, выполнив шаги 5 – 7, еще раз.
5. Запустите hello `ifconfig` команды и убедитесь, что оказались bond0 hello интерфейс отображается вверх. 
 
 >[!NOTE]
      >Приложения, использующие ускорителем сети должен обмениваться данными по hello *bond0* интерфейс не *eth0*.  Имя интерфейса Hello может измениться до выхода общедоступной версии ускорителем сети.

#### <a name="rhelcentos"></a>RHEL или CentOS

Создание виртуальной Машины CentOS 7.3 или Red Hat Enterprise Linux требуются некоторые дополнительные шаги tooload hello последние версии драйверов, необходимых для SR-IOV и hello драйвер виртуальной функции (Виртуальной) для hello сетевой карты. Hello первый этап инструкции hello подготавливает образ, который может быть toomake используется один или несколько виртуальных машин, имеющих предварительно загрузить драйверы hello.

##### <a name="phase-one-prepare-a-red-hat-enterprise-linux-or-centos-73-base-image"></a>Первый этап: подготовка базового образа Red Hat Enterprise Linux или CentOS 7.3 

1.  Подготовьте виртуальную машину CentOS 7.3 без SRIOV в Azure.

2.  Установите LIS 4.2.2:
    
    ```bash
    wget http://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.2-2.tar.gz
    tar -xvf lis-rpms-4.2.2-2.tar.gz
    cd LISISO && sudo ./install.sh
    ```

3.  Скачайте файлы конфигурации.
    
    ```bash
    cd /etc/udev/rules.d/  
    sudo wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/60-hyperv-vf-name.rules 
    cd /usr/sbin/
    sudo wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/hv_vf_name 
    sudo chmod +x hv_vf_name
    cd /etc/sysconfig/network-scripts/
    sudo wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/ifcfg-vf1   
    ```

4.  Отзовите эту виртуальную машину.

    ```bash
    sudo waagent -deprovision+user 
    ```

5.  Из портала Azure остановить эту виртуальную Машину; и перейдите в tooVM «диски», записи hello OSDisk URI виртуального жесткого диска. Этот URI содержит имя виртуального жесткого диска hello базового образа и его учетной записи хранилища. 
 
##### <a name="phase-two-provision-new-vms-on-azure"></a>Второй этап: подготовка новых виртуальных машин в Azure

1.  Подготовка новых виртуальных машин на основе с AzureRMVMConfig создать с помощью hello базовый образ виртуального жесткого диска, записанный в первый этап, с помощью AcceleratedNetworking включена hello виртуального сетевого адаптера:

    ```powershell
    $RgName="MyResourceGroup"
    $Location="westus2"
    
    # Create a resource group
    New-AzureRmResourceGroup `
     -Name $RgName `
     -Location $Location

    # Create a subnet
    $Subnet = New-AzureRmVirtualNetworkSubnetConfig `
     -Name MySubnet `
     -AddressPrefix 10.0.0.0/24

    # Create a virtual network
    $Vnet=New-AzureRmVirtualNetwork `
     -ResourceGroupName $RgName `
     -Location $Location `
     -Name MyVnet `
     -AddressPrefix 10.0.0.0/16 `
     -Subnet $Subnet
    
    # Create a public IP address
    $Pip = New-AzureRmPublicIpAddress `
     -Name MyPublicIp `
     -ResourceGroupName $RgName `
     -Location $Location `
     -AllocationMethod Static
    
    # Create a virtual network interface and associate hello public IP address tooit
    $Nic = New-AzureRmNetworkInterface `
     -Name MyNic `
     -ResourceGroupName $RgName `
     -Location $Location `
     -SubnetId $Vnet.Subnets[0].Id `
     -PublicIpAddressId $Pip.Id `
     -EnableAcceleratedNetworking
    
    # Specify hello base image's VHD URI (from phase one step 5). 
    # Note: hello storage account of this base image vhd should have "Storage service encryption" disabled
    # See more from here: https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption
    # This is just an example URI, you will need tooreplace this when running this script
    $sourceUri="https://myexamplesa.blob.core.windows.net/vhds/CentOS73-Base-Test120170629111341.vhd" 

    # Specify a URI for hello location from which hello new image binary large object (BLOB) is copied toostart hello virtual machine. 
    # Must end with ".vhd" extension
    $OsDiskName = "MyOsDiskName.vhd" 
    $destOsDiskUri = "https://myexamplesa.blob.core.windows.net/vhds/" + $OsDiskName
    
    # Define a credential object for hello VM. PowerShell prompts you for a username and password.
    $Cred = Get-Credential
    
    # Create a custom virtual machine configuration
    $VmConfig = New-AzureRmVMConfig `
     -VMName MyVM -VMSize Standard_DS4_v2 | `
    Set-AzureRmVMOperatingSystem `
     -Linux `
     -ComputerName myVM `
     -Credential $Cred | `
    Add-AzureRmVMNetworkInterface -Id $Nic.Id | `
    Set-AzureRmVMOSDisk `
     -Name $OsDiskName `
     -SourceImageUri $sourceUri `
     -VhdUri $destOsDiskUri `
     -CreateOption FromImage `
     -Linux
    
    # Create hello virtual machine.    
    New-AzureRmVM `
     -ResourceGroupName $RgName `
     -Location $Location `
     -VM $VmConfig
    ```

2.  После загрузки виртуальных машин, проверьте устройство VF hello, «lspci» и проверьте запись Mellanox hello. Например мы должны увидеть этот элемент в выходных данных lspci hello:
    
    ```
    0001:00:02.0 Ethernet controller: Mellanox Technologies MT27500/MT27520 Family [ConnectX-3/ConnectX-3 Pro Virtual Function]
    ```
    
3.  Выполните сценарии hello резервирование с помощью:

    ```bash
    sudo bondvf.sh
    ```

4.  Перезагрузите hello новые виртуальные машины:

    ```bash
    sudo reboot
    ```

Hello виртуальной Машины должен начинаться с bond0 настроен и hello Accelerated сетевые пути включена.  Запустите `ifconfig` tooconfirm.
