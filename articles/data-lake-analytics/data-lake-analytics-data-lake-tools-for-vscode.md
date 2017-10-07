---
title: "Средства Azure Data Lake — использование средств Azure Data Lake для Visual Studio Code | Документация Майкрософт"
description: "Узнайте, как проверить toouse средства Озера данных Azure для toocreate кода Visual Studio и выполнить скрипт U-SQL. "
Keywords: "VScode, средства Озера данных Azure, локального выполнения файла хранилища предварительного просмотра локальной отладки, локальной отладки, отправьте toostorage путь"
services: data-lake-analytics
documentationcenter: 
author: jejiang
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: dc9b21d8-c5f4-4f77-bcbc-eff458f48de2
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/14/2017
ms.author: jejiang
ms.openlocfilehash: 77771c5d5dae3bfce4ad2df240ea6c6ef848f288
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-data-lake-tools-for-visual-studio-code"></a>Использование средств Azure Data Lake для Visual Studio Code

Узнайте, как проверить toouse средства Озера данных Azure для toocreate кода Visual Studio (VS Code) и выполнить скрипт U-SQL. Hello сведения рассматриваются следующие видео hello:

<a href="https://www.youtube.com/watch?v=J_gWuyFnaGA&feature=youtu.be"><img src="./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-video.png"></a>

## <a name="prerequisites"></a>Предварительные требования

Средства Озера данных могут устанавливаться на платформах hello, поддерживаемых в VS Code. Hello поддерживается платформам относятся Windows, Linux и MacOS. Hello различных платформ имеют hello следующие предварительные требования:

