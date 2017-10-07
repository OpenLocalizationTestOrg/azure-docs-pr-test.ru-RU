---
title: "aaaImport и доменной зоны экспорта файла tooAzure DNS с помощью Azure CLI 1.0 | Документы Microsoft"
description: "Узнайте, как tooimport экспорта DNS зоны и файл tooAzure DNS с помощью Azure CLI 1.0"
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
ms.openlocfilehash: 4c3163395e151e9934c730349b828c612491016f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="import-and-export-a-dns-zone-file-using-hello-azure-cli-10"></a><span data-ttu-id="2293f-103">Импорт и экспорт в файл зоны DNS, с помощью hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="2293f-103">Import and export a DNS zone file using hello Azure CLI 1.0</span></span> 

<span data-ttu-id="2293f-104">В этой статье рассматриваются как tooimport и экспорт файлов зоны DNS с помощью Azure DNS hello Azure CLI 1.0.</span><span class="sxs-lookup"><span data-stu-id="2293f-104">This article walks you through how tooimport and export DNS zone files for Azure DNS using hello Azure CLI 1.0.</span></span>

## <a name="introduction-toodns-zone-migration"></a><span data-ttu-id="2293f-105">Введение tooDNS зоны миграции</span><span class="sxs-lookup"><span data-stu-id="2293f-105">Introduction tooDNS zone migration</span></span>

<span data-ttu-id="2293f-106">Файл зоны DNS является файлом, содержащим сведения о каждой записи доменных имен (DNS) в зоне hello.</span><span class="sxs-lookup"><span data-stu-id="2293f-106">A DNS zone file is a text file that contains details of every Domain Name System (DNS) record in hello zone.</span></span> <span data-ttu-id="2293f-107">Он соответствует стандартному формату и позволяет передавать записи DNS в системы DNS.</span><span class="sxs-lookup"><span data-stu-id="2293f-107">It follows a standard format, making it suitable for transferring DNS records between DNS systems.</span></span> <span data-ttu-id="2293f-108">С помощью файла зоны — это быстрый, надежный и удобный способ tootransfer зоны DNS в или из Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="2293f-108">Using a zone file is a quick, reliable, and convenient way tootransfer a DNS zone into or out of Azure DNS.</span></span>

<span data-ttu-id="2293f-109">Azure DNS поддерживает импорт и экспорт файлов зоны с помощью hello Azure командной строки (CLI).</span><span class="sxs-lookup"><span data-stu-id="2293f-109">Azure DNS supports importing and exporting zone files by using hello Azure command-line interface (CLI).</span></span> <span data-ttu-id="2293f-110">Импорт файла зоны **не** в настоящее время поддерживается через Azure PowerShell или портал Azure hello.</span><span class="sxs-lookup"><span data-stu-id="2293f-110">Zone file import is **not** currently supported via Azure PowerShell or hello Azure portal.</span></span>

