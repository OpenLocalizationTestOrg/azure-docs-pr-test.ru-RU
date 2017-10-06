---
title: "Доменные службы Azure Active Directory: руководство по администрированию | Документация Майкрософт"
description: "Присоедините виртуальную машину tooa управляемого домена Windows с помощью Azure PowerShell и hello классической модели развертывания."
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 9143b843-7327-43c3-baab-6e24a18db25e
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 21bc5930d84c5368a120f9d81f09320e2a0168fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="join-a-windows-server-virtual-machine-tooa-managed-domain-using-powershell"></a>К домену Windows Server виртуальной машины tooa управляемых с помощью PowerShell
> [!div class="op_single_selector"]
> * [Классический портал Azure — Windows](active-directory-ds-admin-guide-join-windows-vm.md)
> * [PowerShell — Windows](active-directory-ds-admin-guide-join-windows-vm-classic-powershell.md)
>
>

<br>

> [!IMPORTANT]
> В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель Resource Manager и классическая модель](../azure-resource-manager/resource-manager-deployment-model.md). В этой статье описан с помощью hello классической модели развертывания. Доменные службы Azure AD в настоящее время не поддерживает модель диспетчера ресурсов hello.
>
>

Следующие шаги показывают, как toocustomize набор Azure PowerShell команды, создание и предварительная настройка виртуальной машины на основе Windows Azure, используя подход стандартного блока. Эти шаги помогут выполнить виртуальной машины на основе Windows Azure и присоединить ее управляемый домен tooan доменные службы Azure AD.

Материал в этих шагах для создания наборов команд Azure PowerShell представлен таким образом, что достаточно лишь заполнить пробелы. Этот подход может оказаться полезным, если вы являетесь новый tooPowerShell или требуется tooknow toospecify какие значения для успешной настройки. Опытные пользователи PowerShell можно воспользоваться командами hello и подставьте собственные значения для переменных hello (hello строки, начинающиеся с «$»).

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

## <a name="step-3-step-by-step-walkthrough---provision-hello-virtual-machine-and-join-it-toohello-managed-domain"></a>Шаг 3: Пошаговое руководство - подготовки виртуальной машины hello и присоедините его toohello управляемого домена
Вот hello соответствующего Azure PowerShell команду set toocreate этой виртуальной машины с пустой строки между каждым разделом для удобства чтения.

Укажите сведения о подготовки виртуальной машины toobe с Windows hello.

    $family="Windows Server 2012 R2 Datacenter"
    $vmname="Contoso100-test"
    $vmsize="ExtraSmall"

Hello InstanceSize значения для D-, DS- или виртуальные машины серии G см [виртуальной машины размеры и облачных служб для Azure](https://msdn.microsoft.com/library/azure/dn197896.aspx).

Приводятся сведения о hello управляемый домен.

    $domaindns="contoso100.com"
    $domacctdomain="contoso100"

Укажите имя hello hello облачной службы.

    $svcname="Contoso100-test"

Укажите имя hello toowhich hello hello виртуальной сети, должны быть присоединены к виртуальной Машине. Убедитесь, hello AAD-управляемого домена в этой виртуальной сети.

    $vnetname="MyPreviewVnet"

Toobe образ виртуальной Машины выберите hello используется tooprovision hello виртуальной Машины.

    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

Настройка виртуальной Машины — имя набора ВМ, hello экземпляр размер & изображения toobe используется.

    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

Получите учетные данные локального администратора для hello виртуальной Машины. Укажите надежный пароль локального администратора.

    $localadmincred=Get-Credential –Message "Type hello name and password of hello local administrator account."

Получите учетные данные для учетной записи пользователя, принадлежащий too'AAD контроллера домена Администраторы группы toojoin ВМ toohello управляемый домен. Не указывайте hello имя домена — как имя пользователя hello для экземпляра, в нашем примере мы указываем «bob».

    $domainadmincred=Get-Credential –Message "Now type hello name (DO NOT INCLUDE hello DOMAIN) and password of an account in hello AAD DC Administrators group, that has permission tooadd hello machine toohello domain."

Настройка виртуальной Машины hello - указать требования к соединения домена и необходимые учетные данные.

    $vm1 | Add-AzureProvisioningConfig -AdminUsername $localadmincred.Username -Password $localadmincred.GetNetworkCredential().Password -WindowsDomain -Domain $domacctdomain -DomainUserName $domainadmincred.Username -DomainPassword $domainadmincred.GetNetworkCredential().Password -JoinDomain $domaindns

Задайте подсеть для hello виртуальной Машины.

    $vm1 | Set-AzureSubnet -SubnetNames "Subnet-1"

Необязательно: Точка toohello IP-адрес домена hello. Если значение hello toobe управляемого домена доменные службы Azure AD hello hello IP-адреса DNS-серверов для виртуальной сети hello, этот шаг не требуется.

    $dns = New-AzureDns -Name 'contoso100-dc1' -IPAddress '10.0.0.4'

Теперь hello подготовки присоединенных к домену Windows виртуальной Машины.

    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname -Location "Central US" -DnsSettings $dns

<br>

## <a name="script-tooprovision-a-windows-vm-and-automatically-join-it-tooan-aad-domain-services-managed-domain"></a>Сценарий tooprovision виртуальной Машины Windows и автоматически присоединить управляемого домена tooan AAD доменных служб
Этот набор команд PowerShell создает виртуальную машину для бизнес-сервера со следующими свойствами:

* Использует образ Windows Server 2012 R2 Datacenter hello.
* имеет размер "очень малая";
* Имеет имя hello Contoso100 теста.
* — Автоматически домена присоединены к домену toohello contoso100 управляемый домен.
* Добавляется toohello же виртуальной сети hello управляемого домена.

Ниже приведен полный пример скрипта toocreate hello на виртуальной машине Windows hello и автоматически присоединить управляемого домена toohello доменные службы Azure AD.

    $family="Windows Server 2012 R2 Datacenter"
    $vmname="Contoso100-test"
    $vmsize="ExtraSmall"

    $domaindns="contoso100.com"
    $domacctdomain="contoso100"

    $svcname="Contoso100-test"
    $vnetname="MyPreviewVnet"

    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

    $localadmincred=Get-Credential –Message "Type hello name and password of hello local administrator account."

    $domainadmincred=Get-Credential –Message "Now type hello name (not including hello domain) and password of an account in hello AAD DC Administrators group, that has permission tooadd hello machine toohello domain."

    $vm1 | Add-AzureProvisioningConfig -AdminUsername $localadmincred.Username -Password $localadmincred.GetNetworkCredential().Password -WindowsDomain -Domain $domacctdomain -DomainUserName $domainadmincred.Username -DomainPassword $domainadmincred.GetNetworkCredential().Password -JoinDomain $domaindns

    $vm1 | Set-AzureSubnet -SubnetNames "Subnet-1"

    $dns = New-AzureDns -Name 'contoso100-dc1' -IPAddress '10.0.0.4'

    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname -Location "Central US" -DnsSettings $dns

<br>

## <a name="related-content"></a>Похожий контент
* [Приступая к работе с доменными службами Azure AD](active-directory-ds-getting-started.md)
* [Administer an Azure AD Domain Services managed domain (Администрирование управляемого домена доменных служб Azure AD)](active-directory-ds-admin-guide-administer-domain.md)
