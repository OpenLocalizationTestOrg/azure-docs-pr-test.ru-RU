---
title: "Перемещение данных из источника HTTP в Azure | Документация Майкрософт"
description: "Сведения о перемещении данных из локального или облачного источника HTTP с помощью фабрики данных Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: 3cc1bd293868b0bb093f617ac12e16c26780fc89
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="move-data-from-an-http-source-using-azure-data-factory"></a><span data-ttu-id="2ae3a-103">Перемещение данных из источника HTTP с помощью фабрики данных Azure</span><span class="sxs-lookup"><span data-stu-id="2ae3a-103">Move data from an HTTP source using Azure Data Factory</span></span>
<span data-ttu-id="2ae3a-104">В этой статье описано, как с помощью действия копирования в фабрике данных Azure переместить данные из локальной или облачной конечной точки HTTP в поддерживаемый приемник данных.</span><span class="sxs-lookup"><span data-stu-id="2ae3a-104">This article outlines how to use the Copy Activity in Azure Data Factory to move data from an on-premises/cloud HTTP endpoint to a supported sink data store.</span></span> <span data-ttu-id="2ae3a-105">В этой статье в продолжение темы о [действиях перемещения данных](data-factory-data-movement-activities.md) приведены общие сведения о перемещении данных с помощью действия копирования, а также список поддерживаемых хранилищ данных, используемых в качестве источников и приемников.</span><span class="sxs-lookup"><span data-stu-id="2ae3a-105">This article builds on the [data movement activities](data-factory-data-movement-activities.md) article that presents a general overview of data movement with copy activity and the list of data stores supported as sources/sinks.</span></span>

<span data-ttu-id="2ae3a-106">В настоящее время фабрика данных поддерживает только перемещение данных из источника HTTP в другие хранилища данных, но не наоборот.</span><span class="sxs-lookup"><span data-stu-id="2ae3a-106">Data factory currently supports only moving data from an HTTP source to other data stores, but not moving data from other data stores to an HTTP destination.</span></span>

## <a name="supported-scenarios-and-authentication-types"></a><span data-ttu-id="2ae3a-107">Поддерживаемые сценарии и типы аутентификации</span><span class="sxs-lookup"><span data-stu-id="2ae3a-107">Supported scenarios and authentication types</span></span>
<span data-ttu-id="2ae3a-108">Вы можете использовать этот соединитель HTTP, чтобы получить данные из **облачной и локальной конечных точек HTTP** с помощью метода HTTP **GET** или **POST**.</span><span class="sxs-lookup"><span data-stu-id="2ae3a-108">You can use this HTTP connector to retrieve data from **both cloud and on-premises HTTP/s endpoint** by using HTTP **GET** or **POST** method.</span></span> <span data-ttu-id="2ae3a-109">Поддерживаемые типы аутентификации: **Anonymous**, **Basic**, **Digest**, **Windows** и **ClientCertificate**.</span><span class="sxs-lookup"><span data-stu-id="2ae3a-109">The following authentication types are supported: **Anonymous**, **Basic**, **Digest**, **Windows**, and **ClientCertificate**.</span></span> <span data-ttu-id="2ae3a-110">Разница между этим соединителем и [соединителем для веб-таблиц](data-factory-web-table-connector.md) заключается в том, что соединитель для веб-таблиц используется для извлечения содержимого таблицы из веб-страницы HTML.</span><span class="sxs-lookup"><span data-stu-id="2ae3a-110">Note the difference between this connector and the [Web table connector](data-factory-web-table-connector.md) is: the latter is used to extract table content from web HTML page.</span></span>

<span data-ttu-id="2ae3a-111">При копировании данных из локальной конечной точки HTTP необходимо установить шлюз управления данными в локальной среде или на виртуальной машине Azure.</span><span class="sxs-lookup"><span data-stu-id="2ae3a-111">When copying data from an on-premises HTTP endpoint, you need install a Data Management Gateway in the on-premises environment/Azure VM.</span></span> <span data-ttu-id="2ae3a-112">В статье [Перемещение данных между локальными и облачными ресурсами](data-factory-move-data-between-onprem-and-cloud.md) приведены сведения о шлюзе управления данными и пошаговые инструкции по его настройке.</span><span class="sxs-lookup"><span data-stu-id="2ae3a-112">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article to learn about Data Management Gateway and step-by-step instructions on setting up the gateway.</span></span>

## <a name="getting-started"></a><span data-ttu-id="2ae3a-113">Приступая к работе</span><span class="sxs-lookup"><span data-stu-id="2ae3a-113">Getting started</span></span>
<span data-ttu-id="2ae3a-114">Вы можете создать конвейер с действием копирования, которое перемещает данные из источника HTTP с помощью разных инструментов и интерфейсов API.</span><span class="sxs-lookup"><span data-stu-id="2ae3a-114">You can create a pipeline with a copy activity that moves data from an HTTP source by using different tools/APIs.</span></span>

- <span data-ttu-id="2ae3a-115">Проще всего создать конвейер с помощью **мастера копирования**.</span><span class="sxs-lookup"><span data-stu-id="2ae3a-115">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="2ae3a-116">В статье [Руководство. Создание конвейера с действием копирования с помощью мастера копирования фабрики данных](data-factory-copy-data-wizard-tutorial.md) приведены краткие пошаговые указания по созданию конвейера с помощью мастера копирования данных.</span><span class="sxs-lookup"><span data-stu-id="2ae3a-116">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

