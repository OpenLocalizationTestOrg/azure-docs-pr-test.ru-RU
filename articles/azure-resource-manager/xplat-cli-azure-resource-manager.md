---
title: "ресурсы aaaManage с hello Azure CLI | Документы Microsoft"
description: "Использовать toomanage Azure интерфейс командной строки (CLI) hello Azure ресурсов и групп"
editor: 
manager: timlt
documentationcenter: 
author: tfitzmac
services: azure-resource-manager
ms.assetid: bb0af466-4f65-4559-ac3a-43985fa096ff
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 08/22/2016
ms.author: tomfitz
ms.openlocfilehash: 3df70e123d14d3bbf2648c71970bac1db4afc025
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-cli-toomanage-azure-resources-and-resource-groups"></a>Использовать toomanage Azure CLI hello Azure ресурсов и групп ресурсов
> [!div class="op_single_selector"]
> * [Портал](resource-group-portal.md) 
> * [Интерфейс командной строки Azure](xplat-cli-azure-resource-manager.md)
> * [Azure PowerShell](powershell-azure-resource-manager.md)
> * [REST API](resource-manager-rest-api.md)
> 
> 

Hello Azure командной строки (CLI Azure) является одним из нескольких средств можно использовать toodeploy и управление ресурсами с помощью диспетчера ресурсов. В этой статье описаны распространенные способы toomanage Azure ресурсов и групп ресурсов с помощью hello Azure CLI в режим диспетчера ресурсов. Сведения об использовании ресурсов toodeploy hello CLI см. в разделе [развертывания ресурсов с помощью шаблонов диспетчера ресурсов и Azure CLI](resource-group-template-deploy-cli.md). Дополнительные сведения о ресурсах Azure и диспетчер ресурсов посетите hello [Обзор диспетчера ресурсов Azure](resource-group-overview.md).

> [!NOTE]
> toomanage Azure ресурсы с hello Azure CLI требуется слишком[установить hello Azure CLI](../cli-install-nodejs.md), и [вход tooAzure](../xplat-cli-connect.md) с помощью hello `azure login` команды. Убедитесь, что hello CLI находится в режиме диспетчера ресурсов (запустить `azure config mode arm`). Если вы сделали это, вы готовы toogo.
> 
> 

## <a name="get-resource-groups-and-resources"></a>Получение сведений о ресурсах и группах ресурсов
### <a name="resource-groups"></a>Группы ресурсов
tooget список всех групп ресурсов в подписке и их расположения, выполните следующую команду.

    azure group list


### <a name="resources"></a>Ресурсы
 имя всех ресурсов в группе, например с toolist *testRG*, использовать hello следующую команду:

    azure resource list testRG

отдельный ресурс в группе hello, такие как виртуальная машина с именем tooview *MyUbuntuVM*, используйте команду hello следующим образом:

    azure resource show testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15"

Обратите внимание hello **Microsoft.Compute/virtualMachines** параметра. Этот параметр указывает тип hello hello ресурса, который вы запрашиваете сведения.

> [!NOTE]
> При использовании hello **ресурсов azure** команд, отличных от hello **списка** команды необходимо указать версию hello API hello ресурса с hello **-o** параметра. Если вы знаете о версии API hello, просмотрите файл шаблона hello и найти поле apiVersion hello для ресурса hello. Дополнительные сведения о версиях API в Resource Manager см. в статье о [поставщиках и типах ресурсов](resource-manager-supported-services.md).
> 
> 

При просмотре сведений о ресурсе, часто бывает полезно toouse hello `--json` параметра. Этот параметр становится вывода hello удобнее, так как некоторые значения являются вложенными структурами или коллекций. Hello следующем примере показано возвращение результатов hello hello **Показать** как документ JSON.

    azure resource show testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15" --json

> [!NOTE]
> Если требуется, сохраните hello toofile данных JSON с помощью hello &gt; tooa выходной файл для символа toodirect hello. Например:
> 
> `azure resource show testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15" --json > myfile.json`
> 
> 

### <a name="tags"></a>Теги
[!INCLUDE [resource-manager-tag-resources-cli](../../includes/resource-manager-tag-resources-cli.md)]

## <a name="manage-resources"></a>Управление ресурсами
tooadd ресурсов, таких как группы ресурсов tooa учетной записи хранилища, выполните команду, подобную:

    azure resource create testRG MyStorageAccount "Microsoft.Storage/storageAccounts" "westus" -o "2015-06-15" -p "{\"accountType\": \"Standard_LRS\"}"

В дополнение к этому toospecifying hello версии API-интерфейса hello ресурсов с hello **-o** параметр, используйте hello **-p** строку формата JSON toopass параметр с все необходимые или дополнительные свойства.

toodelete существующий ресурс, например, ресурсы виртуальной машины, используйте команду hello следующим образом:

    azure resource delete testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15"

toomove существующую группу ресурсов tooanother ресурсов или подписку, используйте hello **перемещение ресурсов azure** команды. Следующий пример показывает как Hello toomove tooa кэша Redis новую группу ресурсов. В hello **-i** параметр, укажите идентификатор ресурса hello toomove список разделенных запятыми.

    azure resource move -i "/subscriptions/{guid}/resourceGroups/OldRG/providers/Microsoft.Cache/Redis/examplecache" -d "NewRG"

