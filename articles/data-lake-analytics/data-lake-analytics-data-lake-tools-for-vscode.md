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
# <a name="use-azure-data-lake-tools-for-visual-studio-code"></a><span data-ttu-id="6699c-104">Использование средств Azure Data Lake для Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="6699c-104">Use Azure Data Lake Tools for Visual Studio Code</span></span>

<span data-ttu-id="6699c-105">Узнайте, как проверить toouse средства Озера данных Azure для toocreate кода Visual Studio (VS Code) и выполнить скрипт U-SQL.</span><span class="sxs-lookup"><span data-stu-id="6699c-105">Learn how toouse Azure Data Lake Tools for Visual Studio Code (VS Code) toocreate, test, and run U-SQL scripts.</span></span> <span data-ttu-id="6699c-106">Hello сведения рассматриваются следующие видео hello:</span><span class="sxs-lookup"><span data-stu-id="6699c-106">hello information is also covered in hello following video:</span></span>

<a href="https://www.youtube.com/watch?v=J_gWuyFnaGA&feature=youtu.be"><img src="./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-video.png"></a>

## <a name="prerequisites"></a><span data-ttu-id="6699c-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="6699c-107">Prerequisites</span></span>

<span data-ttu-id="6699c-108">Средства Озера данных могут устанавливаться на платформах hello, поддерживаемых в VS Code.</span><span class="sxs-lookup"><span data-stu-id="6699c-108">Data Lake Tools can be installed on hello platforms supported by VS Code.</span></span> <span data-ttu-id="6699c-109">Hello поддерживается платформам относятся Windows, Linux и MacOS.</span><span class="sxs-lookup"><span data-stu-id="6699c-109">hello supported platforms include Windows, Linux, and MacOS.</span></span> <span data-ttu-id="6699c-110">Hello различных платформ имеют hello следующие предварительные требования:</span><span class="sxs-lookup"><span data-stu-id="6699c-110">hello different platforms have hello following prerequisites:</span></span>

