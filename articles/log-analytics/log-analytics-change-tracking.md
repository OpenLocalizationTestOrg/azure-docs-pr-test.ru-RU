---
title: "aaaTrack изменения с помощью аналитики журналов Azure | Документы Microsoft"
description: "Hello решения для отслеживания изменений в службе анализа журналов помогает определить изменения по и служб Windows, происходящие в существующей среде."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: f8040d5d-3c89-4f0c-8520-751c00251cb7
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2bb1938caad25101e167927200ac3ef495120fe0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="track-software-changes-in-your-environment-with-hello-change-tracking-solution"></a>Отслеживать изменения программного обеспечения в среде с hello решения для отслеживания изменений

![символ отслеживания изменений](./media/log-analytics-change-tracking/change-tracking-symbol.png)

Эта статья поможет вам hello используйте решения для отслеживания изменений в службе анализа журналов tooeasily выявления изменений в вашей среде. решение Hello отслеживает изменения tooWindows и программного обеспечения Linux, файлы Windows и разделы реестра, службы Windows и управляющих программ Linux. что, в свою очередь, позволяет точно определять проблемы с работоспособностью.

Необходимо установить hello tooupdate решения hello типа агента, установки. Программное обеспечение tooinstalled изменения служб Windows и управляющих программ Linux на серверах hello отслеживаемых доступны для чтения. Затем hello в выполняется отправка данных службы анализа журналов toohello hello облако для обработки. Логика является примененных toohello полученных данных и hello облачная служба записывает данные hello. С помощью hello сведения на панели мониторинга отслеживания изменений hello, вы увидите легко hello изменения, внесенные в инфраструктуру серверов.

## <a name="installing-and-configuring-hello-solution"></a>Установка и настройка решения hello
Используйте следующие сведения tooinstall hello и настроить решение hello.

* Необходимо иметь [Windows](log-analytics-windows-agents.md), [Operations Manager](log-analytics-om-agents.md), или [Linux](log-analytics-linux-agents.md) агента на каждом компьютере, где необходимо toomonitor изменения.
* Добавить из hello hello отслеживания изменений решения tooyour рабочей области OMS [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.ChangeTrackingOMS?tab=Overview). Или можно добавить решение hello, используя сведения о hello в [решений добавьте анализа журналов из коллекции решений hello](log-analytics-add-solutions.md). Дальнейшая настройка не требуется.

### <a name="configure-linux-files-tootrack"></a>Настройка файлов tootrack Linux
Используйте следующие шаги tooconfigure файлы tootrack на компьютерах Linux hello.

