---
title: "роли hello aaaConfigure для Azure облачной службы с помощью Visual Studio | Документы Microsoft"
description: "Узнайте, как tooset и Настройка ролей для облачных служб Azure с помощью Visual Studio."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: d397ef87-64e5-401a-aad5-7f83f1022e16
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/21/2017
ms.author: kraigb
ms.openlocfilehash: d3c62eb57040ebe987787e73b17b468bb82122bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-cloud-service-roles-with-visual-studio"></a>Настройка ролей для облачной службы Azure в Visual Studio
Облачной службе Azure можно назначить одну или несколько рабочих ролей или веб-ролей. Для каждой роли требуется toodefine, как настроить эту роль и также настроить способ выполнения этой роли. toolearn Дополнительные сведения о ролях в облачных службах см. видео hello [tooAzure введение облачные службы](https://channel9.msdn.com/Series/Windows-Azure-Cloud-Services-Tutorials/Introduction-to-Windows-Azure-Cloud-Services). 

Hello для облачной службы хранится в hello следующие файлы:

- **ServiceDefinition.csdef** -hello файла определения службы определяет параметры среды выполнения hello для облачной службы, включая какие роли являются обязательными, конечные точки и размер виртуальной машины. Ни один из hello данные, хранящиеся в `ServiceDefinition.csdef` можно изменить, если ваша роль выполняется.
- **ServiceConfiguration.cscfg** - файл конфигурации службы hello настраивает, сколько экземпляров роли выполняются и значения hello hello параметров, определенных для роли. Здравствуйте, данные, хранящиеся в `ServiceConfiguration.cscfg` можно изменить во время вашей роли.

toostore разные значения для hello параметры, управляющие ходом роли, можно определить несколько конфигураций службы. Разные конфигурации службы можно использовать для разных сред развертывания. Например можно задать вашей учетной записи подключения строка toouse hello локального хранилища Azure эмулятор хранилища в конфигурации локальной службы и создать другой toouse конфигурации службы хранилища Azure в облаке hello.

При создании облачной службы Azure в Visual Studio две конфигурации службы создаются автоматически и добавлены tooyour проекта Azure:

- `ServiceConfiguration.Cloud.cscfg`
- `ServiceConfiguration.Local.cscfg`

## <a name="configure-an-azure-cloud-service"></a>Настройка облачной службы Azure
Можно настроить облачную службу Azure из обозревателя решений в Visual Studio, как показано в hello следующие шаги:

1. Создайте или откройте проект облачной службы Azure в среде Visual Studio.

1. В **обозревателе решений**, щелкните правой кнопкой мыши проект hello и hello контекстном меню, выберите **свойства**.
   
    ![Контекстное меню проекта в обозревателе решений](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-project-context-menu.png)

1. На странице свойств проекта hello, выберите hello **разработки** вкладки. 

    ![Страница свойств проекта — вкладка "Разработка"](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-development-tab.png)

1. В hello **конфигурации службы** список, выберите hello имя конфигурации службы hello, что требуется tooedit. (Toomake изменения конфигурации службы hello tooall для этой роли, установите **все конфигурации**.)
   
    > [!IMPORTANT]
    > При выборе конкретной конфигурации службы некоторые ее свойства будут отключены, так как их можно задать только для всех конфигураций. tooedit эти свойства, необходимо выбрать **все конфигурации**.
    > 
    > 
   
    ![Список конфигураций службы для облачной службы Azure](./media/vs-azure-tools-configure-roles-for-cloud-service/cloud-service-service-configuration-property.png)

## <a name="change-hello-number-of-role-instances"></a>Изменение hello число экземпляров роли
tooimprove hello производительность облачной службы, можно изменить hello числа экземпляров роли, работающих под управлением, основываясь на номере hello пользователей или нагрузки hello, ожидаемый для определенной роли. Отдельная виртуальная машина создается для каждого экземпляра роли при hello облачной службы в Azure. Это влияет на выставление счетов hello hello развертывания облачной службы. Дополнительные сведения о плате за использование Azure см. в статье [Расшифровка счета за использование Microsoft Azure](billing/billing-understand-your-bill.md).

1. Создайте или откройте проект облачной службы Azure в среде Visual Studio.

1. В **обозревателе решений**, разверните узел проекта hello. В разделе hello **ролей** узел, щелкните правой кнопкой мыши роль hello tooupdate и, hello контекстном меню, выберите **свойства**.

    ![Контекстное меню роли в обозревателе решений Azure](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. Выберите hello **конфигурации** вкладки.

    ![Вкладка "Конфигурация"](./media/vs-azure-tools-configure-roles-for-cloud-service/role-configuration-properties-page.png)

1. В hello **конфигурации службы** список, выберите hello конфигурации службы, что требуется tooupdate.
   
    ![Список "Конфигурация службы"](./media/vs-azure-tools-configure-roles-for-cloud-service/role-configuration-properties-page-select-configuration.png)

1. В hello **число экземпляров** текста введите hello число экземпляров, что требуется toostart для этой роли. Каждый экземпляр выполняется на отдельной виртуальной машине, при публикации службы tooAzure hello облака.

    ![Обновление hello число экземпляров](./media/vs-azure-tools-configure-roles-for-cloud-service/role-configuration-properties-page-instance-count.png)

1. Из Visual Studio hello панели инструментов выберите **Сохранить**.

## <a name="manage-connection-strings-for-storage-accounts"></a>Управление строками подключения для учетных записей хранения
Вы можете добавлять, удалять или изменять строки подключения для конфигураций службы. Например, вы можете использовать строку локального подключения для конфигурации локальной службы, которая имеет значение `UseDevelopmentStorage=true`. Может также потребоваться tooconfigure конфигурацию облачной службы, который использует учетную запись хранилища в Azure.

> [!WARNING]
> При вводе hello хранилища Azure ключ доступа для строки подключения учетной записи хранилища, эти сведения сохраняются локально в файле конфигурации службы hello. Тем не менее эти сведения в настоящее время не хранятся в виде зашифрованного текста.
> 
> 

Используя другое значение для каждой конфигурации службы, не имеют toouse различные строки подключения в облачной службе или модифицировать код при публикации на tooAzure облачной службы. Можно использовать одно имя для строки подключения hello в ваш код и hello значение отличается, зависит от конфигурации службы hello, выбранной при построении облачной службы или при его публикации приветствия.

1. Создайте или откройте проект облачной службы Azure в среде Visual Studio.

1. В **обозревателе решений**, разверните узел проекта hello. В разделе hello **ролей** узел, щелкните правой кнопкой мыши роль hello tooupdate и, hello контекстном меню, выберите **свойства**.

    ![Контекстное меню роли в обозревателе решений Azure](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. Выберите hello **параметры** вкладки.

    ![Вкладка "Параметры"](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab.png)

1. В hello **конфигурации службы** список, выберите hello конфигурации службы, что требуется tooupdate.

    ![Конфигурация службы](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-select-configuration.png)

1. Выберите строку подключения tooadd **добавить параметр**.

    ![Добавление строки подключения](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting.png)

1. После списка toohello добавления нового параметра hello, обновите строку hello в списке hello hello необходимых сведений.

    ![Новая строка подключения](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting-new-setting.png)

    - **Имя** -введите имя hello, что необходимо toouse для строки подключения hello.
    - **Тип** — выберите **строка подключения** из раскрывающегося списка hello.
    - **Значение** -hello строку подключения можно вводить непосредственно в hello **значение** ячейки или toowork hello выберите кнопку с многоточием (...) в hello **Создание строки подключения хранилища** диалогового окна.  

1. В hello **Создание строки подключения хранилища** диалоговое окно, выберите один из вариантов для **подключение с использованием**. Следуйте инструкциям hello для выбранных параметров hello:

    - **Эмулятор хранилища Microsoft Azure** -отключены при выборе этого параметра hello остальные параметры в диалоговом окне приветствия, как они характерны только tooAzure. Нажмите кнопку **ОК**.
    - **Подписки** — Если вы установите этот параметр, использовать hello раскрывающегося списка tooeither выбирать и входа в учетную запись Майкрософт или добавить учетную запись Майкрософт. Выберите подписку и учетную запись хранения Azure. Нажмите кнопку **ОК**.
    - **Ручной ввод учетных данных** — введите имя учетной записи хранения hello и либо hello первичный или вторичный ключ. Выберите вариант **подключения** (в большинстве случаев рекомендуется использовать протокол HTTPS). Нажмите кнопку **ОК**.

1. toodelete строка подключения, выберите строку hello подключения, а затем выберите **удалить параметр**.

1. Из Visual Studio hello панели инструментов выберите **Сохранить**.

## <a name="programmatically-access-a-connection-string"></a>Программный доступ к строке подключения

Hello следующие шаги показывают, как tooprogrammatically к строке подключения с помощью C#.

1. Добавьте следующее hello с помощью файла директив tooa C#, где вы собираетесь toouse приветствия:

    ```csharp
    using Microsoft.WindowsAzure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.ServiceRuntime;
    ```

1. Hello ниже показан пример tooaccess строку подключения. Замените hello &lt;ConnectionStringName > заполнитель hello соответствующее значение. 

    ```csharp
    // Setup hello connection tooAzure Storage
    var storageAccount = CloudStorageAccount.Parse(RoleEnvironment.GetConfigurationSettingValue("<ConnectionStringName>"));
    ```

## <a name="add-custom-settings-toouse-in-your-azure-cloud-service"></a>Добавить пользовательские параметры toouse в облачной службе Azure
Пользовательские параметры в файле конфигурации службы hello позволяют добавлять имя и значение для строки для конкретной конфигурации службы. Вы можете toouse tooconfigure этот параметр, функция в облачной службе, считывая значение hello Здравствуйте, Настройка и использование этой логики hello toocontrol значение в коде. Можно изменить эти значения конфигурации службы без необходимости toorebuild ваш пакет служб или при выполнении облачной службы. Ваш код может проверять наличие уведомлений об изменении параметра. См. статью, посвященную [событию RoleEnvironment.Changing](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changing.aspx).

Вы можете добавлять, удалять или изменять пользовательские параметры для конфигураций службы. Также можно использовать разные значения этих строк для разных конфигураций службы.

Используя другое значение для каждой конфигурации службы, не имеют разные строки toouse в облачной службе или модифицировать код при публикации на tooAzure облачной службы. Можно использовать одно имя для строки hello в ваш код и hello значение отличается, зависит от конфигурации службы hello, выбранной при построении облачной службы или при его публикации приветствия.

1. Создайте или откройте проект облачной службы Azure в среде Visual Studio.

1. В **обозревателе решений**, разверните узел проекта hello. В разделе hello **ролей** узел, щелкните правой кнопкой мыши роль hello tooupdate и, hello контекстном меню, выберите **свойства**.

    ![Контекстное меню роли в обозревателе решений Azure](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. Выберите hello **параметры** вкладки.

    ![Вкладка "Параметры"](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab.png)

1. В hello **конфигурации службы** список, выберите hello конфигурации службы, что требуется tooupdate.

    ![Список "Конфигурация службы"](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-select-configuration.png)

1. Выберите пользовательскую настройку tooadd **добавить параметр**.

    ![Добавление пользовательского параметра](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting.png)

1. После списка toohello добавления нового параметра hello, обновите строку hello в списке hello hello необходимых сведений.

    ![Новый пользовательский параметр](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting-new-setting.png)

    - **Имя** -введите имя hello приветствия.
    - **Тип** — выберите **строка** из раскрывающегося списка hello.
    - **Значение** -введите значение hello приветствия. Вы можете ввести значение hello непосредственно в hello **значение** ячейки или значение hello tooenter hello выберите кнопку с многоточием (...) в hello **Изменение строкового** диалогового окна.  

1. toodelete пользовательского параметра, выберите параметр hello, а затем выберите **удалить параметр**.

1. Из Visual Studio hello панели инструментов выберите **Сохранить**.

## <a name="programmatically-access-a-custom-settings-value"></a>Программный доступ к значению пользовательского параметра
 
Hello следующие шаги показывают, как tooprogrammatically доступ к пользовательским параметром, с помощью C#.

1. Добавьте следующее hello с помощью файла директив tooa C#, где вы собираетесь toouse приветствия:

    ```csharp
    using Microsoft.WindowsAzure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.ServiceRuntime;
    ```

1. Hello ниже показан пример tooaccess пользовательский параметр. Замените hello &lt;SettingName > заполнитель hello соответствующее значение. 
    
    ```csharp
    var settingValue = RoleEnvironment.GetConfigurationSettingValue("<SettingName>");
    ```

## <a name="manage-local-storage-for-each-role-instance"></a>Управление локальным хранилищем для каждого экземпляра роли
Каждому экземпляру роли можно назначить хранилище локальной файловой системы. Hello данным, хранящимся в хранилище не доступно на других экземплярах роли hello, для которых hello данные хранятся или других ролей.  

1. Создайте или откройте проект облачной службы Azure в среде Visual Studio.

1. В **обозревателе решений**, разверните узел проекта hello. В разделе hello **ролей** узел, щелкните правой кнопкой мыши роль hello tooupdate и, hello контекстном меню, выберите **свойства**.

    ![Контекстное меню роли в обозревателе решений Azure](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. Выберите hello **локального хранилища** вкладки.

    ![Вкладка "Локальное хранилище"](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab.png)

1. В hello **конфигурации службы** убедитесь, что **все конфигурации** выбранное hello локального хранилища параметры применяются tooall конфигураций службы. Любое другое значение приводит все поля входных hello на странице приветствия отключен. 

    ![Список "Конфигурация службы"](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab-service-configuration.png)

1. Выберите запись локального хранилища tooadd **добавить локальное хранилище**.

    ![Добавление локального хранилища](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab-add-local-storage.png)

1. После списка toohello добавления hello новая запись локального хранилища, обновите строку hello в списке hello hello необходимых сведений.

    ![Новая запись локального хранилища](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab-new-local-storage.png)

    - **Имя** -введите имя hello, чтобы получить toouse hello новое локальное хранилище.
    - **Размер (МБ)** -введите hello размер в Мегабайтах, который требуется для hello новое локальное хранилище.
    - **Очистить при повторном использовании роли** -выберите этот параметр tooremove hello данных в новое локальное хранилище hello при очистке hello виртуальной машины для роли hello.

1. toodelete запись локального хранилища, выберите запись hello, а затем выберите **удалить локальное хранилище**.

1. Из Visual Studio hello панели инструментов выберите **Сохранить**.

## <a name="programmatically-accessing-local-storage"></a>Программный доступ к локальному хранилищу

В этом разделе показано, как локальное хранилище с помощью C#, написав текстовый файл теста доступ к tooprogrammatically `MyLocalStorageTest.txt`.  

### <a name="write-a-text-file-toolocal-storage"></a>Запись текстового файла toolocal хранилища

Привет, следующий код является примером как toowrite текстовый файл toolocal хранилища. Замените hello &lt;LocalStorageName > заполнитель hello соответствующее значение. 

    ```csharp
    // Retrieve an object that points toohello local storage resource
    LocalResource localResource = RoleEnvironment.GetLocalResource("<LocalStorageName>");
    
    //Define hello file name and path
    string[] paths = { localResource.RootPath, "MyLocalStorageTest.txt" };
    String filePath = Path.Combine(paths);
    
    using (FileStream writeStream = File.Create(filePath))
    {
        Byte[] textToWrite = new UTF8Encoding(true).GetBytes("Testing Web role storage");
        writeStream.Write(textToWrite, 0, textToWrite.Length);
    }

    ```

### <a name="find-a-file-written-toolocal-storage"></a>Найти файл, написанный toolocal хранилища

файл hello tooview создается кодом hello в предыдущем разделе hello, выполните следующие действия.
    
1.  В области уведомлений Windows hello, щелкните правой кнопкой мыши значок Azure hello и hello контекстном меню, выберите **Показать пользовательский Интерфейс эмулятора вычислений**. 

    ![Показать пользовательский интерфейс эмулятора вычислений](./media/vs-azure-tools-configure-roles-for-cloud-service/show-compute-emulator.png)

1. Выберите веб-роли hello.

    ![Эмулятор вычислений Azure](./media/vs-azure-tools-configure-roles-for-cloud-service/compute-emulator.png)

1. На hello **эмулятор вычислений Microsoft Azure** последовательно выберите пункты **средства** > **открыть локальное хранилище**.

    ![Пункт меню "Открыть локальное хранилище"](./media/vs-azure-tools-configure-roles-for-cloud-service/compute-emulator-open-local-store-menu.png)

1. При открытии окна проводника Windows hello, введите "MyLocalStorageTest.txt'' в hello **поиска** текста, а затем выберите **ввод** toostart hello поиска. 

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения о проектах Azure в Visual Studio см. в статье [Настройка проекта облачной службы в Visual Studio](vs-azure-tools-configuring-an-azure-project.md). Дополнительные сведения о hello облачной службы схемы путем чтения [Справочник по схеме](https://msdn.microsoft.com/library/azure/dd179398).

