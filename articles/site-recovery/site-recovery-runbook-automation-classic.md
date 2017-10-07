---
title: "планы toorecovery модулей Runbook службы автоматизации Azure aaaAdd классическом портале hello | Документы Microsoft"
description: "В этой статье описывается, как Azure Site Recovery теперь позволяет с помощью службы автоматизации Azure toocomplete сложных задач во время восстановления tooAzure планы восстановления tooextend"
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
ms.openlocfilehash: 3bb7420911afbce289b656f28823b1923e8af0c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="add-azure-automation-runbooks-toorecovery-plans-in-hello-classic-portal"></a>Добавить схемы toorecovery модулей Runbook службы автоматизации Azure hello классическом портале
Этот учебник описывает, как интегрируется Azure Site Recovery с планами toorecovery расширяемости tooprovide автоматизации Azure. Планы восстановления может управлять восстановления виртуальных машин, защищенных с помощью Azure Site Recovery для облака toosecondary репликации и tooAzure сценарии репликации. Они также помогут при выполнении восстановления hello **точных**, **repeatable**, и **автоматических**. Если выполняется переход к tooAzure виртуальных машин, интеграция в службе автоматизации Azure расширяет планов восстановления и дает возможность tooexecute Runbook, позволяя тем самым мощным автоматизации задач.

