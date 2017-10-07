---
title: "aaaLOB приложения тестовой среды | Документы Microsoft"
description: "Узнайте, как Интернет toocreate бизнес-приложений в гибридной облачной среды для IT pro или разработка тестирование."
services: virtual-machines-windows
documentationcenter: 
author: JoeDavies-MSFT
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 92d2d8ce-60ed-4512-95e5-a7fe3b0ca00b
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 09/30/2016
ms.author: josephd
ms.openlocfilehash: e9f825bbb1cbeb841ee3c974ebf6721dc236c311
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-web-based-lob-application-in-a-hybrid-cloud-for-testing"></a>Настройка веб бизнес-приложения в гибридном облаке для тестирования
В этом разделе описываются шаги по созданию имитации гибридной облачной среды для тестирования сетевого бизнес-приложения, размещенного в Microsoft Azure. Здесь представлена конфигурация полученный hello.

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph3.png)

В эту конфигурацию входят:

* Имитация локальной сети, размещенных в Azure (hello тестовая лаборатория виртуальной сети).
* виртуальная сеть с подключением между организациями, размещенная в Azure (TestVNET);
* VPN-подключение типа "виртуальная сеть — виртуальная сеть";
* Веб-сервера LOB, SQL server и дополнительный контроллер домена в виртуальной сети TestVNET hello.

Это основа и общая начальная точка, на базе которой можно:

* разрабатывать и тестировать бизнес-приложения, размещенные в службах IIS, с помощью сервера базы данных SQL Server 2014 в Azure.
* выполнять тестирование имитации гибридной облачной рабочей нагрузки ИТ-среды.

Существует три основных этапа toosetting этой тестовой среды гибридного облака:

1. Настройка hello имитацию гибридной облачной среды.
2. Настройка компьютера hello SQL server (SQL1).
3. Настройка сервера LOB hello (LOB1).

Для этой рабочей нагрузки требуется подписка Azure. Если у вас есть подписка MSDN или Visual Studio, ознакомьтесь с разделом [Ежемесячная сумма денег на счете в Azure для подписчиков Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).

