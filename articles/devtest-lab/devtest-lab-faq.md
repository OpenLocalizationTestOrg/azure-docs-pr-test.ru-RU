---
title: "часто задаваемые вопросы о DevTest Labs aaaAzure | Документы Microsoft"
description: "Найти ответы на вопросы toocommon Azure DevTest Labs"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: afe83109-b89f-4f18-bddd-b8b4a30f11b4
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/22/2017
ms.author: tarcher
ms.openlocfilehash: 07d4c870eca21856750a472ed503de4a2734a438
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-devtest-labs-faq"></a>Часто задаваемые вопросы об Azure DevTest Labs
В этой статье приведены ответы на некоторые hello самые распространенные вопросы по Azure DevTest Labs.

**Общие сведения**
## <a name="what-if-my-question-isnt-answered-here"></a>Мне не удалось найти ответ на свой вопрос. Что делать?
Если вашего вопроса нет в списке, сообщите нам об этом, и мы поможем найти ответ.

* Разместить вопрос на hello [Disqus поток](#comments) в конце hello вопросы и ответы и связаться с team hello кэша Azure и другими участниками сообщества о в этой статье.
* tooreach более широкую аудиторию разместить вопрос на hello [форум Azure DevTest Labs MSDN](https://social.msdn.microsoft.com/Forums/azure/home?forum=AzureDevTestLabs)и связаться с hello Azure DevTest Labs команды и другими членами сообщества hello.
* toomake запрос на функции отправки на запросы и идеи toohello [Azure DevTest Labs User Voice](https://feedback.azure.com/forums/320373-azure-devtest-labs).

## <a name="why-should-i-use-azure-devtest-labs"></a>Почему следует использовать Azure DevTest Labs?
Azure DevTest Labs позволяет сэкономить время и сократить затраты рабочей группы. Разработчики могут создавать свои собственные среды с помощью нескольких различных базовых классов и использовать артефакты tooquickly развертывания и настройки приложений. Благодаря пользовательским образам и формулам виртуальные машины можно сохранять в качестве шаблонов, которые позже можно легко воспроизвести. Кроме того labs предлагают несколько настраиваемых политик, которые дают Администраторы лаборатории tooreduce тратить среды и управлять ими группы. К таким политикам относятся автоматическое завершение работы, пороговое значение затрат, максимальное количество виртуальных машин для каждого пользователя и максимальные размеры виртуальных машин. Более подробное объяснение Azure DevTest Labs, чтение hello [Обзор](devtest-lab-overview.md) или контрольные значения hello [видеоролике](/documentation/videos/videos/what-is-azure-devtest-labs).

## <a name="what-does-worry-free-self-service-mean"></a>Что означает "самообслуживание без проблем"?
«Затем безо всяких самообслуживания» означает, что разработчики и тест-инженеры создавать свои собственные среды при необходимости и Администраторы имеют hello безопасности знать, что Azure DevTest Labs помогает свести к минимуму тратить и управления расходами. Администраторы могут указать, какие размеры виртуальных Машин, разрешены, hello максимальное число виртуальных машин, и при запуске и завершите работу виртуальных машин. Azure DevTest Labs также позволяет легко toomonitor затраты и toostay набор предупреждения об использовании ресурсов в лаборатории hello.

## <a name="how-can-i-use-azure-devtest-labs"></a>Как можно использовать Azure DevTest Labs?
Azure DevTest Labs полезно каждый раз, когда требуется разработки или тестирования среды, и требуется, чтобы tooreproduce их быстро и/или управлять ими с помощью политик затрат.

Ниже приведено несколько сценариев использования Azure DevTest Labs.

* Управление сред разработки и тестирования в одном месте, стоимость tooreduce политики и настраиваемых образов tooshare строит между командными hello.
* Разработка приложения с помощью пользовательских образов состояния диска hello toosave на протяжении hello этапах разработки.
* Отслеживание затрат hello в tooprogress отношения.
* Создание массовых сред тестирования для гарантии качества.
* С помощью tooeasily артефактов и формулы, настройте и воспроизвести приложения в различных средах.
* Распределение виртуальных машин для hackathons (совместной разработки или тестирования работы), а также легко отменить подготовку их при завершении события hello.

## <a name="how-am-i-billed-for-azure-devtest-labs"></a>Как выставляются счета за использование Azure DevTest Labs?
Azure DevTest Labs — это бесплатная служба, то, создание лаборатории и настройка политики hello, шаблоны и артефакты предоставляется бесплатно. Вы платите только за hello Azure ресурсы, используемые в лабораториях, такие как виртуальные машины, учетные записи хранилища и виртуальных сетей. Дополнительные сведения по стоимости hello лабораторные ресурсы Узнайте, как [ценообразования Azure DevTest Labs](https://azure.microsoft.com/pricing/details/devtest-lab/).


**Безопасность**
## <a name="what-are-hello-different-security-levels-in-azure-devtest-labs"></a>Что такое hello различным уровням безопасности в Azure DevTest Labs
Доступ к DevTest Labs определяется [службой управления доступом на основе ролей Azure (RBAC)](../active-directory/role-based-access-built-in-roles.md). toounderstand способ доступа к работает, он помогает toounderstand hello различия между разрешение, роли и области в соответствии с определением RBAC.

* **Разрешение** -разрешение представляет определенное действие tooa определенного доступа. Например разрешение может быть доступ для чтения tooall виртуальных машин.
* **Роль** -роль — это набор разрешений, которые могут быть сгруппированы и назначенный пользователь tooa. Например «владелец подписки» имеет доступ к ресурсам tooall в пределах подписки.
* **Область** -область представляет уровень в иерархии hello Azure ресурса. Например область может быть группой ресурсов или одной лаборатории или hello всей подписки.

Области hello Azure DevTest Labs, существует два типа разрешений пользователя роли toodefine: владелец лаборатории и пользователя лаборатории.

* **Владелец лаборатории** -владельцем лаборатории имеет hello доступ к ресурсам tooany в лаборатории hello. Таким образом их можно изменить политики, чтения и записи все виртуальные машины, изменить hello виртуальной сети и т.д.
* **Пользователь лаборатории** — это роль, которая позволяет просматривать все ресурсы лаборатории, такие как виртуальные машины, политики и виртуальные сети, но не дает возможности изменять политики или управлять виртуальными машинами, созданными другими пользователями. Он также возможных toocreate настраиваемые роли в Azure DevTest Labs, и рассказывается, как toodo в статье hello [предоставление разрешений пользователю политики лаборатории toospecific](devtest-lab-grant-user-permissions-to-specific-lab-policies.md).

Области имеют иерархическую структуру, поэтому когда пользователю назначаются разрешения на определенном уровне, они автоматически применяются к областям более низкого уровня. Для экземпляра Если пользователю назначено toohello роль владельца подписки, то у них есть tooall доступ к ресурсам в подписке. Эти ресурсы включают все виртуальные машины, виртуальные сети и лаборатории. Таким образом владелец подписки автоматически наследует hello роль владельца лаборатории. Однако hello противоположной неверно. Владелец лаборатории имеет доступ tooa лаборатории, представляющей область, нижний уровень подписки hello. Таким образом владельцем лаборатории не может toosee виртуальных машин или виртуальные сети или все ресурсы, которые находятся вне hello лаборатории.

## <a name="how-do-i-create-a-role-tooallow-users-tooperform-a-specific-task"></a>Создание роли tooallow пользователей tooperform конкретную задачу?
Комплексный статьи о том, как toocreate пользовательские роли и назначить разрешения toothat роли можно найти здесь. Ниже приведен пример скрипта, который создает hello роль «DevTest Labs Advanced User», который имеет разрешение toostart и остановки всех виртуальных машин в лаборатории hello:

    $policyRoleDef = Get-AzureRmRoleDefinition "DevTest Labs User"
    $policyRoleDef.Actions.Remove('Microsoft.DevTestLab/Environments/*')
    $policyRoleDef.Id = $null
    $policyRoleDef.Name = "DevTest Labs Advance User"
    $policyRoleDef.IsCustom = $true
    $policyRoleDef.AssignableScopes.Clear()
    $policyRoleDef.AssignableScopes.Add("subscriptions/<subscription Id>")
    $policyRoleDef.Actions.Add("Microsoft.DevTestLab/labs/virtualMachines/Start/action")
    $policyRoleDef.Actions.Add("Microsoft.DevTestLab/labs/virtualMachines/Stop/action")
    $policyRoleDef = New-AzureRmRoleDefinition -Role $policyRoleDef  


**Интеграция и автоматизация средств непрерывной интеграции и доставки (CI/CD)**
## <a name="does-azure-devtest-labs-integrate-with-my-cicd-toolchain"></a>Можно ли интегрировать Azure DevTest Labs с собственным набором инструментов CI/CD?
При использовании VSTS имеется [расширение Azure DevTest Labs задания](https://marketplace.visualstudio.com/items?itemName=ms-azuredevtestlabs.tasks) , позволяющий tooautomate конвейера выпуска в Azure DevTest Labs. Ниже перечислены некоторые использует hello этого расширения.

* Создание и развертывание виртуальной Машины автоматически и настроить в ней последнюю сборку hello, с помощью копирования файлов Azure или PowerShell VSTS задач.
* Автоматически записи состояния hello виртуальной машины после тестирования tooreproduce ошибки на hello одной виртуальной Машины для дальнейшего изучения.
* Удаление hello ВМ в конце hello hello освободить конвейера, когда он больше не нужен.

Hello следующие записи в блогах предоставляют руководство и сведения об использовании расширения VSTS hello.

* [Azure DevTest Labs – VSTS extension (Azure DevTest Labs: расширение VSTS)](https://blogs.msdn.microsoft.com/devtestlab/2016/06/15/azure-devtest-labs-vsts-extension/)
* [Deploying a new VM in an existing AzureDevTestLab from VSTS (Развертывание из VSTS новой виртуальной машины в имеющейся лаборатории Azure DevTest Labs)](http://www.visualstudiogeeks.com/blog/DevOps/Deploy-New-VM-To-Existing-AzureDevTestLab-From-VSTS)
* [С помощью VSTS Release Management для непрерывного развертывания tooAzureDevTestLabs](http://www.visualstudiogeeks.com/blog/DevOps/Use-VSTS-ReleaseManagement-to-Deploy-and-Test-in-AzureDevTestLabs)

Для других toolchains CI/CD hello всех упомянутых выше сценарии, в которых может осуществляться через модуль задач VSTS аналогичным образом достигается путем развертывания hello [шаблоны Azure Resource Manager](https://aka.ms/dtlquickstarttemplate) с помощью [ Командлеты PowerShell Azure](../azure-resource-manager/resource-group-template-deploy.md) и [пакетами SDK .NET](https://www.nuget.org/packages/Microsoft.Azure.Management.DevTestLabs/). Можно также использовать [интерфейсы API REST для DevTest Labs](http://aka.ms/dtlrestapis) toointegrate с вашей инструментов.  


**Виртуальные машины**
## <a name="why-cant-i-see-certain-vms-in-hello-azure-virtual-machines-blade-that-i-see-within-azure-devtest-labs"></a>Не отображаются некоторые виртуальные машины в колонку hello виртуальных машинах Azure, которая отображается в Azure DevTest Labs
При создании виртуальной Машины в Azure DevTest Labs разрешение является заданным tooaccess этой виртуальной Машины. — Может tooview его в колонке labs hello и hello **виртуальные машины** колонку. Пользователи с ролью DevTest Labs hello можно увидеть все виртуальные машины, созданные в лаборатории hello через hello лаборатории **все виртуальные машины** колонку. Тем не менее пользователи с ролью DevTest Labs hello не предоставляются автоматически tooVM доступ для чтения ресурсы, созданные другими. Таким образом, эти виртуальные машины, не отображаются в hello **виртуальные машины** колонку.

## <a name="what-is-hello-difference-between-custom-images-and-formulas"></a>Что такое hello различие между пользовательских образов и формулы
Пользовательский образ — это виртуальный жесткий диск (VHD), а формула — настраиваемый образ, для которого можно задать дополнительные параметры, а затем сохранить их для воспроизведения в будущем. Пользовательское изображение может быть предпочтительнее tooquickly создать несколько сред с hello одного образа: basic, неизменяемыми. Формула может быть лучше, если требуется, чтобы конфигурация hello tooreproduce ВМ с последней bits hello, виртуальной сети и подсеть или определенного размера. Более подробное описание см. в статье hello, [сравнение пользовательских образов и формул в DevTest Labs](devtest-lab-comparing-vm-base-image-types.md).

## <a name="how-do-i-create-multiple-vms-from-hello-same-template-at-once"></a>Как создать несколько виртуальных машин из hello сразу же шаблон?
Можно использовать hello [модуль задач VSTS](https://marketplace.visualstudio.com/items?itemName=ms-azuredevtestlabs.tasks) или [сформировать шаблон диспетчера ресурсов Azure](devtest-lab-add-vm.md#save-azure-resource-manager-template) при создании виртуальной Машины и [развертывания шаблона диспетчера ресурсов Azure hello из Windows PowerShell ](../azure-resource-manager/resource-group-template-deploy.md).

## <a name="how-do-i-move-my-existing-azure-vms-into-my-azure-devtest-labs-lab"></a>Как переместить имеющиеся виртуальные машины Azure в лабораторию Azure DevTest Labs?
Выполните шаги hello ниже toocopy вашей существующей ВМ tooAzure DevTest Labs.

1. Копирование файла виртуального жесткого диска hello существующей виртуальной машины с помощью этого [сценарий Windows PowerShell](https://github.com/Azure/azure-devtestlab/blob/master/Scripts/CopyVHDFromVMToLab.ps1)
2. [Создать пользовательский образ hello](devtest-lab-create-template.md) внутри Azure DevTest Labs лаборатории.
3. Создайте виртуальную Машину в лаборатории hello из настраиваемого образа

## <a name="can-i-attach-multiple-disks-toomy-vms"></a>Можно подключить несколько toomy дисков виртуальных машин?
Присоединение несколько дисков tooVMs поддерживается.  

## <a name="if-i-want-toouse-a-windows-os-image-for-my-testing-do-i-have-toopurchase-an-msdn-subscription"></a>Если я хочу toouse образа операционной системы Windows для моей тестирования, нужно ли toopurchase подписки MSDN?
Если вам требуется toouse образов клиента Windows ОС (Windows 7 или более поздней версии) для разработки или тестирования в Azure, нажмите Да, необходимо:

- [Приобретите подписку MSDN](https://www.visualstudio.com/products/how-to-buy-vs).
- Если имеется соглашение Enterprise создать подписку Azure с hello [предложение Enterprise разработки и тестирования](https://azure.microsoft.com/en-us/offers/ms-azr-0148p).

Дополнительные сведения о hello кредиты Azure, для каждого предложения MSDN в разделе [кредит ежемесячные Azure для подписчиков Visual Studio](https://azure.microsoft.com/en-us/pricing/member-offers/msdn-benefits-details/).

## <a name="how-do-i-automate-hello-process-of-uploading-vhd-files-toocreate-custom-images"></a>Как автоматизировать процесс передачи пользовательских образов виртуальных жестких ДИСКОВ файлы toocreate hello?
Существуют два варианта:

* [Azure AzCopy](../storage/common/storage-use-azcopy.md#blob-upload) можно используется toocopy и отправка виртуального жесткого диска учетной записи для хранения файлов toohello связанной с hello лаборатории.
* [Обозреватель службы хранилища Microsoft Azure](../vs-azure-tools-storage-manage-with-storage-explorer.md) , работающее на платформе Windows, OSX и Linux.   

toofind hello целевой учетной записью хранения связанных с лаборатории, выполните следующие действия.

1. Войдите в toohello [портал Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
2. Выберите **групп ресурсов** из левой панели hello.
3. Найдите и выберите группу ресурсов hello, связанную с лаборатории.
4. На hello **Обзор** колонки, выберите одну из учетных записей хранения hello.
5. Выберите **Большие двоичные объекты**.
6. Найдите передачи файлов в списке hello. Если она не существует, возвращают tooStep #4 и попробуйте другую учетную запись.
7. Используйте hello **URL-адрес** качестве места расположения в вашей команде AzCopy.

## <a name="how-can-i-automate-hello-process-of-deleting-all-hello-vms-in-my-lab"></a>Как автоматизировать процесс удаления всех виртуальных машин hello в моей лаборатории hello
В дополнение к этому toodeleting виртуальных машин из лабораторию hello портал Azure, можно удалить все виртуальные машины hello в лаборатории с помощью сценария PowerShell. Hello следующий пример, измените значения параметров hello под hello **toochange значения** комментарий. Вы можете получить hello `subscriptionId`, `labResourceGroup`, и `labName` значения из колонки лаборатории hello в hello портал Azure.

    # Delete all hello VMs in a lab

    # Values toochange
    $subscriptionId = "<Enter Azure subscription ID here>"
    $labResourceGroup = "<Enter lab's resource group here>"
    $labName = "<Enter lab name here>"

    # Login tooyour Azure account
    Login-AzureRmAccount

    # Select hello Azure subscription that contains hello lab. This step is optional
    # if you have only one subscription.
    Select-AzureRmSubscription -SubscriptionId $subscriptionId

    # Get hello lab that contains hello VMs toodelete.
    $lab = Get-AzureRmResource -ResourceId ('subscriptions/' + $subscriptionId + '/resourceGroups/' + $labResourceGroup + '/providers/Microsoft.DevTestLab/labs/' + $labName)

    # Get hello VMs from that lab.
    $labVMs = Get-AzureRmResource | Where-Object {
              $_.ResourceType -eq 'microsoft.devtestlab/labs/virtualmachines' -and
              $_.ResourceName -like "$($lab.ResourceName)/*"}

    # Delete hello VMs.
    foreach($labVM in $labVMs)
    {
        Remove-AzureRmResource -ResourceId $labVM.ResourceId -Force
    }

**Артефакты**
## <a name="what-are-artifacts"></a>Что такое артефакты?
Артефакты, настраиваемые элементы, которые могут быть используется toodeploy вашей последней битов или вашей разработки средств на виртуальной Машине. Они являются tooyour подключенных виртуальных Машин во время создания с помощью нескольких щелчков мышью и после подготовки виртуальной Машины hello артефакты hello развертывание и настройка виртуальной Машины. В [общедоступном репозитории GitHub](https://github.com/Azure/azure-devtestlab/tree/master/Artifacts) находится несколько созданных ранее артефактов, но вы также можете без труда [создать собственные](devtest-lab-artifact-author.md).


**Настройка лаборатории**
## <a name="how-do-i-create-a-lab-from-an-azure-resource-manager-template"></a>Как создать лабораторию на основе шаблона Azure Resource Manager?
Мы предоставили [репозитории GitHub лабораторных шаблонов диспетчера ресурсов Azure](https://aka.ms/dtlquickstarttemplate) , можно развернуть в качестве- или изменить toocreate пользовательские шаблоны для вашей лабораторий. Каждый из этих шаблонов имеет ссылку, которую можно щелкнуть лаборатории hello toodeploy-находится в своей подписке Azure, или можно настроить шаблон hello и [развертывание с помощью PowerShell или Azure CLI](../azure-resource-manager/resource-group-template-deploy.md).

## <a name="why-are-my-vms-created-in-different-resource-groups-with-arbitrary-names-can-i-rename-or-modify-these-resource-groups"></a>Почему виртуальные машины создаются в разных группах ресурсов с произвольными именами? Можно ли переименовать или изменить эти группы ресурсов?
Группы ресурсов создаются таким образом в порядке для Azure DevTest Labs toomanage hello пользовательские разрешения и доступ toovirtual машины. При перемещении группы ресурсов tooanother hello виртуальной Машины на нужное имя делать так не рекомендуется. Мы работаем над повышение этого tooallow качества большую гибкость.   

## <a name="how-many-labs-can-i-create-under-hello-same-subscription"></a>Сколько labs, можно ли создать в группе hello одной подписке?
Нет определенных ограничений на число hello labs, которые могут быть созданы для каждой подписки. Однако hello ресурсы, используемые ограничены одной подписки. Вы можете прочесть об hello [ограничения и квоты, заданный для подписок Azure](../azure-subscription-service-limits.md) и [как tooincrease этих ограничений](https://azure.microsoft.com/blog/azure-limits-quotas-increase-requests).

## <a name="how-many-vms-can-i-create-per-lab"></a>Сколько виртуальных машин можно создать на лабораторию?
Нет определенных ограничений на hello число виртуальных машин, которые могут быть созданы в лаборатории. Тем не менее, ограничены hello ресурсы, используемые для каждой подписки (например Виртуальных машинах, общедоступные IP-адреса и т. д.). Вы можете прочесть об hello [ограничения и квоты, заданный для подписок Azure](../azure-subscription-service-limits.md) и [как tooincrease этих ограничений](https://azure.microsoft.com/blog/azure-limits-quotas-increase-requests).

## <a name="how-do-i-share-a-direct-link-toomy-lab"></a>Как общий доступ к лабораторной среде toomy прямую ссылку?
Прямая связь tooshare пользователи лаборатории tooyour, могут выполнять процедуры hello:

1. Обзор лаборатории toohello в hello портал Azure.
2. Скопируйте URL-адрес лаборатории hello из браузера и использовать его совместно с пользователями лаборатории.

> [!NOTE]
> Если пользователи лаборатории внешних пользователей с [учетную запись Майкрософт](#what-is-a-microsoft-account) и они не принадлежат tooyour корпоративной службой Active directory, они могут получать ошибку при навигации по toohello предоставленный ссылку. Если они получают ошибку, предложите им их имя в правом верхнем углу hello hello портал Azure и выберите hello каталог, где существует hello лаборатории из hello tooclick **каталога** части меню hello.
>
>

## <a name="what-is-a-microsoft-account"></a>Что такое учетная запись Майкрософт?
Учетная запись Майкрософт используется практически для всех действий с устройствами и службами Майкрософт. Это адрес электронной почты и пароль, используйте toosign в tooSkype, Outlook.com, OneDrive, Windows Phone и Xbox LIVE — и значит вашей файлы, фотографии, контакты и параметров можно следовать tooany устройства.

> [!NOTE]
> Учетная запись Майкрософт используется toobe название «Windows Live ID».
>
>


**Устранение неполадок**
## <a name="my-artifact-failed-during-vm-creation-how-do-i-troubleshoot-it"></a>Во время создания виртуальной машины произошел сбой артефакта. Как устранить эту проблему?
См. слишком[как toodiagnose сбоев артефакта в DevTest Labs](devtest-lab-troubleshoot-artifact-failure.md) toolearn как журналы tooobtain относительно вашего неудачных артефакта.

## <a name="why-isnt-my-existing-virtual-network-saving-properly"></a>Почему имеющаяся виртуальная сеть не сохраняется должным образом?
Причина этого может заключаться в том, что в имени виртуальной сети содержатся точки. Если таким образом, попробуйте удалить hello точки или заменив дефисы, а затем повторите попытку сохранения hello виртуальной сети.

## <a name="why-do-i-get-a-parent-resource-not-found-error-when-provisioning-a-vm-from-powershell"></a>Почему при подготовке из PowerShell выводится ошибка "Родительский ресурс не найден"?
При один ресурс является ресурсом родительского tooanother, hello родительского ресурса должна существовать до создания hello дочерний ресурс. Если он не существует, появится ошибка **ParentResourceNotFound**. Если не задать зависимость от родительского ресурса hello, hello дочерний ресурс может быть развернут перед родительского hello.

Виртуальные машины представляют собой дочерние ресурсы в лаборатории в группе ресурсов. При использовании toodeploy шаблонов диспетчера ресурсов Azure с помощью PowerShell в hello сценария PowerShell указано имя группы ресурсов hello следует имя группы ресурсов hello hello лаборатории. Дополнительные сведения см. в разделе [Устранение распространенных ошибок развертывания в Azure](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-manager-common-deployment-errors#parentresourcenotfound).

## <a name="where-can-i-find-more-error-information-if-a-vm-deployment-fails"></a>Где найти дополнительные сведения об ошибке при сбое развертывания виртуальной машины?
Ошибки при развертывании виртуальной Машины записываются в журналы действий hello. Лаборатории можно найти журналы действий виртуальных машин через hello **журналы аудита** или **диагностики виртуальной машины** ресурсов меню hello колонки виртуальной Машины лаборатории hello (hello колонке отображается после выбора hello виртуальной Машины из **Моих виртуальных машин** списка).

В некоторых случаях ошибка развертывания hello происходит перед запуском hello развертывания виртуальной Машины - например, при превышении лимита подписки hello для ресурсов, созданных с помощью hello виртуальной Машины. В этом случае сведения об ошибке hello фиксируются в уровне лаборатории hello **журналы действий** , можно найти внизу hello hello **конфигурации и политиках** параметры. Дополнительные сведения об использовании действия входит в Azure, см. в разделе [представление действие регистрирует действия tooaudit ресурсов](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-audit).

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]
