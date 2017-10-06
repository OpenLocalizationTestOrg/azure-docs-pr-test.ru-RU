---
title: "aaaAzure установки среды выполнения функции | Документы Microsoft"
description: "Как tooInstall hello среды выполнения функций Azure"
services: functions
documentationcenter: 
author: apwestgarth
manager: stefsch
editor: 
ms.assetid: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 05/08/2017
ms.author: anwestg
ms.openlocfilehash: 67c6d10b5c0ac43e880d29cff0ae7b099f82bdb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="install-hello-azure-functions-runtime-preview"></a>Установка hello предварительной версии Azure функции среды выполнения

При желании tooinstall hello среды выполнения функций Azure preview, необходимо выполнить следующие действия:

1. Убедитесь, что компьютер передает hello минимальные требования
1. Загрузите hello [установщик предварительного выполнения функций Azure](https://aka.ms/azafr). 
1. Установка среды выполнения функций Azure preview hello
1. Полный hello конфигурации предварительной версии среды выполнения Azure функции hello

## <a name="prerequisites"></a>Предварительные требования

Перед установкой предварительной версии среды выполнения Azure функции hello, необходимо иметь следующие hello.

1. Компьютер под управлением Microsoft Windows Server 2016 или обновление Microsoft Windows 10 для дизайнеров (Professional или Enterprise Edition).
1. Экземпляр SQL Server в вашей сети.  Минимальное требование по выпуску — SQL Server Express.

## <a name="install-hello-azure-functions-runtime-preview"></a>Установка hello предварительной версии Azure функции среды выполнения

Установщик предварительной версии среды выполнения Azure функции Hello поможет выполнить установку hello предварительной версии среды выполнения Azure функции hello управления и рабочих ролей.  Возможные tooinstall hello управления и рабочей роли в hello же компьютере.  Тем не менее как добавить дополнительные функции, необходимо развернуть дополнительные рабочие роли на возможности tooscale toobe дополнительных компьютеров функций на несколько рабочих процессов.

## <a name="install-hello-management-and-worker-role-on-hello-same-machine"></a>Установите на hello hello управления и рабочая роль одном компьютере

1. Запустите установщик предварительной версии среды выполнения Azure функции hello.

    ![Установщик предварительной версии среды выполнения Функций Azure][1]

1. **Нажмите кнопку Далее** Авансовая за первый этап hello установщика hello
1. После прочтения hello условия hello **лицензионное соглашение**, **флажок hello** tooaccept hello условия и **нажмите кнопку Далее** tooadvance.
1. Теперь выберите hello ролей требуется tooinstall на этом компьютере **роль функций управления** и/или **функции рабочей роли** и **нажмите кнопку Далее.**

    ![Установщик предварительной версии среды выполнения Функций Azure. Выбор роли][3]

    > [!NOTE]
    > Вы можете установить hello **функции рабочей роли** на многих других машин toodo таким образом, выполните следующие действия и выбрать только **функции рабочей роли** в установщике hello.

1. **Нажмите кнопку Далее** toohave hello **установщика среды выполнения Azure функции** устанавливается на компьютере.
1. После завершения hello установщика запустит hello **средство настройки среды выполнения Azure функции**.

    ![Установщик предварительной версии среды выполнения Функций Azure — завершение][5]

    > [!NOTE]
    > Если вы устанавливаете на **Windows 10** и hello **контейнера** функция не включена ранее, hello **выполнения функции Azure** установщик предложит tooreboot Установите hello toocomplete вашего компьютера.

## <a name="configure-hello-azure-functions-runtime"></a>Настройка среды выполнения Azure функции hello

Здравствуйте, toocomplete установки среды выполнения функции Azure, необходимо выполнить настройку hello.

1. Hello **средство настройки среды выполнения Azure функции** показывает, какие роли установлены на компьютере.

    ![Инструмент настройки предварительной версии среды выполнения Функций Azure][6]

1. Нажмите кнопку hello **базы данных** введите hello **сведения о соединении для экземпляра SQL Server** и **нажмите кнопку Применить**.  Это необходимо в порядке toohello toocreate среды выполнения Azure функции hello toosupport базы данных времени выполнения.
    
    ![Настройка базы данных предварительной версии среды выполнения Функций Azure][7]

1. Нажмите кнопку hello **учетные данные** вкладки.  На этом экране необходимо создать две пары учетных данных для использования с общей папкой для размещения всех Функций Azure.  **Укажите имя пользователя и пароль** комбинации для hello **владельца общей папки** и для hello **пользователя общего файлового ресурса** и нажмите кнопку **применить**.

    ![Учетные данные предварительной версии среды выполнения Функций Azure][8]

1. Нажмите кнопку hello **общей папки** вкладки.  На этом экране необходимо указать подробности hello hello **расположение общей папки**.  Она может быть создана автоматически, или вы можете использовать имеющуюся общую папку и нажать кнопку **Применить**.  Если выбрать новое расположение общей папки, необходимо указать каталог для использования с hello среды выполнения функций Azure.
    
    ![Предварительная версия среды выполнения Функций Azure — общая папка][9]

1. Нажмите кнопку hello **IIS** вкладки.  На этой вкладке отображаются подробные сведения об hello hello веб-сайтов в службах IIS, создаваемых установки среды выполнения Azure функции hello.  **Нажмите кнопку Применить** toocomplete.

    ![Предварительная версия среды выполнения Функций Azure — IIS][10]

1. Нажмите кнопку hello **служб** вкладки.  На этой вкладке отображается состояние hello служб hello в установке среды выполнения функций Azure.  Если после начальной настройки hello **службы активации узла Azure функции** не запущена, нажмите **запуск службы**

    ![Предварительная версия среды выполнения Функций Azure — завершение настройки][11]

1. Наконец Обзор toohello **портала среды выполнения Azure функции** как`https://<machinename>/`

    ![Портал предварительной версии среды выполнения Функций Azure][12]


<!--Image references-->
[1]: ./media/functions-runtime-install/AzureFunctionsRuntime_Installer1.png
[2]: ./media/functions-runtime-install/AzureFunctionsRuntime_Installer2-EULA.png
[3]: ./media/functions-runtime-install/AzureFunctionsRuntime_Installer3-ChooseRoles.png
[4]: ./media/functions-runtime-install/AzureFunctionsRuntime_Installer4-Install.png
[5]: ./media/functions-runtime-install/AzureFunctionsRuntime_Installer5-InstallComplete.png
[6]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration1.png
[7]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration2_SQL.png
[8]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration3_Credentials.png
[9]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration4_Fileshare.png
[10]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration5_IIS.png
[11]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration6_Services.png
[12]: ./media/functions-runtime-install/AzureFunctionsRuntime_Portal.png