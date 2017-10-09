---
title: "aaaSet виртуальную машину в качестве сервера ноутбук IPython | Документы Microsoft"
description: "Настройка виртуальной машины Azure для использования в среде обработки и анализа данных с сервером IPython для расширенной аналитики."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 818617c1-048e-49c2-b941-f9a983f93998
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: xibingao;bradsev
ms.openlocfilehash: 58386140ec7742ade1f7e183ec842a2b09b9dfca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-an-azure-virtual-machine-as-an-ipython-notebook-server-for-advanced-analytics"></a>Настройка виртуальной машины Azure как сервера IPython Notebook для расширенной аналитики
В этом разделе показано, как tooprovision и настройка виртуальной машины Azure для расширенной аналитики, который может использоваться как часть среды обработки и анализа данных. Виртуальная машина Windows Hello настраивается с вспомогательными средствами, например ноутбук IPython, обозреватель хранилища Azure, AzCopy, а также других средств, которые полезны для расширенной аналитики проектов. Azure Storage Explorer и AzCopy, например, обеспечивают удобный tooupload данных tooAzure хранилища BLOB-данных с локального компьютера или toodownload его tooyour локального компьютера из хранилища больших двоичных объектов.

## <a name="create-vm"></a>Шаг 1. Создание виртуальной машины Azure общего назначения
Если вы уже настроили виртуальной машине Azure и просто нужно tooset ноутбук IPython сервера на нем, можно пропустить этот шаг и продолжить слишком[шаг 2: добавить конечную точку для ноутбуков IPython tooan существующей виртуальной машины](#add-endpoint).

Перед запуском процесса hello создания виртуальной машины в Azure необходимо toodetermine hello размер машины hello необходимые tooprocess hello данные для своего проекта. У небольших машин меньше памяти и ядер ЦП, чем у больших, но они менее дорогие. Список типов компьютеров и ценах см. в разделе hello <a href="http://azure.microsoft.com/pricing/details/virtual-machines/" target="_blank">расценки на виртуальные машины </a> страницы

1. Войдите в слишком<a href="https://manage.windowsazure.com" target="_blank">классический портал Azure</a>и нажмите кнопку **New** в левом нижнем углу hello. Откроется новое окно. Выберите **Среда выполнения приложений** -> **Виртуальная машина** -> **Из коллекции**.
   
    ![Создание рабочей области][24]
2. Выберите один из hello после изображения.
   
   * Центр обработки данных Windows Server 2012 R2;
   * Режим Windows Server Essentials (Windows Server 2012 R2).
     
     Нажмите кнопку hello стрелкой, указывающей вправо на hello нижний правый toogo hello следующей странице конфигурации.
     
     ![Создание рабочей области][25]
3. Введите имя для виртуальной машины hello требуется toocreate выберите hello размера машины hello (по умолчанию: A3) на основе размера hello машины hello hello данных является постоянной tooprocess и о том, как нужно toobe машины hello (памяти размером и hello количество вычислительных ядер) , введите имя пользователя и пароль для машины hello. Нажмите кнопку hello стрелка, указывающая вправо toogo toohello следующей странице конфигурации.
   
    ![Создание рабочей области][26]
4. Выберите hello **регион, ТЕРРИТОРИАЛЬНАЯ ГРУППА или ВИРТУАЛЬНАЯ сеть** , содержащий hello **учетной записи ХРАНИЛИЩА** планировании toouse для этой виртуальной машины и затем выберите этой учетной записи хранения. Добавить конечную точку внизу hello в hello **конечные ТОЧКИ** поля, введя имя hello hello конечной точки («IPython» ниже). Можно выбрать любую строку как hello **имя** hello конечной точки, а любое целое число от 0 до 65536, **доступных** как hello **общий ПОРТ**. Hello **ЧАСТНЫЙ ПОРТ** имеет toobe **9999**. **Не следует** использовать общие порты, уже назначенные для служб Интернета. В таблице <a href="http://www.chebucto.ns.ca/~rakerman/port-table.html" target="_blank">Порты для служб Интернета</a> приведен список портов, которые не следует использовать, так как они уже назначены.
   
    ![Создание рабочей области][27]
5. Щелкните hello флажок toostart hello виртуальную машину, процесс подготовки.
   
    ![Создание рабочей области][28]

Может потребоваться 15 – 25 минут hello toocomplete виртуальную машину, процесс подготовки. После создания виртуальной машины hello hello состояния этой машины должно отображаться как **под управлением**.

![Создание рабочей области][29]

## <a name="add-endpoint"></a>Шаг 2: Добавьте конечную точку для ноутбуков IPython tooan существующей виртуальной машины
Если вы создали hello виртуальной машины в соответствии с инструкциями hello в шаге 1, hello конечную точку для ноутбук IPython уже был добавлен, и этот шаг можно пропустить.

Если hello виртуальная машина уже существует, и требуется tooadd конечную точку для ноутбук IPython, которая будет установлена на шаге 3 Далее, первого входа tooAzure классический портал, выберите виртуальную машину, hello и добавить конечную точку hello ноутбук IPython сервера. Hello на этом рисунке содержит снимок экрана приветствия портала после добавления виртуальной машины tooa Windows hello конечную точку для ноутбук IPython.

![Создание рабочей области][17]

## <a name="run-commands"></a>Шаг 3. Установка IPython Notebook и других вспомогательных средств
После создания виртуальной машины hello используйте toolog протокола удаленного рабочего стола (RDP) на виртуальной машине Windows toohello. Инструкции см. в разделе [как tooLog на виртуальной машине под управлением Windows Server tooa](../virtual-machines/windows/classic/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json). Откройте hello **командной строки** (**не hello командное окно Powershell**) как **администратора** и выполнения hello следующую команду.

    set script='https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/MachineSetup/Azure_VM_Setup_Windows.ps1'

    @powershell -NoProfile -ExecutionPolicy unrestricted -Command "iex ((new-object net.webclient).DownloadString(%script%))"

После завершения установки hello hello server ноутбук IPython автоматически открывается в hello *C:\\пользователей\\\<имя пользователя\>\\документов\\IPython Портативные компьютеры* каталога.

При появлении запроса введите пароль для hello ноутбук IPython и hello пароль администратора машины hello. Это включает hello toorun ноутбук IPython в качестве службы на машине hello.

## <a name="access"></a>Шаг 4. Доступ к IPython Notebook из веб-браузера
tooaccess hello server ноутбук IPython открыть веб-браузер и ввода *https://&#60;virtual компьютера DNS-имя >: &#60; номер общего порта >* в текстовом поле hello URL-адрес. Здравствуйте, *&#60; номер общего порта >* должен быть указан при hello ноутбук IPython конечная точка была добавлена номер порта hello.

Hello *&#60; DNS-имя виртуальной машины >* можно найти в hello классический портал Azure. После входа в toohello классического портала щелкните **виртуальные МАШИНЫ**выберите hello машины создана, а затем выберите **панели МОНИТОРИНГА**, hello DNS-имя будет выглядеть следующим образом:

![Создание рабочей области][19]

Вы столкнетесь с предупреждением о том, что *существует проблема с сертификатом безопасности этого веб-сайта* (Internet Explorer) или *подключение не является закрытым* (Chrome), как показано в следующих hello фигуры. Нажмите кнопку **(не рекомендуется) веб-сайта toothis Продолжить** (Internet Explorer) или **Дополнительно** и затем  **продолжить слишком &#60;* DNS-имя*> (небезопасный) ** toocontinue (Chrome). Затем ввод пароля hello, вы указанной более ранней tooaccess hello ноутбуков IPython.

**Internet Explorer:**
![Создание рабочей области][20]

**Chrome:**
![Создание рабочей области][21]

После входа в систему toohello ноутбук IPython, каталог *DataScienceSamples* будет отображаться в браузере hello. Эта папка содержит образец IPython ноутбуки, общие для задач обработки и анализа данных поведения пользователей Microsoft toohelp. Эти примеры записных книжек IPython будут извлечены из [ **репозитории GitHub** ](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks) toohello виртуальных машин во время hello ноутбук IPython процесс установки сервера. Мы обслуживаем и обновляем этот репозиторий на постоянной основе. Hello GitHub репозитория tooget hello последние обновленные образец ноутбуков IPython могут посещать пользователи.
![Создание рабочей области][18]

## <a name="upload"></a>Шаг 5: Отправка книжки IPython с локального компьютера toohello ноутбук IPython сервера
Ноутбуков IPython предоставляют простой способ для пользователей tooupload книжки IPython на их локальных компьютерах toohello ноутбук IPython server на виртуальных машинах hello. После входа в систему toohello ноутбук IPython в веб-браузере, щелкните значок hello **каталог** , hello, будут отправлены ноутбук IPython. Выберите tooupload файл .ipynb ноутбук IPython с локального компьютера hello в hello **проводнике**и перетащите его toohello ноутбук IPython directory hello веб-браузере. Нажмите кнопку hello **отправить** кнопку tooupload hello .ipynb файл toohello ноутбук IPython сервера. После этого другие люди смогут пользоваться этим файлом из своих веб-браузеров.

![Создание рабочей области][22]

![Создание рабочей области][23]

## <a name="shutdown"></a>Завершение работы и отмена распределения памяти для виртуальной машины, когда она не используется
За виртуальные машины Azure вы **платите только по факту использования**. tooensure, не выполняется выставлен счет, без использования виртуальной машины, он имеет toobe hello **остановлена (освобождена)** состояние в случае использования.

> [!NOTE]
> При завершении работы виртуальной машины hello с внутри виртуальной Машины (с помощью параметров электропитания Windows), hello hello ВМ останавливается, но остается выделенной. tooensure toobe выставлен счет, не используют всегда остановка виртуальных машин из hello [классический портал Azure](http://manage.windowsazure.com/). Также можно остановить hello ВМ с помощью Powershell, вызвав **ShutdownRoleOperation** слишком с «PostShutdownAction» равно «StoppedDeallocated».
> 
> 

tooshut вниз и освобождать hello виртуальной машины:

1. Войдите в toohello [классический портал Azure](http://manage.windowsazure.com/) под своей учетной записью.  
2. Выберите **виртуальные МАШИНЫ** hello левой навигационной панели.
3. В списке hello виртуальных машин, щелкните имя вашей виртуальной машины, а затем последовательно выберите toohello hello **МОНИТОРИНГА** страницы.
4. Внизу hello страницы приветствия щелкните **завершение работы**.

![Завершение работы виртуальной машины][15]

Hello виртуальной машины будут освобождены, но не удаляется. Можно выполнить перезагрузку виртуальной машины в любое время с hello классический портал Azure.

## <a name="your-azure-vm-is-ready-toouse-whats-next"></a>ВМ Azure — Готово toouse: дальнейшие действия?
Виртуальная машина больше не готов toouse в вашей упражнениях обработки и анализа данных. Виртуальная машина Hello также готова для использования в качестве сервер ноутбук IPython для исследования hello и обработку данных и других задач в сочетании с машинного обучения Azure и hello командного процесса обработки и анализа данных.

Дальнейшие действия Hello в сопоставлении командных процессов обработки и анализа данных в hello hello [обучения путь](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) и могут включать действия для перемещения данных в HDInsight процесса и пример он существует в процессе подготовки для обучения на основе данных hello с машиной Azure Изучение.

[15]: ./media/machine-learning-data-science-setup-virtual-machine/vmshutdown.png
[17]: ./media/machine-learning-data-science-setup-virtual-machine/add-endpoints-after-creation.png
[18]: ./media/machine-learning-data-science-setup-virtual-machine/sample-ipnbs.png
[19]: ./media/machine-learning-data-science-setup-virtual-machine/dns-name-and-host-name.png
[20]: ./media/machine-learning-data-science-setup-virtual-machine/browser-warning-ie.png
[21]: ./media/machine-learning-data-science-setup-virtual-machine/browser-warning.png
[22]: ./media/machine-learning-data-science-setup-virtual-machine/upload-ipnb-1.png
[23]: ./media/machine-learning-data-science-setup-virtual-machine/upload-ipnb-2.png
[24]: ./media/machine-learning-data-science-setup-virtual-machine/create-virtual-machine-1.png
[25]: ./media/machine-learning-data-science-setup-virtual-machine/create-virtual-machine-2.png
[26]: ./media/machine-learning-data-science-setup-virtual-machine/create-virtual-machine-3.png
[27]: ./media/machine-learning-data-science-setup-virtual-machine/create-virtual-machine-4.png
[28]: ./media/machine-learning-data-science-setup-virtual-machine/create-virtual-machine-5.png
[29]: ./media/machine-learning-data-science-setup-virtual-machine/create-virtual-machine-6.png
