---
title: "списки управления aaaManage доступ к конечной точке Azure | PowerShell | Классический | Документы Microsoft"
description: "Узнайте, как toomanage списки управления доступом с помощью PowerShell"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: c84e40af-f351-4572-b3f0-d572d46bafe7
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.openlocfilehash: a7ca241ea108a266085bfb689b742d781e58da1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-endpoint-access-control-lists-using-powershell-in-hello-classic-deployment-model"></a>Управление списками управления доступом конечной точки, с помощью PowerShell в hello классической модели развертывания
Можно создать и управлять сети списки управления доступом (ACL) для конечных точек с помощью Azure PowerShell или в hello портала управления. В этом разделе мы расскажем о том, как выполнять наиболее распространенные действия со списками ACL с помощью PowerShell. Список hello Azure PowerShell командлеты разделе [командлеты управления Azure](http://go.microsoft.com/fwlink/?LinkId=317721). Дополнительные сведения о списках ACL см. в статье [Список управления доступом (ACL) конечной точки](virtual-networks-acl.md). Если toomanage списками ACL с помощью портала управления hello, см. [как tooa tooSet Настройка конечных точек виртуальной машины](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

## <a name="manage-network-acls-by-using-azure-powershell"></a>Управление сетевыми списками ACL с помощью Azure PowerShell
Можно использовать toocreate командлетов Azure PowerShell, удаления и настройки (set) сети списки управления доступом (ACL). Мы включили несколько примеров некоторых hello способов настройки ACL с помощью PowerShell.

tooretrieve полный список командлетов ACL PowerShell hello, воспользуйтесь одним из следующих hello:

    Get-Help *AzureACL*
    Get-Command -Noun AzureACLConfig

### <a name="create-a-network-acl-with-rules-that-permit-access-from-a-remote-subnet"></a>Создание сетевого списка ACL с правилами, которые разрешают доступ из удаленной подсети
в следующем примере Hello иллюстрируется способ toocreate новый список, который содержит правила. Этот список затем применяется tooa конечной точки виртуальной машины. правила списков ACL Hello в приведенном ниже примере hello разрешают доступ из удаленной подсети. toocreate нового списка управления Доступом с разрешающими правилами для удаленной подсети, откройте Azure PowerShell ISE. Скопируйте и вставьте ниже, настройка сценария hello собственными значениями hello сценарий и затем запустите скрипт hello.

1. Создайте новый объект и список управления Доступом по сети hello.
   
        $acl1 = New-AzureAclConfig
2. Настройте правило, разрешающее доступ из удаленной подсети. В следующем примере hello, задать правило *100* (имеющее приоритет выше правила 200 и более поздние версии) удаленной подсети hello tooallow *10.0.0.0/8* доступ к конечной точке виртуальной машины toohello. Замените значения hello свои собственные требования к конфигурации. Hello имя «SharePoint ACL config» следует заменить понятным именем hello требуется toocall это правило.
   
        Set-AzureAclConfig –AddRule –ACL $acl1 –Order 100 `
            –Action permit –RemoteSubnet "10.0.0.0/8" `
            –Description "SharePoint ACL config"
3. Для дополнительных правил повторите hello командлета, заменив значения hello свои собственные требования к конфигурации. Убедиться, что toochange hello правило номера заказа tooreflect hello порядок будет которой требуется применить toobe правила hello. чем меньше номер правила Hello имеет приоритет над hello большее число.
   
        Set-AzureAclConfig –AddRule –ACL $acl1 –Order 200 `
            –Action permit –RemoteSubnet "157.0.0.0/8" `
            –Description "web frontend ACL config"
4. После этого можно создать новую конечную точку (Добавить) или задать hello ACL для существующей конечной точки (Set). В этом примере мы добавим новую конечную точку виртуальной машины под названием «web» и обновление hello конечной точки виртуальной машины с hello параметры списка управления Доступом.
   
        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        | Add-AzureEndpoint –Name "web" –Protocol tcp –Localport 80 - PublicPort 80 –ACL $acl1 `
        | Update-AzureVM
5. Затем совместить командлеты hello и запустите сценарий hello. В этом примере hello объединенные командлеты будет выглядеть следующим образом:
   
        $acl1 = New-AzureAclConfig
        Set-AzureAclConfig –AddRule –ACL $acl1 –Order 100 `
            –Action permit –RemoteSubnet "10.0.0.0/8" `
            –Description "Sharepoint ACL config"
        Set-AzureAclConfig –AddRule –ACL $acl1 –Order 200 `
            –Action permit –RemoteSubnet "157.0.0.0/8" `
            –Description "web frontend ACL config"
        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        |Add-AzureEndpoint –Name "web" –Protocol tcp –Localport 80 - PublicPort 80 –ACL $acl1 `
        |Update-AzureVM

### <a name="remove-a-network-acl-rule-that-permits-access-from-a-remote-subnet"></a>Удаление из сетевого списка ACL правила, разрешающего доступ из удаленной подсети
в следующем примере Hello иллюстрируется способ tooremove Сетевые правила списка управления Доступом.  tooremove правило списка управления Доступом с разрешающими правилами для удаленной подсети, откройте Azure PowerShell ISE. Скопируйте и вставьте ниже, настройка сценария hello собственными значениями hello сценарий и затем запустите скрипт hello.

1. Первым шагом является объект списка управления Доступом hello tooget для конечной точки виртуальной машины hello. Затем необходимо удалить правило списка управления Доступом hello. В этом случае мы удаляем правило по его идентификатору. Только идентификатор правила hello 0 будут удалены из hello ACL. Не удаляет hello объекта списка управления Доступом из конечной точки виртуальной машины hello.
   
        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        | Get-AzureAclConfig –EndpointName "web" `
        | Set-AzureAclConfig –RemoveRule –ID 0 –ACL $acl1
2. Далее необходимо применить конечной точки виртуальной машины toohello объект списка управления Доступом hello и обновить hello виртуальную машину.
   
        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        | Set-AzureEndpoint –ACL $acl1 –Name "web" `
        | Update-AzureVM

### <a name="remove-a-network-acl-from-a-virtual-machine-endpoint"></a>Удаление сетевого списка ACL с конечной точки виртуальной машины
В некоторых сценариях может потребоваться tooremove объект списка управления Доступом из конечной точки виртуальной машины. toodo, откройте Azure PowerShell ISE. Скопируйте и вставьте ниже, настройка сценария hello собственными значениями hello сценарий и затем запустите скрипт hello.

        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        | Remove-AzureAclConfig –EndpointName "web" `
        | Update-AzureVM

## <a name="next-steps"></a>Дальнейшие действия
[Сетевой список управления доступом](virtual-networks-acl.md)

