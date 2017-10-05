---
title: "Импорт и экспорт файла зоны домена в Azure DNS с помощью Azure CLI 1.0 | Документы Майкрософт"
description: "Узнайте, как импортировать файл зоны DNS в Azure DNS и экспортировать его оттуда с помощью интерфейса командной строки Azure CLI 1.0."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: f5797782-3005-4663-a488-ac0089809010
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/16/2016
ms.author: gwallace
ms.openlocfilehash: d6d3fa7aa0e8b2462b3a6b4b66d3d87ab5535314
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="import-and-export-a-dns-zone-file-using-the-azure-cli-10"></a><span data-ttu-id="43158-103">Импорт и экспорт файла зоны DNS с помощью Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="43158-103">Import and export a DNS zone file using the Azure CLI 1.0</span></span> 

<span data-ttu-id="43158-104">В этой статье приводятся пошаговые инструкции по импорту и экспорту файлов зоны DNS для Azure DNS с помощью Azure CLI 1.0.</span><span class="sxs-lookup"><span data-stu-id="43158-104">This article walks you through how to import and export DNS zone files for Azure DNS using the Azure CLI 1.0.</span></span>

## <a name="introduction-to-dns-zone-migration"></a><span data-ttu-id="43158-105">Общие сведения о миграции зоны DNS</span><span class="sxs-lookup"><span data-stu-id="43158-105">Introduction to DNS zone migration</span></span>

<span data-ttu-id="43158-106">Файл зоны DNS — текстовый файл, содержащий сведения о каждой записи службы доменных имен (DNS) в зоне.</span><span class="sxs-lookup"><span data-stu-id="43158-106">A DNS zone file is a text file that contains details of every Domain Name System (DNS) record in the zone.</span></span> <span data-ttu-id="43158-107">Он соответствует стандартному формату и позволяет передавать записи DNS в системы DNS.</span><span class="sxs-lookup"><span data-stu-id="43158-107">It follows a standard format, making it suitable for transferring DNS records between DNS systems.</span></span> <span data-ttu-id="43158-108">Использование файла зоны — это быстрый, надежный и удобный способ передачи зоны DNS в Azure DNS или в обратном направлении.</span><span class="sxs-lookup"><span data-stu-id="43158-108">Using a zone file is a quick, reliable, and convenient way to transfer a DNS zone into or out of Azure DNS.</span></span>

<span data-ttu-id="43158-109">Azure DNS поддерживает импорт и экспорт файлов зоны с помощью интерфейса командной строки Azure (CLI).</span><span class="sxs-lookup"><span data-stu-id="43158-109">Azure DNS supports importing and exporting zone files by using the Azure command-line interface (CLI).</span></span> <span data-ttu-id="43158-110">Импорт файла зоны с помощью Azure PowerShell или портала Azure в настоящее время **не** поддерживается.</span><span class="sxs-lookup"><span data-stu-id="43158-110">Zone file import is **not** currently supported via Azure PowerShell or the Azure portal.</span></span>

