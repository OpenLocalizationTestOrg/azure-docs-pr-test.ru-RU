---
title: "aaaCreate виртуальной Машины Windows с помощью PowerShell | Документы Microsoft"
description: "Создайте виртуальные машины Windows с помощью Azure PowerShell и hello классической модели развертывания."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 42c0d4be-573c-45d1-b9b0-9327537702f7
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: cynthn
ms.openlocfilehash: 5339f458c1f08f6e1752a53191f19402fab8ea25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-virtual-machine-with-powershell-and-hello-classic-deployment-model"></a>Создание виртуальной машины Windows с помощью PowerShell и hello классической модели развертывания
> [!div class="op_single_selector"]
> * [Портал Azure — Windows](tutorial.md)
> * [PowerShell — Windows](create-powershell.md)
> 
> 

<br>

> [!IMPORTANT] 
> В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../../../resource-manager-deployment-model.md). В этой статье описан с помощью hello классической модели развертывания. Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов. Узнайте, каким образом слишком[выполните следующие действия с помощью диспетчера ресурсов модели hello](../../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Следующие шаги показывают, как toocustomize набор Azure PowerShell команды, создание и предварительная настройка виртуальной машины на основе Windows Azure, используя подход стандартного блока. Этот процесс можно использовать tooquickly создать набор команд для новой виртуальной машины под управлением Windows и разверните существующего развертывания, или toocreate несколько команда задает, быстро строить пользовательские разработки и тестирования или специалистов ИТ-среде.

Материал в этих шагах для создания наборов команд Azure PowerShell представлен таким образом, что достаточно лишь заполнить пробелы. Этот подход может оказаться полезным, если вы являетесь новый tooPowerShell или необходимо просто tooknow toospecify какие значения для успешной настройки. Опытные пользователи PowerShell можно воспользоваться командами hello и подставьте собственные значения для переменных hello (hello строки, начинающиеся с «$»).

Если вы еще не сделали этого, используйте инструкции hello в [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview) tooinstall Azure PowerShell на локальном компьютере. Затем откройте командную строку Windows PowerShell.

## <a name="step-1-add-your-account"></a>Шаг 1. Добавление учетной записи
1. Введите в командной строке PowerShell hello **Add-AzureAccount** и нажмите кнопку **ввод**. 
2. Введите адрес электронной почты hello, связанных с подпиской Azure и нажмите кнопку **Продолжить**. 
3. Введите в hello пароль своей учетной записи. 
4. Щелкните **Войти**.

## <a name="step-2-set-your-subscription-and-storage-account"></a>Шаг 2. Выбор подписки и учетной записи хранения
Задайте подписка Azure и учетной записи хранилища, выполнив следующие команды в командной строке Windows PowerShell hello. Замените все содержимое в кавычках hello, включая hello < и > символы, правильные имена hello.

    $subscr="<subscription name>"
    $staccount="<storage account name>"
    Select-AzureSubscription -SubscriptionName $subscr –Current
    Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount

Hello правильное имя подписки можно получить из hello свойство Имя_подписки выходной hello hello **Get-AzureSubscription** команды. Можно получить имя учетной записи хранения правильно hello hello свойства Label выходные данные hello hello **Get AzureStorageAccount** команду после запуска hello **Select-AzureSubscription** команды.

## <a name="step-3-determine-hello-imagefamily"></a>Шаг 3: Определение hello ImageFamily
Далее необходимо toodetermine hello ImageFamily или значение метки для соответствующего toohello hello конкретный образ виртуальной машины Azure требуется toocreate. Вы можете получить hello список доступных значений ImageFamily с помощью этой команды.

    Get-AzureVMImage | select ImageFamily -Unique

Ниже приведено несколько примеров значений ImageFamily для компьютеров под управлением Windows:

* Центр обработки данных Windows Server 2012 R2
* Windows Server 2008 R2 с пакетом обновления 1
* Windows Server 2016 Technical Preview 4
* SQL Server 2012 SP1 Enterprise на базе Windows Server 2012

Если найти образ hello, которую вы ищете, откройте создания нового экземпляра редактора текста hello choice или hello PowerShell интегрированная среда сценариев (ISE). Скопируйте следующие hello в hello новый текстовый файл или hello интегрированной среды Сценариев PowerShell, заменив значение ImageFamily hello.

    $family="<ImageFamily value>"
    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

В некоторых случаях имя образа hello уже hello свойства Label вместо hello значение ImageFamily. Если вы не нашли hello образ, который вы ищете с помощью свойства ImageFamily hello, списка образов hello по их свойству метки с помощью этой команды.

    Get-AzureVMImage | select Label -Unique

Если вы нашли hello правом изображении с помощью этой команды, откройте создания нового экземпляра hello текстовом редакторе choice или hello интегрированной среды Сценариев PowerShell. Скопируйте следующие hello в hello новый текстовый файл или hello интегрированной среды Сценариев PowerShell, заменив значение метки hello.

    $label="<Label value>"
    $image = Get-AzureVMImage | where { $_.Label -eq $label } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

## <a name="step-4-build-your-command-set"></a>Шаг 4. Создание своего набора команд
Построение rest hello набор путем копирования в новый текстовый файл или hello интегрированной среды Сценариев и затем заполнив hello значения переменных, а также удаление hello < и > символов hello соответствующий набор блоков ниже команды. . В разделе hello двух [примеры](#examples) конце hello в этой статье для получения представления hello конечного результата.

Начните создавать свой набор команд, выбрав один из этих двух блоков команд (обязательно).

Вариант 1. Укажите имя и размер виртуальной машины.

    $vmname="<machine name>"
    $vmsize="<Specify one: Small, Medium, Large, ExtraLarge, A5, A6, A7, A8, A9>"
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

Вариант 2. Укажите имя, размер, а также имя группы доступности.

    $vmname="<machine name>"
    $vmsize="<Specify one: Small, Medium, Large, ExtraLarge, A5, A6, A7, A8, A9>"
    $availset="<set name>"
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image -AvailabilitySetName $availset

Hello InstanceSize значения для D-, DS- или виртуальные машины серии G см [виртуальной машины размеры и облачных служб для Azure](https://msdn.microsoft.com/library/azure/dn197896.aspx).

> [!NOTE]
> Если Enterprise Agreement с программой Software Assurance и предполагаете tootake преимуществами hello Windows Server [преимущество использования гибридной](https://azure.microsoft.com/pricing/hybrid-use-benefit/), добавьте **- LicenseType** toohello параметр  **Новый AzureVMConfig** командлета, передав значение hello **Windows_Server** hello типичный вариант использования.  Убедитесь, что вы используете образ, который вы отправили; нельзя использовать стандартный образ из коллекции hello с hello гибридного использовать преимущество.
> 
> 

При необходимости для автономном компьютере Windows, укажите hello учетной записи локального администратора и пароль.

    $cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
    $vm1 | Add-AzureProvisioningConfig -Windows -AdminUsername $cred.Username -Password $cred.GetNetworkCredential().Password

Выберите надежный пароль. toocheck его надежность. в разделе [проверки паролей: использование надежных паролей](https://www.microsoft.com/security/pc-security/password-checker.aspx).

При необходимости tooadd hello Windows компьютер tooan существующему домену Active Directory, укажите hello учетной записи локального администратора и пароль, домен hello hello имя и пароль учетной записи домена.

    $cred1=Get-Credential –Message "Type hello name and password of hello local administrator account."
    $cred2=Get-Credential –Message "Now type hello name (not including hello domain) and password of an account that has permission tooadd hello machine toohello domain."
    $domaindns="<FQDN of hello domain that hello machine is joining>"
    $domacctdomain="<domain of hello account that has permission tooadd hello machine toohello domain>"
    $vm1 | Add-AzureProvisioningConfig -AdminUsername $cred1.Username -Password $cred1.GetNetworkCredential().Password -WindowsDomain -Domain $domacctdomain -DomainUserName $cred2.Username -DomainPassword $cred2.GetNetworkCredential().Password -JoinDomain $domaindns

Дополнительные способы предварительной настройки виртуальных машин под управлением Windows, см. синтаксис hello hello **Windows** и **WindowsDomain** наборы параметров [ -AzureProvisioningConfig](/powershell/module/azure/add-azureprovisioningconfig).

При необходимости назначьте виртуальной машине hello определенный IP-адрес, известный как статический DIP-адрес.

    $vm1 | Set-AzureStaticVNetIP -IPAddress <IP address>

Доступность определенного IP-адреса можно проверить следующим образом:

    Test-AzureStaticVNetIP –VNetName <VNet name> –IPAddress <IP address>

При необходимости назначьте hello виртуальной машины tooa конкретной подсети в виртуальной сети Azure.

    $vm1 | Set-AzureSubnet -SubnetNames "<name of hello subnet>"

При необходимости добавьте данные одного диска toohello виртуальной машины.

    $disksize=<size of hello disk in GB>
    $disklabel="<hello label on hello disk>"
    $lun=<Logical Unit Number (LUN) of hello disk>
    $hcaching="<Specify one: ReadOnly, ReadWrite, None>"
    $vm1 | Add-AzureDataDisk -CreateNew -DiskSizeInGB $disksize -DiskLabel $disklabel -LUN $lun -HostCaching $hcaching

Для контроллера домена Active Directory, задайте $hcaching слишком «None».

При необходимости добавьте hello виртуальной машины tooan существующий набор балансировки нагрузки для внешнего трафика.

    $protocol="<Specify one: tcp, udp>"
    $localport=<port number of hello internal port>
    $pubport=<port number of hello external port>
    $endpointname="<name of hello endpoint>"
    $lbsetname="<name of hello existing load-balanced set>"
    $probeprotocol="<Specify one: tcp, http>"
    $probeport=<TCP or HTTP port number of probe traffic>
    $probepath="<URL path for probe traffic>"
    $vm1 | Add-AzureEndpoint -Name $endpointname -Protocol $protocol -LocalPort $localport -PublicPort $pubport -LBSetName $lbsetname -ProbeProtocol $probeprotocol -ProbePort $probeport -ProbePath $probepath

Наконец можно выберите один из этих блоков необходимую команду для создания виртуальной машины hello.

Вариант 1: Создание виртуальной машины hello в существующей облачной службе.

    New-AzureVM –ServiceName "<short name of hello cloud service>" -VMs $vm1

Краткое имя Hello hello облачной службы является hello имя, которое отображается в списке hello облачных служб в hello портал Azure или hello список групп ресурсов в hello портал Azure.

Вариант 2: Создание виртуальной машины hello в существующей облачной службы и виртуальной сети.

    $svcname="<short name of hello cloud service>"
    $vnetname="<name of hello virtual network>"
    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname

## <a name="step-5-run-your-command-set"></a>Шаг 5. Запуск набора команд
Просмотрите набор команд Azure PowerShell hello, созданных в текстовом редакторе или hello интегрированной среды Сценариев PowerShell, состоящий из нескольких блоков команды из шага 4. Убедитесь, что указаны все переменные hello требуется и что они имеют правильные значения hello. Убедитесь, что были удалены все символы hello < и >.

При использовании в текстовом редакторе, команду копирования hello задать toohello буфер обмена и щелкните правой кнопкой мыши откройте командную строку Windows PowerShell. Это будет выдавать набор команд hello как ряд команд PowerShell, а также создать виртуальную машину Azure. Кроме того выполните команду hello, установка в интегрированной среде Сценариев PowerShell hello.

Если вы собираетесь снова создать эту или подобную виртуальную машину, можно предпринять следующее:

* Сохраните этот набор команд как файл сценария PowerShell (PS1-файл).
* Эта команда задать в качестве runbook службы автоматизации Azure в hello Сохранить **учетные записи автоматизации** раздел hello портал Azure.

## <a id="examples"></a>Примеры
Ниже приведены два примера использования hello уровня выше наборов команд Azure PowerShell toobuild, создаваемые на основе Windows Azure виртуальные машины.

### <a name="example-1"></a>Пример 1
Требуется PowerShell команда задавать toocreate hello начальной виртуальную машину для контроллера домена Active Directory:

* Использует образ Windows Server 2012 R2 Datacenter hello.
* Имеет имя hello AZDC1.
* является автономным компьютером;
* имеет дополнительный диск данных объемом 20 ГБ;
* Имеет статический IP-адрес hello 192.168.244.4.
* Находится в подсети серверной hello hello AZDatacenter виртуальной сети.
* — В облачной службе Azure TailspinToys hello.

Вот hello соответствующего Azure PowerShell команду set toocreate этой виртуальной машины с пустой строки между каждым разделом для удобства чтения.

    $family="Windows Server 2012 R2 Datacenter"
    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1
    $vmname="AZDC1"
    $vmsize="Medium"
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

    $cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
    $vm1 | Add-AzureProvisioningConfig -Windows -AdminUsername $cred.Username -Password $cred.GetNetworkCredential().Password

    $vm1 | Set-AzureSubnet -SubnetNames "BackEnd"

    $vm1 | Set-AzureStaticVNetIP -IPAddress 192.168.244.4

    $disksize=20
    $disklabel="DCData"
    $lun=0
    $hcaching="None"
    $vm1 | Add-AzureDataDisk -CreateNew -DiskSizeInGB $disksize -DiskLabel $disklabel -LUN $lun -HostCaching $hcaching

    $svcname="Azure-TailspinToys"
    $vnetname="AZDatacenter"
    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname

### <a name="example-2"></a>Пример 2
Требуется PowerShell набора команд toocreate виртуальной машины для бизнес-сервера:

* Использует образ Windows Server 2012 R2 Datacenter hello.
* Имеет имя hello LOB1.
* Является членом домена corp.contoso.com hello.
* имеет дополнительный диск данных объемом 200 ГБ;
* Возможности hello внешней подсети виртуальной сети AZDatacenter hello.
* — В облачной службе Azure TailspinToys hello.

Вот hello соответствующего Azure PowerShell команду set toocreate этой виртуальной машины.

    $family="Windows Server 2012 R2 Datacenter"
    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1
    $vmname="LOB1"
    $vmsize="Large"
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

    $cred1=Get-Credential –Message "Type hello name and password of hello local administrator account."
    $cred2=Get-Credential –Message "Now type hello name (not including hello domain) and password of an account that has permission tooadd hello machine toohello domain."
    $domaindns="corp.contoso.com"
    $domacctdomain="CORP"
    $vm1 | Add-AzureProvisioningConfig -AdminUsername $cred1.Username -Password $cred1.GetNetworkCredential().Password -WindowsDomain -Domain $domacctdomain -DomainUserName $cred2.Username -DomainPassword $cred2.GetNetworkCredential().Password -JoinDomain $domaindns

    $vm1 | Set-AzureSubnet -SubnetNames "FrontEnd"

    $disksize=200
    $disklabel="LOBData"
    $lun=0
    $hcaching="ReadWrite"
    $vm1 | Add-AzureDataDisk -CreateNew -DiskSizeInGB $disksize -DiskLabel $disklabel -LUN $lun -HostCaching $hcaching

    $svcname="Azure-TailspinToys"
    $vnetname="AZDatacenter"
    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname


## <a name="next-steps"></a>Дальнейшие действия
Если потребуется диск ОС, не должен превышать 127 ГБ, вы можете [разверните диск hello ОС](../../virtual-machines-windows-expand-os-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

