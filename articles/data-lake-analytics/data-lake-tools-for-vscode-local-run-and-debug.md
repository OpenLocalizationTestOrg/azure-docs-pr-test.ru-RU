---
title: "Средства Azure Data Lake — локальный запуск и локальная отладка U-SQL в Visual Studio Code | Документация Майкрософт"
description: "Узнайте, как отлаживать toouse средства Озера данных Azure для Visual Studio Code toolocal выполнения и локальные."
Keywords: "VScode, средства Озера данных Azure, локального выполнения файла хранилища предварительного просмотра локальной отладки, локальной отладки, отправьте toostorage путь"
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
ms.openlocfilehash: fb152f07fe8c4b03dde8fb8e62c7475eccda0578
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="u-sql-local-run-and-local-debug-with-visual-studio-code"></a><span data-ttu-id="fc606-104">Локальный запуск и локальная отладка U-SQL в Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="fc606-104">U-SQL local run and local debug with Visual Studio Code</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fc606-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="fc606-105">Prerequisites</span></span>
<span data-ttu-id="fc606-106">Убедитесь, что у вас есть следующие необходимые условия, прежде чем начать эти процедуры hello:</span><span class="sxs-lookup"><span data-stu-id="fc606-106">Make sure you have hello following prerequisites in place before you start these procedures:</span></span>
- <span data-ttu-id="fc606-107">Средства Azure Data Lake для Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="fc606-107">Azure Data Lake Tool for Visual Studio Code.</span></span> <span data-ttu-id="fc606-108">Инструкции см. в статье [Использование средств Azure Data Lake для Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).</span><span class="sxs-lookup"><span data-stu-id="fc606-108">For instructions, see [Use Azure Data Lake Tools for Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).</span></span>
- <span data-ttu-id="fc606-109">C# для кода на Visual Studio (если локальной отладки tooperform U-SQL).</span><span class="sxs-lookup"><span data-stu-id="fc606-109">C# for Visual Studio Code (if you want tooperform a U-SQL local debug).</span></span>

   ![Установка C# в средствах Data Lake для Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-install-ms-vscodecsharp.png)
   
   > [!NOTE]
   > <span data-ttu-id="fc606-111">Здравствуйте, локального запуска U-SQL и средств отладки в настоящее время поддерживается только пользователей Windows.</span><span class="sxs-lookup"><span data-stu-id="fc606-111">hello U-SQL local run and debug features currently only support Windows users.</span></span> 


## <a name="set-up-hello-u-sql-local-run-environment"></a><span data-ttu-id="fc606-112">Настройка среды локального выполнения U-SQL hello</span><span class="sxs-lookup"><span data-stu-id="fc606-112">Set up hello U-SQL local run environment</span></span>

1. <span data-ttu-id="fc606-113">Выберите палитру команд hello tooopen Ctrl + Shift + P, а затем введите **ADL: загрузить зависимостей LocalRun** toodownload hello пакетов.</span><span class="sxs-lookup"><span data-stu-id="fc606-113">Select Ctrl+Shift+P tooopen hello command palette, and then enter **ADL: Download LocalRun Dependency** toodownload hello packages.</span></span>  

   ![Загрузить пакеты зависимостей LocalRun ADL hello](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/DownloadLocalRun.png)

2. <span data-ttu-id="fc606-115">Найдите пакеты зависимостей hello из путь hello hello **выходные данные** области и установите BuildTools и Win10SDK 10240.</span><span class="sxs-lookup"><span data-stu-id="fc606-115">Locate hello dependency packages from hello path shown in hello **Output** pane, and then install BuildTools and Win10SDK 10240.</span></span> <span data-ttu-id="fc606-116">Пример пути:</span><span class="sxs-lookup"><span data-stu-id="fc606-116">Here is an example path:</span></span>  
`C:\Users\xxx\.vscode\extensions\usqlextpublisher.usql-vscode-ext-x.x.x\LocalRunDependency
`  
  <span data-ttu-id="fc606-117">![Найдите пакеты зависимостей hello](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/LocateDependencyPath.png)</span><span class="sxs-lookup"><span data-stu-id="fc606-117">![Locate hello dependency packages](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/LocateDependencyPath.png)</span></span>

   <span data-ttu-id="fc606-118">а.</span><span class="sxs-lookup"><span data-stu-id="fc606-118">a.</span></span> <span data-ttu-id="fc606-119">tooinstall BuildTools, следуйте инструкциям мастера hello.</span><span class="sxs-lookup"><span data-stu-id="fc606-119">tooinstall BuildTools, follow hello wizard instructions.</span></span>   

  ![Установка BuildTools](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/InstallBuildTools.png)

   <span data-ttu-id="fc606-121">b.</span><span class="sxs-lookup"><span data-stu-id="fc606-121">b.</span></span> <span data-ttu-id="fc606-122">tooinstall Win10SDK 10240, следуйте инструкциям мастера hello.</span><span class="sxs-lookup"><span data-stu-id="fc606-122">tooinstall Win10SDK 10240, follow hello wizard instructions.</span></span>  

  ![Установка Win10SDK 10240](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/InstallWin10SDK.png)

3. <span data-ttu-id="fc606-124">Настройте переменную среды hello.</span><span class="sxs-lookup"><span data-stu-id="fc606-124">Set up hello environment variable.</span></span> <span data-ttu-id="fc606-125">Набор hello **SCOPE_CPP_SDK** переменной среды:</span><span class="sxs-lookup"><span data-stu-id="fc606-125">Set hello **SCOPE_CPP_SDK** environment variable to:</span></span>  
`C:\Users\xxx\.vscode\extensions\usqlextpublisher.usql-vscode-ext-x.x.x\LocalRunDependency\CppSDK_3rdparty
`  
4. <span data-ttu-id="fc606-126">Перезапустите hello ОС toomake убедиться, что hello параметров переменных среды вступили в силу.</span><span class="sxs-lookup"><span data-stu-id="fc606-126">Restart hello OS toomake sure that hello environment variable settings take effect.</span></span>  

   ![Убедитесь, что устанавливается переменная среды SCOPE_CPP_SDK hello](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/ConfigScopeCppSDk.png)

## <a name="start-hello-local-run-service-and-submit-hello-u-sql-job-tooa-local-account"></a><span data-ttu-id="fc606-128">Запуск службы локального выполнения hello и отправьте hello U-SQL задания tooa локальной учетной записи</span><span class="sxs-lookup"><span data-stu-id="fc606-128">Start hello local run service and submit hello U-SQL job tooa local account</span></span> 
<span data-ttu-id="fc606-129">Hello первом входе в систему, не запрошенные toodownload hello ADL: загрузить LocalRun зависимостей пакетов, если они еще не установлены.</span><span class="sxs-lookup"><span data-stu-id="fc606-129">For hello first-time user, you are prompted toodownload hello ADL: Download LocalRun Dependency packages if they are not already installed.</span></span>
1. <span data-ttu-id="fc606-130">Выберите палитру команд hello tooopen Ctrl + Shift + P, а затем введите **ADL: запуск службы локального запуска**.</span><span class="sxs-lookup"><span data-stu-id="fc606-130">Select Ctrl+Shift+P tooopen hello command palette, and then enter **ADL: Start Local Run Service**.</span></span>
2. <span data-ttu-id="fc606-131">Выберите **Accept** tooaccept hello лицензионного соглашения Майкрософт для hello первый раз.</span><span class="sxs-lookup"><span data-stu-id="fc606-131">Select **Accept** tooaccept hello Microsoft Software License Terms for hello first time.</span></span> 

   ![Примите условия лицензии программного обеспечения Microsoft hello](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/AcceptEULA.png)   
3. <span data-ttu-id="fc606-133">Откроется консоль cmd Hello.</span><span class="sxs-lookup"><span data-stu-id="fc606-133">hello cmd console opens.</span></span> <span data-ttu-id="fc606-134">Для пользователей, впервые, необходимо tooenter **3**, а затем найдите hello локальный путь к папке для входных и выходных данных.</span><span class="sxs-lookup"><span data-stu-id="fc606-134">For first-time users, you need tooenter **3**, and then locate hello local folder path for your data input and output.</span></span> <span data-ttu-id="fc606-135">Чтобы задать другие параметры можно использовать значения по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="fc606-135">For other options, you can use hello default values.</span></span> 

   ![Локальный запуск команд в средствах Data Lake для Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-run-cmd.png)
4. <span data-ttu-id="fc606-137">Выберите палитру команд hello tooopen Ctrl + Shift + P, введите **ADL: отправить задание**и выберите **локального** toosubmit hello задания tooyour локальной учетной записи.</span><span class="sxs-lookup"><span data-stu-id="fc606-137">Select Ctrl+Shift+P tooopen hello command palette, enter **ADL: Submit Job**, and then select **Local** toosubmit hello job tooyour local account.</span></span>

   ![Выбор локальной учетной записи в средствах Data Lake для Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-select-local.png)
5. <span data-ttu-id="fc606-139">После отправки задания hello, можно просмотреть сведения об отправке hello.</span><span class="sxs-lookup"><span data-stu-id="fc606-139">After you submit hello job, you can view hello submission details.</span></span> <span data-ttu-id="fc606-140">tooview hello отправки сведений выберите **jobUrl** в hello **вывода** окна.</span><span class="sxs-lookup"><span data-stu-id="fc606-140">tooview hello submission details select **jobUrl** in hello **Output** window.</span></span> <span data-ttu-id="fc606-141">Можно также просмотреть состояние отправки задания hello из консоли cmd hello.</span><span class="sxs-lookup"><span data-stu-id="fc606-141">You can also view hello job submission status from hello cmd console.</span></span> <span data-ttu-id="fc606-142">Введите **7** в консоли cmd hello Если tooknow Дополнительные сведения о задании.</span><span class="sxs-lookup"><span data-stu-id="fc606-142">Enter **7** in hello cmd console if you want tooknow more job details.</span></span>

   <span data-ttu-id="fc606-143">![Результат локального запуска для средств Data Lake в Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-run-result.png)
   ![Состояние локального запуска команды для средств Data Lake в Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-localrun-cmd-status.png)</span><span class="sxs-lookup"><span data-stu-id="fc606-143">![Data Lake Tools for Visual Studio Code local run output](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-run-result.png)
![Data Lake Tools for Visual Studio Code local run cmd status](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-localrun-cmd-status.png)</span></span> 


## <a name="start-a-local-debug-for-hello-u-sql-job"></a><span data-ttu-id="fc606-144">Запуск локальной отладки для задания hello U-SQL</span><span class="sxs-lookup"><span data-stu-id="fc606-144">Start a local debug for hello U-SQL job</span></span>  
<span data-ttu-id="fc606-145">Hello первом входе в систему, не запрошенные toodownload hello ADL: загрузить LocalRun зависимостей пакетов, если они еще не установлены.</span><span class="sxs-lookup"><span data-stu-id="fc606-145">For hello first-time user, you are prompted toodownload hello ADL: Download LocalRun Dependency packages if they are not already installed.</span></span>
  
1. <span data-ttu-id="fc606-146">Выберите палитру команд hello tooopen Ctrl + Shift + P, а затем введите **ADL: запуск службы локального запуска**.</span><span class="sxs-lookup"><span data-stu-id="fc606-146">Select Ctrl+Shift+P tooopen hello command palette, and then enter **ADL: Start Local Run Service**.</span></span> <span data-ttu-id="fc606-147">Откроется консоль cmd Hello.</span><span class="sxs-lookup"><span data-stu-id="fc606-147">hello cmd console opens.</span></span> <span data-ttu-id="fc606-148">Убедитесь в том, что hello **DataRoot** имеет значение.</span><span class="sxs-lookup"><span data-stu-id="fc606-148">Make sure that hello **DataRoot** is set.</span></span>
3. <span data-ttu-id="fc606-149">Установите точку останова в коде программной части C#.</span><span class="sxs-lookup"><span data-stu-id="fc606-149">Set a breakpoint in your C# code-behind.</span></span>
4. <span data-ttu-id="fc606-150">Вернитесь в редакторе сценариев hello, выберите сочетание клавиш Ctrl + Shift + P tooopen hello командной консоли, а затем введите **локальной отладки** toostart локальной отладки службы.</span><span class="sxs-lookup"><span data-stu-id="fc606-150">Back in hello script editor, select Ctrl+Shift+P tooopen hello command console, and then enter **Local Debug** toostart your local debug service.</span></span>

![Результат локальной отладки в средствах Data Lake для Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-debug-result.png)


## <a name="next-steps"></a><span data-ttu-id="fc606-152">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fc606-152">Next steps</span></span>
- <span data-ttu-id="fc606-153">Сведения об использовании средств Azure Data Lake для Visual Studio Code см. в статье [Использование средств Azure Data Lake для Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).</span><span class="sxs-lookup"><span data-stu-id="fc606-153">For using Azure Data Lake Tools for Visual Studio Code, see [Use Azure Data Lake Tools for Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).</span></span>
- <span data-ttu-id="fc606-154">Дополнительные сведения о начале работы с Data Lake Analytics см. в статье [Начало работы с Azure Data Lake Analytics с помощью портала Azure](data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="fc606-154">For getting started information on Data Lake Analytics, see [Tutorial: Get started with Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md).</span></span>
- <span data-ttu-id="fc606-155">Дополнительные сведения об использовании средств Data Lake для U-SQL см. в статье [Разработка скриптов U-SQL с помощью средств Data Lake для Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="fc606-155">For information about Data Lake Tools for Visual Studio, see [Tutorial: Develop U-SQL scripts by using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
- <span data-ttu-id="fc606-156">Hello сведения о разработке сборок см. в разделе [сборки разрабатывать U-SQL для задания аналитики Озера данных Azure](data-lake-analytics-u-sql-develop-assemblies.md).</span><span class="sxs-lookup"><span data-stu-id="fc606-156">For hello information on developing assemblies, see [Develop U-SQL assemblies for Azure Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-assemblies.md).</span></span>
