---
title: "Настройка ролей для облачной службы Azure в среде Visual Studio | Документация Майкрософт"
description: "Узнайте, как настроить роли для облачных служб Azure с помощью Visual Studio."
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
ms.openlocfilehash: 17da71ac0c5ab9330b9244c0354e4d161d98229e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="configure-azure-cloud-service-roles-with-visual-studio"></a><span data-ttu-id="ca706-103">Настройка ролей для облачной службы Azure в Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ca706-103">Configure Azure cloud service roles with Visual Studio</span></span>
<span data-ttu-id="ca706-104">Облачной службе Azure можно назначить одну или несколько рабочих ролей или веб-ролей.</span><span class="sxs-lookup"><span data-stu-id="ca706-104">An Azure cloud service can have one or more worker or web roles.</span></span> <span data-ttu-id="ca706-105">Для каждой роли нужно определить способ настройки, а также настроить способ выполнения.</span><span class="sxs-lookup"><span data-stu-id="ca706-105">For each role, you need to define how that role is set up and also configure how that role runs.</span></span> <span data-ttu-id="ca706-106">Дополнительные сведения о ролях в облачных службах см. в видео [Введение в облачные службы Azure](https://channel9.msdn.com/Series/Windows-Azure-Cloud-Services-Tutorials/Introduction-to-Windows-Azure-Cloud-Services).</span><span class="sxs-lookup"><span data-stu-id="ca706-106">To learn more about roles in cloud services, see the video [Introduction to Azure Cloud Services](https://channel9.msdn.com/Series/Windows-Azure-Cloud-Services-Tutorials/Introduction-to-Windows-Azure-Cloud-Services).</span></span> 

<span data-ttu-id="ca706-107">Эта информация для облачной службы хранится в следующих файлах.</span><span class="sxs-lookup"><span data-stu-id="ca706-107">The information for your cloud service is stored in the following files:</span></span>

- <span data-ttu-id="ca706-108">**ServiceDefinition.csdef** — файл определения службы, в котором заданы параметры среды выполнения для облачной службы, в том числе требуемые роли, конечные точки и размер виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="ca706-108">**ServiceDefinition.csdef** - The service definition file defines the runtime settings for your cloud service including what roles are required, endpoints, and virtual machine size.</span></span> <span data-ttu-id="ca706-109">Данные хранящиеся в файле `ServiceDefinition.csdef`, нельзя изменить во время выполнения роли.</span><span class="sxs-lookup"><span data-stu-id="ca706-109">None of the data stored in `ServiceDefinition.csdef` can be changed when your role is running.</span></span>
- <span data-ttu-id="ca706-110">**ServiceConfiguration.cscfg** — файл конфигурации службы, в котором задано количество выполняемых экземпляров роли и значения параметров, определенных для роли.</span><span class="sxs-lookup"><span data-stu-id="ca706-110">**ServiceConfiguration.cscfg** - The service configuration file configures how many instances of a role are run and the values of the settings defined for a role.</span></span> <span data-ttu-id="ca706-111">Данные, хранящиеся в файле `ServiceConfiguration.cscfg`, можно изменить во время выполнения роли.</span><span class="sxs-lookup"><span data-stu-id="ca706-111">The data stored in `ServiceConfiguration.cscfg` can be changed while your role is running.</span></span>

<span data-ttu-id="ca706-112">Для хранения различных значений параметров, контролирующих выполнение роли, можно задать несколько конфигураций службы.</span><span class="sxs-lookup"><span data-stu-id="ca706-112">To store different values for the settings that control how a role runs, you can define multiple service configurations.</span></span> <span data-ttu-id="ca706-113">Разные конфигурации службы можно использовать для разных сред развертывания.</span><span class="sxs-lookup"><span data-stu-id="ca706-113">You can use a different service configuration for each deployment environment.</span></span> <span data-ttu-id="ca706-114">Например, можно задать строку подключения к учетной записи хранения, чтобы использовать локальный эмулятор службы хранилища Azure в конфигурации локальной службы. Таким образом вы сможете создать другую конфигурацию службы для использования облачной службы хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="ca706-114">For example, you can set your storage account connection string to use the local Azure storage emulator in a local service configuration and create another service configuration to use Azure storage in the cloud.</span></span>

<span data-ttu-id="ca706-115">При создании облачной службы Azure в среде Visual Studio к вашему проекту Azure добавляются две автоматически созданные конфигурации службы:</span><span class="sxs-lookup"><span data-stu-id="ca706-115">When you create an Azure cloud service in Visual Studio, two service configurations are automatically created and added to your Azure project:</span></span>

- `ServiceConfiguration.Cloud.cscfg`
- `ServiceConfiguration.Local.cscfg`

## <a name="configure-an-azure-cloud-service"></a><span data-ttu-id="ca706-116">Настройка облачной службы Azure</span><span class="sxs-lookup"><span data-stu-id="ca706-116">Configure an Azure cloud service</span></span>
<span data-ttu-id="ca706-117">В среде Visual Studio можно настроить облачную службу Azure, используя обозреватель решений, как описано ниже.</span><span class="sxs-lookup"><span data-stu-id="ca706-117">You can configure an Azure cloud service from Solution Explorer in Visual Studio, as shown in the following steps:</span></span>

1. <span data-ttu-id="ca706-118">Создайте или откройте проект облачной службы Azure в среде Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ca706-118">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="ca706-119">В **обозревателе решений** щелкните проект правой кнопкой мыши и в контекстном меню выберите пункт **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="ca706-119">In **Solution Explorer**, right-click the project, and, from the context menu, select **Properties**.</span></span>
   
    ![Контекстное меню проекта в обозревателе решений](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-project-context-menu.png)

1. <span data-ttu-id="ca706-121">На странице свойств проекта выберите вкладку **Разработка**.</span><span class="sxs-lookup"><span data-stu-id="ca706-121">In the project's properties page, select the **Development** tab.</span></span> 

    ![Страница свойств проекта — вкладка "Разработка"](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-development-tab.png)

1. <span data-ttu-id="ca706-123">В списке **Конфигурация службы** выберите имя конфигурации службы, которую нужно изменить.</span><span class="sxs-lookup"><span data-stu-id="ca706-123">In the **Service Configuration** list, select the name of the service configuration that you want to edit.</span></span> <span data-ttu-id="ca706-124">(Если нужно изменить все конфигурации службы для этой роли, выберите пункт **Все конфигурации**.)</span><span class="sxs-lookup"><span data-stu-id="ca706-124">(If you want to make changes to all the service configurations for this role, select **All Configurations**.)</span></span>
   
    > [!IMPORTANT]
    > <span data-ttu-id="ca706-125">При выборе конкретной конфигурации службы некоторые ее свойства будут отключены, так как их можно задать только для всех конфигураций.</span><span class="sxs-lookup"><span data-stu-id="ca706-125">If you choose a specific service configuration, some properties are disabled because they can only be set for all configurations.</span></span> <span data-ttu-id="ca706-126">Чтобы изменить эти свойства, выберите пункт **Все конфигурации**.</span><span class="sxs-lookup"><span data-stu-id="ca706-126">To edit these properties, you must select **All Configurations**.</span></span>
    > 
    > 
   
    ![Список конфигураций службы для облачной службы Azure](./media/vs-azure-tools-configure-roles-for-cloud-service/cloud-service-service-configuration-property.png)

## <a name="change-the-number-of-role-instances"></a><span data-ttu-id="ca706-128">Изменение количества экземпляров роли</span><span class="sxs-lookup"><span data-stu-id="ca706-128">Change the number of role instances</span></span>
<span data-ttu-id="ca706-129">Чтобы повысить производительность облачной службы, можно изменить количество запущенных экземпляров роли в зависимости от количества пользователей или нагрузки, ожидаемой для определенной роли.</span><span class="sxs-lookup"><span data-stu-id="ca706-129">To improve the performance of your cloud service, you can change the number of instances of a role that are running, based on the number of users or the load expected for a particular role.</span></span> <span data-ttu-id="ca706-130">При запуске облачной службы в Azure для каждого экземпляра роли создается отдельная виртуальная машина.</span><span class="sxs-lookup"><span data-stu-id="ca706-130">A separate virtual machine is created for each instance of a role when the cloud service runs in Azure.</span></span> <span data-ttu-id="ca706-131">От этого зависят выставленные счета за развертывание этой облачной службы.</span><span class="sxs-lookup"><span data-stu-id="ca706-131">This affects the billing for the deployment of this cloud service.</span></span> <span data-ttu-id="ca706-132">Дополнительные сведения о плате за использование Azure см. в статье [Расшифровка счета за использование Microsoft Azure](billing/billing-understand-your-bill.md).</span><span class="sxs-lookup"><span data-stu-id="ca706-132">For more information about billing, see [Understand your bill for Microsoft Azure](billing/billing-understand-your-bill.md).</span></span>

1. <span data-ttu-id="ca706-133">Создайте или откройте проект облачной службы Azure в среде Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ca706-133">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="ca706-134">В **обозревателе решений** разверните узел проекта.</span><span class="sxs-lookup"><span data-stu-id="ca706-134">In **Solution Explorer**, expand the project node.</span></span> <span data-ttu-id="ca706-135">В узле **Роли** щелкните правой кнопкой мыши роль, которую нужно обновить, и в контекстном меню выберите пункт **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="ca706-135">Under the **Roles** node, right-click the role you want to update, and, from the context menu, select **Properties**.</span></span>

    ![Контекстное меню роли в обозревателе решений Azure](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. <span data-ttu-id="ca706-137">Перейдите на вкладку **Конфигурация**.</span><span class="sxs-lookup"><span data-stu-id="ca706-137">Select the **Configuration** tab.</span></span>

    ![Вкладка "Конфигурация"](./media/vs-azure-tools-configure-roles-for-cloud-service/role-configuration-properties-page.png)

1. <span data-ttu-id="ca706-139">В списке **Конфигурация службы** выберите конфигурацию службы, которую нужно обновить.</span><span class="sxs-lookup"><span data-stu-id="ca706-139">In the **Service Configuration** list, select the service configuration that you want to update.</span></span>
   
    ![Список "Конфигурация службы"](./media/vs-azure-tools-configure-roles-for-cloud-service/role-configuration-properties-page-select-configuration.png)

1. <span data-ttu-id="ca706-141">В поле **Количество экземпляров** введите количество экземпляров, которые будут запущены для этой роли.</span><span class="sxs-lookup"><span data-stu-id="ca706-141">In the **Instance count** text box, enter the number of instances that you want to start for this role.</span></span> <span data-ttu-id="ca706-142">Каждый экземпляр выполняется на отдельной виртуальной машине при публикации облачной службы в Azure.</span><span class="sxs-lookup"><span data-stu-id="ca706-142">Each instance runs on a separate virtual machine when you publish the cloud service to Azure.</span></span>

    ![Обновление количества экземпляров](./media/vs-azure-tools-configure-roles-for-cloud-service/role-configuration-properties-page-instance-count.png)

1. <span data-ttu-id="ca706-144">На панели инструментов Visual Studio щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="ca706-144">From the Visual Studio, toolbar, select **Save**.</span></span>

## <a name="manage-connection-strings-for-storage-accounts"></a><span data-ttu-id="ca706-145">Управление строками подключения для учетных записей хранения</span><span class="sxs-lookup"><span data-stu-id="ca706-145">Manage connection strings for storage accounts</span></span>
<span data-ttu-id="ca706-146">Вы можете добавлять, удалять или изменять строки подключения для конфигураций службы.</span><span class="sxs-lookup"><span data-stu-id="ca706-146">You can add, remove, or modify connection strings for your service configurations.</span></span> <span data-ttu-id="ca706-147">Например, вы можете использовать строку локального подключения для конфигурации локальной службы, которая имеет значение `UseDevelopmentStorage=true`.</span><span class="sxs-lookup"><span data-stu-id="ca706-147">For example, you might want a local connection string for a local service configuration that has a value of `UseDevelopmentStorage=true`.</span></span> <span data-ttu-id="ca706-148">Можно также настроить конфигурацию облачной службы, которая использует учетную запись хранения в Azure.</span><span class="sxs-lookup"><span data-stu-id="ca706-148">You might also want to configure a cloud service configuration that uses a storage account in Azure.</span></span>

> [!WARNING]
> <span data-ttu-id="ca706-149">Когда вы вводите ключ учетной записи хранения Azure для строки подключения к учетной записи хранения, эти сведения сохраняются локально в CSCFG-файле.</span><span class="sxs-lookup"><span data-stu-id="ca706-149">When you enter the Azure storage account key information for a storage account connection string, this information is stored locally in the service configuration file.</span></span> <span data-ttu-id="ca706-150">Тем не менее эти сведения в настоящее время не хранятся в виде зашифрованного текста.</span><span class="sxs-lookup"><span data-stu-id="ca706-150">However, this information is currently not stored as encrypted text.</span></span>
> 
> 

<span data-ttu-id="ca706-151">Использование разных значений для разных конфигураций службы избавляет от необходимости использовать разные строки подключения в облачной службе или изменять код при публикации этой службы в Azure.</span><span class="sxs-lookup"><span data-stu-id="ca706-151">By using a different value for each service configuration, you do not have to use different connection strings in your cloud service or modify your code when you publish your cloud service to Azure.</span></span> <span data-ttu-id="ca706-152">Для строки подключения в коде можно использовать одно и то же имя и разные значения в зависимости от конфигурации службы, выбранной при сборке или публикации облачной службы.</span><span class="sxs-lookup"><span data-stu-id="ca706-152">You can use the same name for the connection string in your code and the value is different, based on the service configuration that you select when you build your cloud service or when you publish it.</span></span>

1. <span data-ttu-id="ca706-153">Создайте или откройте проект облачной службы Azure в среде Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ca706-153">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="ca706-154">В **обозревателе решений** разверните узел проекта.</span><span class="sxs-lookup"><span data-stu-id="ca706-154">In **Solution Explorer**, expand the project node.</span></span> <span data-ttu-id="ca706-155">В узле **Роли** щелкните правой кнопкой мыши роль, которую нужно обновить, и в контекстном меню выберите пункт **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="ca706-155">Under the **Roles** node, right-click the role you want to update, and, from the context menu, select **Properties**.</span></span>

    ![Контекстное меню роли в обозревателе решений Azure](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. <span data-ttu-id="ca706-157">Перейдите на вкладку **Параметры**.</span><span class="sxs-lookup"><span data-stu-id="ca706-157">Select the **Settings** tab.</span></span>

    ![Вкладка "Параметры"](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab.png)

1. <span data-ttu-id="ca706-159">В списке **Конфигурация службы** выберите конфигурацию службы, которую нужно обновить.</span><span class="sxs-lookup"><span data-stu-id="ca706-159">In the **Service Configuration** list, select the service configuration that you want to update.</span></span>

    ![Конфигурация службы](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-select-configuration.png)

1. <span data-ttu-id="ca706-161">Чтобы добавить строку подключения, нажмите кнопку **Добавить параметр**.</span><span class="sxs-lookup"><span data-stu-id="ca706-161">To add a connection string, select **Add Setting**.</span></span>

    ![Добавление строки подключения](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting.png)

1. <span data-ttu-id="ca706-163">После добавления в список нового параметра введите необходимые сведения в строку списка.</span><span class="sxs-lookup"><span data-stu-id="ca706-163">Once the new setting has been added to the list, update the row in the list with the necessary information.</span></span>

    ![Новая строка подключения](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting-new-setting.png)

    - <span data-ttu-id="ca706-165">Поле **Имя**. Введите имя, которое будет использоваться для строки подключения.</span><span class="sxs-lookup"><span data-stu-id="ca706-165">**Name** - Enter the name that you want to use for the connection string.</span></span>
    - <span data-ttu-id="ca706-166">Поле **Тип**. В раскрывающемся списке выберите пункт **Строка подключения**.</span><span class="sxs-lookup"><span data-stu-id="ca706-166">**Type** - Select **Connection String** from the drop-down list.</span></span>
    - <span data-ttu-id="ca706-167">Поле **Значение**. Здесь вы можете ввести строку подключения непосредственно в ячейку **Значение** или щелкнуть многоточие (…), чтобы продолжить работу в диалоговом окне **Создание строки подключения к хранилищу**.</span><span class="sxs-lookup"><span data-stu-id="ca706-167">**Value** - You can either enter the connection string directly into the **Value** cell, or select the ellipsis (...) to work in the **Create Storage Connection String** dialog.</span></span>  

1. <span data-ttu-id="ca706-168">В диалоговом окне **Создание строки подключения к хранилищу** выберите один из вариантов для параметра **Подключиться с помощью**.</span><span class="sxs-lookup"><span data-stu-id="ca706-168">In the **Create Storage Connection String** dialog, select an option for **Connect using**.</span></span> <span data-ttu-id="ca706-169">Затем следуйте инструкциям для выбранного варианта.</span><span class="sxs-lookup"><span data-stu-id="ca706-169">Then follow the instructions for the option you select:</span></span>

    - <span data-ttu-id="ca706-170">**Эмулятор хранилища Microsoft Azure**. Если вы выбрали этот вариант, остальные параметры в диалоговом окне будут отключены, так как они применяются только к Azure.</span><span class="sxs-lookup"><span data-stu-id="ca706-170">**Microsoft Azure storage emulator** - If you select this option, the remaining settings on the dialog are disabled as they apply only to Azure.</span></span> <span data-ttu-id="ca706-171">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="ca706-171">Select **OK**.</span></span>
    - <span data-ttu-id="ca706-172">**Ваша подписка**. Если выбран этот вариант, воспользуйтесь раскрывающимся списком, чтобы выбрать учетную запись Майкрософт и войти в нее или добавить учетную запись Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="ca706-172">**Your subscription** - If you select this option, use the dropdown list to either select and sign into a Microsoft account, or add a Microsoft account.</span></span> <span data-ttu-id="ca706-173">Выберите подписку и учетную запись хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="ca706-173">Select an Azure subscription and storage account.</span></span> <span data-ttu-id="ca706-174">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="ca706-174">Select **OK**.</span></span>
    - <span data-ttu-id="ca706-175">**Введенные вручную учетные данные**. Введите имя учетной записи хранения, а также первичный или вторичный ключ.</span><span class="sxs-lookup"><span data-stu-id="ca706-175">**Manually entered credentials** - Enter the storage account name, and either the primary or second key.</span></span> <span data-ttu-id="ca706-176">Выберите вариант **подключения** (в большинстве случаев рекомендуется использовать протокол HTTPS). Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="ca706-176">Select an option for **Connection** (HTTPS is recommended for most scenarios.) Select **OK**.</span></span>

1. <span data-ttu-id="ca706-177">Чтобы удалить строку подключения, выберите ее, а затем нажмите кнопку **Удалить параметр**.</span><span class="sxs-lookup"><span data-stu-id="ca706-177">To delete a connection string, select the connection string, and then select **Remove Setting**.</span></span>

1. <span data-ttu-id="ca706-178">На панели инструментов Visual Studio щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="ca706-178">From the Visual Studio, toolbar, select **Save**.</span></span>

## <a name="programmatically-access-a-connection-string"></a><span data-ttu-id="ca706-179">Программный доступ к строке подключения</span><span class="sxs-lookup"><span data-stu-id="ca706-179">Programmatically access a connection string</span></span>

<span data-ttu-id="ca706-180">Ниже показано, как получить программный доступ к строке подключения с помощью C#.</span><span class="sxs-lookup"><span data-stu-id="ca706-180">The following steps show how to programmatically access a connection string using C#.</span></span>

1. <span data-ttu-id="ca706-181">Добавьте следующие директивы using в файл C#, в котором планируется использовать параметр:</span><span class="sxs-lookup"><span data-stu-id="ca706-181">Add the following using directives to a C# file where you are going to use the setting:</span></span>

    ```csharp
    using Microsoft.WindowsAzure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.ServiceRuntime;
    ```

1. <span data-ttu-id="ca706-182">В следующем примере показано, как получить доступ к строке подключения.</span><span class="sxs-lookup"><span data-stu-id="ca706-182">The following code illustrates an example of how to access a connection string.</span></span> <span data-ttu-id="ca706-183">Замените заполнитель &lt;ConnectionStringName> соответствующим значением.</span><span class="sxs-lookup"><span data-stu-id="ca706-183">Replace the &lt;ConnectionStringName> placeholder with the appropriate value.</span></span> 

    ```csharp
    // Setup the connection to Azure Storage
    var storageAccount = CloudStorageAccount.Parse(RoleEnvironment.GetConfigurationSettingValue("<ConnectionStringName>"));
    ```

## <a name="add-custom-settings-to-use-in-your-azure-cloud-service"></a><span data-ttu-id="ca706-184">Добавление пользовательских параметров для использования в облачной службе Azure</span><span class="sxs-lookup"><span data-stu-id="ca706-184">Add custom settings to use in your Azure cloud service</span></span>
<span data-ttu-id="ca706-185">Пользовательские параметры в файле конфигурации службы позволяют добавлять имя и значение строки для конкретной конфигурации службы.</span><span class="sxs-lookup"><span data-stu-id="ca706-185">Custom settings in the service configuration file let you add a name and value for a string for a specific service configuration.</span></span> <span data-ttu-id="ca706-186">Можно использовать этот параметр, чтобы настроить функцию в облачной службе: значение параметра считывается и используется для управления логикой в коде.</span><span class="sxs-lookup"><span data-stu-id="ca706-186">You might choose to use this setting to configure a feature in your cloud service by reading the value of the setting and using this value to control the logic in your code.</span></span> <span data-ttu-id="ca706-187">Вы можете изменять эти значения конфигурации службы без необходимости выполнять повторную сборку пакета служб, а также при запуске облачной службы.</span><span class="sxs-lookup"><span data-stu-id="ca706-187">You can change these service configuration values without having to rebuild your service package or when your cloud service is running.</span></span> <span data-ttu-id="ca706-188">Ваш код может проверять наличие уведомлений об изменении параметра.</span><span class="sxs-lookup"><span data-stu-id="ca706-188">Your code can check for notifications of when a setting changes.</span></span> <span data-ttu-id="ca706-189">См. статью, посвященную [событию RoleEnvironment.Changing](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changing.aspx).</span><span class="sxs-lookup"><span data-stu-id="ca706-189">See [RoleEnvironment.Changing Event](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changing.aspx).</span></span>

<span data-ttu-id="ca706-190">Вы можете добавлять, удалять или изменять пользовательские параметры для конфигураций службы.</span><span class="sxs-lookup"><span data-stu-id="ca706-190">You can add, remove, or modify custom settings for your service configurations.</span></span> <span data-ttu-id="ca706-191">Также можно использовать разные значения этих строк для разных конфигураций службы.</span><span class="sxs-lookup"><span data-stu-id="ca706-191">You might want different values for these strings for different service configurations.</span></span>

<span data-ttu-id="ca706-192">Использование разных значений для разных конфигураций службы избавляет от необходимости использовать разные строки в облачной службе или изменять код при публикации этой службы в Azure.</span><span class="sxs-lookup"><span data-stu-id="ca706-192">By using a different value for each service configuration, you do not have to use different strings in your cloud service or modify your code when you publish your cloud service to Azure.</span></span> <span data-ttu-id="ca706-193">Для строки в коде можно использовать одно и то же имя и разные значения в зависимости от конфигурации службы, выбранной при сборке или публикации облачной службы.</span><span class="sxs-lookup"><span data-stu-id="ca706-193">You can use the same name for the string in your code and the value is different, based on the service configuration that you select when you build your cloud service or when you publish it.</span></span>

1. <span data-ttu-id="ca706-194">Создайте или откройте проект облачной службы Azure в среде Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ca706-194">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="ca706-195">В **обозревателе решений** разверните узел проекта.</span><span class="sxs-lookup"><span data-stu-id="ca706-195">In **Solution Explorer**, expand the project node.</span></span> <span data-ttu-id="ca706-196">В узле **Роли** щелкните правой кнопкой мыши роль, которую нужно обновить, и в контекстном меню выберите пункт **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="ca706-196">Under the **Roles** node, right-click the role you want to update, and, from the context menu, select **Properties**.</span></span>

    ![Контекстное меню роли в обозревателе решений Azure](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. <span data-ttu-id="ca706-198">Перейдите на вкладку **Параметры**.</span><span class="sxs-lookup"><span data-stu-id="ca706-198">Select the **Settings** tab.</span></span>

    ![Вкладка "Параметры"](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab.png)

1. <span data-ttu-id="ca706-200">В списке **Конфигурация службы** выберите конфигурацию службы, которую нужно обновить.</span><span class="sxs-lookup"><span data-stu-id="ca706-200">In the **Service Configuration** list, select the service configuration that you want to update.</span></span>

    ![Список "Конфигурация службы"](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-select-configuration.png)

1. <span data-ttu-id="ca706-202">Чтобы добавить пользовательский параметр, нажмите кнопку **Добавить параметр**.</span><span class="sxs-lookup"><span data-stu-id="ca706-202">To add a custom setting, select **Add Setting**.</span></span>

    ![Добавление пользовательского параметра](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting.png)

1. <span data-ttu-id="ca706-204">После добавления в список нового параметра введите необходимые сведения в строку списка.</span><span class="sxs-lookup"><span data-stu-id="ca706-204">Once the new setting has been added to the list, update the row in the list with the necessary information.</span></span>

    ![Новый пользовательский параметр](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting-new-setting.png)

    - <span data-ttu-id="ca706-206">В поле **Имя** введите имя параметра.</span><span class="sxs-lookup"><span data-stu-id="ca706-206">**Name** - Enter the name of the setting.</span></span>
    - <span data-ttu-id="ca706-207">В раскрывающемся списке **Тип** выберите пункт **Строка**.</span><span class="sxs-lookup"><span data-stu-id="ca706-207">**Type** - Select **String** from the drop-down list.</span></span>
    - <span data-ttu-id="ca706-208">В поле **Значение** задайте значение параметра.</span><span class="sxs-lookup"><span data-stu-id="ca706-208">**Value** - Enter the value of the setting.</span></span> <span data-ttu-id="ca706-209">Вы можете ввести значение непосредственно в ячейку **Значение** или щелкнуть многоточие (…), чтобы задать значение в диалоговом окне **Изменить строку**.</span><span class="sxs-lookup"><span data-stu-id="ca706-209">You can either enter the value directly into the **Value** cell, or select the ellipsis (...) to enter the value in the **Edit String** dialog.</span></span>  

1. <span data-ttu-id="ca706-210">Чтобы удалить пользовательский параметр, сначала выберите его, а затем нажмите кнопку **Удалить параметр**.</span><span class="sxs-lookup"><span data-stu-id="ca706-210">To delete a custom setting, select the setting, and then select **Remove Setting**.</span></span>

1. <span data-ttu-id="ca706-211">На панели инструментов Visual Studio щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="ca706-211">From the Visual Studio, toolbar, select **Save**.</span></span>

## <a name="programmatically-access-a-custom-settings-value"></a><span data-ttu-id="ca706-212">Программный доступ к значению пользовательского параметра</span><span class="sxs-lookup"><span data-stu-id="ca706-212">Programmatically access a custom setting's value</span></span>
 
<span data-ttu-id="ca706-213">Ниже показано, как получить программный доступ к пользовательскому параметру с помощью C#.</span><span class="sxs-lookup"><span data-stu-id="ca706-213">The following steps show how to programmatically access a custom setting using C#.</span></span>

1. <span data-ttu-id="ca706-214">Добавьте следующие директивы using в файл C#, в котором планируется использовать параметр:</span><span class="sxs-lookup"><span data-stu-id="ca706-214">Add the following using directives to a C# file where you are going to use the setting:</span></span>

    ```csharp
    using Microsoft.WindowsAzure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.ServiceRuntime;
    ```

1. <span data-ttu-id="ca706-215">В следующем примере показано, как получить доступ к пользовательскому параметру.</span><span class="sxs-lookup"><span data-stu-id="ca706-215">The following code illustrates an example of how to access a custom setting.</span></span> <span data-ttu-id="ca706-216">Замените заполнитель &lt;SettingName> соответствующим значением.</span><span class="sxs-lookup"><span data-stu-id="ca706-216">Replace the &lt;SettingName> placeholder with the appropriate value.</span></span> 
    
    ```csharp
    var settingValue = RoleEnvironment.GetConfigurationSettingValue("<SettingName>");
    ```

## <a name="manage-local-storage-for-each-role-instance"></a><span data-ttu-id="ca706-217">Управление локальным хранилищем для каждого экземпляра роли</span><span class="sxs-lookup"><span data-stu-id="ca706-217">Manage local storage for each role instance</span></span>
<span data-ttu-id="ca706-218">Каждому экземпляру роли можно назначить хранилище локальной файловой системы.</span><span class="sxs-lookup"><span data-stu-id="ca706-218">You can add local file system storage for each instance of a role.</span></span> <span data-ttu-id="ca706-219">Данные, находящиеся в этом хранилище, недоступны для других экземпляров роли, для которой хранятся данные, или для других ролей.</span><span class="sxs-lookup"><span data-stu-id="ca706-219">The data stored in that storage is not accessible by other instances of the role for which the data is stored, or by other roles.</span></span>  

1. <span data-ttu-id="ca706-220">Создайте или откройте проект облачной службы Azure в среде Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ca706-220">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="ca706-221">В **обозревателе решений** разверните узел проекта.</span><span class="sxs-lookup"><span data-stu-id="ca706-221">In **Solution Explorer**, expand the project node.</span></span> <span data-ttu-id="ca706-222">В узле **Роли** щелкните правой кнопкой мыши роль, которую нужно обновить, и в контекстном меню выберите пункт **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="ca706-222">Under the **Roles** node, right-click the role you want to update, and, from the context menu, select **Properties**.</span></span>

    ![Контекстное меню роли в обозревателе решений Azure](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. <span data-ttu-id="ca706-224">Перейдите на вкладку **Локальное хранилище**.</span><span class="sxs-lookup"><span data-stu-id="ca706-224">Select the **Local Storage** tab.</span></span>

    ![Вкладка "Локальное хранилище"](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab.png)

1. <span data-ttu-id="ca706-226">Убедитесь, что в списке **Конфигурация службы** выбран параметр **Все конфигурации**, так как локальные параметры хранилища применяются ко всем конфигурациям службы.</span><span class="sxs-lookup"><span data-stu-id="ca706-226">In the **Service Configuration** list, ensure that **All Configurations** is selected as the local storage settings apply to all service configurations.</span></span> <span data-ttu-id="ca706-227">Если выбрано любое другое значение, это приведет к отключению параметров во всех полях ввода данных на странице.</span><span class="sxs-lookup"><span data-stu-id="ca706-227">Any other value results in all the input fields on the page being disabled.</span></span> 

    ![Список "Конфигурация службы"](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab-service-configuration.png)

1. <span data-ttu-id="ca706-229">Для добавления записи локального хранилища щелкните **Добавить локальное хранилище**.</span><span class="sxs-lookup"><span data-stu-id="ca706-229">To add a local storage entry, select **Add Local Storage**.</span></span>

    ![Добавление локального хранилища](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab-add-local-storage.png)

1. <span data-ttu-id="ca706-231">После добавления в список новой записи локального хранилища введите необходимые сведения в строку списка.</span><span class="sxs-lookup"><span data-stu-id="ca706-231">Once the new local storage entry has been added to the list, update the row in the list with the necessary information.</span></span>

    ![Новая запись локального хранилища](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab-new-local-storage.png)

    - <span data-ttu-id="ca706-233">В поле **Имя** введите имя, которое будет использоваться для нового локального хранилища.</span><span class="sxs-lookup"><span data-stu-id="ca706-233">**Name** - Enter the name that you want to use for the new local storage.</span></span>
    - <span data-ttu-id="ca706-234">В поле **Размер (МБ)** задайте необходимый размер нового локального хранилища в мегабайтах.</span><span class="sxs-lookup"><span data-stu-id="ca706-234">**Size (MB)** - Enter the size in MB that you need for the new local storage.</span></span>
    - <span data-ttu-id="ca706-235">В поле **Очистить при повторном использовании роли** установите флажок, чтобы удалить данные из нового локального хранилища при перезапуске виртуальной машины для этой роли.</span><span class="sxs-lookup"><span data-stu-id="ca706-235">**Clean on role recycle** - Select this option to remove the data in the new local storage when the virtual machine for the role is recycled.</span></span>

1. <span data-ttu-id="ca706-236">Чтобы удалить запись локального хранилища, выберите запись, а затем нажмите кнопку **Удалить локальное хранилище**.</span><span class="sxs-lookup"><span data-stu-id="ca706-236">To delete a local storage entry, select the entry, and then select **Remove Local Storage**.</span></span>

1. <span data-ttu-id="ca706-237">На панели инструментов Visual Studio щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="ca706-237">From the Visual Studio, toolbar, select **Save**.</span></span>

## <a name="programmatically-accessing-local-storage"></a><span data-ttu-id="ca706-238">Программный доступ к локальному хранилищу</span><span class="sxs-lookup"><span data-stu-id="ca706-238">Programmatically accessing local storage</span></span>

<span data-ttu-id="ca706-239">В этом разделе показано, как получить программный доступ к локальному хранилищу, написав тестовый текстовый файл `MyLocalStorageTest.txt` с помощью C#.</span><span class="sxs-lookup"><span data-stu-id="ca706-239">This section illustrates how to programmatically access local storage using C# by writing a test text file `MyLocalStorageTest.txt`.</span></span>  

### <a name="write-a-text-file-to-local-storage"></a><span data-ttu-id="ca706-240">Написание текстового файла для локального хранилища</span><span class="sxs-lookup"><span data-stu-id="ca706-240">Write a text file to local storage</span></span>

<span data-ttu-id="ca706-241">В следующем примере показано, как написать текстовый файл для локального хранилища.</span><span class="sxs-lookup"><span data-stu-id="ca706-241">The following code shows an example of how to write a text file to local storage.</span></span> <span data-ttu-id="ca706-242">Замените заполнитель &lt;LocalStorageName> соответствующим значением.</span><span class="sxs-lookup"><span data-stu-id="ca706-242">Replace the &lt;LocalStorageName> placeholder with the appropriate value.</span></span> 

    ```csharp
    // Retrieve an object that points to the local storage resource
    LocalResource localResource = RoleEnvironment.GetLocalResource("<LocalStorageName>");
    
    //Define the file name and path
    string[] paths = { localResource.RootPath, "MyLocalStorageTest.txt" };
    String filePath = Path.Combine(paths);
    
    using (FileStream writeStream = File.Create(filePath))
    {
        Byte[] textToWrite = new UTF8Encoding(true).GetBytes("Testing Web role storage");
        writeStream.Write(textToWrite, 0, textToWrite.Length);
    }

    ```

### <a name="find-a-file-written-to-local-storage"></a><span data-ttu-id="ca706-243">Поиск файла, написанного для локального хранилища</span><span class="sxs-lookup"><span data-stu-id="ca706-243">Find a file written to local storage</span></span>

<span data-ttu-id="ca706-244">Чтобы просмотреть файл, созданный с помощью кода из предыдущего раздела, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="ca706-244">To view the file created by the code in the previous section, follow these steps:</span></span>
    
1.  <span data-ttu-id="ca706-245">В области уведомлений Windows щелкните правой кнопкой мыши значок Azure и в контекстном меню выберите пункт **Show Compute Emulator UI** (Показать пользовательский интерфейс эмулятора вычислений).</span><span class="sxs-lookup"><span data-stu-id="ca706-245">In the Windows notification area, right-click the Azure icon, and, from the context menu, select **Show Compute Emulator UI**.</span></span> 

    ![Показать пользовательский интерфейс эмулятора вычислений](./media/vs-azure-tools-configure-roles-for-cloud-service/show-compute-emulator.png)

1. <span data-ttu-id="ca706-247">Выберите веб-роль.</span><span class="sxs-lookup"><span data-stu-id="ca706-247">Select the web role.</span></span>

    ![Эмулятор вычислений Azure](./media/vs-azure-tools-configure-roles-for-cloud-service/compute-emulator.png)

1. <span data-ttu-id="ca706-249">В меню **Эмулятор вычислений Microsoft Azure** выберите **Средства** > **Open local store** (Открыть локальное хранилище).</span><span class="sxs-lookup"><span data-stu-id="ca706-249">On the **Microsoft Azure Compute Emulator** menu, select **Tools** > **Open local store**.</span></span>

    ![Пункт меню "Открыть локальное хранилище"](./media/vs-azure-tools-configure-roles-for-cloud-service/compute-emulator-open-local-store-menu.png)

1. <span data-ttu-id="ca706-251">Когда откроется окно проводника Windows, введите в текстовое поле **поиска** запрос "MyLocalStorageTest.txt'' и нажмите клавишу **ВВОД**, чтобы начать поиск.</span><span class="sxs-lookup"><span data-stu-id="ca706-251">When the Windows Explorer window opens, enter `MyLocalStorageTest.txt`\` into the **Search** text box, and select **Enter** to start the search.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="ca706-252">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ca706-252">Next steps</span></span>
<span data-ttu-id="ca706-253">Дополнительные сведения о проектах Azure в Visual Studio см. в статье [Настройка проекта облачной службы в Visual Studio](vs-azure-tools-configuring-an-azure-project.md).</span><span class="sxs-lookup"><span data-stu-id="ca706-253">Learn more about Azure projects in Visual Studio by reading [Configuring an Azure Project](vs-azure-tools-configuring-an-azure-project.md).</span></span> <span data-ttu-id="ca706-254">Дополнительные сведения о схеме облачной службы см. в статье [Справка по схемам Windows Azure](https://msdn.microsoft.com/library/azure/dd179398).</span><span class="sxs-lookup"><span data-stu-id="ca706-254">Learn more about the cloud service schema by reading [Schema Reference](https://msdn.microsoft.com/library/azure/dd179398).</span></span>

