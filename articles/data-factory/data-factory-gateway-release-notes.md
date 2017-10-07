---
title: "заметки о aaaRelease для шлюза управления данными | Документы Microsoft"
description: "Заметки о выпуске шлюза управления данными"
services: data-factory
author: nabhishek
manager: jhubbard
editor: monicar
ms.assetid: 14762e82-76d9-41c4-ba9f-14a54da29c36
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: abnarain
published: True
ms.openlocfilehash: 3165d7537410a0531e0bb7f7fe584767f9155574
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="release-notes-for-data-management-gateway"></a><span data-ttu-id="0e1bc-103">Заметки о выпуске шлюза управления данными</span><span class="sxs-lookup"><span data-stu-id="0e1bc-103">Release notes for Data Management Gateway</span></span>
<span data-ttu-id="0e1bc-104">Одной из проблем hello для интеграции данных современных — toomove tooand данных из локальной toocloud.</span><span class="sxs-lookup"><span data-stu-id="0e1bc-104">One of hello challenges for modern data integration is toomove data tooand from on-premises toocloud.</span></span> <span data-ttu-id="0e1bc-105">Фабрика данных делает такая интеграция с шлюз управления данными, — это агент, что вы можете установить перенос гибридных данных локальной tooenable.</span><span class="sxs-lookup"><span data-stu-id="0e1bc-105">Data Factory makes this integration with Data Management Gateway, which is an agent that you can install on-premises tooenable hybrid data movement.</span></span>

<span data-ttu-id="0e1bc-106">См. следующие статьи подробные сведения о шлюзе управления данными hello и как toouse его:</span><span class="sxs-lookup"><span data-stu-id="0e1bc-106">See hello following articles for detailed information about Data Management Gateway and how toouse it:</span></span>

*  [<span data-ttu-id="0e1bc-107">Шлюз управления данными</span><span class="sxs-lookup"><span data-stu-id="0e1bc-107">Data Management Gateway</span></span>](data-factory-data-management-gateway.md)
*  [<span data-ttu-id="0e1bc-108">Перемещение данных между локальным и облачным хранилищами с помощью фабрики данных Azure</span><span class="sxs-lookup"><span data-stu-id="0e1bc-108">Move data between on-premises and cloud using Azure Data Factory</span></span>](data-factory-move-data-between-onprem-and-cloud.md)


## <a name="current-version-21063477"></a><span data-ttu-id="0e1bc-109">Текущая версия (2.10.6347.7)</span><span class="sxs-lookup"><span data-stu-id="0e1bc-109">CURRENT VERSION (2.10.6347.7)</span></span>