## <a name="control-access-tooresources"></a>Tooresources управления доступом
Можно использовать toocreate hello Azure CLI и управлять ресурсами tooAzure доступа toocontrol политики. Основные сведения о определения политик и назначение политики tooresources см. в разделе [использовать ресурсы toomanage политики и управления доступом](resource-manager-policy.md).

Например определите следующие политики toodeny hello все запросы, где местоположение не Запад США или North Central US и сохраните его policy.json файла определения политики toohello:

    {
    "if" : {
        "not" : {
        "field" : "location",
        "in" : ["westus" ,  "northcentralus"]
        }
    },
    "then" : {
        "effect" : "deny"
    }
    }

Затем запустите hello **Создание определения политики** команды:

    azure policy definition create MyPolicy -p c:\temp\policy.json

Эта команда показывает, как toohello следующие выходные данные:

    + Creating policy definition MyPolicy data:    PolicyName:             MyPolicy data:    PolicyDefinitionId:     /subscriptions/########-####-####-####-############/providers/Microsoft.Authorization/policyDefinitions/MyPolicy

    data:    PolicyType:             Custom data:    DisplayName:            undefined data:    Description:            undefined data:    PolicyRule:             field=location, in=[westus, northcentralus], effect=deny

 tooassign политику в области hello, требуется, используйте hello **PolicyDefinitionId** возвращенные hello предыдущей команды. В следующем примере hello эта область является hello подписки, но вы можете задать область tooresource групп или отдельных ресурсов:

    azure policy assignment create MyPolicyAssignment -p /subscriptions/########-####-####-####-############/providers/Microsoft.Authorization/policyDefinitions/MyPolicy -s /subscriptions/########-####-####-####-############/

Можно получить, изменение или удаление определения политики с помощью hello **Показать определения политики**, **набор определения политики**, и **удаление определения политики** команд.

Аналогичным образом, можно получить, изменить или удалить назначения политики с помощью hello **показ назначения политики**, **набора назначения политики**, и **удалить назначение политики** команд .

## <a name="export-a-resource-group-as-a-template"></a>Экспорт группы ресурсов в виде шаблона
Для существующей группы ресурсов можно просмотреть hello шаблона диспетчера ресурсов для группы ресурсов hello. Экспорт шаблона hello имеет два преимущества:

1. Можно легко автоматизировать будущих развертываний hello решения, поскольку всю инфраструктуру hello определен в шаблоне hello.
2. Ознакомьтесь с синтаксисом шаблона, просмотрев hello JSON, представляющее решения.

С помощью hello Azure CLI, можно либо экспортировать шаблон, который представляет текущее состояние группы ресурсов hello, или загрузите hello шаблона, который был использован для конкретного развертывания.

* **Экспорт шаблона hello для группы ресурсов** -это полезно, если были внесены изменения группы ресурсов tooa и требуется tooretrieve hello JSON-представление текущего состояния. Тем не менее созданный шаблон hello содержит минимальным числом параметров и переменных. Большинство значений hello в шаблоне hello жестко запрограммированы. Перед развертыванием hello созданный шаблон, вы можете tooconvert несколько значений hello в параметры для настройки развертывания hello для различных сред.
  
    шаблон hello tooexport для ресурсов группы tooa локального каталога, запустите hello `azure group export` команды, как показано в следующий пример hello. (Замените указанный в примере локальный каталог каталогом, используемым в вашей операционной системе.)
  
        azure group export testRG ~/azure/templates/
* **Загрузите шаблон hello для конкретного развертывания** — это может оказаться полезным, когда требуется фактическое шаблон hello tooview, который используется toodeploy ресурсов. шаблон Hello включает все параметры и переменные, определенные для hello исходного развертывания. Тем не менее если кто-то в вашей организации группы ресурсов toohello изменений за пределами определения hello в шаблоне hello, этот шаблон не представляют Привет текущее состояние группы ресурсов hello.
  
    шаблон toodownload hello, используемый для конкретного развертывания tooa локального каталога, запустите hello `azure group deployment template download` команды. Например:
  
        azure group deployment template download TestRG testRGDeploy ~/azure/templates/downloads/

> [!NOTE]
> Так как функция экспорта шаблона пока доступна в предварительной версии, поддерживаются не все типы ресурсов. При попытке tooexport шаблона, может появиться ошибка о том, что некоторые ресурсы не были экспортированы. При необходимости эти ресурсы можно определить вручную после скачивания шаблона.
> 
> 

## <a name="next-steps"></a>Дальнейшие действия
* tooget сведения об операции развертывания и устранение ошибок при развертывании с hello Azure CLI см. в разделе [просмотреть операции развертывания](resource-manager-deployment-operations.md).
* Tooset CLI hello toouse приложения или сценария tooaccess ресурсы см [toocreate использования Azure CLI участника службы ресурсы tooaccess](resource-group-authenticate-service-principal-cli.md).
* Для получения рекомендаций по как предприятия могут использовать диспетчер ресурсов tooeffectively управление подписками см. в разделе [корпоративные функции формирования шаблонов - управление конкретные подписки](resource-manager-subscription-governance.md).

