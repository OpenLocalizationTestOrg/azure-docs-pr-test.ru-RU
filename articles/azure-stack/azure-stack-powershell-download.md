---
title: "средства Azure стека aaaDownload из GitHub | Документы Microsoft"
description: "Узнайте, как средства toodownload необходимые toowork со стеком Azure."
services: azure-stack
documentationcenter: 
author: SnehaGunda
manager: byronr
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: sngun
ms.openlocfilehash: a88c97b0ef1dd70e63771f0607cc07ec7a00b533
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="download-azure-stack-tools-from-github"></a>Загрузить набор средств Azure стека из GitHub

Средства AzureStack является репозиторием GitHub, на котором размещена модули PowerShell можно использовать toomanage и развертывать ресурсы tooAzure стека. Можно загрузить и использовать эти PowerShell модули toohello пакет средств разработки Azure стека или tooa на основе windows внешний клиент при планировании tooestablish VPN-подключение. tooobtain этих средств, клонирование репозитория GitHub hello или hello средства AzureStack папка загрузки. 

репозиторий tooclone hello, загрузите [Git](https://git-scm.com/download/win) для Windows, откройте окно командной строки и выполните следующий скрипт hello:

```PowerShell
# Change directory toohello root directory 
cd \

# clone hello repository
git clone https://github.com/Azure/AzureStack-Tools.git --recursive

# Change toohello tools directory
cd AzureStack-Tools
```

toodownload hello папке инструменты, запустите следующий сценарий hello:

```PowerShell
# Change directory toohello root directory 
cd \

# Download hello tools archive
invoke-webrequest `
  https://github.com/Azure/AzureStack-Tools/archive/master.zip `
  -OutFile master.zip

# Expand hello downloaded files
expand-archive master.zip `
  -DestinationPath . `
  -Force

# Change toohello tools directory
cd AzureStack-Tools-master

```

## <a name="functionalities-provided-by-hello-modules"></a>Функциональные возможности, предоставляемые hello модулей

репозиторий Hello средства AzureStack содержит модули PowerShell, которые поддерживают следующие функции для стека Azure hello:  

| Функции | Описание | Этот модуль, который можно использовать? |
| --- | --- | --- |
| [Возможности облака](azure-stack-validate-templates.md) | Используйте этот модуль tooget hello возможности облачной среды облака. Например можно получить hello возможностей облака, такие как версия API, ресурсы диспетчера ресурсов Azure, расширения виртуальных Машин и т.д. для стека Azure и Azure облака, использующие этот модуль. | Облако администраторов и пользователей. |
| [Администрирование вычислений Azure стека](azure-stack-add-vm-image.md) | Используйте этот модуль tooadd или удалите образ виртуальной Машины из стека Azure marketplace hello. | Администраторов облака. |
| [Администрирование Azure инфраструктуры стека](https://github.com/Azure/AzureStack-Tools/blob/master/Infrastructure/README.md) | Используйте этот модуль toomanage стека Azure инфраструктуры виртуальных машин, предупреждения, обновления и т. д. |  Администраторов облака.|
| [Политика диспетчера ресурсов для стек Azure](azure-stack-policy-module.md) | Использовать этот модуль tooconfigure подписки Azure или групповую ресурс Azure с hello же управления версиями и доступность службы как стек Azure. | Облако Администраторы и пользователи |
| [Зарегистрировать в Azure](azure-stack-register.md) | Используйте этот модуль tooregister экземпляра комплект средств для разработки с Azure. После регистрации, можно загрузить элементы marketplace hello из Azure и использовать их в стек Azure. | Администраторов облака |
| [Развертывания Azure стека](azure-stack-run-powershell-script.md) | Используйте этот модуль tooprepare hello Azure стека узла компьютера toodeploy и повторное развертывание с помощью образа Azure стека виртуального жесткого Disk(VHD) hello. | Администраторов облака. |
| [Подключение tooAzure стека](azure-stack-connect-powershell.md) | Используйте этот экземпляр модуля tooconnect tooan стека Azure через PowerShell и tooconfigure tooAzure подключения VPN стека. | Облако Администраторы и пользователи |
| [Администрирование служб Azure стека](azure-stack-create-offer.md) | Azure стека администраторы могут использовать этот модуль toocreate, обеспечивают клиента по умолчанию с неограниченной квоты, между службами вычислений, хранения, сеть и хранилище ключей.   | Администраторов облака.|
| [Проверяющий элемент управления шаблона](azure-stack-validate-templates.md) | Используйте этот модуль tooverify, если существующий или новый шаблон может быть развернутой tooAzure стека. | Облако Администраторы и пользователи |


## <a name="next-steps"></a>Дальнейшие действия
* [Настройка среды PowerShell hello Azure стека пользователя](azure-stack-powershell-configure-user.md)   
* [Подключение через виртуальную частную сеть tooAzure пакет средств разработки стека](azure-stack-connect-azure-stack.md)  