- Windows

    - [Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).
    - [Среда выполнения Java SE, версия 8 с обновлением 77 или более поздние выпуски](https://java.com/download/manual.jsp). Добавьте hello java.exe путь toohello системы среды переменной путь. Инструкции по настройке см. в разделе [как задать или изменить системную переменную пути hello?]( https://www.java.com/download/help/path.xml). аналогичные tooC:\Program Files\Java\jdk1.8.0_77\jre\bin указан путь Hello.
    - [Пакет SDK для .NET Core 1.0.3 или среда выполнения .NET Core 1.1](https://www.microsoft.com/net/download).
    
- Linux (мы рекомендуем использовать Ubuntu 14.04 LTS)

    - [Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx). tooinstall Здравствуйте кода, введите следующую команду hello:

              sudo dpkg -i code_<version_number>_amd64.deb

    - [Mono 4.2.x](http://www.mono-project.com/docs/getting-started/install/linux/). 

        - пакет deb hello tooupdate источников, вводить hello, следующие команды:

                sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF
                echo "deb http://download.mono-project.com/repo/debian wheezy/snapshots 4.2.4.4/main" | sudo tee /etc/apt/sources.list.d/mono-xamarin.list
                sudo apt-get update

        - tooinstall моно, введите следующую команду hello:

                sudo apt-get install mono-complete

            > [!NOTE] 
            > Mono 4.6 не поддерживается. Полностью удалите версию 4.6 перед установкой версии 4.2.х.  

        - [Среда выполнения Java SE, версия 8 с обновлением 77 или более поздние выпуски](https://java.com/download/manual.jsp). Инструкции по установке см. в разделе hello [инструкции по установке Linux x 64 для Java]( https://java.com/en/download/help/linux_x64_install.xml) страницы.
        - [Пакет SDK для .NET Core 1.0.3 или среда выполнения .NET Core 1.1](https://www.microsoft.com/net/download).
- MacOS

    - [Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).
    - [Mono 4.2.4](http://download.mono-project.com/archive/4.2.4/macos-10-x86/). 
    - [Среда выполнения Java SE, версия 8 с обновлением 77 или более поздние выпуски](https://java.com/download/manual.jsp). Инструкции по установке см. в разделе hello [инструкции по установке Linux x 64 для Java](https://java.com/en/download/help/mac_install.xml) страницы.
    - [Пакет SDK для .NET Core 1.0.3 или среда выполнения .NET Core 1.1](https://www.microsoft.com/net/download).

## <a name="install-data-lake-tools"></a>Установка средств Data Lake

После установки необходимых компонентов hello, можно установить средства Озера данных для VS Code.

**tooinstall средства Озера данных**

1. Откройте Visual Studio Code.
2. Выберите сочетание клавиш Ctrl + P, а затем введите hello следующую команду:
```
ext install usql-vscode-ext
```
Вы увидите список расширений для Visual Studio Code. Среди них есть **средства Azure Data Lake**.

3. Выберите **установить** Далее слишком**средства Озера данных Azure**. Через несколько секунд hello **установить** кнопку изменения слишком**перезагрузить**.
4. Выберите **перезагрузить** tooactivate hello расширения.
5. Выберите **ОК** tooconfirm. Вы увидите средства Озера данных Azure на hello **расширения** области.
    ![Средства Data Lake в области "Расширения" Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extensions.png)

## <a name="activate-azure-data-lake-tools"></a>Активация Средств Azure Data Lake
Создайте новый файл .usql или откройте существующий .usql tooactivate hello расширение файла. 

## <a name="connect-tooazure"></a>Подключение tooAzure

Прежде чем можно будет скомпилировать и выполнить скрипт U-SQL в аналитике Озера данных, необходимо подключить tooyour учетная запись Azure.

**tooconnect tooAzure**

1.  Выберите палитру команд hello tooopen Ctrl + Shift + P. 
2.  Введите текст **ADL: Login**. сведения об имени входа Hello отображается в hello **вывода** области.

    ![Палитра команд средств Data Lake для Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extension-login.png)
    ![Сведения о входе устройства в средства Data Lake для Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-login-info.png)
3. Выберите сочетание клавиш Ctrl + щелкнуть URL-адрес входа hello: https://aka.ms/devicelogin tooopen hello входа веб-страницы. Введите код hello **G567LX42V** в hello текстовое поле, а затем выберите **Продолжить**.

   ![Вставка кода для входа в Средства Data Lake для Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extension-login-paste-code.png )   
4.  Следуйте toosign инструкции hello в веб-страницу приветствия. Если вы подключены, имя учетной записи Azure отображается в строке состояния hello в левом нижнем углу hello hello **VS Code** окна. 

    > [!NOTE] 
    > Если для учетной записи используется двухфакторная проверка подлинности, мы советуем использовать проверку подлинности через телефон, а не PIN-код.

toosign, введите команду hello **ADL: выхода**.

## <a name="list-your-data-lake-analytics-accounts"></a>Вывод списка учетных записей Data Lake Analytics

соединение tootest hello, получить список учетных записей аналитики Озера данных.

**учетные записи аналитики Озера данных toolist hello в рамках подписки Azure**

1. Выберите палитру команд hello tooopen Ctrl + Shift + P.
2. Введите команду **ADL: List Accounts**. Hello учетные записи отображаются в hello **вывода** области.

## <a name="open-hello-sample-script"></a>Привет открыть образец сценария
Откройте палитру команд hello (Ctrl + Shift + P) и введите **ADL: Откройте пример сценария**. При этом откроется другой экземпляр этого примера. Также можно изменять, настраивать и отправлять скрипт в этом экземпляре.

## <a name="work-with-u-sql"></a>Работа с U-SQL

Требуется откройте файл U-SQL или toowork папки с U-SQL.

**tooopen папки для проекта U-SQL**

1. Из кода Visual Studio, выберите hello **файл** меню, а затем выберите **открыть папку**.
2. Укажите папку и выберите **Выбрать папку**.
3. Выберите hello **файл** меню, а затем выберите **New**. Toohello проект добавляется файл безымянный-1.
4. Введите следующий код в файл hello безымянный 1 hello:

        @departments  = 
            SELECT * FROM 
                (VALUES
                    (31,    "Sales"),
                    (33,    "Engineering"), 
                    (34,    "Clerical"),
                    (35,    "Marketing")
                ) AS 
                      D( DepID, DepName );
         
        OUTPUT @departments
            TO “/Output/departments.csv”

    Hello сценарий создает файл departments.csv часть данных, включенных в папке/Output hello.

5. Сохраните файл как файл hello **myUSQL.usql** в Привет открыть папку. Файл конфигурации adltools_settings.json также добавляется toohello проекта.
4. Откройте и настройте adltools_settings.json с hello следующие свойства:

    - Account: учетная запись Data Lake Analytics, входящая в вашу подписку Azure.
    - Database: база данных в вашей учетной записи. по умолчанию Hello — **master**.
    - Schema: схема в базе данных. по умолчанию Hello — **dbo**.
    - Необязательные параметры:
        - Приоритет: hello приоритет диапазон: 1 too1000 с 1 как hello наивысший приоритет. значение по умолчанию Hello — **1000**.
        - Параллелизм: hello параллелизма диапазон: 1 too150. значение по умолчанию Hello — Максимальная параллелизма hello допускается в вашей учетной записи аналитики Озера данных Azure. 
        
        > [!NOTE] 
        > Если параметры hello являются недопустимыми, используются значения по умолчанию hello.

    ![Файл конфигурации средств Data Lake для Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-configuration-file.png)

    Учетная запись аналитики Озера данных является вычислительных требуется toocompile и запустите задания U-SQL. Перед можно скомпилировать и запустить задания U-SQL, необходимо настроить учетную запись компьютера hello.
    
После сохранения конфигурации hello hello сведения учетной записи, базы данных и схемы отображается в строке состояния hello в нижний левый угол hello соответствующего файла .usql hello. 
 
 
Сравниваемые tooopening файл при открытии папки, которые вы можете:

- Использовать файл с выделенным кодом. В режиме одного файла hello кода не поддерживается.
- Использовать файл конфигурации. При открытии папки сценариев hello в рабочую папку hello совместно использовать один файл конфигурации.


Hello скрипт U-SQL компилирует удаленно через hello Служба аналитики Озера данных. При использовании команды hello **компиляции** команды отправки учетной записи аналитики Озера данных tooyour hello скрипт U-SQL. Более поздней версии Visual Studio Code получает результат компиляции hello. Из-за toohello удаленного компиляции кода Visual Studio требуется перечисляются сведения hello tooconnect tooyour учетную запись аналитики Озера данных в файле конфигурации hello.

**сценарий toocompile U-SQL**

1. Выберите палитру команд hello tooopen Ctrl + Shift + P. 
2. Введите **ADL: Compile Script**. Hello компиляции результаты отображаются в hello **вывода** окна. Можно также щелкнуть правой кнопкой файл скрипта и выберите **ADL: компиляции сценария** задания toocompile U-SQL. Результат компиляции Hello появится в hello **вывода** области.
 

**сценарий toosubmit U-SQL**

1. Выберите палитру команд hello tooopen Ctrl + Shift + P. 
2. Введите **ADL: Submit Job**.  Также можно щелкнуть правой кнопкой мыши файл скрипта и выбрать **ADL: Submit Job**. 

После отправки задания U-SQL, журналы отправки hello, отображаются в hello **вывода** окна в VS Code. При успешном выполнении отправки hello также появляются hello задания URL-адрес. Можно открыть URL-адрес задания hello веб браузера tootrack hello задания в режиме реального времени состояние.

задать tooenable hello вывод сведений о задании hello, **jobInformationOutputPath** в hello **vs code для hello u-sql_settings.json** файл.
 
## <a name="use-a-code-behind-file"></a>Использование файла с выделенным кодом

Файл с выделенным кодом является файлом C#, который связан с одним скриптом U-SQL. Можно определить tooUDO выделенное сценария, определяемая пользователем Агрегатная Функция, определяемый пользователем тип и определяемой пользователем функции в файле кода hello. Hello определяемого пользователем ОПЕРАТОРА, определяемая пользователем Агрегатная Функция, определяемый пользователем тип и определяемой пользователем функции можно использовать непосредственно в скрипт hello без регистрации сборки hello сначала. Hello кода файл будет помещен в hello же папке, что файл пиринга скрипт U-SQL. Если скрипт hello называется xxx.usql, кода hello называется xxx.usql.cs. Если вы вручную удалите файл кода hello, компонент кода hello отключен для его связанный скрипт U-SQL. Дополнительные сведения о написании пользовательского кода для скриптов U-SQL можно найти в записи блога [Writing and Using Custom Code in U-SQL – User-Defined Functions]( https://blogs.msdn.microsoft.com/visualstudio/2015/10/28/writing-and-using-custom-code-in-u-sql-user-defined-functions/) (Написание и использование пользовательского кода в U-SQL — определяемые пользователем функции).

toosupport кода программной части, необходимо открыть рабочую папку. 

**файл кода программной toogenerate**

1. Откройте исходный файл. 
2. Выберите палитру команд hello tooopen Ctrl + Shift + P.
3. Введите **ADL: Generate Code Behind**. Файл кода создается в hello же папки. 

Также можно щелкнуть правой кнопкой мыши файл скрипта и выбрать **ADL: Generate Code Behind**. 

toocompile и отправка Здравствуйте скрипт U-SQL с помощью файла кода, так же, как файл скрипта hello автономный U-SQL.

следующие два снимка экрана приветствия отображения файла кода и связанный с ней файл скрипт U-SQL:
 
![Код программной части в средствах Data Lake для Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-code-behind.png)

![Файл скрипта кода программной части в средствах Data Lake для Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-code-behind-call.png) 

## <a name="use-assemblies"></a>Использование сборок

Дополнительные сведения о разработке сборок см. в статье [Разработка сборок U-SQL для заданий Azure Data Lake Analytics](data-lake-analytics-u-sql-develop-assemblies.md).

Сборки с пользовательским кодом tooregister средств Озера данных можно использовать в каталоге аналитики Озера данных hello.

**tooregister сборки**

Можно зарегистрировать сборку hello через hello **ADL: регистрация сборки** или **ADL: регистрация сборки с помощью конфигурации** команд.

**tooregister через hello ADL: команда регистрация сборки**
1.  Выберите палитру команд hello tooopen Ctrl + Shift + P.
2.  Введите **ADL: Register Assembly**. 
3.  Укажите путь к локальной сборки hello. 
4.  Выберите учетную запись Data Lake Analytics.
5.  Выберите базу данных.

Результаты: hello портала открывается в браузере и отображает процесс регистрации сборки hello.  

Другой hello удобный способ tootrigger **ADL: регистрация сборки** команда является tooright щелчком hello DLL-файл в проводнике. 

**tooregister хотя hello ADL: регистрация сборки с помощью команды конфигурации**
1.  Выберите палитру команд hello tooopen Ctrl + Shift + P.
2.  Введите **ADL: Register Assembly through Configuration**. 
3.  Укажите путь к локальной сборки hello. 
4.  отображается Hello JSON-файла. Просмотрите и при необходимости измените зависимости сборки hello и параметров ресурса. Инструкции отображаются в hello **вывода** окна. tooproceed toohello регистрацию сборки, сохраните файл JSON hello (Ctrl + S).

![Код программной части в средствах Data Lake для Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-register-assembly-advance.png)
>[!NOTE]
>- Зависимости сборок: инструменты Azure Озера данных autodetects ли hello DLL не зависит. зависимости Hello отображаются в файле JSON hello после их обнаружения. 
>- Ресурсы: Библиотека DLL ресурсов (например, txt, .png и CSV) можно передать в процессе регистрации сборки hello. 

Другой способ tootrigger hello **ADL: регистрация сборки с помощью конфигурации** команда является tooright щелчком hello DLL-файл в проводнике. 

Hello после кода U-SQL демонстрирует, каким образом toocall сборки. В образце hello является имя сборки hello *тестирования*.

```
REFERENCE ASSEMBLY [test];

@a = 
    EXTRACT 
        Iid int,
    Starts DateTime,
    Region string,
    Query string,
    DwellTime int,
    Results string,
    ClickedUrls string 
    FROM @"Sample/SearchLog.txt" 
    USING Extractors.Tsv();

@d =
    SELECT DISTINCT Region 
    FROM @a;

@d1 = 
    PROCESS @d
    PRODUCE 
        Region string,
    Mkt string
    USING new USQLApplication_codebehind.MyProcessor();

OUTPUT @d1 
    too@"Sample/SearchLogtest.txt" 
    USING Outputters.Tsv();
```


## <a name="access-hello-data-lake-analytics-catalog"></a>Аналитика Озера данных каталога доступа hello

После подключения tooAzure, можно использовать следующие шаги tooaccess hello U-SQL каталога hello.

**Аналитика Озера данных Azure метаданных tooaccess hello**

1.  Нажмите клавиши CTRL+SHIFT+P, а затем введите **ADL: List Tables**.
2.  Выберите одну из учетных записей hello аналитики Озера данных.
3.  Выберите одну из баз данных hello аналитики Озера данных.
4.  Выберите одну из схем hello. Вы увидите список hello таблиц.

## <a name="view-data-lake-analytics-jobs"></a>Просмотр заданий Data Lake Analytics

**Аналитика Озера данных задания tooview**
1.  Откройте палитру команд hello (Ctrl + Shift + P) и выберите **ADL: Показать задания**. 
2.  Выберите Data Lake Analytics или локальную учетную запись. 
3.  Дождитесь hello список заданий для hello tooappear учетной записи.
4.  Выберите задание из списка заданий, средства Озера данных открывается сведений о задании hello в hello портал Azure и открывает файл JobInfo hello в VS Code.

![Типы объектов IntelliSencse в средствах Data Lake для Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-show-job.png)

## <a name="azure-data-lake-storage-integration"></a>Интеграция с Azure Data Lake Store

Связанные с Azure Data Lake Store команды можно использовать для:
 - Выполнять поиск ресурсов хранилища Озера данных Azure hello. 
 - Файл хранилища Озера данных Azure hello предварительного просмотра.  
 - Отправка hello tooAzure хранилища Озера данных файла непосредственно в VS Code. 

### <a name="list-hello-storage-path"></a>Путь к списку hello хранилища 
Можно составить список hello путь к хранилищу через палитру команд hello или щелкните правой кнопкой мыши.

**путь к хранилищу hello toolist через палитру команд hello**

1.  Откройте палитру команд hello (Ctrl + Shift + P) и введите **ADL: путь к хранилищу списка**.

    ![Вывод пути к хранилищу в средствах Data Lake для Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-storage.png)

2.  Выберите для перечисления путь к хранилищу hello предпочтительным. В этом примере выбран вариант **Enter a path** (Введите путь).

    ![Средства Озера данных для кода Visual Studio одним из способов toolist путь к хранилищу hello](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account-selectoneway.png)

    > [!NOTE]
    >- VS Code сохраняет путь к последней посетил hello в каждой учетной записи аналитики Озера данных. Например, /tt/ss.
    >- Браузер из путь к корневому каталогу: корневой путь к списку hello из выбранной учетной записи аналитики Озера данных или локальный путь.
    >- Введите путь: вывод указанного пути из выбранной учетной записи Azure Data Lake Analytics или локального пути.
    
3. Выберите учетную запись из hello локальный путь или учетную запись аналитики Озера данных.

    ![Средства Data Lake для Visual Studio Code: выбор дополнительных учетных записей](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

4. Выберите **дополнительные** toolist дополнительные учетные записи аналитики Озера данных, а затем выберите учетную запись аналитики Озера данных.

    ![Средства Data Lake для Visual Studio Code: выбор учетной записи](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-select-adla-account.png)

5.  Введите путь к хранилищу Azure. Например, /output.

    ![Ввод пути к хранилищу в средствах Data Lake для Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-input-path.png)

6.  Результаты: hello палитры команд сведения hello путь на основе ваших записей.

    ![Результат вывода пути к хранилищу в средствах Data Lake для Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-path.png)

Более удобный toolist hello относительный путь — через hello контекстное меню, щелкните правой кнопкой мыши.

**Щелкните правой кнопкой мыши путь к хранилищу hello toolist через**

1.  Щелкните правой кнопкой мыши tooselect строку hello путь **путь к списку хранилища**.

       ![Контекстное меню в средствах Data Lake для Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-right-click-path.png)

2. Выбранный путь относительный Hello появляется в палитру команд hello.

   ![Выбранный относительный путь средств Data Lake для Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-relative-path.png)

3.  Выберите учетную запись из hello локальный путь или учетную запись аналитики Озера данных.

       ![Средства Data Lake для Visual Studio Code: выбор учетной записи](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

4.  Результаты: hello палитры команд перечислены hello папок и файлов для hello текущий путь.

       ![Средства Озера данных для списка кода Visual Studio из текущего пути hello](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-current.png)

### <a name="preview-hello-storage-file"></a>Файл хранилища hello предварительного просмотра
Можно просмотреть файл хранилища hello через палитру команд hello или щелкните правой кнопкой мыши.

**файл хранилища hello toopreview через палитру команд hello**

1.  Откройте палитру команд hello (Ctrl + Shift + P) и введите **ADL: просмотр хранения файла**.

       ![Предварительный просмотр файла хранилища в средствах Data Lake для Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-preview.png)

2.  Выберите учетную запись из hello локальный путь или учетную запись аналитики Озера данных.

       ![Список учетных данных в средствах Data Lake для Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

3.  Выберите **дополнительные** toolist дополнительные учетные записи аналитики Озера данных, а затем выберите учетную запись аналитики Озера данных.

       ![Средства Data Lake для Visual Studio Code: выбор учетной записи](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-select-adla-account.png)

4.  Введите путь к хранилищу или имя файла хранилища Azure. Например, /output/SearchLog.txt.

       ![Ввод пути к хранилищу и имени файла хранилища в средствах Data Lake для Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-input-preview-file.png)

5.  Результаты: hello палитры команд сведения hello путь на основе ваших записей.

       ![Результат предварительного просмотра файла в Средствах Data Lake для Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-preview-results.png)

**Щелкните правой кнопкой мыши путь к хранилищу hello toolist через**

1.  toopreview файл, щелкните правой кнопкой мыши путь к файлу hello.

   ![Контекстное меню в средствах Data Lake для Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-right-click-preview.png) 

2.  Выберите учетную запись из hello локальный путь или учетную запись аналитики Озера данных.

       ![Средства Data Lake для Visual Studio Code: выбор учетной записи](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

3.  Результаты: VS Code отображает hello результатов предварительного просмотра файла hello.

       ![Результат предварительного просмотра файла в Средствах Data Lake для Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-preview-results.png)

### <a name="upload-a-file"></a>Отправить файл. 

Можно отправить файлы, введя hello команды **ADL: Отправьте файл** или **ADL: Отправьте файл через конфигурацию**.

**файлы tooupload хотя hello ADL: Отправьте файл-команда**
1. Выберите палитру команд hello tooopen Ctrl + Shift + P или щелкните правой кнопкой мыши редактор сценариев hello, а затем введите **передать файл**.
2.  tooupload hello, введите локальный путь.

    ![Ввод локального пути в средствах Data Lake для Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-auto-input-local-path.png)

3. Выберите один из способов hello путь к хранилищу листинг hello. В этом примере выбран вариант **Enter a path** (Введите путь).

    ![Вывод пути к хранилищу в средствах Data Lake для Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account-selectoneway.png)
    >[!NOTE]
    >- VS Code сохраняет путь к последней посетил hello в каждой учетной записи аналитики Озера данных. Например, /tt/ss.
    >- Браузер из путь к корневому каталогу: корневой путь к списку hello из выбранной учетной записи аналитики Озера данных или локальный путь.
    >- Введите путь: вывод указанного пути из выбранной учетной записи Azure Data Lake Analytics или локального пути.

4. Выберите учетную запись из hello локальный путь или учетную запись аналитики Озера данных.

    ![Контекстное меню хранилища в средствах Data Lake для Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

5. Введите путь к хранилищу Azure. Например, /output.

       ![Data Lake Tools for Visual Studio Code enter storage path](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-input-preview-file.png)

6. Найдите путь к хранилищу Azure. Выберите пункт **Choose current folder** (Выбрать текущую папку).

    ![Выбор папки в средствах Data Lake для Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-choose-current-folder.png)

7.  Результаты: hello **вывода** окно отображает состояние передачи файла hello.

       ![Состояние отправки в средствах Data Lake для Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-upload-status.png)    

**файлы tooupload хотя hello ADL: Отправьте файл через команду конфигурации**
1.  Выберите палитру команд hello tooopen Ctrl + Shift + P или щелкните правой кнопкой мыши редактор сценариев hello, а затем введите **передать файл конфигурации**.
2.  В VS Code отобразится JSON-файл. Можно ввести пути к файлам и отправить несколько файлов в hello то же время. Инструкции отображаются в hello **вывода** окна. tooproceed tooupload hello файл, сохраните файл JSON hello (Ctrl + S).

       ![Путь к файлу в средствах Data Lake для Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-upload-file.png)

3.  Результаты: hello **вывода** окно отображает состояние передачи файла hello.

       ![Состояние отправки в средствах Data Lake для Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-upload-status.png)     

Другой способ tooupload toostorage файла — через hello щелкните правой кнопкой мыши меню полный путь к файлу hello или относительный путь файла hello в редакторе сценариев hello. Введите путь к локальному файлу hello, а затем выберите hello учетной записи. Hello **вывода** окне отображается состояние передачи hello. 

### <a name="open-azure-storage-explorer"></a>Открытие обозревателя хранилищ Azure
Можно открыть **обозреватель хранилищ Azure** , введя команду hello **ADL: Откройте веб-обозреватель хранилища Azure** или выбрав его из контекстного меню hello.

**tooopen обозреватель хранилищ Azure**

1. Выберите палитру команд hello tooopen Ctrl + Shift + P.
2. Введите **откройте веб-обозреватель хранилища Azure** или щелкните правой кнопкой мыши на относительный путь или полный путь hello в редакторе сценариев hello и выберите **откройте веб-обозреватель хранилища Azure**.
3. Выберите учетную запись Data Lake Analytics.

Средства Озера данных открывает путь хранилища Azure hello в hello портал Azure. Можно найти hello пути и предварительного просмотра файла hello из Интернета hello.

### <a name="local-run-and-local-debug-for-windows-users"></a>Локальное выполнение и локальная отладка для пользователей Windows
U-SQL локального выполнения проверяет локальных данных и проверяет скрипт с локально, перед код является опубликованной tooData аналитики Озера. Аналитика Озера tooData отправлен вам toocomplete hello следующие задачи, прежде чем код станет компонент позволяет локальной отладки Hello: 
- Отладка кода программной части C#. 
- Пошаговое выполнение кода hello. 
- Проверка скрипта локально.

Инструкции по локальному выполнению и отладке см. в статье [Локальный запуск и локальная отладка U-SQL в Visual Studio Code](data-lake-tools-for-vscode-local-run-and-debug.md).

## <a name="additional-features"></a>Дополнительные функции

Средства Озера данных для VS Code поддерживает hello следующие атрибуты:

-   Автоматическое завершение IntelliSense: предлагаемые варианты отображаются во всплывающих окнах вокруг элементов, таких как ключевые слова, методы и переменные. Другие значки представляют различные типы объектов hello.

    - тип данных Scala;
    - сложный тип данных;
    - встроенные пользовательские типы;
    - коллекции и классы .NET;
    - выражения C#;
    - встроенные функции и объекты C#, определяемые пользователем; 
    - функции U-SQL;
    - функции U-SQL для работы с окнами.
 
    ![Типы объектов IntelliSencse в средствах Data Lake для Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-auto-complete-objects.png)
 
-   Технология IntelliSense, автоматическое завершение метаданных аналитики Озера данных: средства Озера данных загружает hello аналитики Озера данных сведения о метаданных локально. функция IntelliSense Hello автоматически заполняет объекты, включая hello базы данных, схемы, таблиц, представлений, возвращающих табличные значения функции, процедуры и C# сборки, из метаданных hello аналитики Озера данных.
 
    ![Метаданные IntelliSense в средствах Data Lake для Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-auto-complete-metastore.png)

-   Маркер ошибки IntelliSense: средства Озера данных подчеркивает hello редактирования ошибки U-SQL и C#. 
-   Выделение синтаксиса: средств Озера данных использует элементы toodifferentiate различные цвета, например переменные, ключевые слова, тип данных и функции. 

    ![Подсветка синтаксиса в средствах Data Lake для Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-syntax-highlights.png)

## <a name="next-steps"></a>Дальнейшие действия

- Дополнительные сведения о локальном выполнении и локальной отладке U-SQL с помощью Visual Studio Code см. в статье [Локальный запуск и локальная отладка U-SQL в Visual Studio Code](data-lake-tools-for-vscode-local-run-and-debug.md).
- Дополнительные сведения о начале работы с Data Lake Analytics см. в статье [Начало работы с Azure Data Lake Analytics с помощью портала Azure](data-lake-analytics-get-started-portal.md).
- Дополнительные сведения об использовании средств Data Lake для U-SQL см. в статье [Разработка скриптов U-SQL с помощью средств Data Lake для Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).
- Дополнительные сведения о разработке сборок см. в статье [Разработка сборок U-SQL для заданий Azure Data Lake Analytics](data-lake-analytics-u-sql-develop-assemblies.md).