1. На портале OMS hello щелкните **параметры** (символ шестеренки hello).
2. На hello **параметры** щелкните **данные**и нажмите кнопку **отслеживания Linux файл**.
3. В группе отслеживания изменений файла Linux, введите hello весь путь, включая имя файла hello hello файла tootrack и нажмите кнопку hello **добавить** символов. Например: /etc/*.conf.
4. Щелкните **Сохранить**.  

> [!NOTE]
> Отслеживание файлов Linux имеет дополнительные возможности, включая отслеживание каталогов, рекурсию в каталогах и отслеживание подстановочных знаков.

### <a name="configure-windows-files-tootrack"></a>Настройка tootrack файлы Windows
Используйте следующие шаги tooconfigure файлы tootrack на компьютерах с Windows hello.

1. На портале OMS hello щелкните **параметры** (символ шестеренки hello).
2. На hello **параметры** щелкните **данные**и нажмите кнопку **отслеживание Windows файл**.
3. В группе отслеживания изменений файла Windows, введите hello весь путь, включая имя файла hello hello файла tootrack и нажмите кнопку hello **добавить** символов. Например, C:\Program Files (x86)\Internet Explorer\iexplore.exe или C:\Windows\System32\drivers\etc\hosts.
4. Щелкните **Сохранить**.  
   ![Отслеживание изменений в файлах Windows](./media/log-analytics-change-tracking/windows-file-change-tracking.png)

### <a name="configure-windows-registry-keys-tootrack"></a>Настройка tootrack ключи реестра Windows
Используйте следующие tootrack ключи реестра tooconfigure шаги на компьютерах с Windows hello.

1. На портале OMS hello щелкните **параметры** (символ шестеренки hello).
2. На hello **параметры** щелкните **данных**, а затем нажмите кнопку **отслеживание реестра Windows**.
3. В группе отслеживания изменений реестра Windows, введите ключ полностью hello tootrack и нажмите кнопку hello **добавить** символов.
4. Щелкните **Сохранить**.  
   ![Отслеживание изменений в реестре Windows](./media/log-analytics-change-tracking/windows-registry-change-tracking.png)

### <a name="explanation-of-linux-file-collection-properties"></a>Описание свойств коллекции файлов Linux
1. **Тип**
   * **Файл** (метаданные файла отчета — размер, дата изменения, хэш и т. д.).
   * **Каталог** (метаданные файла отчета — размер, дата изменения, хэш и т. д.).
2. **Ссылки** (обработка Linux Символьная ссылка ссылается на tooother файлы или каталоги)
   * **Игнорировать** (Ignore символических ссылок во время recurions toonot включают файлы hello и ссылки на каталоги)
   * **Выполните** (символических ссылок hello выполните во время рекурсии tooalso включают файлы hello и ссылки на каталоги)
   * **Управление** (выполните hello символьных ссылок и alter hello обработки полученного содержимого)

   > [!NOTE]   
   > параметр ссылки «Manage» Hello не рекомендуется. Получение содержимого файлов не поддерживается.

3. **Recurse** (Recurse по уровням папки и отслеживать все файлы, соответствующие инструкции hello path)
4. **Sudo** (включение доступа к файлам или каталогам, требующим привилегии sudo).

### <a name="limitations"></a>Ограничения
Hello решения для отслеживания изменений в настоящее время не поддерживает hello следующих элементов:

* Папки (каталоги) для отслеживания файлов Windows
* Рекурсия для отслеживания файлов Windows
* Подстановочные знаки для отслеживания файлов Windows
* Переменные пути
* Сетевые файловые системы
* Содержимое файла

Другие ограничения:

* Hello **максимальный размер файла** столбец, а значения не используются в текущей реализации hello.
* Если собрать более чем 2500 файлы в цикле hello коллекции 30 минут, может снизиться производительность решения.
* При высокой загрузке сетевого трафика, записи об изменениях может занять tooa максимального значения toodisplay шесть часов.
* Если редактируется конфигурации hello завершать работу компьютера, hello компьютера может учитывать изменения файлов, которые принадлежали toohello предыдущей конфигурации.

## <a name="change-tracking-data-collection-details"></a>Сведения о сборе данных отслеживания изменений.
Отслеживание изменений, сбор данных инвентаризации программного обеспечения и метаданные службы Windows, с помощью hello агенты, которые вы включили.

Hello следующей таблице приведены методы сбора данных и другие сведения о сборе данных для отслеживания изменений.

| платформа | Direct Agent | Агент Operations Manager | Агент Linux | Хранилище Azure | Нужен ли Operations Manager? | Отправка данных агента Operations Manager через группу управления | частота сбора |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Windows и Linux | &#8226; | &#8226; | &#8226; |  |  | &#8226; | 5 минут too50 минут, в зависимости от типа изменений hello. См. в следующей таблице подробнее hello. |


Hello следующей таблице показаны hello частоту сбора данных для hello типы изменений.

| **тип изменения** | **frequency** | **Отправляет** **ли** **агент сведения об обнаруженных изменениях?** |
| --- | --- | --- |
| Реестр Windows | 50 минут | Нет |
| Файловый ресурс Windows | 30 минут | Да. Если изменения не происходят в течение 24 часов, отправляется моментальный снимок. |
| Файловый ресурс Linux | 15 минут | Да. Если изменения не происходят в течение 24 часов, отправляется моментальный снимок. |
| Службы Windows | 30 минут | Да, каждые 30 минут, при обнаружении изменений. Каждые 24 часа отправляется моментальный снимок независимо от изменений. Таким образом, моментальный снимок hello отправляется даже там, где нет изменений. |
| Управляющие программы Linux | 5 мин | Да. Если изменения не происходят в течение 24 часов, отправляется моментальный снимок. |
| Программное обеспечение Windows | 30 минут | Да, каждые 30 минут, при обнаружении изменений. Каждые 24 часа отправляется моментальный снимок независимо от изменений. Таким образом, моментальный снимок hello отправляется даже там, где нет изменений. |
| Программное обеспечение Linux | 5 мин | Да. Если изменения не происходят в течение 24 часов, отправляется моментальный снимок. |

### <a name="registry-key-change-tracking"></a>Отслеживание изменений в разделах реестра

Служба аналитики журналов выполняет реестра Windows, наблюдение и отслеживание с hello решения для отслеживания изменений. Hello мониторинга ключами tooregistry изменения предназначен toopinpoint точки расширения, где можно активировать код сторонних производителей и вредоносных программ. следующие Hello вывода показывает hello по умолчанию разделов отслеживаемые решением hello и почему каждого отслеживается.

- HKEY\_LOCAL\_MACHINE\Software\Microsoft\Windows\CurrentVersion\Group Policy\Scripts\Startup
    - Отслеживаются сценарии, выполняемые при запуске.
- HKEY\_LOCAL\_MACHINE\Software\Microsoft\Windows\CurrentVersion\Group Policy\Scripts\Shutdown
    - Отслеживаются сценарии, выполняемые при завершении работы.
- HKEY\_LOCAL\_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Windows\CurrentVersion\Run
    - Отслеживает ключи, которые загружаются до hello пользователь входит в tootheir учетной записи Windows. Hello ключ используется для 32-разрядных программ, запущенных на 64-разрядных компьютерах.
- HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\Active Setup\Installed Components
    - Ведет наблюдение за изменениями tooapplication параметры.
- HKEY\_LOCAL\_MACHINE\Software\Classes\Directory\ShellEx\ContextMenuHandlers
    - Отслеживаются общие записи автозапуска, привязывающиеся непосредственно к проводнику Windows и выполняющиеся с внутрипроцессным файлом Explorer.exe.
- HKEY\_LOCAL\_MACHINE\Software\Classes\Directory\Shellex\CopyHookHandlers
    - Отслеживаются общие записи автозапуска, привязывающиеся непосредственно к проводнику Windows и выполняющиеся с внутрипроцессным файлом Explorer.exe.
- HKEY\_LOCAL\_MACHINE\Software\Classes\Directory\Background\ShellEx\ContextMenuHandlers
    - Отслеживаются общие записи автозапуска, привязывающиеся непосредственно к проводнику Windows и выполняющиеся с внутрипроцессным файлом Explorer.exe.
- HKEY\_LOCAL\_MACHINE\Software\Microsoft\Windows\CurrentVersion\Explorer\ShellIconOverlayIdentifiers
    - Отслеживается регистрация обработчика дополнительных значков.
- HKEY\_LOCAL\_MACHINE\Software\Wow6432Node\Microsoft\Windows\CurrentVersion\Explorer\ShellIconOverlayIdentifiers
    - Отслеживается регистрация обработчика дополнительных значков для 32-битных программ, работающих на 64-разрядных компьютерах.
- HKEY\_LOCAL\_MACHINE\Software\Microsoft\Windows\CurrentVersion\Explorer\Browser Helper Objects
    - Отслеживаются новые подключаемые модули вспомогательных объектов браузера для Internet Explorer. Используется tooaccess hello объектной модели документа (DOM) hello текущей страницы и toocontrol навигации.
- HKEY\_LOCAL\_MACHINE\Software\Wow6432Node\Microsoft\Windows\CurrentVersion\Explorer\Browser Helper Objects
    - Отслеживаются новые подключаемые модули вспомогательных объектов браузера для Internet Explorer. Используется tooaccess hello объектной модели документа (DOM) hello текущей страницы и toocontrol навигации для 32-разрядных программ, запущенных на 64-разрядных компьютерах.
- HKEY\_LOCAL\_MACHINE\Software\Microsoft\Internet Explorer\Extensions
    - Отслеживаются новые расширения Internet Explorer, например пользовательские меню инструментов и пользовательские кнопки панели инструментов.
- HKEY\_LOCAL\_MACHINE\Software\Wow6432Node\Microsoft\Internet Explorer\Extensions
    - Отслеживаются новые расширения Internet Explorer, например пользовательские меню инструментов и пользовательские кнопки панели инструментов для 32-битных программ, работающих на 64-разрядных компьютерах.
- HKEY\_LOCAL\_MACHINE\Software\Microsoft\Windows NT\CurrentVersion\Drivers32
    - Отслеживание 32-разрядные драйверы hello, связанные с wavemapper, wave1 и wave2, msacm.imaadpcm, .msadpcm, .msgsm610 и vidc. Toohello [drivers] разделом hello системы. INI-файл.
- HKEY\_LOCAL\_MACHINE\Software\Wow6432Node\Microsoft\Windows NT\CurrentVersion\Drivers32
    - 32-разрядные драйверы hello мониторы, связанный с wavemapper, wave1 и wave2, msacm.imaadpcm, .msadpcm, .msgsm610 и vidc для 32-разрядных программ, запущенных на 64-разрядных компьютерах. Toohello [drivers] разделом hello системы. INI-файл.
- HKEY\_LOCAL\_MACHINE\System\CurrentControlSet\Control\Session Manager\KnownDlls
    - Мониторы hello список известных или часто используемых системных DLL; Эта система не позволит использовать разрешения каталога слабое приложения путем перетаскивания в версиях троянская программа системные библиотеки DLL с.
- HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon\Notify
    - Мониторы hello список пакетов будет tooreceive уведомлений о событиях из Winlogon, модель поддержки hello интерактивный вход в систему для операционной системы Windows hello.


## <a name="use-change-tracking"></a>Использование функции отслеживания изменений
После установки решения hello, можно просмотреть сводку hello изменений для отслеживаемых серверов с помощью hello **отслеживания изменений** плитки приветствия **Обзор** в службе OMS.

![image of Change Tracking tile](./media/log-analytics-change-tracking/change-tracking-tile.png)

Можно просмотреть изменения tooyour инфраструктуры, а затем глубже изучить для hello, следующие категории:

* изменения по типу конфигурации для ПО и служб Windows;
* Изменения по tooapplications и обновлений для отдельных серверов
* общее количество изменений ПО для каждого приложения;
* Пакеты Linux
* изменения служб Windows для отдельных серверов.
* Изменения в управляющих программах Linux

![image of Change Tracking dashboard](./media/log-analytics-change-tracking/change-tracking-dash01.png)

![image of Change Tracking dashboard](./media/log-analytics-change-tracking/change-tracking-dash02.png)

### <a name="tooview-changes-for-any-change-type"></a>tooview изменений для любого типа изменений
1. На hello **Обзор** щелкните hello **отслеживания изменений** плитки.
2. На hello **отслеживание изменений** панели мониторинга, просмотрите сводные сведения о hello в одной из колонок типов изменений hello, а затем выберите один tooview подробные сведения о нем в hello **поиска журналов** страницы.
3. На любой из страниц поиска журналов hello можно просмотреть результаты по времени, подробные результаты и историю поиска журналов. Можно также фильтровать по результатам hello toonarrow аспектов.

## <a name="next-steps"></a>Дальнейшие действия
* Используйте [входа поиска аналитики журналов](log-analytics-log-searches.md) tooview подробные данные отслеживания изменений.
