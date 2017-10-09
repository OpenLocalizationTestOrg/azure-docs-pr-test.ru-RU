---
title: "Типы Runbook автоматизации aaaAzure | Документы Microsoft"
description: "Описывает различные типы hello модулей Runbook, можно использовать в службе автоматизации Azure и вопросы, которые следует учитывать при определении, какой тип toouse. "
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 9265c975-4281-4819-a84f-d86641277f36
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/01/2017
ms.author: bwren
ms.openlocfilehash: c28aa57c77025764b16784372308a4ff2f596914
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-runbook-types"></a>Типы модулей Runbook в службе автоматизации Azure
Служба автоматизации Azure поддерживает четыре типа модулей Runbook, кратко описаны в следующей таблице hello.  Hello разделы содержат дополнительные сведения о каждом типе, включая вопросы о том, когда toouse каждого.

| Тип | Описание |
|:--- |:--- |
| [Графический](#graphical-runbooks) |Опирается на Windows PowerShell, а полностью создается и редактируется в графическом редакторе на портале Azure. |
| [Графический модуль рабочего процесса PowerShell](#graphical-runbooks) |На основе рабочего процесса Windows PowerShell и графического редактора hello созданного и измененного полностью в портале Azure. |
| [PowerShell](#powershell-runbooks) |Текстовый модуль Runbook, основанный на сценарии Windows PowerShell. |
| [Рабочий процесс PowerShell](#powershell-workflow-runbooks) |Текстовый модуль Runbook, основанный на рабочем процессе Windows PowerShell. |

## <a name="graphical-runbooks"></a>Графические модули Runbook
[Графический](automation-runbook-types.md#graphical-runbooks) и графического рабочего процесса PowerShell Runbook создаются и редактировать с помощью графического редактора hello в hello портал Azure.  Можно экспортировать их в файл tooa и затем импортировать их в другую учетную запись автоматизации, но нельзя создать или изменить их с помощью другого средства.  Графические модули Runbook создают код PowerShell, однако нельзя напрямую просмотреть или изменить код hello. Графические модули Runbook не может быть преобразованный tooone hello [текстовых форматов](automation-runbook-types.md), ни runbook текст может быть преобразованный toographical формат. Графические модули Runbook может быть преобразованный tooGraphical модулях Runbook рабочего процесса PowerShell во время импорта и наоборот.

### <a name="advantages"></a>Преимущества
* Визуальная модель создания insert-link-configure.  
* Сосредоточиться на потоки данных через процесс hello  
* Визуальное представление процессов управления.  
* Включать другие модули Runbook в качестве дочерних модулей Runbook toocreate высокий уровень рабочих процессов  
* Способствует модульному программированию.  


### <a name="limitations"></a>Ограничения
* Редактировать модуль Runbook за пределами портала Azure нельзя.
* Может потребоваться действия кода, содержащего PowerShell кода tooperform сложную логику.
* Нельзя просматривать или непосредственно редактировать код PowerShell hello, созданный hello графического рабочего процесса. Обратите внимание, можно просматривать код hello, созданные в любой действия кода.

## <a name="powershell-runbooks"></a>Модули Runbook PowerShell
Модули Runbook PowerShell используют Windows PowerShell.  Можно непосредственно редактировать кода hello Runbook hello, с помощью текстового редактора hello в hello портал Azure.  Также можно использовать любой редактор текста в автономном режиме и [Импорт hello runbook](http://msdn.microsoft.com/library/azure/dn643637.aspx) в службу автоматизации Azure.

### <a name="advantages"></a>Преимущества
* Реализуйте все сложной логики с кодом PowerShell без hello дополнительные сложности рабочего процесса PowerShell. 
* Runbook запускает быстрее, чем Runbook рабочего процесса PowerShell, так как для нее не требуется toobe компиляции перед запуском.

### <a name="limitations"></a>Ограничения
* Необходимо знание сценариев PowerShell.
* Нельзя использовать [параллельной обработки](automation-powershell-workflow.md#parallel-processing) tooperform несколько действий в параллельном режиме.
* Нельзя использовать [контрольные точки](automation-powershell-workflow.md#checkpoints) tooresume runbook в случае ошибки.
* Рабочий процесс PowerShell Runbook и графические модули Runbook могут быть включены только как дочерние модули с помощью командлета Start-AzureAutomationRunbook hello, создающий новое задание.

### <a name="known-issues"></a>Известные проблемы
Ниже перечислены проблемы с модулями Runbook PowerShell, известные на данный момент.

* Runbook PowerShell не могут извлекать незашифрованный [переменный ресурс-контейнер](automation-variables.md) с пустым значением.
* Не удалось получить модули Runbook PowerShell [переменной активов](automation-variables.md) с  *~*  в имени hello.
* Модуль Get-Process в цикле в модуле Runbook PowerShell может аварийно завершить работу после примерно 80 итераций. 
* PowerShell может завершиться неуспешно, если она пытается одновременно toowrite очень большой объем данных toohello выходной поток.   Обычно можно обойти эту проблему, выводя только hello сведения, необходимые при работе с большими объектами.  Например, вместо вывода примерно *Get-Process*, можно вывести только hello необходимые поля с *Get-Process | Выберите ProcessName ЦП*.

## <a name="powershell-workflow-runbooks"></a>Модули Runbook рабочих процессов PowerShell
Runbook рабочих процессов PowerShell представляют собой текстовые Runbook, основанные на [рабочем процессе Windows PowerShell](automation-powershell-workflow.md).  Можно непосредственно редактировать кода hello Runbook hello, с помощью текстового редактора hello в hello портал Azure.  Также можно использовать любой редактор текста в автономном режиме и [Импорт hello runbook](http://msdn.microsoft.com/library/azure/dn643637.aspx) в службу автоматизации Azure.

### <a name="advantages"></a>Преимущества
* Реализация сложной логики с помощью кода рабочего процесса PowerShell.
* Используйте [контрольные точки](automation-powershell-workflow.md#checkpoints) tooresume runbook в случае ошибки.
* Используйте [параллельной обработки](automation-powershell-workflow.md#parallel-processing) tooperform несколько действий в параллельном режиме.
* Можно добавить другие графические модули Runbook и модулей Runbook рабочего процесса PowerShell как дочерние модули Runbook toocreate высокий уровень рабочих процессов.

### <a name="limitations"></a>Ограничения
* Автор должен знать рабочий процесс PowerShell.
* Runbook приходится иметь дело с hello дополнительные сложности рабочего процесса PowerShell например [десериализации объектов](automation-powershell-workflow.md#code-changes).
* Runbook принимает toostart больше времени, чем Runbook PowerShell, поскольку он должен toobe компиляции перед запуском.
* Модули Runbook PowerShell могут быть включены как дочерние модули только с помощью командлета Start-AzureAutomationRunbook hello, создающий новое задание.

## <a name="considerations"></a>Рекомендации
Следует учитывать hello учетной записи следующие дополнительные соображения при определении, какой тип toouse для конкретного модуля runbook.

* Модули Runbook не удается преобразовать из типа графического tootextual или наоборот.
* При использовании других типов дочерних модулей Runbook могут действовать некоторые ограничения.  Дополнительные сведения см. в статье [Дочерние модули Runbook в службе автоматизации Azure](automation-child-runbooks.md).

## <a name="next-steps"></a>Дальнейшие действия
* в разделе toolearn Дополнительные сведения о создании графического модуля runbook, [графический разработки автоматизации Azure](automation-graphical-authoring-intro.md)
* toounderstand hello различия между PowerShell и PowerShell рабочих процессов для модулей Runbook см. в разделе [обучения рабочего процесса Windows PowerShell](automation-powershell-workflow.md)
* Дополнительные сведения о статье toocreate или импорт модуля Runbook [Создание или импорт модуля Runbook](automation-creating-importing-runbook.md)

