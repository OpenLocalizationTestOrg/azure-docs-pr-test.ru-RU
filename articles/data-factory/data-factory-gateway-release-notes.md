---
title: "Заметки о выпуске шлюза управления данными | Документация Майкрософт"
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
ms.openlocfilehash: c052d7e9f757164429ce867201b96305e405dce9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="release-notes-for-data-management-gateway"></a><span data-ttu-id="d454d-103">Заметки о выпуске шлюза управления данными</span><span class="sxs-lookup"><span data-stu-id="d454d-103">Release notes for Data Management Gateway</span></span>
<span data-ttu-id="d454d-104">Одной из проблем интеграции данных в наше время является перемещение данных между локальной средой и облаком.</span><span class="sxs-lookup"><span data-stu-id="d454d-104">One of the challenges for modern data integration is to move data to and from on-premises to cloud.</span></span> <span data-ttu-id="d454d-105">Для решения этой проблемы в фабрике данных используется шлюз управления данными. Это агент, который можно установить локально для переноса гибридных данных.</span><span class="sxs-lookup"><span data-stu-id="d454d-105">Data Factory makes this integration with Data Management Gateway, which is an agent that you can install on-premises to enable hybrid data movement.</span></span>

<span data-ttu-id="d454d-106">Следующие статьи содержат подробные сведения о шлюзе управления данными и о его применении.</span><span class="sxs-lookup"><span data-stu-id="d454d-106">See the following articles for detailed information about Data Management Gateway and how to use it:</span></span>

*  [<span data-ttu-id="d454d-107">Шлюз управления данными</span><span class="sxs-lookup"><span data-stu-id="d454d-107">Data Management Gateway</span></span>](data-factory-data-management-gateway.md)
*  [<span data-ttu-id="d454d-108">Перемещение данных между локальным и облачным хранилищами с помощью фабрики данных Azure</span><span class="sxs-lookup"><span data-stu-id="d454d-108">Move data between on-premises and cloud using Azure Data Factory</span></span>](data-factory-move-data-between-onprem-and-cloud.md)


## <a name="current-version-21063477"></a><span data-ttu-id="d454d-109">Текущая версия (2.10.6347.7)</span><span class="sxs-lookup"><span data-stu-id="d454d-109">CURRENT VERSION (2.10.6347.7)</span></span>

