---
title: "масштабирования виртуальных машин aaaMake наборов, доступных в стек Azure"
description: "Узнайте, как добавить администратора облака toohello масштабирования виртуальной машины Azure Marketplace стека"
services: azure-stack
author: anjayajodha
ms.service: azure-stack
ms.topic: article
ms.date: 8/4/2017
ms.author: anajod
keywords: 
ms.openlocfilehash: 14365d62ac2f2bc453c25ce4769464eb30180ea8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="make-virtual-machine-scale-sets-available-in-azure-stack"></a>Открытие набора масштабирования виртуальной машины в стек Azure
Наборы масштабирования виртуальной машины — это ресурс Azure стека вычислений. Можно использовать их toodeploy и управление набором одинаковые виртуальные машины. Здравствуйте, же со всех виртуальных машин, наборы масштабирования не требуется предварительно подготовку виртуальных машин. Это упрощает toobuild крупномасштабных служб, предназначенных для больших вычислений, большие наборы данных и контейнерах рабочих нагрузок.

В этом разделе поможет hello процесса toomake наборы масштабирования в Azure Marketplace стека hello. После завершения этой процедуры, пользователи могут добавлять подписки tootheir наборов масштабирования виртуальных машин.

Наборы масштабирования виртуальных машин Azure стеке похожи на наборы масштабирования виртуальных машин в Azure. Дополнительные сведения см. в разделе hello следующие видео:
* [Марк Руссинович (Mark Russinovich) рассказывает о масштабируемых наборах Azure.](https://channel9.msdn.com/Blogs/Regular-IT-Guy/Mark-Russinovich-Talks-Azure-Scale-Sets/)
* [Масштабируемые наборы виртуальных машин с Гаем Бауэрманом (Guy Bowerman).](https://channel9.msdn.com/Shows/Cloud+Cover/Episode-191-Virtual-Machine-Scale-Sets-with-Guy-Bowerman)

Стек Azure наборы масштабирования виртуальных машин не поддерживают автоматическое масштабирование. Можно добавить дополнительные экземпляры tooa масштабирования, заданные с помощью портала Azure стека hello, шаблоны диспетчера ресурсов или PowerShell.

## <a name="prerequisites"></a>Предварительные требования
* **PowerShell и средства**

   Установка и настроенный PowerShell для Azure стека и средства Azure стека hello. В разделе [приступить к работе с PowerShell Azure стека](azure-stack-powershell-configure-quickstart.md).

   После установки средств Azure стека hello, убедитесь, что импорт hello следующий модуль PowerShell (toohello относительный путь. \ComputeAdmin папки в папке hello AzureStack средства главным):

        Import-Module .\AzureStack.ComputeAdmin.psm1

* **Образ операционной системы**

   Если вы не добавляли tooyour образа операционной системы Azure Marketplace стека, см. раздел [добавить hello виртуальной Машины Windows Server 2016 изображения toohello стека Azure marketplace](azure-stack-add-default-image.md).

   Поддержка Linux загрузить Ubuntu Server 16.04 и добавить его с помощью ```Add-AzsVMImage``` с hello следующие параметры: ```-publisher "Canonical" -offer "UbuntuServer" -sku "16.04-LTS"```.

## <a name="add-hello-virtual-machine-scale-set"></a>Добавление набора масштабирования виртуальных машин hello

Измените hello следующие команды PowerShell, скрипт для вашей среды, а затем запустите ее tooadd tooyour набор масштабирования виртуальной машины Azure Marketplace стека. 

``$User``— Учетная запись hello, портал администратора hello tooconnect использовать. Например, serviceadmin@contoso.onmicrosoft.com.

```
$Arm = "https://adminmanagement.local.azurestack.external"
$Location = "local"

Add-AzureRMEnvironment -Name AzureStackAdmin -ArmEndpoint $Arm

$Password = ConvertTo-SecureString -AsPlainText -Force "<your Azure Stack administrator password>"

$User = "<your Azure Stack service administrator user name>"

$Creds =  New-Object System.Management.Automation.PSCredential $User, $Password

$AzsEnv = Get-AzureRmEnvironment AzureStackAdmin
$AzsEnvContext = Add-AzureRmAccount -Environment $AzsEnv -Credential $Creds
Select-AzureRmProfile -Profile $AzsEnvContext

Select-AzureRmSubscription -SubscriptionName "Default Provider Subscription"

Add-AzsVMSSGalleryItem -Location $Location
```

## <a name="remove-a-virtual-machine-scale-set"></a>Удалить набор масштабирования виртуальной машины

tooremove элемент коллекции набора масштабирования виртуальных машин, запустите следующую команду PowerShell hello:

    Remove-AzsVMSSGalleryItem

> [!NOTE]
> элемент коллекции Hello не может быть удалено непосредственно. Может потребоваться несколько раз toorefresh hello портала, перед удалением из hello Marketplace.


## <a name="next-steps"></a>Дальнейшие действия
[Часто задаваемые вопросы про Azure стека](azure-stack-faq.md)