Если вы еще не знакомы со службой автоматизации Azure, зарегистрируйтесь [здесь](https://azure.microsoft.com/services/automation/) и скачайте примеры сценариев [здесь](https://azure.microsoft.com/documentation/scripts/). Дополнительные сведения о [Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/) и как планы восстановления tooAzure tooorchestrate, с помощью восстановления [здесь](https://azure.microsoft.com/blog/?p=166264).

В этом кратком руководстве мы рассмотрим то, как можно интегрировать модули Runbook службы автоматизации Azure в планы восстановления. Мы автоматизации простых задач, которые более ранних версий требуется ручное вмешательство и разделе как tooconvert нескольких шаг восстановления в действие восстановления одним щелчком. Также мы рассмотрим порядок устранения ошибок, возникающих при выполнении простого сценария.

## <a name="protect-hello-application-tooazure"></a>Защита tooAzure приложения hello
Начнем с простого приложения HRweb компании Fabrikam, состоящего из двух виртуальных машин: Fabrikam HRweb переднего плана и Fabrikam Hrweb серверной части являются hello две виртуальные машины, защищенные с помощью Azure Site Recovery tooAzure. tooprotect hello виртуальных машин с помощью Azure Site Recovery, выполните шаги hello.

1. Включите защиту для виртуальных машин.
2. Убедитесь, что виртуальные машины hello завершена начальная репликация и выполняется репликация.
3. Дождитесь завершения начальной репликации hello и Protected говорит hello состояние репликации.

## ![](media/site-recovery-runbook-automation/01.png)
В этом учебнике мы создадим для hello Fabrikam HRweb приложения toofailover hello приложения tooAzure плана восстановления. Затем мы будет интегрировать с runbook, который создаст конечную точку на hello отработку отказа виртуальной машины Azure tooserve веб-страниц на порт 80.

Сначала создадим план восстановления для приложения.

## <a name="create-hello-recovery-plan"></a>Создание плана восстановления hello
tooAzure приложения hello toorecover, необходимо toocreate план восстановления.
С помощью плана восстановления, которые можно задать порядок hello восстановления виртуальных машин. Hello виртуальной машине размещена в группе 1 будет восстановить и запустите первый, и следуйте hello виртуальной машины в группе 2.

Создайте план восстановления, как показано ниже.

![](media/site-recovery-runbook-automation/12.png)

Дополнительные сведения о планах восстановления, ознакомьтесь с документацией tooread [здесь](https://msdn.microsoft.com/library/azure/dn788799.aspx "здесь").

Теперь давайте создадим hello необходимые артефакты в службе автоматизации Azure.

## <a name="create-hello-automation-account-and-its-assets"></a>Создать учетную запись автоматизации hello и ресурсы
Необходимо Runbook toocreate учетной записи автоматизации Azure. Если у вас еще нет учетной записи, перейдите обозначается вкладка автоматизации tooAzure ![](media/site-recovery-runbook-automation/02.png)и создать новую учетную запись.

1. Предоставьте учетной записи hello tooidentify имя с.
2. Укажите географический регион, где требуется учетная запись tooplace hello.

Рекомендуется использовать учетную запись hello tooplace в hello же регионе, что хранилище hello ASR.

![](media/site-recovery-runbook-automation/03.png)

Создайте следующие ресурсы в учетной записи hello hello.

### <a name="add-a-subscription-name-as-asset"></a>Добавление названия подписки в качестве ресурса
1. Добавьте новый параметр ![](media/site-recovery-runbook-automation/04.png) в hello ресурсы автоматизации Azure и выберите слишком![](media/site-recovery-runbook-automation/05.png)
2. Выберите тип переменной hello как **строка**
3. В качестве имени переменной укажите **AzureSubscriptionName**

   ![](media/site-recovery-runbook-automation/06.png)
4. Задайте в качестве значения переменной hello фактическое имя подписки Azure.

   ![](media/site-recovery-runbook-automation/07_1.png)

Можно определить имя hello подписки со страницы приветствия параметры учетной записи пользователя на портал Azure hello.

### <a name="add-an-azure-login-credential-as-asset"></a>Добавление учетных данных для входа в Azure в качестве ресурса
Служба автоматизации Azure использует Azure PowerShell tooconnect toothe подписки и работает с существует артефакты hello. Для этого необходимо пройти проверку подлинности с использованием учетной записи Майкрософт или рабочей учетной записи.
Hello учетные данные можно хранить в toobe активов использовать безопасным образом модулем hello runbook.

1. Добавьте новый параметр ![](media/site-recovery-runbook-automation/04.png) в hello ресурсы автоматизации Azure и выберите пункт![](media/site-recovery-runbook-automation/09.png)
2. Выберите тип учетных данных hello как **учетные данные Windows PowerShell**
3. Укажите имя hello как **AzureCredential**

   ![](media/site-recovery-runbook-automation/10.png)
4. Укажите hello имя пользователя и пароль в toosign с.

Теперь оба этих параметра доступны в ресурсах.

![](media/site-recovery-runbook-automation/11.png)

Дополнительные сведения о предоставляется как tooconnect tooyour подписки через PowerShell [здесь](/powershell/azure/overview).

Далее будет создан модуль runbook в службе автоматизации Azure, можно добавить конечную точку для hello интерфейса виртуальной машины после отработки отказа.

## <a name="azure-automation-context"></a>Контекст службы автоматизации Azure
ASR передает контекст переменной toohello runbook toohelp детерминированным сценариев. Можно утверждать, что предсказуемы имена hello hello облачной службы и hello виртуальной машины, но происходит в том, что он не всегда hello место по причине toocertain сценариев, таких как hello один которых могли измениться имя hello hello виртуальной машины, из-за toounsupported символы в Azure. Поэтому эти сведения передаются toohello ASR плана восстановления в рамках hello *контекста*.

Ниже приведен пример того, как выглядит hello контекстной переменной.

        {"RecoveryPlanName":"hrweb-recovery",

        "FailoverType":"Test",

        "FailoverDirection":"PrimaryToSecondary",

        "GroupId":"1",

        "VmMap":{"7a1069c6-c1d6-49c5-8c5d-33bfce8dd183":

                {"CloudServiceName":"pod02hrweb-Chicago-test",

                "RoleName":"Fabrikam-Hrweb-frontend-test"}

                }

        }


в следующей таблице Hello содержит имя и описание для каждой переменной в контексте hello.

| **Имя переменной** | **Описание** |
| --- | --- |
| RecoveryPlanName |Имя выполняемого плана. Помогает выполнить действия в имени с помощью hello же сценарий |
| FailoverType |Указывает, является ли hello отработки отказа тестировать, плановой или незапланированной. |
| FailoverDirection |Укажите, является ли восстановления tooprimary или получателя |
| GroupID |Определите hello номер группы в соответствии с планом восстановления hello при выполнении плана hello |
| VmMap |Массив всех hello виртуальных машин в группе hello |
| Ключ VMMap |Уникальный ключ (GUID) для каждой виртуальной машины. Имеет hello равна hello VMM с Идентификатором hello виртуальной машины, где это возможно. |
| RoleName |Имя виртуальной Машины Azure, в которой выполняется восстановление hello |
| CloudServiceName |В разделе какие hello создается виртуальная машина Azure имя облачной службы. |

Здравствуйте, tooidentify VmMap ключ в контексте hello можно также перейти на странице свойств виртуальной Машины toohello в ASR и посмотрите на hello свойство GUID виртуальной Машины.

![](media/site-recovery-runbook-automation/13.png)

## <a name="author-an-automation-runbook"></a>Создание модуля Runbook службы автоматизации
Теперь создайте hello runbook tooopen порт 80 на виртуальной машине hello для переднего плана.

1. Создание модуля runbook в учетной записи службы автоматизации Azure с именем hello hello **OpenPort80**

   ![](media/site-recovery-runbook-automation/14.png)
2. Перейдите toohello представление Автор hello runbook и введите hello черновом режиме.
3. Сначала укажите hello переменной toouse как hello контекст плана восстановления

   ```
       param (
           [Object]$RecoveryPlanContext
       )

   ```
4. Затем подключения toohello подписку, используя имя учетных данных и подписки hello

   ```
       $Cred = Get-AutomationPSCredential -Name 'AzureCredential'

       # Connect tooAzure
       $AzureAccount = Add-AzureAccount -Credential $Cred
       $AzureSubscriptionName = Get-AutomationVariable –Name ‘AzureSubscriptionName’
       Select-AzureSubscription -SubscriptionName $AzureSubscriptionName
   ```

   Обратите внимание, что используется hello Azure активы — **AzureCredential** и **AzureSubscriptionName** здесь.
5. Теперь укажите сведения о конечной точке hello и hello GUID hello виртуальной машины, для которого требуется конечная точка tooexpose hello. Виртуальная машина переднего плана вариантов hello.

   ```
       # Specify hello parameters toobe used by hello script
       $AEProtocol = "TCP"
       $AELocalPort = 80
       $AEPublicPort = 80
       $AEName = "Port 80 for HTTP"
       $VMGUID = "7a1069c6-c1d6-49c5-8c5d-33bfce8dd183"
   ```

   Указывает hello протокола конечной точки Azure, локальный на hello виртуальной Машины и ее сопоставленных открытый порт. Эти переменные, параметры, необходимые по hello Azure команды, добавить tooVMs конечных точек. Hello VMGUID содержит hello hello виртуальная машина, которую требуется toooperate на идентификатор GUID.
6. Hello скрипт будет извлечь hello контекст для hello, заданный идентификатором GUID виртуальной Машины и создайте конечную точку на виртуальной машине hello, он ссылается.

   ```
       #Read hello VM GUID from hello context
       $VM = $RecoveryPlanContext.VmMap.$VMGUID

       if ($VM -ne $null)
       {
           # Invoke pipeline commands within an InlineScript

           $EndpointStatus = InlineScript {
               # Invoke hello necessary pipeline commands tooadd a Azure Endpoint tooa specified Virtual Machine
               # Commands include: Get-AzureVM | Add-AzureEndpoint | Update-AzureVM (including parameters)

               $Status = Get-AzureVM -ServiceName $Using:VM.CloudServiceName -Name $Using:VM.RoleName | `
                   Add-AzureEndpoint -Name $Using:AEName -Protocol $Using:AEProtocol -PublicPort $Using:AEPublicPort -LocalPort $Using:AELocalPort | `
                   Update-AzureVM
               Write-Output $Status
           }
       }
   ```
7. После завершения этого процесса попаданий публикации ![](media/site-recovery-runbook-automation/20.png) tooallow toobe вашего сценария, для выполнения.

для справки ниже приведен полный сценарий Hello

```
  workflow OpenPort80
  {
    param (
        [Object]$RecoveryPlanContext
    )

    $Cred = Get-AutomationPSCredential -Name 'AzureCredential'

    # Connect tooAzure
    $AzureAccount = Add-AzureAccount -Credential $Cred
    $AzureSubscriptionName = Get-AutomationVariable –Name ‘AzureSubscriptionName’
    Select-AzureSubscription -SubscriptionName $AzureSubscriptionName

    # Specify hello parameters toobe used by hello script
    $AEProtocol = "TCP"
    $AELocalPort = 80
    $AEPublicPort = 80
    $AEName = "Port 80 for HTTP"
    $VMGUID = "7a1069c6-c1d6-49c5-8c5d-33bfce8dd183"

    #Read hello VM GUID from hello context
    $VM = $RecoveryPlanContext.VmMap.$VMGUID

    if ($VM -ne $null)
    {
        # Invoke pipeline commands within an InlineScript

        $EndpointStatus = InlineScript {
            # Invoke hello necessary pipeline commands tooadd an Azure Endpoint tooa specified Virtual Machine
            # This set of commands includes: Get-AzureVM | Add-AzureEndpoint | Update-AzureVM (including necessary parameters)

            $Status = Get-AzureVM -ServiceName $Using:VM.CloudServiceName -Name $Using:VM.RoleName | `
                Add-AzureEndpoint -Name $Using:AEName -Protocol $Using:AEProtocol -PublicPort $Using:AEPublicPort -LocalPort $Using:AELocalPort | `
                Update-AzureVM
            Write-Output $Status
        }
    }
  }
```

## <a name="add-hello-script-toohello-recovery-plan"></a>Добавление плана восстановления toohello сценария hello
После подготовки скрипта hello, его можно добавить toohello план восстановления, созданной ранее.

1. В план восстановления hello, который вы создали выберите tooadd сценарий после группы 2. ![](media/site-recovery-runbook-automation/15.png)
2. Укажите название сценария. Это просто понятное имя для этого сценария для отображение в плане восстановления hello.
3. В скрипте tooAzure hello перехода на другой ресурс — выберите имя учетной записи службы автоматизации Azure hello.
4. Выберите runbook hello, созданные в hello Azure модули Runbook.

![](media/site-recovery-runbook-automation/16.png)

## <a name="primary-side-scripts"></a>Первичные сценарии
При выполнении tooAzure перехода на другой ресурс, также можно tooexecute первичный скриптов. Эти скрипты будут выполняться на сервере VMM hello во время перехода на другой ресурс.
Первичные сценарии доступны только для этапов «до выключения» и «после выключения». Это так, как ожидается, что основной сайт toobe hello обычно недоступна при аварии на сервере.
Во время внеплановой отработки отказа только в том случае, если вы выбрали в операциях первичного сайта, он предпримет toorun hello первичный скриптов. Если они не доступны или тайм-аута hello отработки отказа продолжит toorecover hello виртуальных машин.
Первичный сценариев без доступны для узлов VMware или физических/Hyper-v без VMM защищенных tooAzure - во время перехода на другой ресурс tooAzure.
Тем не менее, когда восстановление из Azure tooon организациями, первичный скриптов (Runbooks) может использоваться для всех целевых объектов, за исключением VMware.

## <a name="test-hello-recovery-plan"></a>План восстановления hello тестирования
После добавления hello runbook toohello плана можно инициировать тестовую отработку отказа и посмотрите в действии. Всегда рекомендуется toorun tootest теста отработки отказа вашего приложения и hello восстановления плана tooensure, нет ли ошибок.

1. Выберите план восстановления hello и инициировать тестовую отработку отказа.
2. Во время выполнения плана hello вы увидите hello runbook выполнен или не с помощью его состояние.

   ![](media/site-recovery-runbook-automation/17.png)
3. Можно также просмотреть hello сведения о состоянии выполнения runbook на странице заданий службы автоматизации Azure hello hello runbook.

   ![](media/site-recovery-runbook-automation/18.png)
4. После завершения отработки отказа hello, отдельно от результата выполнения модуля runbook hello, видно ли hello выполнение было успешным или нет, посетив страницу приветствия виртуальной машины Azure и оценив hello конечных точек.

![](media/site-recovery-runbook-automation/19.png)

## <a name="sample-scripts"></a>Примеры сценариев
Хотя мы рассмотрения автоматизация один часто используемые задачи по добавлению конечной точки tooan виртуальной машины Azure в этом учебнике, можно выполнить ряд других мощных автоматизации задач, с помощью автоматизации Azure. Корпорация Майкрософт и сообщества Azure Automation hello предоставляют образцы модулей Runbook, которые помогут вам приступить к созданию собственного решения и программа Runbook, которые можно использовать в качестве стандартных блоков для более крупных задач автоматизации. Начать использовать их из галереи hello и мощные восстановления одним щелчком на планы построения для приложений с помощью Azure Site Recovery.

## <a name="additional-resources"></a>Дополнительные ресурсы
[Обзор службы автоматизации Azure](http://msdn.microsoft.com/library/azure/dn643629.aspx "Обзор службы автоматизации Azure")

[Примеры сценариев службы автоматизации Azure](http://gallery.technet.microsoft.com/scriptcenter/site/search?f\[0\].Type=User&f\[0\].Value=SC%20Automation%20Product%20Team&f\[0\].Text=SC%20Automation%20Product%20Team "Примеры сценариев службы автоматизации Azure")
