---
title: "aaaMove данные из источника HTTP - Azure | Документы Microsoft"
description: "Дополнительные сведения о том, как toomove из локальной или облачной HTTP источника с помощью фабрики данных Azure."
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
ms.openlocfilehash: e39b9cbff870aef4be91938cacff39a2fd12d64a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-an-http-source-using-azure-data-factory"></a><span data-ttu-id="a1c93-103">Перемещение данных из источника HTTP с помощью фабрики данных Azure</span><span class="sxs-lookup"><span data-stu-id="a1c93-103">Move data from an HTTP source using Azure Data Factory</span></span>
<span data-ttu-id="a1c93-104">В этой статье рассматриваются как hello toouse действие копирования в данных toomove фабрики данных Azure из tooa конечной точки HTTP на локальная/облачная поддерживается приемника хранилища данных.</span><span class="sxs-lookup"><span data-stu-id="a1c93-104">This article outlines how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises/cloud HTTP endpoint tooa supported sink data store.</span></span> <span data-ttu-id="a1c93-105">Эта статья основана на hello [действия перемещения данных](data-factory-data-movement-activities.md) статьи, дан обзор перемещения данных на копии действия и hello список хранилищ данных, поддерживаемые в качестве источников и приемников.</span><span class="sxs-lookup"><span data-stu-id="a1c93-105">This article builds on hello [data movement activities](data-factory-data-movement-activities.md) article that presents a general overview of data movement with copy activity and hello list of data stores supported as sources/sinks.</span></span>

<span data-ttu-id="a1c93-106">Фабрика данных в настоящее время поддерживает только перемещение данных из HTTP источника tooother хранилищ данных, но не перемещения данных из других данных хранит назначения tooan HTTP.</span><span class="sxs-lookup"><span data-stu-id="a1c93-106">Data factory currently supports only moving data from an HTTP source tooother data stores, but not moving data from other data stores tooan HTTP destination.</span></span>

## <a name="supported-scenarios-and-authentication-types"></a><span data-ttu-id="a1c93-107">Поддерживаемые сценарии и типы аутентификации</span><span class="sxs-lookup"><span data-stu-id="a1c93-107">Supported scenarios and authentication types</span></span>
<span data-ttu-id="a1c93-108">Можно использовать эти данные tooretrieve HTTP соединителя с **облачной и локальной конечной точки HTTP/s** по протоколу HTTP **получить** или **POST** метод.</span><span class="sxs-lookup"><span data-stu-id="a1c93-108">You can use this HTTP connector tooretrieve data from **both cloud and on-premises HTTP/s endpoint** by using HTTP **GET** or **POST** method.</span></span> <span data-ttu-id="a1c93-109">поддерживаются следующие типы проверки подлинности Hello: **Anonymous**, **основные**, **дайджест**, **Windows**, и  **ClientCertificate**.</span><span class="sxs-lookup"><span data-stu-id="a1c93-109">hello following authentication types are supported: **Anonymous**, **Basic**, **Digest**, **Windows**, and **ClientCertificate**.</span></span> <span data-ttu-id="a1c93-110">Обратите внимание, hello отличие от этого соединителя hello [соединитель таблицы веб](data-factory-web-table-connector.md) является: hello последний является таблица используется tooextract содержимого с веб-страницы HTML.</span><span class="sxs-lookup"><span data-stu-id="a1c93-110">Note hello difference between this connector and hello [Web table connector](data-factory-web-table-connector.md) is: hello latter is used tooextract table content from web HTML page.</span></span>

<span data-ttu-id="a1c93-111">При копировании данных из локальной конечной точки HTTP, необходимо установить шлюз управления данными в hello в локальной среде и ВМ Azure.</span><span class="sxs-lookup"><span data-stu-id="a1c93-111">When copying data from an on-premises HTTP endpoint, you need install a Data Management Gateway in hello on-premises environment/Azure VM.</span></span> <span data-ttu-id="a1c93-112">В разделе [перемещение данных между расположениями локальных и облачных](data-factory-move-data-between-onprem-and-cloud.md) toolearn статьи о шлюз управления данными и пошаговые инструкции по настройке шлюза hello.</span><span class="sxs-lookup"><span data-stu-id="a1c93-112">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article toolearn about Data Management Gateway and step-by-step instructions on setting up hello gateway.</span></span>

## <a name="getting-started"></a><span data-ttu-id="a1c93-113">Приступая к работе</span><span class="sxs-lookup"><span data-stu-id="a1c93-113">Getting started</span></span>
<span data-ttu-id="a1c93-114">Вы можете создать конвейер с действием копирования, которое перемещает данные из источника HTTP с помощью разных инструментов и интерфейсов API.</span><span class="sxs-lookup"><span data-stu-id="a1c93-114">You can create a pipeline with a copy activity that moves data from an HTTP source by using different tools/APIs.</span></span>