<span data-ttu-id="43158-111">Azure CLI 1.0 — это кроссплатформенная программа командной строки для управления службами Azure.</span><span class="sxs-lookup"><span data-stu-id="43158-111">The Azure CLI 1.0 is a cross-platform command-line tool used for managing Azure services.</span></span> <span data-ttu-id="43158-112">Для платформ Windows, Mac и Linux ее можно скачать на [странице скачивания Azure](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="43158-112">It is available for the Windows, Mac, and Linux platforms from the [Azure downloads page](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="43158-113">Поддержка разных платформ важна при экспорте и импорте файлов зоны, так как наиболее распространенное программное обеспечение сервера доменных имен ([BIND](https://www.isc.org/downloads/bind/)) обычно выполняется в системе Linux.</span><span class="sxs-lookup"><span data-stu-id="43158-113">Cross-platform support is important for importing and exporting zone files, because the most common name server software, [BIND](https://www.isc.org/downloads/bind/), typically runs on Linux.</span></span>

> [!NOTE]
> <span data-ttu-id="43158-114">В настоящее время имеются две версии Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="43158-114">There are currently two versions of the Azure CLI.</span></span> <span data-ttu-id="43158-115">Версия CLI1.0 основана на Node.js, и ее команды начинаются с "azure".</span><span class="sxs-lookup"><span data-stu-id="43158-115">CLI1.0 is based on Node.js, and has commands beginning with "azure".</span></span>
> <span data-ttu-id="43158-116">Версия CLI2.0 основана на Python, и ее команды начинаются с "az".</span><span class="sxs-lookup"><span data-stu-id="43158-116">CLI2.0 is based on Python and has commands beginning with "az".</span></span> <span data-ttu-id="43158-117">Импорт файла зоны поддерживается в обеих версиях, однако мы рекомендуем использовать команды CLI1.0, как описано на этой странице.</span><span class="sxs-lookup"><span data-stu-id="43158-117">While zone file import is supported in both versions, we recommend using the CLI1.0 commands, as described in this page.</span></span>

## <a name="obtain-your-existing-dns-zone-file"></a><span data-ttu-id="43158-118">Получение существующего файла зоны DNS</span><span class="sxs-lookup"><span data-stu-id="43158-118">Obtain your existing DNS zone file</span></span>

<span data-ttu-id="43158-119">Прежде чем импортировать файл зоны DNS в Azure DNS, необходимо получить копию файла зоны.</span><span class="sxs-lookup"><span data-stu-id="43158-119">Before you import a DNS zone file into Azure DNS, you need to obtain a copy of the zone file.</span></span> <span data-ttu-id="43158-120">Источник этого файла зависит от текущего размещения зоны DNS.</span><span class="sxs-lookup"><span data-stu-id="43158-120">The source of this file depends on where the DNS zone is currently hosted.</span></span>

* <span data-ttu-id="43158-121">Если для размещения зоны DNS используется партнерская служба (например, регистратор доменных имен, поставщик услуг размещения DNS или альтернативный поставщик облачных служб), такая служба должна поддерживать скачивание файла зоны DNS.</span><span class="sxs-lookup"><span data-stu-id="43158-121">If your DNS zone is hosted by a partner service (such as a domain registrar, dedicated DNS hosting provider, or alternative cloud provider), that service should provide the ability to download the DNS zone file.</span></span>
* <span data-ttu-id="43158-122">Если зона DNS размещена на DNS-сервере Windows, по умолчанию файлы зоны можно найти в папке **%systemroot%\system32\dns**.</span><span class="sxs-lookup"><span data-stu-id="43158-122">If your DNS zone is hosted on Windows DNS, the default folder for the zone files is **%systemroot%\system32\dns**.</span></span> <span data-ttu-id="43158-123">Полный путь к каждому файлу зоны также отображается на вкладке **Общие** консоли DNS.</span><span class="sxs-lookup"><span data-stu-id="43158-123">The full path to each zone file also shows on the **General** tab of the DNS console.</span></span>
* <span data-ttu-id="43158-124">Если для размещения зоны DNS используется BIND, расположение файла зоны для каждой зоны задается в файле конфигурации BIND **named.conf**.</span><span class="sxs-lookup"><span data-stu-id="43158-124">If your DNS zone is hosted by using BIND, the location of the zone file for each zone is specified in the BIND configuration file **named.conf**.</span></span>

> [!NOTE]
> <span data-ttu-id="43158-125">Файлы зоны, скачанные с GoDaddy, слегка нестандартного формата.</span><span class="sxs-lookup"><span data-stu-id="43158-125">Zone files downloaded from GoDaddy have a slightly nonstandard format.</span></span> <span data-ttu-id="43158-126">Это нужно исправить, прежде чем импортировать эти файлы зоны в Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="43158-126">You need to correct this before you import these zone files into Azure DNS.</span></span>
>
> <span data-ttu-id="43158-127">DNS-имена в RDATA каждой записи DNS указываются как полные имена без точки в конце. Это означает, что другие системы DNS интерпретируют их как относительные имена.</span><span class="sxs-lookup"><span data-stu-id="43158-127">DNS names in the RDATA of each DNS record are specified as fully qualified names, but they don't have a terminating "." This means they are interpreted by other DNS systems as relative names.</span></span> <span data-ttu-id="43158-128">Необходимо изменить файл зоны, добавив точку в конце каждого имени, прежде чем импортировать их в Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="43158-128">You need to edit the zone file to append the terminating "." to their names before you import them into Azure DNS.</span></span>
>
> <span data-ttu-id="43158-129">Например, запись CNAME "www 3600 IN CNAME contoso.com" следует изменить на "www 3600 IN CNAME contoso.com."</span><span class="sxs-lookup"><span data-stu-id="43158-129">For example, the CNAME record "www 3600 IN CNAME contoso.com" should be changed to "www 3600 IN CNAME contoso.com."</span></span>
> <span data-ttu-id="43158-130">(с точкой в конце).</span><span class="sxs-lookup"><span data-stu-id="43158-130">(with a terminating ".").</span></span>

## <a name="import-a-dns-zone-file-into-azure-dns"></a><span data-ttu-id="43158-131">Импорт файла зоны DNS в Azure DNS</span><span class="sxs-lookup"><span data-stu-id="43158-131">Import a DNS zone file into Azure DNS</span></span>

<span data-ttu-id="43158-132">Импорт файла зоны создает зону в Azure DNS, если таковая не существует.</span><span class="sxs-lookup"><span data-stu-id="43158-132">Importing a zone file creates a new zone in Azure DNS if one does not already exist.</span></span> <span data-ttu-id="43158-133">Если зона существует, наборы записей в файле зоны нужно объединить с существующими наборами.</span><span class="sxs-lookup"><span data-stu-id="43158-133">If the zone already exists, the record sets in the zone file must be merged with the existing record sets.</span></span>

### <a name="merge-behavior"></a><span data-ttu-id="43158-134">Поведение объединения</span><span class="sxs-lookup"><span data-stu-id="43158-134">Merge behavior</span></span>

* <span data-ttu-id="43158-135">По умолчанию объединяются существующие и новые наборы записей.</span><span class="sxs-lookup"><span data-stu-id="43158-135">By default, existing and new record sets are merged.</span></span> <span data-ttu-id="43158-136">Одинаковые записи в рамках объединенного набора записей дедуплицируются.</span><span class="sxs-lookup"><span data-stu-id="43158-136">Identical records within a merged record set are de-duplicated.</span></span>
* <span data-ttu-id="43158-137">Если указать параметр `--force`, процесс импорта будет заменять существующие наборы записей новыми.</span><span class="sxs-lookup"><span data-stu-id="43158-137">Alternatively, by specifying the `--force` option, the import process replaces existing record sets with new record sets.</span></span> <span data-ttu-id="43158-138">Существующие наборы записей, у которых нет соответствующих наборов записей в импортированном файле зоны, не удаляются.</span><span class="sxs-lookup"><span data-stu-id="43158-138">Existing record sets that do not have a corresponding record set in the imported zone file are not be removed.</span></span>
* <span data-ttu-id="43158-139">При объединении наборов записей используется значение срока жизни (TTL) существующих наборов записей.</span><span class="sxs-lookup"><span data-stu-id="43158-139">When record sets are merged, the time to live (TTL) of preexisting record sets is used.</span></span> <span data-ttu-id="43158-140">При использовании параметра `--force` задается значение срока жизни нового набора записей.</span><span class="sxs-lookup"><span data-stu-id="43158-140">When `--force` is used, the TTL of the new record set is used.</span></span>
* <span data-ttu-id="43158-141">Параметры начальной записи зоны (SOA) (кроме `host`) всегда берутся из импортированного файла зоны (независимо от использования параметра `--force`).</span><span class="sxs-lookup"><span data-stu-id="43158-141">Start of Authority (SOA) parameters (except `host`) are always taken from the imported zone file, regardless of whether `--force` is used.</span></span> <span data-ttu-id="43158-142">Аналогичным образом для набора записей сервера доменных имен на вершине зоны значение срока жизни всегда извлекается из импортированного файла зоны.</span><span class="sxs-lookup"><span data-stu-id="43158-142">Similarly, for the name server record set at the zone apex, the TTL is always taken from the imported zone file.</span></span>
* <span data-ttu-id="43158-143">Импортированная запись CNAME не заменяет существующую запись CNAME с тем же именем, если только не указан параметр `--force`.</span><span class="sxs-lookup"><span data-stu-id="43158-143">An imported CNAME record does not replace an existing CNAME record with the same name unless the `--force` parameter is specified.</span></span>
* <span data-ttu-id="43158-144">Если возникает конфликт между записью CNAME и другой записью с таким же именем, но другим типом (независимо от того, новая она или существующая), сохраняется существующая запись.</span><span class="sxs-lookup"><span data-stu-id="43158-144">When a conflict arises between a CNAME record and another record of the same name but different type (regardless of which is existing or new), the existing record is retained.</span></span> <span data-ttu-id="43158-145">Это не зависит от параметра `--force`.</span><span class="sxs-lookup"><span data-stu-id="43158-145">This is independent of the use of `--force`.</span></span>

### <a name="additional-information-about-importing"></a><span data-ttu-id="43158-146">Дополнительная информация об импорте</span><span class="sxs-lookup"><span data-stu-id="43158-146">Additional information about importing</span></span>

<span data-ttu-id="43158-147">Ниже приведены дополнительные технические сведения о процессе импорта зоны.</span><span class="sxs-lookup"><span data-stu-id="43158-147">The following notes provide additional technical details about the zone import process.</span></span>

* <span data-ttu-id="43158-148">`$TTL` — необязательная поддерживаемая директива.</span><span class="sxs-lookup"><span data-stu-id="43158-148">The `$TTL` directive is optional, and it is supported.</span></span> <span data-ttu-id="43158-149">Если директива `$TTL` не указывается, записи без явного значения срока жизни импортируются со значением срока жизни по умолчанию (3600 секунд).</span><span class="sxs-lookup"><span data-stu-id="43158-149">When no `$TTL` directive is given, records without an explicit TTL are imported set to a default TTL of 3600 seconds.</span></span> <span data-ttu-id="43158-150">Если в одном наборе записей есть две записи с разными значениями срока жизни, используется меньшее значение.</span><span class="sxs-lookup"><span data-stu-id="43158-150">When two records in the same record set specify different TTLs, the lower value is used.</span></span>
* <span data-ttu-id="43158-151">`$ORIGIN` — необязательная поддерживаемая директива.</span><span class="sxs-lookup"><span data-stu-id="43158-151">The `$ORIGIN` directive is optional, and it is supported.</span></span> <span data-ttu-id="43158-152">Если директива `$ORIGIN` не указывается, используется значение по умолчанию — имя зоны, указанное в командной строке (с точкой в конце).</span><span class="sxs-lookup"><span data-stu-id="43158-152">When no `$ORIGIN` is set, the default value used is the zone name as specified on the command line (plus the terminating ".").</span></span>
* <span data-ttu-id="43158-153">Директивы `$INCLUDE` и `$GENERATE` не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="43158-153">The `$INCLUDE` and `$GENERATE` directives are not supported.</span></span>
* <span data-ttu-id="43158-154">Поддерживаются такие типы записей: A, AAAA, CNAME, MX, NS, SOA, SRV и TXT.</span><span class="sxs-lookup"><span data-stu-id="43158-154">These record types are supported: A, AAAA, CNAME, MX, NS, SOA, SRV, and TXT.</span></span>
* <span data-ttu-id="43158-155">Запись типа SOA автоматически создается в Azure DNS во время создания зоны.</span><span class="sxs-lookup"><span data-stu-id="43158-155">The SOA record is created automatically by Azure DNS when a zone is created.</span></span> <span data-ttu-id="43158-156">При импорте файла зоны все параметры SOA, *кроме* параметра `host`, берутся из файла зоны.</span><span class="sxs-lookup"><span data-stu-id="43158-156">When you import a zone file, all SOA parameters are taken from the zone file *except* the `host` parameter.</span></span> <span data-ttu-id="43158-157">Этот параметр использует значение, предоставляемое Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="43158-157">This parameter uses the value provided by Azure DNS.</span></span> <span data-ttu-id="43158-158">Это происходит, потому что данный параметр должен ссылаться на первичный сервер имен, предоставляемый Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="43158-158">This is because this parameter must refer to the primary name server provided by Azure DNS.</span></span>
* <span data-ttu-id="43158-159">Набор записей сервера доменных имен в вершине зоны также создается службой Azure DNS автоматически во время создания зоны.</span><span class="sxs-lookup"><span data-stu-id="43158-159">The name server record set at the zone apex is also created automatically by Azure DNS when the zone is created.</span></span> <span data-ttu-id="43158-160">Импортируется только значение TTL этого набора записей.</span><span class="sxs-lookup"><span data-stu-id="43158-160">Only the TTL of this record set is imported.</span></span> <span data-ttu-id="43158-161">Эти записи содержат имена серверов доменных имен, предоставляемые Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="43158-161">These records contain the name server names provided by Azure DNS.</span></span> <span data-ttu-id="43158-162">Данные записей не перезаписываются значениями в импортированном файле зоны.</span><span class="sxs-lookup"><span data-stu-id="43158-162">The record data is not overwritten by the values contained in the imported zone file.</span></span>
* <span data-ttu-id="43158-163">Общедоступная предварительная версия Azure DNS поддерживает только записи типа TXT с одной строкой.</span><span class="sxs-lookup"><span data-stu-id="43158-163">During Public Preview, Azure DNS supports only single-string TXT records.</span></span> <span data-ttu-id="43158-164">Записи типа TXT, состоящие из нескольких строк, сцепляются и усекаются до 255 символов.</span><span class="sxs-lookup"><span data-stu-id="43158-164">Multistring TXT records are be concatenated and truncated to 255 characters.</span></span>

### <a name="cli-format-and-values"></a><span data-ttu-id="43158-165">Формат и значения CLI</span><span class="sxs-lookup"><span data-stu-id="43158-165">CLI format and values</span></span>

<span data-ttu-id="43158-166">Команда Azure CLI для импорта зоны DNS имеет следующий формат.</span><span class="sxs-lookup"><span data-stu-id="43158-166">The format of the Azure CLI command to import a DNS zone is:</span></span>

```azurecli
azure network dns zone import [options] <resource group> <zone name> <zone file name>
```

<span data-ttu-id="43158-167">Значения:</span><span class="sxs-lookup"><span data-stu-id="43158-167">Values:</span></span>

* <span data-ttu-id="43158-168">`<resource group>` — имя группы ресурсов для зоны в Azure DNS;</span><span class="sxs-lookup"><span data-stu-id="43158-168">`<resource group>` is the name of the resource group for the zone in Azure DNS.</span></span>
* <span data-ttu-id="43158-169">`<zone name>` — имя зоны;</span><span class="sxs-lookup"><span data-stu-id="43158-169">`<zone name>` is the name of the zone.</span></span>
* <span data-ttu-id="43158-170">`<zone file name>` — путь и имя импортируемого файла зоны.</span><span class="sxs-lookup"><span data-stu-id="43158-170">`<zone file name>` is the path/name of the zone file to be imported.</span></span>

<span data-ttu-id="43158-171">Если зона с таким именем не существует в группе ресурсов, она создается автоматически.</span><span class="sxs-lookup"><span data-stu-id="43158-171">If a zone with this name does not exist in the resource group, it is created for you.</span></span> <span data-ttu-id="43158-172">Если зона существует, импортированные наборы записей объединяются с существующими наборами.</span><span class="sxs-lookup"><span data-stu-id="43158-172">If the zone already exists, the imported record sets are merged with existing record sets.</span></span> <span data-ttu-id="43158-173">Чтобы перезаписать существующие наборы записей, используйте параметр `--force` .</span><span class="sxs-lookup"><span data-stu-id="43158-173">To overwrite the existing record sets, use the `--force` option.</span></span>

<span data-ttu-id="43158-174">Чтобы проверить формат файла зоны, не импортируя его, используйте параметр `--parse-only` .</span><span class="sxs-lookup"><span data-stu-id="43158-174">To verify the format of a zone file without actually importing it, use the `--parse-only` option.</span></span>

### <a name="step-1-import-a-zone-file"></a><span data-ttu-id="43158-175">Шаг 1.</span><span class="sxs-lookup"><span data-stu-id="43158-175">Step 1.</span></span> <span data-ttu-id="43158-176">Импорт файла зоны</span><span class="sxs-lookup"><span data-stu-id="43158-176">Import a zone file</span></span>

<span data-ttu-id="43158-177">Предположим, необходимо импортировать файл зоны для зоны **contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="43158-177">To import a zone file for the zone **contoso.com**.</span></span>

1. <span data-ttu-id="43158-178">Войдите в подписку Azure с помощью Azure CLI 1.0.</span><span class="sxs-lookup"><span data-stu-id="43158-178">Sign in to your Azure subscription by using the Azure CLI 1.0.</span></span>

    ```azurecli
    azure login
    ```

2. <span data-ttu-id="43158-179">Выберите подписку, в рамках которой будет создана зона DNS.</span><span class="sxs-lookup"><span data-stu-id="43158-179">Select the subscription where you want to create your new DNS zone.</span></span>

    ```azurecli
    azure account set <subscription name>
    ```

3. <span data-ttu-id="43158-180">Azure DNS — это служба, управляемая диспетчером ресурсов Azure, поэтому Azure CLI необходимо переключить в режим диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="43158-180">Azure DNS is an Azure Resource Manager-only service, so the Azure CLI must be switched to Resource Manager mode.</span></span>

    ```azurecli
    azure config mode arm
    ```

4. <span data-ttu-id="43158-181">Прежде чем использовать службу Azure DNS, необходимо зарегистрировать подписку для использования поставщика ресурсов Microsoft.Network.</span><span class="sxs-lookup"><span data-stu-id="43158-181">Before you use the Azure DNS service, you must register your subscription to use the Microsoft.Network resource provider.</span></span> <span data-ttu-id="43158-182">(Эта операция выполняется один раз для каждой подписки).</span><span class="sxs-lookup"><span data-stu-id="43158-182">(This is a one-time operation for each subscription.)</span></span>

    ```azurecli
    azure provider register Microsoft.Network
    ```

5. <span data-ttu-id="43158-183">Если у вас еще нет группы ресурсов Resource Manager, создайте ее.</span><span class="sxs-lookup"><span data-stu-id="43158-183">If you don't have one already, you also need to create a Resource Manager resource group.</span></span>

    ```azurecli
    azure group create myresourcegroup westeurope
    ```

6. <span data-ttu-id="43158-184">Чтобы импортировать зону **contoso.com** из файла **contoso.com.txt** в зону DNS в группе ресурсов **myresourcegroup**, выполните команду `azure network dns zone import`.</span><span class="sxs-lookup"><span data-stu-id="43158-184">To import the zone **contoso.com** from the file **contoso.com.txt** into a new DNS zone in the resource group **myresourcegroup**, run the command `azure network dns zone import`.</span></span><BR><span data-ttu-id="43158-185">Эта команда загружает файл зоны и анализирует его.</span><span class="sxs-lookup"><span data-stu-id="43158-185">This command loads the zone file and parse it.</span></span> <span data-ttu-id="43158-186">Затем она инициирует выполнение ряда команд в службе Azure DNS, чтобы создать зону и все наборы записей в ней.</span><span class="sxs-lookup"><span data-stu-id="43158-186">The command executes a series of commands on the Azure DNS service to create the zone and all the record sets in the zone.</span></span> <span data-ttu-id="43158-187">В окне консоли виден ход выполнения команды, а также все ошибки и предупреждения.</span><span class="sxs-lookup"><span data-stu-id="43158-187">The command reports progress in the console window, along with any errors or warnings.</span></span> <span data-ttu-id="43158-188">Так как наборы записей создаются в серии, при импорте большого файла зоны этот процесс может занять несколько минут.</span><span class="sxs-lookup"><span data-stu-id="43158-188">Because record sets are created in series, it may take a few minutes to import a large zone file.</span></span>

    ```azurecli
    azure network dns zone import myresourcegroup contoso.com contoso.com.txt
    ```

### <a name="step-2-verify-the-zone"></a><span data-ttu-id="43158-189">Шаг 2.</span><span class="sxs-lookup"><span data-stu-id="43158-189">Step 2.</span></span> <span data-ttu-id="43158-190">Проверка зоны</span><span class="sxs-lookup"><span data-stu-id="43158-190">Verify the zone</span></span>

<span data-ttu-id="43158-191">Чтобы проверить зону DNS после импорта файла, можно использовать один из следующих методов.</span><span class="sxs-lookup"><span data-stu-id="43158-191">To verify the DNS zone after you import the file, you can use any one of the following methods:</span></span>

* <span data-ttu-id="43158-192">Список записей можно получить, используя следующую команду Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="43158-192">You can list the records by using the following Azure CLI command:</span></span>

    ```azurecli
    azure network dns record-set list myresourcegroup contoso.com
    ```

* <span data-ttu-id="43158-193">Список записей можно вывести с помощью командлета PowerShell `Get-AzureRmDnsRecordSet`.</span><span class="sxs-lookup"><span data-stu-id="43158-193">You can list the records by using the PowerShell cmdlet `Get-AzureRmDnsRecordSet`.</span></span>
* <span data-ttu-id="43158-194">С помощью `nslookup` можно проверить разрешение имен для записей.</span><span class="sxs-lookup"><span data-stu-id="43158-194">You can use `nslookup` to verify name resolution for the records.</span></span> <span data-ttu-id="43158-195">Так как зона еще не делегирована, нужно явно указать правильные серверы доменных имен Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="43158-195">Because the zone isn't delegated yet, you need to specify the correct Azure DNS name servers explicitly.</span></span> <span data-ttu-id="43158-196">В примере ниже показано, как получить имена серверов доменных имен, назначенных зоне.</span><span class="sxs-lookup"><span data-stu-id="43158-196">The following sample shows how to retrieve the name server names assigned to the zone.</span></span> <span data-ttu-id="43158-197">В нем также показано, как запросить запись www с помощью команды `nslookup`.</span><span class="sxs-lookup"><span data-stu-id="43158-197">IT also shows how to query the "www" record by using `nslookup`.</span></span>

        C:\>azure network dns record-set show myresourcegroup contoso.com @ NS
        info:Executing command network dns record-set show
        + Looking up the DNS Record Set "@" of type "NS"
        data:Id: /subscriptions/.../resourceGroups/myresourcegroup/providers/Microsoft.Network/dnszones/contoso.com/NS/@
        data:Name: @
        data:Type: Microsoft.Network/dnszones/NS
        data:Location: global
        data:TTL : 3600
        data:NS records
        data:Name server domain name : ns1-01.azure-dns.com
        data:Name server domain name : ns2-01.azure-dns.net
        data:Name server domain name : ns3-01.azure-dns.org
        data:Name server domain name : ns4-01.azure-dns.info
        data:
        info:network dns record-set show command OK

        C:\> nslookup www.contoso.com ns1-01.azure-dns.com

        Server: ns1-01.azure-dns.com
        Address:  40.90.4.1

        Name:www.contoso.com
        Addresses:  134.170.185.46
        134.170.188.221

### <a name="step-3-update-dns-delegation"></a><span data-ttu-id="43158-198">Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="43158-198">Step 3.</span></span> <span data-ttu-id="43158-199">Обновление делегирования DNS</span><span class="sxs-lookup"><span data-stu-id="43158-199">Update DNS delegation</span></span>

<span data-ttu-id="43158-200">После проверки правильности импорта зоны требуется обновить делегирование DNS, чтобы указать серверы доменных имен Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="43158-200">After you have verified that the zone has been imported correctly, you need to update the DNS delegation to point to the Azure DNS name servers.</span></span> <span data-ttu-id="43158-201">Дополнительные сведения см. в статье [Делегирование домена в Azure DNS](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="43158-201">For more information, see the article [Update the DNS delegation](dns-domain-delegation.md).</span></span>

## <a name="export-a-dns-zone-file-from-azure-dns"></a><span data-ttu-id="43158-202">Экспорт файла зоны DNS из Azure DNS</span><span class="sxs-lookup"><span data-stu-id="43158-202">Export a DNS zone file from Azure DNS</span></span>

<span data-ttu-id="43158-203">Команда Azure CLI для импорта зоны DNS имеет следующий формат.</span><span class="sxs-lookup"><span data-stu-id="43158-203">The format of the Azure CLI command to import a DNS zone is:</span></span>

```azurecli
azure network dns zone export [options] <resource group> <zone name> <zone file name>
```

<span data-ttu-id="43158-204">Значения:</span><span class="sxs-lookup"><span data-stu-id="43158-204">Values:</span></span>

* <span data-ttu-id="43158-205">`<resource group>` — имя группы ресурсов для зоны в Azure DNS;</span><span class="sxs-lookup"><span data-stu-id="43158-205">`<resource group>` is the name of the resource group for the zone in Azure DNS.</span></span>
* <span data-ttu-id="43158-206">`<zone name>` — имя зоны;</span><span class="sxs-lookup"><span data-stu-id="43158-206">`<zone name>` is the name of the zone.</span></span>
* <span data-ttu-id="43158-207">`<zone file name>` — путь и имя экспортируемого файла зоны.</span><span class="sxs-lookup"><span data-stu-id="43158-207">`<zone file name>` is the path/name of the zone file to be exported.</span></span>

<span data-ttu-id="43158-208">Как и при импорте зоны, сначала требуется войти, выбрать подписку и настроить Azure CLI для использования режима Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="43158-208">As with the zone import, you first need to sign in, choose your subscription, and configure the Azure CLI to use Resource Manager mode.</span></span>

### <a name="to-export-a-zone-file"></a><span data-ttu-id="43158-209">Экспорт файла зоны</span><span class="sxs-lookup"><span data-stu-id="43158-209">To export a zone file</span></span>

1. <span data-ttu-id="43158-210">Войдите в подписку Azure с помощью Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="43158-210">Sign in to your Azure subscription by using the Azure CLI.</span></span>

    ```azurecli
    azure login
    ```

2. <span data-ttu-id="43158-211">Выберите подписку, в которой нужно создать зону DNS.</span><span class="sxs-lookup"><span data-stu-id="43158-211">Select the subscription where you want to create your DNS zone.</span></span>

    ```azurecli
    azure account set <subscription name>
    ```

3. <span data-ttu-id="43158-212">DNS Azure является исключительно службой диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="43158-212">Azure DNS is an Azure Resource Manager-only service.</span></span> <span data-ttu-id="43158-213">Azure CLI необходимо переключить в режим диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="43158-213">The Azure CLI must be switched to Resource Manager mode.</span></span>

    ```azurecli
    azure config mode arm
    ```

4. <span data-ttu-id="43158-214">Чтобы экспортировать имеющуюся зону Azure DNS **contoso.com** (в группе ресурсов **myresourcegroup**) в файл **contoso.com.txt** (в текущей папке), выполните команду `azure network dns zone export`.</span><span class="sxs-lookup"><span data-stu-id="43158-214">To export the existing Azure DNS zone **contoso.com** in resource group **myresourcegroup** to the file **contoso.com.txt** (in the current folder), run `azure network dns zone export`.</span></span> <span data-ttu-id="43158-215">Эта команда вызывает службу Azure DNS для перечисления наборов записей в зоне и экспорта результатов в файл зоны, совместимый с форматом BIND.</span><span class="sxs-lookup"><span data-stu-id="43158-215">This command  calls the Azure DNS service to enumerate record sets in the zone and export the results to a BIND-compatible zone file.</span></span>

    ```azurecli
    azure network dns zone export myresourcegroup contoso.com contoso.com.txt
    ```
