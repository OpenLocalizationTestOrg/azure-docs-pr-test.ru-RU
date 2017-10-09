---
title: "планы toorecovery aaaAdd автоматизации Azure модули Runbook в Azure Site Recovery | Документы Microsoft"
description: "Узнайте, как Azure Site Recovery помогает расширить планы восстановления с помощью службы автоматизации Azure. Узнайте, как toocomplete комплексных задач во время восстановления tooAzure."
services: site-recovery
documentationcenter: 
author: ruturaj
manager: gauravd
editor: 
ms.assetid: ecece14d-5f92-4596-bbaf-5204addb95c2
ms.service: site-recovery
ms.devlang: powershell
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: storage-backup-recovery
ms.date: 06/23/2017
ms.author: ruturajd@microsoft.com
ms.openlocfilehash: 90d517200cec5527e98a0d00da466bace587b70b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="add-azure-automation-runbooks-toorecovery-plans"></a>Добавить схемы toorecovery модулей Runbook службы автоматизации Azure
В этой статье описывается как интегрируется Azure Site Recovery с toohelp автоматизации Azure расширить планах восстановления. Планы восстановления могут управлять восстановлением виртуальных машин, защищенных с помощью Azure Site Recovery. Планы восстановления работают как для репликации tooa вторичное облако, так и для tooAzure репликации. Планы восстановления также помогают сделать hello восстановления **точных**, **repeatable**, и **автоматических**. Если переход на виртуальных машинах tooAzure интеграции в службе автоматизации Azure расширяет планах восстановления. Его можно использовать tooexecute Runbook, которые предоставляют мощные автоматизации задач.

