---
title: "Добавление модулей Runbook службы автоматизации Azure в планы восстановления на классическом портале | Документация Майкрософт"
description: "В этой статье описывается, как Azure Site Recovery позволяет расширить планы восстановления с помощью службы автоматизации Azure для выполнения сложных задач во время восстановления в Azure."
services: site-recovery
documentationcenter: 
author: ruturaj
manager: gauravd
editor: 
ms.assetid: f24eaa62-9dea-4fce-92e1-a72513ca0289
ms.service: site-recovery
ms.devlang: powershell
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: storage-backup-recovery
ms.date: 08/11/2017
ms.author: ruturajd
ms.openlocfilehash: 0a248e7c3f39a35ac10dc6ac64e5cef7d152e033
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="add-azure-automation-runbooks-to-recovery-plans-in-the-classic-portal"></a>Добавление модулей Runbook службы автоматизации Azure в планы восстановления на классическом портале
В этом руководстве описывается, как Azure Site Recovery интегрируется со службой автоматизации Azure для обеспечения расширяемости для планов восстановления. Планы восстановления позволяют управлять восстановлением виртуальных машин, защищенных с помощью Azure Site Recovery, как для репликации в дополнительное облако, так и для репликации в сценарии Azure. Они также помогают реализовать **точное**, **воспроизводимое** и **автоматическое** восстановление. Если выполняется отработка отказа с переносом виртуальных машин в Azure, интеграция со службой автоматизации Azure позволяет расширить планы восстановления и предоставляет возможность выполнять Runbook, а это, в свою очередь, позволяет значительно облегчить выполнение задач автоматизации.