<span data-ttu-id="2293f-111">Hello Azure CLI 1.0 является кросс платформенных средство командной строки для управления службами Azure.</span><span class="sxs-lookup"><span data-stu-id="2293f-111">hello Azure CLI 1.0 is a cross-platform command-line tool used for managing Azure services.</span></span> <span data-ttu-id="2293f-112">Он доступен для платформ Windows, Mac и Linux hello из hello [страницу загрузок Azure](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="2293f-112">It is available for hello Windows, Mac, and Linux platforms from hello [Azure downloads page](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="2293f-113">Кроссплатформенная поддержка важна для импорта и экспорта файлов зоны, поскольку hello наиболее распространенные программного обеспечения имя сервера [ПРИВЯЗКИ](https://www.isc.org/downloads/bind/), как правило, работает на платформе Linux.</span><span class="sxs-lookup"><span data-stu-id="2293f-113">Cross-platform support is important for importing and exporting zone files, because hello most common name server software, [BIND](https://www.isc.org/downloads/bind/), typically runs on Linux.</span></span>

> [!NOTE]
> <span data-ttu-id="2293f-114">В настоящее время существует две версии hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="2293f-114">There are currently two versions of hello Azure CLI.</span></span> <span data-ttu-id="2293f-115">Версия CLI1.0 основана на Node.js, и ее команды начинаются с "azure".</span><span class="sxs-lookup"><span data-stu-id="2293f-115">CLI1.0 is based on Node.js, and has commands beginning with "azure".</span></span>
> <span data-ttu-id="2293f-116">Версия CLI2.0 основана на Python, и ее команды начинаются с "az".</span><span class="sxs-lookup"><span data-stu-id="2293f-116">CLI2.0 is based on Python and has commands beginning with "az".</span></span> <span data-ttu-id="2293f-117">Хотя в обеих версиях поддерживается импорт файла зоны, рекомендуется использовать команды CLI1.0 hello, как описано на этой странице.</span><span class="sxs-lookup"><span data-stu-id="2293f-117">While zone file import is supported in both versions, we recommend using hello CLI1.0 commands, as described in this page.</span></span>

## <a name="obtain-your-existing-dns-zone-file"></a><span data-ttu-id="2293f-118">Получение существующего файла зоны DNS</span><span class="sxs-lookup"><span data-stu-id="2293f-118">Obtain your existing DNS zone file</span></span>

<span data-ttu-id="2293f-119">Прежде чем импортировать файл зоны DNS в Azure DNS, необходимо tooobtain копию файла зоны hello.</span><span class="sxs-lookup"><span data-stu-id="2293f-119">Before you import a DNS zone file into Azure DNS, you need tooobtain a copy of hello zone file.</span></span> <span data-ttu-id="2293f-120">Источник Hello этого файла зависит от того, где в настоящее время размещены hello зоны DNS.</span><span class="sxs-lookup"><span data-stu-id="2293f-120">hello source of this file depends on where hello DNS zone is currently hosted.</span></span>

* <span data-ttu-id="2293f-121">Если вашей зоны DNS размещена служба партнеров (например регистратора доменных имен, выделенных поставщика услуг размещения DNS или альтернативный облачного поставщика), службы должен предоставить файл зоны DNS hello toodownload hello возможности.</span><span class="sxs-lookup"><span data-stu-id="2293f-121">If your DNS zone is hosted by a partner service (such as a domain registrar, dedicated DNS hosting provider, or alternative cloud provider), that service should provide hello ability toodownload hello DNS zone file.</span></span>
* <span data-ttu-id="2293f-122">Если ваш зоны DNS находится в системе DNS Windows, устанавливается в папку по умолчанию hello файлов зоны hello **%systemroot%\system32\dns**.</span><span class="sxs-lookup"><span data-stu-id="2293f-122">If your DNS zone is hosted on Windows DNS, hello default folder for hello zone files is **%systemroot%\system32\dns**.</span></span> <span data-ttu-id="2293f-123">файл зоны tooeach полный путь Hello также показывает hello **Общие** hello консоли DNS.</span><span class="sxs-lookup"><span data-stu-id="2293f-123">hello full path tooeach zone file also shows on hello **General** tab of hello DNS console.</span></span>
* <span data-ttu-id="2293f-124">Если ваш зоны DNS размещается с помощью ПРИВЯЗКИ, расположение hello hello файл зоны для каждой зоны указано в файле конфигурации ПРИВЯЗКИ hello **named.conf**.</span><span class="sxs-lookup"><span data-stu-id="2293f-124">If your DNS zone is hosted by using BIND, hello location of hello zone file for each zone is specified in hello BIND configuration file **named.conf**.</span></span>

> [!NOTE]
> <span data-ttu-id="2293f-125">Файлы зоны, скачанные с GoDaddy, слегка нестандартного формата.</span><span class="sxs-lookup"><span data-stu-id="2293f-125">Zone files downloaded from GoDaddy have a slightly nonstandard format.</span></span> <span data-ttu-id="2293f-126">Требуется toocorrect прежде чем импортировать эти файлы зоны Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="2293f-126">You need toocorrect this before you import these zone files into Azure DNS.</span></span>
>
> <span data-ttu-id="2293f-127">DNS-имена в hello RDATA каждой записи DNS задаются в виде полных имен, но они не имеют завершающей «.» Это означает, что другие системы DNS интерпретируют их как относительные имена.</span><span class="sxs-lookup"><span data-stu-id="2293f-127">DNS names in hello RDATA of each DNS record are specified as fully qualified names, but they don't have a terminating "." This means they are interpreted by other DNS systems as relative names.</span></span> <span data-ttu-id="2293f-128">Требуется tooedit hello зоны файл tooappend hello завершение». «tootheir имена, прежде чем импортировать их в Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="2293f-128">You need tooedit hello zone file tooappend hello terminating "." tootheir names before you import them into Azure DNS.</span></span>
>
> <span data-ttu-id="2293f-129">Например, запись CNAME «www 3600 в домене contoso.com CNAME» hello должны изменяться слишком «www 3600 CNAME в contoso.com».</span><span class="sxs-lookup"><span data-stu-id="2293f-129">For example, hello CNAME record "www 3600 IN CNAME contoso.com" should be changed too"www 3600 IN CNAME contoso.com."</span></span>
> <span data-ttu-id="2293f-130">(с точкой в конце).</span><span class="sxs-lookup"><span data-stu-id="2293f-130">(with a terminating ".").</span></span>

## <a name="import-a-dns-zone-file-into-azure-dns"></a><span data-ttu-id="2293f-131">Импорт файла зоны DNS в Azure DNS</span><span class="sxs-lookup"><span data-stu-id="2293f-131">Import a DNS zone file into Azure DNS</span></span>

<span data-ttu-id="2293f-132">Импорт файла зоны создает зону в Azure DNS, если таковая не существует.</span><span class="sxs-lookup"><span data-stu-id="2293f-132">Importing a zone file creates a new zone in Azure DNS if one does not already exist.</span></span> <span data-ttu-id="2293f-133">Если зона hello уже существует, hello наборов записей в файл зоны hello должны быть объединены с существующие наборы записей hello.</span><span class="sxs-lookup"><span data-stu-id="2293f-133">If hello zone already exists, hello record sets in hello zone file must be merged with hello existing record sets.</span></span>

### <a name="merge-behavior"></a><span data-ttu-id="2293f-134">Поведение объединения</span><span class="sxs-lookup"><span data-stu-id="2293f-134">Merge behavior</span></span>

* <span data-ttu-id="2293f-135">По умолчанию объединяются существующие и новые наборы записей.</span><span class="sxs-lookup"><span data-stu-id="2293f-135">By default, existing and new record sets are merged.</span></span> <span data-ttu-id="2293f-136">Одинаковые записи в рамках объединенного набора записей дедуплицируются.</span><span class="sxs-lookup"><span data-stu-id="2293f-136">Identical records within a merged record set are de-duplicated.</span></span>
* <span data-ttu-id="2293f-137">Кроме того, указав hello `--force` , то hello заменяет процесс импорта задает существующей записи с новые наборы записей.</span><span class="sxs-lookup"><span data-stu-id="2293f-137">Alternatively, by specifying hello `--force` option, hello import process replaces existing record sets with new record sets.</span></span> <span data-ttu-id="2293f-138">Существующие наборы записей, у которых нет соответствующей записи в файл импортированных зоны hello не удаляется.</span><span class="sxs-lookup"><span data-stu-id="2293f-138">Existing record sets that do not have a corresponding record set in hello imported zone file are not be removed.</span></span>
* <span data-ttu-id="2293f-139">При слиянии наборов записей hello toolive (TTL) уже существующих наборов записей используется время.</span><span class="sxs-lookup"><span data-stu-id="2293f-139">When record sets are merged, hello time toolive (TTL) of preexisting record sets is used.</span></span> <span data-ttu-id="2293f-140">Когда `--force` — используется, hello TTL hello новый набор записей используется.</span><span class="sxs-lookup"><span data-stu-id="2293f-140">When `--force` is used, hello TTL of hello new record set is used.</span></span>
* <span data-ttu-id="2293f-141">Параметры зоны (SOA) начала (за исключением `host`) взяты из файла зоны импортированных hello, независимо от того, следует ли всегда `--force` используется.</span><span class="sxs-lookup"><span data-stu-id="2293f-141">Start of Authority (SOA) parameters (except `host`) are always taken from hello imported zone file, regardless of whether `--force` is used.</span></span> <span data-ttu-id="2293f-142">Аналогичным образом для записи сервера имен hello на вершине зоны hello, hello TTL всегда берется из файла импортированного зоны hello.</span><span class="sxs-lookup"><span data-stu-id="2293f-142">Similarly, for hello name server record set at hello zone apex, hello TTL is always taken from hello imported zone file.</span></span>
* <span data-ttu-id="2293f-143">Импортированные записи CNAME не заменяет существующие CNAME записи с точно такое же имя, если hello hello `--force` указан параметр.</span><span class="sxs-lookup"><span data-stu-id="2293f-143">An imported CNAME record does not replace an existing CNAME record with hello same name unless hello `--force` parameter is specified.</span></span>
* <span data-ttu-id="2293f-144">Когда возникает конфликт между запись CNAME и другую запись hello одинаковые имена, но разные введите (независимо от того, что существует или новые), hello существующую запись сохраняется.</span><span class="sxs-lookup"><span data-stu-id="2293f-144">When a conflict arises between a CNAME record and another record of hello same name but different type (regardless of which is existing or new), hello existing record is retained.</span></span> <span data-ttu-id="2293f-145">Это зависит от использования hello `--force`.</span><span class="sxs-lookup"><span data-stu-id="2293f-145">This is independent of hello use of `--force`.</span></span>

### <a name="additional-information-about-importing"></a><span data-ttu-id="2293f-146">Дополнительная информация об импорте</span><span class="sxs-lookup"><span data-stu-id="2293f-146">Additional information about importing</span></span>

<span data-ttu-id="2293f-147">Hello следующие примечания предоставляют дополнительные технические сведения о зоне hello процессе импорта.</span><span class="sxs-lookup"><span data-stu-id="2293f-147">hello following notes provide additional technical details about hello zone import process.</span></span>

* <span data-ttu-id="2293f-148">Hello `$TTL` директива является необязательным, и он поддерживается.</span><span class="sxs-lookup"><span data-stu-id="2293f-148">hello `$TTL` directive is optional, and it is supported.</span></span> <span data-ttu-id="2293f-149">Если аргумент `$TTL` дается директивы, импорт без явного TTL по умолчанию tooa TTL 3600 секунд.</span><span class="sxs-lookup"><span data-stu-id="2293f-149">When no `$TTL` directive is given, records without an explicit TTL are imported set tooa default TTL of 3600 seconds.</span></span> <span data-ttu-id="2293f-150">Если две записи в hello того же набора записей укажите разные TTLs, используется меньшее значение hello.</span><span class="sxs-lookup"><span data-stu-id="2293f-150">When two records in hello same record set specify different TTLs, hello lower value is used.</span></span>
* <span data-ttu-id="2293f-151">Hello `$ORIGIN` директива является необязательным, и он поддерживается.</span><span class="sxs-lookup"><span data-stu-id="2293f-151">hello `$ORIGIN` directive is optional, and it is supported.</span></span> <span data-ttu-id="2293f-152">Если аргумент `$ORIGIN` имеет значение по умолчанию hello hello имя зоны, как указано в командной строке hello является значение, используемое (плюс завершение hello «.»).</span><span class="sxs-lookup"><span data-stu-id="2293f-152">When no `$ORIGIN` is set, hello default value used is hello zone name as specified on hello command line (plus hello terminating ".").</span></span>
* <span data-ttu-id="2293f-153">Hello `$INCLUDE` и `$GENERATE` директивы не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="2293f-153">hello `$INCLUDE` and `$GENERATE` directives are not supported.</span></span>
* <span data-ttu-id="2293f-154">Поддерживаются такие типы записей: A, AAAA, CNAME, MX, NS, SOA, SRV и TXT.</span><span class="sxs-lookup"><span data-stu-id="2293f-154">These record types are supported: A, AAAA, CNAME, MX, NS, SOA, SRV, and TXT.</span></span>
* <span data-ttu-id="2293f-155">Hello начальной записи автоматически создается системой Azure DNS при создании зоны.</span><span class="sxs-lookup"><span data-stu-id="2293f-155">hello SOA record is created automatically by Azure DNS when a zone is created.</span></span> <span data-ttu-id="2293f-156">При импорте файла зоны, все параметры SOA, взяты из файла зоны hello *за исключением* hello `host` параметра.</span><span class="sxs-lookup"><span data-stu-id="2293f-156">When you import a zone file, all SOA parameters are taken from hello zone file *except* hello `host` parameter.</span></span> <span data-ttu-id="2293f-157">Этот параметр использует значение hello, предоставляемое Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="2293f-157">This parameter uses hello value provided by Azure DNS.</span></span> <span data-ttu-id="2293f-158">Это, поскольку этот параметр необходимо указывать toohello первичный сервер имен, предоставляемые Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="2293f-158">This is because this parameter must refer toohello primary name server provided by Azure DNS.</span></span>
* <span data-ttu-id="2293f-159">Hello запись сервера доменных имен на вершине зоны hello также создается автоматически системой Azure DNS при создании зоны hello.</span><span class="sxs-lookup"><span data-stu-id="2293f-159">hello name server record set at hello zone apex is also created automatically by Azure DNS when hello zone is created.</span></span> <span data-ttu-id="2293f-160">Только hello TTL этого набора записей импортируется.</span><span class="sxs-lookup"><span data-stu-id="2293f-160">Only hello TTL of this record set is imported.</span></span> <span data-ttu-id="2293f-161">Эти записи содержат имена серверов имя hello, предоставляемые Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="2293f-161">These records contain hello name server names provided by Azure DNS.</span></span> <span data-ttu-id="2293f-162">данные записи Hello hello значения, содержащиеся в файле импортированных зоны hello не перезаписывается.</span><span class="sxs-lookup"><span data-stu-id="2293f-162">hello record data is not overwritten by hello values contained in hello imported zone file.</span></span>
* <span data-ttu-id="2293f-163">Общедоступная предварительная версия Azure DNS поддерживает только записи типа TXT с одной строкой.</span><span class="sxs-lookup"><span data-stu-id="2293f-163">During Public Preview, Azure DNS supports only single-string TXT records.</span></span> <span data-ttu-id="2293f-164">Состоящее из нескольких строк записи TXT быть объединенное и усеченное too255 символов.</span><span class="sxs-lookup"><span data-stu-id="2293f-164">Multistring TXT records are be concatenated and truncated too255 characters.</span></span>

### <a name="cli-format-and-values"></a><span data-ttu-id="2293f-165">Формат и значения CLI</span><span class="sxs-lookup"><span data-stu-id="2293f-165">CLI format and values</span></span>

<span data-ttu-id="2293f-166">Hello объекта hello Azure CLI команда tooimport зоны DNS выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="2293f-166">hello format of hello Azure CLI command tooimport a DNS zone is:</span></span>

```azurecli
azure network dns zone import [options] <resource group> <zone name> <zone file name>
```

<span data-ttu-id="2293f-167">Значения:</span><span class="sxs-lookup"><span data-stu-id="2293f-167">Values:</span></span>

* <span data-ttu-id="2293f-168">`<resource group>`— Имя группы ресурсов hello hello hello зоны в Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="2293f-168">`<resource group>` is hello name of hello resource group for hello zone in Azure DNS.</span></span>
* <span data-ttu-id="2293f-169">`<zone name>`— Имя зоны hello hello.</span><span class="sxs-lookup"><span data-stu-id="2293f-169">`<zone name>` is hello name of hello zone.</span></span>
* <span data-ttu-id="2293f-170">`<zone file name>`— путь и имя hello зоны файл toobe импортированы hello.</span><span class="sxs-lookup"><span data-stu-id="2293f-170">`<zone file name>` is hello path/name of hello zone file toobe imported.</span></span>

<span data-ttu-id="2293f-171">Если зоны с таким именем не существует в группе ресурсов hello, он создается автоматически.</span><span class="sxs-lookup"><span data-stu-id="2293f-171">If a zone with this name does not exist in hello resource group, it is created for you.</span></span> <span data-ttu-id="2293f-172">Если hello зона уже существует, hello импортированной записи наборы объединяются с существующие наборы записей.</span><span class="sxs-lookup"><span data-stu-id="2293f-172">If hello zone already exists, hello imported record sets are merged with existing record sets.</span></span> <span data-ttu-id="2293f-173">toooverwrite hello существующие наборы записей, используйте hello `--force` параметр.</span><span class="sxs-lookup"><span data-stu-id="2293f-173">toooverwrite hello existing record sets, use hello `--force` option.</span></span>

<span data-ttu-id="2293f-174">Формат hello tooverify файл зоны без импорта фактически, используйте hello `--parse-only` параметр.</span><span class="sxs-lookup"><span data-stu-id="2293f-174">tooverify hello format of a zone file without actually importing it, use hello `--parse-only` option.</span></span>

### <a name="step-1-import-a-zone-file"></a><span data-ttu-id="2293f-175">Шаг 1.</span><span class="sxs-lookup"><span data-stu-id="2293f-175">Step 1.</span></span> <span data-ttu-id="2293f-176">Импорт файла зоны</span><span class="sxs-lookup"><span data-stu-id="2293f-176">Import a zone file</span></span>

<span data-ttu-id="2293f-177">файл зоны для зоны hello tooimport **contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="2293f-177">tooimport a zone file for hello zone **contoso.com**.</span></span>

1. <span data-ttu-id="2293f-178">Войдите в tooyour подписки Azure с помощью hello Azure CLI 1.0.</span><span class="sxs-lookup"><span data-stu-id="2293f-178">Sign in tooyour Azure subscription by using hello Azure CLI 1.0.</span></span>

    ```azurecli
    azure login
    ```

2. <span data-ttu-id="2293f-179">Выберите подписку hello место toocreate вашей новой зоны DNS.</span><span class="sxs-lookup"><span data-stu-id="2293f-179">Select hello subscription where you want toocreate your new DNS zone.</span></span>

    ```azurecli
    azure account set <subscription name>
    ```

3. <span data-ttu-id="2293f-180">Azure DNS — это только для диспетчера ресурсов служба Azure, поэтому hello Azure CLI должны быть выключены tooResource режим диспетчера.</span><span class="sxs-lookup"><span data-stu-id="2293f-180">Azure DNS is an Azure Resource Manager-only service, so hello Azure CLI must be switched tooResource Manager mode.</span></span>

    ```azurecli
    azure config mode arm
    ```

4. <span data-ttu-id="2293f-181">Прежде чем использовать службу Azure DNS hello, необходимо зарегистрировать поставщика ресурсов Microsoft.Network из подписки toouse hello.</span><span class="sxs-lookup"><span data-stu-id="2293f-181">Before you use hello Azure DNS service, you must register your subscription toouse hello Microsoft.Network resource provider.</span></span> <span data-ttu-id="2293f-182">(Эта операция выполняется один раз для каждой подписки).</span><span class="sxs-lookup"><span data-stu-id="2293f-182">(This is a one-time operation for each subscription.)</span></span>

    ```azurecli
    azure provider register Microsoft.Network
    ```

5. <span data-ttu-id="2293f-183">Если у еще его нет, необходимо также toocreate группу ресурсов диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="2293f-183">If you don't have one already, you also need toocreate a Resource Manager resource group.</span></span>

    ```azurecli
    azure group create myresourcegroup westeurope
    ```

6. <span data-ttu-id="2293f-184">зоны hello tooimport **contoso.com** из файла hello **contoso.com.txt** в зоне DNS в группе ресурсов hello **myresourcegroup**, выполните команду hello `azure network dns zone import`.</span><span class="sxs-lookup"><span data-stu-id="2293f-184">tooimport hello zone **contoso.com** from hello file **contoso.com.txt** into a new DNS zone in hello resource group **myresourcegroup**, run hello command `azure network dns zone import`.</span></span><BR><span data-ttu-id="2293f-185">Эта команда загружает файл зоны hello и проанализировать его.</span><span class="sxs-lookup"><span data-stu-id="2293f-185">This command loads hello zone file and parse it.</span></span> <span data-ttu-id="2293f-186">Команда Hello выполняет ряд команд на hello Azure службы toocreate hello зоны DNS и задает все записи hello в зоне hello.</span><span class="sxs-lookup"><span data-stu-id="2293f-186">hello command executes a series of commands on hello Azure DNS service toocreate hello zone and all hello record sets in hello zone.</span></span> <span data-ttu-id="2293f-187">Команда Hello сообщает о ходе выполнения в окне консоли hello, а также все ошибки и предупреждения.</span><span class="sxs-lookup"><span data-stu-id="2293f-187">hello command reports progress in hello console window, along with any errors or warnings.</span></span> <span data-ttu-id="2293f-188">Из-за создания наборов записей в последовательности, может занять несколько минут tooimport большой файл.</span><span class="sxs-lookup"><span data-stu-id="2293f-188">Because record sets are created in series, it may take a few minutes tooimport a large zone file.</span></span>

    ```azurecli
    azure network dns zone import myresourcegroup contoso.com contoso.com.txt
    ```

### <a name="step-2-verify-hello-zone"></a><span data-ttu-id="2293f-189">Шаг 2.</span><span class="sxs-lookup"><span data-stu-id="2293f-189">Step 2.</span></span> <span data-ttu-id="2293f-190">Проверьте hello зоны</span><span class="sxs-lookup"><span data-stu-id="2293f-190">Verify hello zone</span></span>

<span data-ttu-id="2293f-191">tooverify hello зоны DNS после импорта файла hello, можно использовать один из следующих методов hello:</span><span class="sxs-lookup"><span data-stu-id="2293f-191">tooverify hello DNS zone after you import hello file, you can use any one of hello following methods:</span></span>

* <span data-ttu-id="2293f-192">Список записей hello можно, используя следующую команду Azure CLI hello:</span><span class="sxs-lookup"><span data-stu-id="2293f-192">You can list hello records by using hello following Azure CLI command:</span></span>

    ```azurecli
    azure network dns record-set list myresourcegroup contoso.com
    ```

* <span data-ttu-id="2293f-193">Список записей hello можно с помощью командлета PowerShell hello `Get-AzureRmDnsRecordSet`.</span><span class="sxs-lookup"><span data-stu-id="2293f-193">You can list hello records by using hello PowerShell cmdlet `Get-AzureRmDnsRecordSet`.</span></span>
* <span data-ttu-id="2293f-194">Можно использовать `nslookup` tooverify разрешение имен для записей hello.</span><span class="sxs-lookup"><span data-stu-id="2293f-194">You can use `nslookup` tooverify name resolution for hello records.</span></span> <span data-ttu-id="2293f-195">Поскольку еще не делегировать зону hello, вам потребуется toospecify hello правильный Azure DNS-серверами, явным образом.</span><span class="sxs-lookup"><span data-stu-id="2293f-195">Because hello zone isn't delegated yet, you need toospecify hello correct Azure DNS name servers explicitly.</span></span> <span data-ttu-id="2293f-196">Hello следующий пример иллюстрирует, как имена серверов имя hello tooretrieve назначает toohello зоны.</span><span class="sxs-lookup"><span data-stu-id="2293f-196">hello following sample shows how tooretrieve hello name server names assigned toohello zone.</span></span> <span data-ttu-id="2293f-197">ИТ также показано, как запись hello tooquery «www» с помощью `nslookup`.</span><span class="sxs-lookup"><span data-stu-id="2293f-197">IT also shows how tooquery hello "www" record by using `nslookup`.</span></span>

        C:\>azure network dns record-set show myresourcegroup contoso.com @ NS
        info:Executing command network dns record-set show
        + Looking up hello DNS Record Set "@" of type "NS"
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

### <a name="step-3-update-dns-delegation"></a><span data-ttu-id="2293f-198">Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="2293f-198">Step 3.</span></span> <span data-ttu-id="2293f-199">Обновление делегирования DNS</span><span class="sxs-lookup"><span data-stu-id="2293f-199">Update DNS delegation</span></span>

<span data-ttu-id="2293f-200">После подтверждения что hello зоны импортированы правильно, необходимо tooupdate hello DNS делегирования toopoint toohello Azure серверами DNS.</span><span class="sxs-lookup"><span data-stu-id="2293f-200">After you have verified that hello zone has been imported correctly, you need tooupdate hello DNS delegation toopoint toohello Azure DNS name servers.</span></span> <span data-ttu-id="2293f-201">Дополнительные сведения см. в статье hello [обновить делегирование DNS hello](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="2293f-201">For more information, see hello article [Update hello DNS delegation](dns-domain-delegation.md).</span></span>

## <a name="export-a-dns-zone-file-from-azure-dns"></a><span data-ttu-id="2293f-202">Экспорт файла зоны DNS из Azure DNS</span><span class="sxs-lookup"><span data-stu-id="2293f-202">Export a DNS zone file from Azure DNS</span></span>

<span data-ttu-id="2293f-203">Hello объекта hello Azure CLI команда tooimport зоны DNS выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="2293f-203">hello format of hello Azure CLI command tooimport a DNS zone is:</span></span>

```azurecli
azure network dns zone export [options] <resource group> <zone name> <zone file name>
```

<span data-ttu-id="2293f-204">Значения:</span><span class="sxs-lookup"><span data-stu-id="2293f-204">Values:</span></span>

* <span data-ttu-id="2293f-205">`<resource group>`— Имя группы ресурсов hello hello hello зоны в Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="2293f-205">`<resource group>` is hello name of hello resource group for hello zone in Azure DNS.</span></span>
* <span data-ttu-id="2293f-206">`<zone name>`— Имя зоны hello hello.</span><span class="sxs-lookup"><span data-stu-id="2293f-206">`<zone name>` is hello name of hello zone.</span></span>
* <span data-ttu-id="2293f-207">`<zone file name>`— путь и имя hello зоны файл toobe экспортировать hello.</span><span class="sxs-lookup"><span data-stu-id="2293f-207">`<zone file name>` is hello path/name of hello zone file toobe exported.</span></span>

<span data-ttu-id="2293f-208">Как с помощью импорта зоны hello, необходимо сначала toosign в, выберите подписку и настройте режим диспетчера ресурсов toouse hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="2293f-208">As with hello zone import, you first need toosign in, choose your subscription, and configure hello Azure CLI toouse Resource Manager mode.</span></span>

### <a name="tooexport-a-zone-file"></a><span data-ttu-id="2293f-209">tooexport файл зоны</span><span class="sxs-lookup"><span data-stu-id="2293f-209">tooexport a zone file</span></span>

1. <span data-ttu-id="2293f-210">Войдите в tooyour подписки Azure с помощью hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="2293f-210">Sign in tooyour Azure subscription by using hello Azure CLI.</span></span>

    ```azurecli
    azure login
    ```

2. <span data-ttu-id="2293f-211">Выберите подписку hello место toocreate вашей зоны DNS.</span><span class="sxs-lookup"><span data-stu-id="2293f-211">Select hello subscription where you want toocreate your DNS zone.</span></span>

    ```azurecli
    azure account set <subscription name>
    ```

3. <span data-ttu-id="2293f-212">DNS Azure является исключительно службой диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="2293f-212">Azure DNS is an Azure Resource Manager-only service.</span></span> <span data-ttu-id="2293f-213">Hello Azure CLI должен быть в режиме коммутируемые tooResource диспетчера.</span><span class="sxs-lookup"><span data-stu-id="2293f-213">hello Azure CLI must be switched tooResource Manager mode.</span></span>

    ```azurecli
    azure config mode arm
    ```

4. <span data-ttu-id="2293f-214">Существующая зона Azure DNS hello tooexport **contoso.com** в группе ресурсов **myresourcegroup** файл toohello **contoso.com.txt** (в текущей папке hello), запустите `azure network dns zone export`.</span><span class="sxs-lookup"><span data-stu-id="2293f-214">tooexport hello existing Azure DNS zone **contoso.com** in resource group **myresourcegroup** toohello file **contoso.com.txt** (in hello current folder), run `azure network dns zone export`.</span></span> <span data-ttu-id="2293f-215">Эта команда вызывает hello tooenumerate служба Azure DNS наборов записей в зоне hello и экспортировать hello результаты tooa совместимость ПРИВЯЗКИ зоны.</span><span class="sxs-lookup"><span data-stu-id="2293f-215">This command  calls hello Azure DNS service tooenumerate record sets in hello zone and export hello results tooa BIND-compatible zone file.</span></span>

    ```azurecli
    azure network dns zone export myresourcegroup contoso.com contoso.com.txt
    ```
