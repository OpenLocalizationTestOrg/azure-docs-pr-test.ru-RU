---
title: "Разработка с помощью эмулятора Cosmos DB в локальной среде | Документация Майкрософт"
description: "С помощью эмулятора Azure Cosmos DB вы можете бесплатно разрабатывать и тестировать приложения локально. Для этого вам не нужно создавать подписку Azure."
services: cosmos-db
documentationcenter: 
keywords: "Эмулятор Azure Cosmos DB"
author: arramac
manager: jhubbard
editor: 
ms.assetid: 90b379a6-426b-4915-9635-822f1a138656
ms.service: cosmos-db
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: arramac
ms.openlocfilehash: a0f6a845a345ebd4ef0a58abf4934ce400103109
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="use-the-azure-cosmos-db-emulator-for-local-development-and-testing"></a><span data-ttu-id="047d5-104">Использование эмулятора Azure Cosmos DB для разработки и тестирования в локальной среде</span><span class="sxs-lookup"><span data-stu-id="047d5-104">Use the Azure Cosmos DB Emulator for local development and testing</span></span>

<table>
<tr>
  <td><span data-ttu-id="047d5-105"><strong>Двоичные файлы</strong></span><span class="sxs-lookup"><span data-stu-id="047d5-105"><strong>Binaries</strong></span></span></td>
  <td>[<span data-ttu-id="047d5-106">Скачивание MSI</span><span class="sxs-lookup"><span data-stu-id="047d5-106">Download MSI</span></span>](https://aka.ms/cosmosdb-emulator)</td>
</tr>
<tr>
  <td><span data-ttu-id="047d5-107"><strong>Docker</strong></span><span class="sxs-lookup"><span data-stu-id="047d5-107"><strong>Docker</strong></span></span></td>
  <td>[<span data-ttu-id="047d5-108">Концентратор Docker</span><span class="sxs-lookup"><span data-stu-id="047d5-108">Docker Hub</span></span>](https://hub.docker.com/r/microsoft/azure-documentdb-emulator/)</td>
</tr>
<tr>
  <td><span data-ttu-id="047d5-109"><strong>Источник Docker</strong></span><span class="sxs-lookup"><span data-stu-id="047d5-109"><strong>Docker source</strong></span></span></td>
  <td>[<span data-ttu-id="047d5-110">Github</span><span class="sxs-lookup"><span data-stu-id="047d5-110">Github</span></span>](https://github.com/azure/azure-documentdb-emulator-docker)</td>
</tr>
</table>
  
<span data-ttu-id="047d5-111">Эмулятор Azure Cosmos DB предоставляет локальную среду для разработки, которая эмулирует службу Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="047d5-111">The Azure Cosmos DB Emulator provides a local environment that emulates the Azure Cosmos DB service for development purposes.</span></span> <span data-ttu-id="047d5-112">С помощью эмулятора Azure Cosmos DB вы можете локально разрабатывать и тестировать приложения, не создавая подписку Azure и не тратя средства.</span><span class="sxs-lookup"><span data-stu-id="047d5-112">Using the Azure Cosmos DB Emulator, you can develop and test your application locally, without creating an Azure subscription or incurring any costs.</span></span> <span data-ttu-id="047d5-113">Если приложение в эмуляторе Azure Cosmos DB работает правильно, вы можете использовать учетную запись Azure Cosmos DB в облаке.</span><span class="sxs-lookup"><span data-stu-id="047d5-113">When you're satisfied with how your application is working in the Azure Cosmos DB Emulator, you can switch to using an Azure Cosmos DB account in the cloud.</span></span>

<span data-ttu-id="047d5-114">В этой статье рассматриваются следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="047d5-114">This article covers the following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="047d5-115">Установка эмулятора</span><span class="sxs-lookup"><span data-stu-id="047d5-115">Installing the Emulator</span></span>
> * <span data-ttu-id="047d5-116">Запуск эмулятора в Docker для Windows</span><span class="sxs-lookup"><span data-stu-id="047d5-116">Running the Emulator on Docker for Windows</span></span>
> * <span data-ttu-id="047d5-117">Выполнение проверки подлинности запросов</span><span class="sxs-lookup"><span data-stu-id="047d5-117">Authenticating requests</span></span>
> * <span data-ttu-id="047d5-118">Использование обозревателя данных в эмуляторе</span><span class="sxs-lookup"><span data-stu-id="047d5-118">Using the Data Explorer in the Emulator</span></span>
> * <span data-ttu-id="047d5-119">Экспорт сертификатов SSL</span><span class="sxs-lookup"><span data-stu-id="047d5-119">Exporting SSL certificates</span></span>
> * <span data-ttu-id="047d5-120">Вызов эмулятора из командной строки</span><span class="sxs-lookup"><span data-stu-id="047d5-120">Calling the Emulator from the command line</span></span>
> * <span data-ttu-id="047d5-121">Сбор файлов трассировки</span><span class="sxs-lookup"><span data-stu-id="047d5-121">Collecting trace files</span></span>

<span data-ttu-id="047d5-122">Рекомендуем просмотреть следующий видеоролик, в котором Кирилл Гаврилюк покажет, как начать работу с эмулятором Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="047d5-122">We recommend getting started by watching the following video, where Kirill Gavrylyuk shows how to get started with the Azure Cosmos DB Emulator.</span></span> <span data-ttu-id="047d5-123">Обратите внимание, что в видео эмулятор называется эмулятором DocumentDB, но с момента съемки видео сам инструмент переименован в эмулятор Azure Cosmos DB с момента записи видео.</span><span class="sxs-lookup"><span data-stu-id="047d5-123">Note that the video refers to the emulator as the DocumentDB Emulator, but the tool itself has been renamed the Azure Cosmos DB Emulator since taping the video.</span></span> <span data-ttu-id="047d5-124">Все данные в видео актуальны для эмулятора Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="047d5-124">All information in the video is still accurate for the Azure Cosmos DB Emulator.</span></span> 

> [!VIDEO https://channel9.msdn.com/Events/Connect/2016/192/player]
> 
> 

## <a name="how-the-emulator-works"></a><span data-ttu-id="047d5-125">Принцип работы эмулятора</span><span class="sxs-lookup"><span data-stu-id="047d5-125">How the Emulator works</span></span>
<span data-ttu-id="047d5-126">Эмулятор Azure Cosmos DB обеспечивает высокоточную эмуляцию службы Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="047d5-126">The Azure Cosmos DB Emulator provides a high-fidelity emulation of the Azure Cosmos DB service.</span></span> <span data-ttu-id="047d5-127">В эмуляторе реализованы те же функции, что и в службе Azure Cosmos DB, включая поддержку создания документов JSON и выполнение запросов к ним, подготовку и масштабирование коллекций, а также выполнение хранимых процедур и триггеров.</span><span class="sxs-lookup"><span data-stu-id="047d5-127">It supports identical functionality as Azure Cosmos DB, including support for creating and querying JSON documents, provisioning and scaling collections, and executing stored procedures and triggers.</span></span> <span data-ttu-id="047d5-128">С помощью эмулятора Azure Cosmos DB можно разрабатывать и тестировать приложения. Чтобы развернуть эти приложения в глобальной среде Azure, нужно изменить всего один параметр конфигурации для конечной точки подключения к Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="047d5-128">You can develop and test applications using the Azure Cosmos DB Emulator, and deploy them to Azure at global scale by just making a single configuration change to the connection endpoint for Azure Cosmos DB.</span></span>

<span data-ttu-id="047d5-129">Хотя мы и создали высокоточную локальную эмуляцию настоящей службы Azure Cosmos DB, реализация эмулятора Azure Cosmos DB несколько отличается.</span><span class="sxs-lookup"><span data-stu-id="047d5-129">While we created a high-fidelity local emulation of the actual Azure Cosmos DB service, the implementation of the Azure Cosmos DB Emulator is different than that of the service.</span></span> <span data-ttu-id="047d5-130">Например, эмулятор Azure Cosmos DB использует стандартные компоненты ОС: локальную файловую систему для сохранения данных и стек протокола HTTPS для подключений.</span><span class="sxs-lookup"><span data-stu-id="047d5-130">For example, the Azure Cosmos DB Emulator uses standard OS components such as the local file system for persistence, and HTTPS protocol stack for connectivity.</span></span> <span data-ttu-id="047d5-131">Это означает, что некоторые возможности инфраструктуры Azure будут не доступны в эмуляторе Azure Cosmos DB, включая глобальную репликацию, задержку менее 10 миллисекунд для операций чтения и записи или настраиваемые уровни согласованности.</span><span class="sxs-lookup"><span data-stu-id="047d5-131">This means that some functionality that relies on Azure infrastructure like global replication, single-digit millisecond latency for reads/writes, and tunable consistency levels are not available via the Azure Cosmos DB Emulator.</span></span>

> [!NOTE]
> <span data-ttu-id="047d5-132">Сейчас обозреватель данных в эмуляторе поддерживает создание коллекций API DocumentDB и MongoDB.</span><span class="sxs-lookup"><span data-stu-id="047d5-132">At this time the Data Explorer in the emulator only supports the creation of DocumentDB API collections and MongoDB collections.</span></span> <span data-ttu-id="047d5-133">Сейчас обозреватель данных в эмуляторе не поддерживает создание таблиц и графов.</span><span class="sxs-lookup"><span data-stu-id="047d5-133">The Data Explorer in the emulator does not currently support the creation of tables and graphs.</span></span> 

## <a name="system-requirements"></a><span data-ttu-id="047d5-134">Требования к системе</span><span class="sxs-lookup"><span data-stu-id="047d5-134">System requirements</span></span>
<span data-ttu-id="047d5-135">Эмулятор Azure Cosmos DB имеет следующие требования к оборудованию и программному обеспечению.</span><span class="sxs-lookup"><span data-stu-id="047d5-135">The Azure Cosmos DB Emulator has the following hardware and software requirements:</span></span>

* <span data-ttu-id="047d5-136">Требования к программному обеспечению</span><span class="sxs-lookup"><span data-stu-id="047d5-136">Software requirements</span></span>
  * <span data-ttu-id="047d5-137">Windows Server 2012 R2, Windows Server 2016 или Windows 10.</span><span class="sxs-lookup"><span data-stu-id="047d5-137">Windows Server 2012 R2, Windows Server 2016, or Windows 10</span></span>
*   <span data-ttu-id="047d5-138">Минимальные требования к оборудованию</span><span class="sxs-lookup"><span data-stu-id="047d5-138">Minimum Hardware requirements</span></span>
  * <span data-ttu-id="047d5-139">ОЗУ 2 ГБ.</span><span class="sxs-lookup"><span data-stu-id="047d5-139">2 GB RAM</span></span>
  * <span data-ttu-id="047d5-140">10 ГБ свободного дискового пространства.</span><span class="sxs-lookup"><span data-stu-id="047d5-140">10 GB available hard disk space</span></span>

## <a name="installation"></a><span data-ttu-id="047d5-141">Установка</span><span class="sxs-lookup"><span data-stu-id="047d5-141">Installation</span></span>
<span data-ttu-id="047d5-142">Эмулятор Azure Cosmos DB можно скачать и установить из [центра загрузки Майкрософт](https://aka.ms/cosmosdb-emulator).</span><span class="sxs-lookup"><span data-stu-id="047d5-142">You can download and install the Azure Cosmos DB Emulator from the [Microsoft Download Center](https://aka.ms/cosmosdb-emulator).</span></span> 

> [!NOTE]
> <span data-ttu-id="047d5-143">Чтобы установить, настроить и запустить эмулятор Azure Cosmos DB, нужны права администратора на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="047d5-143">To install, configure, and run the Azure Cosmos DB Emulator, you must have administrative privileges on the computer.</span></span>

## <a name="running-on-docker-for-windows"></a><span data-ttu-id="047d5-144">Выполнение в Docker для Windows</span><span class="sxs-lookup"><span data-stu-id="047d5-144">Running on Docker for Windows</span></span>

<span data-ttu-id="047d5-145">Эмулятор Azure Cosmos DB может выполняться в Docker для Windows.</span><span class="sxs-lookup"><span data-stu-id="047d5-145">The Azure Cosmos DB Emulator can be run on Docker for Windows.</span></span> <span data-ttu-id="047d5-146">Этот эмулятор не работает в Docker для Oracle Linux.</span><span class="sxs-lookup"><span data-stu-id="047d5-146">The Emulator does not work on Docker for Oracle Linux.</span></span>

<span data-ttu-id="047d5-147">Если установлен [Docker для Windows](https://www.docker.com/docker-windows), вы можете извлечь образ эмулятора из Docker Hub, выполнив следующую команду из любой оболочки по своему усмотрению (cmd.exe, PowerShell и т. д.).</span><span class="sxs-lookup"><span data-stu-id="047d5-147">Once you have [Docker for Windows](https://www.docker.com/docker-windows) installed, you can pull the Emulator image from Docker Hub by running the following command from your favorite shell (cmd.exe, PowerShell, etc.).</span></span>

```      
docker pull microsoft/azure-cosmosdb-emulator 
```
<span data-ttu-id="047d5-148">Чтобы запустить образ, выполните следующие команды:</span><span class="sxs-lookup"><span data-stu-id="047d5-148">To start the image, run the following commands.</span></span>

``` 
md %LOCALAPPDATA%\CosmosDBEmulatorCert 2>nul
docker run -v %LOCALAPPDATA%\CosmosDBEmulatorCert:c:\CosmosDBEmulator\CosmosDBEmulatorCert -P -t -i microsoft/azure-cosmosdb-emulator 
```

<span data-ttu-id="047d5-149">Ответ выглядит примерно так:</span><span class="sxs-lookup"><span data-stu-id="047d5-149">The response looks similar to the following:</span></span>

```
Starting Emulator
Emulator Endpoint: https://172.20.229.193:8081/
Master Key: C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==
Exporting SSL Certificate
You can import the SSL certificate from an administrator command prompt on the host by running:
cd /d %LOCALAPPDATA%\CosmosDBEmulatorCert
powershell .\importcert.ps1
--------------------------------------------------------------------------------------------------
Starting interactive shell
``` 

<span data-ttu-id="047d5-150">Если закрыть интерактивную оболочку после запуска эмулятора, его контейнер завершит работу.</span><span class="sxs-lookup"><span data-stu-id="047d5-150">Closing the interactive shell once the Emulator has been started will shutdown the Emulator’s container.</span></span>

<span data-ttu-id="047d5-151">Воспользуйтесь конечной точкой и главным ключом из ответа в клиенте и импортируйте SSL-сертификат в узел.</span><span class="sxs-lookup"><span data-stu-id="047d5-151">Use the endpoint and master key in from the response in your client and import the SSL certificate into your host.</span></span> <span data-ttu-id="047d5-152">Чтобы импортировать SSL-сертификат, выполните следующие действия из командной строки с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="047d5-152">To import the SSL certificate, do the following from an admin command prompt:</span></span>

```
cd %LOCALAPPDATA%\CosmosDBEmulatorCert
powershell .\importcert.ps1
```


## <a name="start-the-emulator"></a><span data-ttu-id="047d5-153">Запуск эмулятора</span><span class="sxs-lookup"><span data-stu-id="047d5-153">Start the Emulator</span></span>

<span data-ttu-id="047d5-154">Чтобы запустить эмулятор Azure Cosmos DB, нажмите кнопку "Пуск" или клавишу Windows.</span><span class="sxs-lookup"><span data-stu-id="047d5-154">To start the Azure Cosmos DB Emulator, select the Start button or press the Windows key.</span></span> <span data-ttu-id="047d5-155">Начните вводить текст **Эмулятор Azure Cosmos DB** и выберите эмулятор в списке приложений.</span><span class="sxs-lookup"><span data-stu-id="047d5-155">Begin typing **Azure Cosmos DB Emulator**, and select the emulator from the list of applications.</span></span> 

![Нажмите кнопку "Пуск" или клавишу Windows, начните вводить **Эмулятор Azure Cosmos DB**, а затем выберите эмулятор в списке приложений](./media/local-emulator/database-local-emulator-start.png)

<span data-ttu-id="047d5-157">При запуске эмулятора в области уведомлений панели задач Windows появится соответствующий значок.</span><span class="sxs-lookup"><span data-stu-id="047d5-157">When the emulator is running, you'll see an icon in the Windows taskbar notification area.</span></span> ![Уведомление локального эмулятора Azure Cosmos DB на панели задач](./media/local-emulator/database-local-emulator-taskbar.png)

<span data-ttu-id="047d5-159">Эмулятор Azure Cosmos DB по умолчанию выполняется на локальном компьютере (localhost) и прослушивает порт 8081.</span><span class="sxs-lookup"><span data-stu-id="047d5-159">The Azure Cosmos DB Emulator by default runs on the local machine ("localhost") listening on port 8081.</span></span>

<span data-ttu-id="047d5-160">Эмулятор Azure Cosmos DB по умолчанию устанавливается в каталог `C:\Program Files\Azure Cosmos DB Emulator`.</span><span class="sxs-lookup"><span data-stu-id="047d5-160">The Azure Cosmos DB Emulator is installed by default to the `C:\Program Files\Azure Cosmos DB Emulator` directory.</span></span> <span data-ttu-id="047d5-161">Можно также запустить и остановить эмулятор из командной строки.</span><span class="sxs-lookup"><span data-stu-id="047d5-161">You can also start and stop the emulator from the command-line.</span></span> <span data-ttu-id="047d5-162">Дополнительные сведения см. в [справочнике программы командной строки](#command-line).</span><span class="sxs-lookup"><span data-stu-id="047d5-162">See [command-line tool reference](#command-line) for more information.</span></span>

## <a name="start-data-explorer"></a><span data-ttu-id="047d5-163">Запуск обозревателя данных</span><span class="sxs-lookup"><span data-stu-id="047d5-163">Start Data Explorer</span></span>

<span data-ttu-id="047d5-164">При запуске эмулятор Azure Cosmos DB автоматически откроет в браузере страницу обозревателя данных Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="047d5-164">When the Azure Cosmos DB emulator launches it will automatically open the Azure Cosmos DB Data Explorer in your browser.</span></span> <span data-ttu-id="047d5-165">В адресной строке вы увидите адрес [https://localhost:8081/_explorer/index.html](https://localhost:8081/_explorer/index.html).</span><span class="sxs-lookup"><span data-stu-id="047d5-165">The address will appear as [https://localhost:8081/_explorer/index.html](https://localhost:8081/_explorer/index.html).</span></span> <span data-ttu-id="047d5-166">Чтобы позднее открыть страницу обозревателя данных, вы можете ввести в браузере этот URL-адрес или запустить обозреватель из эмулятора Azure Cosmos DB, используя значок в области уведомлений Windows, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="047d5-166">If you close the explorer and would like to re-open it later, you can either open the URL in your browser or launch it from the Azure Cosmos DB Emulator in the Windows Tray Icon as shown below.</span></span>

![Запуск обозревателя данных из локального эмулятора Azure Cosmos DB](./media/local-emulator/database-local-emulator-data-explorer-launcher.png)

## <a name="checking-for-updates"></a><span data-ttu-id="047d5-168">Проверка наличия обновлений</span><span class="sxs-lookup"><span data-stu-id="047d5-168">Checking for updates</span></span>
<span data-ttu-id="047d5-169">Обозреватель данных сообщает о наличии нового обновления, доступного для скачивания.</span><span class="sxs-lookup"><span data-stu-id="047d5-169">Data Explorer indicates if there is a new update available for download.</span></span> 

> [!NOTE]
> <span data-ttu-id="047d5-170">Данные, созданные в одной версии эмулятора Azure Cosmos DB, могут оказаться недоступными при использовании другой версии.</span><span class="sxs-lookup"><span data-stu-id="047d5-170">Data created in one version of the Azure Cosmos DB Emulator is not guaranteed to be accessible when using a different version.</span></span> <span data-ttu-id="047d5-171">Если нужно сохранить данные на длительный срок, мы рекомендуем хранить их в учетной записи хранения Azure Cosmos DB, а не эмуляторе Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="047d5-171">If you need to persist your data for the long term, it is recommended that you store that data in an Azure Cosmos DB account, rather than in the Azure Cosmos DB Emulator.</span></span> 

## <a name="authenticating-requests"></a><span data-ttu-id="047d5-172">Выполнение проверки подлинности запросов</span><span class="sxs-lookup"><span data-stu-id="047d5-172">Authenticating requests</span></span>
<span data-ttu-id="047d5-173">Как и в настоящей облачной службе Azure, в эмуляторе Azure Cosmos DB для каждого полученного запроса должна выполняться аутентификация.</span><span class="sxs-lookup"><span data-stu-id="047d5-173">Just as with Azure Cosmos DB in the cloud, every request that you make against the Azure Cosmos DB Emulator must be authenticated.</span></span> <span data-ttu-id="047d5-174">Эмулятор Azure Cosmos DB поддерживает аутентификацию с помощью главного ключа, используя одну предопределенную учетную запись и известный ключ аутентификации.</span><span class="sxs-lookup"><span data-stu-id="047d5-174">The Azure Cosmos DB Emulator supports a single fixed account and a well-known authentication key for master key authentication.</span></span> <span data-ttu-id="047d5-175">В качестве учетных данных для эмулятора Azure Cosmos DB можно использовать только эту учетную запись и только этот ключ.</span><span class="sxs-lookup"><span data-stu-id="047d5-175">This account and key are the only credentials permitted for use with the Azure Cosmos DB Emulator.</span></span> <span data-ttu-id="047d5-176">К ним относятся:</span><span class="sxs-lookup"><span data-stu-id="047d5-176">They are:</span></span>

    Account name: localhost:<port>
    Account key: C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==

> [!NOTE]
> <span data-ttu-id="047d5-177">Главный ключ, поддерживаемый эмулятором Azure Cosmos DB, предназначен для использования только с этим эмулятором.</span><span class="sxs-lookup"><span data-stu-id="047d5-177">The master key supported by the Azure Cosmos DB Emulator is intended for use only with the emulator.</span></span> <span data-ttu-id="047d5-178">Нельзя использовать рабочую учетную запись Azure Cosmos DB и ключ с эмулятором Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="047d5-178">You cannot use your production Azure Cosmos DB account and key with the Azure Cosmos DB Emulator.</span></span> 

> [!NOTE] 
> <span data-ttu-id="047d5-179">Если вы запустили эмулятор с параметром /Key, то используйте созданный ключ вместо "C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw=="</span><span class="sxs-lookup"><span data-stu-id="047d5-179">If you have started the emulator with the /Key option, then use the generated key instead of "C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw=="</span></span>

<span data-ttu-id="047d5-180">Кроме того, как и настоящая служба Azure Cosmos DB, эмулятор Azure Cosmos DB поддерживает только безопасное подключение по протоколу SSL.</span><span class="sxs-lookup"><span data-stu-id="047d5-180">Additionally, just as the Azure Cosmos DB service, the Azure Cosmos DB Emulator supports only secure communication via SSL.</span></span>

## <a name="running-the-emulator-on-a-local-network"></a><span data-ttu-id="047d5-181">Запуск эмулятора в локальной сети</span><span class="sxs-lookup"><span data-stu-id="047d5-181">Running the emulator on a local network</span></span>

<span data-ttu-id="047d5-182">Вы можете запустить эмулятор в локальной сети.</span><span class="sxs-lookup"><span data-stu-id="047d5-182">You can run the emulator on a local network.</span></span> <span data-ttu-id="047d5-183">Чтобы разрешить доступ к сети, укажите параметр /AllowNetworkAccess в [командной строке](#command-line-syntax), а также один из обязательных дополнительных параметров /Key=key_string или /KeyFile=file_name.</span><span class="sxs-lookup"><span data-stu-id="047d5-183">To enable network access, specify the /AllowNetworkAccess option at the [command line](#command-line-syntax), which also requires that you specify /Key=key_string or /KeyFile=file_name.</span></span> <span data-ttu-id="047d5-184">Можно также применить параметр GenKeyFile=file_name, чтобы заранее создать случайный ключ.</span><span class="sxs-lookup"><span data-stu-id="047d5-184">You can use /GenKeyFile=file_name to generate a file with a random key upfront.</span></span>  <span data-ttu-id="047d5-185">Затем передайте этот ключ в параметре /KeyFile=file_name или /Key=contents_of_file.</span><span class="sxs-lookup"><span data-stu-id="047d5-185">Then you can pass that to /KeyFile=file_name or /Key=contents_of_file.</span></span>

<span data-ttu-id="047d5-186">Чтобы в первый раз получить доступ к сети, пользователь должен завершить работу эмулятора и удалить каталог данных эмулятора (C:\Users\имя_пользователя\AppData\Local\CosmosDBEmulator).</span><span class="sxs-lookup"><span data-stu-id="047d5-186">To enable network access for the first time the user should shutdown the emulator and delete the emulator’s data directory (C:\Users\user_name\AppData\Local\CosmosDBEmulator).</span></span>

## <a name="developing-with-the-emulator"></a><span data-ttu-id="047d5-187">Разработка с помощью эмулятора</span><span class="sxs-lookup"><span data-stu-id="047d5-187">Developing with the Emulator</span></span>
<span data-ttu-id="047d5-188">Когда эмулятор Azure Cosmos DB будет запущен на рабочем столе, вы сможете работать с ним с помощью любых поддерживаемых [пакетов SDK для Azure Cosmos DB](documentdb-sdk-dotnet.md) или [REST API Azure Cosmos DB](/rest/api/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="047d5-188">Once you have the Azure Cosmos DB Emulator running on your desktop, you can use any supported [Azure Cosmos DB SDK](documentdb-sdk-dotnet.md) or the [Azure Cosmos DB REST API](/rest/api/documentdb/) to interact with the Emulator.</span></span> <span data-ttu-id="047d5-189">Эмулятор Azure Cosmos DB также содержит встроенный обозреватель данных, позволяющий создавать коллекции для API DocumentDB и MongoDB, а также просматривать и редактировать документы без написания кода.</span><span class="sxs-lookup"><span data-stu-id="047d5-189">The Azure Cosmos DB Emulator also includes a built-in Data Explorer that lets you create collections for the DocumentDB and MongoDB APIs, and view and edit documents without writing any code.</span></span>   

    // Connect to the Azure Cosmos DB Emulator running locally
    DocumentClient client = new DocumentClient(
        new Uri("https://localhost:8081"), 
        "C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==");

<span data-ttu-id="047d5-190">Если вы используете [поддержку протокола Azure Cosmos DB для MongoDB](mongodb-introduction.md), используйте следующую строку подключения:</span><span class="sxs-lookup"><span data-stu-id="047d5-190">If you're using [Azure Cosmos DB protocol support for MongoDB](mongodb-introduction.md), please use the following connection string:</span></span>

    mongodb://localhost:C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==@localhost:10255/admin?ssl=true&3t.sslSelfSignedCerts=true

<span data-ttu-id="047d5-191">Для подключения к эмулятору Azure Cosmos DB вы можете использовать имеющиеся инструменты, такие как [Azure DocumentDB Studio](https://github.com/mingaliu/DocumentDBStudio).</span><span class="sxs-lookup"><span data-stu-id="047d5-191">You can use existing tools like [Azure DocumentDB Studio](https://github.com/mingaliu/DocumentDBStudio) to connect to the Azure Cosmos DB Emulator.</span></span> <span data-ttu-id="047d5-192">Можно также переносить данные между эмулятором Azure Cosmos DB и службой Azure Cosmos DB с помощью [средства миграции данных Azure Cosmos DB](https://github.com/azure/azure-documentdb-datamigrationtool).</span><span class="sxs-lookup"><span data-stu-id="047d5-192">You can also migrate data between the Azure Cosmos DB Emulator and the Azure Cosmos DB service using the [Azure Cosmos DB Data Migration Tool](https://github.com/azure/azure-documentdb-datamigrationtool).</span></span>

> [!NOTE] 
> <span data-ttu-id="047d5-193">Если вы запустили эмулятор с параметром /Key, то используйте созданный ключ вместо "C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw=="</span><span class="sxs-lookup"><span data-stu-id="047d5-193">If you have started the emulator with the /Key option, then use the generated key instead of "C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw=="</span></span>

<span data-ttu-id="047d5-194">По умолчанию с помощью эмулятора Azure Cosmos DB можно создать до 25 односекционных коллекций или одну секционированную коллекцию.</span><span class="sxs-lookup"><span data-stu-id="047d5-194">Using the Azure Cosmos DB emulator, by default, you can create up to 25 single partition collections or 1 partitioned collection.</span></span> <span data-ttu-id="047d5-195">Дополнительные сведения об изменении этого значения см. в разделе [Изменение количества коллекций](#set-partitioncount).</span><span class="sxs-lookup"><span data-stu-id="047d5-195">For more information about changing this value, see [Setting the PartitionCount value](#set-partitioncount).</span></span>

## <a name="export-the-ssl-certificate"></a><span data-ttu-id="047d5-196">Экспорт SSL-сертификата</span><span class="sxs-lookup"><span data-stu-id="047d5-196">Export the SSL certificate</span></span>

<span data-ttu-id="047d5-197">Языки и среда выполнения .NET используют хранилище сертификатов Windows для безопасного подключения к локальному эмулятору Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="047d5-197">.NET languages and runtime use the Windows Certificate Store to securely connect to the Azure Cosmos DB local emulator.</span></span> <span data-ttu-id="047d5-198">Другие языки используют собственные методы для управления сертификатами и использования сертификатов.</span><span class="sxs-lookup"><span data-stu-id="047d5-198">Other languages have their own method of managing and using certificates.</span></span> <span data-ttu-id="047d5-199">Java поддерживает собственное [хранилище сертификатов](https://docs.oracle.com/cd/E19830-01/819-4712/ablqw/index.html), а Python применяет [оболочки сокетов](https://docs.python.org/2/library/ssl.html).</span><span class="sxs-lookup"><span data-stu-id="047d5-199">Java uses its own [certificate store](https://docs.oracle.com/cd/E19830-01/819-4712/ablqw/index.html) whereas Python uses [socket wrappers](https://docs.python.org/2/library/ssl.html).</span></span>

<span data-ttu-id="047d5-200">Чтобы использовать сертификат с языками и средами выполнения, которые не интегрируются с хранилищем сертификатов Windows, необходимо экспортировать сертификат с помощью диспетчера сертификатов Windows.</span><span class="sxs-lookup"><span data-stu-id="047d5-200">In order to obtain a certificate to use with languages and runtimes that do not integrate with the Windows Certificate Store you will need to export it using the Windows Certificate Manager.</span></span> <span data-ttu-id="047d5-201">Чтобы открыть его, запустите файл certlm.msc или выполните пошаговые инструкции по [экспорту сертификатов в эмуляторе Azure Cosmos DB](./local-emulator-export-ssl-certificates.md).</span><span class="sxs-lookup"><span data-stu-id="047d5-201">You can start it by running certlm.msc or follow the step by step instructions in [Export the Azure Cosmos DB Emulator Certificates](./local-emulator-export-ssl-certificates.md).</span></span> <span data-ttu-id="047d5-202">Когда откроется диспетчер сертификатов, откройте в нем "Личные сертификаты", как показано ниже, и экспортируйте сертификат с понятным именем DocumentDBEmulatorCertificate в формате X.509 с кодировкой BASE-64 (CER-файл).</span><span class="sxs-lookup"><span data-stu-id="047d5-202">Once the certificate manager is running, open the Personal Certificates as shown below and export the certificate with the friendly name "DocumentDBEmulatorCertificate" as a BASE-64 encoded X.509 (.cer) file.</span></span>

![Сертификат SSL для эмулятора Azure Cosmos DB](./media/local-emulator/database-local-emulator-ssl_certificate.png)

<span data-ttu-id="047d5-204">Чтобы импортировать сертификат X.509 в хранилище сертификатов Java, выполните инструкции из статьи [Добавление сертификата в хранилище сертификатов ЦС Java](https://docs.microsoft.com/azure/java-add-certificate-ca-store).</span><span class="sxs-lookup"><span data-stu-id="047d5-204">The X.509 certificate can be imported into the Java certificate store by following the instructions in [Adding a Certificate to the Java CA Certificates Store](https://docs.microsoft.com/azure/java-add-certificate-ca-store).</span></span> <span data-ttu-id="047d5-205">После импорта сертификата в хранилище сертификатов приложения Java и MongoDB смогут подключаться к эмулятору DB Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="047d5-205">Once the certificate is imported into the certificate store, Java and MongoDB applications will be able to connect to the Azure Cosmos DB Emulator.</span></span>

<span data-ttu-id="047d5-206">При подключении к эмулятору с помощью пакетов SDK для Python и Node.js проверка SSL отключена.</span><span class="sxs-lookup"><span data-stu-id="047d5-206">When connecting to the emulator from Python and Node.js SDKs, SSL verification is disabled.</span></span>

## <span data-ttu-id="047d5-207"><a id="command-line"></a>Справочник по программе командной строки</span><span class="sxs-lookup"><span data-stu-id="047d5-207"><a id="command-line"></a>Command-line tool reference</span></span>
<span data-ttu-id="047d5-208">С помощью командной строки из папки установки можно запускать и останавливать эмулятор, настраивать параметры и выполнять другие операции.</span><span class="sxs-lookup"><span data-stu-id="047d5-208">From the installation location, you can use the command-line to start and stop the emulator, configure options, and perform other operations.</span></span>

### <a name="command-line-syntax"></a><span data-ttu-id="047d5-209">Синтаксис для командной строки</span><span class="sxs-lookup"><span data-stu-id="047d5-209">Command-line Syntax</span></span>

    CosmosDB.Emulator.exe [/Shutdown] [/DataPath] [/Port] [/MongoPort] [/DirectPorts] [/Key] [/EnableRateLimiting] [/DisableRateLimiting] [/NoUI] [/NoExplorer] [/?]

<span data-ttu-id="047d5-210">Чтобы просмотреть список параметров, в командной строке введите `CosmosDB.Emulator.exe /?` .</span><span class="sxs-lookup"><span data-stu-id="047d5-210">To view the list of options, type `CosmosDB.Emulator.exe /?` at the command prompt.</span></span>

<table>
<tr>
  <td><span data-ttu-id="047d5-211"><strong>Параметр</strong></span><span class="sxs-lookup"><span data-stu-id="047d5-211"><strong>Option</strong></span></span></td>
  <td><span data-ttu-id="047d5-212"><strong>Описание</strong></span><span class="sxs-lookup"><span data-stu-id="047d5-212"><strong>Description</strong></span></span></td>
  <td><span data-ttu-id="047d5-213"><strong>Команда</strong></span><span class="sxs-lookup"><span data-stu-id="047d5-213"><strong>Command</strong></span></span></td>
  <td><span data-ttu-id="047d5-214"><strong>Аргументы</strong></span><span class="sxs-lookup"><span data-stu-id="047d5-214"><strong>Arguments</strong></span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="047d5-215">[Нет аргументов]</span><span class="sxs-lookup"><span data-stu-id="047d5-215">[No arguments]</span></span></td>
  <td><span data-ttu-id="047d5-216">Запускает эмулятор Azure Cosmos DB с параметрами по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="047d5-216">Starts up the Azure Cosmos DB Emulator with default settings.</span></span></td>
  <td><span data-ttu-id="047d5-217">CosmosDB.Emulator.exe</span><span class="sxs-lookup"><span data-stu-id="047d5-217">CosmosDB.Emulator.exe</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="047d5-218">[Help]</span><span class="sxs-lookup"><span data-stu-id="047d5-218">[Help]</span></span></td>
  <td><span data-ttu-id="047d5-219">Отображает список поддерживаемых аргументов командной строки.</span><span class="sxs-lookup"><span data-stu-id="047d5-219">Displays the list of supported command-line arguments.</span></span></td>
  <td><span data-ttu-id="047d5-220">CosmosDB.Emulator.exe /?</span><span class="sxs-lookup"><span data-stu-id="047d5-220">CosmosDB.Emulator.exe /?</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="047d5-221">Shutdown</span><span class="sxs-lookup"><span data-stu-id="047d5-221">Shutdown</span></span></td>
  <td><span data-ttu-id="047d5-222">Завершает работу эмулятора Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="047d5-222">Shuts down the Azure Cosmos DB Emulator.</span></span></td>
  <td><span data-ttu-id="047d5-223">CosmosDB.Emulator.exe /Shutdown</span><span class="sxs-lookup"><span data-stu-id="047d5-223">CosmosDB.Emulator.exe /Shutdown</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="047d5-224">DataPath</span><span class="sxs-lookup"><span data-stu-id="047d5-224">DataPath</span></span></td>
  <td><span data-ttu-id="047d5-225">Указывает путь для сохранения файлов данных.</span><span class="sxs-lookup"><span data-stu-id="047d5-225">Specifies the path in which to store data files.</span></span> <span data-ttu-id="047d5-226">Значение по умолчанию — %LocalAppdata%\CosmosDBEmulator.</span><span class="sxs-lookup"><span data-stu-id="047d5-226">Default is %LocalAppdata%\CosmosDBEmulator.</span></span></td>
  <td><span data-ttu-id="047d5-227">CosmosDB.Emulator.exe /DataPath=&lt;путь_к_данным&gt;</span><span class="sxs-lookup"><span data-stu-id="047d5-227">CosmosDB.Emulator.exe /DataPath=&lt;datapath&gt;</span></span></td>
  <td><span data-ttu-id="047d5-228">&lt;datapath&gt;: любой доступный путь</span><span class="sxs-lookup"><span data-stu-id="047d5-228">&lt;datapath&gt;: An accessible path</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="047d5-229">Порт</span><span class="sxs-lookup"><span data-stu-id="047d5-229">Port</span></span></td>
  <td><span data-ttu-id="047d5-230">Указывает номер порта, который должен использоваться эмулятором.</span><span class="sxs-lookup"><span data-stu-id="047d5-230">Specifies the port number to use for the emulator.</span></span>  <span data-ttu-id="047d5-231">Значение по умолчанию — 8081.</span><span class="sxs-lookup"><span data-stu-id="047d5-231">Default is 8081.</span></span></td>
  <td><span data-ttu-id="047d5-232">CosmosDB.Emulator.exe /Port=&lt;порт&gt;</span><span class="sxs-lookup"><span data-stu-id="047d5-232">CosmosDB.Emulator.exe /Port=&lt;port&gt;</span></span></td>
  <td><span data-ttu-id="047d5-233">&lt;port&gt;: один номер порта</span><span class="sxs-lookup"><span data-stu-id="047d5-233">&lt;port&gt;: Single port number</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="047d5-234">MongoPort</span><span class="sxs-lookup"><span data-stu-id="047d5-234">MongoPort</span></span></td>
  <td><span data-ttu-id="047d5-235">Указывает номер порта для использования с интерфейсом совместимости с MongoDB.</span><span class="sxs-lookup"><span data-stu-id="047d5-235">Specifies the port number to use for MongoDB compatibility API.</span></span> <span data-ttu-id="047d5-236">Значение по умолчанию — 10255.</span><span class="sxs-lookup"><span data-stu-id="047d5-236">Default is 10255.</span></span></td>
  <td><span data-ttu-id="047d5-237">CosmosDB.Emulator.exe /MongoPort=&lt;порт_mongo&gt;</span><span class="sxs-lookup"><span data-stu-id="047d5-237">CosmosDB.Emulator.exe /MongoPort=&lt;mongoport&gt;</span></span></td>
  <td><span data-ttu-id="047d5-238">&lt;mongoport&gt;: один номер порта</span><span class="sxs-lookup"><span data-stu-id="047d5-238">&lt;mongoport&gt;: Single port number</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="047d5-239">DirectPorts</span><span class="sxs-lookup"><span data-stu-id="047d5-239">DirectPorts</span></span></td>
  <td><span data-ttu-id="047d5-240">Указывает порты, которые нужно использовать для прямого подключения.</span><span class="sxs-lookup"><span data-stu-id="047d5-240">Specifies the ports to use for direct connectivity.</span></span> <span data-ttu-id="047d5-241">По умолчанию это порты 10251, 10252, 10253, 10254.</span><span class="sxs-lookup"><span data-stu-id="047d5-241">Defaults are 10251,10252,10253,10254.</span></span></td>
  <td><span data-ttu-id="047d5-242">CosmosDB.Emulator.exe /DirectPorts:&lt;directports&gt;</span><span class="sxs-lookup"><span data-stu-id="047d5-242">CosmosDB.Emulator.exe /DirectPorts:&lt;directports&gt;</span></span></td>
  <td><span data-ttu-id="047d5-243">&lt;directports&gt;: разделенный запятыми список из 4 портов</span><span class="sxs-lookup"><span data-stu-id="047d5-243">&lt;directports&gt;: Comma-delimited list of 4 ports</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="047d5-244">Ключ</span><span class="sxs-lookup"><span data-stu-id="047d5-244">Key</span></span></td>
  <td><span data-ttu-id="047d5-245">Ключ проверки подлинности для эмулятора.</span><span class="sxs-lookup"><span data-stu-id="047d5-245">Authorization key for the emulator.</span></span> <span data-ttu-id="047d5-246">Ключ должен иметь формат 64-разрядного вектора в кодировке Base-64.</span><span class="sxs-lookup"><span data-stu-id="047d5-246">Key must be the base-64 encoding of a 64-byte vector.</span></span></td>
  <td><span data-ttu-id="047d5-247">CosmosDB.Emulator.exe /Key:&lt;ключ&gt;</span><span class="sxs-lookup"><span data-stu-id="047d5-247">CosmosDB.Emulator.exe /Key:&lt;key&gt;</span></span></td>
  <td><span data-ttu-id="047d5-248">&lt;key&gt;: ключ в формате 64-разрядного вектора в кодировке base-64</span><span class="sxs-lookup"><span data-stu-id="047d5-248">&lt;key&gt;: Key must be the base-64 encoding of a 64-byte vector</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="047d5-249">EnableRateLimiting</span><span class="sxs-lookup"><span data-stu-id="047d5-249">EnableRateLimiting</span></span></td>
  <td><span data-ttu-id="047d5-250">Указывает, что ограничение частоты запросов включено.</span><span class="sxs-lookup"><span data-stu-id="047d5-250">Specifies that request rate limiting behavior is enabled.</span></span></td>
  <td><span data-ttu-id="047d5-251">CosmosDB.Emulator.exe /EnableRateLimiting</span><span class="sxs-lookup"><span data-stu-id="047d5-251">CosmosDB.Emulator.exe /EnableRateLimiting</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="047d5-252">DisableRateLimiting</span><span class="sxs-lookup"><span data-stu-id="047d5-252">DisableRateLimiting</span></span></td>
  <td><span data-ttu-id="047d5-253">Указывает, что ограничение частоты запросов отключено.</span><span class="sxs-lookup"><span data-stu-id="047d5-253">Specifies that request rate limiting behavior is disabled.</span></span></td>
  <td><span data-ttu-id="047d5-254">CosmosDB.Emulator.exe /DisableRateLimiting</span><span class="sxs-lookup"><span data-stu-id="047d5-254">CosmosDB.Emulator.exe /DisableRateLimiting</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="047d5-255">NoUI</span><span class="sxs-lookup"><span data-stu-id="047d5-255">NoUI</span></span></td>
  <td><span data-ttu-id="047d5-256">Скрывает пользовательский интерфейс эмулятора.</span><span class="sxs-lookup"><span data-stu-id="047d5-256">Do not show the emulator user interface.</span></span></td>
  <td><span data-ttu-id="047d5-257">CosmosDB.Emulator.exe /NoUI</span><span class="sxs-lookup"><span data-stu-id="047d5-257">CosmosDB.Emulator.exe /NoUI</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="047d5-258">NoExplorer</span><span class="sxs-lookup"><span data-stu-id="047d5-258">NoExplorer</span></span></td>
  <td><span data-ttu-id="047d5-259">Скрывает обозреватель документов при запуске.</span><span class="sxs-lookup"><span data-stu-id="047d5-259">Don't show document explorer on startup.</span></span></td>
  <td><span data-ttu-id="047d5-260">CosmosDB.Emulator.exe /NoExplorer</span><span class="sxs-lookup"><span data-stu-id="047d5-260">CosmosDB.Emulator.exe /NoExplorer</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="047d5-261">PartitionCount</span><span class="sxs-lookup"><span data-stu-id="047d5-261">PartitionCount</span></span></td>
  <td><span data-ttu-id="047d5-262">Указывает максимальное количество секционированных коллекций.</span><span class="sxs-lookup"><span data-stu-id="047d5-262">Specifies the maximum number of partitioned collections.</span></span> <span data-ttu-id="047d5-263">Дополнительные сведения см. в разделе [Изменение количества коллекций](#set-partitioncount).</span><span class="sxs-lookup"><span data-stu-id="047d5-263">See [Change the number of collections](#set-partitioncount) for more information.</span></span></td>
  <td><span data-ttu-id="047d5-264">CosmosDB.Emulator.exe /PartitionCount=&lt;число_разделов&gt;</span><span class="sxs-lookup"><span data-stu-id="047d5-264">CosmosDB.Emulator.exe /PartitionCount=&lt;partitioncount&gt;</span></span></td>
  <td><span data-ttu-id="047d5-265">&lt;partitioncount&gt;: максимально допустимое количество односекционных коллекций.</span><span class="sxs-lookup"><span data-stu-id="047d5-265">&lt;partitioncount&gt;: Maximum number of allowed single partition collections.</span></span> <span data-ttu-id="047d5-266">Значение по умолчанию — 25.</span><span class="sxs-lookup"><span data-stu-id="047d5-266">Default is 25.</span></span> <span data-ttu-id="047d5-267">Максимально допустимое значение — 250.</span><span class="sxs-lookup"><span data-stu-id="047d5-267">Maximum allowed is 250.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="047d5-268">DefaultPartitionCount</span><span class="sxs-lookup"><span data-stu-id="047d5-268">DefaultPartitionCount</span></span></td>
  <td><span data-ttu-id="047d5-269">Указывает количество секций по умолчанию для секционированной коллекции.</span><span class="sxs-lookup"><span data-stu-id="047d5-269">Specifies the default number of partitions for a partitioned collection.</span></span></td>
  <td><span data-ttu-id="047d5-270">CosmosDB.Emulator.exe /DefaultPartitionCount=&lt;defaultpartitioncount&gt;</span><span class="sxs-lookup"><span data-stu-id="047d5-270">CosmosDB.Emulator.exe /DefaultPartitionCount=&lt;defaultpartitioncount&gt;</span></span></td>
  <td><span data-ttu-id="047d5-271">&lt;defaultpartitioncount&gt; Значение по умолчанию — 25.</span><span class="sxs-lookup"><span data-stu-id="047d5-271">&lt;defaultpartitioncount&gt; Default is 25.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="047d5-272">AllowNetworkAccess</span><span class="sxs-lookup"><span data-stu-id="047d5-272">AllowNetworkAccess</span></span></td>
  <td><span data-ttu-id="047d5-273">Разрешает доступ к эмулятору по сети.</span><span class="sxs-lookup"><span data-stu-id="047d5-273">Enables access to the emulator over a network.</span></span> <span data-ttu-id="047d5-274">Для включения сетевого доступа нужно также передать один из параметров: /Key=&lt;строка_ключа&gt; или /KeyFile=&lt;имя_файла&gt;.</span><span class="sxs-lookup"><span data-stu-id="047d5-274">You must also pass /Key=&lt;key_string&gt; or /KeyFile=&lt;file_name&gt; to enable network access.</span></span></td>
  <td><span data-ttu-id="047d5-275">CosmosDB.Emulator.exe /AllowNetworkAccess /Key=&lt;строка_ключа&gt;</span><span class="sxs-lookup"><span data-stu-id="047d5-275">CosmosDB.Emulator.exe /AllowNetworkAccess /Key=&lt;key_string&gt;</span></span><br><br><span data-ttu-id="047d5-276">или</span><span class="sxs-lookup"><span data-stu-id="047d5-276">or</span></span><br><br><span data-ttu-id="047d5-277">CosmosDB.Emulator.exe /AllowNetworkAccess /KeyFile=&lt;имя_файла&gt;</span><span class="sxs-lookup"><span data-stu-id="047d5-277">CosmosDB.Emulator.exe /AllowNetworkAccess /KeyFile=&lt;file_name&gt;</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="047d5-278">NoFirewall</span><span class="sxs-lookup"><span data-stu-id="047d5-278">NoFirewall</span></span></td>
  <td><span data-ttu-id="047d5-279">Не изменять правила брандмауэра при использовании /AllowNetworkAccess.</span><span class="sxs-lookup"><span data-stu-id="047d5-279">Don't adjust firewall rules when /AllowNetworkAccess is used.</span></span></td>
  <td><span data-ttu-id="047d5-280">CosmosDB.Emulator.exe /NoFirewall</span><span class="sxs-lookup"><span data-stu-id="047d5-280">CosmosDB.Emulator.exe /NoFirewall</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="047d5-281">GenKeyFile</span><span class="sxs-lookup"><span data-stu-id="047d5-281">GenKeyFile</span></span></td>
  <td><span data-ttu-id="047d5-282">Создает новый ключ авторизации и сохраняет его в указанном файле.</span><span class="sxs-lookup"><span data-stu-id="047d5-282">Generate a new authorization key and save to the specified file.</span></span> <span data-ttu-id="047d5-283">Созданный ключ можно использовать с параметрами/Key или/KeyFile.</span><span class="sxs-lookup"><span data-stu-id="047d5-283">The generated key can be used with the /Key or /KeyFile options.</span></span></td>
  <td><span data-ttu-id="047d5-284">CosmosDB.Emulator.exe  /GenKeyFile=&lt;путь к файлу ключа&gt;</span><span class="sxs-lookup"><span data-stu-id="047d5-284">CosmosDB.Emulator.exe  /GenKeyFile=&lt;path to key file&gt;</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="047d5-285">Целостность</span><span class="sxs-lookup"><span data-stu-id="047d5-285">Consistency</span></span></td>
  <td><span data-ttu-id="047d5-286">Определяет уровень согласованности по умолчанию для учетной записи.</span><span class="sxs-lookup"><span data-stu-id="047d5-286">Set the default consistency level for the account.</span></span></td>
  <td><span data-ttu-id="047d5-287">CosmosDB.Emulator.exe /Consistency=&lt;consistency&gt;</span><span class="sxs-lookup"><span data-stu-id="047d5-287">CosmosDB.Emulator.exe /Consistency=&lt;consistency&gt;</span></span></td>
  <td><span data-ttu-id="047d5-288">&lt;consistency&gt;: допускается любое значение из следующих [уровней согласованности](consistency-levels.md): Session (на уровне сеансов), Strong (сильная), Eventual (итоговая) или BoundedStaleness (с ограниченным устареванием).</span><span class="sxs-lookup"><span data-stu-id="047d5-288">&lt;consistency&gt;: Value must be one of the following [consistency levels](consistency-levels.md): Session, Strong, Eventual, or BoundedStaleness.</span></span>  <span data-ttu-id="047d5-289">По умолчанию используется значение Session.</span><span class="sxs-lookup"><span data-stu-id="047d5-289">The default value is Session.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="047d5-290">?</span><span class="sxs-lookup"><span data-stu-id="047d5-290">?</span></span></td>
  <td><span data-ttu-id="047d5-291">Показывает справочные сообщения.</span><span class="sxs-lookup"><span data-stu-id="047d5-291">Show the help message.</span></span></td>
  <td></td>
  <td></td>
</tr>
</table>

## <a name="differences-between-the-azure-cosmos-db-emulator-and-azure-cosmos-db"></a><span data-ttu-id="047d5-292">Различия между эмулятором Azure Cosmos DB и службой Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="047d5-292">Differences between the Azure Cosmos DB Emulator and Azure Cosmos DB</span></span> 
<span data-ttu-id="047d5-293">Эмулятор Azure Cosmos DB обеспечивает эмулированную среду, выполняемую на локальном компьютере разработчика. Поэтому возможности эмулятора и облачной учетной записи Azure Cosmos DB несколько отличаются.</span><span class="sxs-lookup"><span data-stu-id="047d5-293">Because the Azure Cosmos DB Emulator provides an emulated environment running on a local developer workstation, there are some differences in functionality between the emulator and an Azure Cosmos DB account in the cloud:</span></span>

* <span data-ttu-id="047d5-294">Эмулятор Azure Cosmos DB поддерживает только одну предопределенную учетную запись и известный главный ключ.</span><span class="sxs-lookup"><span data-stu-id="047d5-294">The Azure Cosmos DB Emulator supports only a single fixed account and a well-known master key.</span></span>  <span data-ttu-id="047d5-295">Повторное создание ключей в эмуляторе Azure Cosmos DB не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="047d5-295">Key regeneration is not possible in the Azure Cosmos DB Emulator.</span></span>
* <span data-ttu-id="047d5-296">Эмулятор Azure Cosmos DB не поддерживает масштабирование и не может работать с большим числом коллекций.</span><span class="sxs-lookup"><span data-stu-id="047d5-296">The Azure Cosmos DB Emulator is not a scalable service and will not support a large number of collections.</span></span>
* <span data-ttu-id="047d5-297">Эмулятор Azure Cosmos DB не поддерживает [уровни согласованности Azure Cosmos DB](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="047d5-297">The Azure Cosmos DB Emulator does not simulate different [Azure Cosmos DB consistency levels](consistency-levels.md).</span></span>
* <span data-ttu-id="047d5-298">Эмулятор Azure Cosmos DB не поддерживает [репликацию между несколькими регионами](distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="047d5-298">The Azure Cosmos DB Emulator does not simulate [multi-region replication](distribute-data-globally.md).</span></span>
* <span data-ttu-id="047d5-299">Эмулятор Azure Cosmos DB не поддерживает переопределение квот для службы, которое возможно в службе Azure Cosmos DB (например, ограничения на размер документа, увеличение хранилища для секционированных коллекций).</span><span class="sxs-lookup"><span data-stu-id="047d5-299">The Azure Cosmos DB Emulator does not support the service quota overrides that are available in the Azure Cosmos DB service (e.g. document size limits, increased partitioned collection storage).</span></span>
* <span data-ttu-id="047d5-300">Локальная версия эмулятора Azure Cosmos DB может не всегда отражать свежие изменения в службе Azure Cosmos DB. Поэтому, чтобы точно оценить необходимую пропускную способность для приложения, используйте [планировщик ресурсов Azure Cosmos DB](https://www.documentdb.com/capacityplanner).</span><span class="sxs-lookup"><span data-stu-id="047d5-300">As your copy of the Azure Cosmos DB Emulator might not be up to date with the most recent changes with the Azure Cosmos DB service, please [Azure Cosmos DB capacity planner](https://www.documentdb.com/capacityplanner) to accurately estimate production throughput (RUs) needs of your application.</span></span>

## <span data-ttu-id="047d5-301"><a id="set-partitioncount"></a>Изменение количества коллекций</span><span class="sxs-lookup"><span data-stu-id="047d5-301"><a id="set-partitioncount"></a>Change the number of collections</span></span>

<span data-ttu-id="047d5-302">По умолчанию с помощью эмулятора Azure Cosmos DB можно создать до 25 односекционных коллекций или одну секционированную коллекцию.</span><span class="sxs-lookup"><span data-stu-id="047d5-302">By default, you can create up to 25 single partition collections, or 1 partitioned collection using the Azure Cosmos DB Emulator.</span></span> <span data-ttu-id="047d5-303">Изменив значение **PartitionCount**, можно создать до 250 односекционных или 10 секционированных коллекций. А также можно комбинировать оба типа коллекций, при этом количество отдельных секций не должно превышать 250 (из расчета, что 1 секционированная коллекция = 25 односекционных коллекций).</span><span class="sxs-lookup"><span data-stu-id="047d5-303">By modifying the **PartitionCount** value, you can create up to 250 single partition collections or 10 partitioned collections, or any combination of the two that does not exceed 250 single partitions (where 1 partitioned collection = 25 single partition collection).</span></span>

<span data-ttu-id="047d5-304">При попытке создать коллекцию сверх этих ограничений на количество секций эмулятор порождает исключение ServiceUnavailable со следующим сообщением:</span><span class="sxs-lookup"><span data-stu-id="047d5-304">If you attempt to create a collection after the current partition count has been exceeded, the emulator throws a ServiceUnavailable exception, with the following message.</span></span>

    Sorry, we are currently experiencing high demand in this region, 
    and cannot fulfill your request at this time. We work continuously 
    to bring more and more capacity online, and encourage you to try again. 
    Please do not hesitate to email docdbswat@microsoft.com at any time or 
    for any reason. ActivityId: 29da65cc-fba1-45f9-b82c-bf01d78a1f91

<span data-ttu-id="047d5-305">Чтобы изменить число доступных для эмулятора Azure Cosmos DB коллекций, сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="047d5-305">To change the number of collections available to the Azure Cosmos DB Emulator, do the following:</span></span>

1. <span data-ttu-id="047d5-306">Удалите все локальные данные эмулятора Azure Cosmos DB, щелкнув правой кнопкой мыши значок **эмулятора Azure Cosmos DB** в области уведомлений и выбрав **Сброс данных**.</span><span class="sxs-lookup"><span data-stu-id="047d5-306">Delete all local Azure Cosmos DB Emulator data by right-clicking the **Azure Cosmos DB Emulator** icon on the system tray, and then clicking **Reset Data…**.</span></span>
2. <span data-ttu-id="047d5-307">Удалите все данные эмулятора в этой папке: C:\Users\имя_пользователя\AppData\Local\CosmosDBEmulator.</span><span class="sxs-lookup"><span data-stu-id="047d5-307">Delete all emulator data in this folder C:\Users\user_name\AppData\Local\CosmosDBEmulator.</span></span>
3. <span data-ttu-id="047d5-308">Выйдите из всех открытых экземпляров, щелкнув правой кнопкой мыши значок **эмулятора Azure Cosmos DB** в области уведомлений и выбрав **Выход**.</span><span class="sxs-lookup"><span data-stu-id="047d5-308">Exit all open instances by right-clicking the **Azure Cosmos DB Emulator** icon on the system tray, and then clicking **Exit**.</span></span> <span data-ttu-id="047d5-309">Выход из всех экземпляров может занять около минуты.</span><span class="sxs-lookup"><span data-stu-id="047d5-309">It may take a minute for all instances to exit.</span></span>
4. <span data-ttu-id="047d5-310">Установите последнюю версию [эмулятора Azure Cosmos DB](https://aka.ms/cosmosdb-emulator).</span><span class="sxs-lookup"><span data-stu-id="047d5-310">Install the latest version of the [Azure Cosmos DB Emulator](https://aka.ms/cosmosdb-emulator).</span></span>
5. <span data-ttu-id="047d5-311">Запустите эмулятор с флагом PartitionCount, задав значение <= 250.</span><span class="sxs-lookup"><span data-stu-id="047d5-311">Launch the emulator with the PartitionCount flag by setting a value <= 250.</span></span> <span data-ttu-id="047d5-312">Например, `C:\Program Files\Azure CosmosDB Emulator>CosmosDB.Emulator.exe /PartitionCount=100`.</span><span class="sxs-lookup"><span data-stu-id="047d5-312">For example: `C:\Program Files\Azure CosmosDB Emulator>CosmosDB.Emulator.exe /PartitionCount=100`.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="047d5-313">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="047d5-313">Troubleshooting</span></span>

<span data-ttu-id="047d5-314">Ниже перечислены способы устранения неполадок с эмулятором Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="047d5-314">Use the following tips to help troubleshoot issues you encounter with the Azure Cosmos DB emulator:</span></span>

- <span data-ttu-id="047d5-315">Если установлена новая версия эмулятора и возникли ошибки, убедитесь, что вы сбросили данные.</span><span class="sxs-lookup"><span data-stu-id="047d5-315">If you installed a new version of the Emulator and are experiencing errors, ensure you reset your data.</span></span> <span data-ttu-id="047d5-316">Вы можете сбросить данные, щелкнув правой кнопкой мыши значок эмулятора Azure Cosmos DB в области уведомлений и выбрав "Сбросить данные".</span><span class="sxs-lookup"><span data-stu-id="047d5-316">You can reset your data by right-clicking the Azure Cosmos DB Emulator icon on the system tray, and then clicking Reset Data….</span></span> <span data-ttu-id="047d5-317">Если ошибки не устранены, можно удалить и переустановить приложение.</span><span class="sxs-lookup"><span data-stu-id="047d5-317">If that does not fix the errors, you can uninstall and reinstall the app.</span></span> <span data-ttu-id="047d5-318">Инструкции см. в разделе [Удаление локального эмулятора](#uninstall).</span><span class="sxs-lookup"><span data-stu-id="047d5-318">See [Uninstall the local emulator](#uninstall) for instructions.</span></span>

- <span data-ttu-id="047d5-319">В случае аварийного завершения эмулятора Azure Cosmos DB соберите файлы дампа из папки c:\Users\user_name\AppData\Local\CrashDumps, сожмите их, вложите в электронное сообщение и отправьте по адресу [askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="047d5-319">If the Azure Cosmos DB emulator crashes, collect dump files from c:\Users\user_name\AppData\Local\CrashDumps folder, compress them, and attach them to an email to [askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span></span>

- <span data-ttu-id="047d5-320">При возникновении сбоев в CosmosDB.StartupEntryPoint.exe выполните следующую команду из командной строки администратора: `lodctr /R`</span><span class="sxs-lookup"><span data-stu-id="047d5-320">If you experience crashes in CosmosDB.StartupEntryPoint.exe, run the following command from an admin command prompt: `lodctr /R`</span></span> 

- <span data-ttu-id="047d5-321">Если возникли проблемы с подключением, [соберите файлы трассировки](#trace-files), сожмите их, вложите в электронное сообщение и отправьте по адресу [askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="047d5-321">If you encounter a connectivity issue, [collect trace files](#trace-files), compress them, and attach them to an email to [askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span></span>

- <span data-ttu-id="047d5-322">При получении сообщения **Служба недоступна** эмулятор может не инициализировать сетевой стек.</span><span class="sxs-lookup"><span data-stu-id="047d5-322">If you receive a **Service Unavailable** message, the emulator might be failing to initialize the network stack.</span></span> <span data-ttu-id="047d5-323">Проверьте, установлен ли защищенный клиент Pulse или сетевой клиент Juniper, так как драйверы их сетевого фильтра могут вызвать проблему.</span><span class="sxs-lookup"><span data-stu-id="047d5-323">Check to see if you have the Pulse secure client or Juniper networks client installed, as their network filter drivers may cause the problem.</span></span> <span data-ttu-id="047d5-324">Удаление драйверов сетевого фильтра сторонних производителей обычно устраняет проблему.</span><span class="sxs-lookup"><span data-stu-id="047d5-324">Uninstalling third party network filter drivers typically fixes the issue.</span></span>

### <span data-ttu-id="047d5-325"><a id="trace-files"></a>Сбор файлов трассировки</span><span class="sxs-lookup"><span data-stu-id="047d5-325"><a id="trace-files"></a>Collect trace files</span></span>

<span data-ttu-id="047d5-326">Для сбора отладочных трассировок выполните следующие команды в командной строке с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="047d5-326">To collect debugging traces, run the following commands from an administrative command prompt:</span></span>

1. `cd /d "%ProgramFiles%\Azure Cosmos DB Emulator"`
2. <span data-ttu-id="047d5-327">`CosmosDB.Emulator.exe /shutdown`.</span><span class="sxs-lookup"><span data-stu-id="047d5-327">`CosmosDB.Emulator.exe /shutdown`.</span></span> <span data-ttu-id="047d5-328">Проверьте область уведомлений, чтобы убедиться, что работа программы завершена, так как на это может потребоваться до минуты.</span><span class="sxs-lookup"><span data-stu-id="047d5-328">Watch the system tray to make sure the program has shut down, it may take a minute.</span></span> <span data-ttu-id="047d5-329">Кроме того, можно просто щелкнуть **Выйти** в пользовательском интерфейсе эмулятора Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="047d5-329">You can also just click **Exit** in the Azure Cosmos DB emulator user interface.</span></span>
3. `CosmosDB.Emulator.exe /starttraces`
4. `CosmosDB.Emulator.exe`
5. <span data-ttu-id="047d5-330">Воспроизведите проблему.</span><span class="sxs-lookup"><span data-stu-id="047d5-330">Reproduce the problem.</span></span> <span data-ttu-id="047d5-331">Если обозреватель данных не работает, необходимо подождать несколько секунд, чтобы открылся браузер и ошибка возникла снова.</span><span class="sxs-lookup"><span data-stu-id="047d5-331">If Data Explorer is not working, you only need to wait for the browser to open for a few seconds to catch the error.</span></span>
5. `CosmosDB.Emulator.exe /stoptraces`
6. <span data-ttu-id="047d5-332">Перейдите к `%ProgramFiles%\Azure Cosmos DB Emulator` и найдите файл docdbemulator_000001.etl.</span><span class="sxs-lookup"><span data-stu-id="047d5-332">Navigate to `%ProgramFiles%\Azure Cosmos DB Emulator` and find the docdbemulator_000001.etl file.</span></span>
7. <span data-ttu-id="047d5-333">Отправьте ETL-файл и описание действий, которые привели к ошибке, на электронный адрес [askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com) для отладки.</span><span class="sxs-lookup"><span data-stu-id="047d5-333">Send the .etl file along with repro steps to [askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com) for debugging.</span></span>

### <span data-ttu-id="047d5-334"><a id="uninstall"></a>Удаление локального эмулятора</span><span class="sxs-lookup"><span data-stu-id="047d5-334"><a id="uninstall"></a>Uninstall the local Emulator</span></span>

1. <span data-ttu-id="047d5-335">Выйдите из всех открытых экземпляров локального эмулятора, щелкнув правой кнопкой мыши значок эмулятора Azure Cosmos DB в области уведомлений и выбрав "Выход".</span><span class="sxs-lookup"><span data-stu-id="047d5-335">Exit all open instances of the local Emulator by right-clicking the Azure Cosmos DB Emulator icon on the system tray, and then clicking Exit.</span></span> <span data-ttu-id="047d5-336">Выход из всех экземпляров может занять около минуты.</span><span class="sxs-lookup"><span data-stu-id="047d5-336">It may take a minute for all instances to exit.</span></span>
2. <span data-ttu-id="047d5-337">Введите в поле поиска Windows **Приложения и возможности** и выберите команду **Apps & features (System settings)** (Приложения и возможности (системные параметры)).</span><span class="sxs-lookup"><span data-stu-id="047d5-337">In the Windows search box, type **Apps & features** and click on the **Apps & features (System settings)** result.</span></span>
3. <span data-ttu-id="047d5-338">В списке приложений перейдите к **эмулятору Azure Cosmos DB**, выберите его, щелкните **Удалить**, подтвердите и щелкните **Удалить** еще раз.</span><span class="sxs-lookup"><span data-stu-id="047d5-338">In the list of apps, scroll to **Azure Cosmos DB Emulator**, select it, click **Uninstall**, then confirm and click **Uninstall** again.</span></span>
4. <span data-ttu-id="047d5-339">Удалив приложение, перейдите к папке C:\Users\<пользователя>\AppData\Local\CosmosDBEmulator и удалите ее.</span><span class="sxs-lookup"><span data-stu-id="047d5-339">When the app is uninstalled, navigate to C:\Users\<user>\AppData\Local\CosmosDBEmulator and delete the folder.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="047d5-340">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="047d5-340">Next steps</span></span>

<span data-ttu-id="047d5-341">В этом руководстве вы выполнили следующее:</span><span class="sxs-lookup"><span data-stu-id="047d5-341">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="047d5-342">установили локальный эмулятор;</span><span class="sxs-lookup"><span data-stu-id="047d5-342">Installed the local Emulator</span></span>
> * <span data-ttu-id="047d5-343">запустили эмулятор в Docker для Windows;</span><span class="sxs-lookup"><span data-stu-id="047d5-343">Rand the Emulator on Docker for Windows</span></span>
> * <span data-ttu-id="047d5-344">выполнили аутентификацию запросов;</span><span class="sxs-lookup"><span data-stu-id="047d5-344">Authenticated requests</span></span>
> * <span data-ttu-id="047d5-345">использовали обозреватель данных в эмуляторе;</span><span class="sxs-lookup"><span data-stu-id="047d5-345">Used the Data Explorer in the Emulator</span></span>
> * <span data-ttu-id="047d5-346">экспортировали сертификаты SSL;</span><span class="sxs-lookup"><span data-stu-id="047d5-346">Exported SSL certificates</span></span>
> * <span data-ttu-id="047d5-347">вызвали эмулятор из командной строки;</span><span class="sxs-lookup"><span data-stu-id="047d5-347">Called the Emulator from the command line</span></span>
> * <span data-ttu-id="047d5-348">собрали файлы трассировки.</span><span class="sxs-lookup"><span data-stu-id="047d5-348">Collected trace files</span></span>

<span data-ttu-id="047d5-349">Из этого руководства вы также узнали, как использовать локальный эмулятор для бесплатной разработки в локальной среде.</span><span class="sxs-lookup"><span data-stu-id="047d5-349">In this tutorial, you've learned how to use the local Emulator for free local development.</span></span> <span data-ttu-id="047d5-350">Теперь вы можете перейти к следующему руководству, из которого вы узнаете, как экспортировать сертификаты SSL эмулятора.</span><span class="sxs-lookup"><span data-stu-id="047d5-350">You can now proceed to the next tutorial and learn how to export Emulator SSL certificates.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="047d5-351">Экспорт сертификатов эмулятора Azure Cosmos DB для использования с Java, Python и Node.js</span><span class="sxs-lookup"><span data-stu-id="047d5-351">Export the Azure Cosmos DB Emulator certificates</span></span>](local-emulator-export-ssl-certificates.md)