### <a name="enhancements-"></a><span data-ttu-id="d454d-110">Улучшения</span><span class="sxs-lookup"><span data-stu-id="d454d-110">Enhancements-</span></span>
- <span data-ttu-id="d454d-111">Записи DNS можно добавить в список разрешений служебной шины, вместо того чтобы создавать список всех разрешенных IP-адресов Azure из брандмауэра (при необходимости).</span><span class="sxs-lookup"><span data-stu-id="d454d-111">You can add DNS entries to whitelist service bus rather than whitelisting all Azure IP addresses from your firewall (if needed).</span></span> <span data-ttu-id="d454d-112">Соответствующие записи DNS можно найти на портале Azure, последовательно выбрав "Фабрика данных" -> "Создать и развернуть" -> "Шлюзы" -> serviceUrls (URL-адреса служб) (в формате JSON).</span><span class="sxs-lookup"><span data-stu-id="d454d-112">You can find respective DNS entry on Azure portal (Data Factory -> ‘Author and Deploy’ -> ‘Gateways’ -> "serviceUrls" (in JSON)</span></span>
- <span data-ttu-id="d454d-113">Соединитель HDFS теперь поддерживает открытый самозаверяющий сертификат, позволяя пропускать проверку SSL.</span><span class="sxs-lookup"><span data-stu-id="d454d-113">HDFS connector now supports self-signed public certificate by letting you skip SSL validation.</span></span>
- <span data-ttu-id="d454d-114">Исправлено. Проблема с отключением шлюза от сети при обновлении (из-за разницы в показаниях часов).</span><span class="sxs-lookup"><span data-stu-id="d454d-114">Fixed: Issue with gateway offline during update (due to clock skew)</span></span>



## <a name="earlier-versions"></a><span data-ttu-id="d454d-115">Более ранние версии</span><span class="sxs-lookup"><span data-stu-id="d454d-115">Earlier versions</span></span>

## <a name="2963132"></a><span data-ttu-id="d454d-116">2.9.6313.2</span><span class="sxs-lookup"><span data-stu-id="d454d-116">2.9.6313.2</span></span>
### <a name="enhancements-"></a><span data-ttu-id="d454d-117">Улучшения</span><span class="sxs-lookup"><span data-stu-id="d454d-117">Enhancements-</span></span>
-   <span data-ttu-id="d454d-118">Записи DNS можно добавить в список разрешений служебной шины, вместо того чтобы создавать утвержденный список всех IP-адресов Azure из брандмауэра (при необходимости).</span><span class="sxs-lookup"><span data-stu-id="d454d-118">You can add DNS entries to whitelist Service Bus rather than whitelisting all Azure IP addresses from your firewall (if needed).</span></span> <span data-ttu-id="d454d-119">Здесь можно получить дополнительные сведения.</span><span class="sxs-lookup"><span data-stu-id="d454d-119">More details here.</span></span>
-   <span data-ttu-id="d454d-120">Теперь вы можете скопировать данные в единичный блочный BLOB-объект размером до 4,75 ТБ (максимальный поддерживаемый размер блочного BLOB-объекта) и из него.</span><span class="sxs-lookup"><span data-stu-id="d454d-120">You can now copy data to/from a single block blob up to 4.75 TB, which is the max supported size of block blob.</span></span> <span data-ttu-id="d454d-121">(Предыдущий лимит составлял 195 ГБ.)</span><span class="sxs-lookup"><span data-stu-id="d454d-121">(earlier limit was 195 GB).</span></span>
-   <span data-ttu-id="d454d-122">Исправлено. Проблема нехватки памяти при распаковке нескольких небольших файлов во время действия копирования.</span><span class="sxs-lookup"><span data-stu-id="d454d-122">Fixed: Out of memory issue while unzipping several small files during copy activity.</span></span>
-   <span data-ttu-id="d454d-123">Исправлено. Проблема, когда индекс выходил за пределы диапазона при копировании из DocumentDB на локальный сервер SQL Server с использованием функции идемпотентности.</span><span class="sxs-lookup"><span data-stu-id="d454d-123">Fixed: Index out of range issue while copying from Document DB to an on-premises SQL Server with idempotency feature.</span></span>
-   <span data-ttu-id="d454d-124">Исправлено. Скрипт очистки SQL не работал с локальным сервером SQL Server из мастера копирования.</span><span class="sxs-lookup"><span data-stu-id="d454d-124">Fixed: SQL cleanup script doesn't work with on-premises SQL Server from Copy Wizard.</span></span>
-   <span data-ttu-id="d454d-125">Исправлено. Имя столбца с пробелом в конце не поддерживается в действии копирования.</span><span class="sxs-lookup"><span data-stu-id="d454d-125">Fixed: Column name with space at the end does not work in copy activity.</span></span>

## <a name="28662833"></a><span data-ttu-id="d454d-126">2.8.66283.3</span><span class="sxs-lookup"><span data-stu-id="d454d-126">2.8.66283.3</span></span>
### <a name="enhancements-"></a><span data-ttu-id="d454d-127">Улучшения</span><span class="sxs-lookup"><span data-stu-id="d454d-127">Enhancements-</span></span>
- <span data-ttu-id="d454d-128">Исправлено. Проблема отсутствия учетных данных при перезагрузке компьютера шлюза.</span><span class="sxs-lookup"><span data-stu-id="d454d-128">Fixed: Issue with missing credentials on gateway machine reboot.</span></span>
- <span data-ttu-id="d454d-129">Исправлено. Проблемы с регистрацией во время восстановления шлюза с помощью файла резервной копии.</span><span class="sxs-lookup"><span data-stu-id="d454d-129">Fixed: Issue with registration during gateway restore using a backup file.</span></span>


## <a name="2762401"></a><span data-ttu-id="d454d-130">2.7.6240.1</span><span class="sxs-lookup"><span data-stu-id="d454d-130">2.7.6240.1</span></span>
### <a name="enhancements-"></a><span data-ttu-id="d454d-131">Улучшения</span><span class="sxs-lookup"><span data-stu-id="d454d-131">Enhancements-</span></span>
- <span data-ttu-id="d454d-132">Исправлено. Неправильное считывание десятичного значения Null из источника Oracle.</span><span class="sxs-lookup"><span data-stu-id="d454d-132">Fixed: Incorrect read of Decimal null value from Oracle as source.</span></span>

## <a name="2661922"></a><span data-ttu-id="d454d-133">2.6.6192.2</span><span class="sxs-lookup"><span data-stu-id="d454d-133">2.6.6192.2</span></span>
### <a name="whats-new"></a><span data-ttu-id="d454d-134">Новые возможности</span><span class="sxs-lookup"><span data-stu-id="d454d-134">What’s new</span></span>
- <span data-ttu-id="d454d-135">Клиенты могут оставлять отзывы о регистрации шлюза.</span><span class="sxs-lookup"><span data-stu-id="d454d-135">Customers can provide feedback on gateway registering experience.</span></span>
- <span data-ttu-id="d454d-136">Поддерживается сжатие в формате ZIP (Deflate).</span><span class="sxs-lookup"><span data-stu-id="d454d-136">Support a new compression format: ZIP (Deflate)</span></span>

### <a name="enhancements-"></a><span data-ttu-id="d454d-137">Улучшения</span><span class="sxs-lookup"><span data-stu-id="d454d-137">Enhancements-</span></span>
- <span data-ttu-id="d454d-138">Повышение производительности приемника Oracle и источника HDFS.</span><span class="sxs-lookup"><span data-stu-id="d454d-138">Performance improvement for Oracle Sink, HDFS source.</span></span>
- <span data-ttu-id="d454d-139">Исправлена ошибка автоматического обновления шлюза и ошибка производительности при параллельной обработке шлюза.</span><span class="sxs-lookup"><span data-stu-id="d454d-139">Bug fix for gateway auto update, gateway parallel processing capacity.</span></span>


## <a name="2561641"></a><span data-ttu-id="d454d-140">2.5.6164.1</span><span class="sxs-lookup"><span data-stu-id="d454d-140">2.5.6164.1</span></span>
### <a name="enhancements"></a><span data-ttu-id="d454d-141">Улучшения</span><span class="sxs-lookup"><span data-stu-id="d454d-141">Enhancements</span></span>
- <span data-ttu-id="d454d-142">Улучшенный и более надежный процесс регистрации шлюза. Теперь можно отслеживать ход выполнения процесса регистрации шлюза, что делает этот процесс более быстрым.</span><span class="sxs-lookup"><span data-stu-id="d454d-142">Improved and more robust Gateway registration experience- Now you can track progress status during the Gateway registration process, which makes the registration experience more responsive.</span></span>
- <span data-ttu-id="d454d-143">Улучшенный процесс восстановления шлюза. Вы по-прежнему можете восстановить данные шлюза, даже если у вас нет файла резервной копии с обновлением.</span><span class="sxs-lookup"><span data-stu-id="d454d-143">Improvement in Gateway Restore Process- You can still recover gateway even if you do not have the gateway backup file with this update.</span></span> <span data-ttu-id="d454d-144">Для этого потребуется сбросить учетные данные связанной службы на портале.</span><span class="sxs-lookup"><span data-stu-id="d454d-144">This would require you to reset Linked Service credentials in Portal.</span></span>
- <span data-ttu-id="d454d-145">Исправление ошибок.</span><span class="sxs-lookup"><span data-stu-id="d454d-145">Bug fix.</span></span>

## <a name="2461511"></a><span data-ttu-id="d454d-146">2.4.6151.1</span><span class="sxs-lookup"><span data-stu-id="d454d-146">2.4.6151.1</span></span>

### <a name="whats-new"></a><span data-ttu-id="d454d-147">Новые возможности</span><span class="sxs-lookup"><span data-stu-id="d454d-147">What’s new</span></span>

- <span data-ttu-id="d454d-148">Теперь учетные данные источника данных можно хранить локально.</span><span class="sxs-lookup"><span data-stu-id="d454d-148">You can now store data source credentials locally.</span></span> <span data-ttu-id="d454d-149">Эти учетные данные шифруются, и</span><span class="sxs-lookup"><span data-stu-id="d454d-149">The credentials are encrypted.</span></span> <span data-ttu-id="d454d-150">их можно восстановить с помощью файла резервной копии, который можно экспортировать с имеющегося шлюза. Все эти действия выполняются локально.</span><span class="sxs-lookup"><span data-stu-id="d454d-150">The data source credentials can be recovered and restored using the backup file that can be exported from the existing Gateway, all on-premises.</span></span>

### <a name="enhancements-"></a><span data-ttu-id="d454d-151">Улучшения</span><span class="sxs-lookup"><span data-stu-id="d454d-151">Enhancements-</span></span>

- <span data-ttu-id="d454d-152">Улучшенный и более надежный процесс регистрации шлюза.</span><span class="sxs-lookup"><span data-stu-id="d454d-152">Improved and more robust Gateway registration experience.</span></span>
- <span data-ttu-id="d454d-153">Добавлена поддержка автоматического обнаружения конфигурации QuoteChar для текстового формата в мастере копирования, а также улучшена точность определения формата.</span><span class="sxs-lookup"><span data-stu-id="d454d-153">Support auto detection of QuoteChar configuration for Text format in copy wizard, and improve the overall format detection accuracy.</span></span>

## <a name="2361002"></a><span data-ttu-id="d454d-154">2.3.6100.2</span><span class="sxs-lookup"><span data-stu-id="d454d-154">2.3.6100.2</span></span>

- <span data-ttu-id="d454d-155">Добавлена поддержка автоматического обнаружения конфигурации firstRowAsHeader и SkipLineCount в мастере копирования для текстовых файлов в локальной файловой системе и HDFS.</span><span class="sxs-lookup"><span data-stu-id="d454d-155">Support firstRowAsHeader and SkipLineCount auto detection in copy wizard for text files in on-premises File system and HDFS.</span></span>
- <span data-ttu-id="d454d-156">Улучшена стабильность сетевого подключения между шлюзом и служебной шиной.</span><span class="sxs-lookup"><span data-stu-id="d454d-156">Enhance the stability of network connection between gateway and Service Bus</span></span>
- <span data-ttu-id="d454d-157">Исправления ошибок</span><span class="sxs-lookup"><span data-stu-id="d454d-157">A few bug fixes</span></span>


## <a name="2260721"></a><span data-ttu-id="d454d-158">2.2.6072.1</span><span class="sxs-lookup"><span data-stu-id="d454d-158">2.2.6072.1</span></span>

*  <span data-ttu-id="d454d-159">Поддерживает настройку HTTP-прокси для шлюза с помощью диспетчера конфигурации шлюза.</span><span class="sxs-lookup"><span data-stu-id="d454d-159">Supports setting HTTP proxy for the gateway using the Gateway Configuration Manager.</span></span> <span data-ttu-id="d454d-160">При наличии данной настройки доступ к большим двоичным объектам Azure, таблицам Azure, Azure Data Lake и Document DB осуществляется через HTTP-прокси.</span><span class="sxs-lookup"><span data-stu-id="d454d-160">If configured, Azure Blob, Azure Table, Azure Data Lake, and Document DB are accessed through HTTP proxy.</span></span>
*  <span data-ttu-id="d454d-161">Поддерживает обработку заголовков для TextFormat при копировании данных из больших двоичных объектов Azure, Azure Data Lake Store, локальной файловой системы и локальной системы HDFS, а также обратно.</span><span class="sxs-lookup"><span data-stu-id="d454d-161">Supports header handling for TextFormat when copying data from/to Azure Blob, Azure Data Lake Store, on-premises File System, and on-premises HDFS.</span></span>
*  <span data-ttu-id="d454d-162">Поддерживает копирование данных из добавочных и страничных BLOB-объектов в дополнение к уже поддерживаемым блочным BLOB-объектам.</span><span class="sxs-lookup"><span data-stu-id="d454d-162">Supports copying data from Append Blob and Page Blob along with the already supported Block Blob.</span></span>
*  <span data-ttu-id="d454d-163">Вводит новое состояние шлюза **Online (Limited)**(В сети (ограничено)), указывающее, что поддерживаются основные функциональные возможности шлюза за исключением интерактивной работы мастера копирования.</span><span class="sxs-lookup"><span data-stu-id="d454d-163">Introduces a new gateway status **Online (Limited)**, which indicates that the main functionality of the gateway works except the interactive operation support for Copy Wizard.</span></span>
*  <span data-ttu-id="d454d-164">Повышает надежность регистрации шлюза с помощью ключа регистрации.</span><span class="sxs-lookup"><span data-stu-id="d454d-164">Enhances the robustness of gateway registration using registration key.</span></span>

## <a name="216040"></a><span data-ttu-id="d454d-165">2.1.6040.</span><span class="sxs-lookup"><span data-stu-id="d454d-165">2.1.6040.</span></span>

*  <span data-ttu-id="d454d-166">Драйвер DB2 теперь включен в пакет установки шлюза.</span><span class="sxs-lookup"><span data-stu-id="d454d-166">DB2 driver is included in the gateway installation package now.</span></span> <span data-ttu-id="d454d-167">Вам не нужно устанавливать его отдельно.</span><span class="sxs-lookup"><span data-stu-id="d454d-167">You do not need to install it separately.</span></span>
*  <span data-ttu-id="d454d-168">Наряду с уже поддерживаемыми платформами (Linux, Unix и Windows) драйвер DB2 теперь поддерживает z/OS и DB2 для i (AS/400).</span><span class="sxs-lookup"><span data-stu-id="d454d-168">DB2 driver now supports z/OS and DB2 for i (AS/400) along with the platforms already supported (Linux, Unix, and Windows).</span></span>
*  <span data-ttu-id="d454d-169">Поддержка использования Azure Cosmos DB в качестве источника или назначения для локальных хранилищ данных.</span><span class="sxs-lookup"><span data-stu-id="d454d-169">Supports using Azure Cosmos DB as a source or destination for on-premises data stores</span></span>
*  <span data-ttu-id="d454d-170">Поддержка копирования данных в горячее и холодное хранилище BLOB-объектов наряду с уже поддерживаемой учетной записью общего назначения.</span><span class="sxs-lookup"><span data-stu-id="d454d-170">Supports copying data from/to cold/hot blob storage along with the already supported general-purpose storage account.</span></span>
*  <span data-ttu-id="d454d-171">Возможность подключения к локальному серверу SQL Server через шлюз с правами для удаленного входа.</span><span class="sxs-lookup"><span data-stu-id="d454d-171">Allows you to connect to on-premises SQL Server via gateway with remote login privileges.</span></span>  

## <a name="2060131"></a><span data-ttu-id="d454d-172">2.0.6013.1</span><span class="sxs-lookup"><span data-stu-id="d454d-172">2.0.6013.1</span></span>

*  <span data-ttu-id="d454d-173">Можно выбрать язык и региональные параметры, используемые при ручной установке шлюза.</span><span class="sxs-lookup"><span data-stu-id="d454d-173">You can select the language/culture to be used by a gateway during manual installation.</span></span>

*  <span data-ttu-id="d454d-174">Если шлюз не работает, как ожидалось, то можно отправить в корпорацию Майкрософт журналы шлюза за последние семь дней, чтобы упростить устранение проблемы.</span><span class="sxs-lookup"><span data-stu-id="d454d-174">When gateway does not work as expected, you can choose to send gateway logs of last seven days to Microsoft to facilitate troubleshooting of the issue.</span></span> <span data-ttu-id="d454d-175">Если шлюз не подключен к облачной службе, то можно выбрать сохранение и архивирование журналов шлюза.</span><span class="sxs-lookup"><span data-stu-id="d454d-175">If gateway is not connected to the cloud service, you can choose to save and archive gateway logs.</span></span>  

*  <span data-ttu-id="d454d-176">Улучшения пользовательского интерфейса диспетчера конфигурации шлюза:</span><span class="sxs-lookup"><span data-stu-id="d454d-176">User interface improvements for gateway configuration manager:</span></span>

    *  <span data-ttu-id="d454d-177">Улучшено отображение состояния шлюза на вкладке "Главная".</span><span class="sxs-lookup"><span data-stu-id="d454d-177">Make gateway status more visible on the Home tab.</span></span>

    *  <span data-ttu-id="d454d-178">Элементы управления реорганизованы и упрощены.</span><span class="sxs-lookup"><span data-stu-id="d454d-178">Reorganized and simplified controls.</span></span>

    *  <span data-ttu-id="d454d-179">Вы можете скопировать данные из хранилища, используя [инструмент копирования с предварительным просмотром, не требующий программирования](data-factory-copy-data-wizard-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="d454d-179">You can copy data from a storage using the [code-free copy preview tool](data-factory-copy-data-wizard-tutorial.md).</span></span> <span data-ttu-id="d454d-180">В разделе [Промежуточное копирование](data-factory-copy-activity-performance.md#staged-copy) приведены общие сведения об этой функции.</span><span class="sxs-lookup"><span data-stu-id="d454d-180">See [Staged Copy](data-factory-copy-activity-performance.md#staged-copy) for details about this feature in general.</span></span>
*  <span data-ttu-id="d454d-181">Шлюз управления данными можно использовать для передачи данных непосредственно из локальной базы данных SQL Server в Машинное обучение Azure.</span><span class="sxs-lookup"><span data-stu-id="d454d-181">You can use Data Management Gateway to ingress data directly from an on-premises SQL Server database into Azure Machine Learning.</span></span>

*  <span data-ttu-id="d454d-182">Повышение производительности.</span><span class="sxs-lookup"><span data-stu-id="d454d-182">Performance improvements</span></span>

    * <span data-ttu-id="d454d-183">Повысьте производительность при просмотре схемы или предварительном просмотре данных SQL Server с помощью инструмента копирования с предварительным просмотром, не требующего программирования.</span><span class="sxs-lookup"><span data-stu-id="d454d-183">Improve performance on viewing Schema/Preview against SQL Server in code-free copy preview tool.</span></span>

## <a name="11259531"></a><span data-ttu-id="d454d-184">1.12.5953.1</span><span class="sxs-lookup"><span data-stu-id="d454d-184">1.12.5953.1</span></span>

*  <span data-ttu-id="d454d-185">Исправления ошибок</span><span class="sxs-lookup"><span data-stu-id="d454d-185">Bug fixes</span></span>

## <a name="11159181"></a><span data-ttu-id="d454d-186">1.11.5918.1</span><span class="sxs-lookup"><span data-stu-id="d454d-186">1.11.5918.1</span></span>

*  <span data-ttu-id="d454d-187">Максимальный размер журнала событий шлюза был увеличен с 1 МБ до 40 МБ.</span><span class="sxs-lookup"><span data-stu-id="d454d-187">Maximum size of the gateway event log has been increased from 1 MB to 40 MB.</span></span>

*  <span data-ttu-id="d454d-188">Если во время автоматического обновления шлюза требуется перезагрузка, отображается диалоговое окно с предупреждением.</span><span class="sxs-lookup"><span data-stu-id="d454d-188">A warning dialog is displayed in case a restart is needed during gateway auto-update.</span></span> <span data-ttu-id="d454d-189">Перезагрузку можно запустить сразу или отложить.</span><span class="sxs-lookup"><span data-stu-id="d454d-189">You can choose to restart right then or later.</span></span>

*  <span data-ttu-id="d454d-190">При сбое автоматического обновления установщик шлюза пытается выполнить автоматическое обновление не больше трех раз.</span><span class="sxs-lookup"><span data-stu-id="d454d-190">In case auto-update fails, gateway installer retries auto-updating three times at maximum.</span></span>

*  <span data-ttu-id="d454d-191">Повышение производительности.</span><span class="sxs-lookup"><span data-stu-id="d454d-191">Performance improvements</span></span>

    * <span data-ttu-id="d454d-192">Повышена эффективность загрузки больших таблиц из локального сервера в сценарий копирования без кода.</span><span class="sxs-lookup"><span data-stu-id="d454d-192">Improve performance for loading large tables from on-premises server in code-free copy scenario.</span></span>

*  <span data-ttu-id="d454d-193">Исправления ошибок</span><span class="sxs-lookup"><span data-stu-id="d454d-193">Bug fixes</span></span>

## <a name="11058921"></a><span data-ttu-id="d454d-194">1.10.5892.1</span><span class="sxs-lookup"><span data-stu-id="d454d-194">1.10.5892.1</span></span>

*  <span data-ttu-id="d454d-195">Повышение производительности.</span><span class="sxs-lookup"><span data-stu-id="d454d-195">Performance improvements</span></span>

*  <span data-ttu-id="d454d-196">Исправления ошибок</span><span class="sxs-lookup"><span data-stu-id="d454d-196">Bug fixes</span></span>

## <a name="1958652"></a><span data-ttu-id="d454d-197">1.9.5865.2</span><span class="sxs-lookup"><span data-stu-id="d454d-197">1.9.5865.2</span></span>

*  <span data-ttu-id="d454d-198">Полностью автоматическое обновление.</span><span class="sxs-lookup"><span data-stu-id="d454d-198">Zero touch auto update capability</span></span>
*  <span data-ttu-id="d454d-199">Новый значок на панели задач, позволяющий просматривать индикаторы состояния шлюза.</span><span class="sxs-lookup"><span data-stu-id="d454d-199">New tray icon with gateway status indicators</span></span>
*  <span data-ttu-id="d454d-200">Возможность немедленного выполнения обновления из клиента.</span><span class="sxs-lookup"><span data-stu-id="d454d-200">Ability to “Update now” from the client</span></span>
*  <span data-ttu-id="d454d-201">Настройка времени обновления.</span><span class="sxs-lookup"><span data-stu-id="d454d-201">Ability to set update schedule time</span></span>
*  <span data-ttu-id="d454d-202">Включение и выключение автоматического обновления с использованием сценария PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d454d-202">PowerShell script for toggling auto-update on/off</span></span>
*  <span data-ttu-id="d454d-203">Поддержка формата JSON</span><span class="sxs-lookup"><span data-stu-id="d454d-203">Support for JSON format</span></span>  
*  <span data-ttu-id="d454d-204">Повышение производительности.</span><span class="sxs-lookup"><span data-stu-id="d454d-204">Performance improvements</span></span>
*  <span data-ttu-id="d454d-205">Исправления ошибок</span><span class="sxs-lookup"><span data-stu-id="d454d-205">Bug fixes</span></span>

## <a name="1858221"></a><span data-ttu-id="d454d-206">1.8.5822.1</span><span class="sxs-lookup"><span data-stu-id="d454d-206">1.8.5822.1</span></span>

*  <span data-ttu-id="d454d-207">Улучшение возможностей устранения неполадок.</span><span class="sxs-lookup"><span data-stu-id="d454d-207">Improve troubleshooting experience</span></span>
*  <span data-ttu-id="d454d-208">Повышение производительности.</span><span class="sxs-lookup"><span data-stu-id="d454d-208">Performance improvements</span></span>
*  <span data-ttu-id="d454d-209">Исправления ошибок</span><span class="sxs-lookup"><span data-stu-id="d454d-209">Bug fixes</span></span>

### <a name="1757951"></a><span data-ttu-id="d454d-210">1.7.5795.1</span><span class="sxs-lookup"><span data-stu-id="d454d-210">1.7.5795.1</span></span>

*  <span data-ttu-id="d454d-211">Повышение производительности.</span><span class="sxs-lookup"><span data-stu-id="d454d-211">Performance improvements</span></span>
*  <span data-ttu-id="d454d-212">Исправления ошибок</span><span class="sxs-lookup"><span data-stu-id="d454d-212">Bug fixes</span></span>

### <a name="1757641"></a><span data-ttu-id="d454d-213">1.7.5764.1</span><span class="sxs-lookup"><span data-stu-id="d454d-213">1.7.5764.1</span></span>

*  <span data-ttu-id="d454d-214">Повышение производительности.</span><span class="sxs-lookup"><span data-stu-id="d454d-214">Performance improvements</span></span>
*  <span data-ttu-id="d454d-215">Исправления ошибок</span><span class="sxs-lookup"><span data-stu-id="d454d-215">Bug fixes</span></span>

### <a name="1657351"></a><span data-ttu-id="d454d-216">1.6.5735.1</span><span class="sxs-lookup"><span data-stu-id="d454d-216">1.6.5735.1</span></span>

*  <span data-ttu-id="d454d-217">Поддержка локальной системы HDFS для источника и приемника.</span><span class="sxs-lookup"><span data-stu-id="d454d-217">Support on-premises HDFS Source/Sink</span></span>
*  <span data-ttu-id="d454d-218">Повышение производительности.</span><span class="sxs-lookup"><span data-stu-id="d454d-218">Performance improvements</span></span>
*  <span data-ttu-id="d454d-219">Исправления ошибок</span><span class="sxs-lookup"><span data-stu-id="d454d-219">Bug fixes</span></span>

### <a name="1656961"></a><span data-ttu-id="d454d-220">1.6.5696.1</span><span class="sxs-lookup"><span data-stu-id="d454d-220">1.6.5696.1</span></span>

*  <span data-ttu-id="d454d-221">Повышение производительности.</span><span class="sxs-lookup"><span data-stu-id="d454d-221">Performance improvements</span></span>
*  <span data-ttu-id="d454d-222">Исправления ошибок</span><span class="sxs-lookup"><span data-stu-id="d454d-222">Bug fixes</span></span>

### <a name="1656761"></a><span data-ttu-id="d454d-223">1.6.5676.1</span><span class="sxs-lookup"><span data-stu-id="d454d-223">1.6.5676.1</span></span>

*  <span data-ttu-id="d454d-224">Поддержка средств диагностики в диспетчере конфигурации.</span><span class="sxs-lookup"><span data-stu-id="d454d-224">Support diagnostic tools on Configuration Manager</span></span>
*  <span data-ttu-id="d454d-225">Поддержка столбцов источников табличных данных для фабрики данных Azure.</span><span class="sxs-lookup"><span data-stu-id="d454d-225">Support table columns for tabular data sources for Azure Data Factory</span></span>
*  <span data-ttu-id="d454d-226">Поддержка хранилища данных SQL для фабрики данных Azure.</span><span class="sxs-lookup"><span data-stu-id="d454d-226">Support SQL DW for Azure Data Factory</span></span>
*  <span data-ttu-id="d454d-227">Поддержка свойства reclusive в BlobSource и FileSource для фабрики данных Azure.</span><span class="sxs-lookup"><span data-stu-id="d454d-227">Support Reclusive in BlobSource and FileSource for Azure Data Factory</span></span>
*  <span data-ttu-id="d454d-228">Поддержка значений MergeFiles, PreserveHierarchy и FlattenHierarchy свойства copyBehavior в BlobSink и FileSink для двоичного копирования в фабрике данных Azure.</span><span class="sxs-lookup"><span data-stu-id="d454d-228">Support CopyBehavior – MergeFiles, PreserveHierarchy, and FlattenHierarchy in BlobSink and FileSink with Binary Copy for Azure Data Factory</span></span>
*  <span data-ttu-id="d454d-229">Поддержка сообщения о ходе выполнения действия копирования в фабрике данных Azure.</span><span class="sxs-lookup"><span data-stu-id="d454d-229">Support Copy Activity reporting progress for Azure Data Factory</span></span>
*  <span data-ttu-id="d454d-230">Поддержка проверки подключения к источнику данных в фабрике данных Azure.</span><span class="sxs-lookup"><span data-stu-id="d454d-230">Support Data Source Connectivity Validation for Azure Data Factory</span></span>
*  <span data-ttu-id="d454d-231">Исправления ошибок</span><span class="sxs-lookup"><span data-stu-id="d454d-231">Bug fixes</span></span>

### <a name="1656721"></a><span data-ttu-id="d454d-232">1.6.5672.1</span><span class="sxs-lookup"><span data-stu-id="d454d-232">1.6.5672.1</span></span>

*  <span data-ttu-id="d454d-233">Поддержка задания имени таблицы для источника данных ODBC в фабрике данных Azure</span><span class="sxs-lookup"><span data-stu-id="d454d-233">Support table name for ODBC data source for Azure Data Factory</span></span>
*  <span data-ttu-id="d454d-234">Повышение производительности.</span><span class="sxs-lookup"><span data-stu-id="d454d-234">Performance improvements</span></span>
*  <span data-ttu-id="d454d-235">Исправления ошибок</span><span class="sxs-lookup"><span data-stu-id="d454d-235">Bug fixes</span></span>

### <a name="1656581"></a><span data-ttu-id="d454d-236">1.6.5658.1</span><span class="sxs-lookup"><span data-stu-id="d454d-236">1.6.5658.1</span></span>

*  <span data-ttu-id="d454d-237">Поддержка FileSink для фабрики данных Azure.</span><span class="sxs-lookup"><span data-stu-id="d454d-237">Support File Sink for Azure Data Factory</span></span>
*  <span data-ttu-id="d454d-238">Поддержка сохранения иерархии при двоичном копировании в фабрике данных Azure.</span><span class="sxs-lookup"><span data-stu-id="d454d-238">Support preserving hierarchy in binary copy for Azure Data Factory</span></span>
*  <span data-ttu-id="d454d-239">Поддержка идемпотентности действия копирования в фабрике данных Azure.</span><span class="sxs-lookup"><span data-stu-id="d454d-239">Support Copy Activity Idempotency for Azure Data Factory</span></span>
*  <span data-ttu-id="d454d-240">Исправления ошибок</span><span class="sxs-lookup"><span data-stu-id="d454d-240">Bug fixes</span></span>

### <a name="1656401"></a><span data-ttu-id="d454d-241">1.6.5640.1</span><span class="sxs-lookup"><span data-stu-id="d454d-241">1.6.5640.1</span></span>

*  <span data-ttu-id="d454d-242">Поддержка 3 дополнительных источников данных (ODBC, OData, HDFS) для фабрики данных Azure.</span><span class="sxs-lookup"><span data-stu-id="d454d-242">Support 3 more data sources for Azure Data Factory (ODBC, OData, HDFS)</span></span>
*  <span data-ttu-id="d454d-243">Поддержка символа кавычек в средстве синтаксического анализа CSV-файлов для фабрики данных Azure.</span><span class="sxs-lookup"><span data-stu-id="d454d-243">Support quote character in csv parser for Azure Data Factory</span></span>
*  <span data-ttu-id="d454d-244">Поддержка сжатия (в формат BZIP2).</span><span class="sxs-lookup"><span data-stu-id="d454d-244">Compression support (BZip2)</span></span>
*  <span data-ttu-id="d454d-245">Исправления ошибок</span><span class="sxs-lookup"><span data-stu-id="d454d-245">Bug fixes</span></span>

### <a name="1556121"></a><span data-ttu-id="d454d-246">1.5.5612.1</span><span class="sxs-lookup"><span data-stu-id="d454d-246">1.5.5612.1</span></span>

*  <span data-ttu-id="d454d-247">Поддержка пяти реляционных баз данных (MySQL, PostgreSQL, DB2, Teradata и Sybase) для фабрики данных Azure.</span><span class="sxs-lookup"><span data-stu-id="d454d-247">Support five relational databases for Azure Data Factory (MySQL, PostgreSQL, DB2, Teradata, and Sybase)</span></span>
*  <span data-ttu-id="d454d-248">Поддержка сжатия (в форматы GZIP и DEFLATE).</span><span class="sxs-lookup"><span data-stu-id="d454d-248">Compression support (Gzip and Deflate)</span></span>
*  <span data-ttu-id="d454d-249">Повышение производительности.</span><span class="sxs-lookup"><span data-stu-id="d454d-249">Performance improvements</span></span>
*  <span data-ttu-id="d454d-250">Исправления ошибок</span><span class="sxs-lookup"><span data-stu-id="d454d-250">Bug fixes</span></span>

### <a name="1455491"></a><span data-ttu-id="d454d-251">1.4.5549.1</span><span class="sxs-lookup"><span data-stu-id="d454d-251">1.4.5549.1</span></span>

*  <span data-ttu-id="d454d-252">Поддержка источника данных Oracle для фабрики данных Azure.</span><span class="sxs-lookup"><span data-stu-id="d454d-252">Add Oracle data source support for Azure Data Factory</span></span>
*  <span data-ttu-id="d454d-253">Повышение производительности.</span><span class="sxs-lookup"><span data-stu-id="d454d-253">Performance improvements</span></span>
*  <span data-ttu-id="d454d-254">Исправления ошибок</span><span class="sxs-lookup"><span data-stu-id="d454d-254">Bug fixes</span></span>

### <a name="1454921"></a><span data-ttu-id="d454d-255">1.4.5492.1</span><span class="sxs-lookup"><span data-stu-id="d454d-255">1.4.5492.1</span></span>

*  <span data-ttu-id="d454d-256">Внедрение единого двоичного файла, который поддерживает фабрику данных Microsoft Azure и службы Power BI для Office 365.</span><span class="sxs-lookup"><span data-stu-id="d454d-256">Unified binary that supports both Microsoft Azure Data Factory and Office 365 Power BI services</span></span>
*  <span data-ttu-id="d454d-257">Детализация пользовательского интерфейса настройки и процесса регистрации.</span><span class="sxs-lookup"><span data-stu-id="d454d-257">Refine the Configuration UI and registration process</span></span>
*  <span data-ttu-id="d454d-258">Поддержка входящих и исходящих данных Azure для источника данных SQL Server в фабрике данных Azure.</span><span class="sxs-lookup"><span data-stu-id="d454d-258">Azure Data Factory – Azure Ingress and Egress support for SQL Server data source</span></span>

### <a name="1253031"></a><span data-ttu-id="d454d-259">1.2.5303.1</span><span class="sxs-lookup"><span data-stu-id="d454d-259">1.2.5303.1</span></span>

*  <span data-ttu-id="d454d-260">Устранение проблемы времени ожидания для поддержки подключений к источникам данных, требующих еще больших затрат времени.</span><span class="sxs-lookup"><span data-stu-id="d454d-260">Fix timeout issue to support more time-consuming data source connections.</span></span>

### <a name="1155268"></a><span data-ttu-id="d454d-261">1.1.5526.8</span><span class="sxs-lookup"><span data-stu-id="d454d-261">1.1.5526.8</span></span>

*  <span data-ttu-id="d454d-262">Добавление необходимого компонента при установке — платформы .NET Framework 4.5.1.</span><span class="sxs-lookup"><span data-stu-id="d454d-262">Requires .NET Framework 4.5.1 as a prerequisite during setup.</span></span>

### <a name="1051442"></a><span data-ttu-id="d454d-263">1.0.5144.2</span><span class="sxs-lookup"><span data-stu-id="d454d-263">1.0.5144.2</span></span>

*  <span data-ttu-id="d454d-264">Нет изменений, которые влияют на сценарии фабрики данных Azure.</span><span class="sxs-lookup"><span data-stu-id="d454d-264">No changes that affect Azure Data Factory scenarios.</span></span>
