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
# <a name="u-sql-local-run-and-local-debug-with-visual-studio-code"></a>Локальный запуск и локальная отладка U-SQL в Visual Studio Code

## <a name="prerequisites"></a>Предварительные требования
Убедитесь, что у вас есть следующие необходимые условия, прежде чем начать эти процедуры hello:
- Средства Azure Data Lake для Visual Studio Code. Инструкции см. в статье [Использование средств Azure Data Lake для Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).
- C# для кода на Visual Studio (если локальной отладки tooperform U-SQL).

   ![Установка C# в средствах Data Lake для Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-install-ms-vscodecsharp.png)
   
   > [!NOTE]
   > Здравствуйте, локального запуска U-SQL и средств отладки в настоящее время поддерживается только пользователей Windows. 


## <a name="set-up-hello-u-sql-local-run-environment"></a>Настройка среды локального выполнения U-SQL hello

1. Выберите палитру команд hello tooopen Ctrl + Shift + P, а затем введите **ADL: загрузить зависимостей LocalRun** toodownload hello пакетов.  

   ![Загрузить пакеты зависимостей LocalRun ADL hello](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/DownloadLocalRun.png)

2. Найдите пакеты зависимостей hello из путь hello hello **выходные данные** области и установите BuildTools и Win10SDK 10240. Пример пути:  
`C:\Users\xxx\.vscode\extensions\usqlextpublisher.usql-vscode-ext-x.x.x\LocalRunDependency
`  
  ![Найдите пакеты зависимостей hello](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/LocateDependencyPath.png)

   а. tooinstall BuildTools, следуйте инструкциям мастера hello.   

  ![Установка BuildTools](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/InstallBuildTools.png)

   b. tooinstall Win10SDK 10240, следуйте инструкциям мастера hello.  

  ![Установка Win10SDK 10240](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/InstallWin10SDK.png)

3. Настройте переменную среды hello. Набор hello **SCOPE_CPP_SDK** переменной среды:  
`C:\Users\xxx\.vscode\extensions\usqlextpublisher.usql-vscode-ext-x.x.x\LocalRunDependency\CppSDK_3rdparty
`  
4. Перезапустите hello ОС toomake убедиться, что hello параметров переменных среды вступили в силу.  

   ![Убедитесь, что устанавливается переменная среды SCOPE_CPP_SDK hello](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/ConfigScopeCppSDk.png)

## <a name="start-hello-local-run-service-and-submit-hello-u-sql-job-tooa-local-account"></a>Запуск службы локального выполнения hello и отправьте hello U-SQL задания tooa локальной учетной записи 
Hello первом входе в систему, не запрошенные toodownload hello ADL: загрузить LocalRun зависимостей пакетов, если они еще не установлены.
1. Выберите палитру команд hello tooopen Ctrl + Shift + P, а затем введите **ADL: запуск службы локального запуска**.
2. Выберите **Accept** tooaccept hello лицензионного соглашения Майкрософт для hello первый раз. 

   ![Примите условия лицензии программного обеспечения Microsoft hello](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/AcceptEULA.png)   
3. Откроется консоль cmd Hello. Для пользователей, впервые, необходимо tooenter **3**, а затем найдите hello локальный путь к папке для входных и выходных данных. Чтобы задать другие параметры можно использовать значения по умолчанию hello. 

   ![Локальный запуск команд в средствах Data Lake для Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-run-cmd.png)
4. Выберите палитру команд hello tooopen Ctrl + Shift + P, введите **ADL: отправить задание**и выберите **локального** toosubmit hello задания tooyour локальной учетной записи.

   ![Выбор локальной учетной записи в средствах Data Lake для Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-select-local.png)
5. После отправки задания hello, можно просмотреть сведения об отправке hello. tooview hello отправки сведений выберите **jobUrl** в hello **вывода** окна. Можно также просмотреть состояние отправки задания hello из консоли cmd hello. Введите **7** в консоли cmd hello Если tooknow Дополнительные сведения о задании.

   ![Результат локального запуска для средств Data Lake в Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-run-result.png)
   ![Состояние локального запуска команды для средств Data Lake в Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-localrun-cmd-status.png) 


## <a name="start-a-local-debug-for-hello-u-sql-job"></a>Запуск локальной отладки для задания hello U-SQL  
Hello первом входе в систему, не запрошенные toodownload hello ADL: загрузить LocalRun зависимостей пакетов, если они еще не установлены.
  
1. Выберите палитру команд hello tooopen Ctrl + Shift + P, а затем введите **ADL: запуск службы локального запуска**. Откроется консоль cmd Hello. Убедитесь в том, что hello **DataRoot** имеет значение.
3. Установите точку останова в коде программной части C#.
4. Вернитесь в редакторе сценариев hello, выберите сочетание клавиш Ctrl + Shift + P tooopen hello командной консоли, а затем введите **локальной отладки** toostart локальной отладки службы.

![Результат локальной отладки в средствах Data Lake для Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-debug-result.png)


## <a name="next-steps"></a>Дальнейшие действия
- Сведения об использовании средств Azure Data Lake для Visual Studio Code см. в статье [Использование средств Azure Data Lake для Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).
- Дополнительные сведения о начале работы с Data Lake Analytics см. в статье [Начало работы с Azure Data Lake Analytics с помощью портала Azure](data-lake-analytics-get-started-portal.md).
- Дополнительные сведения об использовании средств Data Lake для U-SQL см. в статье [Разработка скриптов U-SQL с помощью средств Data Lake для Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).
- Hello сведения о разработке сборок см. в разделе [сборки разрабатывать U-SQL для задания аналитики Озера данных Azure](data-lake-analytics-u-sql-develop-assemblies.md).
