---
title: "aaaMove данные из FTP-сервера с помощью фабрики данных Azure | Документы Microsoft"
description: "Дополнительные сведения о данных toomove с FTP-сервера, с помощью фабрики данных Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: eea3bab0-a6e4-4045-ad44-9ce06229c718
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: jingwang
ms.openlocfilehash: c707e29532b2a8a870603948cb6150ab857bd6ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-an-ftp-server-by-using-azure-data-factory"></a><span data-ttu-id="12e7c-103">Перемещение данных с FTP-сервера с использованием фабрики данных Azure</span><span class="sxs-lookup"><span data-stu-id="12e7c-103">Move data from an FTP server by using Azure Data Factory</span></span>
<span data-ttu-id="12e7c-104">В этой статье объясняется, как toouse hello в действии копирования данных toomove фабрики данных Azure из FTP-сервера.</span><span class="sxs-lookup"><span data-stu-id="12e7c-104">This article explains how toouse hello copy activity in Azure Data Factory toomove data from an FTP server.</span></span> <span data-ttu-id="12e7c-105">Она построена на hello [действия перемещения данных](data-factory-data-movement-activities.md) статьи, которая представляет общие сведения о перемещении данных с действием копирования hello.</span><span class="sxs-lookup"><span data-stu-id="12e7c-105">It builds on hello [Data movement activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="12e7c-106">Можно скопировать данные из хранилища данных приемник tooany поддерживается сервера FTP.</span><span class="sxs-lookup"><span data-stu-id="12e7c-106">You can copy data from an FTP server tooany supported sink data store.</span></span> <span data-ttu-id="12e7c-107">Список данных поддерживается хранилищ, приемники действием копирования hello см hello [поддерживается хранилищ данных](data-factory-data-movement-activities.md#supported-data-stores-and-formats) таблицы.</span><span class="sxs-lookup"><span data-stu-id="12e7c-107">For a list of data stores supported as sinks by hello copy activity, see hello [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="12e7c-108">Фабрика данных в настоящее время поддерживает только хранит перемещение данных из объекта данных tooother сервера FTP, но не перемещения данных из других данных хранит tooan FTP-сервера.</span><span class="sxs-lookup"><span data-stu-id="12e7c-108">Data Factory currently supports only moving data from an FTP server tooother data stores, but not moving data from other data stores tooan FTP server.</span></span> <span data-ttu-id="12e7c-109">Она поддерживает локальные и облачные FTP-серверы.</span><span class="sxs-lookup"><span data-stu-id="12e7c-109">It supports both on-premises and cloud FTP servers.</span></span>

> [!NOTE]
> <span data-ttu-id="12e7c-110">Действие копирования Hello не удаляет исходный файл hello после назначения успешно скопированного toohello.</span><span class="sxs-lookup"><span data-stu-id="12e7c-110">hello copy activity does not delete hello source file after it is successfully copied toohello destination.</span></span> <span data-ttu-id="12e7c-111">Если вам требуется toodelete hello исходного файла после успешным копированием, создайте файл hello toodelete пользовательского действия и использовать действие hello в конвейере hello.</span><span class="sxs-lookup"><span data-stu-id="12e7c-111">If you need toodelete hello source file after a successful copy, create a custom activity toodelete hello file, and use hello activity in hello pipeline.</span></span> 

## <a name="enable-connectivity"></a><span data-ttu-id="12e7c-112">Включение соединения</span><span class="sxs-lookup"><span data-stu-id="12e7c-112">Enable connectivity</span></span>
<span data-ttu-id="12e7c-113">При перемещении данных из **локальной** FTP сервера tooa Облачное хранилище данных (например, tooAzure хранилища больших двоичных объектов), установить и использовать шлюз управления данными.</span><span class="sxs-lookup"><span data-stu-id="12e7c-113">If you are moving data from an **on-premises** FTP server tooa cloud data store (for example, tooAzure Blob storage), install and use Data Management Gateway.</span></span> <span data-ttu-id="12e7c-114">Hello шлюз управления данными — это агент клиента, который установлен на локальном компьютере и позволяет облачных служб tooconnect tooan локального ресурса.</span><span class="sxs-lookup"><span data-stu-id="12e7c-114">hello Data Management Gateway is a client agent that is installed on your on-premises machine, and it allows cloud services tooconnect tooan on-premises resource.</span></span> <span data-ttu-id="12e7c-115">Подробные сведения см. в разделе [Шлюз управления данными](data-factory-data-management-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="12e7c-115">For details, see [Data Management Gateway](data-factory-data-management-gateway.md).</span></span> <span data-ttu-id="12e7c-116">Пошаговые инструкции по настройке шлюза hello и его использования см. в разделе [перемещение данных между расположениями локальных и облачных](data-factory-move-data-between-onprem-and-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="12e7c-116">For step-by-step instructions on setting up hello gateway and using it, see [Moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md).</span></span> <span data-ttu-id="12e7c-117">Hello tooconnect tooan FTP шлюза, использовать, даже если hello server в Azure инфраструктуры как услуги (IaaS) виртуальной машины (VM).</span><span class="sxs-lookup"><span data-stu-id="12e7c-117">You use hello gateway tooconnect tooan FTP server, even if hello server is on an Azure infrastructure as a service (IaaS) virtual machine (VM).</span></span>

<span data-ttu-id="12e7c-118">Он служит шлюзом hello возможных tooinstall hello же на локальный компьютер или ВМ IaaS как hello FTP-сервера.</span><span class="sxs-lookup"><span data-stu-id="12e7c-118">It is possible tooinstall hello gateway on hello same on-premises machine or IaaS VM as hello FTP server.</span></span> <span data-ttu-id="12e7c-119">Тем не менее рекомендуется установить шлюз hello на отдельный компьютер или ВМ IaaS конкуренцию за ресурсы tooavoid и для повышения производительности.</span><span class="sxs-lookup"><span data-stu-id="12e7c-119">However, we recommend that you install hello gateway on a separate machine or IaaS VM tooavoid resource contention, and for better performance.</span></span> <span data-ttu-id="12e7c-120">При установке шлюза hello на отдельном компьютере hello машина должна была может tooaccess hello FTP-сервера.</span><span class="sxs-lookup"><span data-stu-id="12e7c-120">When you install hello gateway on a separate machine, hello machine should be able tooaccess hello FTP server.</span></span>

## <a name="get-started"></a><span data-ttu-id="12e7c-121">Начало работы</span><span class="sxs-lookup"><span data-stu-id="12e7c-121">Get started</span></span>
<span data-ttu-id="12e7c-122">Вы можете создать конвейер с действием копирования, который перемещает данные с исходного FTP-сервера, с помощью разных средств или интерфейсов API.</span><span class="sxs-lookup"><span data-stu-id="12e7c-122">You can create a pipeline with a copy activity that moves data from an FTP source by using different tools or APIs.</span></span>

<span data-ttu-id="12e7c-123">toocreate простым способом Hello конвейера — toouse hello **мастер копирования фабрики данных**.</span><span class="sxs-lookup"><span data-stu-id="12e7c-123">hello easiest way toocreate a pipeline is toouse hello **Data Factory Copy Wizard**.</span></span> <span data-ttu-id="12e7c-124">Краткое пошаговое руководство представлено в статье [Руководство. Создание конвейера с действием копирования с помощью мастера копирования фабрики данных](data-factory-copy-data-wizard-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="12e7c-124">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough.</span></span>

<span data-ttu-id="12e7c-125">Также можно использовать следующие средства toocreate конвейера hello: **портал Azure**, **Visual Studio**, **PowerShell**, **шаблона Azure Resource Manager**, **.NET API**, и **API-интерфейса REST**.</span><span class="sxs-lookup"><span data-stu-id="12e7c-125">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="12e7c-126">В разделе [учебника действия копирования](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) для toocreate пошаговые инструкции конвейера с помощью операции копирования.</span><span class="sxs-lookup"><span data-stu-id="12e7c-126">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span>

<span data-ttu-id="12e7c-127">Используется ли hello инструменты или интерфейсы API, выполните следующие шаги toocreate конвейера, который перемещает данные из источника данных хранилище tooa приемник данных hello.</span><span class="sxs-lookup"><span data-stu-id="12e7c-127">Whether you use hello tools or APIs, perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="12e7c-128">Создание **связанные службы** toolink ввода-вывода хранилища tooyour данных фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="12e7c-128">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="12e7c-129">Создание **наборы данных** toorepresent входных и выходных данных для hello операции копирования.</span><span class="sxs-lookup"><span data-stu-id="12e7c-129">Create **datasets** toorepresent input and output data for hello copy operation.</span></span>
3. <span data-ttu-id="12e7c-130">Создайте **конвейер** с действием копирования, который принимает входной набор данных и возвращает выходной набор данных.</span><span class="sxs-lookup"><span data-stu-id="12e7c-130">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span>

<span data-ttu-id="12e7c-131">При использовании мастера hello JSON определения для этих сущностей фабрики данных (связанные службы, наборы данных и hello конвейера) создаются автоматически.</span><span class="sxs-lookup"><span data-stu-id="12e7c-131">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="12e7c-132">При использовании средств или API-интерфейсы (за исключением .NET API), определяются с использованием формата JSON hello этих сущностей фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="12e7c-132">When you use tools or APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span> <span data-ttu-id="12e7c-133">Пример с определениями JSON для сущностей фабрики данных, используемых toocopy данные из хранилища данных FTP см. в разделе hello [JSON. Пример: копирование данных из большого двоичного объекта tooAzure сервера FTP](#json-example-copy-data-from-ftp-server-to-azure-blob) этой статьи.</span><span class="sxs-lookup"><span data-stu-id="12e7c-133">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an FTP data store, see hello [JSON example: Copy data from FTP server tooAzure blob](#json-example-copy-data-from-ftp-server-to-azure-blob) section of this article.</span></span>

> [!NOTE]
> <span data-ttu-id="12e7c-134">Дополнительные сведения о поддерживаемых сжатие файлов и форматы toouse см [сжатие файлов и форматы в фабрике данных Azure](data-factory-supported-file-and-compression-formats.md).</span><span class="sxs-lookup"><span data-stu-id="12e7c-134">For details about supported file and compression formats toouse, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md).</span></span>

<span data-ttu-id="12e7c-135">Hello в следующих разделах приведены сведения о JSON свойства, которые являются определенной tooFTP используется toodefine фабрики данных сущности.</span><span class="sxs-lookup"><span data-stu-id="12e7c-135">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooFTP.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="12e7c-136">Свойства связанной службы</span><span class="sxs-lookup"><span data-stu-id="12e7c-136">Linked service properties</span></span>
<span data-ttu-id="12e7c-137">Hello в следующей таблице описываются JSON элементов определенного tooan связанные службы FTP.</span><span class="sxs-lookup"><span data-stu-id="12e7c-137">hello following table describes JSON elements specific tooan FTP linked service.</span></span>

| <span data-ttu-id="12e7c-138">Свойство</span><span class="sxs-lookup"><span data-stu-id="12e7c-138">Property</span></span> | <span data-ttu-id="12e7c-139">Описание</span><span class="sxs-lookup"><span data-stu-id="12e7c-139">Description</span></span> | <span data-ttu-id="12e7c-140">Обязательно</span><span class="sxs-lookup"><span data-stu-id="12e7c-140">Required</span></span> | <span data-ttu-id="12e7c-141">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="12e7c-141">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="12e7c-142">type</span><span class="sxs-lookup"><span data-stu-id="12e7c-142">type</span></span> |<span data-ttu-id="12e7c-143">Задайте этот tooFtpServer.</span><span class="sxs-lookup"><span data-stu-id="12e7c-143">Set this tooFtpServer.</span></span> |<span data-ttu-id="12e7c-144">Да</span><span class="sxs-lookup"><span data-stu-id="12e7c-144">Yes</span></span> |&nbsp; |
| <span data-ttu-id="12e7c-145">host</span><span class="sxs-lookup"><span data-stu-id="12e7c-145">host</span></span> |<span data-ttu-id="12e7c-146">Укажите hello имя или IP-адрес сервера FTP hello.</span><span class="sxs-lookup"><span data-stu-id="12e7c-146">Specify hello name or IP address of hello FTP server.</span></span> |<span data-ttu-id="12e7c-147">Да</span><span class="sxs-lookup"><span data-stu-id="12e7c-147">Yes</span></span> |&nbsp; |
| <span data-ttu-id="12e7c-148">authenticationType</span><span class="sxs-lookup"><span data-stu-id="12e7c-148">authenticationType</span></span> |<span data-ttu-id="12e7c-149">Укажите тип проверки подлинности hello.</span><span class="sxs-lookup"><span data-stu-id="12e7c-149">Specify hello authentication type.</span></span> |<span data-ttu-id="12e7c-150">Да</span><span class="sxs-lookup"><span data-stu-id="12e7c-150">Yes</span></span> |<span data-ttu-id="12e7c-151">Обычная, анонимная</span><span class="sxs-lookup"><span data-stu-id="12e7c-151">Basic, Anonymous</span></span> |
| <span data-ttu-id="12e7c-152">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="12e7c-152">username</span></span> |<span data-ttu-id="12e7c-153">Укажите hello пользователя, имеющего доступ toohello FTP-сервера.</span><span class="sxs-lookup"><span data-stu-id="12e7c-153">Specify hello user who has access toohello FTP server.</span></span> |<span data-ttu-id="12e7c-154">Нет</span><span class="sxs-lookup"><span data-stu-id="12e7c-154">No</span></span> |&nbsp; |
| <span data-ttu-id="12e7c-155">пароль</span><span class="sxs-lookup"><span data-stu-id="12e7c-155">password</span></span> |<span data-ttu-id="12e7c-156">Укажите пароль hello hello пользователя (имя пользователя).</span><span class="sxs-lookup"><span data-stu-id="12e7c-156">Specify hello password for hello user (username).</span></span> |<span data-ttu-id="12e7c-157">Нет</span><span class="sxs-lookup"><span data-stu-id="12e7c-157">No</span></span> |&nbsp; |
| <span data-ttu-id="12e7c-158">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="12e7c-158">encryptedCredential</span></span> |<span data-ttu-id="12e7c-159">Укажите tooaccess hello FTP hello зашифрованные учетные данные сервера.</span><span class="sxs-lookup"><span data-stu-id="12e7c-159">Specify hello encrypted credential tooaccess hello FTP server.</span></span> |<span data-ttu-id="12e7c-160">Нет</span><span class="sxs-lookup"><span data-stu-id="12e7c-160">No</span></span> |&nbsp; |
| <span data-ttu-id="12e7c-161">gatewayName</span><span class="sxs-lookup"><span data-stu-id="12e7c-161">gatewayName</span></span> |<span data-ttu-id="12e7c-162">Укажите имя шлюза hello hello в шлюз управления данными tooconnect tooan локальной для FTP-сервера.</span><span class="sxs-lookup"><span data-stu-id="12e7c-162">Specify hello name of hello gateway in Data Management Gateway tooconnect tooan on-premises FTP server.</span></span> |<span data-ttu-id="12e7c-163">Нет</span><span class="sxs-lookup"><span data-stu-id="12e7c-163">No</span></span> |&nbsp; |
| <span data-ttu-id="12e7c-164">порт</span><span class="sxs-lookup"><span data-stu-id="12e7c-164">port</span></span> |<span data-ttu-id="12e7c-165">Укажите порт hello какие hello FTP прослушивает сервер.</span><span class="sxs-lookup"><span data-stu-id="12e7c-165">Specify hello port on which hello FTP server is listening.</span></span> |<span data-ttu-id="12e7c-166">Нет</span><span class="sxs-lookup"><span data-stu-id="12e7c-166">No</span></span> |<span data-ttu-id="12e7c-167">21</span><span class="sxs-lookup"><span data-stu-id="12e7c-167">21</span></span> |
| <span data-ttu-id="12e7c-168">enableSsl</span><span class="sxs-lookup"><span data-stu-id="12e7c-168">enableSsl</span></span> |<span data-ttu-id="12e7c-169">Укажите, является ли toouse FTP через канал SSL/TLS.</span><span class="sxs-lookup"><span data-stu-id="12e7c-169">Specify whether toouse FTP over an SSL/TLS channel.</span></span> |<span data-ttu-id="12e7c-170">Нет</span><span class="sxs-lookup"><span data-stu-id="12e7c-170">No</span></span> |<span data-ttu-id="12e7c-171">Да</span><span class="sxs-lookup"><span data-stu-id="12e7c-171">true</span></span> |
| <span data-ttu-id="12e7c-172">enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="12e7c-172">enableServerCertificateValidation</span></span> |<span data-ttu-id="12e7c-173">Укажите, является ли сервер tooenable SSL проверку сертификата при использовании FTP по каналу SSL/TLS.</span><span class="sxs-lookup"><span data-stu-id="12e7c-173">Specify whether tooenable server SSL certificate validation when you are using FTP over SSL/TLS channel.</span></span> |<span data-ttu-id="12e7c-174">Нет</span><span class="sxs-lookup"><span data-stu-id="12e7c-174">No</span></span> |<span data-ttu-id="12e7c-175">Да</span><span class="sxs-lookup"><span data-stu-id="12e7c-175">true</span></span> |

### <a name="use-anonymous-authentication"></a><span data-ttu-id="12e7c-176">Использование анонимной проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="12e7c-176">Use Anonymous authentication</span></span>

```JSON
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {        
            "authenticationType": "Anonymous",
              "host": "myftpserver.com"
        }
    }
}
```

### <a name="use-username-and-password-in-plain-text-for-basic-authentication"></a><span data-ttu-id="12e7c-177">Использование имени пользователя и пароля в виде обычного текста для обычной проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="12e7c-177">Use username and password in plain text for basic authentication</span></span>

```JSON
{
    "name": "FTPLinkedService",
      "properties": {
    "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",
            "username": "Admin",
            "password": "123456"
        }
      }
}
```

### <a name="use-port-enablessl-enableservercertificatevalidation"></a><span data-ttu-id="12e7c-178">Использование свойств port, enableSsl, enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="12e7c-178">Use port, enableSsl, enableServerCertificateValidation</span></span>

```JSON
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",    
            "username": "Admin",
            "password": "123456",
            "port": "21",
            "enableSsl": true,
            "enableServerCertificateValidation": true
        }
    }
}
```

### <a name="use-encryptedcredential-for-authentication-and-gateway"></a><span data-ttu-id="12e7c-179">Использование свойства encryptedCredential для проверки подлинности и шлюза</span><span class="sxs-lookup"><span data-stu-id="12e7c-179">Use encryptedCredential for authentication and gateway</span></span>

```JSON
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",
            "encryptedCredential": "xxxxxxxxxxxxxxxxx",
            "gatewayName": "mygateway"
        }
      }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="12e7c-180">Свойства набора данных</span><span class="sxs-lookup"><span data-stu-id="12e7c-180">Dataset properties</span></span>
<span data-ttu-id="12e7c-181">Полный список разделов и свойств, доступных для определения наборов данных, см. в разделе [Наборы данных в фабрике данных Azure](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="12e7c-181">For a full list of sections and properties available for defining datasets, see [Creating datasets](data-factory-create-datasets.md).</span></span> <span data-ttu-id="12e7c-182">Разделы структуры, доступности и политики JSON набора данных одинаковы для всех типов наборов данных.</span><span class="sxs-lookup"><span data-stu-id="12e7c-182">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types.</span></span>

<span data-ttu-id="12e7c-183">Hello **typeProperties** раздела отличается для каждого типа набора данных.</span><span class="sxs-lookup"><span data-stu-id="12e7c-183">hello **typeProperties** section is different for each type of dataset.</span></span> <span data-ttu-id="12e7c-184">Он предоставляет сведения о, тип toohello конкретного набора данных.</span><span class="sxs-lookup"><span data-stu-id="12e7c-184">It provides information that is specific toohello dataset type.</span></span> <span data-ttu-id="12e7c-185">Hello **typeProperties** раздел для набора данных типа **FileShare** имеет hello следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="12e7c-185">hello **typeProperties** section for a dataset of type **FileShare** has hello following properties:</span></span>

| <span data-ttu-id="12e7c-186">Свойство</span><span class="sxs-lookup"><span data-stu-id="12e7c-186">Property</span></span> | <span data-ttu-id="12e7c-187">Описание</span><span class="sxs-lookup"><span data-stu-id="12e7c-187">Description</span></span> | <span data-ttu-id="12e7c-188">Обязательно</span><span class="sxs-lookup"><span data-stu-id="12e7c-188">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="12e7c-189">folderPath</span><span class="sxs-lookup"><span data-stu-id="12e7c-189">folderPath</span></span> |<span data-ttu-id="12e7c-190">Папка toohello вложенным.</span><span class="sxs-lookup"><span data-stu-id="12e7c-190">Subpath toohello folder.</span></span> <span data-ttu-id="12e7c-191">Использовать escape-символ "\" для специальных символов в строке приветствия.</span><span class="sxs-lookup"><span data-stu-id="12e7c-191">Use escape character ‘ \ ’ for special characters in hello string.</span></span> <span data-ttu-id="12e7c-192">Примеры приведены в разделе [Примеры определений связанной службы и набора данных](#sample-linked-service-and-dataset-definitions).</span><span class="sxs-lookup"><span data-stu-id="12e7c-192">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="12e7c-193">Можно объединять с помощью этого свойства **partitionBy** toohave пути к папке зависимости среза начальных и конечных дат.</span><span class="sxs-lookup"><span data-stu-id="12e7c-193">You can combine this property with **partitionBy** toohave folder paths based on slice start and end date-times.</span></span> |<span data-ttu-id="12e7c-194">Да</span><span class="sxs-lookup"><span data-stu-id="12e7c-194">Yes</span></span> |
| <span data-ttu-id="12e7c-195">fileName</span><span class="sxs-lookup"><span data-stu-id="12e7c-195">fileName</span></span> |<span data-ttu-id="12e7c-196">Укажите имя файла hello hello в hello **folderPath** Если hello таблицы toorefer tooa конкретный файл в папку hello.</span><span class="sxs-lookup"><span data-stu-id="12e7c-196">Specify hello name of hello file in hello **folderPath** if you want hello table toorefer tooa specific file in hello folder.</span></span> <span data-ttu-id="12e7c-197">Если не указано значение для этого свойства, таблица hello указывает tooall файлы в папке hello.</span><span class="sxs-lookup"><span data-stu-id="12e7c-197">If you do not specify any value for this property, hello table points tooall files in hello folder.</span></span><br/><br/><span data-ttu-id="12e7c-198">Когда **fileName** для не указан выходной набор данных hello hello созданный файл имеет имя в hello следующий формат:</span><span class="sxs-lookup"><span data-stu-id="12e7c-198">When **fileName** is not specified for an output dataset, hello name of hello generated file is in hello following format:</span></span> <br/><br/><span data-ttu-id="12e7c-199">Data.<Guid>.txt (пример: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span><span class="sxs-lookup"><span data-stu-id="12e7c-199">Data.<Guid>.txt (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span></span> |<span data-ttu-id="12e7c-200">Нет</span><span class="sxs-lookup"><span data-stu-id="12e7c-200">No</span></span> |
| <span data-ttu-id="12e7c-201">fileFilter</span><span class="sxs-lookup"><span data-stu-id="12e7c-201">fileFilter</span></span> |<span data-ttu-id="12e7c-202">Укажите фильтр toobe используется tooselect подмножества файлов в hello **folderPath**, а не все файлы.</span><span class="sxs-lookup"><span data-stu-id="12e7c-202">Specify a filter toobe used tooselect a subset of files in hello **folderPath**, rather than all files.</span></span><br/><br/><span data-ttu-id="12e7c-203">Допустимые значения: `*` (несколько знаков) и `?` (один знак).</span><span class="sxs-lookup"><span data-stu-id="12e7c-203">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="12e7c-204">Пример 1: `"fileFilter": "*.log"`</span><span class="sxs-lookup"><span data-stu-id="12e7c-204">Example 1: `"fileFilter": "*.log"`</span></span><br/><span data-ttu-id="12e7c-205">Пример 2: `"fileFilter": 2014-1-?.txt"`</span><span class="sxs-lookup"><span data-stu-id="12e7c-205">Example 2: `"fileFilter": 2014-1-?.txt"`</span></span><br/><br/> <span data-ttu-id="12e7c-206">Свойство **fileFilter** применяется ко входному набору данных FileShare.</span><span class="sxs-lookup"><span data-stu-id="12e7c-206">**fileFilter** is applicable for an input FileShare dataset.</span></span> <span data-ttu-id="12e7c-207">Распределенная файловая система Hadoop (HDFS) не поддерживает это свойство.</span><span class="sxs-lookup"><span data-stu-id="12e7c-207">This property is not supported with Hadoop Distributed File System (HDFS).</span></span> |<span data-ttu-id="12e7c-208">Нет</span><span class="sxs-lookup"><span data-stu-id="12e7c-208">No</span></span> |
| <span data-ttu-id="12e7c-209">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="12e7c-209">partitionedBy</span></span> |<span data-ttu-id="12e7c-210">Использовать динамический toospecify **folderPath** и **fileName** для временного ряда данных.</span><span class="sxs-lookup"><span data-stu-id="12e7c-210">Used toospecify a dynamic **folderPath** and **fileName** for time series data.</span></span> <span data-ttu-id="12e7c-211">Например, можно указать **путь к папке**, который будет параметризироваться для данных за каждый час.</span><span class="sxs-lookup"><span data-stu-id="12e7c-211">For example, you can specify a **folderPath** that is parameterized for every hour of data.</span></span> |<span data-ttu-id="12e7c-212">Нет</span><span class="sxs-lookup"><span data-stu-id="12e7c-212">No</span></span> |
| <span data-ttu-id="12e7c-213">свойства</span><span class="sxs-lookup"><span data-stu-id="12e7c-213">format</span></span> | <span data-ttu-id="12e7c-214">поддерживаются следующие типы формата Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="12e7c-214">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="12e7c-215">Набор hello **тип** свойства в формате tooone из следующих значений.</span><span class="sxs-lookup"><span data-stu-id="12e7c-215">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="12e7c-216">Дополнительные сведения см. в разделе hello [текстовом формате](data-factory-supported-file-and-compression-formats.md#text-format), [формат Json](data-factory-supported-file-and-compression-formats.md#json-format), [формат Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [формат Orc](data-factory-supported-file-and-compression-formats.md#orc-format), и [Parquet формат ](data-factory-supported-file-and-compression-formats.md#parquet-format) разделы.</span><span class="sxs-lookup"><span data-stu-id="12e7c-216">For more information, see hello [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="12e7c-217">Если нужно toocopy файлы, как они находятся в диапазоне от файловых хранилищ (двоичный копия), пропустите hello формат раздела оба определения набора входных и выходных данных.</span><span class="sxs-lookup"><span data-stu-id="12e7c-217">If you want toocopy files as they are between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="12e7c-218">Нет</span><span class="sxs-lookup"><span data-stu-id="12e7c-218">No</span></span> |
| <span data-ttu-id="12e7c-219">compression</span><span class="sxs-lookup"><span data-stu-id="12e7c-219">compression</span></span> | <span data-ttu-id="12e7c-220">Укажите тип hello и уровень сжатия данных hello.</span><span class="sxs-lookup"><span data-stu-id="12e7c-220">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="12e7c-221">Поддерживаемые типы: **GZip**, **Deflate**, **BZip2** и **ZipDeflate**. Поддерживаемые уровни: **Optimal** и **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="12e7c-221">Supported types are **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**, and supported levels are **Optimal** and **Fastest**.</span></span> <span data-ttu-id="12e7c-222">См. дополнительные сведения о [форматах файлов и сжатия данных в фабрике данных Azure](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="12e7c-222">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="12e7c-223">Нет</span><span class="sxs-lookup"><span data-stu-id="12e7c-223">No</span></span> |
| <span data-ttu-id="12e7c-224">useBinaryTransfer</span><span class="sxs-lookup"><span data-stu-id="12e7c-224">useBinaryTransfer</span></span> |<span data-ttu-id="12e7c-225">Укажите toouse hello двоичный режим передачи.</span><span class="sxs-lookup"><span data-stu-id="12e7c-225">Specify whether toouse hello binary transfer mode.</span></span> <span data-ttu-id="12e7c-226">Hello значениями являются true для двоичном режиме (это значение по умолчанию hello) и значение false для ASCII.</span><span class="sxs-lookup"><span data-stu-id="12e7c-226">hello values are true for binary mode (this is hello default value), and false for ASCII.</span></span> <span data-ttu-id="12e7c-227">Это свойство может использоваться, только если hello типа связанного связанной службы типа: FTP-сервер.</span><span class="sxs-lookup"><span data-stu-id="12e7c-227">This property can only be used when hello associated linked service type is of type: FtpServer.</span></span> |<span data-ttu-id="12e7c-228">Нет</span><span class="sxs-lookup"><span data-stu-id="12e7c-228">No</span></span> |

> [!NOTE]
> <span data-ttu-id="12e7c-229">Свойства **fileName** и **fileFilter** нельзя использовать одновременно.</span><span class="sxs-lookup"><span data-stu-id="12e7c-229">**fileName** and **fileFilter** cannot be used simultaneously.</span></span>

### <a name="use-hello-partionedby-property"></a><span data-ttu-id="12e7c-230">Используйте свойство partionedBy hello</span><span class="sxs-lookup"><span data-stu-id="12e7c-230">Use hello partionedBy property</span></span>
<span data-ttu-id="12e7c-231">Как упоминалось в предыдущем разделе hello, можно указать динамический **folderPath** и **fileName** для временного ряда данных с hello **partitionedBy** свойство.</span><span class="sxs-lookup"><span data-stu-id="12e7c-231">As mentioned in hello previous section, you can specify a dynamic **folderPath** and **fileName** for time series data with hello **partitionedBy** property.</span></span>

<span data-ttu-id="12e7c-232">toolearn о наборы данных для ряда времени, планирования и срезов, в разделе [Создание наборов данных](data-factory-create-datasets.md), [планирования и выполнения](data-factory-scheduling-and-execution.md), и [Создание конвейеры](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="12e7c-232">toolearn about time series datasets, scheduling, and slices, see [Creating datasets](data-factory-create-datasets.md), [Scheduling and execution](data-factory-scheduling-and-execution.md), and [Creating pipelines](data-factory-create-pipelines.md).</span></span>

#### <a name="sample-1"></a><span data-ttu-id="12e7c-233">Пример 1</span><span class="sxs-lookup"><span data-stu-id="12e7c-233">Sample 1</span></span>

```json
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```
<span data-ttu-id="12e7c-234">В этом примере {Slice} заменяется hello значение системной переменной фабрики данных SliceStart, в hello форматирования заданного (ГГГГММДДЧЧ).</span><span class="sxs-lookup"><span data-stu-id="12e7c-234">In this example, {Slice} is replaced with hello value of Data Factory system variable SliceStart, in hello format specified (YYYYMMDDHH).</span></span> <span data-ttu-id="12e7c-235">Hello SliceStart ссылается toostart время hello среза.</span><span class="sxs-lookup"><span data-stu-id="12e7c-235">hello SliceStart refers toostart time of hello slice.</span></span> <span data-ttu-id="12e7c-236">путь к папке Hello отличается для каждого среза.</span><span class="sxs-lookup"><span data-stu-id="12e7c-236">hello folder path is different for each slice.</span></span> <span data-ttu-id="12e7c-237">(Пример: wikidatagateway/wikisampledataout/2014100103 или wikidatagateway/wikisampledataout/2014100104.)</span><span class="sxs-lookup"><span data-stu-id="12e7c-237">(For example, wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104.)</span></span>

#### <a name="sample-2"></a><span data-ttu-id="12e7c-238">Пример 2</span><span class="sxs-lookup"><span data-stu-id="12e7c-238">Sample 2</span></span>

```json
"folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
"fileName": "{Hour}.csv",
"partitionedBy":
 [
    { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
    { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
    { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
    { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
],
```
<span data-ttu-id="12e7c-239">В этом примере hello год, месяц, день и время SliceStart извлекаются в отдельные переменные, используемые hello **folderPath** и **fileName** свойства.</span><span class="sxs-lookup"><span data-stu-id="12e7c-239">In this example, hello year, month, day, and time of SliceStart are extracted into separate variables that are used by hello **folderPath** and **fileName** properties.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="12e7c-240">Свойства действия копирования</span><span class="sxs-lookup"><span data-stu-id="12e7c-240">Copy activity properties</span></span>
<span data-ttu-id="12e7c-241">Полный список разделов и свойств, доступных для определения действий, см. в разделе [Конвейеры и действия в фабрике данных Azure](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="12e7c-241">For a full list of sections and properties available for defining activities, see [Creating pipelines](data-factory-create-pipelines.md).</span></span> <span data-ttu-id="12e7c-242">Свойства (такие как имя, описание, входные и выходные таблицы, политики и т. д.) доступны для всех типов действий.</span><span class="sxs-lookup"><span data-stu-id="12e7c-242">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="12e7c-243">Свойства, доступные в hello **typeProperties** раздел Здравствуйте действия на hello другой стороны, могут различаться для каждого типа действия.</span><span class="sxs-lookup"><span data-stu-id="12e7c-243">Properties available in hello **typeProperties** section of hello activity, on hello other hand, vary with each activity type.</span></span> <span data-ttu-id="12e7c-244">Для действия копирования hello hello тип свойства зависят от типов hello источники и приемники.</span><span class="sxs-lookup"><span data-stu-id="12e7c-244">For hello copy activity, hello type properties vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="12e7c-245">В действии копирования, когда источник hello типа **FileSystemSource**, hello следующие свойства доступны в **typeProperties** раздела:</span><span class="sxs-lookup"><span data-stu-id="12e7c-245">In copy activity, when hello source is of type **FileSystemSource**, hello following property is available in **typeProperties** section:</span></span>

| <span data-ttu-id="12e7c-246">Свойство</span><span class="sxs-lookup"><span data-stu-id="12e7c-246">Property</span></span> | <span data-ttu-id="12e7c-247">Описание</span><span class="sxs-lookup"><span data-stu-id="12e7c-247">Description</span></span> | <span data-ttu-id="12e7c-248">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="12e7c-248">Allowed values</span></span> | <span data-ttu-id="12e7c-249">Обязательно</span><span class="sxs-lookup"><span data-stu-id="12e7c-249">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="12e7c-250">recursive</span><span class="sxs-lookup"><span data-stu-id="12e7c-250">recursive</span></span> |<span data-ttu-id="12e7c-251">Указывает, доступна ли для чтения рекурсивно hello данные из вложенных папок hello, или только из указанной папки hello.</span><span class="sxs-lookup"><span data-stu-id="12e7c-251">Indicates whether hello data is read recursively from hello subfolders, or only from hello specified folder.</span></span> |<span data-ttu-id="12e7c-252">True, False (по умолчанию)</span><span class="sxs-lookup"><span data-stu-id="12e7c-252">True, False (default)</span></span> |<span data-ttu-id="12e7c-253">Нет</span><span class="sxs-lookup"><span data-stu-id="12e7c-253">No</span></span> |

## <a name="json-example-copy-data-from-ftp-server-tooazure-blob"></a><span data-ttu-id="12e7c-254">Пример JSON: копирование данных из сервера FTP tooAzure больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="12e7c-254">JSON example: Copy data from FTP server tooAzure Blob</span></span>
<span data-ttu-id="12e7c-255">В этом примере показано, как данные toocopy из tooAzure сервера FTP хранилища больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="12e7c-255">This sample shows how toocopy data from an FTP server tooAzure Blob storage.</span></span> <span data-ttu-id="12e7c-256">Тем не менее, данные можно скопировать непосредственно tooany из hello приемники уже говорилось в hello [поддерживаемых хранилищ данных и форматы](data-factory-data-movement-activities.md#supported-data-stores-and-formats), с помощью действия копирования hello в фабрике данных.</span><span class="sxs-lookup"><span data-stu-id="12e7c-256">However, data can be copied directly tooany of hello sinks stated in hello [supported data stores and formats](data-factory-data-movement-activities.md#supported-data-stores-and-formats), by using hello copy activity in Data Factory.</span></span>  

<span data-ttu-id="12e7c-257">Hello ниже приведены примеры определения образца JSON можно использовать toocreate конвейера с помощью [портал Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), или [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md):</span><span class="sxs-lookup"><span data-stu-id="12e7c-257">hello following examples provide sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md):</span></span>

* <span data-ttu-id="12e7c-258">Связанная служба типа [FtpServer](#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="12e7c-258">A linked service of type [FtpServer](#linked-service-properties)</span></span>
* <span data-ttu-id="12e7c-259">Связанная служба типа [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="12e7c-259">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span></span>
* <span data-ttu-id="12e7c-260">Входной [набор данных](data-factory-create-datasets.md) типа [FileShare](#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="12e7c-260">An input [dataset](data-factory-create-datasets.md) of type [FileShare](#dataset-properties)</span></span>
* <span data-ttu-id="12e7c-261">Выходной [набор данных](data-factory-create-datasets.md) типа [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="12e7c-261">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span></span>
* <span data-ttu-id="12e7c-262">[Конвейер](data-factory-create-pipelines.md) с действием копирования, в котором используются [FileSystemSource](#copy-activity-properties) и [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)</span><span class="sxs-lookup"><span data-stu-id="12e7c-262">A [pipeline](data-factory-create-pipelines.md) with copy activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)</span></span>

<span data-ttu-id="12e7c-263">Образец Hello копирует данные из tooan сервера FTP BLOB-объектов Azure каждый час.</span><span class="sxs-lookup"><span data-stu-id="12e7c-263">hello sample copies data from an FTP server tooan Azure blob every hour.</span></span> <span data-ttu-id="12e7c-264">свойства Hello JSON, используемые в этих примерах описаны в разделах, следующие примеры hello.</span><span class="sxs-lookup"><span data-stu-id="12e7c-264">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

### <a name="ftp-linked-service"></a><span data-ttu-id="12e7c-265">Связанная служба FTP</span><span class="sxs-lookup"><span data-stu-id="12e7c-265">FTP linked service</span></span>

<span data-ttu-id="12e7c-266">Этот пример использует обычную проверку подлинности с hello имя пользователя и пароль в виде обычного текста.</span><span class="sxs-lookup"><span data-stu-id="12e7c-266">This example uses basic authentication, with hello user name and password in plain text.</span></span> <span data-ttu-id="12e7c-267">Также можно использовать один из следующих способов hello:</span><span class="sxs-lookup"><span data-stu-id="12e7c-267">You can also use one of hello following ways:</span></span>

* <span data-ttu-id="12e7c-268">анонимная аутентификация;</span><span class="sxs-lookup"><span data-stu-id="12e7c-268">Anonymous authentication</span></span>
* <span data-ttu-id="12e7c-269">обычная аутентификация и шифрование учетных данных;</span><span class="sxs-lookup"><span data-stu-id="12e7c-269">Basic authentication with encrypted credentials</span></span>
* <span data-ttu-id="12e7c-270">FTP через SSL или TLS (FTPS).</span><span class="sxs-lookup"><span data-stu-id="12e7c-270">FTP over SSL/TLS (FTPS)</span></span>

<span data-ttu-id="12e7c-271">В разделе hello [FTP связанная служба](#linked-service-properties) раздел для различных типов проверки подлинности, можно использовать.</span><span class="sxs-lookup"><span data-stu-id="12e7c-271">See hello [FTP linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

```JSON
{
    "name": "FTPLinkedService",
    "properties": {
    "type": "FtpServer",
    "typeProperties": {
        "host": "myftpserver.com",           
        "authenticationType": "Basic",
        "username": "Admin",
        "password": "123456"
    }
  }
}
```
### <a name="azure-storage-linked-service"></a><span data-ttu-id="12e7c-272">Связанная служба хранения Azure</span><span class="sxs-lookup"><span data-stu-id="12e7c-272">Azure Storage linked service</span></span>

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
### <a name="ftp-input-dataset"></a><span data-ttu-id="12e7c-273">Входной набор данных FTP</span><span class="sxs-lookup"><span data-stu-id="12e7c-273">FTP input dataset</span></span>

<span data-ttu-id="12e7c-274">Этот набор данных указывает папку toohello FTP `mysharedfolder` и файл `test.csv`.</span><span class="sxs-lookup"><span data-stu-id="12e7c-274">This dataset refers toohello FTP folder `mysharedfolder` and file `test.csv`.</span></span> <span data-ttu-id="12e7c-275">конвейер Hello копирует hello файл toohello назначения.</span><span class="sxs-lookup"><span data-stu-id="12e7c-275">hello pipeline copies hello file toohello destination.</span></span>

<span data-ttu-id="12e7c-276">Установка **внешних** слишком**true** информирует hello служба фабрики данных, набор данных hello внешних toohello фабрики данных и не был создан из действия в фабрике данных hello.</span><span class="sxs-lookup"><span data-stu-id="12e7c-276">Setting **external** too**true** informs hello Data Factory service that hello dataset is external toohello data factory, and is not produced by an activity in hello data factory.</span></span>

```JSON
{
  "name": "FTPFileInput",
  "properties": {
    "type": "FileShare",
    "linkedServiceName": "FTPLinkedService",
    "typeProperties": {
      "folderPath": "mysharedfolder",
      "fileName": "test.csv",
      "useBinaryTransfer": true
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

### <a name="azure-blob-output-dataset"></a><span data-ttu-id="12e7c-277">Выходной набор данных BLOB-объекта Azure</span><span class="sxs-lookup"><span data-stu-id="12e7c-277">Azure Blob output dataset</span></span>

<span data-ttu-id="12e7c-278">Записывается новый большой двоичный объект tooa каждый час (частота: час, интервал: 1).</span><span class="sxs-lookup"><span data-stu-id="12e7c-278">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="12e7c-279">путь к папке Hello для большого двоичного объекта hello динамически вычисляется, на основе времени начала hello hello среза, который обрабатывается.</span><span class="sxs-lookup"><span data-stu-id="12e7c-279">hello folder path for hello blob is dynamically evaluated, based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="12e7c-280">путь к папке Hello использует hello года, месяца, дня и часа части времени начала hello.</span><span class="sxs-lookup"><span data-stu-id="12e7c-280">hello folder path uses hello year, month, day, and hours parts of hello start time.</span></span>

```JSON
{
    "name": "AzureBlobOutput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/ftp/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            },
            "partitionedBy": [
                {
                    "name": "Year",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "yyyy"
                    }
                },
                {
                    "name": "Month",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "MM"
                    }
                },
                {
                    "name": "Day",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "dd"
                    }
                },
                {
                    "name": "Hour",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "HH"
                    }
                }
            ]
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```


### <a name="a-copy-activity-in-a-pipeline-with-file-system-source-and-blob-sink"></a><span data-ttu-id="12e7c-281">Действие копирования в конвейере с файловой системой в качестве источника и BLOB-объектом в качестве приемника</span><span class="sxs-lookup"><span data-stu-id="12e7c-281">A copy activity in a pipeline with file system source and blob sink</span></span>

<span data-ttu-id="12e7c-282">Hello конвейера содержит операции копирования, настроенные toouse hello наборы входных и выходных данных, а — запланированных toorun каждый час.</span><span class="sxs-lookup"><span data-stu-id="12e7c-282">hello pipeline contains a copy activity that is configured toouse hello input and output datasets, and is scheduled toorun every hour.</span></span> <span data-ttu-id="12e7c-283">В определении JSON конвейера hello, hello **источника** тип установлен слишком**FileSystemSource**и hello **приемник** тип установлен слишком**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="12e7c-283">In hello pipeline JSON definition, hello **source** type is set too**FileSystemSource**, and hello **sink** type is set too**BlobSink**.</span></span>

```JSON
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "FTPToBlobCopy",
            "inputs": [{
                "name": "FtpFileInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource"
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
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "00:05:00"
            }
        }],
        "start": "2016-08-24T18:00:00Z",
        "end": "2016-08-24T19:00:00Z"
    }
}
```
> [!NOTE]
> <span data-ttu-id="12e7c-284">toomap столбцы из источника toocolumns набора данных из набора данных приемников, в разделе [сопоставление столбцов набора данных в фабрике данных Azure](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="12e7c-284">toomap columns from source dataset toocolumns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="12e7c-285">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="12e7c-285">Next steps</span></span>
<span data-ttu-id="12e7c-286">См. следующие статьи hello.</span><span class="sxs-lookup"><span data-stu-id="12e7c-286">See hello following articles:</span></span>

* <span data-ttu-id="12e7c-287">toolearn о ключе факторы, оказывают влияние на производительность перемещения данных (действие копирования) в фабрике данных и различных способов toooptimize, разделе hello [копирование действия производительности и руководство по настройке](data-factory-copy-activity-performance.md).</span><span class="sxs-lookup"><span data-stu-id="12e7c-287">toolearn about key factors that impact performance of data movement (copy activity) in Data Factory, and various ways toooptimize it, see hello [Copy activity performance and tuning guide](data-factory-copy-activity-performance.md).</span></span>

* <span data-ttu-id="12e7c-288">Пошаговые инструкции для создания конвейера с помощью операции копирования см. в разделе hello [учебника действия копирования](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="12e7c-288">For step-by-step instructions for creating a pipeline with a copy activity, see hello [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