### <a name="enhancements-"></a><span data-ttu-id="0e1bc-110">Улучшения</span><span class="sxs-lookup"><span data-stu-id="0e1bc-110">Enhancements-</span></span>
- <span data-ttu-id="0e1bc-111">Можно добавить шины обслуживания toowhitelist записи DNS, а не список утвержденных всех IP-адресов Azure из брандмауэр (при необходимости).</span><span class="sxs-lookup"><span data-stu-id="0e1bc-111">You can add DNS entries toowhitelist service bus rather than whitelisting all Azure IP addresses from your firewall (if needed).</span></span> <span data-ttu-id="0e1bc-112">Соответствующие записи DNS можно найти на портале Azure, последовательно выбрав "Фабрика данных" -> "Создать и развернуть" -> "Шлюзы" -> serviceUrls (URL-адреса служб) (в формате JSON).</span><span class="sxs-lookup"><span data-stu-id="0e1bc-112">You can find respective DNS entry on Azure portal (Data Factory -> ‘Author and Deploy’ -> ‘Gateways’ -> "serviceUrls" (in JSON)</span></span>
- <span data-ttu-id="0e1bc-113">Соединитель HDFS теперь поддерживает открытый самозаверяющий сертификат, позволяя пропускать проверку SSL.</span><span class="sxs-lookup"><span data-stu-id="0e1bc-113">HDFS connector now supports self-signed public certificate by letting you skip SSL validation.</span></span>
- <span data-ttu-id="0e1bc-114">Исправлена ошибка: Проблема со шлюзом в автономный режим во время обновления (из-за tooclock наклон)</span><span class="sxs-lookup"><span data-stu-id="0e1bc-114">Fixed: Issue with gateway offline during update (due tooclock skew)</span></span>



## <a name="earlier-versions"></a><span data-ttu-id="0e1bc-115">Более ранние версии</span><span class="sxs-lookup"><span data-stu-id="0e1bc-115">Earlier versions</span></span>

## <a name="2963132"></a><span data-ttu-id="0e1bc-116">2.9.6313.2</span><span class="sxs-lookup"><span data-stu-id="0e1bc-116">2.9.6313.2</span></span>
### <a name="enhancements-"></a><span data-ttu-id="0e1bc-117">Улучшения</span><span class="sxs-lookup"><span data-stu-id="0e1bc-117">Enhancements-</span></span>
-   <span data-ttu-id="0e1bc-118">Можно добавить записи DNS toowhitelist Service Bus, а не список утвержденных всех IP-адресов Azure из брандмауэр (при необходимости).</span><span class="sxs-lookup"><span data-stu-id="0e1bc-118">You can add DNS entries toowhitelist Service Bus rather than whitelisting all Azure IP addresses from your firewall (if needed).</span></span> <span data-ttu-id="0e1bc-119">Здесь можно получить дополнительные сведения.</span><span class="sxs-lookup"><span data-stu-id="0e1bc-119">More details here.</span></span>
-   <span data-ttu-id="0e1bc-120">Вы можете скопировать данные из одного большого двоичного объекта вверх too4.75 ТБ, это hello max поддерживается размер блочного большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="0e1bc-120">You can now copy data to/from a single block blob up too4.75 TB, which is hello max supported size of block blob.</span></span> <span data-ttu-id="0e1bc-121">(Предыдущий лимит составлял 195 ГБ.)</span><span class="sxs-lookup"><span data-stu-id="0e1bc-121">(earlier limit was 195 GB).</span></span>
-   <span data-ttu-id="0e1bc-122">Исправлено. Проблема нехватки памяти при распаковке нескольких небольших файлов во время действия копирования.</span><span class="sxs-lookup"><span data-stu-id="0e1bc-122">Fixed: Out of memory issue while unzipping several small files during copy activity.</span></span>
-   <span data-ttu-id="0e1bc-123">Исправлена ошибка: Индекс вне допустимого диапазона проблемы при копировании из документа DB tooan локального SQL Server с помощью функции идемпотентности.</span><span class="sxs-lookup"><span data-stu-id="0e1bc-123">Fixed: Index out of range issue while copying from Document DB tooan on-premises SQL Server with idempotency feature.</span></span>
-   <span data-ttu-id="0e1bc-124">Исправлено. Скрипт очистки SQL не работал с локальным сервером SQL Server из мастера копирования.</span><span class="sxs-lookup"><span data-stu-id="0e1bc-124">Fixed: SQL cleanup script doesn't work with on-premises SQL Server from Copy Wizard.</span></span>
-   <span data-ttu-id="0e1bc-125">Исправлена ошибка: Имя столбца с пространством в конце hello не работает в действии копирования.</span><span class="sxs-lookup"><span data-stu-id="0e1bc-125">Fixed: Column name with space at hello end does not work in copy activity.</span></span>

## <a name="28662833"></a><span data-ttu-id="0e1bc-126">2.8.66283.3</span><span class="sxs-lookup"><span data-stu-id="0e1bc-126">2.8.66283.3</span></span>
### <a name="enhancements-"></a><span data-ttu-id="0e1bc-127">Улучшения</span><span class="sxs-lookup"><span data-stu-id="0e1bc-127">Enhancements-</span></span>
- <span data-ttu-id="0e1bc-128">Исправлено. Проблема отсутствия учетных данных при перезагрузке компьютера шлюза.</span><span class="sxs-lookup"><span data-stu-id="0e1bc-128">Fixed: Issue with missing credentials on gateway machine reboot.</span></span>
- <span data-ttu-id="0e1bc-129">Исправлено. Проблемы с регистрацией во время восстановления шлюза с помощью файла резервной копии.</span><span class="sxs-lookup"><span data-stu-id="0e1bc-129">Fixed: Issue with registration during gateway restore using a backup file.</span></span>


## <a name="2762401"></a><span data-ttu-id="0e1bc-130">2.7.6240.1</span><span class="sxs-lookup"><span data-stu-id="0e1bc-130">2.7.6240.1</span></span>
### <a name="enhancements-"></a><span data-ttu-id="0e1bc-131">Улучшения</span><span class="sxs-lookup"><span data-stu-id="0e1bc-131">Enhancements-</span></span>
- <span data-ttu-id="0e1bc-132">Исправлено. Неправильное считывание десятичного значения Null из источника Oracle.</span><span class="sxs-lookup"><span data-stu-id="0e1bc-132">Fixed: Incorrect read of Decimal null value from Oracle as source.</span></span>

## <a name="2661922"></a><span data-ttu-id="0e1bc-133">2.6.6192.2</span><span class="sxs-lookup"><span data-stu-id="0e1bc-133">2.6.6192.2</span></span>
### <a name="whats-new"></a><span data-ttu-id="0e1bc-134">Новые возможности</span><span class="sxs-lookup"><span data-stu-id="0e1bc-134">What’s new</span></span>
- <span data-ttu-id="0e1bc-135">Клиенты могут оставлять отзывы о регистрации шлюза.</span><span class="sxs-lookup"><span data-stu-id="0e1bc-135">Customers can provide feedback on gateway registering experience.</span></span>
- <span data-ttu-id="0e1bc-136">Поддерживается сжатие в формате ZIP (Deflate).</span><span class="sxs-lookup"><span data-stu-id="0e1bc-136">Support a new compression format: ZIP (Deflate)</span></span>

### <a name="enhancements-"></a><span data-ttu-id="0e1bc-137">Улучшения</span><span class="sxs-lookup"><span data-stu-id="0e1bc-137">Enhancements-</span></span>
- <span data-ttu-id="0e1bc-138">Повышение производительности приемника Oracle и источника HDFS.</span><span class="sxs-lookup"><span data-stu-id="0e1bc-138">Performance improvement for Oracle Sink, HDFS source.</span></span>
- <span data-ttu-id="0e1bc-139">Исправлена ошибка автоматического обновления шлюза и ошибка производительности при параллельной обработке шлюза.</span><span class="sxs-lookup"><span data-stu-id="0e1bc-139">Bug fix for gateway auto update, gateway parallel processing capacity.</span></span>


## <a name="2561641"></a><span data-ttu-id="0e1bc-140">2.5.6164.1</span><span class="sxs-lookup"><span data-stu-id="0e1bc-140">2.5.6164.1</span></span>
### <a name="enhancements"></a><span data-ttu-id="0e1bc-141">Улучшения</span><span class="sxs-lookup"><span data-stu-id="0e1bc-141">Enhancements</span></span>
- <span data-ttu-id="0e1bc-142">Улучшенная более надежное и шлюза регистрации качества-теперь может отслеживать состояние хода выполнения во время процесса регистрации шлюза hello, благодаря чему hello регистрации возникают отклика.</span><span class="sxs-lookup"><span data-stu-id="0e1bc-142">Improved and more robust Gateway registration experience- Now you can track progress status during hello Gateway registration process, which makes hello registration experience more responsive.</span></span>
- <span data-ttu-id="0e1bc-143">Улучшения в шлюз восстановления процесса - вы по-прежнему можно восстановить шлюз, даже если у вас hello шлюза файл резервной копии с этим обновлением.</span><span class="sxs-lookup"><span data-stu-id="0e1bc-143">Improvement in Gateway Restore Process- You can still recover gateway even if you do not have hello gateway backup file with this update.</span></span> <span data-ttu-id="0e1bc-144">Это потребует учетные данные связанной службы tooreset портале.</span><span class="sxs-lookup"><span data-stu-id="0e1bc-144">This would require you tooreset Linked Service credentials in Portal.</span></span>
- <span data-ttu-id="0e1bc-145">Исправление ошибок.</span><span class="sxs-lookup"><span data-stu-id="0e1bc-145">Bug fix.</span></span>

## <a name="2461511"></a><span data-ttu-id="0e1bc-146">2.4.6151.1</span><span class="sxs-lookup"><span data-stu-id="0e1bc-146">2.4.6151.1</span></span>

### <a name="whats-new"></a><span data-ttu-id="0e1bc-147">Новые возможности</span><span class="sxs-lookup"><span data-stu-id="0e1bc-147">What’s new</span></span>

- <span data-ttu-id="0e1bc-148">Теперь учетные данные источника данных можно хранить локально.</span><span class="sxs-lookup"><span data-stu-id="0e1bc-148">You can now store data source credentials locally.</span></span> <span data-ttu-id="0e1bc-149">Hello учетные данные шифруются.</span><span class="sxs-lookup"><span data-stu-id="0e1bc-149">hello credentials are encrypted.</span></span> <span data-ttu-id="0e1bc-150">Hello учетные данные источника данных можно восстановить и восстановить с помощью файла резервной копии hello, можно экспортировать из существующего шлюза, всех локальных hello.</span><span class="sxs-lookup"><span data-stu-id="0e1bc-150">hello data source credentials can be recovered and restored using hello backup file that can be exported from hello existing Gateway, all on-premises.</span></span>

### <a name="enhancements-"></a><span data-ttu-id="0e1bc-151">Улучшения</span><span class="sxs-lookup"><span data-stu-id="0e1bc-151">Enhancements-</span></span>

- <span data-ttu-id="0e1bc-152">Улучшенный и более надежный процесс регистрации шлюза.</span><span class="sxs-lookup"><span data-stu-id="0e1bc-152">Improved and more robust Gateway registration experience.</span></span>
- <span data-ttu-id="0e1bc-153">Поддержка автоматического определения конфигурации QuoteChar текстовом формате в мастер копирования и улучшения hello в целом форматирования точность обнаружения.</span><span class="sxs-lookup"><span data-stu-id="0e1bc-153">Support auto detection of QuoteChar configuration for Text format in copy wizard, and improve hello overall format detection accuracy.</span></span>

## <a name="2361002"></a><span data-ttu-id="0e1bc-154">2.3.6100.2</span><span class="sxs-lookup"><span data-stu-id="0e1bc-154">2.3.6100.2</span></span>

- <span data-ttu-id="0e1bc-155">Добавлена поддержка автоматического обнаружения конфигурации firstRowAsHeader и SkipLineCount в мастере копирования для текстовых файлов в локальной файловой системе и HDFS.</span><span class="sxs-lookup"><span data-stu-id="0e1bc-155">Support firstRowAsHeader and SkipLineCount auto detection in copy wizard for text files in on-premises File system and HDFS.</span></span>
- <span data-ttu-id="0e1bc-156">Улучшения стабильности hello сетевое подключение между шлюзом и Service Bus</span><span class="sxs-lookup"><span data-stu-id="0e1bc-156">Enhance hello stability of network connection between gateway and Service Bus</span></span>
- <span data-ttu-id="0e1bc-157">Исправления ошибок</span><span class="sxs-lookup"><span data-stu-id="0e1bc-157">A few bug fixes</span></span>


## <a name="2260721"></a><span data-ttu-id="0e1bc-158">2.2.6072.1</span><span class="sxs-lookup"><span data-stu-id="0e1bc-158">2.2.6072.1</span></span>

*  <span data-ttu-id="0e1bc-159">Поддерживает настройку прокси-сервер HTTP для hello шлюза с помощью диспетчера конфигурации шлюза hello.</span><span class="sxs-lookup"><span data-stu-id="0e1bc-159">Supports setting HTTP proxy for hello gateway using hello Gateway Configuration Manager.</span></span> <span data-ttu-id="0e1bc-160">При наличии данной настройки доступ к большим двоичным объектам Azure, таблицам Azure, Azure Data Lake и Document DB осуществляется через HTTP-прокси.</span><span class="sxs-lookup"><span data-stu-id="0e1bc-160">If configured, Azure Blob, Azure Table, Azure Data Lake, and Document DB are accessed through HTTP proxy.</span></span>
*  <span data-ttu-id="0e1bc-161">Заголовок поддерживает обработку TextFormat при копировании данных из локальной файловой системе tooAzure больших двоичных объектов, хранилище Озера данных Azure и локальной HDFS.</span><span class="sxs-lookup"><span data-stu-id="0e1bc-161">Supports header handling for TextFormat when copying data from/tooAzure Blob, Azure Data Lake Store, on-premises File System, and on-premises HDFS.</span></span>
*  <span data-ttu-id="0e1bc-162">Поддерживает копирование данных из Append больших двоичных объектов и страничного большого двоичного объекта вместе с hello уже поддерживается блочного большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="0e1bc-162">Supports copying data from Append Blob and Page Blob along with hello already supported Block Blob.</span></span>
*  <span data-ttu-id="0e1bc-163">Вводит новое состояние шлюза **Online (с ограничениями)**, указывающая, что hello основную функциональность шлюза hello работает за исключением hello интерактивная операция поддержка мастера копирования.</span><span class="sxs-lookup"><span data-stu-id="0e1bc-163">Introduces a new gateway status **Online (Limited)**, which indicates that hello main functionality of hello gateway works except hello interactive operation support for Copy Wizard.</span></span>
*  <span data-ttu-id="0e1bc-164">Повышает надежность hello регистрации шлюза, с помощью ключа регистрации.</span><span class="sxs-lookup"><span data-stu-id="0e1bc-164">Enhances hello robustness of gateway registration using registration key.</span></span>

## <a name="216040"></a><span data-ttu-id="0e1bc-165">2.1.6040.</span><span class="sxs-lookup"><span data-stu-id="0e1bc-165">2.1.6040.</span></span>

*  <span data-ttu-id="0e1bc-166">Драйвер DB2 теперь входит в пакет установки шлюза hello.</span><span class="sxs-lookup"><span data-stu-id="0e1bc-166">DB2 driver is included in hello gateway installation package now.</span></span> <span data-ttu-id="0e1bc-167">Нет необходимости tooinstall его отдельно.</span><span class="sxs-lookup"><span data-stu-id="0e1bc-167">You do not need tooinstall it separately.</span></span>
*  <span data-ttu-id="0e1bc-168">Теперь драйвер для DB2 поддерживает z/OS и DB2 для i (AS / 400) вместе с hello уже поддерживаемые платформы (Linux, Unix и Windows).</span><span class="sxs-lookup"><span data-stu-id="0e1bc-168">DB2 driver now supports z/OS and DB2 for i (AS/400) along with hello platforms already supported (Linux, Unix, and Windows).</span></span>
*  <span data-ttu-id="0e1bc-169">Поддержка использования Azure Cosmos DB в качестве источника или назначения для локальных хранилищ данных.</span><span class="sxs-lookup"><span data-stu-id="0e1bc-169">Supports using Azure Cosmos DB as a source or destination for on-premises data stores</span></span>
*  <span data-ttu-id="0e1bc-170">Поддерживает копирование данных большого двоичного объекта из/toocold/горячей хранилище, а также hello уже поддерживается учетной записи хранения общего назначения.</span><span class="sxs-lookup"><span data-stu-id="0e1bc-170">Supports copying data from/toocold/hot blob storage along with hello already supported general-purpose storage account.</span></span>
*  <span data-ttu-id="0e1bc-171">Позволяет вам tooconnect tooon локальный SQL Server через шлюз с правами удаленного имени входа.</span><span class="sxs-lookup"><span data-stu-id="0e1bc-171">Allows you tooconnect tooon-premises SQL Server via gateway with remote login privileges.</span></span>  

## <a name="2060131"></a><span data-ttu-id="0e1bc-172">2.0.6013.1</span><span class="sxs-lookup"><span data-stu-id="0e1bc-172">2.0.6013.1</span></span>

*  <span data-ttu-id="0e1bc-173">Вы можете выбрать toobe hello язык и региональные параметры, используемые шлюз во время ручной установки.</span><span class="sxs-lookup"><span data-stu-id="0e1bc-173">You can select hello language/culture toobe used by a gateway during manual installation.</span></span>

*  <span data-ttu-id="0e1bc-174">Шлюз не работает должным образом, можно toosend журналы шлюза последние семь дней tooMicrosoft toofacilitate по устранению неполадок hello проблемы.</span><span class="sxs-lookup"><span data-stu-id="0e1bc-174">When gateway does not work as expected, you can choose toosend gateway logs of last seven days tooMicrosoft toofacilitate troubleshooting of hello issue.</span></span> <span data-ttu-id="0e1bc-175">Если шлюз не подключен toohello облачной службы, можно выбрать toosave и архивирование журналов шлюза.</span><span class="sxs-lookup"><span data-stu-id="0e1bc-175">If gateway is not connected toohello cloud service, you can choose toosave and archive gateway logs.</span></span>  

*  <span data-ttu-id="0e1bc-176">Улучшения пользовательского интерфейса диспетчера конфигурации шлюза:</span><span class="sxs-lookup"><span data-stu-id="0e1bc-176">User interface improvements for gateway configuration manager:</span></span>

    *  <span data-ttu-id="0e1bc-177">Нагляднее состояние шлюза на вкладке "Главная" hello.</span><span class="sxs-lookup"><span data-stu-id="0e1bc-177">Make gateway status more visible on hello Home tab.</span></span>

    *  <span data-ttu-id="0e1bc-178">Элементы управления реорганизованы и упрощены.</span><span class="sxs-lookup"><span data-stu-id="0e1bc-178">Reorganized and simplified controls.</span></span>

    *  <span data-ttu-id="0e1bc-179">Можно скопировать данные из хранилища, используя hello [средство предварительного просмотра копирование без кода](data-factory-copy-data-wizard-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="0e1bc-179">You can copy data from a storage using hello [code-free copy preview tool](data-factory-copy-data-wizard-tutorial.md).</span></span> <span data-ttu-id="0e1bc-180">В разделе [Промежуточное копирование](data-factory-copy-activity-performance.md#staged-copy) приведены общие сведения об этой функции.</span><span class="sxs-lookup"><span data-stu-id="0e1bc-180">See [Staged Copy](data-factory-copy-activity-performance.md#staged-copy) for details about this feature in general.</span></span>
*  <span data-ttu-id="0e1bc-181">Шлюз управления данными tooingress данных непосредственно из базы данных SQL Server в локальной среде можно использовать в машинном обучении Azure.</span><span class="sxs-lookup"><span data-stu-id="0e1bc-181">You can use Data Management Gateway tooingress data directly from an on-premises SQL Server database into Azure Machine Learning.</span></span>

*  <span data-ttu-id="0e1bc-182">Повышение производительности.</span><span class="sxs-lookup"><span data-stu-id="0e1bc-182">Performance improvements</span></span>

    * <span data-ttu-id="0e1bc-183">Повысьте производительность при просмотре схемы или предварительном просмотре данных SQL Server с помощью инструмента копирования с предварительным просмотром, не требующего программирования.</span><span class="sxs-lookup"><span data-stu-id="0e1bc-183">Improve performance on viewing Schema/Preview against SQL Server in code-free copy preview tool.</span></span>

## <a name="11259531"></a><span data-ttu-id="0e1bc-184">1.12.5953.1</span><span class="sxs-lookup"><span data-stu-id="0e1bc-184">1.12.5953.1</span></span>

*  <span data-ttu-id="0e1bc-185">Исправления ошибок</span><span class="sxs-lookup"><span data-stu-id="0e1bc-185">Bug fixes</span></span>

## <a name="11159181"></a><span data-ttu-id="0e1bc-186">1.11.5918.1</span><span class="sxs-lookup"><span data-stu-id="0e1bc-186">1.11.5918.1</span></span>

*  <span data-ttu-id="0e1bc-187">Максимальный размер журнала событий шлюза hello был увеличен с 1 МБ too40 МБ.</span><span class="sxs-lookup"><span data-stu-id="0e1bc-187">Maximum size of hello gateway event log has been increased from 1 MB too40 MB.</span></span>

*  <span data-ttu-id="0e1bc-188">Если во время автоматического обновления шлюза требуется перезагрузка, отображается диалоговое окно с предупреждением.</span><span class="sxs-lookup"><span data-stu-id="0e1bc-188">A warning dialog is displayed in case a restart is needed during gateway auto-update.</span></span> <span data-ttu-id="0e1bc-189">Затем или более поздней версии, вы можете toorestart справа.</span><span class="sxs-lookup"><span data-stu-id="0e1bc-189">You can choose toorestart right then or later.</span></span>

*  <span data-ttu-id="0e1bc-190">При сбое автоматического обновления установщик шлюза пытается выполнить автоматическое обновление не больше трех раз.</span><span class="sxs-lookup"><span data-stu-id="0e1bc-190">In case auto-update fails, gateway installer retries auto-updating three times at maximum.</span></span>

*  <span data-ttu-id="0e1bc-191">Повышение производительности.</span><span class="sxs-lookup"><span data-stu-id="0e1bc-191">Performance improvements</span></span>

    * <span data-ttu-id="0e1bc-192">Повышена эффективность загрузки больших таблиц из локального сервера в сценарий копирования без кода.</span><span class="sxs-lookup"><span data-stu-id="0e1bc-192">Improve performance for loading large tables from on-premises server in code-free copy scenario.</span></span>

*  <span data-ttu-id="0e1bc-193">Исправления ошибок</span><span class="sxs-lookup"><span data-stu-id="0e1bc-193">Bug fixes</span></span>

## <a name="11058921"></a><span data-ttu-id="0e1bc-194">1.10.5892.1</span><span class="sxs-lookup"><span data-stu-id="0e1bc-194">1.10.5892.1</span></span>

*  <span data-ttu-id="0e1bc-195">Повышение производительности.</span><span class="sxs-lookup"><span data-stu-id="0e1bc-195">Performance improvements</span></span>

*  <span data-ttu-id="0e1bc-196">Исправления ошибок</span><span class="sxs-lookup"><span data-stu-id="0e1bc-196">Bug fixes</span></span>

## <a name="1958652"></a><span data-ttu-id="0e1bc-197">1.9.5865.2</span><span class="sxs-lookup"><span data-stu-id="0e1bc-197">1.9.5865.2</span></span>

*  <span data-ttu-id="0e1bc-198">Полностью автоматическое обновление.</span><span class="sxs-lookup"><span data-stu-id="0e1bc-198">Zero touch auto update capability</span></span>
*  <span data-ttu-id="0e1bc-199">Новый значок на панели задач, позволяющий просматривать индикаторы состояния шлюза.</span><span class="sxs-lookup"><span data-stu-id="0e1bc-199">New tray icon with gateway status indicators</span></span>
*  <span data-ttu-id="0e1bc-200">Возможность слишком «обновить» от клиента hello</span><span class="sxs-lookup"><span data-stu-id="0e1bc-200">Ability too“Update now” from hello client</span></span>
*  <span data-ttu-id="0e1bc-201">В расписании tooset возможность обновления</span><span class="sxs-lookup"><span data-stu-id="0e1bc-201">Ability tooset update schedule time</span></span>
*  <span data-ttu-id="0e1bc-202">Включение и выключение автоматического обновления с использованием сценария PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0e1bc-202">PowerShell script for toggling auto-update on/off</span></span>
*  <span data-ttu-id="0e1bc-203">Поддержка формата JSON</span><span class="sxs-lookup"><span data-stu-id="0e1bc-203">Support for JSON format</span></span>  
*  <span data-ttu-id="0e1bc-204">Повышение производительности.</span><span class="sxs-lookup"><span data-stu-id="0e1bc-204">Performance improvements</span></span>
*  <span data-ttu-id="0e1bc-205">Исправления ошибок</span><span class="sxs-lookup"><span data-stu-id="0e1bc-205">Bug fixes</span></span>

## <a name="1858221"></a><span data-ttu-id="0e1bc-206">1.8.5822.1</span><span class="sxs-lookup"><span data-stu-id="0e1bc-206">1.8.5822.1</span></span>

*  <span data-ttu-id="0e1bc-207">Улучшение возможностей устранения неполадок.</span><span class="sxs-lookup"><span data-stu-id="0e1bc-207">Improve troubleshooting experience</span></span>
*  <span data-ttu-id="0e1bc-208">Повышение производительности.</span><span class="sxs-lookup"><span data-stu-id="0e1bc-208">Performance improvements</span></span>
*  <span data-ttu-id="0e1bc-209">Исправления ошибок</span><span class="sxs-lookup"><span data-stu-id="0e1bc-209">Bug fixes</span></span>

### <a name="1757951"></a><span data-ttu-id="0e1bc-210">1.7.5795.1</span><span class="sxs-lookup"><span data-stu-id="0e1bc-210">1.7.5795.1</span></span>

*  <span data-ttu-id="0e1bc-211">Повышение производительности.</span><span class="sxs-lookup"><span data-stu-id="0e1bc-211">Performance improvements</span></span>
*  <span data-ttu-id="0e1bc-212">Исправления ошибок</span><span class="sxs-lookup"><span data-stu-id="0e1bc-212">Bug fixes</span></span>

### <a name="1757641"></a><span data-ttu-id="0e1bc-213">1.7.5764.1</span><span class="sxs-lookup"><span data-stu-id="0e1bc-213">1.7.5764.1</span></span>

*  <span data-ttu-id="0e1bc-214">Повышение производительности.</span><span class="sxs-lookup"><span data-stu-id="0e1bc-214">Performance improvements</span></span>
*  <span data-ttu-id="0e1bc-215">Исправления ошибок</span><span class="sxs-lookup"><span data-stu-id="0e1bc-215">Bug fixes</span></span>

### <a name="1657351"></a><span data-ttu-id="0e1bc-216">1.6.5735.1</span><span class="sxs-lookup"><span data-stu-id="0e1bc-216">1.6.5735.1</span></span>

*  <span data-ttu-id="0e1bc-217">Поддержка локальной системы HDFS для источника и приемника.</span><span class="sxs-lookup"><span data-stu-id="0e1bc-217">Support on-premises HDFS Source/Sink</span></span>
*  <span data-ttu-id="0e1bc-218">Повышение производительности.</span><span class="sxs-lookup"><span data-stu-id="0e1bc-218">Performance improvements</span></span>
*  <span data-ttu-id="0e1bc-219">Исправления ошибок</span><span class="sxs-lookup"><span data-stu-id="0e1bc-219">Bug fixes</span></span>

### <a name="1656961"></a><span data-ttu-id="0e1bc-220">1.6.5696.1</span><span class="sxs-lookup"><span data-stu-id="0e1bc-220">1.6.5696.1</span></span>

*  <span data-ttu-id="0e1bc-221">Повышение производительности.</span><span class="sxs-lookup"><span data-stu-id="0e1bc-221">Performance improvements</span></span>
*  <span data-ttu-id="0e1bc-222">Исправления ошибок</span><span class="sxs-lookup"><span data-stu-id="0e1bc-222">Bug fixes</span></span>

### <a name="1656761"></a><span data-ttu-id="0e1bc-223">1.6.5676.1</span><span class="sxs-lookup"><span data-stu-id="0e1bc-223">1.6.5676.1</span></span>

*  <span data-ttu-id="0e1bc-224">Поддержка средств диагностики в диспетчере конфигурации.</span><span class="sxs-lookup"><span data-stu-id="0e1bc-224">Support diagnostic tools on Configuration Manager</span></span>
*  <span data-ttu-id="0e1bc-225">Поддержка столбцов источников табличных данных для фабрики данных Azure.</span><span class="sxs-lookup"><span data-stu-id="0e1bc-225">Support table columns for tabular data sources for Azure Data Factory</span></span>
*  <span data-ttu-id="0e1bc-226">Поддержка хранилища данных SQL для фабрики данных Azure.</span><span class="sxs-lookup"><span data-stu-id="0e1bc-226">Support SQL DW for Azure Data Factory</span></span>
*  <span data-ttu-id="0e1bc-227">Поддержка свойства reclusive в BlobSource и FileSource для фабрики данных Azure.</span><span class="sxs-lookup"><span data-stu-id="0e1bc-227">Support Reclusive in BlobSource and FileSource for Azure Data Factory</span></span>
*  <span data-ttu-id="0e1bc-228">Поддержка значений MergeFiles, PreserveHierarchy и FlattenHierarchy свойства copyBehavior в BlobSink и FileSink для двоичного копирования в фабрике данных Azure.</span><span class="sxs-lookup"><span data-stu-id="0e1bc-228">Support CopyBehavior – MergeFiles, PreserveHierarchy, and FlattenHierarchy in BlobSink and FileSink with Binary Copy for Azure Data Factory</span></span>
*  <span data-ttu-id="0e1bc-229">Поддержка сообщения о ходе выполнения действия копирования в фабрике данных Azure.</span><span class="sxs-lookup"><span data-stu-id="0e1bc-229">Support Copy Activity reporting progress for Azure Data Factory</span></span>
*  <span data-ttu-id="0e1bc-230">Поддержка проверки подключения к источнику данных в фабрике данных Azure.</span><span class="sxs-lookup"><span data-stu-id="0e1bc-230">Support Data Source Connectivity Validation for Azure Data Factory</span></span>
*  <span data-ttu-id="0e1bc-231">Исправления ошибок</span><span class="sxs-lookup"><span data-stu-id="0e1bc-231">Bug fixes</span></span>

### <a name="1656721"></a><span data-ttu-id="0e1bc-232">1.6.5672.1</span><span class="sxs-lookup"><span data-stu-id="0e1bc-232">1.6.5672.1</span></span>

*  <span data-ttu-id="0e1bc-233">Поддержка задания имени таблицы для источника данных ODBC в фабрике данных Azure</span><span class="sxs-lookup"><span data-stu-id="0e1bc-233">Support table name for ODBC data source for Azure Data Factory</span></span>
*  <span data-ttu-id="0e1bc-234">Повышение производительности.</span><span class="sxs-lookup"><span data-stu-id="0e1bc-234">Performance improvements</span></span>
*  <span data-ttu-id="0e1bc-235">Исправления ошибок</span><span class="sxs-lookup"><span data-stu-id="0e1bc-235">Bug fixes</span></span>

### <a name="1656581"></a><span data-ttu-id="0e1bc-236">1.6.5658.1</span><span class="sxs-lookup"><span data-stu-id="0e1bc-236">1.6.5658.1</span></span>

*  <span data-ttu-id="0e1bc-237">Поддержка FileSink для фабрики данных Azure.</span><span class="sxs-lookup"><span data-stu-id="0e1bc-237">Support File Sink for Azure Data Factory</span></span>
*  <span data-ttu-id="0e1bc-238">Поддержка сохранения иерархии при двоичном копировании в фабрике данных Azure.</span><span class="sxs-lookup"><span data-stu-id="0e1bc-238">Support preserving hierarchy in binary copy for Azure Data Factory</span></span>
*  <span data-ttu-id="0e1bc-239">Поддержка идемпотентности действия копирования в фабрике данных Azure.</span><span class="sxs-lookup"><span data-stu-id="0e1bc-239">Support Copy Activity Idempotency for Azure Data Factory</span></span>
*  <span data-ttu-id="0e1bc-240">Исправления ошибок</span><span class="sxs-lookup"><span data-stu-id="0e1bc-240">Bug fixes</span></span>

### <a name="1656401"></a><span data-ttu-id="0e1bc-241">1.6.5640.1</span><span class="sxs-lookup"><span data-stu-id="0e1bc-241">1.6.5640.1</span></span>

*  <span data-ttu-id="0e1bc-242">Поддержка 3 дополнительных источников данных (ODBC, OData, HDFS) для фабрики данных Azure.</span><span class="sxs-lookup"><span data-stu-id="0e1bc-242">Support 3 more data sources for Azure Data Factory (ODBC, OData, HDFS)</span></span>
*  <span data-ttu-id="0e1bc-243">Поддержка символа кавычек в средстве синтаксического анализа CSV-файлов для фабрики данных Azure.</span><span class="sxs-lookup"><span data-stu-id="0e1bc-243">Support quote character in csv parser for Azure Data Factory</span></span>
*  <span data-ttu-id="0e1bc-244">Поддержка сжатия (в формат BZIP2).</span><span class="sxs-lookup"><span data-stu-id="0e1bc-244">Compression support (BZip2)</span></span>
*  <span data-ttu-id="0e1bc-245">Исправления ошибок</span><span class="sxs-lookup"><span data-stu-id="0e1bc-245">Bug fixes</span></span>

### <a name="1556121"></a><span data-ttu-id="0e1bc-246">1.5.5612.1</span><span class="sxs-lookup"><span data-stu-id="0e1bc-246">1.5.5612.1</span></span>

*  <span data-ttu-id="0e1bc-247">Поддержка пяти реляционных баз данных (MySQL, PostgreSQL, DB2, Teradata и Sybase) для фабрики данных Azure.</span><span class="sxs-lookup"><span data-stu-id="0e1bc-247">Support five relational databases for Azure Data Factory (MySQL, PostgreSQL, DB2, Teradata, and Sybase)</span></span>
*  <span data-ttu-id="0e1bc-248">Поддержка сжатия (в форматы GZIP и DEFLATE).</span><span class="sxs-lookup"><span data-stu-id="0e1bc-248">Compression support (Gzip and Deflate)</span></span>
*  <span data-ttu-id="0e1bc-249">Повышение производительности.</span><span class="sxs-lookup"><span data-stu-id="0e1bc-249">Performance improvements</span></span>
*  <span data-ttu-id="0e1bc-250">Исправления ошибок</span><span class="sxs-lookup"><span data-stu-id="0e1bc-250">Bug fixes</span></span>

### <a name="1455491"></a><span data-ttu-id="0e1bc-251">1.4.5549.1</span><span class="sxs-lookup"><span data-stu-id="0e1bc-251">1.4.5549.1</span></span>

*  <span data-ttu-id="0e1bc-252">Поддержка источника данных Oracle для фабрики данных Azure.</span><span class="sxs-lookup"><span data-stu-id="0e1bc-252">Add Oracle data source support for Azure Data Factory</span></span>
*  <span data-ttu-id="0e1bc-253">Повышение производительности.</span><span class="sxs-lookup"><span data-stu-id="0e1bc-253">Performance improvements</span></span>
*  <span data-ttu-id="0e1bc-254">Исправления ошибок</span><span class="sxs-lookup"><span data-stu-id="0e1bc-254">Bug fixes</span></span>

### <a name="1454921"></a><span data-ttu-id="0e1bc-255">1.4.5492.1</span><span class="sxs-lookup"><span data-stu-id="0e1bc-255">1.4.5492.1</span></span>

*  <span data-ttu-id="0e1bc-256">Внедрение единого двоичного файла, который поддерживает фабрику данных Microsoft Azure и службы Power BI для Office 365.</span><span class="sxs-lookup"><span data-stu-id="0e1bc-256">Unified binary that supports both Microsoft Azure Data Factory and Office 365 Power BI services</span></span>
*  <span data-ttu-id="0e1bc-257">Пробное hello Интерфейс настройки и регистрации</span><span class="sxs-lookup"><span data-stu-id="0e1bc-257">Refine hello Configuration UI and registration process</span></span>
*  <span data-ttu-id="0e1bc-258">Поддержка входящих и исходящих данных Azure для источника данных SQL Server в фабрике данных Azure.</span><span class="sxs-lookup"><span data-stu-id="0e1bc-258">Azure Data Factory – Azure Ingress and Egress support for SQL Server data source</span></span>

### <a name="1253031"></a><span data-ttu-id="0e1bc-259">1.2.5303.1</span><span class="sxs-lookup"><span data-stu-id="0e1bc-259">1.2.5303.1</span></span>

*  <span data-ttu-id="0e1bc-260">Исправьте проблему toosupport время ожидания более продолжительное время соединения с источниками данных.</span><span class="sxs-lookup"><span data-stu-id="0e1bc-260">Fix timeout issue toosupport more time-consuming data source connections.</span></span>

### <a name="1155268"></a><span data-ttu-id="0e1bc-261">1.1.5526.8</span><span class="sxs-lookup"><span data-stu-id="0e1bc-261">1.1.5526.8</span></span>

*  <span data-ttu-id="0e1bc-262">Добавление необходимого компонента при установке — платформы .NET Framework 4.5.1.</span><span class="sxs-lookup"><span data-stu-id="0e1bc-262">Requires .NET Framework 4.5.1 as a prerequisite during setup.</span></span>

### <a name="1051442"></a><span data-ttu-id="0e1bc-263">1.0.5144.2</span><span class="sxs-lookup"><span data-stu-id="0e1bc-263">1.0.5144.2</span></span>

*  <span data-ttu-id="0e1bc-264">Нет изменений, которые влияют на сценарии фабрики данных Azure.</span><span class="sxs-lookup"><span data-stu-id="0e1bc-264">No changes that affect Azure Data Factory scenarios.</span></span>
