---
title: "модуль и aaaRunbook галерей для службы автоматизации Azure | Документы Microsoft"
description: "Модулей Runbook и модулей из сообщества Майкрософт и hello доступны для вас tooinstall и используется в среде автоматизации Azure.  Этой статье описывается, как можно использовать эти ресурсы и toocontribute галереи toohello модулей Runbook."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: d3fee7b4-630a-4c10-8425-9bf51d7c9e58
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/14/2016
ms.author: magoedte;bwren
ms.openlocfilehash: 10b634460edf66dd7548017e3a2f7111b7125f30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="runbook-and-module-galleries-for-azure-automation"></a>Коллекции модулей Runbook и других модулей для службы автоматизации Azure
Вместо создания собственных модулей Runbook и модулей в службе автоматизации Azure, доступны различные сценарии, уже созданных сообществом Майкрософт и hello.  Эти готовые сценарии можно применять без изменений или использовать в качестве отправной точки, модифицируя их под свои задачи.

Модули Runbook можно получить из hello [коллекции модулей Runbook](#runbooks-in-runbook-gallery) и модули из hello [коллекции PowerShell](#modules-in-powerShell-gallery).  Вы можете также создавать сообщества toohello сценарии, разрабатываемые для управления доступом.

## <a name="runbooks-in-runbook-gallery"></a>Модули Runbook в коллекции Runbook
Hello [коллекции модулей Runbook](http://gallery.technet.microsoft.com/scriptcenter/site/search?f\[0\].Type=RootCategory&f\[0\].Value=WindowsAzure&f\[1\].Type=SubCategory&f\[1\].Value=WindowsAzure_automation&f\[1\].Text=Automation) предоставляет широкий набор модулей Runbook из сообщества Майкрософт и hello, который можно импортировать в службы автоматизации Azure. Runbook можно загрузить из галереи hello, размещаемой в hello [центра сценариев TechNet](https://gallery.technet.microsoft.com/scriptcenter/site/upload), или можно непосредственно импортировать Runbook из галереи hello из hello классический портал Azure или портал Azure.

Можно только импортировать напрямую из коллекции модулей Runbook hello с помощью hello классический портал Azure или портал Azure. Windows PowerShell не поддерживает эту функцию.

> [!NOTE]
> Следует проверить hello содержимое любого модуля Runbook можно получить из коллекции модулей Runbook hello и соблюдать осторожность при установке и работе с ними в рабочей среде. |
> 
> 

### <a name="tooimport-a-runbook-from-hello-runbook-gallery-with-hello-azure-classic-portal"></a>tooimport runbook из hello коллекции модулей Runbook с hello классический портал Azure
1. В hello портала Azure щелкните последовательно **New**, **службы приложений**, **автоматизации**, **Runbook**, **из коллекции**.
2. Выберите tooview категории связанные модули Runbook и выберите runbook tooview сведения о нем. При выборе модуля hello, нажмите кнопку со стрелкой вправо hello.
   
    ![Коллекция Runbook](media/automation-runbook-gallery/runbook-gallery.png)
3. Просмотрите содержимое hello hello runbook и ознакомьтесь со всеми требованиями в описании hello. Нажмите кнопку со стрелкой вправо hello, после завершения.
4. Введите сведения о runbook hello, а затем нажмите кнопку флажок hello. Имя runbook Hello уже быть заполнено.
5. Hello модуль runbook появится на hello **Runbooks** вкладке hello учетной записи автоматизации.

### <a name="tooimport-a-runbook-from-hello-runbook-gallery-with-hello-azure-portal"></a>tooimport runbook из hello коллекции модулей Runbook с hello портал Azure
1. Откройте в hello портал Azure, ваша учетная запись автоматизации.
2. Щелкните hello **Runbooks** плитки tooopen hello список модулей Runbook.
3. Нажмите кнопку **Обзор коллекции** .
   
    ![Кнопка «Обзор коллекции»](media/automation-runbook-gallery/browse-gallery-button.png)
4. Найдите элемент коллекции hello и выберите его tooview сведения о нем.
   
    ![Обзор коллекции](media/automation-runbook-gallery/browse-gallery.png)
5. Щелкните **представление исходный проект** tooview элемента hello в hello [центра сценариев TechNet](http://gallery.technet.microsoft.com/).
6. tooimport элемент, щелкните его tooview его данные и нажмите кнопку hello **импорта** кнопки.
   
    ![Кнопка «Импорт»](media/automation-runbook-gallery/gallery-item-detail.png)
7. При необходимости измените имя hello hello runbook и нажмите кнопку **ОК** tooimport hello runbook.
8. Hello модуль runbook появится на hello **Runbooks** вкладке hello учетной записи автоматизации.

### <a name="adding-a-runbook-toohello-runbook-gallery"></a>Добавление коллекции модулей runbook toohello runbook
Корпорация Майкрософт рекомендует toohello runbooks tooadd коллекции модулей Runbook, которые могут оказаться полезны tooother клиентов.  Можно добавить модуль runbook, [передачи toohello центра сценариев](http://gallery.technet.microsoft.com/site/upload) учитывая hello учетной записи, приведенные ниже сведения.

* Необходимо указать *Windows Azure* для hello **категории** и *автоматизации* для hello **подкатегории** для отображения toobe runbook hello в мастере hello.  
* один файл .ps1 или .graphrunbook необходимо отправить Hello.  Если hello runbook требует все модули, дочерние модули Runbook или активы, затем необходимо указать их в описании hello hello отправки и в разделе комментариев hello hello runbook.  Если сценарий, требующий несколько модулей Runbook, отправить каждого отдельно и список имен hello hello, связанные с Runbook в описании каждого модуля. Убедитесь, что используемая hello же теги, чтобы они будут отображаться в hello одной категории. Пользователь будет иметь tooknow описание hello tooread, что другие модули Runbook являются toowork сценария требуется hello.
* Добавить тег hello «GraphicalPS» при публикации **графический runbook** (не графический рабочий процесс). 
* Вставить фрагмент кода рабочего процесса PowerShell или PowerShell в hello, используя описание **вставить код в разделе** значок.
* Hello для передачи hello будет показана сводка в коллекции модулей Runbook результаты, поэтому следует предоставить подробные сведения, которые помогут пользователям определять функциональные возможности hello hello runbook приветствия.
* Необходимо назначить один toothree hello после передачи toohello тегов.  Hello runbook будет отображаться в мастере hello в категориях hello, соответствующих этим тегам.  Все теги, отсутствующие в этом списке будут игнорироваться мастером hello. Если теги соответствия не указан, будет hello runbook в списке hello другие категории.
  
  * Резервное копирование
  * Управление емкостью;
  * управление изменениями;
  * Соответствие нормативным требованиям
  * среды разработки и тестирования;
  * Аварийное восстановление
  * Мониторинг
  * установка исправлений;
  * Подготовка
  * Исправление
  * управление жизненным циклом виртуальной машины.
* Автоматизации обновляет коллекции hello один раз в час, вы не увидите свои комментарии немедленно.

## <a name="modules-in-powershell-gallery"></a>Модули в коллекции PowerShell
Модули PowerShell содержат командлеты, которые можно использовать в модулях Runbook, и существующие модули, которые можно установить в службе автоматизации Azure доступны в hello [коллекции PowerShell](http://www.powershellgallery.com).  Можно запустить этой галереи из hello портал Azure и устанавливать их непосредственно в службу автоматизации Azure, или можно загрузить их и установить их вручную.  Не удается установить модули hello непосредственно из hello классический портал Azure, но их можно загрузить их установить, как и любой другой модуль.

### <a name="tooimport-a-module-from-hello-automation-module-gallery-with-hello-azure-portal"></a>tooimport модуля из hello в коллекции модулей автоматизации с hello портал Azure
1. Откройте в hello портал Azure, ваша учетная запись автоматизации.
2. Щелкните hello **активы** плитки tooopen hello списка ресурсов.
3. Щелкните hello **модули** плитки tooopen hello список модулей.
4. Щелкните hello **обзора коллекции** запускается кнопки и hello колонке обзора коллекции.
   
    ![Коллекция модулей](media/automation-runbook-gallery/modules-blade.png) <br>
5. После запуска hello обзора коллекции колонки, можно выполнить поиск, hello следующие поля:
   
   * Имя модуля
   * Теги
   * Автор
   * Командлет или имя ресурса DSC
6. Найдите модуль интересует и выберите его tooview сведения о нем.  
   При изменении уровня детализации конкретного модуля, можно просмотреть дополнительные сведения о модуле hello, включая toohello обратной связи коллекции PowerShell, требуемые зависимости, и содержит все командлеты hello и ресурсы DSC, hello модуля.
   
    ![Сведения о модуле PowerShell](media/automation-runbook-gallery/gallery-item-details-blade.png) <br>
7. модуль hello tooinstall непосредственно в службу автоматизации Azure, щелкните hello **импорта** кнопки.
   
    ![Кнопка импорта модуля](media/automation-runbook-gallery/module-import-button.png)
8. При нажатии кнопки Импорт hello, вы увидите hello имя модуля, который вы собираетесь tooimport. Если установлены все зависимости hello, hello **ОК** кнопка будет активна. Если отсутствуют зависимости, необходимо tooimport те перед импортом этого модуля.
9. Нажмите кнопку **ОК** модуль tooimport hello и колонки hello модуль будет запущен. Учетную запись tooyour модуля, импортирующий автоматизации Azure, он извлекает метаданные модуля hello и командлеты hello.
   
    ![Колонка импорта модуля](media/automation-runbook-gallery/module-import-blade.png)
   
    Это может занять несколько минут, после каждого действия должен toobe извлечены.
10. Вы получите уведомление развертываемого модуля hello и уведомление после ее завершения.
11. После импорта модуля hello, вы увидите hello доступных действий, и его ресурсы в Runbook и настройки требуемого состояния можно использовать.

## <a name="requesting-a-runbook-or-module"></a>Запрос на создание модуля Runbook или другого модуля
Можно отправлять запросы слишком[User Voice](https://feedback.azure.com/forums/246290-azure-automation/).  Если необходима помощь при написании модуля или у вас появился вопрос о PowerShell, учет tooour вопрос [форум](http://social.msdn.microsoft.com/Forums/windowsazure/en-US/home?forum=azureautomation&filter=alltypes&sort=lastpostdesc).

## <a name="next-steps"></a>Дальнейшие действия
* tooget к работе с модулями Runbook, в разделе [Создание или импорт модуля runbook в автоматизации Azure](automation-creating-importing-runbook.md)
* toounderstand hello различия PowerShell и рабочий процесс PowerShell с Runbook, в разделе [рабочего процесса PowerShell обучения](automation-powershell-workflow.md)