- <span data-ttu-id="a1c93-115">toocreate простым способом Hello конвейера — toouse hello **мастер копирования**.</span><span class="sxs-lookup"><span data-stu-id="a1c93-115">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="a1c93-116">В разделе [учебника: создать конвейер, с помощью мастера копирования](data-factory-copy-data-wizard-tutorial.md) краткое Пошаговое руководство по создание с помощью мастера данных копирования hello конвейера.</span><span class="sxs-lookup"><span data-stu-id="a1c93-116">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

- <span data-ttu-id="a1c93-117">Также можно использовать следующие средства toocreate конвейера hello: **портал Azure**, **Visual Studio**, **Azure PowerShell**, **шаблона диспетчера ресурсов Azure** , **.NET API**, и **API-интерфейса REST**.</span><span class="sxs-lookup"><span data-stu-id="a1c93-117">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="a1c93-118">В разделе [учебника действия копирования](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) для toocreate пошаговые инструкции конвейера с помощью операции копирования.</span><span class="sxs-lookup"><span data-stu-id="a1c93-118">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> <span data-ttu-id="a1c93-119">JSON выбирает toocopy данные из источника HTTP tooAzure хранилища больших двоичных объектов, см. в разделе [JSON примеры](#json-examples) части этой статьи.</span><span class="sxs-lookup"><span data-stu-id="a1c93-119">For JSON samples toocopy data from HTTP source tooAzure Blob Storage, see [JSON examples](#json-examples) section of this articles.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="a1c93-120">Свойства связанной службы</span><span class="sxs-lookup"><span data-stu-id="a1c93-120">Linked service properties</span></span>
<span data-ttu-id="a1c93-121">Hello в следующей таблице приводится описание службы конкретных tooHTTP связанные элементы JSON.</span><span class="sxs-lookup"><span data-stu-id="a1c93-121">hello following table provides description for JSON elements specific tooHTTP linked service.</span></span>

| <span data-ttu-id="a1c93-122">Свойство</span><span class="sxs-lookup"><span data-stu-id="a1c93-122">Property</span></span> | <span data-ttu-id="a1c93-123">Описание</span><span class="sxs-lookup"><span data-stu-id="a1c93-123">Description</span></span> | <span data-ttu-id="a1c93-124">Обязательно</span><span class="sxs-lookup"><span data-stu-id="a1c93-124">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a1c93-125">type</span><span class="sxs-lookup"><span data-stu-id="a1c93-125">type</span></span> | <span data-ttu-id="a1c93-126">свойство типа Hello должно быть присвоено: `Http`.</span><span class="sxs-lookup"><span data-stu-id="a1c93-126">hello type property must be set to: `Http`.</span></span> | <span data-ttu-id="a1c93-127">Да</span><span class="sxs-lookup"><span data-stu-id="a1c93-127">Yes</span></span> |
| <span data-ttu-id="a1c93-128">url</span><span class="sxs-lookup"><span data-stu-id="a1c93-128">url</span></span> | <span data-ttu-id="a1c93-129">Базовый URL-адрес toohello веб-сервера</span><span class="sxs-lookup"><span data-stu-id="a1c93-129">Base URL toohello Web Server</span></span> | <span data-ttu-id="a1c93-130">Да</span><span class="sxs-lookup"><span data-stu-id="a1c93-130">Yes</span></span> |
| <span data-ttu-id="a1c93-131">authenticationType</span><span class="sxs-lookup"><span data-stu-id="a1c93-131">authenticationType</span></span> | <span data-ttu-id="a1c93-132">Указывает тип проверки подлинности hello.</span><span class="sxs-lookup"><span data-stu-id="a1c93-132">Specifies hello authentication type.</span></span> <span data-ttu-id="a1c93-133">Допустимые значения: **Anonymous**, **Basic**, **Digest**, **Windows** и **ClientCertificate**.</span><span class="sxs-lookup"><span data-stu-id="a1c93-133">Allowed values are: **Anonymous**, **Basic**, **Digest**, **Windows**, **ClientCertificate**.</span></span> <br><br> <span data-ttu-id="a1c93-134">Относятся toosections под этой таблицей в дополнительные свойства и примерами JSON для этих типов проверки подлинности, соответственно.</span><span class="sxs-lookup"><span data-stu-id="a1c93-134">Refer toosections below this table on more properties and JSON samples for those authentication types respectively.</span></span> | <span data-ttu-id="a1c93-135">Да</span><span class="sxs-lookup"><span data-stu-id="a1c93-135">Yes</span></span> |
| <span data-ttu-id="a1c93-136">enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="a1c93-136">enableServerCertificateValidation</span></span> | <span data-ttu-id="a1c93-137">Укажите ли tooenable сервера SSL сертификата проверки, если источником является HTTPS веб-сервера</span><span class="sxs-lookup"><span data-stu-id="a1c93-137">Specify whether tooenable server SSL certificate validation if source is HTTPS Web Server</span></span> | <span data-ttu-id="a1c93-138">Нет. Значение по умолчанию — true.</span><span class="sxs-lookup"><span data-stu-id="a1c93-138">No, default is true</span></span> |
| <span data-ttu-id="a1c93-139">gatewayName</span><span class="sxs-lookup"><span data-stu-id="a1c93-139">gatewayName</span></span> | <span data-ttu-id="a1c93-140">Имя tooan tooconnect шлюз управления данными hello локального источника HTTP.</span><span class="sxs-lookup"><span data-stu-id="a1c93-140">Name of hello Data Management Gateway tooconnect tooan on-premises HTTP source.</span></span> | <span data-ttu-id="a1c93-141">Да, если копирование выполняется из локального источника HTTP.</span><span class="sxs-lookup"><span data-stu-id="a1c93-141">Yes if copying data from an on-premises HTTP source.</span></span> |
| <span data-ttu-id="a1c93-142">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="a1c93-142">encryptedCredential</span></span> | <span data-ttu-id="a1c93-143">Конечная точка HTTP hello tooaccess зашифрованных учетных данных.</span><span class="sxs-lookup"><span data-stu-id="a1c93-143">Encrypted credential tooaccess hello HTTP endpoint.</span></span> <span data-ttu-id="a1c93-144">Автоматически сгенерированный при настройке hello сведения для проверки подлинности в копирования мастера или hello ClickOnce всплывающее диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="a1c93-144">Auto-generated when you configure hello authentication information in copy wizard or hello ClickOnce popup dialog.</span></span> | <span data-ttu-id="a1c93-145">Нет.</span><span class="sxs-lookup"><span data-stu-id="a1c93-145">No.</span></span> <span data-ttu-id="a1c93-146">Применимо, только когда копирование данных выполняется с локального HTTP-сервера.</span><span class="sxs-lookup"><span data-stu-id="a1c93-146">Apply only when copying data from an on-premises HTTP server.</span></span> |

<span data-ttu-id="a1c93-147">В разделе [перемещения данных между локальным источникам и hello облако с помощью шлюза управления данными](data-factory-move-data-between-onprem-and-cloud.md) подробные сведения о задании учетных данных для источника данных соединителя HTTP в локальной среде.</span><span class="sxs-lookup"><span data-stu-id="a1c93-147">See [Move data between on-premises sources and hello cloud with Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md) for details about setting credentials for on-premises HTTP connector data source.</span></span>

### <a name="using-basic-digest-or-windows-authentication"></a><span data-ttu-id="a1c93-148">Использование типов проверки подлинности Basic, Digest или Windows</span><span class="sxs-lookup"><span data-stu-id="a1c93-148">Using Basic, Digest, or Windows authentication</span></span>

<span data-ttu-id="a1c93-149">Задать `authenticationType` как `Basic`, `Digest`, или `Windows`и укажите следующие свойства, кроме hello HTTP соединителя универсального историй, представленные выше hello:</span><span class="sxs-lookup"><span data-stu-id="a1c93-149">Set `authenticationType` as `Basic`, `Digest`, or `Windows`, and specify hello following properties besides hello HTTP connector generic ones introduced above:</span></span>

| <span data-ttu-id="a1c93-150">Свойство</span><span class="sxs-lookup"><span data-stu-id="a1c93-150">Property</span></span> | <span data-ttu-id="a1c93-151">Описание</span><span class="sxs-lookup"><span data-stu-id="a1c93-151">Description</span></span> | <span data-ttu-id="a1c93-152">Обязательно</span><span class="sxs-lookup"><span data-stu-id="a1c93-152">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a1c93-153">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="a1c93-153">username</span></span> | <span data-ttu-id="a1c93-154">Конечная точка HTTP hello tooaccess имя пользователя.</span><span class="sxs-lookup"><span data-stu-id="a1c93-154">Username tooaccess hello HTTP endpoint.</span></span> | <span data-ttu-id="a1c93-155">Да</span><span class="sxs-lookup"><span data-stu-id="a1c93-155">Yes</span></span> |
| <span data-ttu-id="a1c93-156">пароль</span><span class="sxs-lookup"><span data-stu-id="a1c93-156">password</span></span> | <span data-ttu-id="a1c93-157">Пароль для пользователя hello (имя пользователя).</span><span class="sxs-lookup"><span data-stu-id="a1c93-157">Password for hello user (username).</span></span> | <span data-ttu-id="a1c93-158">Да</span><span class="sxs-lookup"><span data-stu-id="a1c93-158">Yes</span></span> |

#### <a name="example-using-basic-digest-or-windows-authentication"></a><span data-ttu-id="a1c93-159">Пример: использование типов проверки подлинности Basic, Digest или Windows</span><span class="sxs-lookup"><span data-stu-id="a1c93-159">Example: using Basic, Digest, or Windows authentication</span></span>

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

### <a name="using-clientcertificate-authentication"></a><span data-ttu-id="a1c93-160">Использование типа проверки подлинности ClientCertificate</span><span class="sxs-lookup"><span data-stu-id="a1c93-160">Using ClientCertificate authentication</span></span>

<span data-ttu-id="a1c93-161">Задайте обычную проверку подлинности toouse `authenticationType` как `ClientCertificate`и укажите следующие свойства, кроме hello HTTP соединителя универсального историй, представленные выше hello:</span><span class="sxs-lookup"><span data-stu-id="a1c93-161">toouse basic authentication, set `authenticationType` as `ClientCertificate`, and specify hello following properties besides hello HTTP connector generic ones introduced above:</span></span>

| <span data-ttu-id="a1c93-162">Свойство</span><span class="sxs-lookup"><span data-stu-id="a1c93-162">Property</span></span> | <span data-ttu-id="a1c93-163">Описание</span><span class="sxs-lookup"><span data-stu-id="a1c93-163">Description</span></span> | <span data-ttu-id="a1c93-164">Обязательно</span><span class="sxs-lookup"><span data-stu-id="a1c93-164">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a1c93-165">embeddedCertData</span><span class="sxs-lookup"><span data-stu-id="a1c93-165">embeddedCertData</span></span> | <span data-ttu-id="a1c93-166">Hello кодировке Base64 содержимое двоичных данных hello файл обмена личной информацией (PFX).</span><span class="sxs-lookup"><span data-stu-id="a1c93-166">hello Base64-encoded contents of binary data of hello Personal Information Exchange (PFX) file.</span></span> | <span data-ttu-id="a1c93-167">Укажите либо hello `embeddedCertData` или `certThumbprint`.</span><span class="sxs-lookup"><span data-stu-id="a1c93-167">Specify either hello `embeddedCertData` or `certThumbprint`.</span></span> |
| <span data-ttu-id="a1c93-168">certThumbprint</span><span class="sxs-lookup"><span data-stu-id="a1c93-168">certThumbprint</span></span> | <span data-ttu-id="a1c93-169">Здравствуйте, отпечаток сертификата hello, который был установлен в хранилище сертификатов на компьютере шлюза.</span><span class="sxs-lookup"><span data-stu-id="a1c93-169">hello thumbprint of hello certificate that was installed on your gateway machine’s cert store.</span></span> <span data-ttu-id="a1c93-170">Применимо, только когда копирование данных выполняется из локального источника HTTP.</span><span class="sxs-lookup"><span data-stu-id="a1c93-170">Apply only when copying data from an on-premises HTTP source.</span></span> | <span data-ttu-id="a1c93-171">Укажите либо hello `embeddedCertData` или `certThumbprint`.</span><span class="sxs-lookup"><span data-stu-id="a1c93-171">Specify either hello `embeddedCertData` or `certThumbprint`.</span></span> |
| <span data-ttu-id="a1c93-172">пароль</span><span class="sxs-lookup"><span data-stu-id="a1c93-172">password</span></span> | <span data-ttu-id="a1c93-173">Пароль, связанный с сертификатом hello.</span><span class="sxs-lookup"><span data-stu-id="a1c93-173">Password associated with hello certificate.</span></span> | <span data-ttu-id="a1c93-174">Нет</span><span class="sxs-lookup"><span data-stu-id="a1c93-174">No</span></span> |

<span data-ttu-id="a1c93-175">При использовании `certThumbprint` необходимо для проверки подлинности и hello сертификат должен быть установлен в личном хранилище локального компьютера hello hello, служба шлюза toohello разрешение на чтение hello toogrant:</span><span class="sxs-lookup"><span data-stu-id="a1c93-175">If you use `certThumbprint` for authentication and hello certificate is installed in hello personal store of hello local computer, you need toogrant hello read permission toohello gateway service:</span></span>

1. <span data-ttu-id="a1c93-176">Запустите консоль управления (MMC).</span><span class="sxs-lookup"><span data-stu-id="a1c93-176">Launch Microsoft Management Console (MMC).</span></span> <span data-ttu-id="a1c93-177">Добавить hello **сертификаты** этой цели hello оснастки **локального компьютера**.</span><span class="sxs-lookup"><span data-stu-id="a1c93-177">Add hello **Certificates** snap-in that targets hello **Local Computer**.</span></span>
2. <span data-ttu-id="a1c93-178">Разверните **Сертификаты**, **Личные**, а затем щелкните **Сертификаты**.</span><span class="sxs-lookup"><span data-stu-id="a1c93-178">Expand **Certificates**, **Personal**, and click **Certificates**.</span></span>
3. <span data-ttu-id="a1c93-179">Щелкните правой кнопкой мыши hello сертификат из личного хранилища hello и выберите **все задачи**->**управление закрытыми ключами...**</span><span class="sxs-lookup"><span data-stu-id="a1c93-179">Right-click hello certificate from hello personal store, and select **All Tasks**->**Manage Private Keys...**</span></span>
3. <span data-ttu-id="a1c93-180">На hello **безопасности** добавьте учетную запись пользователя hello, под которой выполняется служба узла шлюза управления данными с сертификатом toohello hello доступ для чтения.</span><span class="sxs-lookup"><span data-stu-id="a1c93-180">On hello **Security** tab, add hello user account under which Data Management Gateway Host Service is running with hello read access toohello certificate.</span></span>  

#### <a name="example-using-client-certificate"></a><span data-ttu-id="a1c93-181">Пример: использование сертификата клиента</span><span class="sxs-lookup"><span data-stu-id="a1c93-181">Example: using client certificate</span></span>
<span data-ttu-id="a1c93-182">Ссылки на службы связанных данных фабрики tooan локальной HTTP веб-сервере.</span><span class="sxs-lookup"><span data-stu-id="a1c93-182">This linked service links your data factory tooan on-premises HTTP web server.</span></span> <span data-ttu-id="a1c93-183">Она использует сертификат клиента, которая устанавливается на компьютере hello с установлен шлюз управления данными.</span><span class="sxs-lookup"><span data-stu-id="a1c93-183">It uses a client certificate that is installed on hello machine with Data Management Gateway installed.</span></span>

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

#### <a name="example-using-client-certificate-in-a-file"></a><span data-ttu-id="a1c93-184">Пример: использование сертификата клиента в файле</span><span class="sxs-lookup"><span data-stu-id="a1c93-184">Example: using client certificate in a file</span></span>
<span data-ttu-id="a1c93-185">Ссылки на службы связанных данных фабрики tooan локальной HTTP веб-сервере.</span><span class="sxs-lookup"><span data-stu-id="a1c93-185">This linked service links your data factory tooan on-premises HTTP web server.</span></span> <span data-ttu-id="a1c93-186">Он использует файл сертификата клиента на компьютере hello с установлен шлюз управления данными.</span><span class="sxs-lookup"><span data-stu-id="a1c93-186">It uses a client certificate file on hello machine with Data Management Gateway installed.</span></span>

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

## <a name="dataset-properties"></a><span data-ttu-id="a1c93-187">Свойства набора данных</span><span class="sxs-lookup"><span data-stu-id="a1c93-187">Dataset properties</span></span>
<span data-ttu-id="a1c93-188">Полный список разделов и свойства, доступные для определения наборов данных, см. в разделе hello [Создание наборов данных](data-factory-create-datasets.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="a1c93-188">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="a1c93-189">Разделы структуры, доступности и политики JSON набора данных одинаковы для всех типов наборов данных (SQL Azure, большие двоичные объекты Azure, таблицы Azure и т. д.).</span><span class="sxs-lookup"><span data-stu-id="a1c93-189">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="a1c93-190">Hello **typeProperties** раздел отличается для каждого типа набора данных и предоставляет информацию о местоположении hello hello данных в хранилище данных hello.</span><span class="sxs-lookup"><span data-stu-id="a1c93-190">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="a1c93-191">Hello typeProperties статьи для набора данных типа **Http** имеет следующие свойства hello</span><span class="sxs-lookup"><span data-stu-id="a1c93-191">hello typeProperties section for dataset of type **Http** has hello following properties</span></span>

| <span data-ttu-id="a1c93-192">Свойство</span><span class="sxs-lookup"><span data-stu-id="a1c93-192">Property</span></span> | <span data-ttu-id="a1c93-193">Описание</span><span class="sxs-lookup"><span data-stu-id="a1c93-193">Description</span></span> | <span data-ttu-id="a1c93-194">Обязательно</span><span class="sxs-lookup"><span data-stu-id="a1c93-194">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="a1c93-195">type</span><span class="sxs-lookup"><span data-stu-id="a1c93-195">type</span></span> | <span data-ttu-id="a1c93-196">Указанный тип hello hello набора данных.</span><span class="sxs-lookup"><span data-stu-id="a1c93-196">Specified hello type of hello dataset.</span></span> <span data-ttu-id="a1c93-197">необходимо задать слишком`Http`.</span><span class="sxs-lookup"><span data-stu-id="a1c93-197">must be set too`Http`.</span></span> | <span data-ttu-id="a1c93-198">Да</span><span class="sxs-lookup"><span data-stu-id="a1c93-198">Yes</span></span> |
| <span data-ttu-id="a1c93-199">relativeUrl</span><span class="sxs-lookup"><span data-stu-id="a1c93-199">relativeUrl</span></span> | <span data-ttu-id="a1c93-200">Относительный URL-адрес toohello ресурс, содержащий данные hello.</span><span class="sxs-lookup"><span data-stu-id="a1c93-200">A relative URL toohello resource that contains hello data.</span></span> <span data-ttu-id="a1c93-201">Если путь не указан, используется только hello URL-адрес, указанный в определении службы hello связаны.</span><span class="sxs-lookup"><span data-stu-id="a1c93-201">When path is not specified, only hello URL specified in hello linked service definition is used.</span></span> <br><br> <span data-ttu-id="a1c93-202">tooconstruct динамического URL-адреса можно использовать [функции фабрики данных, а системные переменные](data-factory-functions-variables.md), например «relativeUrl»: «$$Text.Format ("/ my/отчета? месяц = {0: yyyy}-{0:MM} & fmt = csv", SliceStart)».</span><span class="sxs-lookup"><span data-stu-id="a1c93-202">tooconstruct dynamic URL, you can use [Data Factory functions and system variables](data-factory-functions-variables.md), e.g. "relativeUrl": "$$Text.Format('/my/report?month={0:yyyy}-{0:MM}&fmt=csv', SliceStart)".</span></span> | <span data-ttu-id="a1c93-203">Нет</span><span class="sxs-lookup"><span data-stu-id="a1c93-203">No</span></span> |
| <span data-ttu-id="a1c93-204">requestMethod</span><span class="sxs-lookup"><span data-stu-id="a1c93-204">requestMethod</span></span> | <span data-ttu-id="a1c93-205">Метод HTTP.</span><span class="sxs-lookup"><span data-stu-id="a1c93-205">Http method.</span></span> <span data-ttu-id="a1c93-206">Допустимые значения: **GET** или **POST**.</span><span class="sxs-lookup"><span data-stu-id="a1c93-206">Allowed values are **GET** or **POST**.</span></span> | <span data-ttu-id="a1c93-207">Нет.</span><span class="sxs-lookup"><span data-stu-id="a1c93-207">No.</span></span> <span data-ttu-id="a1c93-208">Значение по умолчанию — `GET`.</span><span class="sxs-lookup"><span data-stu-id="a1c93-208">Default is `GET`.</span></span> |
| <span data-ttu-id="a1c93-209">additionalHeaders</span><span class="sxs-lookup"><span data-stu-id="a1c93-209">additionalHeaders</span></span> | <span data-ttu-id="a1c93-210">Дополнительные заголовки HTTP-запроса.</span><span class="sxs-lookup"><span data-stu-id="a1c93-210">Additional HTTP request headers.</span></span> | <span data-ttu-id="a1c93-211">Нет</span><span class="sxs-lookup"><span data-stu-id="a1c93-211">No</span></span> |
| <span data-ttu-id="a1c93-212">requestBody</span><span class="sxs-lookup"><span data-stu-id="a1c93-212">requestBody</span></span> | <span data-ttu-id="a1c93-213">Текст HTTP-запроса.</span><span class="sxs-lookup"><span data-stu-id="a1c93-213">Body for HTTP request.</span></span> | <span data-ttu-id="a1c93-214">Нет</span><span class="sxs-lookup"><span data-stu-id="a1c93-214">No</span></span> |
| <span data-ttu-id="a1c93-215">свойства</span><span class="sxs-lookup"><span data-stu-id="a1c93-215">format</span></span> | <span data-ttu-id="a1c93-216">Если требуется toosimply **получения данных hello из конечной точки HTTP-является** без его синтаксического анализа пропустить этот формат параметров.</span><span class="sxs-lookup"><span data-stu-id="a1c93-216">If you want toosimply **retrieve hello data from HTTP endpoint as-is** without parsing it, skip this format settings.</span></span> <br><br> <span data-ttu-id="a1c93-217">Если требуется ответ hello HTTP tooparse содержимого во время копирования, поддерживаются следующие типы формата hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="a1c93-217">If you want tooparse hello HTTP response content during copy, hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="a1c93-218">Дополнительные сведения см. в разделах о [текстовом формате](data-factory-supported-file-and-compression-formats.md#text-format), [формате Json](data-factory-supported-file-and-compression-formats.md#json-format), [формате Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [формате Orc](data-factory-supported-file-and-compression-formats.md#orc-format) и [ формате Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="a1c93-218">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> |<span data-ttu-id="a1c93-219">Нет</span><span class="sxs-lookup"><span data-stu-id="a1c93-219">No</span></span> |
| <span data-ttu-id="a1c93-220">compression</span><span class="sxs-lookup"><span data-stu-id="a1c93-220">compression</span></span> | <span data-ttu-id="a1c93-221">Укажите тип hello и уровень сжатия данных hello.</span><span class="sxs-lookup"><span data-stu-id="a1c93-221">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="a1c93-222">Поддерживаемые типы: **GZip**, **Deflate**, **BZip2** и **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="a1c93-222">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="a1c93-223">Поддерживаемые уровни: **Optimal** и **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="a1c93-223">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="a1c93-224">См. дополнительные сведения о [форматах файлов и сжатия данных в фабрике данных Azure](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="a1c93-224">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="a1c93-225">Нет</span><span class="sxs-lookup"><span data-stu-id="a1c93-225">No</span></span> |

### <a name="example-using-hello-get-default-method"></a><span data-ttu-id="a1c93-226">Пример использования hello метод GET (по умолчанию)</span><span class="sxs-lookup"><span data-stu-id="a1c93-226">Example: using hello GET (default) method</span></span>

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

### <a name="example-using-hello-post-method"></a><span data-ttu-id="a1c93-227">Пример: с помощью метода POST hello</span><span class="sxs-lookup"><span data-stu-id="a1c93-227">Example: using hello POST method</span></span>

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

## <a name="copy-activity-properties"></a><span data-ttu-id="a1c93-228">Свойства действия копирования</span><span class="sxs-lookup"><span data-stu-id="a1c93-228">Copy activity properties</span></span>
<span data-ttu-id="a1c93-229">Полный список разделов и свойства, доступные для определения действий см. в разделе hello [Создание конвейеры](data-factory-create-pipelines.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="a1c93-229">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="a1c93-230">Свойства (включая имя, описание, входные и выходные таблицы, политику и т. д.) доступны для всех типов действий.</span><span class="sxs-lookup"><span data-stu-id="a1c93-230">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="a1c93-231">Свойства, доступные в hello **typeProperties** раздел hello действий на hello другой стороны, зависят от типа каждого действия.</span><span class="sxs-lookup"><span data-stu-id="a1c93-231">Properties available in hello **typeProperties** section of hello activity on hello other hand vary with each activity type.</span></span> <span data-ttu-id="a1c93-232">Для действия копирования они зависят от типов источников и приемников hello.</span><span class="sxs-lookup"><span data-stu-id="a1c93-232">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="a1c93-233">В настоящее время, если источник hello в действии копирования имеет тип **HttpSource**, поддерживаются следующие свойства hello.</span><span class="sxs-lookup"><span data-stu-id="a1c93-233">Currently, when hello source in copy activity is of type **HttpSource**, hello following properties are supported.</span></span>

| <span data-ttu-id="a1c93-234">Свойство</span><span class="sxs-lookup"><span data-stu-id="a1c93-234">Property</span></span> | <span data-ttu-id="a1c93-235">Описание</span><span class="sxs-lookup"><span data-stu-id="a1c93-235">Description</span></span> | <span data-ttu-id="a1c93-236">Обязательно</span><span class="sxs-lookup"><span data-stu-id="a1c93-236">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="a1c93-237">httpRequestTimeout</span><span class="sxs-lookup"><span data-stu-id="a1c93-237">httpRequestTimeout</span></span> | <span data-ttu-id="a1c93-238">Здравствуйте, время ожидания (TimeSpan) для hello HTTP tooget ответа для запроса.</span><span class="sxs-lookup"><span data-stu-id="a1c93-238">hello timeout (TimeSpan) for hello HTTP request tooget a response.</span></span> <span data-ttu-id="a1c93-239">Это tooget hello время ожидания ответа, не hello время ожидания tooread данные ответа.</span><span class="sxs-lookup"><span data-stu-id="a1c93-239">It is hello timeout tooget a response, not hello timeout tooread response data.</span></span> | <span data-ttu-id="a1c93-240">Нет.</span><span class="sxs-lookup"><span data-stu-id="a1c93-240">No.</span></span> <span data-ttu-id="a1c93-241">Значение по умолчанию  — 00:01:40.</span><span class="sxs-lookup"><span data-stu-id="a1c93-241">Default value: 00:01:40</span></span> |

## <a name="supported-file-and-compression-formats"></a><span data-ttu-id="a1c93-242">Поддерживаемые форматы файлов и сжатия</span><span class="sxs-lookup"><span data-stu-id="a1c93-242">Supported file and compression formats</span></span>
<span data-ttu-id="a1c93-243">Дополнительные сведения см. в статье [Форматы файлов и сжатия данных, поддерживаемые фабрикой данных Azure](data-factory-supported-file-and-compression-formats.md).</span><span class="sxs-lookup"><span data-stu-id="a1c93-243">See [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article on details.</span></span>

## <a name="json-examples"></a><span data-ttu-id="a1c93-244">Примеры определений JSON</span><span class="sxs-lookup"><span data-stu-id="a1c93-244">JSON examples</span></span>
<span data-ttu-id="a1c93-245">Следующий пример Hello предоставить определения образца JSON можно использовать toocreate конвейера с помощью [портал Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) или [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) или [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="a1c93-245">hello following example provide sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="a1c93-246">Они показывают, как toocopy из HTTP источника tooAzure хранилища больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="a1c93-246">They show how toocopy data from HTTP source tooAzure Blob Storage.</span></span> <span data-ttu-id="a1c93-247">Тем не менее, данные можно скопировать **непосредственно** из любых источников tooany приемников hello указано [здесь](data-factory-data-movement-activities.md#supported-data-stores-and-formats) с помощью hello действие копирования в фабрике данных Azure.</span><span class="sxs-lookup"><span data-stu-id="a1c93-247">However, data can be copied **directly** from any of sources tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>

### <a name="example-copy-data-from-http-source-tooazure-blob-storage"></a><span data-ttu-id="a1c93-248">Пример: Копирование данных из источника HTTP tooAzure хранилища больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="a1c93-248">Example: Copy data from HTTP source tooAzure Blob Storage</span></span>
<span data-ttu-id="a1c93-249">решение фабрики данных для данного образца Hello содержит hello, следуя фабрики данных сущности:</span><span class="sxs-lookup"><span data-stu-id="a1c93-249">hello Data Factory solution for this sample contains hello following Data Factory entities:</span></span>

1. <span data-ttu-id="a1c93-250">Связанная служба типа [HTTP](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="a1c93-250">A linked service of type [HTTP](#linked-service-properties).</span></span>
2. <span data-ttu-id="a1c93-251">Связанная служба типа [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="a1c93-251">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="a1c93-252">Входной [набор данных](data-factory-create-datasets.md) типа [Http](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="a1c93-252">An input [dataset](data-factory-create-datasets.md) of type [Http](#dataset-properties).</span></span>
4. <span data-ttu-id="a1c93-253">Выходной [набор данных](data-factory-create-datasets.md) типа [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="a1c93-253">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="a1c93-254">[Конвейер](data-factory-create-pipelines.md) с действием копирования, в котором используются [HttpSource](#copy-activity-properties) и [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="a1c93-254">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [HttpSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="a1c93-255">Образец Hello копирует данные из tooan источника HTTP BLOB-объектов Azure каждый час.</span><span class="sxs-lookup"><span data-stu-id="a1c93-255">hello sample copies data from an HTTP source tooan Azure blob every hour.</span></span> <span data-ttu-id="a1c93-256">свойства Hello JSON, используемые в этих примерах описаны в разделах, следующие примеры hello.</span><span class="sxs-lookup"><span data-stu-id="a1c93-256">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

### <a name="http-linked-service"></a><span data-ttu-id="a1c93-257">Связанная служба HTTP</span><span class="sxs-lookup"><span data-stu-id="a1c93-257">HTTP linked service</span></span>
<span data-ttu-id="a1c93-258">В этом примере, что использует hello HTTP связанная служба с анонимной проверкой подлинности.</span><span class="sxs-lookup"><span data-stu-id="a1c93-258">This example uses hello HTTP linked service with anonymous authentication.</span></span> <span data-ttu-id="a1c93-259">Сведения о возможных типах аутентификации см. в разделе о [связанной службе HTTP](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="a1c93-259">See [HTTP linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

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

### <a name="azure-storage-linked-service"></a><span data-ttu-id="a1c93-260">Связанная служба хранения Azure</span><span class="sxs-lookup"><span data-stu-id="a1c93-260">Azure Storage linked service</span></span>

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

### <a name="http-input-dataset"></a><span data-ttu-id="a1c93-261">Входной набор данных HTTP</span><span class="sxs-lookup"><span data-stu-id="a1c93-261">HTTP input dataset</span></span>
<span data-ttu-id="a1c93-262">Установка **внешних** слишком**true** информирует hello служба фабрики данных, набор данных hello фабрики toohello внешних данных и не был создан из действия в фабрике данных hello.</span><span class="sxs-lookup"><span data-stu-id="a1c93-262">Setting **external** too**true** informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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

### <a name="azure-blob-output-dataset"></a><span data-ttu-id="a1c93-263">Выходной набор данных BLOB-объекта Azure</span><span class="sxs-lookup"><span data-stu-id="a1c93-263">Azure Blob output dataset</span></span>

<span data-ttu-id="a1c93-264">Записывается новый большой двоичный объект tooa каждый час (частота: час, интервал: 1).</span><span class="sxs-lookup"><span data-stu-id="a1c93-264">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span>

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

### <a name="pipeline-with-copy-activity"></a><span data-ttu-id="a1c93-265">Конвейер с действием копирования</span><span class="sxs-lookup"><span data-stu-id="a1c93-265">Pipeline with Copy activity</span></span>

<span data-ttu-id="a1c93-266">Hello конвейера содержит операции копирования, настроенные toouse hello входные и выходные наборы данных и является запланированных toorun каждый час.</span><span class="sxs-lookup"><span data-stu-id="a1c93-266">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="a1c93-267">В определении JSON конвейера hello, hello **источника** тип установлен слишком**HttpSource** и **приемник** тип установлен слишком**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="a1c93-267">In hello pipeline JSON definition, hello **source** type is set too**HttpSource** and **sink** type is set too**BlobSink**.</span></span>

<span data-ttu-id="a1c93-268">В разделе [HttpSource](#copy-activity-properties) список свойств, поддерживаемых hello HttpSource hello.</span><span class="sxs-lookup"><span data-stu-id="a1c93-268">See [HttpSource](#copy-activity-properties) for hello list of properties supported by hello HttpSource.</span></span>

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
        "description": "Copy from an HTTP source tooan Azure blob",
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
> <span data-ttu-id="a1c93-269">toomap столбцы из источника toocolumns набора данных из набора данных приемников, в разделе [сопоставление столбцов набора данных в фабрике данных Azure](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="a1c93-269">toomap columns from source dataset toocolumns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="a1c93-270">Производительность и настройка</span><span class="sxs-lookup"><span data-stu-id="a1c93-270">Performance and Tuning</span></span>
<span data-ttu-id="a1c93-271">В разделе [производительности для действия копирования & руководство по настройке](data-factory-copy-activity-performance.md) toolearn о ключе факторы, оказывают влияние на производительность перемещения данных (действие копирования) в фабрике данных Azure и различных способов toooptimize его.</span><span class="sxs-lookup"><span data-stu-id="a1c93-271">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
