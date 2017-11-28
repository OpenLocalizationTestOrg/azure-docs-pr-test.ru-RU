---
title: "aaaDevelop локально с hello DB эмулятор Azure Cosmos | Документы Microsoft"
description: "Hello эмулятор DB Cosmos Azure можно разрабатывать и тестировать приложение для локально бесплатный, без создания подписки Azure."
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
ms.openlocfilehash: fb5449489e5f71664e72d8e11e583315be371bf3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-cosmos-db-emulator-for-local-development-and-testing"></a><span data-ttu-id="00a07-104">Использовать hello DB эмулятор Azure Cosmos локальной разработки и тестирования</span><span class="sxs-lookup"><span data-stu-id="00a07-104">Use hello Azure Cosmos DB Emulator for local development and testing</span></span>

<table>
<tr>
  <td><span data-ttu-id="00a07-105"><strong>Двоичные файлы</strong></span><span class="sxs-lookup"><span data-stu-id="00a07-105"><strong>Binaries</strong></span></span></td>
  <td>[<span data-ttu-id="00a07-106">Скачивание MSI</span><span class="sxs-lookup"><span data-stu-id="00a07-106">Download MSI</span></span>](https://aka.ms/cosmosdb-emulator)</td>
</tr>
<tr>
  <td><span data-ttu-id="00a07-107"><strong>Docker</strong></span><span class="sxs-lookup"><span data-stu-id="00a07-107"><strong>Docker</strong></span></span></td>
  <td>[<span data-ttu-id="00a07-108">Концентратор Docker</span><span class="sxs-lookup"><span data-stu-id="00a07-108">Docker Hub</span></span>](https://hub.docker.com/r/microsoft/azure-documentdb-emulator/)</td>
</tr>
<tr>
  <td><span data-ttu-id="00a07-109"><strong>Источник Docker</strong></span><span class="sxs-lookup"><span data-stu-id="00a07-109"><strong>Docker source</strong></span></span></td>
  <td>[<span data-ttu-id="00a07-110">Github</span><span class="sxs-lookup"><span data-stu-id="00a07-110">Github</span></span>](https://github.com/azure/azure-documentdb-emulator-docker)</td>
</tr>
</table>
  
<span data-ttu-id="00a07-111">Hello эмулятор DB Cosmos Azure предоставляет локальную среду, эмулирующую hello Azure Cosmos DB службу в целях разработки.</span><span class="sxs-lookup"><span data-stu-id="00a07-111">hello Azure Cosmos DB Emulator provides a local environment that emulates hello Azure Cosmos DB service for development purposes.</span></span> <span data-ttu-id="00a07-112">Hello эмулятор DB Cosmos Azure можно разрабатывать и тестировать приложение локально, без создания подписки Azure или любой расходов.</span><span class="sxs-lookup"><span data-stu-id="00a07-112">Using hello Azure Cosmos DB Emulator, you can develop and test your application locally, without creating an Azure subscription or incurring any costs.</span></span> <span data-ttu-id="00a07-113">Если вас устраивают, как приложение работает в hello эмулятор DB Cosmos Azure, можно переключиться toousing учетную запись Azure Cosmos DB в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="00a07-113">When you're satisfied with how your application is working in hello Azure Cosmos DB Emulator, you can switch toousing an Azure Cosmos DB account in hello cloud.</span></span>

<span data-ttu-id="00a07-114">В этой статье рассматриваются hello следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="00a07-114">This article covers hello following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="00a07-115">Установка hello эмулятора</span><span class="sxs-lookup"><span data-stu-id="00a07-115">Installing hello Emulator</span></span>
> * <span data-ttu-id="00a07-116">ОС Docker для Windows hello эмулятора</span><span class="sxs-lookup"><span data-stu-id="00a07-116">Running hello Emulator on Docker for Windows</span></span>
> * <span data-ttu-id="00a07-117">Выполнение проверки подлинности запросов</span><span class="sxs-lookup"><span data-stu-id="00a07-117">Authenticating requests</span></span>
> * <span data-ttu-id="00a07-118">С помощью hello обозреватель данных, в эмуляторе hello</span><span class="sxs-lookup"><span data-stu-id="00a07-118">Using hello Data Explorer in hello Emulator</span></span>
> * <span data-ttu-id="00a07-119">Экспорт сертификатов SSL</span><span class="sxs-lookup"><span data-stu-id="00a07-119">Exporting SSL certificates</span></span>
> * <span data-ttu-id="00a07-120">Вызов из командной строки hello hello эмулятора</span><span class="sxs-lookup"><span data-stu-id="00a07-120">Calling hello Emulator from hello command line</span></span>
> * <span data-ttu-id="00a07-121">Сбор файлов трассировки</span><span class="sxs-lookup"><span data-stu-id="00a07-121">Collecting trace files</span></span>

<span data-ttu-id="00a07-122">Корпорация Майкрософт рекомендует Приступая к работе посмотрите следующие видео, где Kirill Gavrylyuk показано, как tooget работу с hello DB эмулятор Azure Cosmos hello.</span><span class="sxs-lookup"><span data-stu-id="00a07-122">We recommend getting started by watching hello following video, where Kirill Gavrylyuk shows how tooget started with hello Azure Cosmos DB Emulator.</span></span> <span data-ttu-id="00a07-123">Примечание видео hello называется toohello эмулятор hello DocumentDB эмулятора, что был переименован средству hello hello DB эмулятор Azure Cosmos с момента щелкните hello видео.</span><span class="sxs-lookup"><span data-stu-id="00a07-123">Note that hello video refers toohello emulator as hello DocumentDB Emulator, but hello tool itself has been renamed hello Azure Cosmos DB Emulator since taping hello video.</span></span> <span data-ttu-id="00a07-124">Все сведения в видео hello актуальны для hello Azure Cosmos DB эмулятора.</span><span class="sxs-lookup"><span data-stu-id="00a07-124">All information in hello video is still accurate for hello Azure Cosmos DB Emulator.</span></span> 

> [!VIDEO https://channel9.msdn.com/Events/Connect/2016/192/player]
> 
> 

## <a name="how-hello-emulator-works"></a><span data-ttu-id="00a07-125">Как работает hello эмулятора</span><span class="sxs-lookup"><span data-stu-id="00a07-125">How hello Emulator works</span></span>
<span data-ttu-id="00a07-126">Hello эмулятор DB Cosmos Azure предоставляет эмуляцию hello Azure Cosmos DB службы высокого качества.</span><span class="sxs-lookup"><span data-stu-id="00a07-126">hello Azure Cosmos DB Emulator provides a high-fidelity emulation of hello Azure Cosmos DB service.</span></span> <span data-ttu-id="00a07-127">В эмуляторе реализованы те же функции, что и в службе Azure Cosmos DB, включая поддержку создания документов JSON и выполнение запросов к ним, подготовку и масштабирование коллекций, а также выполнение хранимых процедур и триггеров.</span><span class="sxs-lookup"><span data-stu-id="00a07-127">It supports identical functionality as Azure Cosmos DB, including support for creating and querying JSON documents, provisioning and scaling collections, and executing stored procedures and triggers.</span></span> <span data-ttu-id="00a07-128">Можно разрабатывать и тестирования приложений с помощью hello Azure Cosmos DB эмулятор и развернуть tooAzure по всему миру, просто чтобы изменить конечную точку подключения toohello для Azure Cosmos DB отдельную конфигурацию.</span><span class="sxs-lookup"><span data-stu-id="00a07-128">You can develop and test applications using hello Azure Cosmos DB Emulator, and deploy them tooAzure at global scale by just making a single configuration change toohello connection endpoint for Azure Cosmos DB.</span></span>

<span data-ttu-id="00a07-129">Хотя мы создали высококачественных локальной эмуляции фактические службы Azure Cosmos DB hello, реализация hello hello DB эмулятор Azure Cosmos отличается от службы hello.</span><span class="sxs-lookup"><span data-stu-id="00a07-129">While we created a high-fidelity local emulation of hello actual Azure Cosmos DB service, hello implementation of hello Azure Cosmos DB Emulator is different than that of hello service.</span></span> <span data-ttu-id="00a07-130">Например hello DB эмулятор Azure Cosmos использует стандартных компонентов операционной системы, таких как hello локальной файловой системе сохраняемости и стек протокола HTTPS для подключения.</span><span class="sxs-lookup"><span data-stu-id="00a07-130">For example, hello Azure Cosmos DB Emulator uses standard OS components such as hello local file system for persistence, and HTTPS protocol stack for connectivity.</span></span> <span data-ttu-id="00a07-131">Это означает, что некоторые функции, которая зависит от инфраструктуры Azure как глобальный репликации, задержка до миллисекунды десяти для операций чтения и записи и уровни согласованности пройтись недоступны через hello Azure Cosmos DB эмулятора.</span><span class="sxs-lookup"><span data-stu-id="00a07-131">This means that some functionality that relies on Azure infrastructure like global replication, single-digit millisecond latency for reads/writes, and tunable consistency levels are not available via hello Azure Cosmos DB Emulator.</span></span>

> [!NOTE]
> <span data-ttu-id="00a07-132">В это время hello обозреватель данных, в hello эмулятор поддерживает только создание hello DocumentDB API и коллекций MongoDB.</span><span class="sxs-lookup"><span data-stu-id="00a07-132">At this time hello Data Explorer in hello emulator only supports hello creation of DocumentDB API collections and MongoDB collections.</span></span> <span data-ttu-id="00a07-133">Hello обозреватель данных, в эмуляторе hello в настоящее время не поддерживает hello создания таблиц и диаграмм.</span><span class="sxs-lookup"><span data-stu-id="00a07-133">hello Data Explorer in hello emulator does not currently support hello creation of tables and graphs.</span></span> 

## <a name="system-requirements"></a><span data-ttu-id="00a07-134">Требования к системе</span><span class="sxs-lookup"><span data-stu-id="00a07-134">System requirements</span></span>
<span data-ttu-id="00a07-135">Hello эмулятор DB Cosmos Azure имеет следующие требования к оборудованию и программному обеспечению hello.</span><span class="sxs-lookup"><span data-stu-id="00a07-135">hello Azure Cosmos DB Emulator has hello following hardware and software requirements:</span></span>

* <span data-ttu-id="00a07-136">Требования к программному обеспечению</span><span class="sxs-lookup"><span data-stu-id="00a07-136">Software requirements</span></span>
  * <span data-ttu-id="00a07-137">Windows Server 2012 R2, Windows Server 2016 или Windows 10.</span><span class="sxs-lookup"><span data-stu-id="00a07-137">Windows Server 2012 R2, Windows Server 2016, or Windows 10</span></span>
*   <span data-ttu-id="00a07-138">Минимальные требования к оборудованию</span><span class="sxs-lookup"><span data-stu-id="00a07-138">Minimum Hardware requirements</span></span>
  * <span data-ttu-id="00a07-139">ОЗУ 2 ГБ.</span><span class="sxs-lookup"><span data-stu-id="00a07-139">2 GB RAM</span></span>
  * <span data-ttu-id="00a07-140">10 ГБ свободного дискового пространства.</span><span class="sxs-lookup"><span data-stu-id="00a07-140">10 GB available hard disk space</span></span>

## <a name="installation"></a><span data-ttu-id="00a07-141">Установка</span><span class="sxs-lookup"><span data-stu-id="00a07-141">Installation</span></span>
<span data-ttu-id="00a07-142">Можно загрузить и установить эмулятор DB Cosmos Azure hello из hello [центра загрузки Майкрософт](https://aka.ms/cosmosdb-emulator).</span><span class="sxs-lookup"><span data-stu-id="00a07-142">You can download and install hello Azure Cosmos DB Emulator from hello [Microsoft Download Center](https://aka.ms/cosmosdb-emulator).</span></span> 

> [!NOTE]
> <span data-ttu-id="00a07-143">tooinstall, настройки и запуска hello эмулятор DB Cosmos Azure, необходимо иметь права администратора на компьютере hello.</span><span class="sxs-lookup"><span data-stu-id="00a07-143">tooinstall, configure, and run hello Azure Cosmos DB Emulator, you must have administrative privileges on hello computer.</span></span>

## <a name="running-on-docker-for-windows"></a><span data-ttu-id="00a07-144">Выполнение в Docker для Windows</span><span class="sxs-lookup"><span data-stu-id="00a07-144">Running on Docker for Windows</span></span>

<span data-ttu-id="00a07-145">Hello Azure Cosmos DB эмулятор может выполняться на Docker для Windows.</span><span class="sxs-lookup"><span data-stu-id="00a07-145">hello Azure Cosmos DB Emulator can be run on Docker for Windows.</span></span> <span data-ttu-id="00a07-146">Hello эмулятор не поддерживает Docker для Oracle Linux.</span><span class="sxs-lookup"><span data-stu-id="00a07-146">hello Emulator does not work on Docker for Oracle Linux.</span></span>

<span data-ttu-id="00a07-147">После получения [Docker для Windows](https://www.docker.com/docker-windows) установлен, вы можете извлечь образа эмулятора hello из Docker Hub, выполнив следующую команду из избранных оболочка hello (cmd.exe, PowerShell, и т. д.).</span><span class="sxs-lookup"><span data-stu-id="00a07-147">Once you have [Docker for Windows](https://www.docker.com/docker-windows) installed, you can pull hello Emulator image from Docker Hub by running hello following command from your favorite shell (cmd.exe, PowerShell, etc.).</span></span>

```      
docker pull microsoft/azure-cosmosdb-emulator 
```
<span data-ttu-id="00a07-148">hello изображение toostart, запустите следующие команды hello.</span><span class="sxs-lookup"><span data-stu-id="00a07-148">toostart hello image, run hello following commands.</span></span>

``` 
md %LOCALAPPDATA%\CosmosDBEmulatorCert 2>nul
docker run -v %LOCALAPPDATA%\CosmosDBEmulatorCert:c:\CosmosDBEmulator\CosmosDBEmulatorCert -P -t -i microsoft/azure-cosmosdb-emulator 
```

<span data-ttu-id="00a07-149">Hello ответа выглядит примерно toohello следующее:</span><span class="sxs-lookup"><span data-stu-id="00a07-149">hello response looks similar toohello following:</span></span>

```
Starting Emulator
Emulator Endpoint: https://172.20.229.193:8081/
Master Key: C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==
Exporting SSL Certificate
You can import hello SSL certificate from an administrator command prompt on hello host by running:
cd /d %LOCALAPPDATA%\CosmosDBEmulatorCert
powershell .\importcert.ps1
--------------------------------------------------------------------------------------------------
Starting interactive shell
``` 

<span data-ttu-id="00a07-150">Закрытие интерактивной оболочки hello один раз hello запуска эмулятора будет завершить работу hello эмулятора контейнера.</span><span class="sxs-lookup"><span data-stu-id="00a07-150">Closing hello interactive shell once hello Emulator has been started will shutdown hello Emulator’s container.</span></span>

<span data-ttu-id="00a07-151">Конечная точка hello и главный ключ в ответе hello в клиентском приложении и импорта hello SSL-сертификата в узле.</span><span class="sxs-lookup"><span data-stu-id="00a07-151">Use hello endpoint and master key in from hello response in your client and import hello SSL certificate into your host.</span></span> <span data-ttu-id="00a07-152">hello tooimport SSL-сертификат hello от командную строку администратора:</span><span class="sxs-lookup"><span data-stu-id="00a07-152">tooimport hello SSL certificate, do hello following from an admin command prompt:</span></span>

```
cd %LOCALAPPDATA%\CosmosDBEmulatorCert
powershell .\importcert.ps1
```


## <a name="start-hello-emulator"></a><span data-ttu-id="00a07-153">Запуск эмулятора hello</span><span class="sxs-lookup"><span data-stu-id="00a07-153">Start hello Emulator</span></span>

<span data-ttu-id="00a07-154">hello toostart эмулятор DB Cosmos Azure, выберите "Пуск" hello, или нажмите клавишу Windows hello.</span><span class="sxs-lookup"><span data-stu-id="00a07-154">toostart hello Azure Cosmos DB Emulator, select hello Start button or press hello Windows key.</span></span> <span data-ttu-id="00a07-155">Начните вводить **DB эмулятор Azure Cosmos**и выберите hello эмулятор из списка приложений hello.</span><span class="sxs-lookup"><span data-stu-id="00a07-155">Begin typing **Azure Cosmos DB Emulator**, and select hello emulator from hello list of applications.</span></span> 

![Выберите hello или клавишу hello Windows ключ запуска, начните вводить ** Azure Cosmos DB эмулятор ** и выберите hello эмулятор из списка приложений hello](./media/local-emulator/database-local-emulator-start.png)

<span data-ttu-id="00a07-157">При запуске эмулятора hello, появится значок в области уведомлений панели задач Windows hello.</span><span class="sxs-lookup"><span data-stu-id="00a07-157">When hello emulator is running, you'll see an icon in hello Windows taskbar notification area.</span></span> ![Уведомление локального эмулятора Azure Cosmos DB на панели задач](./media/local-emulator/database-local-emulator-taskbar.png)

<span data-ttu-id="00a07-159">Hello Azure Cosmos DB эмулятор по умолчанию выполняется на hello локального компьютера («localhost») прослушивания по порту 8081.</span><span class="sxs-lookup"><span data-stu-id="00a07-159">hello Azure Cosmos DB Emulator by default runs on hello local machine ("localhost") listening on port 8081.</span></span>

<span data-ttu-id="00a07-160">Hello Cosmos DB эмулятор Azure установлен по умолчанию toohello `C:\Program Files\Azure Cosmos DB Emulator` каталога.</span><span class="sxs-lookup"><span data-stu-id="00a07-160">hello Azure Cosmos DB Emulator is installed by default toohello `C:\Program Files\Azure Cosmos DB Emulator` directory.</span></span> <span data-ttu-id="00a07-161">Можно также запустить и остановить hello эмулятор из командной строки hello.</span><span class="sxs-lookup"><span data-stu-id="00a07-161">You can also start and stop hello emulator from hello command-line.</span></span> <span data-ttu-id="00a07-162">Дополнительные сведения см. в [справочнике программы командной строки](#command-line).</span><span class="sxs-lookup"><span data-stu-id="00a07-162">See [command-line tool reference](#command-line) for more information.</span></span>

## <a name="start-data-explorer"></a><span data-ttu-id="00a07-163">Запуск обозревателя данных</span><span class="sxs-lookup"><span data-stu-id="00a07-163">Start Data Explorer</span></span>

<span data-ttu-id="00a07-164">При запуске эмулятора Azure Cosmos DB hello он автоматически открывается обозреватель данных Azure Cosmos DB hello в браузере.</span><span class="sxs-lookup"><span data-stu-id="00a07-164">When hello Azure Cosmos DB emulator launches it will automatically open hello Azure Cosmos DB Data Explorer in your browser.</span></span> <span data-ttu-id="00a07-165">Hello адрес будет отображаться как [https://localhost:8081/_explorer/index.html](https://localhost:8081/_explorer/index.html).</span><span class="sxs-lookup"><span data-stu-id="00a07-165">hello address will appear as [https://localhost:8081/_explorer/index.html](https://localhost:8081/_explorer/index.html).</span></span> <span data-ttu-id="00a07-166">Если закрыть hello обозревателя и хотите toore открыть его позже, можно открыть hello URL-адрес в браузере или запустите его из hello DB эмулятор Azure Cosmos в hello значок на панели задач Windows, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="00a07-166">If you close hello explorer and would like toore-open it later, you can either open hello URL in your browser or launch it from hello Azure Cosmos DB Emulator in hello Windows Tray Icon as shown below.</span></span>

![Запуск обозревателя данных из локального эмулятора Azure Cosmos DB](./media/local-emulator/database-local-emulator-data-explorer-launcher.png)

## <a name="checking-for-updates"></a><span data-ttu-id="00a07-168">Проверка наличия обновлений</span><span class="sxs-lookup"><span data-stu-id="00a07-168">Checking for updates</span></span>
<span data-ttu-id="00a07-169">Обозреватель данных сообщает о наличии нового обновления, доступного для скачивания.</span><span class="sxs-lookup"><span data-stu-id="00a07-169">Data Explorer indicates if there is a new update available for download.</span></span> 

> [!NOTE]
> <span data-ttu-id="00a07-170">Данные, созданные в одной версии hello Azure Cosmos DB эмулятор не гарантируется toobe доступны при использовании другой версии.</span><span class="sxs-lookup"><span data-stu-id="00a07-170">Data created in one version of hello Azure Cosmos DB Emulator is not guaranteed toobe accessible when using a different version.</span></span> <span data-ttu-id="00a07-171">Если требуется toopersist данных для долгосрочной hello, рекомендуется хранить их в базе данных Azure Cosmos учетной записи, а не в hello Azure Cosmos DB эмулятора.</span><span class="sxs-lookup"><span data-stu-id="00a07-171">If you need toopersist your data for hello long term, it is recommended that you store that data in an Azure Cosmos DB account, rather than in hello Azure Cosmos DB Emulator.</span></span> 

## <a name="authenticating-requests"></a><span data-ttu-id="00a07-172">Выполнение проверки подлинности запросов</span><span class="sxs-lookup"><span data-stu-id="00a07-172">Authenticating requests</span></span>
<span data-ttu-id="00a07-173">Так же, как с помощью DB Cosmos Azure в облаке hello каждого запроса, выполняемого для hello DB эмулятор Azure Cosmos должен пройти проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="00a07-173">Just as with Azure Cosmos DB in hello cloud, every request that you make against hello Azure Cosmos DB Emulator must be authenticated.</span></span> <span data-ttu-id="00a07-174">Hello эмулятор DB Cosmos Azure поддерживает фиксированной учетной записи и ключ хорошо известных проверки подлинности для проверки подлинности главного ключа.</span><span class="sxs-lookup"><span data-stu-id="00a07-174">hello Azure Cosmos DB Emulator supports a single fixed account and a well-known authentication key for master key authentication.</span></span> <span data-ttu-id="00a07-175">Эта учетная запись и ключ, hello единственные учетные данные для использования с hello Azure Cosmos DB эмулятора.</span><span class="sxs-lookup"><span data-stu-id="00a07-175">This account and key are hello only credentials permitted for use with hello Azure Cosmos DB Emulator.</span></span> <span data-ttu-id="00a07-176">К ним относятся:</span><span class="sxs-lookup"><span data-stu-id="00a07-176">They are:</span></span>

    Account name: localhost:<port>
    Account key: C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==

> [!NOTE]
> <span data-ttu-id="00a07-177">Hello главного ключа, поддерживаемые hello эмулятор DB Cosmos Azure предназначен только для использования с эмулятором hello.</span><span class="sxs-lookup"><span data-stu-id="00a07-177">hello master key supported by hello Azure Cosmos DB Emulator is intended for use only with hello emulator.</span></span> <span data-ttu-id="00a07-178">Учетная запись Azure Cosmos DB производства и ключ нельзя использовать с hello Azure Cosmos DB эмулятора.</span><span class="sxs-lookup"><span data-stu-id="00a07-178">You cannot use your production Azure Cosmos DB account and key with hello Azure Cosmos DB Emulator.</span></span> 

> [!NOTE] 
> <span data-ttu-id="00a07-179">После запуска эмулятора hello с hello параметр/KEY, затем использовать ключ создан hello вместо «C2y6yDjf5/R + ob0N8A7Cgv30VRDJIWEHLM + 4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw ==»</span><span class="sxs-lookup"><span data-stu-id="00a07-179">If you have started hello emulator with hello /Key option, then use hello generated key instead of "C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw=="</span></span>

<span data-ttu-id="00a07-180">Кроме того, точно так же как hello Azure Cosmos DB службы, hello эмулятор DB Cosmos Azure поддерживает только безопасный обмен данными через SSL.</span><span class="sxs-lookup"><span data-stu-id="00a07-180">Additionally, just as hello Azure Cosmos DB service, hello Azure Cosmos DB Emulator supports only secure communication via SSL.</span></span>

## <a name="running-hello-emulator-on-a-local-network"></a><span data-ttu-id="00a07-181">Запуск эмулятора hello в локальной сети</span><span class="sxs-lookup"><span data-stu-id="00a07-181">Running hello emulator on a local network</span></span>

<span data-ttu-id="00a07-182">Можно запустить эмулятор hello в локальной сети.</span><span class="sxs-lookup"><span data-stu-id="00a07-182">You can run hello emulator on a local network.</span></span> <span data-ttu-id="00a07-183">tooenable доступа к сети, укажите параметр /AllowNetworkAccess hello в hello [командной строки](#command-line-syntax), который также необходимо указать/Key = key_string или/keyfile = имя_файла.</span><span class="sxs-lookup"><span data-stu-id="00a07-183">tooenable network access, specify hello /AllowNetworkAccess option at hello [command line](#command-line-syntax), which also requires that you specify /Key=key_string or /KeyFile=file_name.</span></span> <span data-ttu-id="00a07-184">Можно использовать /GenKeyFile = toogenerate имя_файла файл с заранее случайный ключ.</span><span class="sxs-lookup"><span data-stu-id="00a07-184">You can use /GenKeyFile=file_name toogenerate a file with a random key upfront.</span></span>  <span data-ttu-id="00a07-185">Затем можно передать этот слишком/KeyFile = file_name или/KEY = contents_of_file.</span><span class="sxs-lookup"><span data-stu-id="00a07-185">Then you can pass that too/KeyFile=file_name or /Key=contents_of_file.</span></span>

<span data-ttu-id="00a07-186">tooenable доступа к сети для hello первый раз hello пользователь должен завершить работу эмулятора hello и удалите каталог данных hello эмулятор (C:\Users\user_name\AppData\Local\CosmosDBEmulator).</span><span class="sxs-lookup"><span data-stu-id="00a07-186">tooenable network access for hello first time hello user should shutdown hello emulator and delete hello emulator’s data directory (C:\Users\user_name\AppData\Local\CosmosDBEmulator).</span></span>

## <a name="developing-with-hello-emulator"></a><span data-ttu-id="00a07-187">Разработка с использованием эмулятора hello</span><span class="sxs-lookup"><span data-stu-id="00a07-187">Developing with hello Emulator</span></span>
<span data-ttu-id="00a07-188">После имеют hello Azure Cosmos DB эмулятор на рабочем столе, можно использовать любые поддерживаемые [Azure Cosmos DB SDK](documentdb-sdk-dotnet.md) или hello [Azure Cosmos DB REST API](/rest/api/documentdb/) toointeract с hello эмулятора.</span><span class="sxs-lookup"><span data-stu-id="00a07-188">Once you have hello Azure Cosmos DB Emulator running on your desktop, you can use any supported [Azure Cosmos DB SDK](documentdb-sdk-dotnet.md) or hello [Azure Cosmos DB REST API](/rest/api/documentdb/) toointeract with hello Emulator.</span></span> <span data-ttu-id="00a07-189">Hello DB эмулятор Azure Cosmos также включает встроенные обозреватель данных, которая позволяет создавать коллекции hello DocumentDB и представление и MongoDB API и редактировать документы без написания кода.</span><span class="sxs-lookup"><span data-stu-id="00a07-189">hello Azure Cosmos DB Emulator also includes a built-in Data Explorer that lets you create collections for hello DocumentDB and MongoDB APIs, and view and edit documents without writing any code.</span></span>   

    // Connect toohello Azure Cosmos DB Emulator running locally
    DocumentClient client = new DocumentClient(
        new Uri("https://localhost:8081"), 
        "C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==");

<span data-ttu-id="00a07-190">Если вы используете [Azure Cosmos DB поддержка протоколов для MongoDB](mongodb-introduction.md), используйте hello, следующая строка подключения:</span><span class="sxs-lookup"><span data-stu-id="00a07-190">If you're using [Azure Cosmos DB protocol support for MongoDB](mongodb-introduction.md), please use hello following connection string:</span></span>

    mongodb://localhost:C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==@localhost:10255/admin?ssl=true&3t.sslSelfSignedCerts=true

<span data-ttu-id="00a07-191">Можно использовать существующие средства, такие как [Azure DocumentDB Studio](https://github.com/mingaliu/DocumentDBStudio) tooconnect toohello DB эмулятор Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="00a07-191">You can use existing tools like [Azure DocumentDB Studio](https://github.com/mingaliu/DocumentDBStudio) tooconnect toohello Azure Cosmos DB Emulator.</span></span> <span data-ttu-id="00a07-192">Можно также перенести данные между hello эмулятор DB Cosmos Azure и службы Azure Cosmos DB hello, с помощью hello [средство переноса данных DB Cosmos Azure](https://github.com/azure/azure-documentdb-datamigrationtool).</span><span class="sxs-lookup"><span data-stu-id="00a07-192">You can also migrate data between hello Azure Cosmos DB Emulator and hello Azure Cosmos DB service using hello [Azure Cosmos DB Data Migration Tool](https://github.com/azure/azure-documentdb-datamigrationtool).</span></span>

> [!NOTE] 
> <span data-ttu-id="00a07-193">После запуска эмулятора hello с hello параметр/KEY, затем использовать ключ создан hello вместо «C2y6yDjf5/R + ob0N8A7Cgv30VRDJIWEHLM + 4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw ==»</span><span class="sxs-lookup"><span data-stu-id="00a07-193">If you have started hello emulator with hello /Key option, then use hello generated key instead of "C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw=="</span></span>

<span data-ttu-id="00a07-194">С использованием эмулятора Azure Cosmos DB hello, по умолчанию, можно создать коллекции too25 с одной секцией или секционированные коллекцию 1.</span><span class="sxs-lookup"><span data-stu-id="00a07-194">Using hello Azure Cosmos DB emulator, by default, you can create up too25 single partition collections or 1 partitioned collection.</span></span> <span data-ttu-id="00a07-195">Дополнительные сведения об изменении этого значения см. в разделе [значение hello PartitionCount](#set-partitioncount).</span><span class="sxs-lookup"><span data-stu-id="00a07-195">For more information about changing this value, see [Setting hello PartitionCount value](#set-partitioncount).</span></span>

## <a name="export-hello-ssl-certificate"></a><span data-ttu-id="00a07-196">Экспорт сертификата SSL hello</span><span class="sxs-lookup"><span data-stu-id="00a07-196">Export hello SSL certificate</span></span>

<span data-ttu-id="00a07-197">Языки .NET и toosecurely хранилище сертификатов Windows hello использования среды выполнения подключения локальный эмулятор Azure Cosmos DB toohello.</span><span class="sxs-lookup"><span data-stu-id="00a07-197">.NET languages and runtime use hello Windows Certificate Store toosecurely connect toohello Azure Cosmos DB local emulator.</span></span> <span data-ttu-id="00a07-198">Другие языки используют собственные методы для управления сертификатами и использования сертификатов.</span><span class="sxs-lookup"><span data-stu-id="00a07-198">Other languages have their own method of managing and using certificates.</span></span> <span data-ttu-id="00a07-199">Java поддерживает собственное [хранилище сертификатов](https://docs.oracle.com/cd/E19830-01/819-4712/ablqw/index.html), а Python применяет [оболочки сокетов](https://docs.python.org/2/library/ssl.html).</span><span class="sxs-lookup"><span data-stu-id="00a07-199">Java uses its own [certificate store](https://docs.oracle.com/cd/E19830-01/819-4712/ablqw/index.html) whereas Python uses [socket wrappers](https://docs.python.org/2/library/ssl.html).</span></span>

<span data-ttu-id="00a07-200">В порядке tooobtain toouse сертификат с языками и сред выполнения, которые интегрируются с hello хранилище сертификатов Windows вы должны tooexport его с помощью диспетчера сертификатов Windows hello.</span><span class="sxs-lookup"><span data-stu-id="00a07-200">In order tooobtain a certificate toouse with languages and runtimes that do not integrate with hello Windows Certificate Store you will need tooexport it using hello Windows Certificate Manager.</span></span> <span data-ttu-id="00a07-201">Вы можете запустить его, выполнив certlm.msc или следуйте инструкциям в разделе шаг за шагом hello [экспортировать сертификаты hello Azure Cosmos DB эмулятор](./local-emulator-export-ssl-certificates.md).</span><span class="sxs-lookup"><span data-stu-id="00a07-201">You can start it by running certlm.msc or follow hello step by step instructions in [Export hello Azure Cosmos DB Emulator Certificates](./local-emulator-export-ssl-certificates.md).</span></span> <span data-ttu-id="00a07-202">После запуска диспетчера сертификатов hello Привет открыть личные сертификаты, как показано ниже и экспорт hello сертификат с понятным именем hello «DocumentDBEmulatorCertificate» как Base64-кодировке x.509 (CER).</span><span class="sxs-lookup"><span data-stu-id="00a07-202">Once hello certificate manager is running, open hello Personal Certificates as shown below and export hello certificate with hello friendly name "DocumentDBEmulatorCertificate" as a BASE-64 encoded X.509 (.cer) file.</span></span>

![Сертификат SSL для эмулятора Azure Cosmos DB](./media/local-emulator/database-local-emulator-ssl_certificate.png)

<span data-ttu-id="00a07-204">сертификат X.509 Hello можно импортировать в хранилище сертификатов Java hello, следуя инструкциям hello [Добавление toohello сертификат, в хранилище сертификатов ЦС Java](https://docs.microsoft.com/azure/java-add-certificate-ca-store).</span><span class="sxs-lookup"><span data-stu-id="00a07-204">hello X.509 certificate can be imported into hello Java certificate store by following hello instructions in [Adding a Certificate toohello Java CA Certificates Store](https://docs.microsoft.com/azure/java-add-certificate-ca-store).</span></span> <span data-ttu-id="00a07-205">После импорта hello сертификат в хранилище сертификатов hello приложения Java и MongoDB будут может tooconnect toohello DB эмулятор Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="00a07-205">Once hello certificate is imported into hello certificate store, Java and MongoDB applications will be able tooconnect toohello Azure Cosmos DB Emulator.</span></span>

<span data-ttu-id="00a07-206">При подключении toohello эмулятор из Python и Node.js SDK, проверки SSL отключен.</span><span class="sxs-lookup"><span data-stu-id="00a07-206">When connecting toohello emulator from Python and Node.js SDKs, SSL verification is disabled.</span></span>

## <span data-ttu-id="00a07-207"><a id="command-line"></a>Справочник по программе командной строки</span><span class="sxs-lookup"><span data-stu-id="00a07-207"><a id="command-line"></a>Command-line tool reference</span></span>
<span data-ttu-id="00a07-208">Из места установки hello можно использовать toostart командной строки hello и остановки эмулятора hello, настройте параметры и выполнить другие операции.</span><span class="sxs-lookup"><span data-stu-id="00a07-208">From hello installation location, you can use hello command-line toostart and stop hello emulator, configure options, and perform other operations.</span></span>

### <a name="command-line-syntax"></a><span data-ttu-id="00a07-209">Синтаксис для командной строки</span><span class="sxs-lookup"><span data-stu-id="00a07-209">Command-line Syntax</span></span>

    CosmosDB.Emulator.exe [/Shutdown] [/DataPath] [/Port] [/MongoPort] [/DirectPorts] [/Key] [/EnableRateLimiting] [/DisableRateLimiting] [/NoUI] [/NoExplorer] [/?]

<span data-ttu-id="00a07-210">tooview hello список параметров, тип `CosmosDB.Emulator.exe /?` hello командной строки.</span><span class="sxs-lookup"><span data-stu-id="00a07-210">tooview hello list of options, type `CosmosDB.Emulator.exe /?` at hello command prompt.</span></span>

<table>
<tr>
  <td><span data-ttu-id="00a07-211"><strong>Параметр</strong></span><span class="sxs-lookup"><span data-stu-id="00a07-211"><strong>Option</strong></span></span></td>
  <td><span data-ttu-id="00a07-212"><strong>Описание</strong></span><span class="sxs-lookup"><span data-stu-id="00a07-212"><strong>Description</strong></span></span></td>
  <td><span data-ttu-id="00a07-213"><strong>Команда</strong></span><span class="sxs-lookup"><span data-stu-id="00a07-213"><strong>Command</strong></span></span></td>
  <td><span data-ttu-id="00a07-214"><strong>Аргументы</strong></span><span class="sxs-lookup"><span data-stu-id="00a07-214"><strong>Arguments</strong></span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="00a07-215">[Нет аргументов]</span><span class="sxs-lookup"><span data-stu-id="00a07-215">[No arguments]</span></span></td>
  <td><span data-ttu-id="00a07-216">Запускается hello Azure Cosmos DB эмулятора с параметрами по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="00a07-216">Starts up hello Azure Cosmos DB Emulator with default settings.</span></span></td>
  <td><span data-ttu-id="00a07-217">CosmosDB.Emulator.exe</span><span class="sxs-lookup"><span data-stu-id="00a07-217">CosmosDB.Emulator.exe</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="00a07-218">[Help]</span><span class="sxs-lookup"><span data-stu-id="00a07-218">[Help]</span></span></td>
  <td><span data-ttu-id="00a07-219">Отображает hello список поддерживаемых аргументов командной строки.</span><span class="sxs-lookup"><span data-stu-id="00a07-219">Displays hello list of supported command-line arguments.</span></span></td>
  <td><span data-ttu-id="00a07-220">CosmosDB.Emulator.exe /?</span><span class="sxs-lookup"><span data-stu-id="00a07-220">CosmosDB.Emulator.exe /?</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="00a07-221">Shutdown</span><span class="sxs-lookup"><span data-stu-id="00a07-221">Shutdown</span></span></td>
  <td><span data-ttu-id="00a07-222">Завершает работу эмулятора DB Cosmos Azure hello.</span><span class="sxs-lookup"><span data-stu-id="00a07-222">Shuts down hello Azure Cosmos DB Emulator.</span></span></td>
  <td><span data-ttu-id="00a07-223">CosmosDB.Emulator.exe /Shutdown</span><span class="sxs-lookup"><span data-stu-id="00a07-223">CosmosDB.Emulator.exe /Shutdown</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="00a07-224">DataPath</span><span class="sxs-lookup"><span data-stu-id="00a07-224">DataPath</span></span></td>
  <td><span data-ttu-id="00a07-225">Задает путь hello в toostore файлов данных.</span><span class="sxs-lookup"><span data-stu-id="00a07-225">Specifies hello path in which toostore data files.</span></span> <span data-ttu-id="00a07-226">Значение по умолчанию — %LocalAppdata%\CosmosDBEmulator.</span><span class="sxs-lookup"><span data-stu-id="00a07-226">Default is %LocalAppdata%\CosmosDBEmulator.</span></span></td>
  <td><span data-ttu-id="00a07-227">CosmosDB.Emulator.exe /DataPath=&lt;путь_к_данным&gt;</span><span class="sxs-lookup"><span data-stu-id="00a07-227">CosmosDB.Emulator.exe /DataPath=&lt;datapath&gt;</span></span></td>
  <td><span data-ttu-id="00a07-228">&lt;datapath&gt;: любой доступный путь</span><span class="sxs-lookup"><span data-stu-id="00a07-228">&lt;datapath&gt;: An accessible path</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="00a07-229">Порт</span><span class="sxs-lookup"><span data-stu-id="00a07-229">Port</span></span></td>
  <td><span data-ttu-id="00a07-230">Указывает toouse номера порта hello hello эмулятора.</span><span class="sxs-lookup"><span data-stu-id="00a07-230">Specifies hello port number toouse for hello emulator.</span></span>  <span data-ttu-id="00a07-231">Значение по умолчанию — 8081.</span><span class="sxs-lookup"><span data-stu-id="00a07-231">Default is 8081.</span></span></td>
  <td><span data-ttu-id="00a07-232">CosmosDB.Emulator.exe /Port=&lt;порт&gt;</span><span class="sxs-lookup"><span data-stu-id="00a07-232">CosmosDB.Emulator.exe /Port=&lt;port&gt;</span></span></td>
  <td><span data-ttu-id="00a07-233">&lt;port&gt;: один номер порта</span><span class="sxs-lookup"><span data-stu-id="00a07-233">&lt;port&gt;: Single port number</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="00a07-234">MongoPort</span><span class="sxs-lookup"><span data-stu-id="00a07-234">MongoPort</span></span></td>
  <td><span data-ttu-id="00a07-235">Указывает hello toouse номер порта для обеспечения совместимости MongoDB API.</span><span class="sxs-lookup"><span data-stu-id="00a07-235">Specifies hello port number toouse for MongoDB compatibility API.</span></span> <span data-ttu-id="00a07-236">Значение по умолчанию — 10255.</span><span class="sxs-lookup"><span data-stu-id="00a07-236">Default is 10255.</span></span></td>
  <td><span data-ttu-id="00a07-237">CosmosDB.Emulator.exe /MongoPort=&lt;порт_mongo&gt;</span><span class="sxs-lookup"><span data-stu-id="00a07-237">CosmosDB.Emulator.exe /MongoPort=&lt;mongoport&gt;</span></span></td>
  <td><span data-ttu-id="00a07-238">&lt;mongoport&gt;: один номер порта</span><span class="sxs-lookup"><span data-stu-id="00a07-238">&lt;mongoport&gt;: Single port number</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="00a07-239">DirectPorts</span><span class="sxs-lookup"><span data-stu-id="00a07-239">DirectPorts</span></span></td>
  <td><span data-ttu-id="00a07-240">Указывает toouse hello порты для прямого подключения.</span><span class="sxs-lookup"><span data-stu-id="00a07-240">Specifies hello ports toouse for direct connectivity.</span></span> <span data-ttu-id="00a07-241">По умолчанию это порты 10251, 10252, 10253, 10254.</span><span class="sxs-lookup"><span data-stu-id="00a07-241">Defaults are 10251,10252,10253,10254.</span></span></td>
  <td><span data-ttu-id="00a07-242">CosmosDB.Emulator.exe /DirectPorts:&lt;directports&gt;</span><span class="sxs-lookup"><span data-stu-id="00a07-242">CosmosDB.Emulator.exe /DirectPorts:&lt;directports&gt;</span></span></td>
  <td><span data-ttu-id="00a07-243">&lt;directports&gt;: разделенный запятыми список из 4 портов</span><span class="sxs-lookup"><span data-stu-id="00a07-243">&lt;directports&gt;: Comma-delimited list of 4 ports</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="00a07-244">Ключ</span><span class="sxs-lookup"><span data-stu-id="00a07-244">Key</span></span></td>
  <td><span data-ttu-id="00a07-245">Ключ авторизации для эмулятора hello.</span><span class="sxs-lookup"><span data-stu-id="00a07-245">Authorization key for hello emulator.</span></span> <span data-ttu-id="00a07-246">Ключ должен быть hello 64-разрядного вектора кодировку base-64.</span><span class="sxs-lookup"><span data-stu-id="00a07-246">Key must be hello base-64 encoding of a 64-byte vector.</span></span></td>
  <td><span data-ttu-id="00a07-247">CosmosDB.Emulator.exe /Key:&lt;ключ&gt;</span><span class="sxs-lookup"><span data-stu-id="00a07-247">CosmosDB.Emulator.exe /Key:&lt;key&gt;</span></span></td>
  <td><span data-ttu-id="00a07-248">&lt;ключ&gt;: ключ должен иметь кодировку base-64 hello 64-разрядного вектора</span><span class="sxs-lookup"><span data-stu-id="00a07-248">&lt;key&gt;: Key must be hello base-64 encoding of a 64-byte vector</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="00a07-249">EnableRateLimiting</span><span class="sxs-lookup"><span data-stu-id="00a07-249">EnableRateLimiting</span></span></td>
  <td><span data-ttu-id="00a07-250">Указывает, что ограничение частоты запросов включено.</span><span class="sxs-lookup"><span data-stu-id="00a07-250">Specifies that request rate limiting behavior is enabled.</span></span></td>
  <td><span data-ttu-id="00a07-251">CosmosDB.Emulator.exe /EnableRateLimiting</span><span class="sxs-lookup"><span data-stu-id="00a07-251">CosmosDB.Emulator.exe /EnableRateLimiting</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="00a07-252">DisableRateLimiting</span><span class="sxs-lookup"><span data-stu-id="00a07-252">DisableRateLimiting</span></span></td>
  <td><span data-ttu-id="00a07-253">Указывает, что ограничение частоты запросов отключено.</span><span class="sxs-lookup"><span data-stu-id="00a07-253">Specifies that request rate limiting behavior is disabled.</span></span></td>
  <td><span data-ttu-id="00a07-254">CosmosDB.Emulator.exe /DisableRateLimiting</span><span class="sxs-lookup"><span data-stu-id="00a07-254">CosmosDB.Emulator.exe /DisableRateLimiting</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="00a07-255">NoUI</span><span class="sxs-lookup"><span data-stu-id="00a07-255">NoUI</span></span></td>
  <td><span data-ttu-id="00a07-256">Больше не показывать эмулятор hello пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="00a07-256">Do not show hello emulator user interface.</span></span></td>
  <td><span data-ttu-id="00a07-257">CosmosDB.Emulator.exe /NoUI</span><span class="sxs-lookup"><span data-stu-id="00a07-257">CosmosDB.Emulator.exe /NoUI</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="00a07-258">NoExplorer</span><span class="sxs-lookup"><span data-stu-id="00a07-258">NoExplorer</span></span></td>
  <td><span data-ttu-id="00a07-259">Скрывает обозреватель документов при запуске.</span><span class="sxs-lookup"><span data-stu-id="00a07-259">Don't show document explorer on startup.</span></span></td>
  <td><span data-ttu-id="00a07-260">CosmosDB.Emulator.exe /NoExplorer</span><span class="sxs-lookup"><span data-stu-id="00a07-260">CosmosDB.Emulator.exe /NoExplorer</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="00a07-261">PartitionCount</span><span class="sxs-lookup"><span data-stu-id="00a07-261">PartitionCount</span></span></td>
  <td><span data-ttu-id="00a07-262">Указывает максимальное количество hello секционированных коллекций.</span><span class="sxs-lookup"><span data-stu-id="00a07-262">Specifies hello maximum number of partitioned collections.</span></span> <span data-ttu-id="00a07-263">В разделе [изменить номер hello коллекций](#set-partitioncount) для получения дополнительной информации.</span><span class="sxs-lookup"><span data-stu-id="00a07-263">See [Change hello number of collections](#set-partitioncount) for more information.</span></span></td>
  <td><span data-ttu-id="00a07-264">CosmosDB.Emulator.exe /PartitionCount=&lt;число_разделов&gt;</span><span class="sxs-lookup"><span data-stu-id="00a07-264">CosmosDB.Emulator.exe /PartitionCount=&lt;partitioncount&gt;</span></span></td>
  <td><span data-ttu-id="00a07-265">&lt;partitioncount&gt;: максимально допустимое количество односекционных коллекций.</span><span class="sxs-lookup"><span data-stu-id="00a07-265">&lt;partitioncount&gt;: Maximum number of allowed single partition collections.</span></span> <span data-ttu-id="00a07-266">Значение по умолчанию — 25.</span><span class="sxs-lookup"><span data-stu-id="00a07-266">Default is 25.</span></span> <span data-ttu-id="00a07-267">Максимально допустимое значение — 250.</span><span class="sxs-lookup"><span data-stu-id="00a07-267">Maximum allowed is 250.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="00a07-268">DefaultPartitionCount</span><span class="sxs-lookup"><span data-stu-id="00a07-268">DefaultPartitionCount</span></span></td>
  <td><span data-ttu-id="00a07-269">Указывает количество секций в секционированную коллекцию по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="00a07-269">Specifies hello default number of partitions for a partitioned collection.</span></span></td>
  <td><span data-ttu-id="00a07-270">CosmosDB.Emulator.exe /DefaultPartitionCount=&lt;defaultpartitioncount&gt;</span><span class="sxs-lookup"><span data-stu-id="00a07-270">CosmosDB.Emulator.exe /DefaultPartitionCount=&lt;defaultpartitioncount&gt;</span></span></td>
  <td><span data-ttu-id="00a07-271">&lt;defaultpartitioncount&gt; Значение по умолчанию — 25.</span><span class="sxs-lookup"><span data-stu-id="00a07-271">&lt;defaultpartitioncount&gt; Default is 25.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="00a07-272">AllowNetworkAccess</span><span class="sxs-lookup"><span data-stu-id="00a07-272">AllowNetworkAccess</span></span></td>
  <td><span data-ttu-id="00a07-273">Включает эмулятор toohello доступа по сети.</span><span class="sxs-lookup"><span data-stu-id="00a07-273">Enables access toohello emulator over a network.</span></span> <span data-ttu-id="00a07-274">Необходимо также передать/KEY =&lt;key_string&gt; или/keyfile =&lt;имя_файла&gt; tooenable доступа к сети.</span><span class="sxs-lookup"><span data-stu-id="00a07-274">You must also pass /Key=&lt;key_string&gt; or /KeyFile=&lt;file_name&gt; tooenable network access.</span></span></td>
  <td><span data-ttu-id="00a07-275">CosmosDB.Emulator.exe /AllowNetworkAccess /Key=&lt;строка_ключа&gt;</span><span class="sxs-lookup"><span data-stu-id="00a07-275">CosmosDB.Emulator.exe /AllowNetworkAccess /Key=&lt;key_string&gt;</span></span><br><br><span data-ttu-id="00a07-276">или</span><span class="sxs-lookup"><span data-stu-id="00a07-276">or</span></span><br><br><span data-ttu-id="00a07-277">CosmosDB.Emulator.exe /AllowNetworkAccess /KeyFile=&lt;имя_файла&gt;</span><span class="sxs-lookup"><span data-stu-id="00a07-277">CosmosDB.Emulator.exe /AllowNetworkAccess /KeyFile=&lt;file_name&gt;</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="00a07-278">NoFirewall</span><span class="sxs-lookup"><span data-stu-id="00a07-278">NoFirewall</span></span></td>
  <td><span data-ttu-id="00a07-279">Не изменять правила брандмауэра при использовании /AllowNetworkAccess.</span><span class="sxs-lookup"><span data-stu-id="00a07-279">Don't adjust firewall rules when /AllowNetworkAccess is used.</span></span></td>
  <td><span data-ttu-id="00a07-280">CosmosDB.Emulator.exe /NoFirewall</span><span class="sxs-lookup"><span data-stu-id="00a07-280">CosmosDB.Emulator.exe /NoFirewall</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="00a07-281">GenKeyFile</span><span class="sxs-lookup"><span data-stu-id="00a07-281">GenKeyFile</span></span></td>
  <td><span data-ttu-id="00a07-282">Создать новый ключ авторизации и сохраните toohello указанного файла.</span><span class="sxs-lookup"><span data-stu-id="00a07-282">Generate a new authorization key and save toohello specified file.</span></span> <span data-ttu-id="00a07-283">Hello созданный ключ может использоваться с hello/KEY или параметры/keyfile.</span><span class="sxs-lookup"><span data-stu-id="00a07-283">hello generated key can be used with hello /Key or /KeyFile options.</span></span></td>
  <td><span data-ttu-id="00a07-284">CosmosDB.Emulator.exe /GenKeyFile =&lt;tookey путь к файлу&gt;</span><span class="sxs-lookup"><span data-stu-id="00a07-284">CosmosDB.Emulator.exe  /GenKeyFile=&lt;path tookey file&gt;</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="00a07-285">Целостность</span><span class="sxs-lookup"><span data-stu-id="00a07-285">Consistency</span></span></td>
  <td><span data-ttu-id="00a07-286">Задайте уровень согласованности hello по умолчанию для учетной записи hello.</span><span class="sxs-lookup"><span data-stu-id="00a07-286">Set hello default consistency level for hello account.</span></span></td>
  <td><span data-ttu-id="00a07-287">CosmosDB.Emulator.exe /Consistency=&lt;consistency&gt;</span><span class="sxs-lookup"><span data-stu-id="00a07-287">CosmosDB.Emulator.exe /Consistency=&lt;consistency&gt;</span></span></td>
  <td><span data-ttu-id="00a07-288">&lt;согласованность&gt;: значение должно быть одним из следующих hello [уровни согласованности](consistency-levels.md): сеанс, Strong, Eventual или BoundedStaleness.</span><span class="sxs-lookup"><span data-stu-id="00a07-288">&lt;consistency&gt;: Value must be one of hello following [consistency levels](consistency-levels.md): Session, Strong, Eventual, or BoundedStaleness.</span></span>  <span data-ttu-id="00a07-289">значение по умолчанию Hello — сеанса.</span><span class="sxs-lookup"><span data-stu-id="00a07-289">hello default value is Session.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="00a07-290">?</span><span class="sxs-lookup"><span data-stu-id="00a07-290">?</span></span></td>
  <td><span data-ttu-id="00a07-291">Показать справочное сообщение hello.</span><span class="sxs-lookup"><span data-stu-id="00a07-291">Show hello help message.</span></span></td>
  <td></td>
  <td></td>
</tr>
</table>

## <a name="differences-between-hello-azure-cosmos-db-emulator-and-azure-cosmos-db"></a><span data-ttu-id="00a07-292">Различия между hello эмулятор DB Cosmos Azure и Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="00a07-292">Differences between hello Azure Cosmos DB Emulator and Azure Cosmos DB</span></span> 
<span data-ttu-id="00a07-293">Поскольку hello эмулятор DB Cosmos Azure предоставляет эмулированной среду на рабочей станции локальной разработчика, существуют функциональные различия между эмулятором hello и учетную запись Azure Cosmos DB в облаке hello:</span><span class="sxs-lookup"><span data-stu-id="00a07-293">Because hello Azure Cosmos DB Emulator provides an emulated environment running on a local developer workstation, there are some differences in functionality between hello emulator and an Azure Cosmos DB account in hello cloud:</span></span>

* <span data-ttu-id="00a07-294">Hello эмулятор DB Cosmos Azure поддерживает только одной предопределенной учетной записи и хорошо известных главного ключа.</span><span class="sxs-lookup"><span data-stu-id="00a07-294">hello Azure Cosmos DB Emulator supports only a single fixed account and a well-known master key.</span></span>  <span data-ttu-id="00a07-295">Повторное создание ключа невозможна в hello Azure Cosmos DB эмулятора.</span><span class="sxs-lookup"><span data-stu-id="00a07-295">Key regeneration is not possible in hello Azure Cosmos DB Emulator.</span></span>
* <span data-ttu-id="00a07-296">Hello Azure Cosmos DB эмулятора, не является масштабируемой службой и не будет поддерживать большого числа коллекций.</span><span class="sxs-lookup"><span data-stu-id="00a07-296">hello Azure Cosmos DB Emulator is not a scalable service and will not support a large number of collections.</span></span>
* <span data-ttu-id="00a07-297">Hello Azure Cosmos DB эмулятора не применяется для моделирования различных [уровни согласованности в базе данных Azure Cosmos](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="00a07-297">hello Azure Cosmos DB Emulator does not simulate different [Azure Cosmos DB consistency levels](consistency-levels.md).</span></span>
* <span data-ttu-id="00a07-298">Hello Azure Cosmos DB эмулятор не вполне [регионов репликации](distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="00a07-298">hello Azure Cosmos DB Emulator does not simulate [multi-region replication](distribute-data-globally.md).</span></span>
* <span data-ttu-id="00a07-299">Hello Azure Cosmos DB эмулятор не поддерживает переопределения квоты hello службы, доступные в службе Azure Cosmos DB hello (например ограничений на размер документа, повышенная секционированную коллекцию хранилища).</span><span class="sxs-lookup"><span data-stu-id="00a07-299">hello Azure Cosmos DB Emulator does not support hello service quota overrides that are available in hello Azure Cosmos DB service (e.g. document size limits, increased partitioned collection storage).</span></span>
* <span data-ttu-id="00a07-300">Как копию hello Azure Cosmos DB эмулятор может не быть вверх toodate с самых последних изменений hello со службой Azure Cosmos DB hello, пожалуйста, [планировщик ресурсов Azure Cosmos DB](https://www.documentdb.com/capacityplanner) tooaccurately оценки производства пропускной способности (RUs) требования вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="00a07-300">As your copy of hello Azure Cosmos DB Emulator might not be up toodate with hello most recent changes with hello Azure Cosmos DB service, please [Azure Cosmos DB capacity planner](https://www.documentdb.com/capacityplanner) tooaccurately estimate production throughput (RUs) needs of your application.</span></span>

## <span data-ttu-id="00a07-301"><a id="set-partitioncount"></a>Номер hello изменения коллекций</span><span class="sxs-lookup"><span data-stu-id="00a07-301"><a id="set-partitioncount"></a>Change hello number of collections</span></span>

<span data-ttu-id="00a07-302">По умолчанию можно создать коллекции с одной секцией too25 или коллекцию 1 секционированных hello Azure Cosmos DB эмулятора.</span><span class="sxs-lookup"><span data-stu-id="00a07-302">By default, you can create up too25 single partition collections, or 1 partitioned collection using hello Azure Cosmos DB Emulator.</span></span> <span data-ttu-id="00a07-303">Изменив hello **PartitionCount** значение, можно создать копию коллекции с одной секцией too250 или 10 секционированных коллекций или любое сочетание hello двух должен превышать 250 одной секции (где 1 секционированные Коллекция = 25 коллекция одной секции).</span><span class="sxs-lookup"><span data-stu-id="00a07-303">By modifying hello **PartitionCount** value, you can create up too250 single partition collections or 10 partitioned collections, or any combination of hello two that does not exceed 250 single partitions (where 1 partitioned collection = 25 single partition collection).</span></span>

<span data-ttu-id="00a07-304">При попытке toocreate коллекцию после превышения hello текущее количество разделов, эмулятор hello исключение ServiceUnavailable, с сообщением, hello.</span><span class="sxs-lookup"><span data-stu-id="00a07-304">If you attempt toocreate a collection after hello current partition count has been exceeded, hello emulator throws a ServiceUnavailable exception, with hello following message.</span></span>

    Sorry, we are currently experiencing high demand in this region, 
    and cannot fulfill your request at this time. We work continuously 
    toobring more and more capacity online, and encourage you tootry again. 
    Please do not hesitate tooemail docdbswat@microsoft.com at any time or 
    for any reason. ActivityId: 29da65cc-fba1-45f9-b82c-bf01d78a1f91

<span data-ttu-id="00a07-305">число доступных toohello коллекций эмулятор DB Cosmos Azure, hello toochange hello следующие:</span><span class="sxs-lookup"><span data-stu-id="00a07-305">toochange hello number of collections available toohello Azure Cosmos DB Emulator, do hello following:</span></span>

1. <span data-ttu-id="00a07-306">Удалить все локальные данные эмулятора DB Cosmos Azure щелкните правой кнопкой мыши hello **DB эмулятор Azure Cosmos** на hello в панели задач и выбрав значок **сброса данных...** .</span><span class="sxs-lookup"><span data-stu-id="00a07-306">Delete all local Azure Cosmos DB Emulator data by right-clicking hello **Azure Cosmos DB Emulator** icon on hello system tray, and then clicking **Reset Data…**.</span></span>
2. <span data-ttu-id="00a07-307">Удалите все данные эмулятора в этой папке: C:\Users\имя_пользователя\AppData\Local\CosmosDBEmulator.</span><span class="sxs-lookup"><span data-stu-id="00a07-307">Delete all emulator data in this folder C:\Users\user_name\AppData\Local\CosmosDBEmulator.</span></span>
3. <span data-ttu-id="00a07-308">Закройте все открытые экземпляры, щелкнув правой кнопкой мыши hello **DB эмулятор Azure Cosmos** на hello в панели задач и выбрав значок **выхода**.</span><span class="sxs-lookup"><span data-stu-id="00a07-308">Exit all open instances by right-clicking hello **Azure Cosmos DB Emulator** icon on hello system tray, and then clicking **Exit**.</span></span> <span data-ttu-id="00a07-309">Он может занять до минуты для всех экземпляров tooexit.</span><span class="sxs-lookup"><span data-stu-id="00a07-309">It may take a minute for all instances tooexit.</span></span>
4. <span data-ttu-id="00a07-310">Установите последнюю версию hello hello [DB эмулятор Azure Cosmos](https://aka.ms/cosmosdb-emulator).</span><span class="sxs-lookup"><span data-stu-id="00a07-310">Install hello latest version of hello [Azure Cosmos DB Emulator](https://aka.ms/cosmosdb-emulator).</span></span>
5. <span data-ttu-id="00a07-311">Запустите эмулятор hello с hello PartitionCount флаг, задав значение < = 250.</span><span class="sxs-lookup"><span data-stu-id="00a07-311">Launch hello emulator with hello PartitionCount flag by setting a value <= 250.</span></span> <span data-ttu-id="00a07-312">Например, `C:\Program Files\Azure CosmosDB Emulator>CosmosDB.Emulator.exe /PartitionCount=100`.</span><span class="sxs-lookup"><span data-stu-id="00a07-312">For example: `C:\Program Files\Azure CosmosDB Emulator>CosmosDB.Emulator.exe /PartitionCount=100`.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="00a07-313">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="00a07-313">Troubleshooting</span></span>

<span data-ttu-id="00a07-314">Используйте следующие советы toohelp устранения неполадок, которые могут возникнуть в эмулятор Azure Cosmos DB hello hello.</span><span class="sxs-lookup"><span data-stu-id="00a07-314">Use hello following tips toohelp troubleshoot issues you encounter with hello Azure Cosmos DB emulator:</span></span>

- <span data-ttu-id="00a07-315">Если вы установили новую версию эмулятора hello и возникли ошибки, убедитесь, что сброс данных.</span><span class="sxs-lookup"><span data-stu-id="00a07-315">If you installed a new version of hello Emulator and are experiencing errors, ensure you reset your data.</span></span> <span data-ttu-id="00a07-316">Данные можно восстановить, щелкнув правой кнопкой мыши значок эмулятора DB Cosmos Azure hello hello в панели задач, выберите команду восстановить данные...</span><span class="sxs-lookup"><span data-stu-id="00a07-316">You can reset your data by right-clicking hello Azure Cosmos DB Emulator icon on hello system tray, and then clicking Reset Data….</span></span> <span data-ttu-id="00a07-317">Если hello ошибок не устраняется, можно удалить и переустановить приложение hello.</span><span class="sxs-lookup"><span data-stu-id="00a07-317">If that does not fix hello errors, you can uninstall and reinstall hello app.</span></span> <span data-ttu-id="00a07-318">В разделе [удалить локальный эмулятор hello](#uninstall) инструкции.</span><span class="sxs-lookup"><span data-stu-id="00a07-318">See [Uninstall hello local emulator](#uninstall) for instructions.</span></span>

- <span data-ttu-id="00a07-319">В случае отказа эмулятор Azure Cosmos DB hello, собрать файлы дампа из папки c:\Users\user_name\AppData\Local\CrashDumps их сжатие и присоединить их по электронной почте tooan слишком[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="00a07-319">If hello Azure Cosmos DB emulator crashes, collect dump files from c:\Users\user_name\AppData\Local\CrashDumps folder, compress them, and attach them tooan email too[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span></span>

- <span data-ttu-id="00a07-320">При возникновении сбоев в CosmosDB.StartupEntryPoint.exe, выполните следующую команду из командной строки администратора hello:`lodctr /R`</span><span class="sxs-lookup"><span data-stu-id="00a07-320">If you experience crashes in CosmosDB.StartupEntryPoint.exe, run hello following command from an admin command prompt: `lodctr /R`</span></span> 

- <span data-ttu-id="00a07-321">Если возникнет проблема с подключением, [сбор файлов трассировки](#trace-files), их сжатие и присоединить их по электронной почте tooan слишком[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="00a07-321">If you encounter a connectivity issue, [collect trace files](#trace-files), compress them, and attach them tooan email too[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span></span>

- <span data-ttu-id="00a07-322">При получении **служба недоступна** сообщение, hello эмулятор может содержаться ошибка tooinitialize hello сетевой стек.</span><span class="sxs-lookup"><span data-stu-id="00a07-322">If you receive a **Service Unavailable** message, hello emulator might be failing tooinitialize hello network stack.</span></span> <span data-ttu-id="00a07-323">Проверьте toosee при наличии безопасности клиентских Pulse hello или Juniper сетей установленным клиентом, как их сетевые драйверы фильтра может стать причиной проблемы hello.</span><span class="sxs-lookup"><span data-stu-id="00a07-323">Check toosee if you have hello Pulse secure client or Juniper networks client installed, as their network filter drivers may cause hello problem.</span></span> <span data-ttu-id="00a07-324">Удаление фильтра сети сторонних драйверов, обычно устраняет ошибку hello.</span><span class="sxs-lookup"><span data-stu-id="00a07-324">Uninstalling third party network filter drivers typically fixes hello issue.</span></span>

### <span data-ttu-id="00a07-325"><a id="trace-files"></a>Сбор файлов трассировки</span><span class="sxs-lookup"><span data-stu-id="00a07-325"><a id="trace-files"></a>Collect trace files</span></span>

<span data-ttu-id="00a07-326">toocollect отладочной трассировки, запустите следующие команды из командной строки с правами администратора hello:</span><span class="sxs-lookup"><span data-stu-id="00a07-326">toocollect debugging traces, run hello following commands from an administrative command prompt:</span></span>

1. `cd /d "%ProgramFiles%\Azure Cosmos DB Emulator"`
2. <span data-ttu-id="00a07-327">`CosmosDB.Emulator.exe /shutdown`.</span><span class="sxs-lookup"><span data-stu-id="00a07-327">`CosmosDB.Emulator.exe /shutdown`.</span></span> <span data-ttu-id="00a07-328">Контрольное значение hello лоток toomake убедиться, что hello программы системного завершил работу, он может занять около минуты.</span><span class="sxs-lookup"><span data-stu-id="00a07-328">Watch hello system tray toomake sure hello program has shut down, it may take a minute.</span></span> <span data-ttu-id="00a07-329">Можно также просто щелкнуть **выхода** в интерфейсе пользователя эмулятор Azure Cosmos DB hello.</span><span class="sxs-lookup"><span data-stu-id="00a07-329">You can also just click **Exit** in hello Azure Cosmos DB emulator user interface.</span></span>
3. `CosmosDB.Emulator.exe /starttraces`
4. `CosmosDB.Emulator.exe`
5. <span data-ttu-id="00a07-330">Воспроизвести проблему hello.</span><span class="sxs-lookup"><span data-stu-id="00a07-330">Reproduce hello problem.</span></span> <span data-ttu-id="00a07-331">Если обозреватель данных не работают, требуется только toowait tooopen hello браузера для ошибки hello toocatch несколько секунд.</span><span class="sxs-lookup"><span data-stu-id="00a07-331">If Data Explorer is not working, you only need toowait for hello browser tooopen for a few seconds toocatch hello error.</span></span>
5. `CosmosDB.Emulator.exe /stoptraces`
6. <span data-ttu-id="00a07-332">Перейдите в слишком`%ProgramFiles%\Azure Cosmos DB Emulator` и найдите файл docdbemulator_000001.etl hello.</span><span class="sxs-lookup"><span data-stu-id="00a07-332">Navigate too`%ProgramFiles%\Azure Cosmos DB Emulator` and find hello docdbemulator_000001.etl file.</span></span>
7. <span data-ttu-id="00a07-333">Отправить ETL-файла hello, а также шаги по воспроизведению слишком[ askcosmosdb@microsoft.com ](mailto:askcosmosdb@microsoft.com) для отладки.</span><span class="sxs-lookup"><span data-stu-id="00a07-333">Send hello .etl file along with repro steps too[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com) for debugging.</span></span>

### <span data-ttu-id="00a07-334"><a id="uninstall"></a>Удалить локальный эмулятор hello</span><span class="sxs-lookup"><span data-stu-id="00a07-334"><a id="uninstall"></a>Uninstall hello local Emulator</span></span>

1. <span data-ttu-id="00a07-335">Закройте все открытые экземпляры hello локальный эмулятор, щелкнув правой кнопкой мыши значок эмулятора DB Cosmos Azure hello hello в панели задач, выберите команду выхода.</span><span class="sxs-lookup"><span data-stu-id="00a07-335">Exit all open instances of hello local Emulator by right-clicking hello Azure Cosmos DB Emulator icon on hello system tray, and then clicking Exit.</span></span> <span data-ttu-id="00a07-336">Он может занять до минуты для всех экземпляров tooexit.</span><span class="sxs-lookup"><span data-stu-id="00a07-336">It may take a minute for all instances tooexit.</span></span>
2. <span data-ttu-id="00a07-337">Введите в поле поиска Windows hello **приложений и возможности** и щелкнет hello **приложений и компонентов (системные параметры)** результат.</span><span class="sxs-lookup"><span data-stu-id="00a07-337">In hello Windows search box, type **Apps & features** and click on hello **Apps & features (System settings)** result.</span></span>
3. <span data-ttu-id="00a07-338">Hello приложений прокрутите список слишком**DB эмулятор Azure Cosmos**, выберите его, щелкните **удаления**, подтверждение и нажмите кнопку **удаления** еще раз.</span><span class="sxs-lookup"><span data-stu-id="00a07-338">In hello list of apps, scroll too**Azure Cosmos DB Emulator**, select it, click **Uninstall**, then confirm and click **Uninstall** again.</span></span>
4. <span data-ttu-id="00a07-339">При удалении приложения hello перейдите tooC:\Users\<пользователя > \AppData\Local\CosmosDBEmulator и удалить папку hello.</span><span class="sxs-lookup"><span data-stu-id="00a07-339">When hello app is uninstalled, navigate tooC:\Users\<user>\AppData\Local\CosmosDBEmulator and delete hello folder.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="00a07-340">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="00a07-340">Next steps</span></span>

<span data-ttu-id="00a07-341">В этом учебнике вы сделали hello следующее:</span><span class="sxs-lookup"><span data-stu-id="00a07-341">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="00a07-342">Установить локальный эмулятор hello</span><span class="sxs-lookup"><span data-stu-id="00a07-342">Installed hello local Emulator</span></span>
> * <span data-ttu-id="00a07-343">Функция RAND hello эмулятора на Docker для Windows</span><span class="sxs-lookup"><span data-stu-id="00a07-343">Rand hello Emulator on Docker for Windows</span></span>
> * <span data-ttu-id="00a07-344">выполнили аутентификацию запросов;</span><span class="sxs-lookup"><span data-stu-id="00a07-344">Authenticated requests</span></span>
> * <span data-ttu-id="00a07-345">Использовать hello обозреватель данных, в эмуляторе hello</span><span class="sxs-lookup"><span data-stu-id="00a07-345">Used hello Data Explorer in hello Emulator</span></span>
> * <span data-ttu-id="00a07-346">экспортировали сертификаты SSL;</span><span class="sxs-lookup"><span data-stu-id="00a07-346">Exported SSL certificates</span></span>
> * <span data-ttu-id="00a07-347">Вызывается из командной строки hello hello эмулятора</span><span class="sxs-lookup"><span data-stu-id="00a07-347">Called hello Emulator from hello command line</span></span>
> * <span data-ttu-id="00a07-348">собрали файлы трассировки.</span><span class="sxs-lookup"><span data-stu-id="00a07-348">Collected trace files</span></span>

<span data-ttu-id="00a07-349">В этом учебнике вы узнали, как toouse hello локальный эмулятор для свободной локальной разработки.</span><span class="sxs-lookup"><span data-stu-id="00a07-349">In this tutorial, you've learned how toouse hello local Emulator for free local development.</span></span> <span data-ttu-id="00a07-350">Теперь можно продолжить toohello следующее руководство и узнайте, как tooexport эмулятор SSL-сертификаты.</span><span class="sxs-lookup"><span data-stu-id="00a07-350">You can now proceed toohello next tutorial and learn how tooexport Emulator SSL certificates.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="00a07-351">Экспорт сертификатов DB эмулятор Azure Cosmos hello</span><span class="sxs-lookup"><span data-stu-id="00a07-351">Export hello Azure Cosmos DB Emulator certificates</span></span>](local-emulator-export-ssl-certificates.md)
