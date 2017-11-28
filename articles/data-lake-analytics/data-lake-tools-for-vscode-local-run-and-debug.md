---
title: "Средства Azure Data Lake — локальный запуск и локальная отладка U-SQL в Visual Studio Code | Документация Майкрософт"
description: "Узнайте, как выполнять локальную отладку и локальный запуск с помощью средств Azure Data Lake для Visual Studio Code."
Keywords: "VScode,средства Azure Data Lake,локальный запуск,локальная отладка,предварительный просмотр файла хранилища,отправка по пути хранилища"
services: data-lake-analytics
documentationcenter: 
author: jejiang
manager: DJ
editor: jejiang
tags: azure-portal
ms.assetid: dc9b21d8-c5f4-4f77-bcbc-eff458f48de2
ms.service: data-lake-analytics
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: big-data
ms.date: 07/14/2017
ms.author: jejiang
ms.openlocfilehash: 367e4ba792f83d6ee246208306e4c09b69cb49ef
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="u-sql-local-run-and-local-debug-with-visual-studio-code"></a><span data-ttu-id="d2931-104">Локальный запуск и локальная отладка U-SQL в Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="d2931-104">U-SQL local run and local debug with Visual Studio Code</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d2931-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="d2931-105">Prerequisites</span></span>
<span data-ttu-id="d2931-106">Прежде чем приступить к работе, убедитесь, что у вас есть следующие необходимые компоненты.</span><span class="sxs-lookup"><span data-stu-id="d2931-106">Make sure you have the following prerequisites in place before you start these procedures:</span></span>
- <span data-ttu-id="d2931-107">Средства Azure Data Lake для Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="d2931-107">Azure Data Lake Tool for Visual Studio Code.</span></span> <span data-ttu-id="d2931-108">Инструкции см. в статье [Использование средств Azure Data Lake для Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).</span><span class="sxs-lookup"><span data-stu-id="d2931-108">For instructions, see [Use Azure Data Lake Tools for Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).</span></span>
- <span data-ttu-id="d2931-109">C# для Visual Studio Code (для локальной отладки U-SQL).</span><span class="sxs-lookup"><span data-stu-id="d2931-109">C# for Visual Studio Code (if you want to perform a U-SQL local debug).</span></span>

   ![Установка C# в средствах Data Lake для Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-install-ms-vscodecsharp.png)
   
   > [!NOTE]
   > <span data-ttu-id="d2931-111">Функции локального запуска и отладки U-SQL сейчас поддерживаются только для пользователей Windows.</span><span class="sxs-lookup"><span data-stu-id="d2931-111">The U-SQL local run and debug features currently only support Windows users.</span></span> 


## <a name="set-up-the-u-sql-local-run-environment"></a><span data-ttu-id="d2931-112">Настройка среды для локального запуска U-SQL</span><span class="sxs-lookup"><span data-stu-id="d2931-112">Set up the U-SQL local run environment</span></span>

1. <span data-ttu-id="d2931-113">Откройте палитру команд, нажав клавиши CTRL+SHIFT+P, и введите **ADL: Download LocalRun Dependency** (ADL: скачать зависимости для локального запуска), чтобы скачать пакеты.</span><span class="sxs-lookup"><span data-stu-id="d2931-113">Select Ctrl+Shift+P to open the command palette, and then enter **ADL: Download LocalRun Dependency** to download the packages.</span></span>  

   ![Скачивание пакетов зависимостей для локального запуска ADL](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/DownloadLocalRun.png)

2. <span data-ttu-id="d2931-115">Найдите пакеты зависимостей по пути, показанному на панели **вывода**, затем установите BuildTools и Win10SDK 10240.</span><span class="sxs-lookup"><span data-stu-id="d2931-115">Locate the dependency packages from the path shown in the **Output** pane, and then install BuildTools and Win10SDK 10240.</span></span> <span data-ttu-id="d2931-116">Пример пути:</span><span class="sxs-lookup"><span data-stu-id="d2931-116">Here is an example path:</span></span>  
`C:\Users\xxx\.vscode\extensions\usqlextpublisher.usql-vscode-ext-x.x.x\LocalRunDependency
`  
  <span data-ttu-id="d2931-117">![Поиск пакетов зависимостей](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/LocateDependencyPath.png)</span><span class="sxs-lookup"><span data-stu-id="d2931-117">![Locate the dependency packages](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/LocateDependencyPath.png)</span></span>

   <span data-ttu-id="d2931-118">а.</span><span class="sxs-lookup"><span data-stu-id="d2931-118">a.</span></span> <span data-ttu-id="d2931-119">Следуйте инструкциям мастера, чтобы установить BuildTools.</span><span class="sxs-lookup"><span data-stu-id="d2931-119">To install BuildTools, follow the wizard instructions.</span></span>   

  ![Установка BuildTools](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/InstallBuildTools.png)

   <span data-ttu-id="d2931-121">b.</span><span class="sxs-lookup"><span data-stu-id="d2931-121">b.</span></span> <span data-ttu-id="d2931-122">Следуйте инструкциям мастера, чтобы установить Win10SDK 10240.</span><span class="sxs-lookup"><span data-stu-id="d2931-122">To install Win10SDK 10240, follow the wizard instructions.</span></span>  

  ![Установка Win10SDK 10240](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/InstallWin10SDK.png)

3. <span data-ttu-id="d2931-124">Настройте переменную среды.</span><span class="sxs-lookup"><span data-stu-id="d2931-124">Set up the environment variable.</span></span> <span data-ttu-id="d2931-125">Установите для переменной среды **SCOPE_CPP_SDK** значение:</span><span class="sxs-lookup"><span data-stu-id="d2931-125">Set the **SCOPE_CPP_SDK** environment variable to:</span></span>  
`C:\Users\xxx\.vscode\extensions\usqlextpublisher.usql-vscode-ext-x.x.x\LocalRunDependency\CppSDK_3rdparty
`  
4. <span data-ttu-id="d2931-126">Перезапустите ОС, чтобы убедиться, что изменения переменных среды вступили в силу.</span><span class="sxs-lookup"><span data-stu-id="d2931-126">Restart the OS to make sure that the environment variable settings take effect.</span></span>  

   ![Проверка установки переменной среды SCOPE_CPP_SDK](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/ConfigScopeCppSDk.png)

## <a name="start-the-local-run-service-and-submit-the-u-sql-job-to-a-local-account"></a><span data-ttu-id="d2931-128">Локальный запуск службы и отправка задания U-SQL в локальную учетную запись</span><span class="sxs-lookup"><span data-stu-id="d2931-128">Start the local run service and submit the U-SQL job to a local account</span></span> 
<span data-ttu-id="d2931-129">Для новых пользователей будет предложено установить пакеты "ADL: скачать зависимости для локального запуска", если они еще не установлены.</span><span class="sxs-lookup"><span data-stu-id="d2931-129">For the first-time user, you are prompted to download the ADL: Download LocalRun Dependency packages if they are not already installed.</span></span>
1. <span data-ttu-id="d2931-130">Нажмите клавиши CTRL+SHIFT+P, чтобы открыть палитру команд, и введите **ADL: Start Local Run Service** (ADL: скачать зависимости для локального запуска).</span><span class="sxs-lookup"><span data-stu-id="d2931-130">Select Ctrl+Shift+P to open the command palette, and then enter **ADL: Start Local Run Service**.</span></span>
2. <span data-ttu-id="d2931-131">Выберите **Принять**, чтобы принять условия лицензионного соглашения об использовании программного обеспечения Майкрософт в первый раз.</span><span class="sxs-lookup"><span data-stu-id="d2931-131">Select **Accept** to accept the Microsoft Software License Terms for the first time.</span></span> 

   ![Принятие условий лицензионного соглашения об использовании программного обеспечения Майкрософт](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/AcceptEULA.png)   
3. <span data-ttu-id="d2931-133">Откроется консоль команд.</span><span class="sxs-lookup"><span data-stu-id="d2931-133">The cmd console opens.</span></span> <span data-ttu-id="d2931-134">Для новых пользователей введите **3**, а затем найдите локальную папку для входных и выходных данных.</span><span class="sxs-lookup"><span data-stu-id="d2931-134">For first-time users, you need to enter **3**, and then locate the local folder path for your data input and output.</span></span> <span data-ttu-id="d2931-135">Для остальных параметров можно использовать значения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="d2931-135">For other options, you can use the default values.</span></span> 

   ![Локальный запуск команд в средствах Data Lake для Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-run-cmd.png)
4. <span data-ttu-id="d2931-137">Нажмите клавиши CTRL+SHIFT+P, чтобы открыть палитру команд, введите **ADL: Submit Job** (ADL: отправить задание) и выберите **Локальный**, чтобы отправить задание в локальную учетную запись.</span><span class="sxs-lookup"><span data-stu-id="d2931-137">Select Ctrl+Shift+P to open the command palette, enter **ADL: Submit Job**, and then select **Local** to submit the job to your local account.</span></span>

   ![Выбор локальной учетной записи в средствах Data Lake для Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-select-local.png)
5. <span data-ttu-id="d2931-139">После отправки задания можно просмотреть сведения об отправке.</span><span class="sxs-lookup"><span data-stu-id="d2931-139">After you submit the job, you can view the submission details.</span></span> <span data-ttu-id="d2931-140">Чтобы просмотреть сведения об отправке, выберите **jobUrl** в окне **вывода**.</span><span class="sxs-lookup"><span data-stu-id="d2931-140">To view the submission details select **jobUrl** in the **Output** window.</span></span> <span data-ttu-id="d2931-141">Вы также можете просмотреть состояние отправки задания в консоли команд.</span><span class="sxs-lookup"><span data-stu-id="d2931-141">You can also view the job submission status from the cmd console.</span></span> <span data-ttu-id="d2931-142">Для просмотра сведений о задании в консоли команд введите **7**.</span><span class="sxs-lookup"><span data-stu-id="d2931-142">Enter **7** in the cmd console if you want to know more job details.</span></span>

   <span data-ttu-id="d2931-143">![Результат локального запуска для средств Data Lake в Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-run-result.png)
   ![Состояние локального запуска команды для средств Data Lake в Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-localrun-cmd-status.png)</span><span class="sxs-lookup"><span data-stu-id="d2931-143">![Data Lake Tools for Visual Studio Code local run output](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-run-result.png)
![Data Lake Tools for Visual Studio Code local run cmd status](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-localrun-cmd-status.png)</span></span> 


## <a name="start-a-local-debug-for-the-u-sql-job"></a><span data-ttu-id="d2931-144">Запуск локальной отладки для задания U-SQL</span><span class="sxs-lookup"><span data-stu-id="d2931-144">Start a local debug for the U-SQL job</span></span>  
<span data-ttu-id="d2931-145">Для новых пользователей будет предложено установить пакеты "ADL: скачать зависимости для локального запуска", если они еще не установлены.</span><span class="sxs-lookup"><span data-stu-id="d2931-145">For the first-time user, you are prompted to download the ADL: Download LocalRun Dependency packages if they are not already installed.</span></span>
  
1. <span data-ttu-id="d2931-146">Нажмите клавиши CTRL+SHIFT+P, чтобы открыть палитру команд, и введите **ADL: Start Local Run Service** (ADL: скачать зависимости для локального запуска).</span><span class="sxs-lookup"><span data-stu-id="d2931-146">Select Ctrl+Shift+P to open the command palette, and then enter **ADL: Start Local Run Service**.</span></span> <span data-ttu-id="d2931-147">Откроется консоль команд.</span><span class="sxs-lookup"><span data-stu-id="d2931-147">The cmd console opens.</span></span> <span data-ttu-id="d2931-148">Убедитесь, что установлено значение параметра **DataRoot**.</span><span class="sxs-lookup"><span data-stu-id="d2931-148">Make sure that the **DataRoot** is set.</span></span>
3. <span data-ttu-id="d2931-149">Установите точку останова в коде программной части C#.</span><span class="sxs-lookup"><span data-stu-id="d2931-149">Set a breakpoint in your C# code-behind.</span></span>
4. <span data-ttu-id="d2931-150">Вернитесь в редактор скриптов, нажмите клавиши CTRL+SHIFT+P, чтобы открыть командную консоль, а затем введите **Local Debug** (Локальная отладка) для запуска службы локальной отладки.</span><span class="sxs-lookup"><span data-stu-id="d2931-150">Back in the script editor, select Ctrl+Shift+P to open the command console, and then enter **Local Debug** to start your local debug service.</span></span>

![Результат локальной отладки в средствах Data Lake для Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-debug-result.png)


## <a name="next-steps"></a><span data-ttu-id="d2931-152">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d2931-152">Next steps</span></span>
- <span data-ttu-id="d2931-153">Сведения об использовании средств Azure Data Lake для Visual Studio Code см. в статье [Использование средств Azure Data Lake для Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).</span><span class="sxs-lookup"><span data-stu-id="d2931-153">For using Azure Data Lake Tools for Visual Studio Code, see [Use Azure Data Lake Tools for Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).</span></span>
- <span data-ttu-id="d2931-154">Дополнительные сведения о начале работы с Data Lake Analytics см. в статье [Начало работы с Azure Data Lake Analytics с помощью портала Azure](data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d2931-154">For getting started information on Data Lake Analytics, see [Tutorial: Get started with Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md).</span></span>
- <span data-ttu-id="d2931-155">Дополнительные сведения об использовании средств Data Lake для U-SQL см. в статье [Разработка скриптов U-SQL с помощью средств Data Lake для Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d2931-155">For information about Data Lake Tools for Visual Studio, see [Tutorial: Develop U-SQL scripts by using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
- <span data-ttu-id="d2931-156">Сведения о разработке сборок см. в статье [Разработка сборок U-SQL для заданий Azure Data Lake Analytics](data-lake-analytics-u-sql-develop-assemblies.md).</span><span class="sxs-lookup"><span data-stu-id="d2931-156">For the information on developing assemblies, see [Develop U-SQL assemblies for Azure Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-assemblies.md).</span></span>
