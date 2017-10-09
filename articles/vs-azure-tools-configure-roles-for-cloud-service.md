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
# <a name="configure-azure-cloud-service-roles-with-visual-studio"></a><span data-ttu-id="5f729-103">Настройка ролей для облачной службы Azure в Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5f729-103">Configure Azure cloud service roles with Visual Studio</span></span>
<span data-ttu-id="5f729-104">Облачной службе Azure можно назначить одну или несколько рабочих ролей или веб-ролей.</span><span class="sxs-lookup"><span data-stu-id="5f729-104">An Azure cloud service can have one or more worker or web roles.</span></span> <span data-ttu-id="5f729-105">Для каждой роли требуется toodefine, как настроить эту роль и также настроить способ выполнения этой роли.</span><span class="sxs-lookup"><span data-stu-id="5f729-105">For each role, you need toodefine how that role is set up and also configure how that role runs.</span></span> <span data-ttu-id="5f729-106">toolearn Дополнительные сведения о ролях в облачных службах см. видео hello [tooAzure введение облачные службы](https://channel9.msdn.com/Series/Windows-Azure-Cloud-Services-Tutorials/Introduction-to-Windows-Azure-Cloud-Services).</span><span class="sxs-lookup"><span data-stu-id="5f729-106">toolearn more about roles in cloud services, see hello video [Introduction tooAzure Cloud Services](https://channel9.msdn.com/Series/Windows-Azure-Cloud-Services-Tutorials/Introduction-to-Windows-Azure-Cloud-Services).</span></span> 

<span data-ttu-id="5f729-107">Hello для облачной службы хранится в hello следующие файлы:</span><span class="sxs-lookup"><span data-stu-id="5f729-107">hello information for your cloud service is stored in hello following files:</span></span>

- <span data-ttu-id="5f729-108">**ServiceDefinition.csdef** -hello файла определения службы определяет параметры среды выполнения hello для облачной службы, включая какие роли являются обязательными, конечные точки и размер виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="5f729-108">**ServiceDefinition.csdef** - hello service definition file defines hello runtime settings for your cloud service including what roles are required, endpoints, and virtual machine size.</span></span> <span data-ttu-id="5f729-109">Ни один из hello данные, хранящиеся в `ServiceDefinition.csdef` можно изменить, если ваша роль выполняется.</span><span class="sxs-lookup"><span data-stu-id="5f729-109">None of hello data stored in `ServiceDefinition.csdef` can be changed when your role is running.</span></span>
- <span data-ttu-id="5f729-110">**ServiceConfiguration.cscfg** - файл конфигурации службы hello настраивает, сколько экземпляров роли выполняются и значения hello hello параметров, определенных для роли.</span><span class="sxs-lookup"><span data-stu-id="5f729-110">**ServiceConfiguration.cscfg** - hello service configuration file configures how many instances of a role are run and hello values of hello settings defined for a role.</span></span> <span data-ttu-id="5f729-111">Здравствуйте, данные, хранящиеся в `ServiceConfiguration.cscfg` можно изменить во время вашей роли.</span><span class="sxs-lookup"><span data-stu-id="5f729-111">hello data stored in `ServiceConfiguration.cscfg` can be changed while your role is running.</span></span>

<span data-ttu-id="5f729-112">toostore разные значения для hello параметры, управляющие ходом роли, можно определить несколько конфигураций службы.</span><span class="sxs-lookup"><span data-stu-id="5f729-112">toostore different values for hello settings that control how a role runs, you can define multiple service configurations.</span></span> <span data-ttu-id="5f729-113">Разные конфигурации службы можно использовать для разных сред развертывания.</span><span class="sxs-lookup"><span data-stu-id="5f729-113">You can use a different service configuration for each deployment environment.</span></span> <span data-ttu-id="5f729-114">Например можно задать вашей учетной записи подключения строка toouse hello локального хранилища Azure эмулятор хранилища в конфигурации локальной службы и создать другой toouse конфигурации службы хранилища Azure в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="5f729-114">For example, you can set your storage account connection string toouse hello local Azure storage emulator in a local service configuration and create another service configuration toouse Azure storage in hello cloud.</span></span>

<span data-ttu-id="5f729-115">При создании облачной службы Azure в Visual Studio две конфигурации службы создаются автоматически и добавлены tooyour проекта Azure:</span><span class="sxs-lookup"><span data-stu-id="5f729-115">When you create an Azure cloud service in Visual Studio, two service configurations are automatically created and added tooyour Azure project:</span></span>

- `ServiceConfiguration.Cloud.cscfg`
- `ServiceConfiguration.Local.cscfg`

## <a name="configure-an-azure-cloud-service"></a><span data-ttu-id="5f729-116">Настройка облачной службы Azure</span><span class="sxs-lookup"><span data-stu-id="5f729-116">Configure an Azure cloud service</span></span>
<span data-ttu-id="5f729-117">Можно настроить облачную службу Azure из обозревателя решений в Visual Studio, как показано в hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="5f729-117">You can configure an Azure cloud service from Solution Explorer in Visual Studio, as shown in hello following steps:</span></span>

1. <span data-ttu-id="5f729-118">Создайте или откройте проект облачной службы Azure в среде Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5f729-118">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="5f729-119">В **обозревателе решений**, щелкните правой кнопкой мыши проект hello и hello контекстном меню, выберите **свойства**.</span><span class="sxs-lookup"><span data-stu-id="5f729-119">In **Solution Explorer**, right-click hello project, and, from hello context menu, select **Properties**.</span></span>
   
    ![Контекстное меню проекта в обозревателе решений](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-project-context-menu.png)

1. <span data-ttu-id="5f729-121">На странице свойств проекта hello, выберите hello **разработки** вкладки.</span><span class="sxs-lookup"><span data-stu-id="5f729-121">In hello project's properties page, select hello **Development** tab.</span></span> 

    ![Страница свойств проекта — вкладка "Разработка"](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-development-tab.png)

1. <span data-ttu-id="5f729-123">В hello **конфигурации службы** список, выберите hello имя конфигурации службы hello, что требуется tooedit.</span><span class="sxs-lookup"><span data-stu-id="5f729-123">In hello **Service Configuration** list, select hello name of hello service configuration that you want tooedit.</span></span> <span data-ttu-id="5f729-124">(Toomake изменения конфигурации службы hello tooall для этой роли, установите **все конфигурации**.)</span><span class="sxs-lookup"><span data-stu-id="5f729-124">(If you want toomake changes tooall hello service configurations for this role, select **All Configurations**.)</span></span>
   
    > [!IMPORTANT]
    > <span data-ttu-id="5f729-125">При выборе конкретной конфигурации службы некоторые ее свойства будут отключены, так как их можно задать только для всех конфигураций.</span><span class="sxs-lookup"><span data-stu-id="5f729-125">If you choose a specific service configuration, some properties are disabled because they can only be set for all configurations.</span></span> <span data-ttu-id="5f729-126">tooedit эти свойства, необходимо выбрать **все конфигурации**.</span><span class="sxs-lookup"><span data-stu-id="5f729-126">tooedit these properties, you must select **All Configurations**.</span></span>
    > 
    > 
   
    ![Список конфигураций службы для облачной службы Azure](./media/vs-azure-tools-configure-roles-for-cloud-service/cloud-service-service-configuration-property.png)

## <a name="change-hello-number-of-role-instances"></a><span data-ttu-id="5f729-128">Изменение hello число экземпляров роли</span><span class="sxs-lookup"><span data-stu-id="5f729-128">Change hello number of role instances</span></span>
<span data-ttu-id="5f729-129">tooimprove hello производительность облачной службы, можно изменить hello числа экземпляров роли, работающих под управлением, основываясь на номере hello пользователей или нагрузки hello, ожидаемый для определенной роли.</span><span class="sxs-lookup"><span data-stu-id="5f729-129">tooimprove hello performance of your cloud service, you can change hello number of instances of a role that are running, based on hello number of users or hello load expected for a particular role.</span></span> <span data-ttu-id="5f729-130">Отдельная виртуальная машина создается для каждого экземпляра роли при hello облачной службы в Azure.</span><span class="sxs-lookup"><span data-stu-id="5f729-130">A separate virtual machine is created for each instance of a role when hello cloud service runs in Azure.</span></span> <span data-ttu-id="5f729-131">Это влияет на выставление счетов hello hello развертывания облачной службы.</span><span class="sxs-lookup"><span data-stu-id="5f729-131">This affects hello billing for hello deployment of this cloud service.</span></span> <span data-ttu-id="5f729-132">Дополнительные сведения о плате за использование Azure см. в статье [Расшифровка счета за использование Microsoft Azure](billing/billing-understand-your-bill.md).</span><span class="sxs-lookup"><span data-stu-id="5f729-132">For more information about billing, see [Understand your bill for Microsoft Azure](billing/billing-understand-your-bill.md).</span></span>

1. <span data-ttu-id="5f729-133">Создайте или откройте проект облачной службы Azure в среде Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5f729-133">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="5f729-134">В **обозревателе решений**, разверните узел проекта hello.</span><span class="sxs-lookup"><span data-stu-id="5f729-134">In **Solution Explorer**, expand hello project node.</span></span> <span data-ttu-id="5f729-135">В разделе hello **ролей** узел, щелкните правой кнопкой мыши роль hello tooupdate и, hello контекстном меню, выберите **свойства**.</span><span class="sxs-lookup"><span data-stu-id="5f729-135">Under hello **Roles** node, right-click hello role you want tooupdate, and, from hello context menu, select **Properties**.</span></span>

    ![Контекстное меню роли в обозревателе решений Azure](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. <span data-ttu-id="5f729-137">Выберите hello **конфигурации** вкладки.</span><span class="sxs-lookup"><span data-stu-id="5f729-137">Select hello **Configuration** tab.</span></span>

    ![Вкладка "Конфигурация"](./media/vs-azure-tools-configure-roles-for-cloud-service/role-configuration-properties-page.png)

1. <span data-ttu-id="5f729-139">В hello **конфигурации службы** список, выберите hello конфигурации службы, что требуется tooupdate.</span><span class="sxs-lookup"><span data-stu-id="5f729-139">In hello **Service Configuration** list, select hello service configuration that you want tooupdate.</span></span>
   
    ![Список "Конфигурация службы"](./media/vs-azure-tools-configure-roles-for-cloud-service/role-configuration-properties-page-select-configuration.png)

1. <span data-ttu-id="5f729-141">В hello **число экземпляров** текста введите hello число экземпляров, что требуется toostart для этой роли.</span><span class="sxs-lookup"><span data-stu-id="5f729-141">In hello **Instance count** text box, enter hello number of instances that you want toostart for this role.</span></span> <span data-ttu-id="5f729-142">Каждый экземпляр выполняется на отдельной виртуальной машине, при публикации службы tooAzure hello облака.</span><span class="sxs-lookup"><span data-stu-id="5f729-142">Each instance runs on a separate virtual machine when you publish hello cloud service tooAzure.</span></span>

    ![Обновление hello число экземпляров](./media/vs-azure-tools-configure-roles-for-cloud-service/role-configuration-properties-page-instance-count.png)

1. <span data-ttu-id="5f729-144">Из Visual Studio hello панели инструментов выберите **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="5f729-144">From hello Visual Studio, toolbar, select **Save**.</span></span>

## <a name="manage-connection-strings-for-storage-accounts"></a><span data-ttu-id="5f729-145">Управление строками подключения для учетных записей хранения</span><span class="sxs-lookup"><span data-stu-id="5f729-145">Manage connection strings for storage accounts</span></span>
<span data-ttu-id="5f729-146">Вы можете добавлять, удалять или изменять строки подключения для конфигураций службы.</span><span class="sxs-lookup"><span data-stu-id="5f729-146">You can add, remove, or modify connection strings for your service configurations.</span></span> <span data-ttu-id="5f729-147">Например, вы можете использовать строку локального подключения для конфигурации локальной службы, которая имеет значение `UseDevelopmentStorage=true`.</span><span class="sxs-lookup"><span data-stu-id="5f729-147">For example, you might want a local connection string for a local service configuration that has a value of `UseDevelopmentStorage=true`.</span></span> <span data-ttu-id="5f729-148">Может также потребоваться tooconfigure конфигурацию облачной службы, который использует учетную запись хранилища в Azure.</span><span class="sxs-lookup"><span data-stu-id="5f729-148">You might also want tooconfigure a cloud service configuration that uses a storage account in Azure.</span></span>

> [!WARNING]
> <span data-ttu-id="5f729-149">При вводе hello хранилища Azure ключ доступа для строки подключения учетной записи хранилища, эти сведения сохраняются локально в файле конфигурации службы hello.</span><span class="sxs-lookup"><span data-stu-id="5f729-149">When you enter hello Azure storage account key information for a storage account connection string, this information is stored locally in hello service configuration file.</span></span> <span data-ttu-id="5f729-150">Тем не менее эти сведения в настоящее время не хранятся в виде зашифрованного текста.</span><span class="sxs-lookup"><span data-stu-id="5f729-150">However, this information is currently not stored as encrypted text.</span></span>
> 
> 

<span data-ttu-id="5f729-151">Используя другое значение для каждой конфигурации службы, не имеют toouse различные строки подключения в облачной службе или модифицировать код при публикации на tooAzure облачной службы.</span><span class="sxs-lookup"><span data-stu-id="5f729-151">By using a different value for each service configuration, you do not have toouse different connection strings in your cloud service or modify your code when you publish your cloud service tooAzure.</span></span> <span data-ttu-id="5f729-152">Можно использовать одно имя для строки подключения hello в ваш код и hello значение отличается, зависит от конфигурации службы hello, выбранной при построении облачной службы или при его публикации приветствия.</span><span class="sxs-lookup"><span data-stu-id="5f729-152">You can use hello same name for hello connection string in your code and hello value is different, based on hello service configuration that you select when you build your cloud service or when you publish it.</span></span>

1. <span data-ttu-id="5f729-153">Создайте или откройте проект облачной службы Azure в среде Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5f729-153">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="5f729-154">В **обозревателе решений**, разверните узел проекта hello.</span><span class="sxs-lookup"><span data-stu-id="5f729-154">In **Solution Explorer**, expand hello project node.</span></span> <span data-ttu-id="5f729-155">В разделе hello **ролей** узел, щелкните правой кнопкой мыши роль hello tooupdate и, hello контекстном меню, выберите **свойства**.</span><span class="sxs-lookup"><span data-stu-id="5f729-155">Under hello **Roles** node, right-click hello role you want tooupdate, and, from hello context menu, select **Properties**.</span></span>

    ![Контекстное меню роли в обозревателе решений Azure](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. <span data-ttu-id="5f729-157">Выберите hello **параметры** вкладки.</span><span class="sxs-lookup"><span data-stu-id="5f729-157">Select hello **Settings** tab.</span></span>

    ![Вкладка "Параметры"](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab.png)

1. <span data-ttu-id="5f729-159">В hello **конфигурации службы** список, выберите hello конфигурации службы, что требуется tooupdate.</span><span class="sxs-lookup"><span data-stu-id="5f729-159">In hello **Service Configuration** list, select hello service configuration that you want tooupdate.</span></span>

    ![Конфигурация службы](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-select-configuration.png)

1. <span data-ttu-id="5f729-161">Выберите строку подключения tooadd **добавить параметр**.</span><span class="sxs-lookup"><span data-stu-id="5f729-161">tooadd a connection string, select **Add Setting**.</span></span>

    ![Добавление строки подключения](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting.png)

1. <span data-ttu-id="5f729-163">После списка toohello добавления нового параметра hello, обновите строку hello в списке hello hello необходимых сведений.</span><span class="sxs-lookup"><span data-stu-id="5f729-163">Once hello new setting has been added toohello list, update hello row in hello list with hello necessary information.</span></span>

    ![Новая строка подключения](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting-new-setting.png)

    - <span data-ttu-id="5f729-165">**Имя** -введите имя hello, что необходимо toouse для строки подключения hello.</span><span class="sxs-lookup"><span data-stu-id="5f729-165">**Name** - Enter hello name that you want toouse for hello connection string.</span></span>
    - <span data-ttu-id="5f729-166">**Тип** — выберите **строка подключения** из раскрывающегося списка hello.</span><span class="sxs-lookup"><span data-stu-id="5f729-166">**Type** - Select **Connection String** from hello drop-down list.</span></span>
    - <span data-ttu-id="5f729-167">**Значение** -hello строку подключения можно вводить непосредственно в hello **значение** ячейки или toowork hello выберите кнопку с многоточием (...) в hello **Создание строки подключения хранилища** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="5f729-167">**Value** - You can either enter hello connection string directly into hello **Value** cell, or select hello ellipsis (...) toowork in hello **Create Storage Connection String** dialog.</span></span>  

1. <span data-ttu-id="5f729-168">В hello **Создание строки подключения хранилища** диалоговое окно, выберите один из вариантов для **подключение с использованием**.</span><span class="sxs-lookup"><span data-stu-id="5f729-168">In hello **Create Storage Connection String** dialog, select an option for **Connect using**.</span></span> <span data-ttu-id="5f729-169">Следуйте инструкциям hello для выбранных параметров hello:</span><span class="sxs-lookup"><span data-stu-id="5f729-169">Then follow hello instructions for hello option you select:</span></span>

    - <span data-ttu-id="5f729-170">**Эмулятор хранилища Microsoft Azure** -отключены при выборе этого параметра hello остальные параметры в диалоговом окне приветствия, как они характерны только tooAzure.</span><span class="sxs-lookup"><span data-stu-id="5f729-170">**Microsoft Azure storage emulator** - If you select this option, hello remaining settings on hello dialog are disabled as they apply only tooAzure.</span></span> <span data-ttu-id="5f729-171">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="5f729-171">Select **OK**.</span></span>
    - <span data-ttu-id="5f729-172">**Подписки** — Если вы установите этот параметр, использовать hello раскрывающегося списка tooeither выбирать и входа в учетную запись Майкрософт или добавить учетную запись Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="5f729-172">**Your subscription** - If you select this option, use hello dropdown list tooeither select and sign into a Microsoft account, or add a Microsoft account.</span></span> <span data-ttu-id="5f729-173">Выберите подписку и учетную запись хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="5f729-173">Select an Azure subscription and storage account.</span></span> <span data-ttu-id="5f729-174">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="5f729-174">Select **OK**.</span></span>
    - <span data-ttu-id="5f729-175">**Ручной ввод учетных данных** — введите имя учетной записи хранения hello и либо hello первичный или вторичный ключ.</span><span class="sxs-lookup"><span data-stu-id="5f729-175">**Manually entered credentials** - Enter hello storage account name, and either hello primary or second key.</span></span> <span data-ttu-id="5f729-176">Выберите вариант **подключения** (в большинстве случаев рекомендуется использовать протокол HTTPS). Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="5f729-176">Select an option for **Connection** (HTTPS is recommended for most scenarios.) Select **OK**.</span></span>

1. <span data-ttu-id="5f729-177">toodelete строка подключения, выберите строку hello подключения, а затем выберите **удалить параметр**.</span><span class="sxs-lookup"><span data-stu-id="5f729-177">toodelete a connection string, select hello connection string, and then select **Remove Setting**.</span></span>

1. <span data-ttu-id="5f729-178">Из Visual Studio hello панели инструментов выберите **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="5f729-178">From hello Visual Studio, toolbar, select **Save**.</span></span>

## <a name="programmatically-access-a-connection-string"></a><span data-ttu-id="5f729-179">Программный доступ к строке подключения</span><span class="sxs-lookup"><span data-stu-id="5f729-179">Programmatically access a connection string</span></span>

<span data-ttu-id="5f729-180">Hello следующие шаги показывают, как tooprogrammatically к строке подключения с помощью C#.</span><span class="sxs-lookup"><span data-stu-id="5f729-180">hello following steps show how tooprogrammatically access a connection string using C#.</span></span>

1. <span data-ttu-id="5f729-181">Добавьте следующее hello с помощью файла директив tooa C#, где вы собираетесь toouse приветствия:</span><span class="sxs-lookup"><span data-stu-id="5f729-181">Add hello following using directives tooa C# file where you are going toouse hello setting:</span></span>

    ```csharp
    using Microsoft.WindowsAzure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.ServiceRuntime;
    ```

1. <span data-ttu-id="5f729-182">Hello ниже показан пример tooaccess строку подключения.</span><span class="sxs-lookup"><span data-stu-id="5f729-182">hello following code illustrates an example of how tooaccess a connection string.</span></span> <span data-ttu-id="5f729-183">Замените hello &lt;ConnectionStringName > заполнитель hello соответствующее значение.</span><span class="sxs-lookup"><span data-stu-id="5f729-183">Replace hello &lt;ConnectionStringName> placeholder with hello appropriate value.</span></span> 

    ```csharp
    // Setup hello connection tooAzure Storage
    var storageAccount = CloudStorageAccount.Parse(RoleEnvironment.GetConfigurationSettingValue("<ConnectionStringName>"));
    ```

## <a name="add-custom-settings-toouse-in-your-azure-cloud-service"></a><span data-ttu-id="5f729-184">Добавить пользовательские параметры toouse в облачной службе Azure</span><span class="sxs-lookup"><span data-stu-id="5f729-184">Add custom settings toouse in your Azure cloud service</span></span>
<span data-ttu-id="5f729-185">Пользовательские параметры в файле конфигурации службы hello позволяют добавлять имя и значение для строки для конкретной конфигурации службы.</span><span class="sxs-lookup"><span data-stu-id="5f729-185">Custom settings in hello service configuration file let you add a name and value for a string for a specific service configuration.</span></span> <span data-ttu-id="5f729-186">Вы можете toouse tooconfigure этот параметр, функция в облачной службе, считывая значение hello Здравствуйте, Настройка и использование этой логики hello toocontrol значение в коде.</span><span class="sxs-lookup"><span data-stu-id="5f729-186">You might choose toouse this setting tooconfigure a feature in your cloud service by reading hello value of hello setting and using this value toocontrol hello logic in your code.</span></span> <span data-ttu-id="5f729-187">Можно изменить эти значения конфигурации службы без необходимости toorebuild ваш пакет служб или при выполнении облачной службы.</span><span class="sxs-lookup"><span data-stu-id="5f729-187">You can change these service configuration values without having toorebuild your service package or when your cloud service is running.</span></span> <span data-ttu-id="5f729-188">Ваш код может проверять наличие уведомлений об изменении параметра.</span><span class="sxs-lookup"><span data-stu-id="5f729-188">Your code can check for notifications of when a setting changes.</span></span> <span data-ttu-id="5f729-189">См. статью, посвященную [событию RoleEnvironment.Changing](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changing.aspx).</span><span class="sxs-lookup"><span data-stu-id="5f729-189">See [RoleEnvironment.Changing Event](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changing.aspx).</span></span>

<span data-ttu-id="5f729-190">Вы можете добавлять, удалять или изменять пользовательские параметры для конфигураций службы.</span><span class="sxs-lookup"><span data-stu-id="5f729-190">You can add, remove, or modify custom settings for your service configurations.</span></span> <span data-ttu-id="5f729-191">Также можно использовать разные значения этих строк для разных конфигураций службы.</span><span class="sxs-lookup"><span data-stu-id="5f729-191">You might want different values for these strings for different service configurations.</span></span>

<span data-ttu-id="5f729-192">Используя другое значение для каждой конфигурации службы, не имеют разные строки toouse в облачной службе или модифицировать код при публикации на tooAzure облачной службы.</span><span class="sxs-lookup"><span data-stu-id="5f729-192">By using a different value for each service configuration, you do not have toouse different strings in your cloud service or modify your code when you publish your cloud service tooAzure.</span></span> <span data-ttu-id="5f729-193">Можно использовать одно имя для строки hello в ваш код и hello значение отличается, зависит от конфигурации службы hello, выбранной при построении облачной службы или при его публикации приветствия.</span><span class="sxs-lookup"><span data-stu-id="5f729-193">You can use hello same name for hello string in your code and hello value is different, based on hello service configuration that you select when you build your cloud service or when you publish it.</span></span>

1. <span data-ttu-id="5f729-194">Создайте или откройте проект облачной службы Azure в среде Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5f729-194">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="5f729-195">В **обозревателе решений**, разверните узел проекта hello.</span><span class="sxs-lookup"><span data-stu-id="5f729-195">In **Solution Explorer**, expand hello project node.</span></span> <span data-ttu-id="5f729-196">В разделе hello **ролей** узел, щелкните правой кнопкой мыши роль hello tooupdate и, hello контекстном меню, выберите **свойства**.</span><span class="sxs-lookup"><span data-stu-id="5f729-196">Under hello **Roles** node, right-click hello role you want tooupdate, and, from hello context menu, select **Properties**.</span></span>

    ![Контекстное меню роли в обозревателе решений Azure](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. <span data-ttu-id="5f729-198">Выберите hello **параметры** вкладки.</span><span class="sxs-lookup"><span data-stu-id="5f729-198">Select hello **Settings** tab.</span></span>

    ![Вкладка "Параметры"](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab.png)

1. <span data-ttu-id="5f729-200">В hello **конфигурации службы** список, выберите hello конфигурации службы, что требуется tooupdate.</span><span class="sxs-lookup"><span data-stu-id="5f729-200">In hello **Service Configuration** list, select hello service configuration that you want tooupdate.</span></span>

    ![Список "Конфигурация службы"](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-select-configuration.png)

1. <span data-ttu-id="5f729-202">Выберите пользовательскую настройку tooadd **добавить параметр**.</span><span class="sxs-lookup"><span data-stu-id="5f729-202">tooadd a custom setting, select **Add Setting**.</span></span>

    ![Добавление пользовательского параметра](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting.png)

1. <span data-ttu-id="5f729-204">После списка toohello добавления нового параметра hello, обновите строку hello в списке hello hello необходимых сведений.</span><span class="sxs-lookup"><span data-stu-id="5f729-204">Once hello new setting has been added toohello list, update hello row in hello list with hello necessary information.</span></span>

    ![Новый пользовательский параметр](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting-new-setting.png)

    - <span data-ttu-id="5f729-206">**Имя** -введите имя hello приветствия.</span><span class="sxs-lookup"><span data-stu-id="5f729-206">**Name** - Enter hello name of hello setting.</span></span>
    - <span data-ttu-id="5f729-207">**Тип** — выберите **строка** из раскрывающегося списка hello.</span><span class="sxs-lookup"><span data-stu-id="5f729-207">**Type** - Select **String** from hello drop-down list.</span></span>
    - <span data-ttu-id="5f729-208">**Значение** -введите значение hello приветствия.</span><span class="sxs-lookup"><span data-stu-id="5f729-208">**Value** - Enter hello value of hello setting.</span></span> <span data-ttu-id="5f729-209">Вы можете ввести значение hello непосредственно в hello **значение** ячейки или значение hello tooenter hello выберите кнопку с многоточием (...) в hello **Изменение строкового** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="5f729-209">You can either enter hello value directly into hello **Value** cell, or select hello ellipsis (...) tooenter hello value in hello **Edit String** dialog.</span></span>  

1. <span data-ttu-id="5f729-210">toodelete пользовательского параметра, выберите параметр hello, а затем выберите **удалить параметр**.</span><span class="sxs-lookup"><span data-stu-id="5f729-210">toodelete a custom setting, select hello setting, and then select **Remove Setting**.</span></span>

1. <span data-ttu-id="5f729-211">Из Visual Studio hello панели инструментов выберите **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="5f729-211">From hello Visual Studio, toolbar, select **Save**.</span></span>

## <a name="programmatically-access-a-custom-settings-value"></a><span data-ttu-id="5f729-212">Программный доступ к значению пользовательского параметра</span><span class="sxs-lookup"><span data-stu-id="5f729-212">Programmatically access a custom setting's value</span></span>
 
<span data-ttu-id="5f729-213">Hello следующие шаги показывают, как tooprogrammatically доступ к пользовательским параметром, с помощью C#.</span><span class="sxs-lookup"><span data-stu-id="5f729-213">hello following steps show how tooprogrammatically access a custom setting using C#.</span></span>

1. <span data-ttu-id="5f729-214">Добавьте следующее hello с помощью файла директив tooa C#, где вы собираетесь toouse приветствия:</span><span class="sxs-lookup"><span data-stu-id="5f729-214">Add hello following using directives tooa C# file where you are going toouse hello setting:</span></span>

    ```csharp
    using Microsoft.WindowsAzure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.ServiceRuntime;
    ```

1. <span data-ttu-id="5f729-215">Hello ниже показан пример tooaccess пользовательский параметр.</span><span class="sxs-lookup"><span data-stu-id="5f729-215">hello following code illustrates an example of how tooaccess a custom setting.</span></span> <span data-ttu-id="5f729-216">Замените hello &lt;SettingName > заполнитель hello соответствующее значение.</span><span class="sxs-lookup"><span data-stu-id="5f729-216">Replace hello &lt;SettingName> placeholder with hello appropriate value.</span></span> 
    
    ```csharp
    var settingValue = RoleEnvironment.GetConfigurationSettingValue("<SettingName>");
    ```

## <a name="manage-local-storage-for-each-role-instance"></a><span data-ttu-id="5f729-217">Управление локальным хранилищем для каждого экземпляра роли</span><span class="sxs-lookup"><span data-stu-id="5f729-217">Manage local storage for each role instance</span></span>
<span data-ttu-id="5f729-218">Каждому экземпляру роли можно назначить хранилище локальной файловой системы.</span><span class="sxs-lookup"><span data-stu-id="5f729-218">You can add local file system storage for each instance of a role.</span></span> <span data-ttu-id="5f729-219">Hello данным, хранящимся в хранилище не доступно на других экземплярах роли hello, для которых hello данные хранятся или других ролей.</span><span class="sxs-lookup"><span data-stu-id="5f729-219">hello data stored in that storage is not accessible by other instances of hello role for which hello data is stored, or by other roles.</span></span>  

1. <span data-ttu-id="5f729-220">Создайте или откройте проект облачной службы Azure в среде Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5f729-220">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="5f729-221">В **обозревателе решений**, разверните узел проекта hello.</span><span class="sxs-lookup"><span data-stu-id="5f729-221">In **Solution Explorer**, expand hello project node.</span></span> <span data-ttu-id="5f729-222">В разделе hello **ролей** узел, щелкните правой кнопкой мыши роль hello tooupdate и, hello контекстном меню, выберите **свойства**.</span><span class="sxs-lookup"><span data-stu-id="5f729-222">Under hello **Roles** node, right-click hello role you want tooupdate, and, from hello context menu, select **Properties**.</span></span>

    ![Контекстное меню роли в обозревателе решений Azure](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. <span data-ttu-id="5f729-224">Выберите hello **локального хранилища** вкладки.</span><span class="sxs-lookup"><span data-stu-id="5f729-224">Select hello **Local Storage** tab.</span></span>

    ![Вкладка "Локальное хранилище"](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab.png)

1. <span data-ttu-id="5f729-226">В hello **конфигурации службы** убедитесь, что **все конфигурации** выбранное hello локального хранилища параметры применяются tooall конфигураций службы.</span><span class="sxs-lookup"><span data-stu-id="5f729-226">In hello **Service Configuration** list, ensure that **All Configurations** is selected as hello local storage settings apply tooall service configurations.</span></span> <span data-ttu-id="5f729-227">Любое другое значение приводит все поля входных hello на странице приветствия отключен.</span><span class="sxs-lookup"><span data-stu-id="5f729-227">Any other value results in all hello input fields on hello page being disabled.</span></span> 

    ![Список "Конфигурация службы"](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab-service-configuration.png)

1. <span data-ttu-id="5f729-229">Выберите запись локального хранилища tooadd **добавить локальное хранилище**.</span><span class="sxs-lookup"><span data-stu-id="5f729-229">tooadd a local storage entry, select **Add Local Storage**.</span></span>

    ![Добавление локального хранилища](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab-add-local-storage.png)

1. <span data-ttu-id="5f729-231">После списка toohello добавления hello новая запись локального хранилища, обновите строку hello в списке hello hello необходимых сведений.</span><span class="sxs-lookup"><span data-stu-id="5f729-231">Once hello new local storage entry has been added toohello list, update hello row in hello list with hello necessary information.</span></span>

    ![Новая запись локального хранилища](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab-new-local-storage.png)

    - <span data-ttu-id="5f729-233">**Имя** -введите имя hello, чтобы получить toouse hello новое локальное хранилище.</span><span class="sxs-lookup"><span data-stu-id="5f729-233">**Name** - Enter hello name that you want toouse for hello new local storage.</span></span>
    - <span data-ttu-id="5f729-234">**Размер (МБ)** -введите hello размер в Мегабайтах, который требуется для hello новое локальное хранилище.</span><span class="sxs-lookup"><span data-stu-id="5f729-234">**Size (MB)** - Enter hello size in MB that you need for hello new local storage.</span></span>
    - <span data-ttu-id="5f729-235">**Очистить при повторном использовании роли** -выберите этот параметр tooremove hello данных в новое локальное хранилище hello при очистке hello виртуальной машины для роли hello.</span><span class="sxs-lookup"><span data-stu-id="5f729-235">**Clean on role recycle** - Select this option tooremove hello data in hello new local storage when hello virtual machine for hello role is recycled.</span></span>

1. <span data-ttu-id="5f729-236">toodelete запись локального хранилища, выберите запись hello, а затем выберите **удалить локальное хранилище**.</span><span class="sxs-lookup"><span data-stu-id="5f729-236">toodelete a local storage entry, select hello entry, and then select **Remove Local Storage**.</span></span>

1. <span data-ttu-id="5f729-237">Из Visual Studio hello панели инструментов выберите **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="5f729-237">From hello Visual Studio, toolbar, select **Save**.</span></span>

## <a name="programmatically-accessing-local-storage"></a><span data-ttu-id="5f729-238">Программный доступ к локальному хранилищу</span><span class="sxs-lookup"><span data-stu-id="5f729-238">Programmatically accessing local storage</span></span>

<span data-ttu-id="5f729-239">В этом разделе показано, как локальное хранилище с помощью C#, написав текстовый файл теста доступ к tooprogrammatically `MyLocalStorageTest.txt`.</span><span class="sxs-lookup"><span data-stu-id="5f729-239">This section illustrates how tooprogrammatically access local storage using C# by writing a test text file `MyLocalStorageTest.txt`.</span></span>  

### <a name="write-a-text-file-toolocal-storage"></a><span data-ttu-id="5f729-240">Запись текстового файла toolocal хранилища</span><span class="sxs-lookup"><span data-stu-id="5f729-240">Write a text file toolocal storage</span></span>

<span data-ttu-id="5f729-241">Привет, следующий код является примером как toowrite текстовый файл toolocal хранилища.</span><span class="sxs-lookup"><span data-stu-id="5f729-241">hello following code shows an example of how toowrite a text file toolocal storage.</span></span> <span data-ttu-id="5f729-242">Замените hello &lt;LocalStorageName > заполнитель hello соответствующее значение.</span><span class="sxs-lookup"><span data-stu-id="5f729-242">Replace hello &lt;LocalStorageName> placeholder with hello appropriate value.</span></span> 

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

### <a name="find-a-file-written-toolocal-storage"></a><span data-ttu-id="5f729-243">Найти файл, написанный toolocal хранилища</span><span class="sxs-lookup"><span data-stu-id="5f729-243">Find a file written toolocal storage</span></span>

<span data-ttu-id="5f729-244">файл hello tooview создается кодом hello в предыдущем разделе hello, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="5f729-244">tooview hello file created by hello code in hello previous section, follow these steps:</span></span>
    
1.  <span data-ttu-id="5f729-245">В области уведомлений Windows hello, щелкните правой кнопкой мыши значок Azure hello и hello контекстном меню, выберите **Показать пользовательский Интерфейс эмулятора вычислений**.</span><span class="sxs-lookup"><span data-stu-id="5f729-245">In hello Windows notification area, right-click hello Azure icon, and, from hello context menu, select **Show Compute Emulator UI**.</span></span> 

    ![Показать пользовательский интерфейс эмулятора вычислений](./media/vs-azure-tools-configure-roles-for-cloud-service/show-compute-emulator.png)

1. <span data-ttu-id="5f729-247">Выберите веб-роли hello.</span><span class="sxs-lookup"><span data-stu-id="5f729-247">Select hello web role.</span></span>

    ![Эмулятор вычислений Azure](./media/vs-azure-tools-configure-roles-for-cloud-service/compute-emulator.png)

1. <span data-ttu-id="5f729-249">На hello **эмулятор вычислений Microsoft Azure** последовательно выберите пункты **средства** > **открыть локальное хранилище**.</span><span class="sxs-lookup"><span data-stu-id="5f729-249">On hello **Microsoft Azure Compute Emulator** menu, select **Tools** > **Open local store**.</span></span>

    ![Пункт меню "Открыть локальное хранилище"](./media/vs-azure-tools-configure-roles-for-cloud-service/compute-emulator-open-local-store-menu.png)

1. <span data-ttu-id="5f729-251">При открытии окна проводника Windows hello, введите "MyLocalStorageTest.txt'' в hello **поиска** текста, а затем выберите **ввод** toostart hello поиска.</span><span class="sxs-lookup"><span data-stu-id="5f729-251">When hello Windows Explorer window opens, enter `MyLocalStorageTest.txt`\` into hello **Search** text box, and select **Enter** toostart hello search.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="5f729-252">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5f729-252">Next steps</span></span>
<span data-ttu-id="5f729-253">Дополнительные сведения о проектах Azure в Visual Studio см. в статье [Настройка проекта облачной службы в Visual Studio](vs-azure-tools-configuring-an-azure-project.md).</span><span class="sxs-lookup"><span data-stu-id="5f729-253">Learn more about Azure projects in Visual Studio by reading [Configuring an Azure Project](vs-azure-tools-configuring-an-azure-project.md).</span></span> <span data-ttu-id="5f729-254">Дополнительные сведения о hello облачной службы схемы путем чтения [Справочник по схеме](https://msdn.microsoft.com/library/azure/dd179398).</span><span class="sxs-lookup"><span data-stu-id="5f729-254">Learn more about hello cloud service schema by reading [Schema Reference](https://msdn.microsoft.com/library/azure/dd179398).</span></span>

