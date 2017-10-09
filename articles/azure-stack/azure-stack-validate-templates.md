---
title: "шаблоны toocheck aaaUse шаблона проверяющий элемент управления для Azure стек | Документы Microsoft"
description: "Проверьте шаблоны для развертывания tooAzure стека"
services: azure-stack
documentationcenter: 
author: HeathL17
manager: byronr
editor: 
ms.assetid: d9e6aee1-4cba-4df5-b5a3-6f38da9627a3
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: helaw
ms.openlocfilehash: ee649f2ebf77486ca5036116dd73a45d66884704
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="check-your-templates-for-azure-stack-with-template-validator"></a>Проверьте свои шаблоны для стека Azure с помощью шаблона проверяющий элемент управления
Можно использовать toocheck средство проверки шаблона hello, если диспетчер ресурсов Azure [шаблоны](azure-stack-arm-templates.md) готовы для Azure стека. Средство проверки шаблона Hello доступен как часть средств Azure стека hello. Загрузить набор средств hello Azure стека с помощью hello действия, описанные в hello [загрузить набор средств из GitHub](azure-stack-powershell-download.md) статьи. 

шаблоны toovalidate использовать следующие модули PowerShell hello и hello JSON-файл расположен в **TemplateValidator** и **CloudCapabilities** папок: 

 - AzureRM.CloudCapabilities.psm1 создает файл JSON возможности облака, представляющий службы hello и версии в облаке как стек Azure.
 - AzureRM.TemplateValidator.psm1 использует возможности облачной среды шаблонов tootest файлов JSON для развертывания в Azure стека.
 - AzureStackCloudCapabilities_with_AddOns_20170627.json — это файл возможностей облака по умолчанию.  Можно создавать собственные или использовать этот файл, tooget работы. 

В этом разделе выполнить проверку шаблоны и при необходимости создайте файл возможностей облака.

## <a name="validate-templates"></a>Проверить шаблоны
В этом пошаговом руководстве проверить шаблоны с помощью модуля AzureRM.TemplateValidator PowerShell hello. Можно использовать собственные шаблоны, или проверить hello [быстрый запуск Azure стека шаблоны](https://github.com/Azure/AzureStack-QuickStart-Templates).

1.  Импортируйте модуль AzureRM.TemplateValidator.psm1 PowerShell hello:
    
    ```PowerShell
    cd "c:\AzureStack-Tools-master\TemplateValidator"
    Import-Module .\AzureRM.TemplateValidator.psm1
    ```

2.  Выполните hello шаблона проверяющий элемент управления.

    ```PowerShell
    Test-AzureRMTemplate -TemplatePath <path tootemplate.json or template folder> `
    -CapabilitiesPath <path toocloudcapabilities.json> `
    -Verbose
    ```

Любой шаблон предупреждений и ошибок проверки являются toohello регистрируется консоли PowerShell и — журнал tooan HTML-файл в исходной папке hello. Пример выходных данных отчетов проверки hello выглядит следующим образом:

![отчет о проверке образца](./media/azure-stack-validate-templates/image1.png)

### <a name="parameters"></a>Параметры

| Параметр | Описание | Обязательно |
| ----- | -----| ----- |
| TemplatePath | Указывает путь toorecursively hello найти шаблоны диспетчера ресурсов | Да | 
| TemplatePattern | Указывает имя hello toomatch файлы шаблона. | Нет |
| CapabilitiesPath | Указывает hello путь toocloud возможности JSON-файла | Да | 
| IncludeComputeCapabilities | Включает в себя оценки IaaS ресурсов, таких как размеров ВМ и расширения ВМ | Нет |
| IncludeStorageCapabilities | Включает в себя оценки ресурсов хранения, таких как типы SKU | Нет |
| Отчет | Указывает, что имя hello созданный отчет HTML | Нет |
| Подробная информация | Журналы ошибок и предупреждений toohello консоли | Нет|


### <a name="examples"></a>Примеры
В этом примере проверяет все hello [быстрый запуск Azure стека шаблоны](https://github.com/Azure/AzureStack-QuickStart-Templates) загружен локально, а также проверяет hello размеров ВМ и расширения относительно возможностей Azure стека Development Kit.

```PowerShell
test-AzureRMTemplate -TemplatePath C:\AzureStack-Quickstart-Templates `
-CapabilitiesPath .\TemplateValidator\AzureStackCloudCapabilities_with_AddOns_20170627.json.json `
-TemplatePattern MyStandardTemplateName.json`
-IncludeComputeCapabilities`
-Report TemplateReport.html
```

## <a name="build-cloud-capabilities-file"></a>Построение файла возможностей облака
Hello загруженные файлы включают значение по умолчанию *AzureStackCloudCapabilities_with_AddOns_20170627.json* файл, который описывает доступны в пакете средств разработки Azure стека hello службы версии с установленными службами PaaS.  Если установить дополнительные поставщики ресурсов, можно использовать hello toobuild модуль AzureRM.CloudCapabilities PowerShell JSON-файла, включая новые службы hello.  

1.  Убедитесь, что у вас есть подключение tooAzure стека.  Эти шаги можно выполнить на узел комплект средств для разработки Azure стека hello, или можно использовать [VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn) tooconnect с рабочей станции. 
2.  Импортируйте модуль AzureRM.CloudCapabilities PowerShell hello:

    ```PowerShell
    Import-Module .\CloudCapabilities\AzureRM.CloudCapabilities.psm1
    ``` 

3.  Используют версии обновления tooretrieve командлет Get-CloudCapabilities hello и создать файл JSON возможностей облака:

    ```PowerShell
    Get-AzureRMCloudCapabilities -Location 'local' -Verbose
    ```             


## <a name="next-steps"></a>Дальнейшие действия
 - [Развертывание шаблонов tooAzure стека](azure-stack-arm-templates.md)
 - [Разработки шаблонов для стека Azure] (azure стека разрабатывать templates.md)