Если вы еще не знакомы со службой автоматизации Azure, зарегистрируйтесь [здесь](https://azure.microsoft.com/services/automation/) и скачайте примеры сценариев [здесь](https://azure.microsoft.com/documentation/scripts/). Дополнительные сведения об [Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/) и о том, как управлять восстановлением в Azure с помощью планов восстановления, см. [здесь](https://azure.microsoft.com/blog/?p=166264).

В этом кратком руководстве мы рассмотрим то, как можно интегрировать модули Runbook службы автоматизации Azure в планы восстановления. Мы автоматизируем выполнение простых задач, которые ранее требовалось выполнять вручную, и узнаем, как преобразовать процесс восстановления, включающий несколько этапов, в действие восстановления одним щелчком мыши. Также мы рассмотрим порядок устранения ошибок, возникающих при выполнении простого сценария.

## <a name="protect-the-application-to-azure"></a>Защита приложения в Azure
Начнем с простого приложения HRweb компании Fabrikam, состоящего из двух виртуальных машин: Fabrikam-HRweb-frontend и Fabrikam-Hrweb-backend. Эти виртуальные машины защищены в Azure с помощью Azure Site Recovery. Чтобы защитить виртуальные машины с помощью Azure Site Recovery, выполните указанные ниже действия.

1. Включите защиту для виртуальных машин.
2. Убедитесь, что виртуальные машины завершили начальную репликацию и выполняют репликацию.
3. Дождитесь завершения начальной репликации (в столбце "Состояние репликации" должно быть указано "Защищено").

## ![](media/site-recovery-runbook-automation/01.png)
В этом руководстве мы создадим план восстановления для приложения HRweb компании Fabrikam для отработки отказа приложения с переносом его в Azure. Затем мы интегрируем приложение с модулем Runbook, который создаст конечную точку на резервной виртуальной машине Azure для обслуживания веб-страниц через порт 80.

Сначала создадим план восстановления для приложения.

## <a name="create-the-recovery-plan"></a>Создание плана восстановления
Чтобы восстановить приложение в Azure, необходимо создать план восстановления.
С помощью плана восстановления можно задать порядок восстановления виртуальных машин. Виртуальная машина, помещенная в группу 1, будет восстановлена и запущена первой, после чего аналогичные действия выполняются для виртуальной машины в группе 2.

Создайте план восстановления, как показано ниже.

![](media/site-recovery-runbook-automation/12.png)

Дополнительные сведения о планах восстановления см. в документации, представленной[здесь](https://msdn.microsoft.com/library/azure/dn788799.aspx "здесь").

Теперь создадим необходимые артефакты в службе автоматизации Azure.

## <a name="create-the-automation-account-and-its-assets"></a>Создание учетной записи службы автоматизации и соответствующих ресурсов
Для создания модулей Runbook требуется учетная запись службы автоматизации Azure. Если у вас еще нет такой учетной записи, перейдите на вкладку службы автоматизации Azure, обозначенную как ![](media/site-recovery-runbook-automation/02.png), и создайте учетную запись.

1. Присвойте имя учетной записи для ее идентификации.
2. Укажите географический регион, где требуется разместить учетную запись.

Учетную запись рекомендуется размещать в том же регионе, в котором находится хранилище ASR.

![](media/site-recovery-runbook-automation/03.png)

Затем создадим в учетной записи указанные ниже ресурсы.

### <a name="add-a-subscription-name-as-asset"></a>Добавление названия подписки в качестве ресурса
1. Добавьте новый параметр ![](media/site-recovery-runbook-automation/04.png) в разделе ресурсов службы автоматизации Azure и нажмите ![](media/site-recovery-runbook-automation/05.png).
2. В качестве типа переменной выберите **Строка**
3. В качестве имени переменной укажите **AzureSubscriptionName**

   ![](media/site-recovery-runbook-automation/06.png)
4. В качестве значения переменной укажите фактическое имя подписки Azure.

   ![](media/site-recovery-runbook-automation/07_1.png)

Имя подписки указано на странице параметров учетной записи на портале Azure.

### <a name="add-an-azure-login-credential-as-asset"></a>Добавление учетных данных для входа в Azure в качестве ресурса
Служба автоматизации Azure использует Azure PowerShell для подключения к подписке и оперирования артефактами. Для этого необходимо пройти проверку подлинности с использованием учетной записи Майкрософт или рабочей учетной записи.
Учетные данные можно хранить в ресурсе для их безопасного использования модулем Runbook.

1. Добавьте новый параметр ![](media/site-recovery-runbook-automation/04.png) в разделе ресурсов службы автоматизации Azure и нажмите ![](media/site-recovery-runbook-automation/09.png).
2. Для параметра "Тип учетных данных" выберите **Учетные данные Windows PowerShell**
3. Укажите имя **AzureCredential**

   ![](media/site-recovery-runbook-automation/10.png)
4. Укажите имя пользователя и пароль для входа.

Теперь оба этих параметра доступны в ресурсах.

![](media/site-recovery-runbook-automation/11.png)

Дополнительные сведения о подключении к подписке через PowerShell см. [здесь](/powershell/azure/overview).

Затем создадим в службе автоматизации Azure модуль Runbook, который может добавить конечную точку для интерфейсной виртуальной машины после отработки отказа.

## <a name="azure-automation-context"></a>Контекст службы автоматизации Azure
ASR передает в модуль Runbook переменную контекста, которая помогает создавать детерминированные сценарии. Кто-то может утверждать, что имена облачной службы и виртуальной машины предсказуемые, однако это не всегда так, поскольку существуют сценарии, в которых, например, имя виртуальной машины могло быть изменено из-за неподдерживаемых Azure символов. Поэтому такая информация передается в план восстановления ASR как часть *контекста*.

Ниже приведен пример того, как выглядит переменная контекста.

        {"RecoveryPlanName":"hrweb-recovery",

        "FailoverType":"Test",

        "FailoverDirection":"PrimaryToSecondary",

        "GroupId":"1",

        "VmMap":{"7a1069c6-c1d6-49c5-8c5d-33bfce8dd183":

                {"CloudServiceName":"pod02hrweb-Chicago-test",

                "RoleName":"Fabrikam-Hrweb-frontend-test"}

                }

        }


В таблице ниже указаны имя и описание для каждой переменной в контексте.

| **Имя переменной** | **Описание** |
| --- | --- |
| RecoveryPlanName |Имя выполняемого плана. Позволяет предпринять действия на основе имени, используя тот же скрипт |
| FailoverType |Указывает, является ли выполнение тестовым, запланированным или незапланированным. |
| FailoverDirection |Указывает, производится ли восстановление в первичное или вторичное расположение |
| GroupID |Определяет номер группы в плане восстановления при выполнении плана |
| VmMap |Это массив всех виртуальных машин в группе. |
| Ключ VMMap |Уникальный ключ (GUID) для каждой виртуальной машины. Это то же самое, что и VMM ID виртуальной машины, там, где это применимо. |
| RoleName |Имя виртуальной машины Azure, для которой выполняется восстановление |
| CloudServiceName |Имя облачной службы Azure, под которой создана виртуальная машина. |

Чтобы определить переменную VmMap Key в контексте, также можно перейти на страницу свойств виртуальной машины в ASR и обратиться к свойству VMGUID.

![](media/site-recovery-runbook-automation/13.png)

## <a name="author-an-automation-runbook"></a>Создание модуля Runbook службы автоматизации
Теперь создадим модуль Runbook для открытия порта 80 на интерфейсной виртуальной машине.

1. Создайте новый модуль Runbook в учетной записи службы автоматизации Azure и присвойте ему имя **OpenPort80**

   ![](media/site-recovery-runbook-automation/14.png)
2. Перейдите в представление создания модуля Runbook и войдите в режиме черновика.
3. Сначала укажите переменную, которая будет использоваться в качестве контекста плана восстановления.

   ```
       param (
           [Object]$RecoveryPlanContext
       )

   ```
4. Затем подключитесь к подписке, указав учетные данные и имя подписки.

   ```
       $Cred = Get-AutomationPSCredential -Name 'AzureCredential'

       # Connect to Azure
       $AzureAccount = Add-AzureAccount -Credential $Cred
       $AzureSubscriptionName = Get-AutomationVariable –Name ‘AzureSubscriptionName’
       Select-AzureSubscription -SubscriptionName $AzureSubscriptionName
   ```

   Обратите внимание, что здесь используются ресурсы **AzureCredential** и **AzureSubscriptionName**.
5. Теперь укажите сведения о конечной точке и идентификатор GUID виртуальной машины, для которой требуется предоставить конечную точку. В данном случае это интерфейсная виртуальная машина.

   ```
       # Specify the parameters to be used by the script
       $AEProtocol = "TCP"
       $AELocalPort = 80
       $AEPublicPort = 80
       $AEName = "Port 80 for HTTP"
       $VMGUID = "7a1069c6-c1d6-49c5-8c5d-33bfce8dd183"
   ```

   Эти сведения включают протокол конечной точки Azure, локальный порт на виртуальной машине и сопоставленный ему открытый порт. Эти переменные выступают в качестве параметров, необходимых для выполнения команд Azure по добавлению конечных точек для виртуальных машин. VMGUID содержит идентификатор GUID виртуальной машины, с которой необходимо выполнить требуемые операции.
6. Теперь этот сценарий позволит извлечь контекст для заданного идентификатора VMGUID и создать конечную точку на виртуальной машине, на которую указывает этот идентификатор.

   ```
       #Read the VM GUID from the context
       $VM = $RecoveryPlanContext.VmMap.$VMGUID

       if ($VM -ne $null)
       {
           # Invoke pipeline commands within an InlineScript

           $EndpointStatus = InlineScript {
               # Invoke the necessary pipeline commands to add a Azure Endpoint to a specified Virtual Machine
               # Commands include: Get-AzureVM | Add-AzureEndpoint | Update-AzureVM (including parameters)

               $Status = Get-AzureVM -ServiceName $Using:VM.CloudServiceName -Name $Using:VM.RoleName | `
                   Add-AzureEndpoint -Name $Using:AEName -Protocol $Using:AEProtocol -PublicPort $Using:AEPublicPort -LocalPort $Using:AELocalPort | `
                   Update-AzureVM
               Write-Output $Status
           }
       }
   ```
7. После этого нажмите "Опубликовать" ![](media/site-recovery-runbook-automation/20.png) , чтобы сценарий стал доступен для выполнения.

Ниже приведен полный код сценария для справки.

```
  workflow OpenPort80
  {
    param (
        [Object]$RecoveryPlanContext
    )

    $Cred = Get-AutomationPSCredential -Name 'AzureCredential'

    # Connect to Azure
    $AzureAccount = Add-AzureAccount -Credential $Cred
    $AzureSubscriptionName = Get-AutomationVariable –Name ‘AzureSubscriptionName’
    Select-AzureSubscription -SubscriptionName $AzureSubscriptionName

    # Specify the parameters to be used by the script
    $AEProtocol = "TCP"
    $AELocalPort = 80
    $AEPublicPort = 80
    $AEName = "Port 80 for HTTP"
    $VMGUID = "7a1069c6-c1d6-49c5-8c5d-33bfce8dd183"

    #Read the VM GUID from the context
    $VM = $RecoveryPlanContext.VmMap.$VMGUID

    if ($VM -ne $null)
    {
        # Invoke pipeline commands within an InlineScript

        $EndpointStatus = InlineScript {
            # Invoke the necessary pipeline commands to add an Azure Endpoint to a specified Virtual Machine
            # This set of commands includes: Get-AzureVM | Add-AzureEndpoint | Update-AzureVM (including necessary parameters)

            $Status = Get-AzureVM -ServiceName $Using:VM.CloudServiceName -Name $Using:VM.RoleName | `
                Add-AzureEndpoint -Name $Using:AEName -Protocol $Using:AEProtocol -PublicPort $Using:AEPublicPort -LocalPort $Using:AELocalPort | `
                Update-AzureVM
            Write-Output $Status
        }
    }
  }
```

## <a name="add-the-script-to-the-recovery-plan"></a>Добавление сценария в план восстановления
После того как сценарий готов, его можно добавить в план восстановления, который был создан ранее.

1. В созданном ранее плане восстановления выберите команду добавления сценария после группы 2. ![](media/site-recovery-runbook-automation/15.png)
2. Укажите название сценария. Достаточно указать понятное имя для этого сценария для отображения в плане восстановления.
3. В поле выбора сценария отработки отказа в Azure выберите в раскрывающемся списке имя учетной записи службы автоматизации Azure.
4. В поле выбора сценария модуля Runbook Azure выберите в раскрывающемся списке созданный вами модуль.

![](media/site-recovery-runbook-automation/16.png)

## <a name="primary-side-scripts"></a>Первичные сценарии
При отработке отказа в Azure также можно выбрать первичные сценарии для выполнения. Эти сценарии будут запущены на сервере VMM при отработке отказа.
Первичные сценарии доступны только для этапов «до выключения» и «после выключения». Это объясняется тем, что первичный сценарий обычно считается недоступным при возникновении сбоя.
Во время внеплановой отработки отказа первичные сценарии будут запущены только в том случае, если вы выбрали их запуск. Если они недоступны или тайм-аут их ожидания истек, отработка отказа будет продолжена для восстановления виртуальных машин.
При отработке отказа в Azure первичные сценарии недоступны для сайтов VMware/Hyper-v и физических узлов, на которых не настроена защита VMM на Azure.
Однако при отработке отказа из Azure в локальную среду сценарии для первичных реплик могут использоваться для всех целевых объектов, за исключением VMware.

## <a name="test-the-recovery-plan"></a>Тестирование плана восстановления
После добавления модуля Runbook в план можно запустить тестовую отработку отказа и посмотреть модуль в действии. Рекомендуется всегда выполнить тестовую отработку отказа для тестирования приложения и плана восстановления, чтобы убедиться в отсутствии ошибок.

1. Выберите план восстановления и запустите тестовую отработку отказа.
2. Во время выполнения плана можно просмотреть, был ли выполнен модуль или нет, обратившись к сведениям о его состоянии.

   ![](media/site-recovery-runbook-automation/17.png)
3. Кроме того, можно перейти на страницу заданий службы автоматизации Azure для модуля, чтобы ознакомиться с подробными сведениями о состоянии выполнении модуля Runbook.

   ![](media/site-recovery-runbook-automation/18.png)
4. После завершения отработки отказа, помимо результатов выполнения модуля Runbook, можно просмотреть сведения о том, было ли выполнение успешным. Для этого посетите страницу виртуальной машины Azure и обратитесь к сведениям о конечных точках.

![](media/site-recovery-runbook-automation/19.png)

## <a name="sample-scripts"></a>Примеры сценариев
В данном руководстве мы рассмотрели автоматизацию одной часто используемой задачи по добавлению конечной точки к виртуальной машине Azure, однако с помощью службы автоматизации Azure можно выполнять множество других задач по эффективной автоматизации. Мы совместно с сообществом, которое создалось вокруг службы автоматизации Azure, предоставляем примеры модулей Runbook, которые помогут вам научиться создавать собственные решения, а также вспомогательные модули, которые можно использовать для создания более крупных задач автоматизации. Приступите к работе с ними и воспользуйтесь коллекцией примеров для создания эффективных планов восстановления своих приложений одним щелчком мыши с помощью Azure Site Recovery.

## <a name="additional-resources"></a>Дополнительные ресурсы
[Обзор службы автоматизации Azure](http://msdn.microsoft.com/library/azure/dn643629.aspx "Обзор службы автоматизации Azure")

[Примеры сценариев службы автоматизации Azure](http://gallery.technet.microsoft.com/scriptcenter/site/search?f\[0\].Type=User&f\[0\].Value=SC%20Automation%20Product%20Team&f\[0\].Text=SC%20Automation%20Product%20Team "Примеры сценариев службы автоматизации Azure")
