---
title: "Средства Azure Data Lake — использование средств Azure Data Lake для Visual Studio Code | Документация Майкрософт"
description: "Узнайте, как с помощью средств Azure Data Lake для Visual Studio Code создавать, тестировать и выполнять скрипты U-SQL. "
Keywords: "VScode,средства Azure Data Lake,локальный запуск,локальная отладка,предварительный просмотр файла хранилища,отправка по пути хранилища"
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
ms.openlocfilehash: 833d14af47454a01fa3c97ffa854d688dd35871f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-data-lake-tools-for-visual-studio-code"></a><span data-ttu-id="13007-104">Использование средств Azure Data Lake для Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="13007-104">Use Azure Data Lake Tools for Visual Studio Code</span></span>

<span data-ttu-id="13007-105">Узнайте, как с помощью средств Azure Data Lake для Visual Studio Code (VS Code) создавать, тестировать и выполнять скрипты U-SQL.</span><span class="sxs-lookup"><span data-stu-id="13007-105">Learn how to use Azure Data Lake Tools for Visual Studio Code (VS Code) to create, test, and run U-SQL scripts.</span></span> <span data-ttu-id="13007-106">Эти сведения также представлены в следующем видеоролике:</span><span class="sxs-lookup"><span data-stu-id="13007-106">The information is also covered in the following video:</span></span>

<a href="https://www.youtube.com/watch?v=J_gWuyFnaGA&feature=youtu.be"><img src="./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-video.png"></a>

## <a name="prerequisites"></a><span data-ttu-id="13007-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="13007-107">Prerequisites</span></span>

<span data-ttu-id="13007-108">Средства Data Lake можно устанавливать на всех платформах, поддерживаемых VS Code,</span><span class="sxs-lookup"><span data-stu-id="13007-108">Data Lake Tools can be installed on the platforms supported by VS Code.</span></span> <span data-ttu-id="13007-109">то есть на Windows, Linux и MacOS.</span><span class="sxs-lookup"><span data-stu-id="13007-109">The supported platforms include Windows, Linux, and MacOS.</span></span> <span data-ttu-id="13007-110">Для разных платформ есть такие предварительные требования:</span><span class="sxs-lookup"><span data-stu-id="13007-110">The different platforms have the following prerequisites:</span></span>

