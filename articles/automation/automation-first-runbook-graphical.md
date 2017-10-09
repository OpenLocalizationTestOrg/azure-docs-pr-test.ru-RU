---
title: "aaaMy первый графический runbook в автоматизации Azure | Документы Microsoft"
description: "Учебник, в котором описывается создание hello, тестированию и публикации простых графического модуля Runbook."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
keywords: "Runbook, шаблон Runbook, служба автоматизации Runbook и Azure Runbook"
ms.assetid: dcb88f19-ed2b-4372-9724-6625cd287c8a
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/17/2017
ms.author: magoedte;bwren
ms.openlocfilehash: 964cf8bae75ca597959bfc39b2b07c22bbc9acb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="my-first-graphical-runbook"></a>Первый графический Runbook

> [!div class="op_single_selector"]
> * [Графический](automation-first-runbook-graphical.md)
> * [PowerShell](automation-first-runbook-textual-powershell.md)
> * [Рабочий процесс PowerShell](automation-first-runbook-textual.md)
> 
> 

Этот учебник поможет выполнить создание hello [графический runbook](automation-runbook-types.md#graphical-runbooks) в службе автоматизации Azure.  Мы начнем с простого модуля runbook, который проверяет и опубликует мы объясним, как tootrack hello состояния задания runbook hello.  Затем мы измените hello runbook tooactually управления ресурсами Azure, в этом случае запуск виртуальной машины Azure.  Затем мы учебником hello, делая hello runbook более надежными, добавив параметры модуля runbook и условные связи.

## <a name="prerequisites"></a>Предварительные требования
toocomplete этого учебника потребуются следующие hello.

* Подписка Azure.  Если у вас ее нет, [активируйте преимущества для подписчиков MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) или <a href="/pricing/free-account/" target="_blank">[зарегистрируйте бесплатную учетную запись](https://azure.microsoft.com/free/).
* [Учетная запись службы автоматизации Azure](automation-sec-configure-azure-runas-account.md) toohold hello runbook и проверить подлинность tooAzure ресурсов.  Этой учетной записи необходимо разрешение toostart и остановить виртуальную машину hello.
* Виртуальная машина Azure.  Это не должна быть рабочая машина, поскольку в процессе изучения данного материала ее нужно будет остановить и запустить заново.

## <a name="step-1---create-runbook"></a>Шаг 1. Создание нового модуля Runbook
Мы начнем с создания простого модуля runbook, который выводит текст hello *Hello World*.

1. Откройте в hello портал Azure, ваша учетная запись автоматизации.  
   страница учетной записи автоматизации Hello предоставляет быстрый просмотр hello ресурсов в этой учетной записи.  Некоторые ресурсы уже должны быть доступны.  Большинство из них являются hello модули, которые автоматически включаются в новую учетную запись автоматизации.  Вы также должны hello ресурс учетных данных, которая упоминается в hello [необходимых компонентов](#prerequisites).
2. Нажмите кнопку hello **Runbooks** плитки tooopen hello список модулей Runbook.<br> ![Элемент управления "Модули Runbook"](media/automation-first-runbook-graphical/runbooks-resources-tile.png)
3. Создать новый runbook, щелкнув hello **добавить модуль runbook** кнопки и затем **создать новый runbook**.
4. Присвойте имя hello hello runbook *MyFirstRunbook графический*.
5. В этом случае мы будем toocreate [графический runbook](automation-graphical-authoring-intro.md) поэтому выберите **Graphical** для **тип Runbook**.<br> ![Новый Runbook](media/automation-first-runbook-graphical/create-new-runbook.png)<br>
6. Нажмите кнопку **создать** toocreate hello runbook и откройте hello графического редактора.

## <a name="step-2---add-activities-toohello-runbook"></a>Шаг 2 — Добавление действий toohello runbook
Библиотека управления hello левой части редактора hello Hello позволяет tooadd tooyour tooselect действия runbook.  Мы будем tooadd **Write-Output** текст toooutput командлета из модуля runbook hello.

1. В hello элемент управления из библиотеки, щелкните в текстовом поле поиска hello и тип **Write-Output**.  Hello результаты поиска будут показаны ниже. <br> ![Microsoft.PowerShell.Utility](media/automation-first-runbook-graphical/search-powershell-cmdlet-writeoutput.png)
2. Прокрутите вниз toohello нижней части списка hello.  Вы можете либо щелкните правой кнопкой мыши **Write-Output** и выберите **добавить toocanvas** или щелкните следующий командлет toohello hello эллипса, а затем выберите **добавить toocanvas**.
3. Нажмите кнопку hello **Write-Output** действия на холсте hello.  Это открывает колонку управления hello конфигурации, позволяющий tooconfigure hello действия.
4. Hello **метка** по умолчанию используется имя toohello hello командлета, но мы можем изменить toosomething более понятным. Измените его слишком*toooutput записи Hello World*.
5. Нажмите кнопку **параметры** tooprovide значения для параметров командлета hello.  
   Некоторые командлеты имеют несколько наборов параметров, и требуется tooselect какие вы один toouse. В этом случае **Write-Output** имеет только один набор параметров, вам требуется tooselect один. <br> ![Свойства командлета Write-Output](media/automation-first-runbook-graphical/write-output-properties-b.png)
6. Выберите hello **InputObject** параметра.  Это параметр hello, в котором указывается hello текст toosend toohello выходной поток.
7. В hello **источника данных** раскрывающийся список, выберите **PowerShell выражение**.  Hello **источника данных** раскрывающийся список обеспечивает различные источники используется toopopulate значение параметра.  
   Можно использовать выходные данные из таких источников, как другое действие, ресурс автоматизации или выражение PowerShell.  В этом случае нужен только текст hello toooutput *Hello World*. Для этого мы воспользуемся выражением PowerShell и укажем строку.
8. В hello **выражение** введите *«Hello World»* и нажмите кнопку **ОК** дважды tooreturn toohello холста.<br> ![PowerShell Expression](media/automation-first-runbook-graphical/expression-hello-world.png)
9. Сохранить hello runbook, установив **Сохранить**.<br> ![Сохранить Runbook](media/automation-first-runbook-graphical/runbook-toolbar-save-revised20165.png)

## <a name="step-3---test-hello-runbook"></a>Шаг 3. при проверке runbook hello
Прежде чем мы опубликовать hello runbook toomake он доступен в рабочей среде, нам нужно tootest его toomake убедиться, что он работает правильно.  Чтобы протестировать модуль Runbook, нужно запустить его **черновую** версию и проверить его работу в интерактивном режиме.

1. Нажмите кнопку **области тестов** tooopen hello теста колонку.<br> ![Область тестирования](media/automation-first-runbook-graphical/runbook-toolbar-test-revised20165.png)
2. Нажмите кнопку **запустить** toostart hello теста.  Это должно быть включено только hello вариантом.
3. Объект [задание runbook](automation-runbook-execution.md) создается и его состояние, отображаемое в области hello.  
   состояние задания Hello для запуска в качестве *в очереди* означает, что он ожидает runbook worker в доступных toobecome облака hello.  Перемещается на слишком*запуск* когда исполнитель задания hello, а затем *под управлением* при hello runbook фактически начинает выполнение.  
4. По завершении заданий runbook hello его вывода. В нашем случае это должен быть текст *Привет, мир!*.<br> ![Привет, мир!](media/automation-first-runbook-graphical/runbook-test-results.png)
5. Закройте hello теста колонке tooreturn toohello холста.

## <a name="step-4---publish-and-start-hello-runbook"></a>Шаг 4. Публикация и запуск модуля runbook hello
runbook Hello, созданную по-прежнему черновом режиме. Мы должны toopublish перед его можно было запустить в рабочей среде.  При публикации модуля runbook, можно заменить hello существующей опубликованной версии hello черновую версию.  В нашем случае мы опубликованную версию еще нет, потому что мы только что создали hello runbook.

1. Нажмите кнопку **публикации** toopublish hello runbook и затем **Да** при появлении запроса.<br> ![Опубликовать](media/automation-first-runbook-graphical/runbook-toolbar-publish-revised20166.png)
2. При прокрутке левой tooview runbook hello в hello **Runbooks** колонки, он показывает **состояние создания** из **опубликовано**.
3. Колонка hello правой tooview задней toohello прокрутки для **MyFirstRunbook**.  
   Hello параметры сверху hello позволит нам toostart hello runbook, запланировать toostart в некоторый момент в будущем hello или создать [веб-перехватчика](automation-webhooks.md) , оно может начаться через вызов HTTP.
4. Нужен только toostart hello runbook нажмите **запустить** и затем **Да** при появлении запроса.<br> ![Запуск модуля Runbook](media/automation-first-runbook-graphical/runbook-controls-start-revised20165.png)
5. Стоечный модуль задания открывается для hello задание runbook, который мы создали.  Можно закрыть эту колонку, но в этом случае мы оставить его открытым, поэтому мы можно отслеживать ход выполнения задания hello.
6. отображается состояние заданий Hello в **Сводка заданий** и совпадений hello состояния, мы видели, когда мы протестировали hello runbook.<br> ![Сводные данные задания](media/automation-first-runbook-graphical/runbook-job-summary.png)
7. Один раз hello показано состояние runbook *завершено*, нажмите кнопку **вывода**. Hello **вывода** открывается колонка, и мы видим нашей *Hello World* панели hello.<br> ![Сводные данные задания](media/automation-first-runbook-graphical/runbook-job-output.png)  
8. Закрыть hello колонке выходных данных.
9. Нажмите кнопку **все журналы** tooopen hello потоки колонке hello задания runbook.  Мы должны видеть только *Hello World* в выходных данных hello потока, но это может показывать другие потоки для задания runbook, например Verbose и ошибка записывает toothem hello runbook.<br> ![Сводные данные задания](media/automation-first-runbook-graphical/runbook-job-AllLogs.png)
10. Закройте все журналы колонке hello и hello задания колонке tooreturn toohello MyFirstRunbook колонку.
11. Нажмите кнопку **заданий** колонке заданий hello tooopen для этого модуля runbook.  Перечисляет все задания hello, созданные этим модулем runbook. Мы должны видеть только одно задание, так как мы только запуска задания hello один раз в списке.<br> ![Задания](media/automation-first-runbook-graphical/runbook-control-jobs.png)
12. Можно щелкнуть это задание tooopen hello одной области задания, которые мы просматривать, когда мы начали hello runbook.  Это позволяет toogo обратно в времени и просмотреть подробные сведения hello любого задания, который был создан для конкретного модуля runbook.

## <a name="step-5---create-variable-assets"></a>Шаг 5. Создание ресурсов для переменных
Мы протестировали и опубликовали свой модуль Runbook, но пока он не выполняет никаких полезных действий. Мы хотим toohave его управления ресурсами Azure.  Прежде чем мы настраиваем hello runbook tooauthenticate, мы создать идентификатор подписки переменной toohold hello и ссылок на него после мы настраиваем tooauthenticate действие hello в шаге 6 ниже.  Включая контекст подписки toohello ссылка позволяет tooeasily работы между несколькими подписками.  Прежде чем продолжить, скопируйте код подписки из hello подписок параметр выключить панель навигации hello.  

1. В колонке hello учетные записи автоматизации щелкните hello **активы** плитки и hello **активы** открыть колонку.
2. В колонке активы hello щелкните hello **переменных** плитки.
3. В колонке переменные hello, нажмите кнопку **добавить переменную**.<br>![Переменная службы автоматизации](media/automation-first-runbook-graphical/create-new-subscriptionid-variable.png)
4. В hello новой переменной колонке в hello **имя** введите **AzureSubscriptionId** и в hello **значение** введите идентификатор подписки.  Сохранить *строка* для hello **тип** и значение по умолчанию hello **шифрования**.  
5. Нажмите кнопку **создать** toocreate hello переменной.  

## <a name="step-6---add-authentication-toomanage-azure-resources"></a>Шаг 6 — Добавление toomanage проверки подлинности ресурсов Azure
Теперь, когда у нас есть переменной toohold наш код подписки, можно настроить нашей tooauthenticate runbook hello запуска от имени учетных данных, который ссылается tooin hello [необходимых компонентов](#prerequisites).  Нам сделать путем добавления hello запуска от имени Azure подключения **активов** и **AzureRMAccount добавить** холст toohello командлета.  

1. Графический редактор Привет открыть, щелкнув **изменить** колонке MyFirstRunbook hello.<br> ![Изменить Runbook](media/automation-first-runbook-graphical/runbook-controls-edit-revised20165.png)
2. Нам не нужен hello **toooutput записи Hello World** , поэтому ее правой кнопкой мыши и выберите **удалить**.
3. В hello элемент управления из библиотеки, разверните **подключений** и добавьте **AzureRunAsConnection** toohello холст, выбрав **добавить toocanvas**.
4. На холсте hello, выберите **AzureRunAsConnection** и в области управления конфигурации hello введите **получить запуска качестве соединения** в hello **метка** текстового поля.  Это подключение hello
5. В hello библиотеки элементов управления, введите **AzureRmAccount добавить** в текстовом поле поиска hello.
6. Добавить **AzureRmAccount добавить** toohello холста.<br> ![ресурс](media/automation-first-runbook-graphical/search-powershell-cmdlet-addazurermaccount.png)
7. Наведите указатель мыши на **получить запуска качестве соединения** до появления окружности нижней hello hello фигуры. Щелкните круг hello и перетащите стрелку hello слишком**AzureRmAccount добавить**.  Стрелка Hello, созданный *ссылку*.  Hello runbook запускается с **получить запуска качестве соединения** , а затем запустите **AzureRmAccount добавить**.<br> ![Создание связи между действиями](media/automation-first-runbook-graphical/runbook-link-auth-activities.png)
8. На холсте hello выберите **AzureRmAccount добавить** и в конфигурации hello области типа элемента управления **tooAzure входа** в hello **метка** текстового поля.
9. Нажмите кнопку **параметры** и появится в колонке hello действие параметра конфигурации.
10. **Добавить AzureRmAccount** имеет несколько наборов параметров, поэтому необходимо tooselect один, прежде чем мы можем предоставить значения параметров.  Нажмите кнопку **параметру** , а затем выберите hello **ServicePrincipalCertificatewithSubscriptionId** набор параметров.
11. После выбора hello набор параметров, отображаются параметры hello в колонке hello конфигурации параметра действия.  Щелкните **APPLICATIONID**.<br> ![Добавление параметров учетной записи Azure RM](media/automation-first-runbook-graphical/add-azurermaccount-params.png)
12. В колонке hello значение параметра, выберите **выходные данные действия** для hello **источника данных** и выберите **получить запуска качестве соединения** списке hello в hello **поля путь** текстовое поле типа **ApplicationId**, а затем нажмите кнопку **ОК**.  Мы указывается имя hello hello свойства для hello поле пути, потому, что действие hello объекта с несколькими свойствами.
13. Нажмите кнопку **CERTIFICATETHUMBPRINT**и выберите в колонке hello значение параметра **выходные данные действия** для hello **источника данных**.  Выберите **получить запуска качестве соединения** списке hello в hello **путь к полю** текстовое поле типа **CertificateThumbprint**и нажмите кнопку **ОК**.
14. Нажмите кнопку **SERVICEPRINCIPAL**и выберите в колонке hello значение параметра **ConstantValue** для hello **источника данных**, переключатель hello **True**, а затем нажмите кнопку **ОК**.
15. Нажмите кнопку **TENANTID**и выберите в колонке hello значение параметра **выходные данные действия** для hello **источника данных**.  Выберите **получить запуска качестве соединения** списке hello в hello **путь к полю** текстовое поле типа **TenantId**и нажмите кнопку **ОК** дважды.  
16. В hello библиотеки элементов управления, введите **AzureRmContext набора** в текстовом поле поиска hello.
17. Добавить **AzureRmContext набор** toohello холста.
18. На холсте hello выберите **AzureRmContext набор** и в конфигурации hello области типа элемента управления **укажите идентификатор подписки** в hello **метка** текстового поля.
19. Нажмите кнопку **параметры** и появится в колонке hello действие параметра конфигурации.
20. **Набор AzureRmContext** имеет несколько наборов параметров, поэтому необходимо tooselect один, прежде чем мы можем предоставить значения параметров.  Нажмите кнопку **параметру** , а затем выберите hello **SubscriptionId** набор параметров.  
21. После выбора hello набор параметров, отображаются параметры hello в колонке hello конфигурации параметра действия.  Щелкните **SubscriptionID**
22. В колонке hello значение параметра, выберите **переменной активов** для hello **источника данных** и выберите **AzureSubscriptionId** hello списка и нажмите кнопку **ОК**  дважды.   
23. Наведите указатель мыши на **tooAzure входа** до появления окружности нижней hello hello фигуры. Щелкните круг hello и перетащите стрелку hello слишком**укажите идентификатор подписки**.

Модуль runbook должен выглядеть hello на этом этапе следующие: <br>![Настройка проверки подлинности Runbook](media/automation-first-runbook-graphical/runbook-auth-config.png)

## <a name="step-7---add-activity-toostart-a-virtual-machine"></a>Шаг 7 — Добавление toostart действия виртуальной машины
Здесь мы добавляем **AzureRmVM начала** toostart действия виртуальной машины.  Можно выбрать любой виртуальной машине в вашей подписке Azure и теперь можно указывать, имя в командлет hello.

1. В hello библиотеки элементов управления, введите **AzureRm начала** в текстовом поле поиска hello.
2. Добавить **начала AzureRmVM** toohello холст и затем щелкните и перетащите его под **укажите идентификатор подписки**.
3. Наведите указатель мыши на **укажите идентификатор подписки** до появления окружности нижней hello hello фигуры.  Щелкните круг hello и перетащите стрелку hello слишком**AzureRmVM начала**.
4. Выберите **Start-AzureRmVM**.  Нажмите кнопку **параметры** и затем **параметру** tooview hello задает для **AzureRmVM начала**.  Выберите hello **ResourceGroupNameParameterSetName** набор параметров. Обратите внимание, что рядом с параметрами **ResourceGroupName** и **Имя** стоят восклицательные знаки.  Это означает, что данные параметры являются обязательными.  Также оба параметра ожидают ввода строковых значений.
5. Выберите параметр **Имя**.  Выберите **PowerShell выражение** для hello **источника данных** и введите имя hello hello виртуальной машины, заключен в двойные кавычки, которые мы начнем с этим модулем runbook.  Нажмите кнопку **ОК**.<br>![Значение параметра имени для Start-AzureRmVM](media/automation-first-runbook-graphical/runbook-startvm-nameparameter.png)
6. Выберите **ResourceGroupName**. Используйте **PowerShell выражение** для hello **источника данных** и введите имя hello группы ресурсов hello, заключен в двойные кавычки.  Нажмите кнопку **ОК**.<br> ![Параметры Start-AzureRmVM](media/automation-first-runbook-graphical/startazurermvm-params.png)
7. Щелкните области тестов, чтобы мы смогли проверить hello runbook.
8. Нажмите кнопку **запустить** toostart hello теста.  После ее завершения, убедитесь, что виртуальная машина, hello была запущена.

Модуль runbook должен выглядеть hello на этом этапе следующие: <br>![Настройка проверки подлинности Runbook](media/automation-first-runbook-graphical/runbook-startvm.png)

## <a name="step-8---add-additional-input-parameters-toohello-runbook"></a>Шаг 8 — Добавление дополнительных входных параметров toohello runbook
Наш runbook в данный момент запускает hello виртуальную машину в группу ресурсов hello, мы указали в hello **AzureRmVM начала** командлета.  Наш runbook будет более полезным в том случае, если оба можно указать при запуске hello runbook.  Теперь добавим tooprovide runbook toohello входных параметров эта функция.

1. Графический редактор Привет открыть, щелкнув **изменить** на hello **MyFirstRunbook** области.
2. Нажмите кнопку **ввод и вывод** и затем **добавить входные данные** tooopen hello Runbook входной параметр области.<br> ![Входные и выходные данные Runbook](media/automation-first-runbook-graphical/runbook-toolbar-InputandOutput-revised20165.png)
3. Укажите *VMName* для hello **имя**.  Сохранить *строка* для hello **тип**, но изменить **обязательные** слишком*Да*.  Нажмите кнопку **ОК**.
4. Создайте второй обязательный входной параметр с именем *ResourceGroupName* и нажмите кнопку **ОК** tooclose hello **входной и выходной** области.<br> ![Входные параметры Runbook](media/automation-first-runbook-graphical/start-azurermvm-params-outputs.png)
5. Выберите hello **начала AzureRmVM** действия и нажмите кнопку **параметры**.
6. Изменение hello **источника данных** для **имя** слишком**ввода Runbook** , а затем выберите **VMName**.<br>
7. Изменение hello **источника данных** для **ResourceGroupName** слишком**ввода Runbook** , а затем выберите **ResourceGroupName**.<br> ![Параметры командлета Start-AzureVM](media/automation-first-runbook-graphical/start-azurermvm-params-runbookinput.png)
8. Сохраните hello runbook и откройте панель тестовых hello.  Обратите внимание, что вы можете теперь задать значения для hello две входные переменные, используемые в тесте hello.
9. Закрыть hello тестовой области.
10. Нажмите кнопку **публикации** toopublish hello hello runbook в новой версии.
11. Остановите hello виртуальную машину, которая запущена на предыдущем шаге hello.
12. Нажмите кнопку **запустить** toostart hello runbook.  Тип в hello **VMName** и **ResourceGroupName** для виртуальной машины hello ты toostart.<br> ![Start Runbook](media/automation-first-runbook-graphical/runbook-start-inputparams.png)
13. После завершения hello runbook, убедитесь, что виртуальная машина, hello была запущена.

## <a name="step-9---create-a-conditional-link"></a>Шаг 9. Создание условной связи
Теперь мы изменить hello runbook таким образом, чтобы только пытается toostart hello виртуальной машины, если он еще не запущен.  Это можно сделать, добавив **Get AzureRmVM** runbook toohello командлет, который возвращает состояние экземпляра уровня hello hello виртуальной машины. После этого добавить модуль кода рабочий процесс PowerShell с именем **Получение состояния** во фрагмент PowerShell код toodetermine, если состояние виртуальной машины hello запущенной или остановленной.  Условных связей из hello **Получение состояния** модуль выполняется только **AzureRmVM начала** при остановке hello текущее состояние.  Наконец мы вывода tooinform сообщение, если hello ВМ был успешно запущен или не использовать hello командлет PowerShell Write-Output.

1. Откройте **MyFirstRunbook** в графическом редакторе hello.
2. Удалить hello связь между **укажите идентификатор подписки** и **начала AzureRmVM** , щелкнув его и нажав hello *удалить* ключа.
3. В hello библиотеки элементов управления, введите **Get AzureRm** в текстовом поле поиска hello.
4. Добавить **Get AzureRmVM** toohello холста.
5. Выберите **Get AzureRmVM** и затем **параметру** tooview hello задает для **Get AzureRmVM**.  Выберите hello **GetVirtualMachineInResourceGroupNameParamSet** набор параметров.  Обратите внимание, что рядом с параметрами **ResourceGroupName** и **Имя** стоят восклицательные знаки.  Это означает, что данные параметры являются обязательными.  Также оба параметра ожидают ввода строковых значений.
6. В поле **Источник данных** для параметра **Имя** укажите значение **Runbook input** (Входные данные Runbook), а затем выберите **VMName**.  Нажмите кнопку **ОК**.
7. В поле **Источник данных** для параметра **ResourceGroupName** укажите значение **Runbook input** (Входные данные Runbook), а затем выберите **ResourceGroupName**.  Нажмите кнопку **ОК**.
8. В поле **Источник данных** для параметра **Состояние** выберите **Значение-константа**, а затем щелкните **True**.  Нажмите кнопку **ОК**.  
9. Создайте связь от **укажите идентификатор подписки** слишком**Get AzureRmVM**.
10. В элемент управления из библиотеки hello, разверните **управления Runbook** и добавьте **кода** toohello холста.  
11. Создайте связь от **Get AzureRmVM** слишком**кода**.  
12. Нажмите кнопку **кода** и hello конфигурации панели, измените метку слишком**Получение состояния**.
13. Выберите **кода** параметр и hello **редактор кода** колонке отображается.  
14. В редакторе кода hello вставьте следующий фрагмент кода hello:
    
     ```
     $StatusesJson = $ActivityOutput['Get-AzureRmVM'].StatusesText
     $Statuses = ConvertFrom-Json $StatusesJson
     $StatusOut =""
     foreach ($Status in $Statuses){
     if($Status.Code -eq "Powerstate/running"){$StatusOut = "running"}
     elseif ($Status.Code -eq "Powerstate/deallocated") {$StatusOut = "stopped"}
     }
     $StatusOut
     ```
15. Создайте связь от **Получение состояния** слишком**AzureRmVM начала**.<br> ![Runbook с модулем кода](media/automation-first-runbook-graphical/runbook-startvm-get-status.png)  
16. Выберите ссылку, hello и панели конфигурации hello, измените **применять условие** слишком**Да**.   Связь с заметкой hello включает tooa пунктирных строки, указывающее, что hello целевого действия запускается, только если условие hello разрешает tootrue.  
17. Для hello **условия выражения**, тип *$ActivityOutput [«получение состояния»] - eq «Остановлена»*.  **Начало AzureRmVM** выполняется теперь только если hello виртуальная машина остановлена.
18. В hello элемент управления из библиотеки, разверните **командлеты** и затем **Microsoft.PowerShell.Utility**.
19. Добавить **Write-Output** toohello холст дважды.<br> ![Runbook с командлетом Write-Output](media/automation-first-runbook-graphical/runbook-startazurermvm-complete.png)
20. На hello первый **Write-Output** управлять, щелкните **параметры** и измените hello **метка** значение слишком*уведомить работы виртуальной Машины*.
21. Для **InputObject**, изменить **источника данных** слишком**PowerShell выражение** и введите выражение hello *«$VMName успешно запущен».* .
22. На hello второй **Write-Output** управлять, щелкните **параметры** и измените hello **метка** значение слишком*уведомить запустить сбой виртуальной Машины*
23. Для **InputObject**, изменить **источника данных** слишком**PowerShell выражение** и введите выражение hello *«$VMName не удалось запустить.»* .
24. Создайте связь от **начала AzureRmVM** слишком**уведомить работы виртуальной Машины** и **уведомить ВМ запустить не удалось**.
25. Выберите связь hello слишком**уведомить работы виртуальной Машины** и измените **применять условие** слишком**True**.
26. Для hello **условия выражения**, тип *$ActivityOutput [«Start-AzureRmVM»]. IsSuccessStatusCode - eq $true*.  Write-Output управление выполняется теперь только, если успешно запущен hello виртуальной машины.
27. Выберите связь hello слишком**уведомить ВМ запустить не удалось** и измените **применять условие** слишком**True**.
28. Для hello **условия выражения**, тип *$ActivityOutput [«Start-AzureRmVM»]. IsSuccessStatusCode - ne $true*.  Write-Output теперь управление выполняется только если hello виртуальной машины не запущена успешно.
29. Сохраните hello runbook и откройте панель тестовых hello.
30. Запустите hello runbook hello виртуальная машина остановлена, и его запуска.

## <a name="next-steps"></a>Дальнейшие действия
* toolearn Дополнительные сведения о графических разработки. в разделе [графический разработки автоматизации Azure](automation-graphical-authoring-intro.md)
* tooget к работе с PowerShell модули Runbook в разделе [Мой первый runbook PowerShell](automation-first-runbook-textual-powershell.md)
* tooget к работе с PowerShell модули Runbook рабочего процесса, в разделе [Мой первый runbook рабочего процесса PowerShell](automation-first-runbook-textual.md)