- <span data-ttu-id="2ae3a-117">Также для создания конвейера можно использовать следующие инструменты: **портал Azure**, **Visual Studio**, **Azure PowerShell**, **шаблон Azure Resource Manager**, **API .NET** и **REST API**.</span><span class="sxs-lookup"><span data-stu-id="2ae3a-117">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="2ae3a-118">Пошаговые инструкции по созданию конвейера с действием копирования см. в [руководстве по действию копирования](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="2ae3a-118">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> <span data-ttu-id="2ae3a-119">Примеры JSON для копирования данных из источника HTTP в хранилище BLOB-объектов Azure см. в разделе [Примеры определений JSON](#json-examples).</span><span class="sxs-lookup"><span data-stu-id="2ae3a-119">For JSON samples to copy data from HTTP source to Azure Blob Storage, see [JSON examples](#json-examples) section of this articles.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="2ae3a-120">Свойства связанной службы</span><span class="sxs-lookup"><span data-stu-id="2ae3a-120">Linked service properties</span></span>
<span data-ttu-id="2ae3a-121">В следующей таблице содержится описание элементов JSON, которые относятся к связанной службе HTTP.</span><span class="sxs-lookup"><span data-stu-id="2ae3a-121">The following table provides description for JSON elements specific to HTTP linked service.</span></span>

| <span data-ttu-id="2ae3a-122">Свойство</span><span class="sxs-lookup"><span data-stu-id="2ae3a-122">Property</span></span> | <span data-ttu-id="2ae3a-123">Описание</span><span class="sxs-lookup"><span data-stu-id="2ae3a-123">Description</span></span> | <span data-ttu-id="2ae3a-124">Обязательно</span><span class="sxs-lookup"><span data-stu-id="2ae3a-124">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2ae3a-125">type</span><span class="sxs-lookup"><span data-stu-id="2ae3a-125">type</span></span> | <span data-ttu-id="2ae3a-126">Задайте для этого свойства значение `Http`.</span><span class="sxs-lookup"><span data-stu-id="2ae3a-126">The type property must be set to: `Http`.</span></span> | <span data-ttu-id="2ae3a-127">Да</span><span class="sxs-lookup"><span data-stu-id="2ae3a-127">Yes</span></span> |
| <span data-ttu-id="2ae3a-128">url</span><span class="sxs-lookup"><span data-stu-id="2ae3a-128">url</span></span> | <span data-ttu-id="2ae3a-129">Базовый URL-адрес веб-сервера.</span><span class="sxs-lookup"><span data-stu-id="2ae3a-129">Base URL to the Web Server</span></span> | <span data-ttu-id="2ae3a-130">Да</span><span class="sxs-lookup"><span data-stu-id="2ae3a-130">Yes</span></span> |
| <span data-ttu-id="2ae3a-131">authenticationType</span><span class="sxs-lookup"><span data-stu-id="2ae3a-131">authenticationType</span></span> | <span data-ttu-id="2ae3a-132">Указывает тип проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="2ae3a-132">Specifies the authentication type.</span></span> <span data-ttu-id="2ae3a-133">Допустимые значения: **Anonymous**, **Basic**, **Digest**, **Windows** и **ClientCertificate**.</span><span class="sxs-lookup"><span data-stu-id="2ae3a-133">Allowed values are: **Anonymous**, **Basic**, **Digest**, **Windows**, **ClientCertificate**.</span></span> <br><br> <span data-ttu-id="2ae3a-134">В разделах ниже описываются дополнительные свойства и приведены примеры JSON для поддерживаемых типов проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="2ae3a-134">Refer to sections below this table on more properties and JSON samples for those authentication types respectively.</span></span> | <span data-ttu-id="2ae3a-135">Да</span><span class="sxs-lookup"><span data-stu-id="2ae3a-135">Yes</span></span> |
| <span data-ttu-id="2ae3a-136">enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="2ae3a-136">enableServerCertificateValidation</span></span> | <span data-ttu-id="2ae3a-137">Укажите, следует ли включать проверку SSL-сертификата на сервере, если источником является веб-сервер HTTPS.</span><span class="sxs-lookup"><span data-stu-id="2ae3a-137">Specify whether to enable server SSL certificate validation if source is HTTPS Web Server</span></span> | <span data-ttu-id="2ae3a-138">Нет. Значение по умолчанию — true.</span><span class="sxs-lookup"><span data-stu-id="2ae3a-138">No, default is true</span></span> |
| <span data-ttu-id="2ae3a-139">gatewayName</span><span class="sxs-lookup"><span data-stu-id="2ae3a-139">gatewayName</span></span> | <span data-ttu-id="2ae3a-140">Имя шлюза управления данными для подключения к локальному источнику HTTP.</span><span class="sxs-lookup"><span data-stu-id="2ae3a-140">Name of the Data Management Gateway to connect to an on-premises HTTP source.</span></span> | <span data-ttu-id="2ae3a-141">Да, если копирование выполняется из локального источника HTTP.</span><span class="sxs-lookup"><span data-stu-id="2ae3a-141">Yes if copying data from an on-premises HTTP source.</span></span> |
| <span data-ttu-id="2ae3a-142">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="2ae3a-142">encryptedCredential</span></span> | <span data-ttu-id="2ae3a-143">Зашифрованные учетные данные для доступа к конечной точке HTTP.</span><span class="sxs-lookup"><span data-stu-id="2ae3a-143">Encrypted credential to access the HTTP endpoint.</span></span> <span data-ttu-id="2ae3a-144">При настройке сведений для проверки подлинности в мастере копирования или всплывающем диалоговом окне ClickOnce создаются автоматически.</span><span class="sxs-lookup"><span data-stu-id="2ae3a-144">Auto-generated when you configure the authentication information in copy wizard or the ClickOnce popup dialog.</span></span> | <span data-ttu-id="2ae3a-145">Нет.</span><span class="sxs-lookup"><span data-stu-id="2ae3a-145">No.</span></span> <span data-ttu-id="2ae3a-146">Применимо, только когда копирование данных выполняется с локального HTTP-сервера.</span><span class="sxs-lookup"><span data-stu-id="2ae3a-146">Apply only when copying data from an on-premises HTTP server.</span></span> |

<span data-ttu-id="2ae3a-147">Дополнительные сведения о настройке учетных данных для локального источника данных соединителя HTTP см. в статье [Перемещение данных между локальными источниками и облаком с помощью шлюза управления данными](data-factory-move-data-between-onprem-and-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="2ae3a-147">See [Move data between on-premises sources and the cloud with Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md) for details about setting credentials for on-premises HTTP connector data source.</span></span>

### <a name="using-basic-digest-or-windows-authentication"></a><span data-ttu-id="2ae3a-148">Использование типов проверки подлинности Basic, Digest или Windows</span><span class="sxs-lookup"><span data-stu-id="2ae3a-148">Using Basic, Digest, or Windows authentication</span></span>

<span data-ttu-id="2ae3a-149">Задайте для свойства `authenticationType` значения `Basic`, `Digest` или `Windows` и укажите следующие свойства помимо универсальных свойств соединителя HTTP, приведенных выше.</span><span class="sxs-lookup"><span data-stu-id="2ae3a-149">Set `authenticationType` as `Basic`, `Digest`, or `Windows`, and specify the following properties besides the HTTP connector generic ones introduced above:</span></span>

| <span data-ttu-id="2ae3a-150">Свойство</span><span class="sxs-lookup"><span data-stu-id="2ae3a-150">Property</span></span> | <span data-ttu-id="2ae3a-151">Описание</span><span class="sxs-lookup"><span data-stu-id="2ae3a-151">Description</span></span> | <span data-ttu-id="2ae3a-152">Обязательно</span><span class="sxs-lookup"><span data-stu-id="2ae3a-152">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2ae3a-153">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="2ae3a-153">username</span></span> | <span data-ttu-id="2ae3a-154">Имя пользователя для доступа к конечной точке HTTP.</span><span class="sxs-lookup"><span data-stu-id="2ae3a-154">Username to access the HTTP endpoint.</span></span> | <span data-ttu-id="2ae3a-155">Да</span><span class="sxs-lookup"><span data-stu-id="2ae3a-155">Yes</span></span> |
| <span data-ttu-id="2ae3a-156">password</span><span class="sxs-lookup"><span data-stu-id="2ae3a-156">password</span></span> | <span data-ttu-id="2ae3a-157">Пароль пользователя, указанного в свойстве имя пользователя.</span><span class="sxs-lookup"><span data-stu-id="2ae3a-157">Password for the user (username).</span></span> | <span data-ttu-id="2ae3a-158">Да</span><span class="sxs-lookup"><span data-stu-id="2ae3a-158">Yes</span></span> |

#### <a name="example-using-basic-digest-or-windows-authentication"></a><span data-ttu-id="2ae3a-159">Пример: использование типов проверки подлинности Basic, Digest или Windows</span><span class="sxs-lookup"><span data-stu-id="2ae3a-159">Example: using Basic, Digest, or Windows authentication</span></span>

```JSON
{
    "name": "HttpLinkedService",
    "properties":
    {
        "type": "Http",
        "typeProperties":
        {
            "authenticationType": "basic",
            "url" : "https://en.wikipedia.org/wiki/",
            "userName": "user name",
            "password": "password"
        }
    }
}
```

### <a name="using-clientcertificate-authentication"></a><span data-ttu-id="2ae3a-160">Использование типа проверки подлинности ClientCertificate</span><span class="sxs-lookup"><span data-stu-id="2ae3a-160">Using ClientCertificate authentication</span></span>

<span data-ttu-id="2ae3a-161">Чтобы использовать базовую проверку подлинности, задайте для `authenticationType` значение `ClientCertificate` и укажите приведенные ниже свойства помимо универсальных свойств соединителя HTTP, которые описаны выше.</span><span class="sxs-lookup"><span data-stu-id="2ae3a-161">To use basic authentication, set `authenticationType` as `ClientCertificate`, and specify the following properties besides the HTTP connector generic ones introduced above:</span></span>

| <span data-ttu-id="2ae3a-162">Свойство</span><span class="sxs-lookup"><span data-stu-id="2ae3a-162">Property</span></span> | <span data-ttu-id="2ae3a-163">Описание</span><span class="sxs-lookup"><span data-stu-id="2ae3a-163">Description</span></span> | <span data-ttu-id="2ae3a-164">Обязательно</span><span class="sxs-lookup"><span data-stu-id="2ae3a-164">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2ae3a-165">embeddedCertData</span><span class="sxs-lookup"><span data-stu-id="2ae3a-165">embeddedCertData</span></span> | <span data-ttu-id="2ae3a-166">Содержимое двоичных данных файла обмена личной информацией (PFX-файла) с кодировкой Base64.</span><span class="sxs-lookup"><span data-stu-id="2ae3a-166">The Base64-encoded contents of binary data of the Personal Information Exchange (PFX) file.</span></span> | <span data-ttu-id="2ae3a-167">Должно быть указано одно из свойств: `embeddedCertData` или `certThumbprint`.</span><span class="sxs-lookup"><span data-stu-id="2ae3a-167">Specify either the `embeddedCertData` or `certThumbprint`.</span></span> |
| <span data-ttu-id="2ae3a-168">certThumbprint</span><span class="sxs-lookup"><span data-stu-id="2ae3a-168">certThumbprint</span></span> | <span data-ttu-id="2ae3a-169">Отпечаток сертификата, который был установлен в хранилище сертификатов на компьютере шлюза.</span><span class="sxs-lookup"><span data-stu-id="2ae3a-169">The thumbprint of the certificate that was installed on your gateway machine’s cert store.</span></span> <span data-ttu-id="2ae3a-170">Применимо, только когда копирование данных выполняется из локального источника HTTP.</span><span class="sxs-lookup"><span data-stu-id="2ae3a-170">Apply only when copying data from an on-premises HTTP source.</span></span> | <span data-ttu-id="2ae3a-171">Должно быть указано одно из свойств: `embeddedCertData` или `certThumbprint`.</span><span class="sxs-lookup"><span data-stu-id="2ae3a-171">Specify either the `embeddedCertData` or `certThumbprint`.</span></span> |
| <span data-ttu-id="2ae3a-172">password</span><span class="sxs-lookup"><span data-stu-id="2ae3a-172">password</span></span> | <span data-ttu-id="2ae3a-173">Пароль, связанный с сертификатом.</span><span class="sxs-lookup"><span data-stu-id="2ae3a-173">Password associated with the certificate.</span></span> | <span data-ttu-id="2ae3a-174">Нет</span><span class="sxs-lookup"><span data-stu-id="2ae3a-174">No</span></span> |

<span data-ttu-id="2ae3a-175">Если вы используете свойство `certThumbprint` для проверки подлинности, а сертификат установлен в личном хранилище локального компьютера, вам необходимо предоставить службе шлюза разрешение на чтение.</span><span class="sxs-lookup"><span data-stu-id="2ae3a-175">If you use `certThumbprint` for authentication and the certificate is installed in the personal store of the local computer, you need to grant the read permission to the gateway service:</span></span>

1. <span data-ttu-id="2ae3a-176">Запустите консоль управления (MMC).</span><span class="sxs-lookup"><span data-stu-id="2ae3a-176">Launch Microsoft Management Console (MMC).</span></span> <span data-ttu-id="2ae3a-177">Добавьте оснастку **Сертификаты**, которая связана с **локальным компьютером**.</span><span class="sxs-lookup"><span data-stu-id="2ae3a-177">Add the **Certificates** snap-in that targets the **Local Computer**.</span></span>
2. <span data-ttu-id="2ae3a-178">Разверните **Сертификаты**, **Личные**, а затем щелкните **Сертификаты**.</span><span class="sxs-lookup"><span data-stu-id="2ae3a-178">Expand **Certificates**, **Personal**, and click **Certificates**.</span></span>
3. <span data-ttu-id="2ae3a-179">Щелкните правой кнопкой мыши сертификат в личном хранилище, а затем выберите **Все задачи**->**Управление закрытыми ключами...**</span><span class="sxs-lookup"><span data-stu-id="2ae3a-179">Right-click the certificate from the personal store, and select **All Tasks**->**Manage Private Keys...**</span></span>
3. <span data-ttu-id="2ae3a-180">На вкладке **Безопасность** добавьте учетную запись пользователя, под которой запущена служба узла шлюза управления данными с доступом на чтение к сертификату.</span><span class="sxs-lookup"><span data-stu-id="2ae3a-180">On the **Security** tab, add the user account under which Data Management Gateway Host Service is running with the read access to the certificate.</span></span>  

#### <a name="example-using-client-certificate"></a><span data-ttu-id="2ae3a-181">Пример: использование сертификата клиента</span><span class="sxs-lookup"><span data-stu-id="2ae3a-181">Example: using client certificate</span></span>
<span data-ttu-id="2ae3a-182">Эта связанная служба связывает фабрику данных с локальным веб-сервером HTTP.</span><span class="sxs-lookup"><span data-stu-id="2ae3a-182">This linked service links your data factory to an on-premises HTTP web server.</span></span> <span data-ttu-id="2ae3a-183">Она использует сертификат клиента, установленный на компьютере со шлюзом управления данными.</span><span class="sxs-lookup"><span data-stu-id="2ae3a-183">It uses a client certificate that is installed on the machine with Data Management Gateway installed.</span></span>

```JSON
{
    "name": "HttpLinkedService",
    "properties":
    {
        "type": "Http",
        "typeProperties":
        {
            "authenticationType": "ClientCertificate",
            "url": "https://en.wikipedia.org/wiki/",
            "certThumbprint": "thumbprint of certificate",
            "gatewayName": "gateway name"

        }
    }
}
```

#### <a name="example-using-client-certificate-in-a-file"></a><span data-ttu-id="2ae3a-184">Пример: использование сертификата клиента в файле</span><span class="sxs-lookup"><span data-stu-id="2ae3a-184">Example: using client certificate in a file</span></span>
<span data-ttu-id="2ae3a-185">Эта связанная служба связывает фабрику данных с локальным веб-сервером HTTP.</span><span class="sxs-lookup"><span data-stu-id="2ae3a-185">This linked service links your data factory to an on-premises HTTP web server.</span></span> <span data-ttu-id="2ae3a-186">Она использует файл сертификата клиента на компьютере, где установлен шлюз управления данными.</span><span class="sxs-lookup"><span data-stu-id="2ae3a-186">It uses a client certificate file on the machine with Data Management Gateway installed.</span></span>

```JSON
{
    "name": "HttpLinkedService",
    "properties":
    {
        "type": "Http",
        "typeProperties":
        {
            "authenticationType": "ClientCertificate",
            "url": "https://en.wikipedia.org/wiki/",
            "embeddedCertData": "base64 encoded cert data",
            "password": "password of cert"
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="2ae3a-187">Свойства набора данных</span><span class="sxs-lookup"><span data-stu-id="2ae3a-187">Dataset properties</span></span>
<span data-ttu-id="2ae3a-188">Полный список разделов и свойств, используемых для определения наборов данных, см. в статье [Наборы данных](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="2ae3a-188">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="2ae3a-189">Разделы структуры, доступности и политики JSON набора данных одинаковы для всех типов наборов данных (SQL Azure, большие двоичные объекты Azure, таблицы Azure и т. д.).</span><span class="sxs-lookup"><span data-stu-id="2ae3a-189">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="2ae3a-190">Раздел **typeProperties** во всех типах наборов данных разный. В нем содержатся сведения о расположении данных в хранилище данных.</span><span class="sxs-lookup"><span data-stu-id="2ae3a-190">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="2ae3a-191">Раздел typeProperties для набора данных типа **Http** имеет следующие свойства.</span><span class="sxs-lookup"><span data-stu-id="2ae3a-191">The typeProperties section for dataset of type **Http** has the following properties</span></span>

| <span data-ttu-id="2ae3a-192">Свойство</span><span class="sxs-lookup"><span data-stu-id="2ae3a-192">Property</span></span> | <span data-ttu-id="2ae3a-193">Описание</span><span class="sxs-lookup"><span data-stu-id="2ae3a-193">Description</span></span> | <span data-ttu-id="2ae3a-194">Обязательно</span><span class="sxs-lookup"><span data-stu-id="2ae3a-194">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="2ae3a-195">type</span><span class="sxs-lookup"><span data-stu-id="2ae3a-195">type</span></span> | <span data-ttu-id="2ae3a-196">Тип набора данных.</span><span class="sxs-lookup"><span data-stu-id="2ae3a-196">Specified the type of the dataset.</span></span> <span data-ttu-id="2ae3a-197">Нужно задать значение `Http`.</span><span class="sxs-lookup"><span data-stu-id="2ae3a-197">must be set to `Http`.</span></span> | <span data-ttu-id="2ae3a-198">Да</span><span class="sxs-lookup"><span data-stu-id="2ae3a-198">Yes</span></span> |
| <span data-ttu-id="2ae3a-199">relativeUrl</span><span class="sxs-lookup"><span data-stu-id="2ae3a-199">relativeUrl</span></span> | <span data-ttu-id="2ae3a-200">Относительный URL-адрес ресурса, который содержит данные.</span><span class="sxs-lookup"><span data-stu-id="2ae3a-200">A relative URL to the resource that contains the data.</span></span> <span data-ttu-id="2ae3a-201">Если путь не задан, используется только URL-адрес, указанный в определении связанной службы.</span><span class="sxs-lookup"><span data-stu-id="2ae3a-201">When path is not specified, only the URL specified in the linked service definition is used.</span></span> <br><br> <span data-ttu-id="2ae3a-202">Чтобы создать динамический URL-адрес, можно использовать [функции и системные переменные фабрики данных](data-factory-functions-variables.md). Пример: "relativeUrl": "$$Text.Format('/my/report?month={0:yyyy}-{0:MM}&fmt=csv', SliceStart)".</span><span class="sxs-lookup"><span data-stu-id="2ae3a-202">To construct dynamic URL, you can use [Data Factory functions and system variables](data-factory-functions-variables.md), e.g. "relativeUrl": "$$Text.Format('/my/report?month={0:yyyy}-{0:MM}&fmt=csv', SliceStart)".</span></span> | <span data-ttu-id="2ae3a-203">Нет</span><span class="sxs-lookup"><span data-stu-id="2ae3a-203">No</span></span> |
| <span data-ttu-id="2ae3a-204">requestMethod</span><span class="sxs-lookup"><span data-stu-id="2ae3a-204">requestMethod</span></span> | <span data-ttu-id="2ae3a-205">Метод HTTP.</span><span class="sxs-lookup"><span data-stu-id="2ae3a-205">Http method.</span></span> <span data-ttu-id="2ae3a-206">Допустимые значения: **GET** или **POST**.</span><span class="sxs-lookup"><span data-stu-id="2ae3a-206">Allowed values are **GET** or **POST**.</span></span> | <span data-ttu-id="2ae3a-207">Нет.</span><span class="sxs-lookup"><span data-stu-id="2ae3a-207">No.</span></span> <span data-ttu-id="2ae3a-208">Значение по умолчанию — `GET`.</span><span class="sxs-lookup"><span data-stu-id="2ae3a-208">Default is `GET`.</span></span> |
| <span data-ttu-id="2ae3a-209">additionalHeaders</span><span class="sxs-lookup"><span data-stu-id="2ae3a-209">additionalHeaders</span></span> | <span data-ttu-id="2ae3a-210">Дополнительные заголовки HTTP-запроса.</span><span class="sxs-lookup"><span data-stu-id="2ae3a-210">Additional HTTP request headers.</span></span> | <span data-ttu-id="2ae3a-211">Нет</span><span class="sxs-lookup"><span data-stu-id="2ae3a-211">No</span></span> |
| <span data-ttu-id="2ae3a-212">requestBody</span><span class="sxs-lookup"><span data-stu-id="2ae3a-212">requestBody</span></span> | <span data-ttu-id="2ae3a-213">Текст HTTP-запроса.</span><span class="sxs-lookup"><span data-stu-id="2ae3a-213">Body for HTTP request.</span></span> | <span data-ttu-id="2ae3a-214">Нет</span><span class="sxs-lookup"><span data-stu-id="2ae3a-214">No</span></span> |
| <span data-ttu-id="2ae3a-215">свойства</span><span class="sxs-lookup"><span data-stu-id="2ae3a-215">format</span></span> | <span data-ttu-id="2ae3a-216">Если вы хотите просто **извлечь данные из конечной точки HTTP "как есть"** — без анализа, пропустите параметры форматирования.</span><span class="sxs-lookup"><span data-stu-id="2ae3a-216">If you want to simply **retrieve the data from HTTP endpoint as-is** without parsing it, skip this format settings.</span></span> <br><br> <span data-ttu-id="2ae3a-217">Поддерживаемые форматы для выполнения анализа содержимого ответа HTTP в процессе выполнения операции копирования: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat** и **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="2ae3a-217">If you want to parse the HTTP response content during copy, the following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="2ae3a-218">Дополнительные сведения см. в разделах о [текстовом формате](data-factory-supported-file-and-compression-formats.md#text-format), [формате Json](data-factory-supported-file-and-compression-formats.md#json-format), [формате Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [формате Orc](data-factory-supported-file-and-compression-formats.md#orc-format) и [ формате Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="2ae3a-218">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> |<span data-ttu-id="2ae3a-219">Нет</span><span class="sxs-lookup"><span data-stu-id="2ae3a-219">No</span></span> |
| <span data-ttu-id="2ae3a-220">compression</span><span class="sxs-lookup"><span data-stu-id="2ae3a-220">compression</span></span> | <span data-ttu-id="2ae3a-221">Укажите тип и уровень сжатия данных.</span><span class="sxs-lookup"><span data-stu-id="2ae3a-221">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="2ae3a-222">Поддерживаемые типы: **GZip**, **Deflate**, **BZip2** и **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="2ae3a-222">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="2ae3a-223">Поддерживаемые уровни: **Optimal** и **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="2ae3a-223">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="2ae3a-224">См. дополнительные сведения о [форматах файлов и сжатия данных в фабрике данных Azure](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="2ae3a-224">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="2ae3a-225">Нет</span><span class="sxs-lookup"><span data-stu-id="2ae3a-225">No</span></span> |

### <a name="example-using-the-get-default-method"></a><span data-ttu-id="2ae3a-226">Пример: использование метода GET (по умолчанию)</span><span class="sxs-lookup"><span data-stu-id="2ae3a-226">Example: using the GET (default) method</span></span>

```JSON
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "Http",
        "linkedServiceName": "HttpLinkedService",
        "typeProperties": {
            "relativeUrl": "XXX/test.xml",
            "additionalHeaders": "Connection: keep-alive\nUser-Agent: Mozilla/5.0\n"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}
```

### <a name="example-using-the-post-method"></a><span data-ttu-id="2ae3a-227">Пример: использование метода POST</span><span class="sxs-lookup"><span data-stu-id="2ae3a-227">Example: using the POST method</span></span>

```JSON
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "Http",
        "linkedServiceName": "HttpLinkedService",
        "typeProperties": {
            "relativeUrl": "/XXX/test.xml",
           "requestMethod": "Post",
            "requestBody": "body for POST HTTP request"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}
```

## <a name="copy-activity-properties"></a><span data-ttu-id="2ae3a-228">Свойства действия копирования</span><span class="sxs-lookup"><span data-stu-id="2ae3a-228">Copy activity properties</span></span>
<span data-ttu-id="2ae3a-229">Полный список разделов и свойств, используемых для определения действий, см. в статье [Создание конвейеров](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="2ae3a-229">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="2ae3a-230">Свойства (включая имя, описание, входные и выходные таблицы, политику и т. д.) доступны для всех типов действий.</span><span class="sxs-lookup"><span data-stu-id="2ae3a-230">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="2ae3a-231">С другой стороны, свойства, доступные в разделе **typeProperties** действия, зависят от конкретного типа действия.</span><span class="sxs-lookup"><span data-stu-id="2ae3a-231">Properties available in the **typeProperties** section of the activity on the other hand vary with each activity type.</span></span> <span data-ttu-id="2ae3a-232">Для действия копирования они различаются в зависимости от типов источников и приемников.</span><span class="sxs-lookup"><span data-stu-id="2ae3a-232">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="2ae3a-233">В настоящее время, если источник в действии копирования относится к типу **HttpSource**, то поддерживаются следующие свойства.</span><span class="sxs-lookup"><span data-stu-id="2ae3a-233">Currently, when the source in copy activity is of type **HttpSource**, the following properties are supported.</span></span>

| <span data-ttu-id="2ae3a-234">Свойство</span><span class="sxs-lookup"><span data-stu-id="2ae3a-234">Property</span></span> | <span data-ttu-id="2ae3a-235">Описание</span><span class="sxs-lookup"><span data-stu-id="2ae3a-235">Description</span></span> | <span data-ttu-id="2ae3a-236">Обязательно</span><span class="sxs-lookup"><span data-stu-id="2ae3a-236">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="2ae3a-237">httpRequestTimeout</span><span class="sxs-lookup"><span data-stu-id="2ae3a-237">httpRequestTimeout</span></span> | <span data-ttu-id="2ae3a-238">Время ожидания ответа для HTTP-запроса.</span><span class="sxs-lookup"><span data-stu-id="2ae3a-238">The timeout (TimeSpan) for the HTTP request to get a response.</span></span> <span data-ttu-id="2ae3a-239">Это интервал времени для получения ответа, а не считывания данных ответа.</span><span class="sxs-lookup"><span data-stu-id="2ae3a-239">It is the timeout to get a response, not the timeout to read response data.</span></span> | <span data-ttu-id="2ae3a-240">Нет.</span><span class="sxs-lookup"><span data-stu-id="2ae3a-240">No.</span></span> <span data-ttu-id="2ae3a-241">Значение по умолчанию  — 00:01:40.</span><span class="sxs-lookup"><span data-stu-id="2ae3a-241">Default value: 00:01:40</span></span> |

## <a name="supported-file-and-compression-formats"></a><span data-ttu-id="2ae3a-242">Поддерживаемые форматы файлов и сжатия</span><span class="sxs-lookup"><span data-stu-id="2ae3a-242">Supported file and compression formats</span></span>
<span data-ttu-id="2ae3a-243">Дополнительные сведения см. в статье [Форматы файлов и сжатия данных, поддерживаемые фабрикой данных Azure](data-factory-supported-file-and-compression-formats.md).</span><span class="sxs-lookup"><span data-stu-id="2ae3a-243">See [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article on details.</span></span>

## <a name="json-examples"></a><span data-ttu-id="2ae3a-244">Примеры определений JSON</span><span class="sxs-lookup"><span data-stu-id="2ae3a-244">JSON examples</span></span>
<span data-ttu-id="2ae3a-245">Ниже приведены примеры с определениями JSON, которые можно использовать для создания конвейера с помощью [портала Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) или [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="2ae3a-245">The following example provide sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="2ae3a-246">Вы узнаете, как копировать данные из источника HTTP в хранилище BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="2ae3a-246">They show how to copy data from HTTP source to Azure Blob Storage.</span></span> <span data-ttu-id="2ae3a-247">Тем не менее данные можно копировать **непосредственно** из любых источников в любой указанный [здесь](data-factory-data-movement-activities.md#supported-data-stores-and-formats) приемник. Это делается с помощью действия копирования в фабрике данных Azure.</span><span class="sxs-lookup"><span data-stu-id="2ae3a-247">However, data can be copied **directly** from any of sources to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>

### <a name="example-copy-data-from-http-source-to-azure-blob-storage"></a><span data-ttu-id="2ae3a-248">Пример: копирование данных из источника HTTP в хранилище BLOB-объектов Azure</span><span class="sxs-lookup"><span data-stu-id="2ae3a-248">Example: Copy data from HTTP source to Azure Blob Storage</span></span>
<span data-ttu-id="2ae3a-249">Решение фабрики данных для этого примера содержит следующие сущности фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="2ae3a-249">The Data Factory solution for this sample contains the following Data Factory entities:</span></span>

1. <span data-ttu-id="2ae3a-250">Связанная служба типа [HTTP](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="2ae3a-250">A linked service of type [HTTP](#linked-service-properties).</span></span>
2. <span data-ttu-id="2ae3a-251">Связанная служба типа [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="2ae3a-251">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="2ae3a-252">Входной [набор данных](data-factory-create-datasets.md) типа [Http](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="2ae3a-252">An input [dataset](data-factory-create-datasets.md) of type [Http](#dataset-properties).</span></span>
4. <span data-ttu-id="2ae3a-253">Выходной [набор данных](data-factory-create-datasets.md) типа [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="2ae3a-253">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="2ae3a-254">[Конвейер](data-factory-create-pipelines.md) с действием копирования, в котором используются [HttpSource](#copy-activity-properties) и [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="2ae3a-254">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [HttpSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="2ae3a-255">В этом примере данные из источника HTTP каждый час копируются в большой двоичный объект Azure.</span><span class="sxs-lookup"><span data-stu-id="2ae3a-255">The sample copies data from an HTTP source to an Azure blob every hour.</span></span> <span data-ttu-id="2ae3a-256">Используемые в этих примерах свойства JSON описаны в разделах, следующих за примерами.</span><span class="sxs-lookup"><span data-stu-id="2ae3a-256">The JSON properties used in these samples are described in sections following the samples.</span></span>

### <a name="http-linked-service"></a><span data-ttu-id="2ae3a-257">Связанная служба HTTP</span><span class="sxs-lookup"><span data-stu-id="2ae3a-257">HTTP linked service</span></span>
<span data-ttu-id="2ae3a-258">В этом примере используется связанная служба HTTP с анонимной проверкой подлинности.</span><span class="sxs-lookup"><span data-stu-id="2ae3a-258">This example uses the HTTP linked service with anonymous authentication.</span></span> <span data-ttu-id="2ae3a-259">Сведения о возможных типах аутентификации см. в разделе о [связанной службе HTTP](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="2ae3a-259">See [HTTP linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

```JSON
{
    "name": "HttpLinkedService",
    "properties":
    {
        "type": "Http",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "url" : "https://en.wikipedia.org/wiki/"
        }
    }
}
```

### <a name="azure-storage-linked-service"></a><span data-ttu-id="2ae3a-260">Связанная служба хранения Azure</span><span class="sxs-lookup"><span data-stu-id="2ae3a-260">Azure Storage linked service</span></span>

```JSON
{
  "name": "AzureStorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```

### <a name="http-input-dataset"></a><span data-ttu-id="2ae3a-261">Входной набор данных HTTP</span><span class="sxs-lookup"><span data-stu-id="2ae3a-261">HTTP input dataset</span></span>
<span data-ttu-id="2ae3a-262">Если для параметра **external** задать значение **true**, то фабрика данных воспримет этот набор данных как внешний, который создан не в результате какого-либо действия в фабрике данных.</span><span class="sxs-lookup"><span data-stu-id="2ae3a-262">Setting **external** to **true** informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

```JSON
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "Http",
        "linkedServiceName": "HttpLinkedService",
        "typeProperties": {
            "relativeUrl": "$$Text.Format('/my/report?month={0:yyyy}-{0:MM}&fmt=csv', SliceStart)",
            "additionalHeaders": "Connection: keep-alive\nUser-Agent: Mozilla/5.0\n"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}

```

### <a name="azure-blob-output-dataset"></a><span data-ttu-id="2ae3a-263">Выходной набор данных BLOB-объекта Azure</span><span class="sxs-lookup"><span data-stu-id="2ae3a-263">Azure Blob output dataset</span></span>

<span data-ttu-id="2ae3a-264">Данные записываются в новый BLOB-объект каждый час (frequency: hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="2ae3a-264">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span>

```JSON
{
    "name": "AzureBlobOutput",
    "properties":
    {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties":
        {
            "folderPath": "adfgetstarted/Movies"
        },
        "availability":
        {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

### <a name="pipeline-with-copy-activity"></a><span data-ttu-id="2ae3a-265">Конвейер с действием копирования</span><span class="sxs-lookup"><span data-stu-id="2ae3a-265">Pipeline with Copy activity</span></span>

<span data-ttu-id="2ae3a-266">Конвейер содержит действие копирования, которое использует входной и выходной наборы данных и выполняется каждый час.</span><span class="sxs-lookup"><span data-stu-id="2ae3a-266">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="2ae3a-267">В определении конвейера JSON для типа **source** установлено значение **HttpSource**, а для типа **sink** — значение **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="2ae3a-267">In the pipeline JSON definition, the **source** type is set to **HttpSource** and **sink** type is set to **BlobSink**.</span></span>

<span data-ttu-id="2ae3a-268">Список свойств, поддерживаемых HttpSource, см. [здесь](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="2ae3a-268">See [HttpSource](#copy-activity-properties) for the list of properties supported by the HttpSource.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "HttpSourceToAzureBlob",
        "description": "Copy from an HTTP source to an Azure blob",
        "type": "Copy",
        "inputs": [
          {
            "name": "HttpSourceDataInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "HttpSource"
          },
          "sink": {
            "type": "BlobSink"
          }
        },
       "scheduler": {
          "frequency": "Hour",
          "interval": 1
        },
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "OldestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
      ]
   }
}
```

> [!NOTE]
> <span data-ttu-id="2ae3a-269">Сведения о сопоставлении столбцов в наборе данных, используемом в качестве источника, со столбцами в приемнике см. в [этой статье](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="2ae3a-269">To map columns from source dataset to columns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="2ae3a-270">Производительность и настройка</span><span class="sxs-lookup"><span data-stu-id="2ae3a-270">Performance and Tuning</span></span>
<span data-ttu-id="2ae3a-271">Ознакомьтесь со статьей [Руководство по настройке производительности действия копирования](data-factory-copy-activity-performance.md), в которой описываются ключевые факторы, влияющие на производительность перемещения данных (действие копирования) в фабрике данных Azure, и различные способы оптимизации этого процесса.</span><span class="sxs-lookup"><span data-stu-id="2ae3a-271">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