Пример производства бизнес-приложения, размещенные в Azure см. в разделе hello **бизнес-приложений** чертежом архитектуры в [схем архитектуры программного обеспечения корпорации Майкрософт и чертежей](http://msdn.microsoft.com/dn630664).

## <a name="phase-1-set-up-hello-simulated-hybrid-cloud-environment"></a>Этап 1: Настройка hello имитацию гибридной облачной среды
Создать hello [имитацию гибридного облака тестовой среде](ps-hybrid-cloud-test-env-sim.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Поскольку данной тестовой среды не требуется наличие hello server hello APP1 в подсети корпоративной сети hello, можно завершить работу сейчас.

Это текущая конфигурация.

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph1.png)

## <a name="phase-2-configure-hello-sql-server-computer-sql1"></a>Этап 2: Настройка компьютера hello SQL server (SQL1)
При необходимости начать компьютер DC2 hello hello портал Azure.

Теперь создайте виртуальную машину для SQL1, выполнив следующие команды в командной строке Azure PowerShell на локальном компьютере. Предыдущий toorunning эти команды заполнить hello значения переменных и удалить hello < и > символов.

    $rgName="<your resource group name>"
    $locName="<hello Azure location of your resource group>"
    $saName="<your storage account name>"

    $vnet=Get-AzureRMVirtualNetwork -Name "TestVNET" -ResourceGroupName $rgName
    $subnet=Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name "TestSubnet"
    $pip=New-AzureRMPublicIpAddress -Name SQL1-NIC -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic
    $nic=New-AzureRMNetworkInterface -Name SQL1-NIC -ResourceGroupName $rgName -Location $locName -Subnet $subnet -PublicIpAddress $pip
    $vm=New-AzureRMVMConfig -VMName SQL1 -VMSize Standard_A4
    $storageAcc=Get-AzureRMStorageAccount -ResourceGroupName $rgName -Name $saName
    $vhdURI=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/SQL1-SQLDataDisk.vhd"
    Add-AzureRMVMDataDisk -VM $vm -Name "Data" -DiskSizeInGB 100 -VhdUri $vhdURI  -CreateOption empty

    $cred=Get-Credential -Message "Type hello name and password of hello local administrator account for hello SQL Server computer." 
    $vm=Set-AzureRMVMOperatingSystem -VM $vm -Windows -ComputerName SQL1 -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm=Set-AzureRMVMSourceImage -VM $vm -PublisherName MicrosoftSQLServer -Offer SQL2014-WS2012R2 -Skus Standard -Version "latest"
    $vm=Add-AzureRMVMNetworkInterface -VM $vm -Id $nic.Id
    $storageAcc=Get-AzureRMStorageAccount -ResourceGroupName $rgName -Name $saName
    $osDiskUri=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/SQL1-OSDisk.vhd"
    $vm=Set-AzureRMVMOSDisk -VM $vm -Name "OSDisk" -VhdUri $osDiskUri -CreateOption fromImage
    New-AzureRMVM -ResourceGroupName $rgName -Location $locName -VM $vm

Используйте hello Azure портала tooconnect tooSQL1 с помощью учетной записи локального администратора hello SQL1.

Настройте брандмауэр Windows правила tooallow связности тестирования и трафик SQL Server. Из командной строки Windows PowerShell с правами администратора на SQL1 выполните следующие команды.

    New-NetFirewallRule -DisplayName "SQL Server" -Direction Inbound -Protocol TCP -LocalPort 1433,1434,5022 -Action allow 
    Set-NetFirewallRule -DisplayName "File and Printer Sharing (Echo Request - ICMPv4-In)" -enabled True
    ping dc2.corp.contoso.com

команда ping Hello должны появиться четыре успешного ответа от IP-адрес 192.168.0.4.

Добавьте hello дополнительный диск данных на сервере SQL1 как новый том с буквой hello диска «f:».

1. Hello левой панели диспетчера сервера щелкните **файловых служб и служб хранилища**, а затем нажмите кнопку **дисков**.
2. В области содержимого hello в hello **дисков** щелкните **диск 2** (с hello **секции** значение слишком**Неизвестный**).
3. Щелкните **Задачи**, а затем **Новый том**.
4. Hello перед началом страница приветствия мастера создания тома, щелкните **Далее**.
5. На сервере выберите hello hello и страницы с диска, нажмите кнопку **диск 2**, а затем нажмите кнопку **Далее**. При появлении запроса нажмите кнопку **OK**.
6. Щелкните hello задать hello размер страницы приветствия тома, **Далее**.
7. На hello Assign tooa диска буква или папка "нажмите" **Далее**.
8. На странице параметров системы hello выберите файл, нажмите кнопку **Далее**.
9. На странице подтверждения выбранных элементов hello щелкните **создать**.
10. После завершения нажмите кнопку **Закрыть**.

Выполняйте эти команды в командной строке Windows PowerShell hello на SQL1:

    md f:\Data
    md f:\Log
    md f:\Backup

Далее подсоедините SQL1 toohello CORP домена Windows Server Active Directory с помощью следующих команд в командной строке Windows PowerShell hello на SQL1.

    Add-Computer -DomainName corp.contoso.com
    Restart-Computer

Использовать учетную запись hello CORP\User1 при появлении запроса учетных данных учетной записи домена toosupply для hello **Add-Computer** команды.

После перезагрузки компьютера используйте hello Azure портала tooconnect tooSQL1 *учетную запись локального администратора hello SQL1*.

Настройте диска «f:» toouse hello SQL Server 2014 для новых баз данных, а также для разрешения учетной записи пользователя.

1. Hello начальном экране введите **управления SQL Server**, а затем нажмите кнопку **SQL Server 2014 Management Studio**.
2. В **подключения tooServer**, нажмите кнопку **Connect**.
3. Щелкните правой кнопкой мыши в области дерева обозревателя объектов hello **SQL1**, а затем нажмите кнопку **свойства**.
4. В hello **свойства сервера** окно, нажмите кнопку **параметры базы данных**.
5. Найдите hello **базы данных по умолчанию расположений** и задайте следующие значения: 
   * Для **данные**, путь к типу hello **f:\Data**.
   * Для **журнала**, путь к типу hello **f:\Log**.
   * Для **резервного копирования**, путь к типу hello **f:\Backup**.
   * Примечание. Только новые базы данных будут использовать эти расположения.
6. Нажмите кнопку hello **ОК** tooclose окна hello.
7. В hello **обозревателя объектов** древовидном откройте **безопасности**.
8. Щелкните правой кнопкой мыши **Имена входа**, а затем выберите **Создать имя входа**.
9. В поле **Имя входа** введите **CORP\User1**.
10. На hello **ролей сервера** щелкните **sysadmin**, а затем нажмите кнопку **ОК**.
11. Закройте Microsoft SQL Server Management Studio.

Это текущая конфигурация.

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph2.png)

