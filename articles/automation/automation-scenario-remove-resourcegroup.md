---
title: "Удаление группы ресурсов aaaAutomate | Документы Microsoft"
description: "Версия рабочего процесса PowerShell сценария автоматизации Azure, включая модули Runbook tooremove группы всех ресурсов в вашей подписке."
services: automation
documentationcenter: 
author: MGoedtel
manager: jwhit
editor: 
ms.assetid: b848e345-fd5d-4b9d-bc57-3fe41d2ddb5c
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 09/26/2016
ms.author: magoedte
ms.openlocfilehash: d7ff8064842385d57b0eebdf7b263150c958255f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-scenario---automate-removal-of-resource-groups"></a>Сценарий службы автоматизации Azure: автоматизация удаления групп ресурсов
Многие клиенты создают несколько групп ресурсов. Одни можно использовать для управления рабочими приложениями, а другие — в качестве промежуточных сред или сред разработки и тестирования. Автоматизировать развертывание hello эти ресурсы — это одно, но может toodecommission группу ресурсов одним щелчком кнопки «hello», будет другой. С помощью службы автоматизации Azure можно упростить эту распространенную задачу управления. Это полезно, если вы работаете с подпиской Azure, предельная через предложение для участников как MSDN или hello программы Microsoft Partner Network Cloud Essentials.

Этот сценарий основан на модуле runbook PowerShell и является спроектированный tooremove одну или несколько групп ресурсов, определяющие из подписки. Hello по умолчанию hello runbook, tootest, прежде чем продолжить. Это гарантирует, что не удалить случайно hello группы ресурсов, прежде чем вы будете готовы toocomplete этой процедуры.   

## <a name="getting-hello-scenario"></a>Начало сценария hello
Этот сценарий состоит из runbook PowerShell, который можно загрузить из hello [коллекции PowerShell](https://www.powershellgallery.com/packages/Remove-ResourceGroup/1.0/DisplayScript). Можно также импортировать его непосредственно из hello [коллекции модулей Runbook](automation-runbook-gallery.md) в hello портал Azure.<br><br>

| Модуль Runbook | Описание |
| --- | --- |
| Remove-ResourceGroup |Удаляет один или несколько групп ресурсов Azure и связанные ресурсы из подписки hello. |

<br>
для этого модуля runbook определяются Hello следующие входные параметры.

| Параметр | Описание |
| --- | --- |
| NameFilter (обязательный) |Указывает имя фильтра toolimit hello групп ресурсов, которые будут при удалении. Можно передать несколько значений, указав их через запятую.<br>Hello фильтр не учитывает регистр и будет соответствовать любой группы ресурсов, которая содержит строку hello. |
| PreviewMode (необязательный) |Выполняет toosee runbook hello групп ресурсов, которые будут удалены, но не выполняет никаких действий.<br>по умолчанию Hello — **true** toohelp избежать случайного удаления одного или нескольких групп ресурсов, переданным toohello runbook. |

## <a name="install-and-configure-this-scenario"></a>Установка и настройка сценария
### <a name="prerequisites"></a>Предварительные требования
Этот модуль runbook выполняет проверку подлинности с помощью hello [учетная запись запуска от имени Azure](automation-sec-configure-azure-runas-account.md).    

### <a name="install-and-publish-hello-runbooks"></a>Установка и публикации Runbook hello
После загрузки hello runbook, его можно импортировать с помощью процедуры hello в [импорта runbook процедуры](automation-creating-importing-runbook.md#importing-a-runbook-from-a-file-into-azure-automation). Опубликуйте hello runbook после его успешного импорта в вашу учетную запись автоматизации.

## <a name="using-hello-runbook"></a>С помощью hello runbook
Hello ниже поможет hello выполнение этого runbook и помогут ознакомиться с ее работе. Будет только тестироваться hello runbook в этом примере фактически не удаление группы ресурсов hello.  

1. Откройте учетную запись автоматизации hello портал Azure и щелкните **Runbooks**.
2. Выберите hello **удаление ResourceGroup** runbook и нажмите кнопку **запустить**.
3. При запуске hello runbook hello **запустить Runbook** открывает колонку и можно настроить параметры hello. Введите имена hello групп ресурсов в подписке можно использовать для тестирования и вызовет вреда, если случайно удален.<br> ![Параметры модуля Remove-ResouceGroup](media/automation-scenario-remove-resourcegroup/remove-resourcegroup-input-parameters.png)

   > [!NOTE]
   > Убедитесь, что **Previewmode** задано слишком**true** tooavoid удаление hello выбранные группы ресурсов.  **Примечание** этот runbook не удалит hello группы ресурсов, содержащий hello учетной записи автоматизации, на котором выполняется этот runbook.  
   >
   >
4. После настройки все значения параметров hello установите **ОК**, и hello runbook будут помещены в очередь для выполнения.  

Подробности hello tooview hello **удаление ResourceGroup** задания runbook в hello портал Azure, выберите **заданий** в hello runbook. Hello задания сводки Вывод hello входных параметров и вывода hello потока Кроме toogeneral сведения о задании hello и любые исключения, которые возникают.<br> ![Состояние задания модуля Runbook Remove-ResourceGroup](media/automation-scenario-remove-resourcegroup/remove-resourcegroup-runbook-job-status.png).

Hello **Сводка заданий** включает в себя сообщения из hello потоков вывода, предупреждения и ошибки. Выберите **вывода** tooview подробные результаты из выполнения runbook hello.<br> ![Выходные данные модуля Runbook Remove-ResourceGroup](media/automation-scenario-remove-resourcegroup/remove-resourcegroup-runbook-job-output.png)

## <a name="next-steps"></a>Дальнейшие действия
* tooget к созданию собственного модуля runbook в разделе [Создание или импорт модуля runbook в автоматизации Azure](automation-creating-importing-runbook.md).
* tooget к работе с модулями Runbook рабочего процесса PowerShell, в разделе [Мой первый runbook рабочего процесса PowerShell](automation-first-runbook-textual.md).