Если новый tooAzure автоматизации, вы можете [зарегистрироваться](https://azure.microsoft.com/services/automation/) и [загрузить примеры скриптов](https://azure.microsoft.com/documentation/scripts/). Дополнительные сведения и toolearn как tooorchestrate tooAzure восстановления с помощью [планы восстановления](https://azure.microsoft.com/blog/?p=166264), в разделе [Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/).

В этой статье мы описываем, как интегрировать модули Runbook службы автоматизации Azure в планы восстановления. Мы используем простейших задач tooautomate примеры, которые ранее требуется ручное вмешательство. Мы также рассматриваются как tooconvert tooa восстановления многоэтапной одним щелчком действия по восстановлению.

## <a name="customize-hello-recovery-plan"></a>Настройка плана восстановления hello
1. Go toohello **Site Recovery** колонки ресурсов для плана восстановления. В этом примере hello план восстановления содержит две tooit добавленные виртуальные машины, для восстановления. Добавление модуля runbook toobegin щелкните hello **Настройка** вкладки.

    ![При нажатии кнопки настройки hello](media/site-recovery-runbook-automation-new/essentials-rp.png)


2. Щелкните правой кнопкой мыши элемент **Группа 1: запуск**, а затем выберите **Добавить завершающее действие**.

    ![Щелкните правой кнопкой мыши элемент "Группа 1: запуск" и добавьте завершающее действие.](media/site-recovery-runbook-automation-new/customize-rp.png)

3. Нажмите **Выбрать сценарий**.

4. На hello **действие обновления** колонки, сценарий приветствия имен **Hello World**.

    ![Колонка действие обновления Hello](media/site-recovery-runbook-automation-new/update-rp.png)

5. Введите имя учетной записи службы автоматизации Azure.
    >[!NOTE]
    > Hello учетной записи автоматизации могут находиться в любом регионе Azure. Hello учетной записи автоматизации должны находиться в hello той же подписке, хранилище Azure Site Recovery hello.

6. В учетной записи службы автоматизации Azure выберите Runbook. Этот runbook — hello сценарий, который выполняется во время выполнения hello hello плана восстановления, после восстановления hello hello первой группы.

7. сценарий toosave hello, нажмите кнопку **ОК**. Hello скрипт добавляется слишком**группа 1: после действия**.

    !["Группа 1: запуск", последующие действия](media/site-recovery-runbook-automation-new/addedscript-rp.PNG)


## <a name="considerations-for-adding-a-script"></a>Рекомендации по добавлению сценария

* Для параметров слишком**удалить шаг** или **hello скрипт обновления**, щелкните правой кнопкой мыши сценарий hello.
* Можно запустить сценарий в Azure во время отработки отказа из локальной машины tooAzure. Он также может запускать на платформе Azure как сценарий первичный сайт перед завершением работы, при отработке отказа из Azure tooan на локальном компьютере.
* При запуске сценарий внедряет контекст плана восстановления. Следующий пример Hello показана переменная контекста:

    ```
            {"RecoveryPlanName":"hrweb-recovery",

            "FailoverType":"Test",

            "FailoverDirection":"PrimaryToSecondary",

            "GroupId":"1",

            "VmMap":{"7a1069c6-c1d6-49c5-8c5d-33bfce8dd183":

                    { "SubscriptionId":"7a1111111-c1d6-49c5-8c5d-111ce8dd183",

                    "ResourceGroupName":"ContosoRG",

                    "CloudServiceName":"pod02hrweb-Chicago-test",

                    "RoleName":"Fabrikam-Hrweb-frontend-test",

                    "RecoveryPointId":"TimeStamp"}

                    }

            }
    ```

    Привет, в следующей таблице перечислены hello имя и описание каждой переменной в контексте hello.

    | **Имя переменной** | **Описание** |
    | --- | --- |
    | RecoveryPlanName |Имя плана hello Hello. Эта переменная помогает выполнять различные действия на основе имени плана восстановления hello. Также можно повторно использовать скрипт hello. |
    | FailoverType |Указывает, является ли тест hello отработки отказа, плановой или незапланированной. |
    | FailoverDirection |Указывает, является ли восстановления tooa первичного или вторичного сайта. |
    | GroupID |Определяет номер группы hello в плане восстановления hello, при выполнении плана hello. |
    | VmMap |Массив всех виртуальных машин в группе hello. |
    | Ключ VMMap |Уникальный ключ (GUID) для каждой виртуальной машины. Его hello таким же, как hello Azure Virtual Machine Manager (VMM) идентификатор hello виртуальной Машины, где это возможно. |
    | SubscriptionId |Идентификатор подписки Azure Hello Здравствуйте виртуальной Машины, в котором был создан. |
    | RoleName |Имя Hello hello виртуальной Машине Azure, в которой выполняется восстановление. |
    | CloudServiceName |Hello имя облачной службы Azure Здравствуйте виртуальных Машин, под которой был создан. |
    | ResourceGroupName|Имя группы ресурсов Azure Hello, под которой hello виртуальной Машины была создана. |
    | RecoveryPointId|Hello отметка времени при восстановлении hello виртуальной Машины. |

* Убедитесь, что для этой учетной записи автоматизации hello hello следующие модули:
    * AzureRM.profile
    * AzureRM.Resources
    * AzureRM.Automation
    * AzureRM.Network
    * AzureRM.Compute

Все эти модули должны иметь совместимые версии. Простой способ tooensure все модули совместимы — toouse hello последние версии всех модулей hello.

### <a name="access-all-vms-of-hello-vmmap-in-a-loop"></a>Доступ к hello VMMap в цикле все виртуальные машины
Используйте следующие tooloop кода для всех виртуальных машин, hello Microsoft VMMap hello.

```
$VMinfo = $RecoveryPlanContext.VmMap | Get-Member | Where-Object MemberType -EQ NoteProperty | select -ExpandProperty Name
$vmMap = $RecoveryPlanContext.VmMap
 foreach($VMID in $VMinfo)
 {
     $VM = $vmMap.$VMID                
             if( !(($VM -eq $Null) -Or ($VM.ResourceGroupName -eq $Null) -Or ($VM.RoleName -eq $Null))) {
         #this check is tooensure that we skip when some data is not available else it will fail
 Write-output "Resource group name ", $VM.ResourceGroupName
 Write-output "Rolename " = $VM.RoleName
     }
 }

```

> [!NOTE]
> Hello ресурсов группы и роли значения имени были пустыми, если hello сценария — это группа загрузки tooa перед действием. заполняется значениями Hello только в том случае, если переход на другой ресурс успешно hello виртуальной Машины из этой группы. сценарий Hello — после действия группы загрузки hello.

## <a name="use-hello-same-automation-runbook-in-multiple-recovery-plans"></a>Используйте hello же runbook службы автоматизации в несколько планов восстановления

Один и тот же сценарий можно использовать в нескольких планах восстановления, передавая ему внешние переменные. Можно использовать [переменных службы автоматизации Azure](../automation/automation-variables.md) выполнение плана toostore параметры, которые можно передать для восстановления. Добавляя имя плана восстановления hello как переменная toohello префикс, можно создать отдельные переменные для каждого плана восстановления. Затем с помощью переменных hello в качестве параметров. Можно изменить параметр без изменения сценария hello, но по-прежнему изменение hello, каким образом hello скрипт работает.

### <a name="use-a-simple-string-variable-in-a-runbook-script"></a>Использование простых строковых переменных в сценарии Runbook

В этом примере сценария принимает входные данные hello объекта группы безопасности сети (NSG) и применяет его toohello виртуальные машины плана восстановления.

Сценарий toodetect hello, используемого плана восстановления выполняется при помощи контекста плана восстановления hello:

```
workflow AddPublicIPAndNSG {
    param (
          [parameter(Mandatory=$false)]
          [Object]$RecoveryPlanContext
    )

    $RPName = $RecoveryPlanContext.RecoveryPlanName
```

tooapply существующей NSG, необходимо знать имя NSG hello и имя группы ресурсов NSG hello. Используйте эти переменные в качестве входных данных для сценариев плана восстановления. toodo это, создайте две переменные hello ресурсы учетной записи автоматизации. Добавьте имя hello hello плана восстановления, для которого создается как имя переменной toohello префикс параметров hello.

1. Создайте имя переменной toostore hello NSG. Добавьте имя переменной toohello префикс с помощью hello имя плана восстановления hello.

    ![Создание переменной для имени NSG](media/site-recovery-runbook-automation-new/var1.png)

2. Создайте NSG hello переменной toostore имя группы ресурсов. Добавьте имя переменной toohello префикс с помощью hello имя плана восстановления hello.

    ![Создание имени группы ресурсов NSG](media/site-recovery-runbook-automation-new/var2.png)


3.  В сценарии hello используйте следующие hello ссылаться на значения переменных hello tooget кода:

    ```
    $NSGValue = $RecoveryPlanContext.RecoveryPlanName + "-NSG"
    $NSGRGValue = $RecoveryPlanContext.RecoveryPlanName + "-NSGRG"

    $NSGnameVar = Get-AutomationVariable -Name $NSGValue
    $RGnameVar = Get-AutomationVariable -Name $NSGRGValue
    ```

4.  Используйте переменные hello в hello runbook tooapply hello NSG toohello сетевому интерфейсу hello отработка отказа виртуальной Машины:

    ```
    InlineScript {
    if (($Using:NSGname -ne $Null) -And ($Using:NSGRGname -ne $Null)) {
            $NSG = Get-AzureRmNetworkSecurityGroup -Name $Using:NSGname -ResourceGroupName $Using:NSGRGname
            Write-output $NSG.Id
            #Apply hello NSG tooa network interface
            #$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
            #Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd `
            #  -AddressPrefix 192.168.1.0/24 -NetworkSecurityGroup $NSG
        }
    }
    ```

Для каждого плана восстановления создайте независимых переменных, чтобы можно было повторно использовать скрипт hello. Добавление префикса с помощью hello имя плана восстановления. Полный, конца в конец скрипта для этого сценария см. в разделе [добавить открытый IP-адрес и NSG tooVMs во время тестовой отработки отказа плана восстановления Site Recovery](https://gallery.technet.microsoft.com/Add-Public-IP-and-NSG-to-a6bb8fee).


### <a name="use-a-complex-variable-toostore-more-information"></a>Используйте toostore переменной сложного Дополнительные сведения

Рассмотрим ситуацию, в которой будет tooturn один скрипт на общедоступный IP-адрес на конкретных виртуальных машин. В другом сценарии может потребоваться tooapply другой Nsg на разных виртуальных машинах (не на всех виртуальных машинах). Такой сценарий можно многократно использовать для других планов восстановления. Каждый план восстановления может иметь разное число виртуальных машин. Например, точка восстановления SharePoint имеет два внешних интерфейса, а простые бизнес-приложения — только один. В такой ситуации мы не можем просто создать отдельные переменные для каждого плана восстановления. 

В следующем примере hello, мы используем новый метод и создать [переменной сложного](https://msdn.microsoft.com/library/dn913767.aspx?f=255&MSPPError=-2147217396) в ресурсах учетной записи службы автоматизации Azure hello. с несколькими значениями. Необходимо использовать toocomplete hello Azure PowerShell, следующие шаги:

1. В PowerShell войдите в tooyour подписки Azure.

    ```
    login-azurermaccount
    $sub = Get-AzureRmSubscription -Name <SubscriptionName>
    $sub | Select-AzureRmSubscription
    ```

2. Параметры toostore hello, создание переменной сложного hello с помощью hello имя плана восстановления hello.

    ```
    $VMDetails = @{"VMGUID"=@{"ResourceGroupName"="RGNameOfNSG";"NSGName"="NameOfNSG"};"VMGUID2"=@{"ResourceGroupName"="RGNameOfNSG";"NSGName"="NameOfNSG"}}
        New-AzureRmAutomationVariable -ResourceGroupName <RG of Automation Account> -AutomationAccountName <AA Name> -Name <RecoveryPlanName> -Value $VMDetails -Encrypted $false
    ```

3. В этой переменной комплексного **VMDetails** — hello ИД виртуальной Машины, к hello защищенных виртуальных Машин. hello tooget ИД виртуальной Машины в hello портал Azure, просмотреть свойства виртуальной Машины hello. Hello следующем снимке экрана показана переменная, которая хранит hello сведения о двух других виртуальных машин:

    ![Здравствуйте, GUID служит hello ИД виртуальной Машины](media/site-recovery-runbook-automation-new/vmguid.png)

4. Используйте эту переменную в модуле runbook. Если hello указывает, что GUID виртуальной Машины находится в контексте плана восстановления hello, применяются hello NSG на hello виртуальной Машины.

    ```
    $VMDetailsObj = Get-AutomationVariable -Name $RecoveryPlanContext.RecoveryPlanName
    ```

4. В модуле runbook цикла по виртуальным машинам hello контекста плана восстановления hello. Проверьте, существует ли hello виртуальной Машины в **$VMDetailsObj**. Если он существует, доступ к свойствам hello hello hello переменной tooapply NSG:

    ```
        $VMinfo = $RecoveryPlanContext.VmMap | Get-Member | Where-Object MemberType -EQ NoteProperty | select -ExpandProperty Name
        $vmMap = $RecoveryPlanContext.VmMap

        foreach($VMID in $VMinfo) {
            Write-output $VMDetailsObj.value.$VMID

            if ($VMDetailsObj.value.$VMID -ne $Null) { #If hello VM exists in hello context, this will not b Null
                $VM = $vmMap.$VMID
                # Access hello properties of hello variable
                $NSGname = $VMDetailsObj.value.$VMID.'NSGName'
                $NSGRGname = $VMDetailsObj.value.$VMID.'NSGResourceGroupName'

                # Add code tooapply hello NSG properties toohello VM
            }
        }
    ```

Hello же скрипт можно использовать для планов восстановления. Введите различные параметры, сохраняя значение hello, которое соответствует tooa плана восстановления в различные переменные.

## <a name="sample-scripts"></a>Примеры сценариев

tooyour скрипты образца toodeploy учетной записи автоматизации, нажмите кнопку hello **развертывание tooAzure** кнопки.

[![Развертывание tooAzure](https://azurecomcdn.azureedge.net/mediahandler/acomblog/media/Default/blog/c4803408-340e-49e3-9a1f-0ed3f689813d.png)](https://aka.ms/asr-automationrunbooks-deploy)

Еще один пример см. следующие видео hello. Здесь показано, как toorecover tooAzure двухуровневая WordPress приложения:


> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/One-click-failover-of-a-2-tier-WordPress-application-using-Azure-Site-Recovery/player]



## <a name="additional-resources"></a>Дополнительные ресурсы
* [Учетная запись запуска от имени службы автоматизации Azure](../automation/automation-sec-configure-azure-runas-account.md)
* [Обзор службы автоматизации Azure](http://msdn.microsoft.com/library/azure/dn643629.aspx "Обзор службы автоматизации Azure")
* [Примеры сценариев службы автоматизации Azure](http://gallery.technet.microsoft.com/scriptcenter/site/search?f\[0\].Type=User&f\[0\].Value=SC%20Automation%20Product%20Team&f\[0\].Text=SC%20Automation%20Product%20Team "Примеры сценариев службы автоматизации Azure")