## <a name="phase-3-configure-hello-lob-server-lob1"></a>Этап 3: Настройка сервера LOB hello (LOB1)
Сначала создайте виртуальную машину для LOB1 с помощью следующих команд командной hello Azure PowerShell на локальном компьютере.

    $rgName="<your resource group name>"
    $locName="<your Azure location, such as West US>"
    $saName="<your storage account name>"

    $vnet=Get-AzureRMVirtualNetwork -Name "TestVNET" -ResourceGroupName $rgName
    $subnet=Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name "TestSubnet"
    $pip=New-AzureRMPublicIpAddress -Name LOB1-NIC -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic
    $nic=New-AzureRMNetworkInterface -Name LOB1-NIC -ResourceGroupName $rgName -Location $locName -Subnet $subnet -PublicIpAddress $pip
    $vm=New-AzureRMVMConfig -VMName LOB1 -VMSize Standard_A2
    $storageAcc=Get-AzureRMStorageAccount -ResourceGroupName $rgName -Name $saName
    $cred=Get-Credential -Message "Type hello name and password of hello local administrator account for LOB1."
    $vm=Set-AzureRMVMOperatingSystem -VM $vm -Windows -ComputerName LOB1 -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm=Set-AzureRMVMSourceImage -VM $vm -PublisherName MicrosoftWindowsServer -Offer WindowsServer -Skus 2012-R2-Datacenter -Version "latest"
    $vm=Add-AzureRMVMNetworkInterface -VM $vm -Id $nic.Id
    $osDiskUri=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/LOB1-TestLab-OSDisk.vhd"
    $vm=Set-AzureRMVMOSDisk -VM $vm -Name LOB1-TestVNET-OSDisk -VhdUri $osDiskUri -CreateOption fromImage
    New-AzureRMVM -ResourceGroupName $rgName -Location $locName -VM $vm

Затем используйте hello Azure портала tooconnect tooLOB1 с учетными данными hello LOB1 учетной записи локального администратора hello.

Настройте трафика tooallow правило брандмауэра Windows для тестирования связности. Из командной строки Windows PowerShell с правами администратора на LOB1 выполните следующие команды.

    Set-NetFirewallRule -DisplayName "File and Printer Sharing (Echo Request - ICMPv4-In)" -enabled True
    ping dc2.corp.contoso.com

команда ping Hello должны появиться четыре успешного ответа от IP-адрес 192.168.0.4.

Далее присоединен к домену CORP Active Directory toohello LOB1 с помощью следующих команд в командной строке Windows PowerShell hello.

    Add-Computer -DomainName corp.contoso.com
    Restart-Computer

Использовать учетную запись hello CORP\User1 при появлении запроса учетных данных учетной записи домена toosupply для hello **Add-Computer** команды.

После перезагрузки компьютера используйте hello Azure портала tooconnect tooLOB1 с hello CORP\User1 учетную запись и пароль.

Затем настройте LOB1 для служб IIS и протестируйте доступ из CLIENT1.

1. В диспетчере серверов выберите **Добавить роли и компоненты**.
2. На hello **перед началом** щелкните **Далее**.
3. На hello **Выбор типа установки** щелкните **Далее**.
4. На hello **Выбор целевого сервера** щелкните **Далее**.
5. На hello **ролей сервера** щелкните **веб-сервер (IIS)** в списке hello **ролей**.
6. При появлении запроса щелкните **Добавить компоненты**, а затем нажмите кнопку **Далее**.
7. На hello **Выбор компонентов** щелкните **Далее**.
8. На hello **веб-сервер (IIS)** щелкните **Далее**.
9. На hello **Выбор служб ролей** страницы, выберите или снимите флажки hello hello служб для проверки вашей бизнес-приложения и нажмите кнопку **Далее**.
10. На hello **подтверждение выбранных параметров установки** щелкните **установить**.
11. Дождитесь завершения установки hello компонентов и нажмите кнопку **закрыть**.
12. Из hello портал Azure подключите компьютер CLIENT1 toohello с учетными данными учетной записью CORP\User1 hello, а затем запустите Internet Explorer.
13. Введите в адресной строке hello **http://lob1/** и нажмите клавишу ВВОД. Вы увидите веб-страницы IIS 8 умолчанию hello.

Это текущая конфигурация.

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph3.png)

Эта среда хорошо, теперь готовы для вас toodeploy веб-приложения на LOB1 и тестирования функции из CLIENT1 в подсети корпоративной сети hello.

## <a name="next-step"></a>Дальнейшие действия
* Добавить новую виртуальную машину с помощью hello [портал Azure](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

