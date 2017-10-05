---
title: "Установка MongoDB на виртуальной машине Windows в Azure | Документация Майкрософт"
description: "Узнайте, как установить MongoDB на виртуальную машину Azure под управлением Windows Server 2012 R2, созданную посредством модели развертывания с помощью Resource Manager."
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 53faf630-8da5-4955-8d0b-6e829bf30cba
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: db1a550b9273925b304fe4280f2a1b0e115f856d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="install-and-configure-mongodb-on-a-windows-vm-in-azure"></a><span data-ttu-id="9ad8f-103">Установка и настройка базы данных MongoDB на виртуальной машине Windows в Azure</span><span class="sxs-lookup"><span data-stu-id="9ad8f-103">Install and configure MongoDB on a Windows VM in Azure</span></span>
<span data-ttu-id="9ad8f-104">[MongoDB](http://www.mongodb.org) — это популярная высокопроизводительная база данных NoSQL с открытым кодом.</span><span class="sxs-lookup"><span data-stu-id="9ad8f-104">[MongoDB](http://www.mongodb.org) is a popular open-source, high-performance NoSQL database.</span></span> <span data-ttu-id="9ad8f-105">В этой статье приведены инструкции по установке и настройке MongoDB на виртуальной машине Windows Server 2012 R2 в Azure.</span><span class="sxs-lookup"><span data-stu-id="9ad8f-105">This article guides you through installing and configuring MongoDB on a Windows Server 2012 R2 virtual machine (VM) in Azure.</span></span> <span data-ttu-id="9ad8f-106">[MongoDB можно также установить на виртуальной машине Linux в Azure](../linux/install-mongodb.md).</span><span class="sxs-lookup"><span data-stu-id="9ad8f-106">You can also [install MongoDB on a Linux VM in Azure](../linux/install-mongodb.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9ad8f-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="9ad8f-107">Prerequisites</span></span>
<span data-ttu-id="9ad8f-108">Прежде чем установить и настроить MongoDB, необходимо создать виртуальную машину и по возможности добавить в нее диск данных.</span><span class="sxs-lookup"><span data-stu-id="9ad8f-108">Before you install and configure MongoDB, you need to create a VM and, ideally, add a data disk to it.</span></span> <span data-ttu-id="9ad8f-109">С помощью приведенных ниже ссылок можно ознакомиться со статьями, в которых описывается создание виртуальной машины и добавление диска данных.</span><span class="sxs-lookup"><span data-stu-id="9ad8f-109">See the following articles to create a VM and add a data disk:</span></span>

* <span data-ttu-id="9ad8f-110">Создайте виртуальную машину Windows на [портале Azure](quick-create-portal.md) или с помощью [PowerShell](quick-create-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="9ad8f-110">Create a Windows Server VM using [the Azure portal](quick-create-portal.md) or [Azure PowerShell](quick-create-powershell.md).</span></span>
* <span data-ttu-id="9ad8f-111">Подключите диск данных к виртуальной машине Windows Server на [портале Azure](attach-managed-disk-portal.md) или с помощью [PowerShell](attach-disk-ps.md).</span><span class="sxs-lookup"><span data-stu-id="9ad8f-111">Attach a data disk to a Windows Server VM using [the Azure portal](attach-managed-disk-portal.md) or [Azure PowerShell](attach-disk-ps.md).</span></span>

<span data-ttu-id="9ad8f-112">Чтобы начать установку и настройку MongoDB, [выполните вход в виртуальную машину Windows Server](connect-logon.md) с помощью удаленного рабочего стола.</span><span class="sxs-lookup"><span data-stu-id="9ad8f-112">To begin installing and configuring MongoDB, [log on to your Windows Server VM](connect-logon.md) by using Remote Desktop.</span></span>

## <a name="install-mongodb"></a><span data-ttu-id="9ad8f-113">Установка MongoDB</span><span class="sxs-lookup"><span data-stu-id="9ad8f-113">Install MongoDB</span></span>
> [!IMPORTANT]
> <span data-ttu-id="9ad8f-114">Функции безопасности MongoDB, такие как проверка подлинности и привязка IP-адреса, не включены по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="9ad8f-114">MongoDB security features, such as authentication and IP address binding, are not enabled by default.</span></span> <span data-ttu-id="9ad8f-115">Функции безопасности необходимо включить перед развертыванием MongoDB в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="9ad8f-115">Security features should be enabled before deploying MongoDB to a production environment.</span></span> <span data-ttu-id="9ad8f-116">Чтобы узнать больше, ознакомьтесь с [системой безопасности и аутентификацией MongoDB](http://www.mongodb.org/display/DOCS/Security+and+Authentication).</span><span class="sxs-lookup"><span data-stu-id="9ad8f-116">For more information, see [MongoDB Security and Authentication](http://www.mongodb.org/display/DOCS/Security+and+Authentication).</span></span>


1. <span data-ttu-id="9ad8f-117">После подключения к виртуальной машине с помощью удаленного рабочего стола откройте Internet Explorer из меню **Пуск** этой виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="9ad8f-117">After you've connected to your VM using Remote Desktop, open Internet Explorer from the **Start** menu on the VM.</span></span>
2. <span data-ttu-id="9ad8f-118">При первом запуске Internet Explorer выберите **Использовать рекомендуемые параметры безопасности, конфиденциальности и совместимости** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="9ad8f-118">Select **Use recommended security, privacy, and compatibility settings** when Internet Explorer first opens, and click **OK**.</span></span>
3. <span data-ttu-id="9ad8f-119">Конфигурация усиленной безопасности Internet Explorer включена по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="9ad8f-119">Internet Explorer enhanced security configuration is enabled by default.</span></span> <span data-ttu-id="9ad8f-120">Добавьте веб-сайт MongoDB в список разрешенных сайтов.</span><span class="sxs-lookup"><span data-stu-id="9ad8f-120">Add the MongoDB website to the list of allowed sites:</span></span>
   
   * <span data-ttu-id="9ad8f-121">Щелкните значок **Сервис** в правом верхнем углу.</span><span class="sxs-lookup"><span data-stu-id="9ad8f-121">Select the **Tools** icon in the upper-right corner.</span></span>
   * <span data-ttu-id="9ad8f-122">В окне **Свойства браузера** выберите вкладку **Безопасность** и щелкните значок **Надежные сайты**.</span><span class="sxs-lookup"><span data-stu-id="9ad8f-122">In **Internet Options**, select the **Security** tab, and then select the **Trusted Sites** icon.</span></span>
   * <span data-ttu-id="9ad8f-123">Нажмите кнопку **Сайты**.</span><span class="sxs-lookup"><span data-stu-id="9ad8f-123">Click the **Sites** button.</span></span> <span data-ttu-id="9ad8f-124">Добавьте *http://\*.mongodb.org* в список надежных сайтов и закройте диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="9ad8f-124">Add *https://\*.mongodb.org* to the list of trusted sites, and then close the dialog box.</span></span>
     
     ![Настройка параметров безопасности Internet Explorer](./media/install-mongodb/configure-internet-explorer-security.png)
4. <span data-ttu-id="9ad8f-126">Перейдите на страницу [MongoDB - Downloads](http://www.mongodb.org/downloads) (Центр загрузки MongoDB) (http://www.mongodb.org/downloads).</span><span class="sxs-lookup"><span data-stu-id="9ad8f-126">Browse to the [MongoDB - Downloads](http://www.mongodb.org/downloads) page (http://www.mongodb.org/downloads).</span></span>
5. <span data-ttu-id="9ad8f-127">При необходимости выберите выпуск **Community Server** и последний стабильный выпуск 64-разрядной версии Windows Server 2008 R2 и более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="9ad8f-127">If needed, select the **Community Server** edition and then select the latest current stable release for Windows Server 2008 R2 64-bit and later.</span></span> <span data-ttu-id="9ad8f-128">Чтобы скачать установщик, щелкните **DOWNLOAD (msi)** (Скачать (MSI-файл)).</span><span class="sxs-lookup"><span data-stu-id="9ad8f-128">To download the installer, click **DOWNLOAD (msi)**.</span></span>
   
    ![Скачивание установщика MongoDB](./media/install-mongodb/download-mongodb.png)
   
    <span data-ttu-id="9ad8f-130">После завершения скачивания запустите установщик.</span><span class="sxs-lookup"><span data-stu-id="9ad8f-130">Run the installer after the download is complete.</span></span>
6. <span data-ttu-id="9ad8f-131">Прочитайте и примите условия лицензионного соглашения.</span><span class="sxs-lookup"><span data-stu-id="9ad8f-131">Read and accept the license agreement.</span></span> <span data-ttu-id="9ad8f-132">Когда появится запрос, выберите **Complete** (Завершить).</span><span class="sxs-lookup"><span data-stu-id="9ad8f-132">When you're prompted, select **Complete** install.</span></span>
7. <span data-ttu-id="9ad8f-133">На последнем экране щелкните **Install** (Установить).</span><span class="sxs-lookup"><span data-stu-id="9ad8f-133">On the final screen, click **Install**.</span></span>

## <a name="configure-the-vm-and-mongodb"></a><span data-ttu-id="9ad8f-134">Настройка виртуальной машины и MongoDB</span><span class="sxs-lookup"><span data-stu-id="9ad8f-134">Configure the VM and MongoDB</span></span>
1. <span data-ttu-id="9ad8f-135">Установщик MongoDB не обновляет переменные пути.</span><span class="sxs-lookup"><span data-stu-id="9ad8f-135">The path variables are not updated by the MongoDB installer.</span></span> <span data-ttu-id="9ad8f-136">Если расположение MongoDB `bin` не указано в переменной пути, необходимо указывать полный путь при каждом использовании исполняемого файла MongoDB.</span><span class="sxs-lookup"><span data-stu-id="9ad8f-136">Without the MongoDB `bin` location in your path variable, you need to specify the full path each time you use a MongoDB executable.</span></span> <span data-ttu-id="9ad8f-137">Вот как можно добавить расположение в переменную пути.</span><span class="sxs-lookup"><span data-stu-id="9ad8f-137">To add the location to your path variable:</span></span>
   
   * <span data-ttu-id="9ad8f-138">Щелкните правой кнопкой мыши меню **Пуск** и выберите пункт **Система**.</span><span class="sxs-lookup"><span data-stu-id="9ad8f-138">Right-click the **Start** menu, and select **System**.</span></span>
   * <span data-ttu-id="9ad8f-139">Выберите **Дополнительные параметры системы**, а затем щелкните **Переменные среды**.</span><span class="sxs-lookup"><span data-stu-id="9ad8f-139">Click **Advanced system settings**, and then click **Environment Variables**.</span></span>
   * <span data-ttu-id="9ad8f-140">В разделе **Системные переменные** выберите **Путь** и нажмите кнопку **Изменить**.</span><span class="sxs-lookup"><span data-stu-id="9ad8f-140">Under **System variables**, select **Path**, and then click **Edit**.</span></span>
     
     ![Настройка переменных PATH](./media/install-mongodb/configure-path-variables.png)
     
     <span data-ttu-id="9ad8f-142">Добавьте путь к папке MongoDB, `bin`.</span><span class="sxs-lookup"><span data-stu-id="9ad8f-142">Add the path to your MongoDB `bin` folder.</span></span> <span data-ttu-id="9ad8f-143">Приложение MongoDB обычно устанавливается в папку *C:\Program Files\MongoDB*.</span><span class="sxs-lookup"><span data-stu-id="9ad8f-143">MongoDB is typically installed in *C:\Program Files\MongoDB*.</span></span> <span data-ttu-id="9ad8f-144">Проверьте путь установки на виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="9ad8f-144">Verify the installation path on your VM.</span></span> <span data-ttu-id="9ad8f-145">В следующем примере в переменную `PATH` добавляется расположение по умолчанию для установки MongoDB.</span><span class="sxs-lookup"><span data-stu-id="9ad8f-145">The following example adds the default MongoDB install location to the `PATH` variable:</span></span>
     
     ```
     ;C:\Program Files\MongoDB\Server\3.2\bin
     ```
     
     > [!NOTE]
     > <span data-ttu-id="9ad8f-146">Обязательно добавьте начальную точку с запятой (`;`), чтобы указать, что добавляется расположение в переменную `PATH`.</span><span class="sxs-lookup"><span data-stu-id="9ad8f-146">Be sure to add the leading semicolon (`;`) to indicate that you are adding a location to your `PATH` variable.</span></span>

2. <span data-ttu-id="9ad8f-147">Создайте каталоги данных и журналов MongoDB на диске данных.</span><span class="sxs-lookup"><span data-stu-id="9ad8f-147">Create MongoDB data and log directories on your data disk.</span></span> <span data-ttu-id="9ad8f-148">В меню **Пуск** выберите **Командная строка**.</span><span class="sxs-lookup"><span data-stu-id="9ad8f-148">From the **Start** menu, select **Command Prompt**.</span></span> <span data-ttu-id="9ad8f-149">В следующих примерах создаются каталоги на диске F.</span><span class="sxs-lookup"><span data-stu-id="9ad8f-149">The following examples create the directories on drive F:</span></span>
   
    ```
    mkdir F:\MongoData
    mkdir F:\MongoLogs
    ```
3. <span data-ttu-id="9ad8f-150">Запустите экземпляр MongoDB с помощью приведенной команды, соответствующим образом изменив путь к каталогам данных и журналов.</span><span class="sxs-lookup"><span data-stu-id="9ad8f-150">Start a MongoDB instance with the following command, adjusting the path to your data and log directories accordingly:</span></span>
   
    ```
    mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log
    ```
   
    <span data-ttu-id="9ad8f-151">Может пройти несколько минут, пока MongoDB выделит место для файлов журналов и начнет ожидать передачи данных.</span><span class="sxs-lookup"><span data-stu-id="9ad8f-151">It may take several minutes for MongoDB to allocate the journal files and start listening for connections.</span></span> <span data-ttu-id="9ad8f-152">Все сообщения журнала будут направляться в файл *F:\MongoLogs\mongolog.log*, когда сервер `mongod.exe` запустится и выделит место для файлов журналов.</span><span class="sxs-lookup"><span data-stu-id="9ad8f-152">All log messages are directed to the *F:\MongoLogs\mongolog.log* file as `mongod.exe` server starts and allocates journal files.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="9ad8f-153">Фокус командной строки будет оставаться на этой задаче, пока выполняется экземпляр MongoDB.</span><span class="sxs-lookup"><span data-stu-id="9ad8f-153">The command prompt stays focused on this task while your MongoDB instance is running.</span></span> <span data-ttu-id="9ad8f-154">Не закрывайте окно командной строки, чтобы не прерывать выполнение MongoDB.</span><span class="sxs-lookup"><span data-stu-id="9ad8f-154">Leave the command prompt window open to continue running MongoDB.</span></span> <span data-ttu-id="9ad8f-155">Или установите MongoDB в качестве службы, как описано на следующем шаге.</span><span class="sxs-lookup"><span data-stu-id="9ad8f-155">Or, install MongoDB as service, as detailed in the next step.</span></span>

4. <span data-ttu-id="9ad8f-156">Для более надежной работы MongoDB установите `mongod.exe` как службу.</span><span class="sxs-lookup"><span data-stu-id="9ad8f-156">For a more robust MongoDB experience, install the `mongod.exe` as a service.</span></span> <span data-ttu-id="9ad8f-157">Создание службы означает, что вам не нужно будет оставлять окно командной строки открытым каждый раз, когда необходимо использовать MongoDB.</span><span class="sxs-lookup"><span data-stu-id="9ad8f-157">Creating a service means you don't need to leave a command prompt running each time you want to use MongoDB.</span></span> <span data-ttu-id="9ad8f-158">Создайте службу, как описано ниже, указав пути к своим каталогам данных и журналов, соответственно.</span><span class="sxs-lookup"><span data-stu-id="9ad8f-158">Create the service as follows, adjusting the path to your data and log directories accordingly:</span></span>
   
    ```
    mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log `
        --logappend  --install
    ```
   
    <span data-ttu-id="9ad8f-159">Приведенная выше команда создает службу MongoDB с описанием "Mongo DB".</span><span class="sxs-lookup"><span data-stu-id="9ad8f-159">The preceding command creates a service named MongoDB, with a description of "Mongo DB".</span></span> <span data-ttu-id="9ad8f-160">Кроме того, указаны следующие параметры.</span><span class="sxs-lookup"><span data-stu-id="9ad8f-160">The following parameters are also specified:</span></span>
   
   * <span data-ttu-id="9ad8f-161">Параметр `--dbpath` указывает расположение каталога данных.</span><span class="sxs-lookup"><span data-stu-id="9ad8f-161">The `--dbpath` option specifies the location of the data directory.</span></span>
   * <span data-ttu-id="9ad8f-162">Необходимо указать файл журнала с помощью параметра `--logpath`, так как у работающей службы нет командного окна для вывода данных.</span><span class="sxs-lookup"><span data-stu-id="9ad8f-162">The `--logpath` option must be used to specify a log file, because the running service does not have a command window to display output.</span></span>
   * <span data-ttu-id="9ad8f-163">Параметр `--logappend` указывает, что после перезапуска службы выходные данные будут добавляться в имеющийся файл журнала.</span><span class="sxs-lookup"><span data-stu-id="9ad8f-163">The `--logappend` option specifies that a restart of the service causes output to append to the existing log file.</span></span>
   
   <span data-ttu-id="9ad8f-164">Выполните следующую команду, чтобы запустить службу MongoDB.</span><span class="sxs-lookup"><span data-stu-id="9ad8f-164">To start the MongoDB service, run the following command:</span></span>
   
    ```
    net start MongoDB
    ```
   
    <span data-ttu-id="9ad8f-165">Чтобы больше узнать о создании службы MongoDB, ознакомьтесь с [настройкой службы Windows для MongoDB](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-windows/#mongodb-as-a-windows-service).</span><span class="sxs-lookup"><span data-stu-id="9ad8f-165">For more information about creating the MongoDB service, see [Configure a Windows Service for MongoDB](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-windows/#mongodb-as-a-windows-service).</span></span>

## <a name="test-the-mongodb-instance"></a><span data-ttu-id="9ad8f-166">Тестирование экземпляра MongoDB</span><span class="sxs-lookup"><span data-stu-id="9ad8f-166">Test the MongoDB instance</span></span>
<span data-ttu-id="9ad8f-167">Теперь, когда компонент MongoDB выполняется как один экземпляр или установлен в качестве службы, можно приступить к созданию и использованию баз данных.</span><span class="sxs-lookup"><span data-stu-id="9ad8f-167">With MongoDB running as a single instance or installed as a service, you can now start creating and using your databases.</span></span> <span data-ttu-id="9ad8f-168">Чтобы запустить оболочку администрирования MongoDB, откройте еще одно окно командной строки из меню **Пуск** и введите приведенную ниже команду.</span><span class="sxs-lookup"><span data-stu-id="9ad8f-168">To start the MongoDB administrative shell, open another command prompt window from the **Start** menu, and enter the following command:</span></span>

```
mongo  
```

<span data-ttu-id="9ad8f-169">Вы можете вывести список баз данных с помощью команды `db`.</span><span class="sxs-lookup"><span data-stu-id="9ad8f-169">You can list the databases with the `db` command.</span></span> <span data-ttu-id="9ad8f-170">Вставьте некоторые данные следующим образом.</span><span class="sxs-lookup"><span data-stu-id="9ad8f-170">Insert some data as follows:</span></span>

```
db.foo.insert( { a : 1 } )
```

<span data-ttu-id="9ad8f-171">Выполните поиск данных следующим образом.</span><span class="sxs-lookup"><span data-stu-id="9ad8f-171">Search for data as follows:</span></span>

```
db.foo.find()
```

<span data-ttu-id="9ad8f-172">Вы должны увидеть результат, аналогичный приведенному ниже.</span><span class="sxs-lookup"><span data-stu-id="9ad8f-172">The output is similar to the following example:</span></span>

```
{ "_id" : "ObjectId("57f6a86cee873a6232d74842"), "a" : 1 }
```

<span data-ttu-id="9ad8f-173">Завершите работу консоли `mongo` следующим образом.</span><span class="sxs-lookup"><span data-stu-id="9ad8f-173">Exit the `mongo` console as follows:</span></span>

```
exit
```

## <a name="configure-firewall-and-network-security-group-rules"></a><span data-ttu-id="9ad8f-174">Настройка брандмауэра и правил группы безопасности сети</span><span class="sxs-lookup"><span data-stu-id="9ad8f-174">Configure firewall and Network Security Group rules</span></span>
<span data-ttu-id="9ad8f-175">После установки и запуска MongoDB следует открыть порт в брандмауэре Windows для удаленного подключения к MongoDB.</span><span class="sxs-lookup"><span data-stu-id="9ad8f-175">Now that MongoDB is installed and running, open a port in Windows Firewall so you can remotely connect to MongoDB.</span></span> <span data-ttu-id="9ad8f-176">Чтобы создать правило входящего трафика, разрешающее передачу данных через TCP-порт 27017, откройте командную строку PowerShell для администрирования и введите следующую команду.</span><span class="sxs-lookup"><span data-stu-id="9ad8f-176">To create a new inbound rule to allow TCP port 27017, open an administrative PowerShell prompt and enter the following command:</span></span>

```powerahell
New-NetFirewallRule `
    -DisplayName "Allow MongoDB" `
    -Direction Inbound `
    -Protocol TCP `
    -LocalPort 27017 `
    -Action Allow
```

<span data-ttu-id="9ad8f-177">Можно также создать правило с помощью графического средства управления **Брандмауэр Windows в режиме повышенной безопасности**.</span><span class="sxs-lookup"><span data-stu-id="9ad8f-177">You can also create the rule by using the **Windows Firewall with Advanced Security** graphical management tool.</span></span> <span data-ttu-id="9ad8f-178">Создайте правило входящего трафика, чтобы разрешить использовать TCP-порт 27017.</span><span class="sxs-lookup"><span data-stu-id="9ad8f-178">Create a new inbound rule to allow TCP port 27017.</span></span>

<span data-ttu-id="9ad8f-179">При необходимости создайте правило группы безопасности сети, чтобы разрешить доступ к MongoDB извне подсети в существующей виртуальной сети Azure.</span><span class="sxs-lookup"><span data-stu-id="9ad8f-179">If needed, create a Network Security Group rule to allow access to MongoDB from outside of the existing Azure virtual network subnet.</span></span> <span data-ttu-id="9ad8f-180">Правила группы безопасности сети можно создать с помощью [портала Azure](nsg-quickstart-portal.md) или [Azure PowerShell](nsg-quickstart-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="9ad8f-180">You can create the Network Security Group rules by using the [Azure portal](nsg-quickstart-portal.md) or [Azure PowerShell](nsg-quickstart-powershell.md).</span></span> <span data-ttu-id="9ad8f-181">Как и в правилах брандмауэра Windows, разрешите использование TCP-порта 27017 для виртуального сетевого интерфейса виртуальной машины MongoDB.</span><span class="sxs-lookup"><span data-stu-id="9ad8f-181">As with the Windows Firewall rules, allow TCP port 27017 to the virtual network interface of your MongoDB VM.</span></span>

> [!NOTE]
> <span data-ttu-id="9ad8f-182">MongoDB использует TCP-порт 27017 по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="9ad8f-182">TCP port 27017 is the default port used by MongoDB.</span></span> <span data-ttu-id="9ad8f-183">Этот порт можно изменить с помощью параметра `--port` при запуске `mongod.exe` вручную или из службы.</span><span class="sxs-lookup"><span data-stu-id="9ad8f-183">You can change this port by using the `--port` parameter when starting `mongod.exe` manually or from a service.</span></span> <span data-ttu-id="9ad8f-184">Если вы изменяете порт, не забудьте обновить правила брандмауэра Windows и группы безопасности сети, созданные на предыдущих шагах.</span><span class="sxs-lookup"><span data-stu-id="9ad8f-184">If you change the port, make sure to update the Windows Firewall and Network Security Group rules in the preceding steps.</span></span>


## <a name="next-steps"></a><span data-ttu-id="9ad8f-185">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9ad8f-185">Next steps</span></span>
<span data-ttu-id="9ad8f-186">Из этого руководства вы узнали, как установить и настроить MongoDB на виртуальной машине Windows.</span><span class="sxs-lookup"><span data-stu-id="9ad8f-186">In this tutorial, you learned how to install and configure MongoDB on your Windows VM.</span></span> <span data-ttu-id="9ad8f-187">Теперь вы можете получить доступ к MongoDB на виртуальной машине Windows, выполнив действия, описанные в дополнительных разделах [документации по MongoDB](https://docs.mongodb.com/manual/).</span><span class="sxs-lookup"><span data-stu-id="9ad8f-187">You can now access MongoDB on your Windows VM, by following the advanced topics in the [MongoDB documentation](https://docs.mongodb.com/manual/).</span></span>