- <span data-ttu-id="13007-111">Windows</span><span class="sxs-lookup"><span data-stu-id="13007-111">Windows</span></span>

    - <span data-ttu-id="13007-112">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="13007-112">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span></span>
    - <span data-ttu-id="13007-113">[Среда выполнения Java SE, версия 8 с обновлением 77 или более поздние выпуски](https://java.com/download/manual.jsp).</span><span class="sxs-lookup"><span data-stu-id="13007-113">[Java SE Runtime Environment version 8 update 77 or later](https://java.com/download/manual.jsp).</span></span> <span data-ttu-id="13007-114">Добавьте путь к файлу java.exe в переменную среды PATH.</span><span class="sxs-lookup"><span data-stu-id="13007-114">Add the java.exe path to the system environment variable path.</span></span> <span data-ttu-id="13007-115">Инструкции по настройке см. в [разделе справки по установке и изменению системной переменной PATH]( https://www.java.com/download/help/path.xml).</span><span class="sxs-lookup"><span data-stu-id="13007-115">For configuration instructions, see [How do I set or change the Path system variable?]( https://www.java.com/download/help/path.xml).</span></span> <span data-ttu-id="13007-116">Обычно путь имеет формат C:\Program Files\Java\jdk1.8.0_77\jre\bin.</span><span class="sxs-lookup"><span data-stu-id="13007-116">The path is similar to C:\Program Files\Java\jdk1.8.0_77\jre\bin.</span></span>
    - <span data-ttu-id="13007-117">[Пакет SDK для .NET Core 1.0.3 или среда выполнения .NET Core 1.1](https://www.microsoft.com/net/download).</span><span class="sxs-lookup"><span data-stu-id="13007-117">[.NET Core SDK 1.0.3 or .NET Core 1.1 runtime](https://www.microsoft.com/net/download).</span></span>
    
- <span data-ttu-id="13007-118">Linux (мы рекомендуем использовать Ubuntu 14.04 LTS)</span><span class="sxs-lookup"><span data-stu-id="13007-118">Linux (We recommend Ubuntu 14.04 LTS)</span></span>

    - <span data-ttu-id="13007-119">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="13007-119">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span></span> <span data-ttu-id="13007-120">Чтобы установить код, введите такую команду:</span><span class="sxs-lookup"><span data-stu-id="13007-120">To install the code, enter the following command:</span></span>

              sudo dpkg -i code_<version_number>_amd64.deb

    - <span data-ttu-id="13007-121">[Mono 4.2.x](http://www.mono-project.com/docs/getting-started/install/linux/).</span><span class="sxs-lookup"><span data-stu-id="13007-121">[Mono 4.2.x](http://www.mono-project.com/docs/getting-started/install/linux/).</span></span> 

        - <span data-ttu-id="13007-122">Чтобы обновить источник пакетов deb, введите такие команды:</span><span class="sxs-lookup"><span data-stu-id="13007-122">To update the deb package source, enter the following commands:</span></span>

                sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF
                echo "deb http://download.mono-project.com/repo/debian wheezy/snapshots 4.2.4.4/main" | sudo tee /etc/apt/sources.list.d/mono-xamarin.list
                sudo apt-get update

        - <span data-ttu-id="13007-123">Чтобы установить Mono, введите такую команду:</span><span class="sxs-lookup"><span data-stu-id="13007-123">To install Mono, enter the following command:</span></span>

                sudo apt-get install mono-complete

            > [!NOTE] 
            > <span data-ttu-id="13007-124">Mono 4.6 не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="13007-124">Mono 4.6 is not supported.</span></span> <span data-ttu-id="13007-125">Полностью удалите версию 4.6 перед установкой версии 4.2.х.</span><span class="sxs-lookup"><span data-stu-id="13007-125">Uninstall version 4.6 entirely before you install 4.2.x.</span></span>  

        - <span data-ttu-id="13007-126">[Среда выполнения Java SE, версия 8 с обновлением 77 или более поздние выпуски](https://java.com/download/manual.jsp).</span><span class="sxs-lookup"><span data-stu-id="13007-126">[Java SE Runtime Environment version 8 update 77 or later](https://java.com/download/manual.jsp).</span></span> <span data-ttu-id="13007-127">Инструкции по установке см. на странице [Linux 64-bit installation instructions for Java]( https://java.com/en/download/help/linux_x64_install.xml) (Инструкции по установке Java для 64-разрядной версии Linux).</span><span class="sxs-lookup"><span data-stu-id="13007-127">For instructions on installation, see the [Linux 64-bit installation instructions for Java]( https://java.com/en/download/help/linux_x64_install.xml) page.</span></span>
        - <span data-ttu-id="13007-128">[Пакет SDK для .NET Core 1.0.3 или среда выполнения .NET Core 1.1](https://www.microsoft.com/net/download).</span><span class="sxs-lookup"><span data-stu-id="13007-128">[.NET Core SDK 1.0.3 or .NET Core 1.1 runtime](https://www.microsoft.com/net/download).</span></span>
- <span data-ttu-id="13007-129">MacOS</span><span class="sxs-lookup"><span data-stu-id="13007-129">MacOS</span></span>

    - <span data-ttu-id="13007-130">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="13007-130">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span></span>
    - <span data-ttu-id="13007-131">[Mono 4.2.4](http://download.mono-project.com/archive/4.2.4/macos-10-x86/).</span><span class="sxs-lookup"><span data-stu-id="13007-131">[Mono 4.2.4](http://download.mono-project.com/archive/4.2.4/macos-10-x86/).</span></span> 
    - <span data-ttu-id="13007-132">[Среда выполнения Java SE, версия 8 с обновлением 77 или более поздние выпуски](https://java.com/download/manual.jsp).</span><span class="sxs-lookup"><span data-stu-id="13007-132">[Java SE Runtime Environment version 8 update 77 or later](https://java.com/download/manual.jsp).</span></span> <span data-ttu-id="13007-133">Инструкции по установке см. на странице [Linux 64-bit installation instructions for Java](https://java.com/en/download/help/mac_install.xml) (Инструкции по установке Java для 64-разрядной версии Linux).</span><span class="sxs-lookup"><span data-stu-id="13007-133">For instructions on installation, see the [Linux 64-bit installation instructions for Java](https://java.com/en/download/help/mac_install.xml) page.</span></span>
    - <span data-ttu-id="13007-134">[Пакет SDK для .NET Core 1.0.3 или среда выполнения .NET Core 1.1](https://www.microsoft.com/net/download).</span><span class="sxs-lookup"><span data-stu-id="13007-134">[.NET Core SDK 1.0.3 or .NET Core 1.1 runtime](https://www.microsoft.com/net/download).</span></span>

## <a name="install-data-lake-tools"></a><span data-ttu-id="13007-135">Установка средств Data Lake</span><span class="sxs-lookup"><span data-stu-id="13007-135">Install Data Lake Tools</span></span>

<span data-ttu-id="13007-136">После установки необходимых компонентов можно установить средства Data Lake для VS Code.</span><span class="sxs-lookup"><span data-stu-id="13007-136">After you install the prerequisites, you can install Data Lake Tools for VS Code.</span></span>

<span data-ttu-id="13007-137">**Установка средств Data Lake**</span><span class="sxs-lookup"><span data-stu-id="13007-137">**To install Data Lake Tools**</span></span>

1. <span data-ttu-id="13007-138">Откройте Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="13007-138">Open Visual Studio Code.</span></span>
2. <span data-ttu-id="13007-139">Нажмите клавиши CTRL+P и введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="13007-139">Select Ctrl+P, and then enter the following command:</span></span>
```
ext install usql-vscode-ext
```
<span data-ttu-id="13007-140">Вы увидите список расширений для Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="13007-140">You can see a list of Visual Studio code extensions.</span></span> <span data-ttu-id="13007-141">Среди них есть **средства Azure Data Lake**.</span><span class="sxs-lookup"><span data-stu-id="13007-141">One of them is **Azure Data Lake Tools**.</span></span>

3. <span data-ttu-id="13007-142">Выберите **Установить** рядом с элементом **Средства Azure Data Lake**.</span><span class="sxs-lookup"><span data-stu-id="13007-142">Select **Install** next to **Azure Data Lake Tools**.</span></span> <span data-ttu-id="13007-143">Через несколько секунд кнопка **Установить** изменится на **Перезагрузить**.</span><span class="sxs-lookup"><span data-stu-id="13007-143">After a few seconds, the **Install** button changes to **Reload**.</span></span>
4. <span data-ttu-id="13007-144">Щелкните **Перезагрузить**, чтобы активировать расширение.</span><span class="sxs-lookup"><span data-stu-id="13007-144">Select **Reload** to activate the extension.</span></span>
5. <span data-ttu-id="13007-145">Выберите **ОК** для подтверждения.</span><span class="sxs-lookup"><span data-stu-id="13007-145">Select **OK** to confirm.</span></span> <span data-ttu-id="13007-146">Средства Azure Data Lake теперь появятся в области **Расширения**.</span><span class="sxs-lookup"><span data-stu-id="13007-146">You can see Azure Data Lake Tools in the **Extensions** pane.</span></span>
    <span data-ttu-id="13007-147">![Средства Data Lake в области "Расширения" Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extensions.png)</span><span class="sxs-lookup"><span data-stu-id="13007-147">![Data Lake Tools for Visual Studio Code Extensions pane](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extensions.png)</span></span>

## <a name="activate-azure-data-lake-tools"></a><span data-ttu-id="13007-148">Активация Средств Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="13007-148">Activate Azure Data Lake Tools</span></span>
<span data-ttu-id="13007-149">Чтобы активировать расширение, создайте новый или откройте имеющийся USQL-файл.</span><span class="sxs-lookup"><span data-stu-id="13007-149">Create a new .usql file or open an existing .usql file to activate the extension.</span></span> 

## <a name="connect-to-azure"></a><span data-ttu-id="13007-150">Подключение к Azure</span><span class="sxs-lookup"><span data-stu-id="13007-150">Connect to Azure</span></span>

<span data-ttu-id="13007-151">Перед компиляцией и выполнением скрипта U-SQL в Data Lake Analytics необходимо подключиться к учетной записи Azure.</span><span class="sxs-lookup"><span data-stu-id="13007-151">Before you can compile and run U-SQL scripts in Data Lake Analytics, you must connect to your Azure account.</span></span>

<span data-ttu-id="13007-152">**Подключение к Azure**</span><span class="sxs-lookup"><span data-stu-id="13007-152">**To connect to Azure**</span></span>

1.  <span data-ttu-id="13007-153">Нажмите клавиши CTRL+SHIFT+P, чтобы открыть палитру команд.</span><span class="sxs-lookup"><span data-stu-id="13007-153">Select Ctrl+Shift+P to open the command palette.</span></span> 
2.  <span data-ttu-id="13007-154">Введите текст **ADL: Login**.</span><span class="sxs-lookup"><span data-stu-id="13007-154">Enter **ADL: Login**.</span></span> <span data-ttu-id="13007-155">Сведения для входа отобразятся в области **Вывод**.</span><span class="sxs-lookup"><span data-stu-id="13007-155">The login information appears in the **Output** pane.</span></span>

    <span data-ttu-id="13007-156">![Палитра команд средств Data Lake для Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extension-login.png)
    ![Сведения о входе устройства в средства Data Lake для Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-login-info.png)</span><span class="sxs-lookup"><span data-stu-id="13007-156">![Data Lake Tools for Visual Studio Code command palette](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extension-login.png)
![Data Lake Tools for Visual Studio Code device login information](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-login-info.png)</span></span>
3. <span data-ttu-id="13007-157">Удерживая клавишу CTRL, щелкните URL-адрес входа https://aka.ms/devicelogin, чтобы открыть веб-страницу входа.</span><span class="sxs-lookup"><span data-stu-id="13007-157">Select Ctrl+click on the login URL: https://aka.ms/devicelogin to open the login webpage.</span></span> <span data-ttu-id="13007-158">Введите код **G567LX42V** в текстовое поле, а затем выберите **Продолжить**.</span><span class="sxs-lookup"><span data-stu-id="13007-158">Enter the code **G567LX42V** into the text box, and then select **Continue**.</span></span>

   ![Вставка кода для входа в Средства Data Lake для Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extension-login-paste-code.png )   
4.  <span data-ttu-id="13007-160">Следуйте инструкциям, предоставленным на веб-странице входа.</span><span class="sxs-lookup"><span data-stu-id="13007-160">Follow the instructions to sign in from the webpage.</span></span> <span data-ttu-id="13007-161">При подключении имя учетной записи Azure отображается в строке состояния в нижнем левом углу окна **VS Code**.</span><span class="sxs-lookup"><span data-stu-id="13007-161">When you're connected, your Azure account name appears on the status bar in the lower-left corner of the **VS Code** window.</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="13007-162">Если для учетной записи используется двухфакторная проверка подлинности, мы советуем использовать проверку подлинности через телефон, а не PIN-код.</span><span class="sxs-lookup"><span data-stu-id="13007-162">If your account has two factors enabled, we recommend that you use phone authentication rather than using a PIN.</span></span>

<span data-ttu-id="13007-163">Для выхода введите команду **ADL: Logout**.</span><span class="sxs-lookup"><span data-stu-id="13007-163">To sign out, enter the command **ADL: Logout**.</span></span>

## <a name="list-your-data-lake-analytics-accounts"></a><span data-ttu-id="13007-164">Вывод списка учетных записей Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="13007-164">List your Data Lake Analytics accounts</span></span>

<span data-ttu-id="13007-165">Чтобы проверить подключение, получите список учетных записей Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="13007-165">To test the connection, get a list of your Data Lake Analytics accounts.</span></span>

<span data-ttu-id="13007-166">**Получение списка учетных записей Data Lake Analytics в подписке Azure**</span><span class="sxs-lookup"><span data-stu-id="13007-166">**To list the Data Lake Analytics accounts under your Azure subscription**</span></span>

1. <span data-ttu-id="13007-167">Нажмите клавиши CTRL+SHIFT+P, чтобы открыть палитру команд.</span><span class="sxs-lookup"><span data-stu-id="13007-167">Select Ctrl+Shift+P to open the command palette.</span></span>
2. <span data-ttu-id="13007-168">Введите команду **ADL: List Accounts**.</span><span class="sxs-lookup"><span data-stu-id="13007-168">Enter **ADL: List Accounts**.</span></span> <span data-ttu-id="13007-169">Учетные записи отображаются в области **Вывода**.</span><span class="sxs-lookup"><span data-stu-id="13007-169">The accounts appear in the **Output** pane.</span></span>

## <a name="open-the-sample-script"></a><span data-ttu-id="13007-170">Открытие примера скрипта</span><span class="sxs-lookup"><span data-stu-id="13007-170">Open the sample script</span></span>
<span data-ttu-id="13007-171">Откройте палитру команд (CTRL+SHIFT+P) и введите **ADL: Open Sample Script**.</span><span class="sxs-lookup"><span data-stu-id="13007-171">Open the command palette (Ctrl+Shift+P) and enter **ADL: Open Sample Script**.</span></span> <span data-ttu-id="13007-172">При этом откроется другой экземпляр этого примера.</span><span class="sxs-lookup"><span data-stu-id="13007-172">This opens another instance of this sample.</span></span> <span data-ttu-id="13007-173">Также можно изменять, настраивать и отправлять скрипт в этом экземпляре.</span><span class="sxs-lookup"><span data-stu-id="13007-173">You can also edit, configure, and submit script on this instance.</span></span>

## <a name="work-with-u-sql"></a><span data-ttu-id="13007-174">Работа с U-SQL</span><span class="sxs-lookup"><span data-stu-id="13007-174">Work with U-SQL</span></span>

<span data-ttu-id="13007-175">Для работы с U-SQL нужно открыть файл или папку U-SQL.</span><span class="sxs-lookup"><span data-stu-id="13007-175">You need open either a U-SQL file or a folder to work with U-SQL.</span></span>

<span data-ttu-id="13007-176">**Открытие папки для проекта U-SQL**</span><span class="sxs-lookup"><span data-stu-id="13007-176">**To open a folder for your U-SQL project**</span></span>

1. <span data-ttu-id="13007-177">В Visual Studio Code выберите меню **Файл**, а затем — **Открыть папку**.</span><span class="sxs-lookup"><span data-stu-id="13007-177">From Visual Studio Code, select the **File** menu, and then select **Open Folder**.</span></span>
2. <span data-ttu-id="13007-178">Укажите папку и выберите **Выбрать папку**.</span><span class="sxs-lookup"><span data-stu-id="13007-178">Specify a folder, and then select **Select Folder**.</span></span>
3. <span data-ttu-id="13007-179">Выберите меню **Файл**, а затем **Создать**.</span><span class="sxs-lookup"><span data-stu-id="13007-179">Select the **File** menu, and then select **New**.</span></span> <span data-ttu-id="13007-180">К проекту будет добавлен файл с именем Untitled-1.</span><span class="sxs-lookup"><span data-stu-id="13007-180">An Untitled-1 file is added to the project.</span></span>
4. <span data-ttu-id="13007-181">Введите следующий код в файл Untitled-1:</span><span class="sxs-lookup"><span data-stu-id="13007-181">Enter the following code into the Untitled-1 file:</span></span>

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

    <span data-ttu-id="13007-182">Этот скрипт создает в папке/output файл departments.csv с некоторыми данными.</span><span class="sxs-lookup"><span data-stu-id="13007-182">The script creates a departments.csv file with some data included in the /output folder.</span></span>

5. <span data-ttu-id="13007-183">Сохраните файл в открытой папке, присвоив ему имя **myUSQL.usql**.</span><span class="sxs-lookup"><span data-stu-id="13007-183">Save the file as **myUSQL.usql** in the opened folder.</span></span> <span data-ttu-id="13007-184">К проекту добавляется еще и файл конфигурации adltools_settings.json.</span><span class="sxs-lookup"><span data-stu-id="13007-184">A adltools_settings.json configuration file is also added to the project.</span></span>
4. <span data-ttu-id="13007-185">Откройте файл adltools_settings.json и установите следующие значения свойств:</span><span class="sxs-lookup"><span data-stu-id="13007-185">Open and configure adltools_settings.json with the following properties:</span></span>

    - <span data-ttu-id="13007-186">Account: учетная запись Data Lake Analytics, входящая в вашу подписку Azure.</span><span class="sxs-lookup"><span data-stu-id="13007-186">Account:  A Data Lake Analytics account under your Azure subscription.</span></span>
    - <span data-ttu-id="13007-187">Database: база данных в вашей учетной записи.</span><span class="sxs-lookup"><span data-stu-id="13007-187">Database: A database under your account.</span></span> <span data-ttu-id="13007-188">По умолчанию используется база данных **master**.</span><span class="sxs-lookup"><span data-stu-id="13007-188">The default is **master**.</span></span>
    - <span data-ttu-id="13007-189">Schema: схема в базе данных.</span><span class="sxs-lookup"><span data-stu-id="13007-189">Schema: A schema under your database.</span></span> <span data-ttu-id="13007-190">Значение по умолчанию — **dbo**.</span><span class="sxs-lookup"><span data-stu-id="13007-190">The default is **dbo**.</span></span>
    - <span data-ttu-id="13007-191">Необязательные параметры:</span><span class="sxs-lookup"><span data-stu-id="13007-191">Optional settings:</span></span>
        - <span data-ttu-id="13007-192">Priority. Значение приоритета в диапазоне от 1 до 1000, где 1 — наивысший приоритет.</span><span class="sxs-lookup"><span data-stu-id="13007-192">Priority: The priority range is from 1 to 1000 with 1 as the highest priority.</span></span> <span data-ttu-id="13007-193">По умолчанию используется значение **1000**.</span><span class="sxs-lookup"><span data-stu-id="13007-193">The default value is **1000**.</span></span>
        - <span data-ttu-id="13007-194">Parallelism: коэффициент параллелизма в диапазоне от 1 до 150.</span><span class="sxs-lookup"><span data-stu-id="13007-194">Parallelism: The parallelism range is from 1 to 150.</span></span> <span data-ttu-id="13007-195">Значением по умолчанию является максимально допустимый коэффициент параллелизма в учетной записи Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="13007-195">The default value is the maximum parallelism allowed in your Azure Data Lake Analytics account.</span></span> 
        
        > [!NOTE] 
        > <span data-ttu-id="13007-196">Если вы введете недопустимые значения, используются значения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="13007-196">If the settings are invalid, the default values are used.</span></span>

    ![Файл конфигурации средств Data Lake для Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-configuration-file.png)

    <span data-ttu-id="13007-198">Для компиляции и выполнения заданий U-SQL вам потребуется учетная запись вычислений Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="13007-198">A compute Data Lake Analytics account is needed to compile and run U-SQL jobs.</span></span> <span data-ttu-id="13007-199">Настройте учетную запись вычислений, прежде чем компилировать и запускать задания U-SQL.</span><span class="sxs-lookup"><span data-stu-id="13007-199">You must configure the computer account before you can compile and run U-SQL jobs.</span></span>
    
<span data-ttu-id="13007-200">После сохранения конфигурации сведения учетной записи, базы данных и схемы отображаются в строке состояния в нижнем левом углу соответствующего USQL-файла.</span><span class="sxs-lookup"><span data-stu-id="13007-200">After the configuration is saved, the account, database, and schema information appears on the status bar at the bottom-left corner of the corresponding .usql file.</span></span> 
 
 
<span data-ttu-id="13007-201">По сравнению с открытием файла при открытии папки можно:</span><span class="sxs-lookup"><span data-stu-id="13007-201">Compared to opening a file, when you open a folder you can:</span></span>

- <span data-ttu-id="13007-202">Использовать файл с выделенным кодом.</span><span class="sxs-lookup"><span data-stu-id="13007-202">Use a code-behind file.</span></span> <span data-ttu-id="13007-203">В режиме одного файла функция Code Behind не поддерживается;</span><span class="sxs-lookup"><span data-stu-id="13007-203">In the single-file mode, code-behind is not supported.</span></span>
- <span data-ttu-id="13007-204">Использовать файл конфигурации.</span><span class="sxs-lookup"><span data-stu-id="13007-204">Use a configuration file.</span></span> <span data-ttu-id="13007-205">Если открыть папку, скрипты из этой рабочей папки будут совместно использовать один файл конфигурации.</span><span class="sxs-lookup"><span data-stu-id="13007-205">When you open a folder, the scripts in the working folder share a single configuration file.</span></span>


<span data-ttu-id="13007-206">Скрипт U-SQL компилируется удаленно через службу Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="13007-206">The U-SQL script compiles remotely through the Data Lake Analytics service.</span></span> <span data-ttu-id="13007-207">При запуске команды **compile** скрипт U-SQL отправляется в учетную запись Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="13007-207">When you issue the **compile** command, the U-SQL script is sent to your Data Lake Analytics account.</span></span> <span data-ttu-id="13007-208">Позже Visual Studio Code получит результат компилирования.</span><span class="sxs-lookup"><span data-stu-id="13007-208">Later, Visual Studio Code receives the compilation result.</span></span> <span data-ttu-id="13007-209">Из-за удаленной компиляции нужно внести в файл конфигурации сведения, которые позволят Visual Studio Code подключиться к учетной записи Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="13007-209">Due to the remote compilation, Visual Studio Code requires that you list the information to connect to your Data Lake Analytics account in the configuration file.</span></span>

<span data-ttu-id="13007-210">**Компиляция скрипта U-SQL**</span><span class="sxs-lookup"><span data-stu-id="13007-210">**To compile a U-SQL script**</span></span>

1. <span data-ttu-id="13007-211">Нажмите клавиши CTRL+SHIFT+P, чтобы открыть палитру команд.</span><span class="sxs-lookup"><span data-stu-id="13007-211">Select Ctrl+Shift+P to open the command palette.</span></span> 
2. <span data-ttu-id="13007-212">Введите **ADL: Compile Script**.</span><span class="sxs-lookup"><span data-stu-id="13007-212">Enter **ADL: Compile Script**.</span></span> <span data-ttu-id="13007-213">Результаты компиляции отображаются в окне **Вывод**.</span><span class="sxs-lookup"><span data-stu-id="13007-213">The compile results appear in the **Output** window.</span></span> <span data-ttu-id="13007-214">Чтобы запустить компиляцию задания U-SQL можно также щелкнуть правой кнопкой мыши файл скрипта и выбрать **ADL: Compile Script**.</span><span class="sxs-lookup"><span data-stu-id="13007-214">You can also right-click a script file, and then select **ADL: Compile Script** to compile a U-SQL job.</span></span> <span data-ttu-id="13007-215">Результат компиляции отобразится в области **Вывод**.</span><span class="sxs-lookup"><span data-stu-id="13007-215">The compilation result appears in the **Output** pane.</span></span>
 

<span data-ttu-id="13007-216">**Отправка скрипта U-SQL**</span><span class="sxs-lookup"><span data-stu-id="13007-216">**To submit a U-SQL script**</span></span>

1. <span data-ttu-id="13007-217">Нажмите клавиши CTRL+SHIFT+P, чтобы открыть палитру команд.</span><span class="sxs-lookup"><span data-stu-id="13007-217">Select Ctrl+Shift+P to open the command palette.</span></span> 
2. <span data-ttu-id="13007-218">Введите **ADL: Submit Job**.</span><span class="sxs-lookup"><span data-stu-id="13007-218">Enter **ADL: Submit Job**.</span></span>  <span data-ttu-id="13007-219">Также можно щелкнуть правой кнопкой мыши файл скрипта и выбрать **ADL: Submit Job**.</span><span class="sxs-lookup"><span data-stu-id="13007-219">You can also right-click a script file, and then select **ADL: Submit Job**.</span></span> 

<span data-ttu-id="13007-220">После отправки задания U-SQL отобразятся журналы отправки в окне **Вывод** в VS Code.</span><span class="sxs-lookup"><span data-stu-id="13007-220">After you submit a U-SQL job, the submission logs appear in the **Output** window in VS Code.</span></span> <span data-ttu-id="13007-221">Если отправка пройдет успешно, отобразится URL-адрес задания.</span><span class="sxs-lookup"><span data-stu-id="13007-221">If the submission is successful, the job URL appears as well.</span></span> <span data-ttu-id="13007-222">URL-адрес задания можно открыть в веб-браузере, чтобы отслеживать состояние задания в реальном времени.</span><span class="sxs-lookup"><span data-stu-id="13007-222">You can open the job URL in a web browser to track the real-time job status.</span></span>

<span data-ttu-id="13007-223">Чтобы включить вывод сведений о задании, задайте **jobInformationOutputPath** в файле **vs code for the u-sql_settings.json**.</span><span class="sxs-lookup"><span data-stu-id="13007-223">To enable the output of the job details, set **jobInformationOutputPath** in the **vs code for the u-sql_settings.json** file.</span></span>
 
## <a name="use-a-code-behind-file"></a><span data-ttu-id="13007-224">Использование файла с выделенным кодом</span><span class="sxs-lookup"><span data-stu-id="13007-224">Use a code-behind file</span></span>

<span data-ttu-id="13007-225">Файл с выделенным кодом является файлом C#, который связан с одним скриптом U-SQL.</span><span class="sxs-lookup"><span data-stu-id="13007-225">A code-behind file is a C# file associated with a single U-SQL script.</span></span> <span data-ttu-id="13007-226">В файле с выделенным кодом можно определить скрипт, который относится к UDO, UDA, UDT и UDF.</span><span class="sxs-lookup"><span data-stu-id="13007-226">You can define a script dedicated to UDO, UDA, UDT, and UDF in the code-behind file.</span></span> <span data-ttu-id="13007-227">Все эти объекты можно будет напрямую использовать в скрипте, не регистрируя для них сборку.</span><span class="sxs-lookup"><span data-stu-id="13007-227">The UDO, UDA, UDT, and UDF can be used directly in the script without registering the assembly first.</span></span> <span data-ttu-id="13007-228">Файл с выделенным кодом помещается в ту же папку, что и связанный с ним файл скрипта U-SQL.</span><span class="sxs-lookup"><span data-stu-id="13007-228">The code-behind file is put in the same folder as its peering U-SQL script file.</span></span> <span data-ttu-id="13007-229">Например, для скрипта с именем xxx.usql, файл Code Behind будет иметь имя xxx.usql.cs.</span><span class="sxs-lookup"><span data-stu-id="13007-229">If the script is named xxx.usql, the code-behind is named as xxx.usql.cs.</span></span> <span data-ttu-id="13007-230">Если вручную удалить файл с выделенным кодом, функция выделенного кода будет отключена для связанного с ним скрипта U-SQL.</span><span class="sxs-lookup"><span data-stu-id="13007-230">If you manually delete the code-behind file, the code-behind feature is disabled for its associated U-SQL script.</span></span> <span data-ttu-id="13007-231">Дополнительные сведения о написании пользовательского кода для скриптов U-SQL можно найти в записи блога [Writing and Using Custom Code in U-SQL – User-Defined Functions]( https://blogs.msdn.microsoft.com/visualstudio/2015/10/28/writing-and-using-custom-code-in-u-sql-user-defined-functions/) (Написание и использование пользовательского кода в U-SQL — определяемые пользователем функции).</span><span class="sxs-lookup"><span data-stu-id="13007-231">For more information about writing customer code for U-SQL script, see [Writing and Using Custom Code in U-SQL: User-Defined Functions]( https://blogs.msdn.microsoft.com/visualstudio/2015/10/28/writing-and-using-custom-code-in-u-sql-user-defined-functions/).</span></span>

<span data-ttu-id="13007-232">Для поддержки выделенного кода необходимо открыть рабочую папку.</span><span class="sxs-lookup"><span data-stu-id="13007-232">To support code-behind, you must open a working folder.</span></span> 

<span data-ttu-id="13007-233">**Создание файла Code Behind**</span><span class="sxs-lookup"><span data-stu-id="13007-233">**To generate a code-behind file**</span></span>

1. <span data-ttu-id="13007-234">Откройте исходный файл.</span><span class="sxs-lookup"><span data-stu-id="13007-234">Open a source file.</span></span> 
2. <span data-ttu-id="13007-235">Нажмите клавиши CTRL+SHIFT+P, чтобы открыть палитру команд.</span><span class="sxs-lookup"><span data-stu-id="13007-235">Select Ctrl+Shift+P to open the command palette.</span></span>
3. <span data-ttu-id="13007-236">Введите **ADL: Generate Code Behind**.</span><span class="sxs-lookup"><span data-stu-id="13007-236">Enter **ADL: Generate Code Behind**.</span></span> <span data-ttu-id="13007-237">Файл Code Behind будет создан в той же папке.</span><span class="sxs-lookup"><span data-stu-id="13007-237">A code-behind file is created in the same folder.</span></span> 

<span data-ttu-id="13007-238">Также можно щелкнуть правой кнопкой мыши файл скрипта и выбрать **ADL: Generate Code Behind**.</span><span class="sxs-lookup"><span data-stu-id="13007-238">You can also right-click a script file, and then select **ADL: Generate Code Behind**.</span></span> 

<span data-ttu-id="13007-239">Компиляция и отправка скрипта U-SQL с помощью файла с выделенным кодом выполняется так же, как и для автономного файла скрипта U-SQL.</span><span class="sxs-lookup"><span data-stu-id="13007-239">To compile and submit a U-SQL script with a code-behind file is the same as with the standalone U-SQL script file.</span></span>

<span data-ttu-id="13007-240">Следующие два снимка экрана демонстрируют файл Code Behind и связанный с ним файл скрипта U-SQL.</span><span class="sxs-lookup"><span data-stu-id="13007-240">The following two screenshots show a code-behind file and its associated U-SQL script file:</span></span>
 
![Код программной части в средствах Data Lake для Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-code-behind.png)

![Файл скрипта кода программной части в средствах Data Lake для Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-code-behind-call.png) 

## <a name="use-assemblies"></a><span data-ttu-id="13007-243">Использование сборок</span><span class="sxs-lookup"><span data-stu-id="13007-243">Use assemblies</span></span>

<span data-ttu-id="13007-244">Дополнительные сведения о разработке сборок см. в статье [Разработка сборок U-SQL для заданий Azure Data Lake Analytics](data-lake-analytics-u-sql-develop-assemblies.md).</span><span class="sxs-lookup"><span data-stu-id="13007-244">For information on developing assemblies, see [Develop U-SQL assemblies for Azure Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-assemblies.md).</span></span>

<span data-ttu-id="13007-245">Средства Data Lake можно использовать для регистрации сборки пользовательского кода в каталоге Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="13007-245">You can use Data Lake Tools to register custom code assemblies in the Data Lake Analytics catalog.</span></span>

<span data-ttu-id="13007-246">**Регистрация сборки**</span><span class="sxs-lookup"><span data-stu-id="13007-246">**To register an assembly**</span></span>

<span data-ttu-id="13007-247">Зарегистрировать сборку можно с помощью команд **ADL: Register Assembly** или **ADL: Register Assembly through Configuration**.</span><span class="sxs-lookup"><span data-stu-id="13007-247">You can register the assembly through the **ADL: Register Assembly** or **ADL: Register Assembly through Configuration** commands.</span></span>

<span data-ttu-id="13007-248">**Для регистрации с помощью команды ADL: Register Assembly**</span><span class="sxs-lookup"><span data-stu-id="13007-248">**To register through the ADL: Register Assembly command**</span></span>
1.  <span data-ttu-id="13007-249">Нажмите клавиши CTRL+SHIFT+P, чтобы открыть палитру команд.</span><span class="sxs-lookup"><span data-stu-id="13007-249">Select Ctrl+Shift+P to open the command palette.</span></span>
2.  <span data-ttu-id="13007-250">Введите **ADL: Register Assembly**.</span><span class="sxs-lookup"><span data-stu-id="13007-250">Enter **ADL: Register Assembly**.</span></span> 
3.  <span data-ttu-id="13007-251">Укажите локальный путь к сборке.</span><span class="sxs-lookup"><span data-stu-id="13007-251">Specify the local assembly path.</span></span> 
4.  <span data-ttu-id="13007-252">Выберите учетную запись Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="13007-252">Select a Data Lake Analytics account.</span></span>
5.  <span data-ttu-id="13007-253">Выберите базу данных.</span><span class="sxs-lookup"><span data-stu-id="13007-253">Select a database.</span></span>

<span data-ttu-id="13007-254">Результат: портал откроется в браузере и отобразит процесс регистрации сборки.</span><span class="sxs-lookup"><span data-stu-id="13007-254">Results: The portal is opened in a browser and displays the assembly registration process.</span></span>  

<span data-ttu-id="13007-255">Еще один удобный способ запуска команды **ADL: Register Assembly** — щелкнуть правой кнопкой мыши DLL-файл в Проводнике.</span><span class="sxs-lookup"><span data-stu-id="13007-255">Another convenient way to trigger the **ADL: Register Assembly** command is to right-click the .dll file in File Explorer.</span></span> 

<span data-ttu-id="13007-256">**Для регистрации с помощью команды ADL: Register Assembly through Configuration**</span><span class="sxs-lookup"><span data-stu-id="13007-256">**To register though the ADL: Register Assembly through Configuration command**</span></span>
1.  <span data-ttu-id="13007-257">Нажмите клавиши CTRL+SHIFT+P, чтобы открыть палитру команд.</span><span class="sxs-lookup"><span data-stu-id="13007-257">Select Ctrl+Shift+P to open the command palette.</span></span>
2.  <span data-ttu-id="13007-258">Введите **ADL: Register Assembly through Configuration**.</span><span class="sxs-lookup"><span data-stu-id="13007-258">Enter **ADL: Register Assembly through Configuration**.</span></span> 
3.  <span data-ttu-id="13007-259">Укажите локальный путь к сборке.</span><span class="sxs-lookup"><span data-stu-id="13007-259">Specify the local assembly path.</span></span> 
4.  <span data-ttu-id="13007-260">Отобразится JSON-файл.</span><span class="sxs-lookup"><span data-stu-id="13007-260">The JSON file is displayed.</span></span> <span data-ttu-id="13007-261">Просмотрите и при необходимости измените зависимости сборки и параметры ресурсов.</span><span class="sxs-lookup"><span data-stu-id="13007-261">Review and edit the assembly dependencies and resource parameters, if needed.</span></span> <span data-ttu-id="13007-262">Инструкции отображаются в окне **Вывод**.</span><span class="sxs-lookup"><span data-stu-id="13007-262">Instructions are displayed in the **Output** window.</span></span> <span data-ttu-id="13007-263">Чтобы перейти к регистрации сборки, сохраните (CTRL+S) JSON-файл.</span><span class="sxs-lookup"><span data-stu-id="13007-263">To proceed to the assembly registration, save (Ctrl+S) the JSON file.</span></span>

![Код программной части в средствах Data Lake для Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-register-assembly-advance.png)
>[!NOTE]
>- <span data-ttu-id="13007-265">Зависимости сборки. Средства Azure Data Lake автоматически определяют наличие любых зависимостей в библиотеке DLL.</span><span class="sxs-lookup"><span data-stu-id="13007-265">Assembly dependencies: Azure Data Lake Tools autodetects whether the DLL has any dependencies.</span></span> <span data-ttu-id="13007-266">После обнаружения зависимости отображаются в JSON-файле.</span><span class="sxs-lookup"><span data-stu-id="13007-266">The dependencies are displayed in the JSON file after they are detected.</span></span> 
>- <span data-ttu-id="13007-267">Ресурсы. Ресурсы DLL (например, TXT, PNG и CSV) можно отправить как часть регистрации сборки.</span><span class="sxs-lookup"><span data-stu-id="13007-267">Resources: You can upload your DLL resources (for example, .txt, .png, and .csv) as part of the assembly registration.</span></span> 

<span data-ttu-id="13007-268">Еще один удобный способ запуска команды **ADL: Register Assembly through Configuration** — щелкнуть правой кнопкой мыши DLL-файл в Проводнике.</span><span class="sxs-lookup"><span data-stu-id="13007-268">Another way to trigger the **ADL: Register Assembly through Configuration** command is to right-click the .dll file in File Explorer.</span></span> 

<span data-ttu-id="13007-269">В приведенном ниже коде U-SQL показано, как вызвать сборку.</span><span class="sxs-lookup"><span data-stu-id="13007-269">The following U-SQL code demonstrates how to call an assembly.</span></span> <span data-ttu-id="13007-270">В этом примере имя сборки — *test*.</span><span class="sxs-lookup"><span data-stu-id="13007-270">In the sample, the assembly name is *test*.</span></span>

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
    TO @"Sample/SearchLogtest.txt" 
    USING Outputters.Tsv();
```


## <a name="access-the-data-lake-analytics-catalog"></a><span data-ttu-id="13007-271">Доступ к каталогу Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="13007-271">Access the Data Lake Analytics catalog</span></span>

<span data-ttu-id="13007-272">После подключения к Azure можно получить доступ к каталогу U-SQL, выполнив следующие действия.</span><span class="sxs-lookup"><span data-stu-id="13007-272">After you have connected to Azure, you can use the following steps to access the U-SQL catalog.</span></span>

<span data-ttu-id="13007-273">**Доступ к метаданным Azure Data Lake Analytics**</span><span class="sxs-lookup"><span data-stu-id="13007-273">**To access the Azure Data Lake Analytics metadata**</span></span>

1.  <span data-ttu-id="13007-274">Нажмите клавиши CTRL+SHIFT+P, а затем введите **ADL: List Tables**.</span><span class="sxs-lookup"><span data-stu-id="13007-274">Select Ctrl+Shift+P, and then enter **ADL: List Tables**.</span></span>
2.  <span data-ttu-id="13007-275">Выберите одну из учетных записей Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="13007-275">Select one of the Data Lake Analytics accounts.</span></span>
3.  <span data-ttu-id="13007-276">Выберите одну из баз данных Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="13007-276">Select one of the Data Lake Analytics databases.</span></span>
4.  <span data-ttu-id="13007-277">Выберите одну из схем.</span><span class="sxs-lookup"><span data-stu-id="13007-277">Select one of the schemas.</span></span> <span data-ttu-id="13007-278">Можно просмотреть список таблиц.</span><span class="sxs-lookup"><span data-stu-id="13007-278">You can see the list of tables.</span></span>

## <a name="view-data-lake-analytics-jobs"></a><span data-ttu-id="13007-279">Просмотр заданий Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="13007-279">View Data Lake Analytics jobs</span></span>

<span data-ttu-id="13007-280">**Просмотр заданий Data Lake Analytics**</span><span class="sxs-lookup"><span data-stu-id="13007-280">**To view Data Lake Analytics jobs**</span></span>
1.  <span data-ttu-id="13007-281">Откройте палитру команд (CTRL+SHIFT+P) и выберите **ADL: Show Job**.</span><span class="sxs-lookup"><span data-stu-id="13007-281">Open the command palette (Ctrl+Shift+P) and select **ADL: Show Job**.</span></span> 
2.  <span data-ttu-id="13007-282">Выберите Data Lake Analytics или локальную учетную запись.</span><span class="sxs-lookup"><span data-stu-id="13007-282">Select a Data Lake Analytics or local account.</span></span> 
3.  <span data-ttu-id="13007-283">Подождите, пока отобразится список заданий для учетной записи.</span><span class="sxs-lookup"><span data-stu-id="13007-283">Wait for the jobs list for the account to appear.</span></span>
4.  <span data-ttu-id="13007-284">Выберите задание из списка заданий. Средства Data Lake отобразят сведения о задании на портале Azure и откроют файл JobInfo в VS Code.</span><span class="sxs-lookup"><span data-stu-id="13007-284">Select a job from job list, Data Lake Tools opens the job details in the Azure portal and displays the JobInfo file in VS Code.</span></span>

![Типы объектов IntelliSencse в средствах Data Lake для Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-show-job.png)

## <a name="azure-data-lake-storage-integration"></a><span data-ttu-id="13007-286">Интеграция с Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="13007-286">Azure Data Lake Storage integration</span></span>

<span data-ttu-id="13007-287">Связанные с Azure Data Lake Store команды можно использовать для:</span><span class="sxs-lookup"><span data-stu-id="13007-287">You can use Azure Data Lake Storage-related commands to:</span></span>
 - <span data-ttu-id="13007-288">просмотра ресурсов Azure Data Lake Storage;</span><span class="sxs-lookup"><span data-stu-id="13007-288">Browse through the Azure Data Lake Storage resources.</span></span> 
 - <span data-ttu-id="13007-289">предварительного просмотра файла Azure Data Lake Storage;</span><span class="sxs-lookup"><span data-stu-id="13007-289">Preview the Azure Data Lake Storage file.</span></span>  
 - <span data-ttu-id="13007-290">отправки файла напрямую в Azure Data Lake Store в VS Code.</span><span class="sxs-lookup"><span data-stu-id="13007-290">Upload the file directly to Azure Data Lake Storage in VS Code.</span></span> 

### <a name="list-the-storage-path"></a><span data-ttu-id="13007-291">Вывод пути к хранилищу</span><span class="sxs-lookup"><span data-stu-id="13007-291">List the storage path</span></span> 
<span data-ttu-id="13007-292">Путь к хранилищу можно вывести с помощью палитры команд или щелчка правой кнопкой мыши.</span><span class="sxs-lookup"><span data-stu-id="13007-292">You can list the storage path through the command palette or through right-click.</span></span>

<span data-ttu-id="13007-293">**Вывод пути к хранилищу через палитру команд**</span><span class="sxs-lookup"><span data-stu-id="13007-293">**To list the storage path through the command palette**</span></span>

1.  <span data-ttu-id="13007-294">Откройте палитру команд (CTRL+SHIFT+P) и введите **ADL: List Storage Path**.</span><span class="sxs-lookup"><span data-stu-id="13007-294">Open the command palette (Ctrl+Shift+P) and enter **ADL: List Storage Path**.</span></span>

    ![Вывод пути к хранилищу в средствах Data Lake для Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-storage.png)

2.  <span data-ttu-id="13007-296">Выберите предпочтительный способ вывода пути к хранилищу.</span><span class="sxs-lookup"><span data-stu-id="13007-296">Select your preferred way for listing the storage path.</span></span> <span data-ttu-id="13007-297">В этом примере выбран вариант **Enter a path** (Введите путь).</span><span class="sxs-lookup"><span data-stu-id="13007-297">This passage uses **Enter a path** as an example.</span></span>

    ![Data Lake Tools для Visual Studio Code: один из способов вывода пути к хранилищу](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account-selectoneway.png)

    > [!NOTE]
    >- <span data-ttu-id="13007-299">VS Code сохраняет последний посещенный путь в каждой учетной записи Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="13007-299">VS Code keeps the last-visited path in every Data Lake Analytics account.</span></span> <span data-ttu-id="13007-300">Например, /tt/ss.</span><span class="sxs-lookup"><span data-stu-id="13007-300">For example: /tt/ss.</span></span>
    >- <span data-ttu-id="13007-301">Просмотр из корневого пути: вывод корневого пути из выбранной учетной записи Azure Data Lake Analytics или локального пути.</span><span class="sxs-lookup"><span data-stu-id="13007-301">Browser from root path: The list root path from your selected Data Lake Analytics account or a local path.</span></span>
    >- <span data-ttu-id="13007-302">Введите путь: вывод указанного пути из выбранной учетной записи Azure Data Lake Analytics или локального пути.</span><span class="sxs-lookup"><span data-stu-id="13007-302">Enter a path: List a specified path from your selected Data Lake Analytics account or a local path.</span></span>
    
3. <span data-ttu-id="13007-303">Выберите локальную учетную запись или учетную запись Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="13007-303">Select an account from the local path or a Data Lake Analytics account.</span></span>

    ![Средства Data Lake для Visual Studio Code: выбор дополнительных учетных записей](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

4. <span data-ttu-id="13007-305">Выберите **дополнительно**, чтобы перечислить дополнительные учетные записи Data Lake Analytics, а затем выберите учетную запись Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="13007-305">Select **more** to list more Data Lake Analytics accounts, and then select a Data Lake Analytics account.</span></span>

    ![Средства Data Lake для Visual Studio Code: выбор учетной записи](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-select-adla-account.png)

5.  <span data-ttu-id="13007-307">Введите путь к хранилищу Azure.</span><span class="sxs-lookup"><span data-stu-id="13007-307">Enter an Azure storage path.</span></span> <span data-ttu-id="13007-308">Например, /output.</span><span class="sxs-lookup"><span data-stu-id="13007-308">For example, /output.</span></span>

    ![Ввод пути к хранилищу в средствах Data Lake для Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-input-path.png)

6.  <span data-ttu-id="13007-310">Результат: в палитре команд выводятся сведения о пути в соответствии с записями.</span><span class="sxs-lookup"><span data-stu-id="13007-310">Results: The command palette lists the path information based on your entries.</span></span>

    ![Результат вывода пути к хранилищу в средствах Data Lake для Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-path.png)

<span data-ttu-id="13007-312">Более удобный способ вывода относительного пути — открыть контекстное меню.</span><span class="sxs-lookup"><span data-stu-id="13007-312">A more convenient way to list the relative path is through the right-click context menu.</span></span>

<span data-ttu-id="13007-313">**Вывод пути к хранилищу с помощью щелчка правой кнопкой мыши**</span><span class="sxs-lookup"><span data-stu-id="13007-313">**To list the storage path through right-click**</span></span>

1.  <span data-ttu-id="13007-314">Щелкните строку пути правой кнопкой мыши и выберите **List Storage Path** (Вывод пути к хранилищу).</span><span class="sxs-lookup"><span data-stu-id="13007-314">Right-click the path string to select **List Storage Path**.</span></span>

       ![Контекстное меню в средствах Data Lake для Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-right-click-path.png)

2. <span data-ttu-id="13007-316">Выбранный относительный путь отобразится в палитре команд.</span><span class="sxs-lookup"><span data-stu-id="13007-316">The selected relative path appears in the command palette.</span></span>

   ![Выбранный относительный путь средств Data Lake для Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-relative-path.png)

3.  <span data-ttu-id="13007-318">Выберите локальную учетную запись или учетную запись Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="13007-318">Select an account from the local path or a Data Lake Analytics account.</span></span>

       ![Средства Data Lake для Visual Studio Code: выбор учетной записи](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

4.  <span data-ttu-id="13007-320">Результат: в палитре команд будет выведен список папок и файлов, находящихся по текущему пути.</span><span class="sxs-lookup"><span data-stu-id="13007-320">Results: The command palette lists the folders and files for the current path.</span></span>

       ![Вывод из текущего пути в средствах Data Lake для Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-current.png)

### <a name="preview-the-storage-file"></a><span data-ttu-id="13007-322">Предварительный просмотр файла хранилища</span><span class="sxs-lookup"><span data-stu-id="13007-322">Preview the storage file</span></span>
<span data-ttu-id="13007-323">Файл хранилища можно предварительно просмотреть через палитру команд или с помощью щелчка правой кнопкой мыши.</span><span class="sxs-lookup"><span data-stu-id="13007-323">You can preview the storage file through the command palette or through right-click.</span></span>

<span data-ttu-id="13007-324">**Просмотр файла хранилища с помощью палитры команды**</span><span class="sxs-lookup"><span data-stu-id="13007-324">**To preview the storage file through the command palette**</span></span>

1.  <span data-ttu-id="13007-325">Откройте палитру команд (CTRL+SHIFT+P) и введите **ADL: Preview Storage File**.</span><span class="sxs-lookup"><span data-stu-id="13007-325">Open the command palette (Ctrl+Shift+P) and enter **ADL: Preview Storage File**.</span></span>

       ![Предварительный просмотр файла хранилища в средствах Data Lake для Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-preview.png)

2.  <span data-ttu-id="13007-327">Выберите локальную учетную запись или учетную запись Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="13007-327">Select an account from the local path or a Data Lake Analytics account.</span></span>

       ![Список учетных данных в средствах Data Lake для Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

3.  <span data-ttu-id="13007-329">Выберите **дополнительно**, чтобы перечислить дополнительные учетные записи Data Lake Analytics, а затем выберите учетную запись Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="13007-329">Select **more** to list more Data Lake Analytics accounts, and then select a Data Lake Analytics account.</span></span>

       ![Средства Data Lake для Visual Studio Code: выбор учетной записи](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-select-adla-account.png)

4.  <span data-ttu-id="13007-331">Введите путь к хранилищу или имя файла хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="13007-331">Enter an Azure storage path or file.</span></span> <span data-ttu-id="13007-332">Например, /output/SearchLog.txt.</span><span class="sxs-lookup"><span data-stu-id="13007-332">For example, /output/SearchLog.txt.</span></span>

       ![Ввод пути к хранилищу и имени файла хранилища в средствах Data Lake для Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-input-preview-file.png)

5.  <span data-ttu-id="13007-334">Результат: в палитре команд выводятся сведения о пути в соответствии с записями.</span><span class="sxs-lookup"><span data-stu-id="13007-334">Results: The command palette lists the path information based on your entries.</span></span>

       ![Результат предварительного просмотра файла в Средствах Data Lake для Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-preview-results.png)

<span data-ttu-id="13007-336">**Вывод пути к хранилищу с помощью щелчка правой кнопкой мыши**</span><span class="sxs-lookup"><span data-stu-id="13007-336">**To list the storage path through right-click**</span></span>

1.  <span data-ttu-id="13007-337">Чтобы просмотреть файл, щелкните правой кнопкой мыши путь к файлу.</span><span class="sxs-lookup"><span data-stu-id="13007-337">To preview a file, right-click the file path.</span></span>

   ![Контекстное меню в средствах Data Lake для Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-right-click-preview.png) 

2.  <span data-ttu-id="13007-339">Выберите локальную учетную запись или учетную запись Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="13007-339">Select an account from the local path or a Data Lake Analytics account.</span></span>

       ![Средства Data Lake для Visual Studio Code: выбор учетной записи](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

3.  <span data-ttu-id="13007-341">Результат: в VS Code отобразятся результаты предварительного просмотра файла.</span><span class="sxs-lookup"><span data-stu-id="13007-341">Results: VS Code displays the preview results of the file.</span></span>

       ![Результат предварительного просмотра файла в Средствах Data Lake для Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-preview-results.png)

### <a name="upload-a-file"></a><span data-ttu-id="13007-343">Отправить файл.</span><span class="sxs-lookup"><span data-stu-id="13007-343">Upload a file</span></span> 

<span data-ttu-id="13007-344">Файлы можно отправить с помощью команд **ADL: Upload File** и **ADL: Upload File through Configuration**.</span><span class="sxs-lookup"><span data-stu-id="13007-344">You can upload files by entering the commands **ADL: Upload File** or **ADL: Upload File through Configuration**.</span></span>

<span data-ttu-id="13007-345">**Отправка файлов с помощью команды ADL: Upload File**</span><span class="sxs-lookup"><span data-stu-id="13007-345">**To upload files though the ADL: Upload File command**</span></span>
1. <span data-ttu-id="13007-346">Нажмите клавиши CTRL+SHIFT+P, чтобы открыть палитру команд, или щелкните правой кнопкой мыши в редакторе скриптов, а затем введите **Upload File**.</span><span class="sxs-lookup"><span data-stu-id="13007-346">Select Ctrl+Shift+P to open the command palette or right-click the script editor, and then enter **Upload File**.</span></span>
2.  <span data-ttu-id="13007-347">Чтобы отправить файл, введите локальный путь.</span><span class="sxs-lookup"><span data-stu-id="13007-347">To upload the file, enter a local path.</span></span>

    ![Ввод локального пути в средствах Data Lake для Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-auto-input-local-path.png)

3. <span data-ttu-id="13007-349">Выберите один из способов вывода списка путей к хранилищу.</span><span class="sxs-lookup"><span data-stu-id="13007-349">Select one of the ways of listing the storage path.</span></span> <span data-ttu-id="13007-350">В этом примере выбран вариант **Enter a path** (Введите путь).</span><span class="sxs-lookup"><span data-stu-id="13007-350">This passage uses **Enter a path** as an example.</span></span>

    ![Вывод пути к хранилищу в средствах Data Lake для Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account-selectoneway.png)
    >[!NOTE]
    >- <span data-ttu-id="13007-352">VS Code сохраняет последний посещенный путь в каждой учетной записи Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="13007-352">VS Code keeps the last-visited path in every Data Lake Analytics account.</span></span> <span data-ttu-id="13007-353">Например, /tt/ss.</span><span class="sxs-lookup"><span data-stu-id="13007-353">For example: /tt/ss.</span></span>
    >- <span data-ttu-id="13007-354">Просмотр из корневого пути: вывод корневого пути из выбранной учетной записи Azure Data Lake Analytics или локального пути.</span><span class="sxs-lookup"><span data-stu-id="13007-354">Browser from root path: The list root path from your selected Data Lake Analytics account or a local path.</span></span>
    >- <span data-ttu-id="13007-355">Введите путь: вывод указанного пути из выбранной учетной записи Azure Data Lake Analytics или локального пути.</span><span class="sxs-lookup"><span data-stu-id="13007-355">Enter a path: List a specified path from your selected Data Lake Analytics account or a local path.</span></span>

4. <span data-ttu-id="13007-356">Выберите локальную учетную запись или учетную запись Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="13007-356">Select an account from the local path or a Data Lake Analytics account.</span></span>

    ![Контекстное меню хранилища в средствах Data Lake для Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

5. <span data-ttu-id="13007-358">Введите путь к хранилищу Azure.</span><span class="sxs-lookup"><span data-stu-id="13007-358">Enter an Azure storage path.</span></span> <span data-ttu-id="13007-359">Например, /output.</span><span class="sxs-lookup"><span data-stu-id="13007-359">For example: /output.</span></span>

       ![Data Lake Tools for Visual Studio Code enter storage path](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-input-preview-file.png)

6. <span data-ttu-id="13007-360">Найдите путь к хранилищу Azure.</span><span class="sxs-lookup"><span data-stu-id="13007-360">Find your Azure storage path.</span></span> <span data-ttu-id="13007-361">Выберите пункт **Choose current folder** (Выбрать текущую папку).</span><span class="sxs-lookup"><span data-stu-id="13007-361">Select **Choose current folder**.</span></span>

    ![Выбор папки в средствах Data Lake для Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-choose-current-folder.png)

7.  <span data-ttu-id="13007-363">Результат: в окне **Вывод** отобразится состояние отправки файла.</span><span class="sxs-lookup"><span data-stu-id="13007-363">Results: The **Output** window displays the file upload status.</span></span>

       ![Состояние отправки в средствах Data Lake для Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-upload-status.png)    

<span data-ttu-id="13007-365">**Отправка файлов с помощью команды ADL: Upload File through Configuration**</span><span class="sxs-lookup"><span data-stu-id="13007-365">**To upload files though the ADL: Upload File through Configuration command**</span></span>
1.  <span data-ttu-id="13007-366">Нажмите клавиши CTRL+SHIFT+P, чтобы открыть палитру команд, или щелкните правой кнопкой мыши в редакторе скриптов, а затем введите **Upload File through Configuration**.</span><span class="sxs-lookup"><span data-stu-id="13007-366">Select Ctrl+Shift+P to open the command palette or right-click the script editor, and then enter **Upload File through Configuration**.</span></span>
2.  <span data-ttu-id="13007-367">В VS Code отобразится JSON-файл.</span><span class="sxs-lookup"><span data-stu-id="13007-367">VS Code displays a JSON file.</span></span> <span data-ttu-id="13007-368">Вы можете ввести сразу несколько путей к файлам, чтобы отправить несколько файлов.</span><span class="sxs-lookup"><span data-stu-id="13007-368">You can enter file paths and upload multiple files at the same time.</span></span> <span data-ttu-id="13007-369">Инструкции отображаются в окне **Вывод**.</span><span class="sxs-lookup"><span data-stu-id="13007-369">Instructions are displayed in the **Output** window.</span></span> <span data-ttu-id="13007-370">Чтобы продолжить отправку файла, сохраните (CTRL+S) JSON-файл.</span><span class="sxs-lookup"><span data-stu-id="13007-370">To proceed to upload the file, save (Ctrl+S) the JSON file.</span></span>

       ![Путь к файлу в средствах Data Lake для Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-upload-file.png)

3.  <span data-ttu-id="13007-372">Результат: в окне **Вывод** отобразится состояние отправки файла.</span><span class="sxs-lookup"><span data-stu-id="13007-372">Results: The **Output** window displays the file upload status.</span></span>

       ![Состояние отправки в средствах Data Lake для Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-upload-status.png)     

<span data-ttu-id="13007-374">Еще один способ отправки файла в хранилище — открыть контекстное меню полного или относительного пути к файлу в редакторе скриптов.</span><span class="sxs-lookup"><span data-stu-id="13007-374">Another way to upload a file to storage is through the right-click menu on the file's full path or the file's relative path in the script editor.</span></span> <span data-ttu-id="13007-375">Введите локальный путь к файлу, а затем выберите учетную запись.</span><span class="sxs-lookup"><span data-stu-id="13007-375">Enter the local file path, and then select the account.</span></span> <span data-ttu-id="13007-376">В окне **Вывод** отобразится состояние отправки.</span><span class="sxs-lookup"><span data-stu-id="13007-376">The **Output** window displays the upload status.</span></span> 

### <a name="open-azure-storage-explorer"></a><span data-ttu-id="13007-377">Открытие обозревателя хранилищ Azure</span><span class="sxs-lookup"><span data-stu-id="13007-377">Open Azure Storage Explorer</span></span>
<span data-ttu-id="13007-378">Вы можете открыть **обозреватель хранилищ Azure**, введя команду **ADL: Open Web Azure Storage Explorer** или выбрав ее в контекстном меню.</span><span class="sxs-lookup"><span data-stu-id="13007-378">You can open **Azure Storage Explorer** by entering the command **ADL: Open Web Azure Storage Explorer** or by selecting it from the right-click context menu.</span></span>

<span data-ttu-id="13007-379">**Открытие обозревателя хранилищ Azure**</span><span class="sxs-lookup"><span data-stu-id="13007-379">**To open Azure Storage Explorer**</span></span>

1. <span data-ttu-id="13007-380">Нажмите клавиши CTRL+SHIFT+P, чтобы открыть палитру команд.</span><span class="sxs-lookup"><span data-stu-id="13007-380">Select Ctrl+Shift+P to open the command palette.</span></span>
2. <span data-ttu-id="13007-381">Введите команду **Open Web Azure Storage Explorer** или щелкните правой кнопкой мыши относительный либо полный путь в редакторе скриптов, а затем выберите **Open Web Azure Storage Explorer** (Открыть обозреватель веб-хранилищ Azure).</span><span class="sxs-lookup"><span data-stu-id="13007-381">Enter **Open Web Azure Storage Explorer** or right-click on a relative path or the full path in the script editor, and then select **Open Web Azure Storage Explorer**.</span></span>
3. <span data-ttu-id="13007-382">Выберите учетную запись Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="13007-382">Select a Data Lake Analytics account.</span></span>

<span data-ttu-id="13007-383">Средства Data Lake откроют путь к хранилищу Azure на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="13007-383">Data Lake Tools opens the Azure storage path in the Azure portal.</span></span> <span data-ttu-id="13007-384">Можно найти путь и предварительно просмотреть файл в Интернете.</span><span class="sxs-lookup"><span data-stu-id="13007-384">You can find the path and preview the file from the web.</span></span>

### <a name="local-run-and-local-debug-for-windows-users"></a><span data-ttu-id="13007-385">Локальное выполнение и локальная отладка для пользователей Windows</span><span class="sxs-lookup"><span data-stu-id="13007-385">Local run and local debug for Windows users</span></span>
<span data-ttu-id="13007-386">Локальное выполнение U-SQL тестирует локальные данные и проверяет скрипт локально перед публикацией кода в Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="13007-386">U-SQL local run tests your local data and validates your script locally, before your code is published to Data Lake Analytics.</span></span> <span data-ttu-id="13007-387">Функция локальной отладки позволяет завершить следующие задачи перед отправкой кода в Data Lake Analytics:</span><span class="sxs-lookup"><span data-stu-id="13007-387">The local debug feature enables you to complete the following tasks before your code is submitted to Data Lake Analytics:</span></span> 
- <span data-ttu-id="13007-388">Отладка кода программной части C#.</span><span class="sxs-lookup"><span data-stu-id="13007-388">Debug your C# code-behind.</span></span> 
- <span data-ttu-id="13007-389">Пошаговая отладка кода.</span><span class="sxs-lookup"><span data-stu-id="13007-389">Step through the code.</span></span> 
- <span data-ttu-id="13007-390">Проверка скрипта локально.</span><span class="sxs-lookup"><span data-stu-id="13007-390">Validate your script locally.</span></span>

<span data-ttu-id="13007-391">Инструкции по локальному выполнению и отладке см. в статье [Локальный запуск и локальная отладка U-SQL в Visual Studio Code](data-lake-tools-for-vscode-local-run-and-debug.md).</span><span class="sxs-lookup"><span data-stu-id="13007-391">For instructions on local run and local debug, see [U-SQL local run and local debug with Visual Studio Code](data-lake-tools-for-vscode-local-run-and-debug.md).</span></span>

## <a name="additional-features"></a><span data-ttu-id="13007-392">Дополнительные функции</span><span class="sxs-lookup"><span data-stu-id="13007-392">Additional features</span></span>

<span data-ttu-id="13007-393">Средства Data Lake для VS Code поддерживают следующие функции:</span><span class="sxs-lookup"><span data-stu-id="13007-393">Data Lake Tools for VS Code supports the following features:</span></span>

-   <span data-ttu-id="13007-394">Автоматическое завершение IntelliSense: предлагаемые варианты отображаются во всплывающих окнах вокруг элементов, таких как ключевые слова, методы и переменные.</span><span class="sxs-lookup"><span data-stu-id="13007-394">IntelliSense auto-complete: Suggestions appear in pop-up windows around items, such as keywords, methods, and variables.</span></span> <span data-ttu-id="13007-395">Разные значки обозначают объекты разных типов:</span><span class="sxs-lookup"><span data-stu-id="13007-395">Different icons represent different types of the objects:</span></span>

    - <span data-ttu-id="13007-396">тип данных Scala;</span><span class="sxs-lookup"><span data-stu-id="13007-396">Scala data type</span></span>
    - <span data-ttu-id="13007-397">сложный тип данных;</span><span class="sxs-lookup"><span data-stu-id="13007-397">Complex data type</span></span>
    - <span data-ttu-id="13007-398">встроенные пользовательские типы;</span><span class="sxs-lookup"><span data-stu-id="13007-398">Built-in UDTs</span></span>
    - <span data-ttu-id="13007-399">коллекции и классы .NET;</span><span class="sxs-lookup"><span data-stu-id="13007-399">.NET collection and classes</span></span>
    - <span data-ttu-id="13007-400">выражения C#;</span><span class="sxs-lookup"><span data-stu-id="13007-400">C# expressions</span></span>
    - <span data-ttu-id="13007-401">встроенные функции и объекты C#, определяемые пользователем;</span><span class="sxs-lookup"><span data-stu-id="13007-401">Built-in C# UDFs, UDOs, and UDAAGs</span></span> 
    - <span data-ttu-id="13007-402">функции U-SQL;</span><span class="sxs-lookup"><span data-stu-id="13007-402">U-SQL functions</span></span>
    - <span data-ttu-id="13007-403">функции U-SQL для работы с окнами.</span><span class="sxs-lookup"><span data-stu-id="13007-403">U-SQL windowing function</span></span>
 
    ![Типы объектов IntelliSencse в средствах Data Lake для Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-auto-complete-objects.png)
 
-   <span data-ttu-id="13007-405">Автоматическое завершение IntelliSense в метаданных Data Lake Analytics: средства Data Lake скачивают сведения метаданных Data Lake Analytics локально.</span><span class="sxs-lookup"><span data-stu-id="13007-405">IntelliSense auto-complete on Data Lake Analytics metadata: Data Lake Tools downloads the Data Lake Analytics metadata information locally.</span></span> <span data-ttu-id="13007-406">Функция IntelliSense автоматически заполняет объекты, включая базы данных, схемы, таблицы, представления, функции, функции с табличным значением, процедуры и сборки C#, на основе метаданных Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="13007-406">The IntelliSense feature automatically populates objects, including the database, schema, table, view, table-valued function, procedures, and C# assemblies, from the Data Lake Analytics metadata.</span></span>
 
    ![Метаданные IntelliSense в средствах Data Lake для Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-auto-complete-metastore.png)

-   <span data-ttu-id="13007-408">Маркер ошибки IntelliSense: средства Data Lake подчеркивают ошибки ввода в файлах U-SQL и C#.</span><span class="sxs-lookup"><span data-stu-id="13007-408">IntelliSense error marker: Data Lake Tools underlines the editing errors for U-SQL and C#.</span></span> 
-   <span data-ttu-id="13007-409">Выделение синтаксиса: средства Data Lake используют различные цвета для выделения элементов, таких как переменные, ключевые слова, типы данных и функции.</span><span class="sxs-lookup"><span data-stu-id="13007-409">Syntax highlights: Data Lake Tools uses different colors to differentiate items, such as variables, keywords, data type, and functions.</span></span> 

    ![Подсветка синтаксиса в средствах Data Lake для Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-syntax-highlights.png)

## <a name="next-steps"></a><span data-ttu-id="13007-411">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="13007-411">Next steps</span></span>

- <span data-ttu-id="13007-412">Дополнительные сведения о локальном выполнении и локальной отладке U-SQL с помощью Visual Studio Code см. в статье [Локальный запуск и локальная отладка U-SQL в Visual Studio Code](data-lake-tools-for-vscode-local-run-and-debug.md).</span><span class="sxs-lookup"><span data-stu-id="13007-412">For U-SQL local run and local debug with Visual Studio Code, see [U-SQL local run and local debug with Visual Studio Code](data-lake-tools-for-vscode-local-run-and-debug.md).</span></span>
- <span data-ttu-id="13007-413">Дополнительные сведения о начале работы с Data Lake Analytics см. в статье [Начало работы с Azure Data Lake Analytics с помощью портала Azure](data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="13007-413">For getting-started information on Data Lake Analytics, see [Tutorial: Get started with Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md).</span></span>
- <span data-ttu-id="13007-414">Дополнительные сведения об использовании средств Data Lake для U-SQL см. в статье [Разработка скриптов U-SQL с помощью средств Data Lake для Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="13007-414">For information about Data Lake Tools for Visual Studio, see [Tutorial: Develop U-SQL scripts by using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
- <span data-ttu-id="13007-415">Дополнительные сведения о разработке сборок см. в статье [Разработка сборок U-SQL для заданий Azure Data Lake Analytics](data-lake-analytics-u-sql-develop-assemblies.md).</span><span class="sxs-lookup"><span data-stu-id="13007-415">For information on developing assemblies, see [Develop U-SQL assemblies for Azure Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-assemblies.md).</span></span>