- <span data-ttu-id="6699c-111">Windows</span><span class="sxs-lookup"><span data-stu-id="6699c-111">Windows</span></span>

    - <span data-ttu-id="6699c-112">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="6699c-112">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span></span>
    - <span data-ttu-id="6699c-113">[Среда выполнения Java SE, версия 8 с обновлением 77 или более поздние выпуски](https://java.com/download/manual.jsp).</span><span class="sxs-lookup"><span data-stu-id="6699c-113">[Java SE Runtime Environment version 8 update 77 or later](https://java.com/download/manual.jsp).</span></span> <span data-ttu-id="6699c-114">Добавьте hello java.exe путь toohello системы среды переменной путь.</span><span class="sxs-lookup"><span data-stu-id="6699c-114">Add hello java.exe path toohello system environment variable path.</span></span> <span data-ttu-id="6699c-115">Инструкции по настройке см. в разделе [как задать или изменить системную переменную пути hello?]( https://www.java.com/download/help/path.xml).</span><span class="sxs-lookup"><span data-stu-id="6699c-115">For configuration instructions, see [How do I set or change hello Path system variable?]( https://www.java.com/download/help/path.xml).</span></span> <span data-ttu-id="6699c-116">аналогичные tooC:\Program Files\Java\jdk1.8.0_77\jre\bin указан путь Hello.</span><span class="sxs-lookup"><span data-stu-id="6699c-116">hello path is similar tooC:\Program Files\Java\jdk1.8.0_77\jre\bin.</span></span>
    - <span data-ttu-id="6699c-117">[Пакет SDK для .NET Core 1.0.3 или среда выполнения .NET Core 1.1](https://www.microsoft.com/net/download).</span><span class="sxs-lookup"><span data-stu-id="6699c-117">[.NET Core SDK 1.0.3 or .NET Core 1.1 runtime](https://www.microsoft.com/net/download).</span></span>
    
- <span data-ttu-id="6699c-118">Linux (мы рекомендуем использовать Ubuntu 14.04 LTS)</span><span class="sxs-lookup"><span data-stu-id="6699c-118">Linux (We recommend Ubuntu 14.04 LTS)</span></span>

    - <span data-ttu-id="6699c-119">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="6699c-119">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span></span> <span data-ttu-id="6699c-120">tooinstall Здравствуйте кода, введите следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="6699c-120">tooinstall hello code, enter hello following command:</span></span>

              sudo dpkg -i code_<version_number>_amd64.deb

    - <span data-ttu-id="6699c-121">[Mono 4.2.x](http://www.mono-project.com/docs/getting-started/install/linux/).</span><span class="sxs-lookup"><span data-stu-id="6699c-121">[Mono 4.2.x](http://www.mono-project.com/docs/getting-started/install/linux/).</span></span> 

        - <span data-ttu-id="6699c-122">пакет deb hello tooupdate источников, вводить hello, следующие команды:</span><span class="sxs-lookup"><span data-stu-id="6699c-122">tooupdate hello deb package source, enter hello following commands:</span></span>

                sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF
                echo "deb http://download.mono-project.com/repo/debian wheezy/snapshots 4.2.4.4/main" | sudo tee /etc/apt/sources.list.d/mono-xamarin.list
                sudo apt-get update

        - <span data-ttu-id="6699c-123">tooinstall моно, введите следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="6699c-123">tooinstall Mono, enter hello following command:</span></span>

                sudo apt-get install mono-complete

            > [!NOTE] 
            > <span data-ttu-id="6699c-124">Mono 4.6 не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="6699c-124">Mono 4.6 is not supported.</span></span> <span data-ttu-id="6699c-125">Полностью удалите версию 4.6 перед установкой версии 4.2.х.</span><span class="sxs-lookup"><span data-stu-id="6699c-125">Uninstall version 4.6 entirely before you install 4.2.x.</span></span>  

        - <span data-ttu-id="6699c-126">[Среда выполнения Java SE, версия 8 с обновлением 77 или более поздние выпуски](https://java.com/download/manual.jsp).</span><span class="sxs-lookup"><span data-stu-id="6699c-126">[Java SE Runtime Environment version 8 update 77 or later](https://java.com/download/manual.jsp).</span></span> <span data-ttu-id="6699c-127">Инструкции по установке см. в разделе hello [инструкции по установке Linux x 64 для Java]( https://java.com/en/download/help/linux_x64_install.xml) страницы.</span><span class="sxs-lookup"><span data-stu-id="6699c-127">For instructions on installation, see hello [Linux 64-bit installation instructions for Java]( https://java.com/en/download/help/linux_x64_install.xml) page.</span></span>
        - <span data-ttu-id="6699c-128">[Пакет SDK для .NET Core 1.0.3 или среда выполнения .NET Core 1.1](https://www.microsoft.com/net/download).</span><span class="sxs-lookup"><span data-stu-id="6699c-128">[.NET Core SDK 1.0.3 or .NET Core 1.1 runtime](https://www.microsoft.com/net/download).</span></span>
- <span data-ttu-id="6699c-129">MacOS</span><span class="sxs-lookup"><span data-stu-id="6699c-129">MacOS</span></span>

    - <span data-ttu-id="6699c-130">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="6699c-130">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span></span>
    - <span data-ttu-id="6699c-131">[Mono 4.2.4](http://download.mono-project.com/archive/4.2.4/macos-10-x86/).</span><span class="sxs-lookup"><span data-stu-id="6699c-131">[Mono 4.2.4](http://download.mono-project.com/archive/4.2.4/macos-10-x86/).</span></span> 
    - <span data-ttu-id="6699c-132">[Среда выполнения Java SE, версия 8 с обновлением 77 или более поздние выпуски](https://java.com/download/manual.jsp).</span><span class="sxs-lookup"><span data-stu-id="6699c-132">[Java SE Runtime Environment version 8 update 77 or later](https://java.com/download/manual.jsp).</span></span> <span data-ttu-id="6699c-133">Инструкции по установке см. в разделе hello [инструкции по установке Linux x 64 для Java](https://java.com/en/download/help/mac_install.xml) страницы.</span><span class="sxs-lookup"><span data-stu-id="6699c-133">For instructions on installation, see hello [Linux 64-bit installation instructions for Java](https://java.com/en/download/help/mac_install.xml) page.</span></span>
    - <span data-ttu-id="6699c-134">[Пакет SDK для .NET Core 1.0.3 или среда выполнения .NET Core 1.1](https://www.microsoft.com/net/download).</span><span class="sxs-lookup"><span data-stu-id="6699c-134">[.NET Core SDK 1.0.3 or .NET Core 1.1 runtime](https://www.microsoft.com/net/download).</span></span>

## <a name="install-data-lake-tools"></a><span data-ttu-id="6699c-135">Установка средств Data Lake</span><span class="sxs-lookup"><span data-stu-id="6699c-135">Install Data Lake Tools</span></span>

<span data-ttu-id="6699c-136">После установки необходимых компонентов hello, можно установить средства Озера данных для VS Code.</span><span class="sxs-lookup"><span data-stu-id="6699c-136">After you install hello prerequisites, you can install Data Lake Tools for VS Code.</span></span>

<span data-ttu-id="6699c-137">**tooinstall средства Озера данных**</span><span class="sxs-lookup"><span data-stu-id="6699c-137">**tooinstall Data Lake Tools**</span></span>

1. <span data-ttu-id="6699c-138">Откройте Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="6699c-138">Open Visual Studio Code.</span></span>
2. <span data-ttu-id="6699c-139">Выберите сочетание клавиш Ctrl + P, а затем введите hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="6699c-139">Select Ctrl+P, and then enter hello following command:</span></span>
```
ext install usql-vscode-ext
```
<span data-ttu-id="6699c-140">Вы увидите список расширений для Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="6699c-140">You can see a list of Visual Studio code extensions.</span></span> <span data-ttu-id="6699c-141">Среди них есть **средства Azure Data Lake**.</span><span class="sxs-lookup"><span data-stu-id="6699c-141">One of them is **Azure Data Lake Tools**.</span></span>

3. <span data-ttu-id="6699c-142">Выберите **установить** Далее слишком**средства Озера данных Azure**.</span><span class="sxs-lookup"><span data-stu-id="6699c-142">Select **Install** next too**Azure Data Lake Tools**.</span></span> <span data-ttu-id="6699c-143">Через несколько секунд hello **установить** кнопку изменения слишком**перезагрузить**.</span><span class="sxs-lookup"><span data-stu-id="6699c-143">After a few seconds, hello **Install** button changes too**Reload**.</span></span>
4. <span data-ttu-id="6699c-144">Выберите **перезагрузить** tooactivate hello расширения.</span><span class="sxs-lookup"><span data-stu-id="6699c-144">Select **Reload** tooactivate hello extension.</span></span>
5. <span data-ttu-id="6699c-145">Выберите **ОК** tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="6699c-145">Select **OK** tooconfirm.</span></span> <span data-ttu-id="6699c-146">Вы увидите средства Озера данных Azure на hello **расширения** области.</span><span class="sxs-lookup"><span data-stu-id="6699c-146">You can see Azure Data Lake Tools in hello **Extensions** pane.</span></span>
    <span data-ttu-id="6699c-147">![Средства Data Lake в области "Расширения" Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extensions.png)</span><span class="sxs-lookup"><span data-stu-id="6699c-147">![Data Lake Tools for Visual Studio Code Extensions pane](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extensions.png)</span></span>

## <a name="activate-azure-data-lake-tools"></a><span data-ttu-id="6699c-148">Активация Средств Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="6699c-148">Activate Azure Data Lake Tools</span></span>
<span data-ttu-id="6699c-149">Создайте новый файл .usql или откройте существующий .usql tooactivate hello расширение файла.</span><span class="sxs-lookup"><span data-stu-id="6699c-149">Create a new .usql file or open an existing .usql file tooactivate hello extension.</span></span> 

## <a name="connect-tooazure"></a><span data-ttu-id="6699c-150">Подключение tooAzure</span><span class="sxs-lookup"><span data-stu-id="6699c-150">Connect tooAzure</span></span>

<span data-ttu-id="6699c-151">Прежде чем можно будет скомпилировать и выполнить скрипт U-SQL в аналитике Озера данных, необходимо подключить tooyour учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="6699c-151">Before you can compile and run U-SQL scripts in Data Lake Analytics, you must connect tooyour Azure account.</span></span>

<span data-ttu-id="6699c-152">**tooconnect tooAzure**</span><span class="sxs-lookup"><span data-stu-id="6699c-152">**tooconnect tooAzure**</span></span>

1.  <span data-ttu-id="6699c-153">Выберите палитру команд hello tooopen Ctrl + Shift + P.</span><span class="sxs-lookup"><span data-stu-id="6699c-153">Select Ctrl+Shift+P tooopen hello command palette.</span></span> 
2.  <span data-ttu-id="6699c-154">Введите текст **ADL: Login**.</span><span class="sxs-lookup"><span data-stu-id="6699c-154">Enter **ADL: Login**.</span></span> <span data-ttu-id="6699c-155">сведения об имени входа Hello отображается в hello **вывода** области.</span><span class="sxs-lookup"><span data-stu-id="6699c-155">hello login information appears in hello **Output** pane.</span></span>

    <span data-ttu-id="6699c-156">![Палитра команд средств Data Lake для Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extension-login.png)
    ![Сведения о входе устройства в средства Data Lake для Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-login-info.png)</span><span class="sxs-lookup"><span data-stu-id="6699c-156">![Data Lake Tools for Visual Studio Code command palette](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extension-login.png)
![Data Lake Tools for Visual Studio Code device login information](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-login-info.png)</span></span>
3. <span data-ttu-id="6699c-157">Выберите сочетание клавиш Ctrl + щелкнуть URL-адрес входа hello: https://aka.ms/devicelogin tooopen hello входа веб-страницы.</span><span class="sxs-lookup"><span data-stu-id="6699c-157">Select Ctrl+click on hello login URL: https://aka.ms/devicelogin tooopen hello login webpage.</span></span> <span data-ttu-id="6699c-158">Введите код hello **G567LX42V** в hello текстовое поле, а затем выберите **Продолжить**.</span><span class="sxs-lookup"><span data-stu-id="6699c-158">Enter hello code **G567LX42V** into hello text box, and then select **Continue**.</span></span>

   ![Вставка кода для входа в Средства Data Lake для Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extension-login-paste-code.png )   
4.  <span data-ttu-id="6699c-160">Следуйте toosign инструкции hello в веб-страницу приветствия.</span><span class="sxs-lookup"><span data-stu-id="6699c-160">Follow hello instructions toosign in from hello webpage.</span></span> <span data-ttu-id="6699c-161">Если вы подключены, имя учетной записи Azure отображается в строке состояния hello в левом нижнем углу hello hello **VS Code** окна.</span><span class="sxs-lookup"><span data-stu-id="6699c-161">When you're connected, your Azure account name appears on hello status bar in hello lower-left corner of hello **VS Code** window.</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="6699c-162">Если для учетной записи используется двухфакторная проверка подлинности, мы советуем использовать проверку подлинности через телефон, а не PIN-код.</span><span class="sxs-lookup"><span data-stu-id="6699c-162">If your account has two factors enabled, we recommend that you use phone authentication rather than using a PIN.</span></span>

<span data-ttu-id="6699c-163">toosign, введите команду hello **ADL: выхода**.</span><span class="sxs-lookup"><span data-stu-id="6699c-163">toosign out, enter hello command **ADL: Logout**.</span></span>

## <a name="list-your-data-lake-analytics-accounts"></a><span data-ttu-id="6699c-164">Вывод списка учетных записей Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="6699c-164">List your Data Lake Analytics accounts</span></span>

<span data-ttu-id="6699c-165">соединение tootest hello, получить список учетных записей аналитики Озера данных.</span><span class="sxs-lookup"><span data-stu-id="6699c-165">tootest hello connection, get a list of your Data Lake Analytics accounts.</span></span>

<span data-ttu-id="6699c-166">**учетные записи аналитики Озера данных toolist hello в рамках подписки Azure**</span><span class="sxs-lookup"><span data-stu-id="6699c-166">**toolist hello Data Lake Analytics accounts under your Azure subscription**</span></span>

1. <span data-ttu-id="6699c-167">Выберите палитру команд hello tooopen Ctrl + Shift + P.</span><span class="sxs-lookup"><span data-stu-id="6699c-167">Select Ctrl+Shift+P tooopen hello command palette.</span></span>
2. <span data-ttu-id="6699c-168">Введите команду **ADL: List Accounts**.</span><span class="sxs-lookup"><span data-stu-id="6699c-168">Enter **ADL: List Accounts**.</span></span> <span data-ttu-id="6699c-169">Hello учетные записи отображаются в hello **вывода** области.</span><span class="sxs-lookup"><span data-stu-id="6699c-169">hello accounts appear in hello **Output** pane.</span></span>

## <a name="open-hello-sample-script"></a><span data-ttu-id="6699c-170">Привет открыть образец сценария</span><span class="sxs-lookup"><span data-stu-id="6699c-170">Open hello sample script</span></span>
<span data-ttu-id="6699c-171">Откройте палитру команд hello (Ctrl + Shift + P) и введите **ADL: Откройте пример сценария**.</span><span class="sxs-lookup"><span data-stu-id="6699c-171">Open hello command palette (Ctrl+Shift+P) and enter **ADL: Open Sample Script**.</span></span> <span data-ttu-id="6699c-172">При этом откроется другой экземпляр этого примера.</span><span class="sxs-lookup"><span data-stu-id="6699c-172">This opens another instance of this sample.</span></span> <span data-ttu-id="6699c-173">Также можно изменять, настраивать и отправлять скрипт в этом экземпляре.</span><span class="sxs-lookup"><span data-stu-id="6699c-173">You can also edit, configure, and submit script on this instance.</span></span>

## <a name="work-with-u-sql"></a><span data-ttu-id="6699c-174">Работа с U-SQL</span><span class="sxs-lookup"><span data-stu-id="6699c-174">Work with U-SQL</span></span>

<span data-ttu-id="6699c-175">Требуется откройте файл U-SQL или toowork папки с U-SQL.</span><span class="sxs-lookup"><span data-stu-id="6699c-175">You need open either a U-SQL file or a folder toowork with U-SQL.</span></span>

<span data-ttu-id="6699c-176">**tooopen папки для проекта U-SQL**</span><span class="sxs-lookup"><span data-stu-id="6699c-176">**tooopen a folder for your U-SQL project**</span></span>

1. <span data-ttu-id="6699c-177">Из кода Visual Studio, выберите hello **файл** меню, а затем выберите **открыть папку**.</span><span class="sxs-lookup"><span data-stu-id="6699c-177">From Visual Studio Code, select hello **File** menu, and then select **Open Folder**.</span></span>
2. <span data-ttu-id="6699c-178">Укажите папку и выберите **Выбрать папку**.</span><span class="sxs-lookup"><span data-stu-id="6699c-178">Specify a folder, and then select **Select Folder**.</span></span>
3. <span data-ttu-id="6699c-179">Выберите hello **файл** меню, а затем выберите **New**.</span><span class="sxs-lookup"><span data-stu-id="6699c-179">Select hello **File** menu, and then select **New**.</span></span> <span data-ttu-id="6699c-180">Toohello проект добавляется файл безымянный-1.</span><span class="sxs-lookup"><span data-stu-id="6699c-180">An Untitled-1 file is added toohello project.</span></span>
4. <span data-ttu-id="6699c-181">Введите следующий код в файл hello безымянный 1 hello:</span><span class="sxs-lookup"><span data-stu-id="6699c-181">Enter hello following code into hello Untitled-1 file:</span></span>

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

    <span data-ttu-id="6699c-182">Hello сценарий создает файл departments.csv часть данных, включенных в папке/Output hello.</span><span class="sxs-lookup"><span data-stu-id="6699c-182">hello script creates a departments.csv file with some data included in hello /output folder.</span></span>

5. <span data-ttu-id="6699c-183">Сохраните файл как файл hello **myUSQL.usql** в Привет открыть папку.</span><span class="sxs-lookup"><span data-stu-id="6699c-183">Save hello file as **myUSQL.usql** in hello opened folder.</span></span> <span data-ttu-id="6699c-184">Файл конфигурации adltools_settings.json также добавляется toohello проекта.</span><span class="sxs-lookup"><span data-stu-id="6699c-184">A adltools_settings.json configuration file is also added toohello project.</span></span>
4. <span data-ttu-id="6699c-185">Откройте и настройте adltools_settings.json с hello следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="6699c-185">Open and configure adltools_settings.json with hello following properties:</span></span>

    - <span data-ttu-id="6699c-186">Account: учетная запись Data Lake Analytics, входящая в вашу подписку Azure.</span><span class="sxs-lookup"><span data-stu-id="6699c-186">Account:  A Data Lake Analytics account under your Azure subscription.</span></span>
    - <span data-ttu-id="6699c-187">Database: база данных в вашей учетной записи.</span><span class="sxs-lookup"><span data-stu-id="6699c-187">Database: A database under your account.</span></span> <span data-ttu-id="6699c-188">по умолчанию Hello — **master**.</span><span class="sxs-lookup"><span data-stu-id="6699c-188">hello default is **master**.</span></span>
    - <span data-ttu-id="6699c-189">Schema: схема в базе данных.</span><span class="sxs-lookup"><span data-stu-id="6699c-189">Schema: A schema under your database.</span></span> <span data-ttu-id="6699c-190">по умолчанию Hello — **dbo**.</span><span class="sxs-lookup"><span data-stu-id="6699c-190">hello default is **dbo**.</span></span>
    - <span data-ttu-id="6699c-191">Необязательные параметры:</span><span class="sxs-lookup"><span data-stu-id="6699c-191">Optional settings:</span></span>
        - <span data-ttu-id="6699c-192">Приоритет: hello приоритет диапазон: 1 too1000 с 1 как hello наивысший приоритет.</span><span class="sxs-lookup"><span data-stu-id="6699c-192">Priority: hello priority range is from 1 too1000 with 1 as hello highest priority.</span></span> <span data-ttu-id="6699c-193">значение по умолчанию Hello — **1000**.</span><span class="sxs-lookup"><span data-stu-id="6699c-193">hello default value is **1000**.</span></span>
        - <span data-ttu-id="6699c-194">Параллелизм: hello параллелизма диапазон: 1 too150.</span><span class="sxs-lookup"><span data-stu-id="6699c-194">Parallelism: hello parallelism range is from 1 too150.</span></span> <span data-ttu-id="6699c-195">значение по умолчанию Hello — Максимальная параллелизма hello допускается в вашей учетной записи аналитики Озера данных Azure.</span><span class="sxs-lookup"><span data-stu-id="6699c-195">hello default value is hello maximum parallelism allowed in your Azure Data Lake Analytics account.</span></span> 
        
        > [!NOTE] 
        > <span data-ttu-id="6699c-196">Если параметры hello являются недопустимыми, используются значения по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="6699c-196">If hello settings are invalid, hello default values are used.</span></span>

    ![Файл конфигурации средств Data Lake для Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-configuration-file.png)

    <span data-ttu-id="6699c-198">Учетная запись аналитики Озера данных является вычислительных требуется toocompile и запустите задания U-SQL.</span><span class="sxs-lookup"><span data-stu-id="6699c-198">A compute Data Lake Analytics account is needed toocompile and run U-SQL jobs.</span></span> <span data-ttu-id="6699c-199">Перед можно скомпилировать и запустить задания U-SQL, необходимо настроить учетную запись компьютера hello.</span><span class="sxs-lookup"><span data-stu-id="6699c-199">You must configure hello computer account before you can compile and run U-SQL jobs.</span></span>
    
<span data-ttu-id="6699c-200">После сохранения конфигурации hello hello сведения учетной записи, базы данных и схемы отображается в строке состояния hello в нижний левый угол hello соответствующего файла .usql hello.</span><span class="sxs-lookup"><span data-stu-id="6699c-200">After hello configuration is saved, hello account, database, and schema information appears on hello status bar at hello bottom-left corner of hello corresponding .usql file.</span></span> 
 
 
<span data-ttu-id="6699c-201">Сравниваемые tooopening файл при открытии папки, которые вы можете:</span><span class="sxs-lookup"><span data-stu-id="6699c-201">Compared tooopening a file, when you open a folder you can:</span></span>

- <span data-ttu-id="6699c-202">Использовать файл с выделенным кодом.</span><span class="sxs-lookup"><span data-stu-id="6699c-202">Use a code-behind file.</span></span> <span data-ttu-id="6699c-203">В режиме одного файла hello кода не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="6699c-203">In hello single-file mode, code-behind is not supported.</span></span>
- <span data-ttu-id="6699c-204">Использовать файл конфигурации.</span><span class="sxs-lookup"><span data-stu-id="6699c-204">Use a configuration file.</span></span> <span data-ttu-id="6699c-205">При открытии папки сценариев hello в рабочую папку hello совместно использовать один файл конфигурации.</span><span class="sxs-lookup"><span data-stu-id="6699c-205">When you open a folder, hello scripts in hello working folder share a single configuration file.</span></span>


<span data-ttu-id="6699c-206">Hello скрипт U-SQL компилирует удаленно через hello Служба аналитики Озера данных.</span><span class="sxs-lookup"><span data-stu-id="6699c-206">hello U-SQL script compiles remotely through hello Data Lake Analytics service.</span></span> <span data-ttu-id="6699c-207">При использовании команды hello **компиляции** команды отправки учетной записи аналитики Озера данных tooyour hello скрипт U-SQL.</span><span class="sxs-lookup"><span data-stu-id="6699c-207">When you issue hello **compile** command, hello U-SQL script is sent tooyour Data Lake Analytics account.</span></span> <span data-ttu-id="6699c-208">Более поздней версии Visual Studio Code получает результат компиляции hello.</span><span class="sxs-lookup"><span data-stu-id="6699c-208">Later, Visual Studio Code receives hello compilation result.</span></span> <span data-ttu-id="6699c-209">Из-за toohello удаленного компиляции кода Visual Studio требуется перечисляются сведения hello tooconnect tooyour учетную запись аналитики Озера данных в файле конфигурации hello.</span><span class="sxs-lookup"><span data-stu-id="6699c-209">Due toohello remote compilation, Visual Studio Code requires that you list hello information tooconnect tooyour Data Lake Analytics account in hello configuration file.</span></span>

<span data-ttu-id="6699c-210">**сценарий toocompile U-SQL**</span><span class="sxs-lookup"><span data-stu-id="6699c-210">**toocompile a U-SQL script**</span></span>

1. <span data-ttu-id="6699c-211">Выберите палитру команд hello tooopen Ctrl + Shift + P.</span><span class="sxs-lookup"><span data-stu-id="6699c-211">Select Ctrl+Shift+P tooopen hello command palette.</span></span> 
2. <span data-ttu-id="6699c-212">Введите **ADL: Compile Script**.</span><span class="sxs-lookup"><span data-stu-id="6699c-212">Enter **ADL: Compile Script**.</span></span> <span data-ttu-id="6699c-213">Hello компиляции результаты отображаются в hello **вывода** окна.</span><span class="sxs-lookup"><span data-stu-id="6699c-213">hello compile results appear in hello **Output** window.</span></span> <span data-ttu-id="6699c-214">Можно также щелкнуть правой кнопкой файл скрипта и выберите **ADL: компиляции сценария** задания toocompile U-SQL.</span><span class="sxs-lookup"><span data-stu-id="6699c-214">You can also right-click a script file, and then select **ADL: Compile Script** toocompile a U-SQL job.</span></span> <span data-ttu-id="6699c-215">Результат компиляции Hello появится в hello **вывода** области.</span><span class="sxs-lookup"><span data-stu-id="6699c-215">hello compilation result appears in hello **Output** pane.</span></span>
 

<span data-ttu-id="6699c-216">**сценарий toosubmit U-SQL**</span><span class="sxs-lookup"><span data-stu-id="6699c-216">**toosubmit a U-SQL script**</span></span>

1. <span data-ttu-id="6699c-217">Выберите палитру команд hello tooopen Ctrl + Shift + P.</span><span class="sxs-lookup"><span data-stu-id="6699c-217">Select Ctrl+Shift+P tooopen hello command palette.</span></span> 
2. <span data-ttu-id="6699c-218">Введите **ADL: Submit Job**.</span><span class="sxs-lookup"><span data-stu-id="6699c-218">Enter **ADL: Submit Job**.</span></span>  <span data-ttu-id="6699c-219">Также можно щелкнуть правой кнопкой мыши файл скрипта и выбрать **ADL: Submit Job**.</span><span class="sxs-lookup"><span data-stu-id="6699c-219">You can also right-click a script file, and then select **ADL: Submit Job**.</span></span> 

<span data-ttu-id="6699c-220">После отправки задания U-SQL, журналы отправки hello, отображаются в hello **вывода** окна в VS Code.</span><span class="sxs-lookup"><span data-stu-id="6699c-220">After you submit a U-SQL job, hello submission logs appear in hello **Output** window in VS Code.</span></span> <span data-ttu-id="6699c-221">При успешном выполнении отправки hello также появляются hello задания URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="6699c-221">If hello submission is successful, hello job URL appears as well.</span></span> <span data-ttu-id="6699c-222">Можно открыть URL-адрес задания hello веб браузера tootrack hello задания в режиме реального времени состояние.</span><span class="sxs-lookup"><span data-stu-id="6699c-222">You can open hello job URL in a web browser tootrack hello real-time job status.</span></span>

<span data-ttu-id="6699c-223">задать tooenable hello вывод сведений о задании hello, **jobInformationOutputPath** в hello **vs code для hello u-sql_settings.json** файл.</span><span class="sxs-lookup"><span data-stu-id="6699c-223">tooenable hello output of hello job details, set **jobInformationOutputPath** in hello **vs code for hello u-sql_settings.json** file.</span></span>
 
## <a name="use-a-code-behind-file"></a><span data-ttu-id="6699c-224">Использование файла с выделенным кодом</span><span class="sxs-lookup"><span data-stu-id="6699c-224">Use a code-behind file</span></span>

<span data-ttu-id="6699c-225">Файл с выделенным кодом является файлом C#, который связан с одним скриптом U-SQL.</span><span class="sxs-lookup"><span data-stu-id="6699c-225">A code-behind file is a C# file associated with a single U-SQL script.</span></span> <span data-ttu-id="6699c-226">Можно определить tooUDO выделенное сценария, определяемая пользователем Агрегатная Функция, определяемый пользователем тип и определяемой пользователем функции в файле кода hello.</span><span class="sxs-lookup"><span data-stu-id="6699c-226">You can define a script dedicated tooUDO, UDA, UDT, and UDF in hello code-behind file.</span></span> <span data-ttu-id="6699c-227">Hello определяемого пользователем ОПЕРАТОРА, определяемая пользователем Агрегатная Функция, определяемый пользователем тип и определяемой пользователем функции можно использовать непосредственно в скрипт hello без регистрации сборки hello сначала.</span><span class="sxs-lookup"><span data-stu-id="6699c-227">hello UDO, UDA, UDT, and UDF can be used directly in hello script without registering hello assembly first.</span></span> <span data-ttu-id="6699c-228">Hello кода файл будет помещен в hello же папке, что файл пиринга скрипт U-SQL.</span><span class="sxs-lookup"><span data-stu-id="6699c-228">hello code-behind file is put in hello same folder as its peering U-SQL script file.</span></span> <span data-ttu-id="6699c-229">Если скрипт hello называется xxx.usql, кода hello называется xxx.usql.cs.</span><span class="sxs-lookup"><span data-stu-id="6699c-229">If hello script is named xxx.usql, hello code-behind is named as xxx.usql.cs.</span></span> <span data-ttu-id="6699c-230">Если вы вручную удалите файл кода hello, компонент кода hello отключен для его связанный скрипт U-SQL.</span><span class="sxs-lookup"><span data-stu-id="6699c-230">If you manually delete hello code-behind file, hello code-behind feature is disabled for its associated U-SQL script.</span></span> <span data-ttu-id="6699c-231">Дополнительные сведения о написании пользовательского кода для скриптов U-SQL можно найти в записи блога [Writing and Using Custom Code in U-SQL – User-Defined Functions]( https://blogs.msdn.microsoft.com/visualstudio/2015/10/28/writing-and-using-custom-code-in-u-sql-user-defined-functions/) (Написание и использование пользовательского кода в U-SQL — определяемые пользователем функции).</span><span class="sxs-lookup"><span data-stu-id="6699c-231">For more information about writing customer code for U-SQL script, see [Writing and Using Custom Code in U-SQL: User-Defined Functions]( https://blogs.msdn.microsoft.com/visualstudio/2015/10/28/writing-and-using-custom-code-in-u-sql-user-defined-functions/).</span></span>

<span data-ttu-id="6699c-232">toosupport кода программной части, необходимо открыть рабочую папку.</span><span class="sxs-lookup"><span data-stu-id="6699c-232">toosupport code-behind, you must open a working folder.</span></span> 

<span data-ttu-id="6699c-233">**файл кода программной toogenerate**</span><span class="sxs-lookup"><span data-stu-id="6699c-233">**toogenerate a code-behind file**</span></span>

1. <span data-ttu-id="6699c-234">Откройте исходный файл.</span><span class="sxs-lookup"><span data-stu-id="6699c-234">Open a source file.</span></span> 
2. <span data-ttu-id="6699c-235">Выберите палитру команд hello tooopen Ctrl + Shift + P.</span><span class="sxs-lookup"><span data-stu-id="6699c-235">Select Ctrl+Shift+P tooopen hello command palette.</span></span>
3. <span data-ttu-id="6699c-236">Введите **ADL: Generate Code Behind**.</span><span class="sxs-lookup"><span data-stu-id="6699c-236">Enter **ADL: Generate Code Behind**.</span></span> <span data-ttu-id="6699c-237">Файл кода создается в hello же папки.</span><span class="sxs-lookup"><span data-stu-id="6699c-237">A code-behind file is created in hello same folder.</span></span> 

<span data-ttu-id="6699c-238">Также можно щелкнуть правой кнопкой мыши файл скрипта и выбрать **ADL: Generate Code Behind**.</span><span class="sxs-lookup"><span data-stu-id="6699c-238">You can also right-click a script file, and then select **ADL: Generate Code Behind**.</span></span> 

<span data-ttu-id="6699c-239">toocompile и отправка Здравствуйте скрипт U-SQL с помощью файла кода, так же, как файл скрипта hello автономный U-SQL.</span><span class="sxs-lookup"><span data-stu-id="6699c-239">toocompile and submit a U-SQL script with a code-behind file is hello same as with hello standalone U-SQL script file.</span></span>

<span data-ttu-id="6699c-240">следующие два снимка экрана приветствия отображения файла кода и связанный с ней файл скрипт U-SQL:</span><span class="sxs-lookup"><span data-stu-id="6699c-240">hello following two screenshots show a code-behind file and its associated U-SQL script file:</span></span>
 
![Код программной части в средствах Data Lake для Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-code-behind.png)

![Файл скрипта кода программной части в средствах Data Lake для Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-code-behind-call.png) 

## <a name="use-assemblies"></a><span data-ttu-id="6699c-243">Использование сборок</span><span class="sxs-lookup"><span data-stu-id="6699c-243">Use assemblies</span></span>

<span data-ttu-id="6699c-244">Дополнительные сведения о разработке сборок см. в статье [Разработка сборок U-SQL для заданий Azure Data Lake Analytics](data-lake-analytics-u-sql-develop-assemblies.md).</span><span class="sxs-lookup"><span data-stu-id="6699c-244">For information on developing assemblies, see [Develop U-SQL assemblies for Azure Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-assemblies.md).</span></span>

<span data-ttu-id="6699c-245">Сборки с пользовательским кодом tooregister средств Озера данных можно использовать в каталоге аналитики Озера данных hello.</span><span class="sxs-lookup"><span data-stu-id="6699c-245">You can use Data Lake Tools tooregister custom code assemblies in hello Data Lake Analytics catalog.</span></span>

<span data-ttu-id="6699c-246">**tooregister сборки**</span><span class="sxs-lookup"><span data-stu-id="6699c-246">**tooregister an assembly**</span></span>

<span data-ttu-id="6699c-247">Можно зарегистрировать сборку hello через hello **ADL: регистрация сборки** или **ADL: регистрация сборки с помощью конфигурации** команд.</span><span class="sxs-lookup"><span data-stu-id="6699c-247">You can register hello assembly through hello **ADL: Register Assembly** or **ADL: Register Assembly through Configuration** commands.</span></span>

<span data-ttu-id="6699c-248">**tooregister через hello ADL: команда регистрация сборки**</span><span class="sxs-lookup"><span data-stu-id="6699c-248">**tooregister through hello ADL: Register Assembly command**</span></span>
1.  <span data-ttu-id="6699c-249">Выберите палитру команд hello tooopen Ctrl + Shift + P.</span><span class="sxs-lookup"><span data-stu-id="6699c-249">Select Ctrl+Shift+P tooopen hello command palette.</span></span>
2.  <span data-ttu-id="6699c-250">Введите **ADL: Register Assembly**.</span><span class="sxs-lookup"><span data-stu-id="6699c-250">Enter **ADL: Register Assembly**.</span></span> 
3.  <span data-ttu-id="6699c-251">Укажите путь к локальной сборки hello.</span><span class="sxs-lookup"><span data-stu-id="6699c-251">Specify hello local assembly path.</span></span> 
4.  <span data-ttu-id="6699c-252">Выберите учетную запись Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="6699c-252">Select a Data Lake Analytics account.</span></span>
5.  <span data-ttu-id="6699c-253">Выберите базу данных.</span><span class="sxs-lookup"><span data-stu-id="6699c-253">Select a database.</span></span>

<span data-ttu-id="6699c-254">Результаты: hello портала открывается в браузере и отображает процесс регистрации сборки hello.</span><span class="sxs-lookup"><span data-stu-id="6699c-254">Results: hello portal is opened in a browser and displays hello assembly registration process.</span></span>  

<span data-ttu-id="6699c-255">Другой hello удобный способ tootrigger **ADL: регистрация сборки** команда является tooright щелчком hello DLL-файл в проводнике.</span><span class="sxs-lookup"><span data-stu-id="6699c-255">Another convenient way tootrigger hello **ADL: Register Assembly** command is tooright-click hello .dll file in File Explorer.</span></span> 

<span data-ttu-id="6699c-256">**tooregister хотя hello ADL: регистрация сборки с помощью команды конфигурации**</span><span class="sxs-lookup"><span data-stu-id="6699c-256">**tooregister though hello ADL: Register Assembly through Configuration command**</span></span>
1.  <span data-ttu-id="6699c-257">Выберите палитру команд hello tooopen Ctrl + Shift + P.</span><span class="sxs-lookup"><span data-stu-id="6699c-257">Select Ctrl+Shift+P tooopen hello command palette.</span></span>
2.  <span data-ttu-id="6699c-258">Введите **ADL: Register Assembly through Configuration**.</span><span class="sxs-lookup"><span data-stu-id="6699c-258">Enter **ADL: Register Assembly through Configuration**.</span></span> 
3.  <span data-ttu-id="6699c-259">Укажите путь к локальной сборки hello.</span><span class="sxs-lookup"><span data-stu-id="6699c-259">Specify hello local assembly path.</span></span> 
4.  <span data-ttu-id="6699c-260">отображается Hello JSON-файла.</span><span class="sxs-lookup"><span data-stu-id="6699c-260">hello JSON file is displayed.</span></span> <span data-ttu-id="6699c-261">Просмотрите и при необходимости измените зависимости сборки hello и параметров ресурса.</span><span class="sxs-lookup"><span data-stu-id="6699c-261">Review and edit hello assembly dependencies and resource parameters, if needed.</span></span> <span data-ttu-id="6699c-262">Инструкции отображаются в hello **вывода** окна.</span><span class="sxs-lookup"><span data-stu-id="6699c-262">Instructions are displayed in hello **Output** window.</span></span> <span data-ttu-id="6699c-263">tooproceed toohello регистрацию сборки, сохраните файл JSON hello (Ctrl + S).</span><span class="sxs-lookup"><span data-stu-id="6699c-263">tooproceed toohello assembly registration, save (Ctrl+S) hello JSON file.</span></span>

![Код программной части в средствах Data Lake для Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-register-assembly-advance.png)
>[!NOTE]
>- <span data-ttu-id="6699c-265">Зависимости сборок: инструменты Azure Озера данных autodetects ли hello DLL не зависит.</span><span class="sxs-lookup"><span data-stu-id="6699c-265">Assembly dependencies: Azure Data Lake Tools autodetects whether hello DLL has any dependencies.</span></span> <span data-ttu-id="6699c-266">зависимости Hello отображаются в файле JSON hello после их обнаружения.</span><span class="sxs-lookup"><span data-stu-id="6699c-266">hello dependencies are displayed in hello JSON file after they are detected.</span></span> 
>- <span data-ttu-id="6699c-267">Ресурсы: Библиотека DLL ресурсов (например, txt, .png и CSV) можно передать в процессе регистрации сборки hello.</span><span class="sxs-lookup"><span data-stu-id="6699c-267">Resources: You can upload your DLL resources (for example, .txt, .png, and .csv) as part of hello assembly registration.</span></span> 

<span data-ttu-id="6699c-268">Другой способ tootrigger hello **ADL: регистрация сборки с помощью конфигурации** команда является tooright щелчком hello DLL-файл в проводнике.</span><span class="sxs-lookup"><span data-stu-id="6699c-268">Another way tootrigger hello **ADL: Register Assembly through Configuration** command is tooright-click hello .dll file in File Explorer.</span></span> 

<span data-ttu-id="6699c-269">Hello после кода U-SQL демонстрирует, каким образом toocall сборки.</span><span class="sxs-lookup"><span data-stu-id="6699c-269">hello following U-SQL code demonstrates how toocall an assembly.</span></span> <span data-ttu-id="6699c-270">В образце hello является имя сборки hello *тестирования*.</span><span class="sxs-lookup"><span data-stu-id="6699c-270">In hello sample, hello assembly name is *test*.</span></span>

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


## <a name="access-hello-data-lake-analytics-catalog"></a><span data-ttu-id="6699c-271">Аналитика Озера данных каталога доступа hello</span><span class="sxs-lookup"><span data-stu-id="6699c-271">Access hello Data Lake Analytics catalog</span></span>

<span data-ttu-id="6699c-272">После подключения tooAzure, можно использовать следующие шаги tooaccess hello U-SQL каталога hello.</span><span class="sxs-lookup"><span data-stu-id="6699c-272">After you have connected tooAzure, you can use hello following steps tooaccess hello U-SQL catalog.</span></span>

<span data-ttu-id="6699c-273">**Аналитика Озера данных Azure метаданных tooaccess hello**</span><span class="sxs-lookup"><span data-stu-id="6699c-273">**tooaccess hello Azure Data Lake Analytics metadata**</span></span>

1.  <span data-ttu-id="6699c-274">Нажмите клавиши CTRL+SHIFT+P, а затем введите **ADL: List Tables**.</span><span class="sxs-lookup"><span data-stu-id="6699c-274">Select Ctrl+Shift+P, and then enter **ADL: List Tables**.</span></span>
2.  <span data-ttu-id="6699c-275">Выберите одну из учетных записей hello аналитики Озера данных.</span><span class="sxs-lookup"><span data-stu-id="6699c-275">Select one of hello Data Lake Analytics accounts.</span></span>
3.  <span data-ttu-id="6699c-276">Выберите одну из баз данных hello аналитики Озера данных.</span><span class="sxs-lookup"><span data-stu-id="6699c-276">Select one of hello Data Lake Analytics databases.</span></span>
4.  <span data-ttu-id="6699c-277">Выберите одну из схем hello.</span><span class="sxs-lookup"><span data-stu-id="6699c-277">Select one of hello schemas.</span></span> <span data-ttu-id="6699c-278">Вы увидите список hello таблиц.</span><span class="sxs-lookup"><span data-stu-id="6699c-278">You can see hello list of tables.</span></span>

## <a name="view-data-lake-analytics-jobs"></a><span data-ttu-id="6699c-279">Просмотр заданий Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="6699c-279">View Data Lake Analytics jobs</span></span>

<span data-ttu-id="6699c-280">**Аналитика Озера данных задания tooview**</span><span class="sxs-lookup"><span data-stu-id="6699c-280">**tooview Data Lake Analytics jobs**</span></span>
1.  <span data-ttu-id="6699c-281">Откройте палитру команд hello (Ctrl + Shift + P) и выберите **ADL: Показать задания**.</span><span class="sxs-lookup"><span data-stu-id="6699c-281">Open hello command palette (Ctrl+Shift+P) and select **ADL: Show Job**.</span></span> 
2.  <span data-ttu-id="6699c-282">Выберите Data Lake Analytics или локальную учетную запись.</span><span class="sxs-lookup"><span data-stu-id="6699c-282">Select a Data Lake Analytics or local account.</span></span> 
3.  <span data-ttu-id="6699c-283">Дождитесь hello список заданий для hello tooappear учетной записи.</span><span class="sxs-lookup"><span data-stu-id="6699c-283">Wait for hello jobs list for hello account tooappear.</span></span>
4.  <span data-ttu-id="6699c-284">Выберите задание из списка заданий, средства Озера данных открывается сведений о задании hello в hello портал Azure и открывает файл JobInfo hello в VS Code.</span><span class="sxs-lookup"><span data-stu-id="6699c-284">Select a job from job list, Data Lake Tools opens hello job details in hello Azure portal and displays hello JobInfo file in VS Code.</span></span>

![Типы объектов IntelliSencse в средствах Data Lake для Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-show-job.png)

## <a name="azure-data-lake-storage-integration"></a><span data-ttu-id="6699c-286">Интеграция с Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="6699c-286">Azure Data Lake Storage integration</span></span>

<span data-ttu-id="6699c-287">Связанные с Azure Data Lake Store команды можно использовать для:</span><span class="sxs-lookup"><span data-stu-id="6699c-287">You can use Azure Data Lake Storage-related commands to:</span></span>
 - <span data-ttu-id="6699c-288">Выполнять поиск ресурсов хранилища Озера данных Azure hello.</span><span class="sxs-lookup"><span data-stu-id="6699c-288">Browse through hello Azure Data Lake Storage resources.</span></span> 
 - <span data-ttu-id="6699c-289">Файл хранилища Озера данных Azure hello предварительного просмотра.</span><span class="sxs-lookup"><span data-stu-id="6699c-289">Preview hello Azure Data Lake Storage file.</span></span>  
 - <span data-ttu-id="6699c-290">Отправка hello tooAzure хранилища Озера данных файла непосредственно в VS Code.</span><span class="sxs-lookup"><span data-stu-id="6699c-290">Upload hello file directly tooAzure Data Lake Storage in VS Code.</span></span> 

### <a name="list-hello-storage-path"></a><span data-ttu-id="6699c-291">Путь к списку hello хранилища</span><span class="sxs-lookup"><span data-stu-id="6699c-291">List hello storage path</span></span> 
<span data-ttu-id="6699c-292">Можно составить список hello путь к хранилищу через палитру команд hello или щелкните правой кнопкой мыши.</span><span class="sxs-lookup"><span data-stu-id="6699c-292">You can list hello storage path through hello command palette or through right-click.</span></span>

<span data-ttu-id="6699c-293">**путь к хранилищу hello toolist через палитру команд hello**</span><span class="sxs-lookup"><span data-stu-id="6699c-293">**toolist hello storage path through hello command palette**</span></span>

1.  <span data-ttu-id="6699c-294">Откройте палитру команд hello (Ctrl + Shift + P) и введите **ADL: путь к хранилищу списка**.</span><span class="sxs-lookup"><span data-stu-id="6699c-294">Open hello command palette (Ctrl+Shift+P) and enter **ADL: List Storage Path**.</span></span>

    ![Вывод пути к хранилищу в средствах Data Lake для Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-storage.png)

2.  <span data-ttu-id="6699c-296">Выберите для перечисления путь к хранилищу hello предпочтительным.</span><span class="sxs-lookup"><span data-stu-id="6699c-296">Select your preferred way for listing hello storage path.</span></span> <span data-ttu-id="6699c-297">В этом примере выбран вариант **Enter a path** (Введите путь).</span><span class="sxs-lookup"><span data-stu-id="6699c-297">This passage uses **Enter a path** as an example.</span></span>

    ![Средства Озера данных для кода Visual Studio одним из способов toolist путь к хранилищу hello](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account-selectoneway.png)

    > [!NOTE]
    >- <span data-ttu-id="6699c-299">VS Code сохраняет путь к последней посетил hello в каждой учетной записи аналитики Озера данных.</span><span class="sxs-lookup"><span data-stu-id="6699c-299">VS Code keeps hello last-visited path in every Data Lake Analytics account.</span></span> <span data-ttu-id="6699c-300">Например, /tt/ss.</span><span class="sxs-lookup"><span data-stu-id="6699c-300">For example: /tt/ss.</span></span>
    >- <span data-ttu-id="6699c-301">Браузер из путь к корневому каталогу: корневой путь к списку hello из выбранной учетной записи аналитики Озера данных или локальный путь.</span><span class="sxs-lookup"><span data-stu-id="6699c-301">Browser from root path: hello list root path from your selected Data Lake Analytics account or a local path.</span></span>
    >- <span data-ttu-id="6699c-302">Введите путь: вывод указанного пути из выбранной учетной записи Azure Data Lake Analytics или локального пути.</span><span class="sxs-lookup"><span data-stu-id="6699c-302">Enter a path: List a specified path from your selected Data Lake Analytics account or a local path.</span></span>
    
3. <span data-ttu-id="6699c-303">Выберите учетную запись из hello локальный путь или учетную запись аналитики Озера данных.</span><span class="sxs-lookup"><span data-stu-id="6699c-303">Select an account from hello local path or a Data Lake Analytics account.</span></span>

    ![Средства Data Lake для Visual Studio Code: выбор дополнительных учетных записей](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

4. <span data-ttu-id="6699c-305">Выберите **дополнительные** toolist дополнительные учетные записи аналитики Озера данных, а затем выберите учетную запись аналитики Озера данных.</span><span class="sxs-lookup"><span data-stu-id="6699c-305">Select **more** toolist more Data Lake Analytics accounts, and then select a Data Lake Analytics account.</span></span>

    ![Средства Data Lake для Visual Studio Code: выбор учетной записи](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-select-adla-account.png)

5.  <span data-ttu-id="6699c-307">Введите путь к хранилищу Azure.</span><span class="sxs-lookup"><span data-stu-id="6699c-307">Enter an Azure storage path.</span></span> <span data-ttu-id="6699c-308">Например, /output.</span><span class="sxs-lookup"><span data-stu-id="6699c-308">For example, /output.</span></span>

    ![Ввод пути к хранилищу в средствах Data Lake для Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-input-path.png)

6.  <span data-ttu-id="6699c-310">Результаты: hello палитры команд сведения hello путь на основе ваших записей.</span><span class="sxs-lookup"><span data-stu-id="6699c-310">Results: hello command palette lists hello path information based on your entries.</span></span>

    ![Результат вывода пути к хранилищу в средствах Data Lake для Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-path.png)

<span data-ttu-id="6699c-312">Более удобный toolist hello относительный путь — через hello контекстное меню, щелкните правой кнопкой мыши.</span><span class="sxs-lookup"><span data-stu-id="6699c-312">A more convenient way toolist hello relative path is through hello right-click context menu.</span></span>

<span data-ttu-id="6699c-313">**Щелкните правой кнопкой мыши путь к хранилищу hello toolist через**</span><span class="sxs-lookup"><span data-stu-id="6699c-313">**toolist hello storage path through right-click**</span></span>

1.  <span data-ttu-id="6699c-314">Щелкните правой кнопкой мыши tooselect строку hello путь **путь к списку хранилища**.</span><span class="sxs-lookup"><span data-stu-id="6699c-314">Right-click hello path string tooselect **List Storage Path**.</span></span>

       ![Контекстное меню в средствах Data Lake для Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-right-click-path.png)

2. <span data-ttu-id="6699c-316">Выбранный путь относительный Hello появляется в палитру команд hello.</span><span class="sxs-lookup"><span data-stu-id="6699c-316">hello selected relative path appears in hello command palette.</span></span>

   ![Выбранный относительный путь средств Data Lake для Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-relative-path.png)

3.  <span data-ttu-id="6699c-318">Выберите учетную запись из hello локальный путь или учетную запись аналитики Озера данных.</span><span class="sxs-lookup"><span data-stu-id="6699c-318">Select an account from hello local path or a Data Lake Analytics account.</span></span>

       ![Средства Data Lake для Visual Studio Code: выбор учетной записи](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

4.  <span data-ttu-id="6699c-320">Результаты: hello палитры команд перечислены hello папок и файлов для hello текущий путь.</span><span class="sxs-lookup"><span data-stu-id="6699c-320">Results: hello command palette lists hello folders and files for hello current path.</span></span>

       ![Средства Озера данных для списка кода Visual Studio из текущего пути hello](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-current.png)

### <a name="preview-hello-storage-file"></a><span data-ttu-id="6699c-322">Файл хранилища hello предварительного просмотра</span><span class="sxs-lookup"><span data-stu-id="6699c-322">Preview hello storage file</span></span>
<span data-ttu-id="6699c-323">Можно просмотреть файл хранилища hello через палитру команд hello или щелкните правой кнопкой мыши.</span><span class="sxs-lookup"><span data-stu-id="6699c-323">You can preview hello storage file through hello command palette or through right-click.</span></span>

<span data-ttu-id="6699c-324">**файл хранилища hello toopreview через палитру команд hello**</span><span class="sxs-lookup"><span data-stu-id="6699c-324">**toopreview hello storage file through hello command palette**</span></span>

1.  <span data-ttu-id="6699c-325">Откройте палитру команд hello (Ctrl + Shift + P) и введите **ADL: просмотр хранения файла**.</span><span class="sxs-lookup"><span data-stu-id="6699c-325">Open hello command palette (Ctrl+Shift+P) and enter **ADL: Preview Storage File**.</span></span>

       ![Предварительный просмотр файла хранилища в средствах Data Lake для Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-preview.png)

2.  <span data-ttu-id="6699c-327">Выберите учетную запись из hello локальный путь или учетную запись аналитики Озера данных.</span><span class="sxs-lookup"><span data-stu-id="6699c-327">Select an account from hello local path or a Data Lake Analytics account.</span></span>

       ![Список учетных данных в средствах Data Lake для Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

3.  <span data-ttu-id="6699c-329">Выберите **дополнительные** toolist дополнительные учетные записи аналитики Озера данных, а затем выберите учетную запись аналитики Озера данных.</span><span class="sxs-lookup"><span data-stu-id="6699c-329">Select **more** toolist more Data Lake Analytics accounts, and then select a Data Lake Analytics account.</span></span>

       ![Средства Data Lake для Visual Studio Code: выбор учетной записи](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-select-adla-account.png)

4.  <span data-ttu-id="6699c-331">Введите путь к хранилищу или имя файла хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="6699c-331">Enter an Azure storage path or file.</span></span> <span data-ttu-id="6699c-332">Например, /output/SearchLog.txt.</span><span class="sxs-lookup"><span data-stu-id="6699c-332">For example, /output/SearchLog.txt.</span></span>

       ![Ввод пути к хранилищу и имени файла хранилища в средствах Data Lake для Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-input-preview-file.png)

5.  <span data-ttu-id="6699c-334">Результаты: hello палитры команд сведения hello путь на основе ваших записей.</span><span class="sxs-lookup"><span data-stu-id="6699c-334">Results: hello command palette lists hello path information based on your entries.</span></span>

       ![Результат предварительного просмотра файла в Средствах Data Lake для Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-preview-results.png)

<span data-ttu-id="6699c-336">**Щелкните правой кнопкой мыши путь к хранилищу hello toolist через**</span><span class="sxs-lookup"><span data-stu-id="6699c-336">**toolist hello storage path through right-click**</span></span>

1.  <span data-ttu-id="6699c-337">toopreview файл, щелкните правой кнопкой мыши путь к файлу hello.</span><span class="sxs-lookup"><span data-stu-id="6699c-337">toopreview a file, right-click hello file path.</span></span>

   ![Контекстное меню в средствах Data Lake для Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-right-click-preview.png) 

2.  <span data-ttu-id="6699c-339">Выберите учетную запись из hello локальный путь или учетную запись аналитики Озера данных.</span><span class="sxs-lookup"><span data-stu-id="6699c-339">Select an account from hello local path or a Data Lake Analytics account.</span></span>

       ![Средства Data Lake для Visual Studio Code: выбор учетной записи](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

3.  <span data-ttu-id="6699c-341">Результаты: VS Code отображает hello результатов предварительного просмотра файла hello.</span><span class="sxs-lookup"><span data-stu-id="6699c-341">Results: VS Code displays hello preview results of hello file.</span></span>

       ![Результат предварительного просмотра файла в Средствах Data Lake для Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-preview-results.png)

### <a name="upload-a-file"></a><span data-ttu-id="6699c-343">Отправить файл.</span><span class="sxs-lookup"><span data-stu-id="6699c-343">Upload a file</span></span> 

<span data-ttu-id="6699c-344">Можно отправить файлы, введя hello команды **ADL: Отправьте файл** или **ADL: Отправьте файл через конфигурацию**.</span><span class="sxs-lookup"><span data-stu-id="6699c-344">You can upload files by entering hello commands **ADL: Upload File** or **ADL: Upload File through Configuration**.</span></span>

<span data-ttu-id="6699c-345">**файлы tooupload хотя hello ADL: Отправьте файл-команда**</span><span class="sxs-lookup"><span data-stu-id="6699c-345">**tooupload files though hello ADL: Upload File command**</span></span>
1. <span data-ttu-id="6699c-346">Выберите палитру команд hello tooopen Ctrl + Shift + P или щелкните правой кнопкой мыши редактор сценариев hello, а затем введите **передать файл**.</span><span class="sxs-lookup"><span data-stu-id="6699c-346">Select Ctrl+Shift+P tooopen hello command palette or right-click hello script editor, and then enter **Upload File**.</span></span>
2.  <span data-ttu-id="6699c-347">tooupload hello, введите локальный путь.</span><span class="sxs-lookup"><span data-stu-id="6699c-347">tooupload hello file, enter a local path.</span></span>

    ![Ввод локального пути в средствах Data Lake для Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-auto-input-local-path.png)

3. <span data-ttu-id="6699c-349">Выберите один из способов hello путь к хранилищу листинг hello.</span><span class="sxs-lookup"><span data-stu-id="6699c-349">Select one of hello ways of listing hello storage path.</span></span> <span data-ttu-id="6699c-350">В этом примере выбран вариант **Enter a path** (Введите путь).</span><span class="sxs-lookup"><span data-stu-id="6699c-350">This passage uses **Enter a path** as an example.</span></span>

    ![Вывод пути к хранилищу в средствах Data Lake для Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account-selectoneway.png)
    >[!NOTE]
    >- <span data-ttu-id="6699c-352">VS Code сохраняет путь к последней посетил hello в каждой учетной записи аналитики Озера данных.</span><span class="sxs-lookup"><span data-stu-id="6699c-352">VS Code keeps hello last-visited path in every Data Lake Analytics account.</span></span> <span data-ttu-id="6699c-353">Например, /tt/ss.</span><span class="sxs-lookup"><span data-stu-id="6699c-353">For example: /tt/ss.</span></span>
    >- <span data-ttu-id="6699c-354">Браузер из путь к корневому каталогу: корневой путь к списку hello из выбранной учетной записи аналитики Озера данных или локальный путь.</span><span class="sxs-lookup"><span data-stu-id="6699c-354">Browser from root path: hello list root path from your selected Data Lake Analytics account or a local path.</span></span>
    >- <span data-ttu-id="6699c-355">Введите путь: вывод указанного пути из выбранной учетной записи Azure Data Lake Analytics или локального пути.</span><span class="sxs-lookup"><span data-stu-id="6699c-355">Enter a path: List a specified path from your selected Data Lake Analytics account or a local path.</span></span>

4. <span data-ttu-id="6699c-356">Выберите учетную запись из hello локальный путь или учетную запись аналитики Озера данных.</span><span class="sxs-lookup"><span data-stu-id="6699c-356">Select an account from hello local path or a Data Lake Analytics account.</span></span>

    ![Контекстное меню хранилища в средствах Data Lake для Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

5. <span data-ttu-id="6699c-358">Введите путь к хранилищу Azure.</span><span class="sxs-lookup"><span data-stu-id="6699c-358">Enter an Azure storage path.</span></span> <span data-ttu-id="6699c-359">Например, /output.</span><span class="sxs-lookup"><span data-stu-id="6699c-359">For example: /output.</span></span>

       ![Data Lake Tools for Visual Studio Code enter storage path](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-input-preview-file.png)

6. <span data-ttu-id="6699c-360">Найдите путь к хранилищу Azure.</span><span class="sxs-lookup"><span data-stu-id="6699c-360">Find your Azure storage path.</span></span> <span data-ttu-id="6699c-361">Выберите пункт **Choose current folder** (Выбрать текущую папку).</span><span class="sxs-lookup"><span data-stu-id="6699c-361">Select **Choose current folder**.</span></span>

    ![Выбор папки в средствах Data Lake для Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-choose-current-folder.png)

7.  <span data-ttu-id="6699c-363">Результаты: hello **вывода** окно отображает состояние передачи файла hello.</span><span class="sxs-lookup"><span data-stu-id="6699c-363">Results: hello **Output** window displays hello file upload status.</span></span>

       ![Состояние отправки в средствах Data Lake для Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-upload-status.png)    

<span data-ttu-id="6699c-365">**файлы tooupload хотя hello ADL: Отправьте файл через команду конфигурации**</span><span class="sxs-lookup"><span data-stu-id="6699c-365">**tooupload files though hello ADL: Upload File through Configuration command**</span></span>
1.  <span data-ttu-id="6699c-366">Выберите палитру команд hello tooopen Ctrl + Shift + P или щелкните правой кнопкой мыши редактор сценариев hello, а затем введите **передать файл конфигурации**.</span><span class="sxs-lookup"><span data-stu-id="6699c-366">Select Ctrl+Shift+P tooopen hello command palette or right-click hello script editor, and then enter **Upload File through Configuration**.</span></span>
2.  <span data-ttu-id="6699c-367">В VS Code отобразится JSON-файл.</span><span class="sxs-lookup"><span data-stu-id="6699c-367">VS Code displays a JSON file.</span></span> <span data-ttu-id="6699c-368">Можно ввести пути к файлам и отправить несколько файлов в hello то же время.</span><span class="sxs-lookup"><span data-stu-id="6699c-368">You can enter file paths and upload multiple files at hello same time.</span></span> <span data-ttu-id="6699c-369">Инструкции отображаются в hello **вывода** окна.</span><span class="sxs-lookup"><span data-stu-id="6699c-369">Instructions are displayed in hello **Output** window.</span></span> <span data-ttu-id="6699c-370">tooproceed tooupload hello файл, сохраните файл JSON hello (Ctrl + S).</span><span class="sxs-lookup"><span data-stu-id="6699c-370">tooproceed tooupload hello file, save (Ctrl+S) hello JSON file.</span></span>

       ![Путь к файлу в средствах Data Lake для Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-upload-file.png)

3.  <span data-ttu-id="6699c-372">Результаты: hello **вывода** окно отображает состояние передачи файла hello.</span><span class="sxs-lookup"><span data-stu-id="6699c-372">Results: hello **Output** window displays hello file upload status.</span></span>

       ![Состояние отправки в средствах Data Lake для Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-upload-status.png)     

<span data-ttu-id="6699c-374">Другой способ tooupload toostorage файла — через hello щелкните правой кнопкой мыши меню полный путь к файлу hello или относительный путь файла hello в редакторе сценариев hello.</span><span class="sxs-lookup"><span data-stu-id="6699c-374">Another way tooupload a file toostorage is through hello right-click menu on hello file's full path or hello file's relative path in hello script editor.</span></span> <span data-ttu-id="6699c-375">Введите путь к локальному файлу hello, а затем выберите hello учетной записи.</span><span class="sxs-lookup"><span data-stu-id="6699c-375">Enter hello local file path, and then select hello account.</span></span> <span data-ttu-id="6699c-376">Hello **вывода** окне отображается состояние передачи hello.</span><span class="sxs-lookup"><span data-stu-id="6699c-376">hello **Output** window displays hello upload status.</span></span> 

### <a name="open-azure-storage-explorer"></a><span data-ttu-id="6699c-377">Открытие обозревателя хранилищ Azure</span><span class="sxs-lookup"><span data-stu-id="6699c-377">Open Azure Storage Explorer</span></span>
<span data-ttu-id="6699c-378">Можно открыть **обозреватель хранилищ Azure** , введя команду hello **ADL: Откройте веб-обозреватель хранилища Azure** или выбрав его из контекстного меню hello.</span><span class="sxs-lookup"><span data-stu-id="6699c-378">You can open **Azure Storage Explorer** by entering hello command **ADL: Open Web Azure Storage Explorer** or by selecting it from hello right-click context menu.</span></span>

<span data-ttu-id="6699c-379">**tooopen обозреватель хранилищ Azure**</span><span class="sxs-lookup"><span data-stu-id="6699c-379">**tooopen Azure Storage Explorer**</span></span>

1. <span data-ttu-id="6699c-380">Выберите палитру команд hello tooopen Ctrl + Shift + P.</span><span class="sxs-lookup"><span data-stu-id="6699c-380">Select Ctrl+Shift+P tooopen hello command palette.</span></span>
2. <span data-ttu-id="6699c-381">Введите **откройте веб-обозреватель хранилища Azure** или щелкните правой кнопкой мыши на относительный путь или полный путь hello в редакторе сценариев hello и выберите **откройте веб-обозреватель хранилища Azure**.</span><span class="sxs-lookup"><span data-stu-id="6699c-381">Enter **Open Web Azure Storage Explorer** or right-click on a relative path or hello full path in hello script editor, and then select **Open Web Azure Storage Explorer**.</span></span>
3. <span data-ttu-id="6699c-382">Выберите учетную запись Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="6699c-382">Select a Data Lake Analytics account.</span></span>

<span data-ttu-id="6699c-383">Средства Озера данных открывает путь хранилища Azure hello в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="6699c-383">Data Lake Tools opens hello Azure storage path in hello Azure portal.</span></span> <span data-ttu-id="6699c-384">Можно найти hello пути и предварительного просмотра файла hello из Интернета hello.</span><span class="sxs-lookup"><span data-stu-id="6699c-384">You can find hello path and preview hello file from hello web.</span></span>

### <a name="local-run-and-local-debug-for-windows-users"></a><span data-ttu-id="6699c-385">Локальное выполнение и локальная отладка для пользователей Windows</span><span class="sxs-lookup"><span data-stu-id="6699c-385">Local run and local debug for Windows users</span></span>
<span data-ttu-id="6699c-386">U-SQL локального выполнения проверяет локальных данных и проверяет скрипт с локально, перед код является опубликованной tooData аналитики Озера.</span><span class="sxs-lookup"><span data-stu-id="6699c-386">U-SQL local run tests your local data and validates your script locally, before your code is published tooData Lake Analytics.</span></span> <span data-ttu-id="6699c-387">Аналитика Озера tooData отправлен вам toocomplete hello следующие задачи, прежде чем код станет компонент позволяет локальной отладки Hello:</span><span class="sxs-lookup"><span data-stu-id="6699c-387">hello local debug feature enables you toocomplete hello following tasks before your code is submitted tooData Lake Analytics:</span></span> 
- <span data-ttu-id="6699c-388">Отладка кода программной части C#.</span><span class="sxs-lookup"><span data-stu-id="6699c-388">Debug your C# code-behind.</span></span> 
- <span data-ttu-id="6699c-389">Пошаговое выполнение кода hello.</span><span class="sxs-lookup"><span data-stu-id="6699c-389">Step through hello code.</span></span> 
- <span data-ttu-id="6699c-390">Проверка скрипта локально.</span><span class="sxs-lookup"><span data-stu-id="6699c-390">Validate your script locally.</span></span>

<span data-ttu-id="6699c-391">Инструкции по локальному выполнению и отладке см. в статье [Локальный запуск и локальная отладка U-SQL в Visual Studio Code](data-lake-tools-for-vscode-local-run-and-debug.md).</span><span class="sxs-lookup"><span data-stu-id="6699c-391">For instructions on local run and local debug, see [U-SQL local run and local debug with Visual Studio Code](data-lake-tools-for-vscode-local-run-and-debug.md).</span></span>

## <a name="additional-features"></a><span data-ttu-id="6699c-392">Дополнительные функции</span><span class="sxs-lookup"><span data-stu-id="6699c-392">Additional features</span></span>

<span data-ttu-id="6699c-393">Средства Озера данных для VS Code поддерживает hello следующие атрибуты:</span><span class="sxs-lookup"><span data-stu-id="6699c-393">Data Lake Tools for VS Code supports hello following features:</span></span>

-   <span data-ttu-id="6699c-394">Автоматическое завершение IntelliSense: предлагаемые варианты отображаются во всплывающих окнах вокруг элементов, таких как ключевые слова, методы и переменные.</span><span class="sxs-lookup"><span data-stu-id="6699c-394">IntelliSense auto-complete: Suggestions appear in pop-up windows around items, such as keywords, methods, and variables.</span></span> <span data-ttu-id="6699c-395">Другие значки представляют различные типы объектов hello.</span><span class="sxs-lookup"><span data-stu-id="6699c-395">Different icons represent different types of hello objects:</span></span>

    - <span data-ttu-id="6699c-396">тип данных Scala;</span><span class="sxs-lookup"><span data-stu-id="6699c-396">Scala data type</span></span>
    - <span data-ttu-id="6699c-397">сложный тип данных;</span><span class="sxs-lookup"><span data-stu-id="6699c-397">Complex data type</span></span>
    - <span data-ttu-id="6699c-398">встроенные пользовательские типы;</span><span class="sxs-lookup"><span data-stu-id="6699c-398">Built-in UDTs</span></span>
    - <span data-ttu-id="6699c-399">коллекции и классы .NET;</span><span class="sxs-lookup"><span data-stu-id="6699c-399">.NET collection and classes</span></span>
    - <span data-ttu-id="6699c-400">выражения C#;</span><span class="sxs-lookup"><span data-stu-id="6699c-400">C# expressions</span></span>
    - <span data-ttu-id="6699c-401">встроенные функции и объекты C#, определяемые пользователем;</span><span class="sxs-lookup"><span data-stu-id="6699c-401">Built-in C# UDFs, UDOs, and UDAAGs</span></span> 
    - <span data-ttu-id="6699c-402">функции U-SQL;</span><span class="sxs-lookup"><span data-stu-id="6699c-402">U-SQL functions</span></span>
    - <span data-ttu-id="6699c-403">функции U-SQL для работы с окнами.</span><span class="sxs-lookup"><span data-stu-id="6699c-403">U-SQL windowing function</span></span>
 
    ![Типы объектов IntelliSencse в средствах Data Lake для Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-auto-complete-objects.png)
 
-   <span data-ttu-id="6699c-405">Технология IntelliSense, автоматическое завершение метаданных аналитики Озера данных: средства Озера данных загружает hello аналитики Озера данных сведения о метаданных локально.</span><span class="sxs-lookup"><span data-stu-id="6699c-405">IntelliSense auto-complete on Data Lake Analytics metadata: Data Lake Tools downloads hello Data Lake Analytics metadata information locally.</span></span> <span data-ttu-id="6699c-406">функция IntelliSense Hello автоматически заполняет объекты, включая hello базы данных, схемы, таблиц, представлений, возвращающих табличные значения функции, процедуры и C# сборки, из метаданных hello аналитики Озера данных.</span><span class="sxs-lookup"><span data-stu-id="6699c-406">hello IntelliSense feature automatically populates objects, including hello database, schema, table, view, table-valued function, procedures, and C# assemblies, from hello Data Lake Analytics metadata.</span></span>
 
    ![Метаданные IntelliSense в средствах Data Lake для Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-auto-complete-metastore.png)

-   <span data-ttu-id="6699c-408">Маркер ошибки IntelliSense: средства Озера данных подчеркивает hello редактирования ошибки U-SQL и C#.</span><span class="sxs-lookup"><span data-stu-id="6699c-408">IntelliSense error marker: Data Lake Tools underlines hello editing errors for U-SQL and C#.</span></span> 
-   <span data-ttu-id="6699c-409">Выделение синтаксиса: средств Озера данных использует элементы toodifferentiate различные цвета, например переменные, ключевые слова, тип данных и функции.</span><span class="sxs-lookup"><span data-stu-id="6699c-409">Syntax highlights: Data Lake Tools uses different colors toodifferentiate items, such as variables, keywords, data type, and functions.</span></span> 

    ![Подсветка синтаксиса в средствах Data Lake для Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-syntax-highlights.png)

## <a name="next-steps"></a><span data-ttu-id="6699c-411">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6699c-411">Next steps</span></span>

- <span data-ttu-id="6699c-412">Дополнительные сведения о локальном выполнении и локальной отладке U-SQL с помощью Visual Studio Code см. в статье [Локальный запуск и локальная отладка U-SQL в Visual Studio Code](data-lake-tools-for-vscode-local-run-and-debug.md).</span><span class="sxs-lookup"><span data-stu-id="6699c-412">For U-SQL local run and local debug with Visual Studio Code, see [U-SQL local run and local debug with Visual Studio Code](data-lake-tools-for-vscode-local-run-and-debug.md).</span></span>
- <span data-ttu-id="6699c-413">Дополнительные сведения о начале работы с Data Lake Analytics см. в статье [Начало работы с Azure Data Lake Analytics с помощью портала Azure](data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="6699c-413">For getting-started information on Data Lake Analytics, see [Tutorial: Get started with Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md).</span></span>
- <span data-ttu-id="6699c-414">Дополнительные сведения об использовании средств Data Lake для U-SQL см. в статье [Разработка скриптов U-SQL с помощью средств Data Lake для Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="6699c-414">For information about Data Lake Tools for Visual Studio, see [Tutorial: Develop U-SQL scripts by using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
- <span data-ttu-id="6699c-415">Дополнительные сведения о разработке сборок см. в статье [Разработка сборок U-SQL для заданий Azure Data Lake Analytics](data-lake-analytics-u-sql-develop-assemblies.md).</span><span class="sxs-lookup"><span data-stu-id="6699c-415">For information on developing assemblies, see [Develop U-SQL assemblies for Azure Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-assemblies.md).</span></span>



