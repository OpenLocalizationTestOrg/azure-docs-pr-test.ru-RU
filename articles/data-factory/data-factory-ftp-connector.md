---
title: "Перемещение данных с FTP-сервера с использованием фабрики данных Azure | Документы Майкрософт"
description: "Узнайте, как перемещать данные с FTP-сервера с использованием фабрики данных Azure."
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
ms.openlocfilehash: f8f31f3a2ee02c964737dd32145499f3dcfd0624
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="move-data-from-an-ftp-server-by-using-azure-data-factory"></a><span data-ttu-id="6e34c-103">Перемещение данных с FTP-сервера с использованием фабрики данных Azure</span><span class="sxs-lookup"><span data-stu-id="6e34c-103">Move data from an FTP server by using Azure Data Factory</span></span>
<span data-ttu-id="6e34c-104">В этой статье описывается, как с помощью действия копирования в фабрике данных Azure перемещать данные с FTP-сервера.</span><span class="sxs-lookup"><span data-stu-id="6e34c-104">This article explains how to use the copy activity in Azure Data Factory to move data from an FTP server.</span></span> <span data-ttu-id="6e34c-105">Это продолжение статьи о [действиях перемещения данных](data-factory-data-movement-activities.md), в которой приведены общие сведения о перемещении данных с помощью действия копирования.</span><span class="sxs-lookup"><span data-stu-id="6e34c-105">It builds on the [Data movement activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="6e34c-106">Данные с FTP-сервера можно скопировать в любое хранилище данных, поддерживаемое в качестве приемника.</span><span class="sxs-lookup"><span data-stu-id="6e34c-106">You can copy data from an FTP server to any supported sink data store.</span></span> <span data-ttu-id="6e34c-107">Список хранилищ данных, которые поддерживаются в качестве приемников для действия копирования, приведен в таблице [Поддерживаемые хранилища данных и форматы](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="6e34c-107">For a list of data stores supported as sinks by the copy activity, see the [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="6e34c-108">Сейчас фабрика данных поддерживает только перемещение данных с FTP-сервера в другие хранилища данных, но не наоборот.</span><span class="sxs-lookup"><span data-stu-id="6e34c-108">Data Factory currently supports only moving data from an FTP server to other data stores, but not moving data from other data stores to an FTP server.</span></span> <span data-ttu-id="6e34c-109">Она поддерживает локальные и облачные FTP-серверы.</span><span class="sxs-lookup"><span data-stu-id="6e34c-109">It supports both on-premises and cloud FTP servers.</span></span>

> [!NOTE]
> <span data-ttu-id="6e34c-110">Действие копирования не удаляет исходный файл после его успешного копирования в место назначения.</span><span class="sxs-lookup"><span data-stu-id="6e34c-110">The copy activity does not delete the source file after it is successfully copied to the destination.</span></span> <span data-ttu-id="6e34c-111">Если необходимо удалить исходный файл после успешного копирования, создайте настраиваемое действие для удаления файла и используйте это действие в конвейере.</span><span class="sxs-lookup"><span data-stu-id="6e34c-111">If you need to delete the source file after a successful copy, create a custom activity to delete the file, and use the activity in the pipeline.</span></span> 

## <a name="enable-connectivity"></a><span data-ttu-id="6e34c-112">Включение соединения</span><span class="sxs-lookup"><span data-stu-id="6e34c-112">Enable connectivity</span></span>
<span data-ttu-id="6e34c-113">При перемещении данных с **локального** FTP-сервера в облачное хранилище данных (например, хранилище BLOB-объектов Azure) установите и используйте шлюз управления данными.</span><span class="sxs-lookup"><span data-stu-id="6e34c-113">If you are moving data from an **on-premises** FTP server to a cloud data store (for example, to Azure Blob storage), install and use Data Management Gateway.</span></span> <span data-ttu-id="6e34c-114">Шлюз управления данными — это агент клиента, установленный на локальном компьютере и позволяющий облачным службам подключаться к локальному ресурсу.</span><span class="sxs-lookup"><span data-stu-id="6e34c-114">The Data Management Gateway is a client agent that is installed on your on-premises machine, and it allows cloud services to connect to an on-premises resource.</span></span> <span data-ttu-id="6e34c-115">Подробные сведения см. в разделе [Шлюз управления данными](data-factory-data-management-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="6e34c-115">For details, see [Data Management Gateway](data-factory-data-management-gateway.md).</span></span> <span data-ttu-id="6e34c-116">Пошаговые инструкции по настройке и использованию шлюза см. в разделе [Перемещение данных между локальными источниками и облаком](data-factory-move-data-between-onprem-and-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="6e34c-116">For step-by-step instructions on setting up the gateway and using it, see [Moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md).</span></span> <span data-ttu-id="6e34c-117">Шлюз используется для подключения к FTP-серверу, даже если сервер выполняется на виртуальной машине Azure типа "инфраструктура как услуга" (IaaS).</span><span class="sxs-lookup"><span data-stu-id="6e34c-117">You use the gateway to connect to an FTP server, even if the server is on an Azure infrastructure as a service (IaaS) virtual machine (VM).</span></span>

<span data-ttu-id="6e34c-118">Шлюз можно установить на тот же локальный компьютер или виртуальную машину Azure IaaS, что и FTP-сервер.</span><span class="sxs-lookup"><span data-stu-id="6e34c-118">It is possible to install the gateway on the same on-premises machine or IaaS VM as the FTP server.</span></span> <span data-ttu-id="6e34c-119">Тем не менее рекомендуется установить шлюз на отдельный компьютер или виртуальную машину IaaS, чтобы избежать состязания за ресурсы, а также для повышения производительности.</span><span class="sxs-lookup"><span data-stu-id="6e34c-119">However, we recommend that you install the gateway on a separate machine or IaaS VM to avoid resource contention, and for better performance.</span></span> <span data-ttu-id="6e34c-120">При установке шлюза на отдельный компьютер у компьютера должен быть доступ к FTP-серверу.</span><span class="sxs-lookup"><span data-stu-id="6e34c-120">When you install the gateway on a separate machine, the machine should be able to access the FTP server.</span></span>

## <a name="get-started"></a><span data-ttu-id="6e34c-121">Начало работы</span><span class="sxs-lookup"><span data-stu-id="6e34c-121">Get started</span></span>
<span data-ttu-id="6e34c-122">Вы можете создать конвейер с действием копирования, который перемещает данные с исходного FTP-сервера, с помощью разных средств или интерфейсов API.</span><span class="sxs-lookup"><span data-stu-id="6e34c-122">You can create a pipeline with a copy activity that moves data from an FTP source by using different tools or APIs.</span></span>

<span data-ttu-id="6e34c-123">Проще всего создать конвейер с помощью **мастера копирования фабрики данных**.</span><span class="sxs-lookup"><span data-stu-id="6e34c-123">The easiest way to create a pipeline is to use the **Data Factory Copy Wizard**.</span></span> <span data-ttu-id="6e34c-124">Краткое пошаговое руководство представлено в статье [Руководство. Создание конвейера с действием копирования с помощью мастера копирования фабрики данных](data-factory-copy-data-wizard-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="6e34c-124">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough.</span></span>

<span data-ttu-id="6e34c-125">Также для создания конвейера можно использовать следующие средства: **портал Azure**, **Visual Studio**, **PowerShell**, **шаблон Azure Resource Manager**, **API .NET** и **REST API**.</span><span class="sxs-lookup"><span data-stu-id="6e34c-125">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="6e34c-126">Пошаговые инструкции по созданию конвейера с действием копирования см. в [руководстве по действию копирования](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="6e34c-126">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span>

<span data-ttu-id="6e34c-127">Независимо от используемого средства или интерфейса API для создания конвейера, который перемещает данные из исходного хранилища данных в приемник, необходимо выполнить указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="6e34c-127">Whether you use the tools or APIs, perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="6e34c-128">Создайте **связанные службы**, чтобы связать входные и выходные данные с фабрикой данных.</span><span class="sxs-lookup"><span data-stu-id="6e34c-128">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="6e34c-129">Создайте **наборы данных**, которые представляют входные и выходные данные для операции копирования.</span><span class="sxs-lookup"><span data-stu-id="6e34c-129">Create **datasets** to represent input and output data for the copy operation.</span></span>
3. <span data-ttu-id="6e34c-130">Создайте **конвейер** с действием копирования, который принимает входной набор данных и возвращает выходной набор данных.</span><span class="sxs-lookup"><span data-stu-id="6e34c-130">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span>

<span data-ttu-id="6e34c-131">Если вы используете мастер, то он автоматически создает определения JSON для сущностей фабрики данных (связанных служб, наборов данных и конвейера).</span><span class="sxs-lookup"><span data-stu-id="6e34c-131">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="6e34c-132">При использовании средств или интерфейсов API (за исключением API .NET) вы самостоятельно определяете эти сущности фабрики данных в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="6e34c-132">When you use tools or APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span> <span data-ttu-id="6e34c-133">Пример определений JSON для сущностей фабрики данных, которые используются для копирования данных из хранилища данных FTP, доступен в разделе [Пример JSON. Копирование данных с FTP-сервера в большой двоичный объект Azure](#json-example-copy-data-from-ftp-server-to-azure-blob) этой статьи.</span><span class="sxs-lookup"><span data-stu-id="6e34c-133">For a sample with JSON definitions for Data Factory entities that are used to copy data from an FTP data store, see the [JSON example: Copy data from FTP server to Azure blob](#json-example-copy-data-from-ftp-server-to-azure-blob) section of this article.</span></span>

> [!NOTE]
> <span data-ttu-id="6e34c-134">Подробные сведения о поддерживаемых форматах файлов и сжатия см. в разделе [Форматы файлов и сжатия данных, поддерживаемые фабрикой данных Azure](data-factory-supported-file-and-compression-formats.md).</span><span class="sxs-lookup"><span data-stu-id="6e34c-134">For details about supported file and compression formats to use, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md).</span></span>

<span data-ttu-id="6e34c-135">Следующие разделы содержат сведения о свойствах JSON, которые используются для определения сущностей фабрики данных, относящихся к FTP.</span><span class="sxs-lookup"><span data-stu-id="6e34c-135">The following sections provide details about JSON properties that are used to define Data Factory entities specific to FTP.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="6e34c-136">Свойства связанной службы</span><span class="sxs-lookup"><span data-stu-id="6e34c-136">Linked service properties</span></span>
<span data-ttu-id="6e34c-137">В приведенной ниже таблице описываются элементы JSON, которые относятся к связанной службе FTP.</span><span class="sxs-lookup"><span data-stu-id="6e34c-137">The following table describes JSON elements specific to an FTP linked service.</span></span>

| <span data-ttu-id="6e34c-138">Свойство</span><span class="sxs-lookup"><span data-stu-id="6e34c-138">Property</span></span> | <span data-ttu-id="6e34c-139">Описание</span><span class="sxs-lookup"><span data-stu-id="6e34c-139">Description</span></span> | <span data-ttu-id="6e34c-140">Обязательно</span><span class="sxs-lookup"><span data-stu-id="6e34c-140">Required</span></span> | <span data-ttu-id="6e34c-141">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="6e34c-141">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6e34c-142">type</span><span class="sxs-lookup"><span data-stu-id="6e34c-142">type</span></span> |<span data-ttu-id="6e34c-143">Задайте значение FtpServer.</span><span class="sxs-lookup"><span data-stu-id="6e34c-143">Set this to FtpServer.</span></span> |<span data-ttu-id="6e34c-144">Да</span><span class="sxs-lookup"><span data-stu-id="6e34c-144">Yes</span></span> |&nbsp; |
| <span data-ttu-id="6e34c-145">host</span><span class="sxs-lookup"><span data-stu-id="6e34c-145">host</span></span> |<span data-ttu-id="6e34c-146">Укажите имя или IP-адрес FTP-сервера.</span><span class="sxs-lookup"><span data-stu-id="6e34c-146">Specify the name or IP address of the FTP server.</span></span> |<span data-ttu-id="6e34c-147">Да</span><span class="sxs-lookup"><span data-stu-id="6e34c-147">Yes</span></span> |&nbsp; |
| <span data-ttu-id="6e34c-148">authenticationType</span><span class="sxs-lookup"><span data-stu-id="6e34c-148">authenticationType</span></span> |<span data-ttu-id="6e34c-149">Укажите тип проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="6e34c-149">Specify the authentication type.</span></span> |<span data-ttu-id="6e34c-150">Да</span><span class="sxs-lookup"><span data-stu-id="6e34c-150">Yes</span></span> |<span data-ttu-id="6e34c-151">Обычная, анонимная</span><span class="sxs-lookup"><span data-stu-id="6e34c-151">Basic, Anonymous</span></span> |
| <span data-ttu-id="6e34c-152">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="6e34c-152">username</span></span> |<span data-ttu-id="6e34c-153">Укажите пользователя, имеющего доступ к FTP-серверу.</span><span class="sxs-lookup"><span data-stu-id="6e34c-153">Specify the user who has access to the FTP server.</span></span> |<span data-ttu-id="6e34c-154">Нет</span><span class="sxs-lookup"><span data-stu-id="6e34c-154">No</span></span> |&nbsp; |
| <span data-ttu-id="6e34c-155">пароль</span><span class="sxs-lookup"><span data-stu-id="6e34c-155">password</span></span> |<span data-ttu-id="6e34c-156">Укажите пароль для пользователя (username).</span><span class="sxs-lookup"><span data-stu-id="6e34c-156">Specify the password for the user (username).</span></span> |<span data-ttu-id="6e34c-157">Нет</span><span class="sxs-lookup"><span data-stu-id="6e34c-157">No</span></span> |&nbsp; |
| <span data-ttu-id="6e34c-158">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="6e34c-158">encryptedCredential</span></span> |<span data-ttu-id="6e34c-159">Укажите зашифрованные учетные данные для доступа к FTP-серверу.</span><span class="sxs-lookup"><span data-stu-id="6e34c-159">Specify the encrypted credential to access the FTP server.</span></span> |<span data-ttu-id="6e34c-160">Нет</span><span class="sxs-lookup"><span data-stu-id="6e34c-160">No</span></span> |&nbsp; |
| <span data-ttu-id="6e34c-161">gatewayName</span><span class="sxs-lookup"><span data-stu-id="6e34c-161">gatewayName</span></span> |<span data-ttu-id="6e34c-162">Укажите имя шлюза управления данными для подключения к локальному FTP-серверу.</span><span class="sxs-lookup"><span data-stu-id="6e34c-162">Specify the name of the gateway in Data Management Gateway to connect to an on-premises FTP server.</span></span> |<span data-ttu-id="6e34c-163">Нет</span><span class="sxs-lookup"><span data-stu-id="6e34c-163">No</span></span> |&nbsp; |
| <span data-ttu-id="6e34c-164">порт</span><span class="sxs-lookup"><span data-stu-id="6e34c-164">port</span></span> |<span data-ttu-id="6e34c-165">Укажите порт, прослушиваемый FTP-сервером.</span><span class="sxs-lookup"><span data-stu-id="6e34c-165">Specify the port on which the FTP server is listening.</span></span> |<span data-ttu-id="6e34c-166">Нет</span><span class="sxs-lookup"><span data-stu-id="6e34c-166">No</span></span> |<span data-ttu-id="6e34c-167">21</span><span class="sxs-lookup"><span data-stu-id="6e34c-167">21</span></span> |
| <span data-ttu-id="6e34c-168">enableSsl</span><span class="sxs-lookup"><span data-stu-id="6e34c-168">enableSsl</span></span> |<span data-ttu-id="6e34c-169">Укажите, какой канал следует использовать (FTP через SSL или TLS).</span><span class="sxs-lookup"><span data-stu-id="6e34c-169">Specify whether to use FTP over an SSL/TLS channel.</span></span> |<span data-ttu-id="6e34c-170">Нет</span><span class="sxs-lookup"><span data-stu-id="6e34c-170">No</span></span> |<span data-ttu-id="6e34c-171">Да</span><span class="sxs-lookup"><span data-stu-id="6e34c-171">true</span></span> |
| <span data-ttu-id="6e34c-172">enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="6e34c-172">enableServerCertificateValidation</span></span> |<span data-ttu-id="6e34c-173">Укажите, следует ли включать проверку SSL-сертификата на сервере при использовании канала FTP через SSL или TLS.</span><span class="sxs-lookup"><span data-stu-id="6e34c-173">Specify whether to enable server SSL certificate validation when you are using FTP over SSL/TLS channel.</span></span> |<span data-ttu-id="6e34c-174">Нет</span><span class="sxs-lookup"><span data-stu-id="6e34c-174">No</span></span> |<span data-ttu-id="6e34c-175">Да</span><span class="sxs-lookup"><span data-stu-id="6e34c-175">true</span></span> |

### <a name="use-anonymous-authentication"></a><span data-ttu-id="6e34c-176">Использование анонимной проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="6e34c-176">Use Anonymous authentication</span></span>

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

### <a name="use-username-and-password-in-plain-text-for-basic-authentication"></a><span data-ttu-id="6e34c-177">Использование имени пользователя и пароля в виде обычного текста для обычной проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="6e34c-177">Use username and password in plain text for basic authentication</span></span>

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

### <a name="use-port-enablessl-enableservercertificatevalidation"></a><span data-ttu-id="6e34c-178">Использование свойств port, enableSsl, enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="6e34c-178">Use port, enableSsl, enableServerCertificateValidation</span></span>

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

### <a name="use-encryptedcredential-for-authentication-and-gateway"></a><span data-ttu-id="6e34c-179">Использование свойства encryptedCredential для проверки подлинности и шлюза</span><span class="sxs-lookup"><span data-stu-id="6e34c-179">Use encryptedCredential for authentication and gateway</span></span>

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

## <a name="dataset-properties"></a><span data-ttu-id="6e34c-180">Свойства набора данных</span><span class="sxs-lookup"><span data-stu-id="6e34c-180">Dataset properties</span></span>
<span data-ttu-id="6e34c-181">Полный список разделов и свойств, доступных для определения наборов данных, см. в разделе [Наборы данных в фабрике данных Azure](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="6e34c-181">For a full list of sections and properties available for defining datasets, see [Creating datasets](data-factory-create-datasets.md).</span></span> <span data-ttu-id="6e34c-182">Разделы структуры, доступности и политики JSON набора данных одинаковы для всех типов наборов данных.</span><span class="sxs-lookup"><span data-stu-id="6e34c-182">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types.</span></span>

<span data-ttu-id="6e34c-183">Разделы **typeProperties** для каждого типа набора данных отличаются.</span><span class="sxs-lookup"><span data-stu-id="6e34c-183">The **typeProperties** section is different for each type of dataset.</span></span> <span data-ttu-id="6e34c-184">Он предоставляет сведения, которые относятся к типу набора данных.</span><span class="sxs-lookup"><span data-stu-id="6e34c-184">It provides information that is specific to the dataset type.</span></span> <span data-ttu-id="6e34c-185">Раздел **typeProperties** набора данных типа **FileShare** содержит перечисленные ниже свойства.</span><span class="sxs-lookup"><span data-stu-id="6e34c-185">The **typeProperties** section for a dataset of type **FileShare** has the following properties:</span></span>

| <span data-ttu-id="6e34c-186">Свойство</span><span class="sxs-lookup"><span data-stu-id="6e34c-186">Property</span></span> | <span data-ttu-id="6e34c-187">Описание</span><span class="sxs-lookup"><span data-stu-id="6e34c-187">Description</span></span> | <span data-ttu-id="6e34c-188">Обязательно</span><span class="sxs-lookup"><span data-stu-id="6e34c-188">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6e34c-189">folderPath</span><span class="sxs-lookup"><span data-stu-id="6e34c-189">folderPath</span></span> |<span data-ttu-id="6e34c-190">Подпуть к папке.</span><span class="sxs-lookup"><span data-stu-id="6e34c-190">Subpath to the folder.</span></span> <span data-ttu-id="6e34c-191">Чтобы указать специальные знаки в строке, используйте escape-знак "\".</span><span class="sxs-lookup"><span data-stu-id="6e34c-191">Use escape character ‘ \ ’ for special characters in the string.</span></span> <span data-ttu-id="6e34c-192">Примеры приведены в разделе [Примеры определений связанной службы и набора данных](#sample-linked-service-and-dataset-definitions).</span><span class="sxs-lookup"><span data-stu-id="6e34c-192">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="6e34c-193">Вы можете использовать это свойство вместе с параметром **partitionBy**, чтобы в путях к папкам учитывались дата и время начала и окончания среза.</span><span class="sxs-lookup"><span data-stu-id="6e34c-193">You can combine this property with **partitionBy** to have folder paths based on slice start and end date-times.</span></span> |<span data-ttu-id="6e34c-194">Да</span><span class="sxs-lookup"><span data-stu-id="6e34c-194">Yes</span></span> |
| <span data-ttu-id="6e34c-195">fileName</span><span class="sxs-lookup"><span data-stu-id="6e34c-195">fileName</span></span> |<span data-ttu-id="6e34c-196">Укажите имя файла в папке **folderPath** , если таблица должна ссылаться на определенный файл в папке.</span><span class="sxs-lookup"><span data-stu-id="6e34c-196">Specify the name of the file in the **folderPath** if you want the table to refer to a specific file in the folder.</span></span> <span data-ttu-id="6e34c-197">Если этому свойству не присвоить значение, таблица будет указывать на все файлы в папке.</span><span class="sxs-lookup"><span data-stu-id="6e34c-197">If you do not specify any value for this property, the table points to all files in the folder.</span></span><br/><br/><span data-ttu-id="6e34c-198">Если свойство **fileName** не указано для выходного набора данных, то имя созданного файла будет иметь следующий формат:</span><span class="sxs-lookup"><span data-stu-id="6e34c-198">When **fileName** is not specified for an output dataset, the name of the generated file is in the following format:</span></span> <br/><br/><span data-ttu-id="6e34c-199">Data.<Guid>.txt (пример: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span><span class="sxs-lookup"><span data-stu-id="6e34c-199">Data.<Guid>.txt (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span></span> |<span data-ttu-id="6e34c-200">Нет</span><span class="sxs-lookup"><span data-stu-id="6e34c-200">No</span></span> |
| <span data-ttu-id="6e34c-201">fileFilter</span><span class="sxs-lookup"><span data-stu-id="6e34c-201">fileFilter</span></span> |<span data-ttu-id="6e34c-202">Укажите фильтр для выбора подмножества файлов из **folderPath**. Фильтр дает возможность выбирать только некоторые файлы, а не все.</span><span class="sxs-lookup"><span data-stu-id="6e34c-202">Specify a filter to be used to select a subset of files in the **folderPath**, rather than all files.</span></span><br/><br/><span data-ttu-id="6e34c-203">Допустимые значения: `*` (несколько знаков) и `?` (один знак).</span><span class="sxs-lookup"><span data-stu-id="6e34c-203">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="6e34c-204">Пример 1: `"fileFilter": "*.log"`</span><span class="sxs-lookup"><span data-stu-id="6e34c-204">Example 1: `"fileFilter": "*.log"`</span></span><br/><span data-ttu-id="6e34c-205">Пример 2: `"fileFilter": 2014-1-?.txt"`</span><span class="sxs-lookup"><span data-stu-id="6e34c-205">Example 2: `"fileFilter": 2014-1-?.txt"`</span></span><br/><br/> <span data-ttu-id="6e34c-206">Свойство **fileFilter** применяется ко входному набору данных FileShare.</span><span class="sxs-lookup"><span data-stu-id="6e34c-206">**fileFilter** is applicable for an input FileShare dataset.</span></span> <span data-ttu-id="6e34c-207">Распределенная файловая система Hadoop (HDFS) не поддерживает это свойство.</span><span class="sxs-lookup"><span data-stu-id="6e34c-207">This property is not supported with Hadoop Distributed File System (HDFS).</span></span> |<span data-ttu-id="6e34c-208">Нет</span><span class="sxs-lookup"><span data-stu-id="6e34c-208">No</span></span> |
| <span data-ttu-id="6e34c-209">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="6e34c-209">partitionedBy</span></span> |<span data-ttu-id="6e34c-210">Используется для того, чтобы указать динамические **путь к папке** и **имя файла** для временного ряда данных.</span><span class="sxs-lookup"><span data-stu-id="6e34c-210">Used to specify a dynamic **folderPath** and **fileName** for time series data.</span></span> <span data-ttu-id="6e34c-211">Например, можно указать **путь к папке**, который будет параметризироваться для данных за каждый час.</span><span class="sxs-lookup"><span data-stu-id="6e34c-211">For example, you can specify a **folderPath** that is parameterized for every hour of data.</span></span> |<span data-ttu-id="6e34c-212">Нет</span><span class="sxs-lookup"><span data-stu-id="6e34c-212">No</span></span> |
| <span data-ttu-id="6e34c-213">свойства</span><span class="sxs-lookup"><span data-stu-id="6e34c-213">format</span></span> | <span data-ttu-id="6e34c-214">Поддерживаются следующие типы формата: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="6e34c-214">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="6e34c-215">Свойству **type** в разделе format необходимо присвоить одно из этих значений.</span><span class="sxs-lookup"><span data-stu-id="6e34c-215">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="6e34c-216">Дополнительные сведения см. в разделах о [текстовом формате](data-factory-supported-file-and-compression-formats.md#text-format), [формате Json](data-factory-supported-file-and-compression-formats.md#json-format), [формате Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [формате Orc](data-factory-supported-file-and-compression-formats.md#orc-format) и [формате Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="6e34c-216">For more information, see the [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="6e34c-217">Если требуется скопировать файлы между файловыми хранилищами как есть (двоичное копирование), пропустите раздел формата в определениях входного и выходного наборов данных.</span><span class="sxs-lookup"><span data-stu-id="6e34c-217">If you want to copy files as they are between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="6e34c-218">Нет</span><span class="sxs-lookup"><span data-stu-id="6e34c-218">No</span></span> |
| <span data-ttu-id="6e34c-219">compression</span><span class="sxs-lookup"><span data-stu-id="6e34c-219">compression</span></span> | <span data-ttu-id="6e34c-220">Укажите тип и уровень сжатия данных.</span><span class="sxs-lookup"><span data-stu-id="6e34c-220">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="6e34c-221">Поддерживаемые типы: **GZip**, **Deflate**, **BZip2** и **ZipDeflate**. Поддерживаемые уровни: **Optimal** и **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="6e34c-221">Supported types are **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**, and supported levels are **Optimal** and **Fastest**.</span></span> <span data-ttu-id="6e34c-222">См. дополнительные сведения о [форматах файлов и сжатия данных в фабрике данных Azure](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="6e34c-222">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="6e34c-223">Нет</span><span class="sxs-lookup"><span data-stu-id="6e34c-223">No</span></span> |
| <span data-ttu-id="6e34c-224">useBinaryTransfer</span><span class="sxs-lookup"><span data-stu-id="6e34c-224">useBinaryTransfer</span></span> |<span data-ttu-id="6e34c-225">Укажите, следует ли использовать режим передачи в двоичном формате.</span><span class="sxs-lookup"><span data-stu-id="6e34c-225">Specify whether to use the binary transfer mode.</span></span> <span data-ttu-id="6e34c-226">Значение true, если следует использовать двоичный формат (это значение по умолчанию), и false, если следует использовать ASCII.</span><span class="sxs-lookup"><span data-stu-id="6e34c-226">The values are true for binary mode (this is the default value), and false for ASCII.</span></span> <span data-ttu-id="6e34c-227">Это свойство можно использовать, только когда тип связанной службы — FtpServer.</span><span class="sxs-lookup"><span data-stu-id="6e34c-227">This property can only be used when the associated linked service type is of type: FtpServer.</span></span> |<span data-ttu-id="6e34c-228">Нет</span><span class="sxs-lookup"><span data-stu-id="6e34c-228">No</span></span> |

> [!NOTE]
> <span data-ttu-id="6e34c-229">Свойства **fileName** и **fileFilter** нельзя использовать одновременно.</span><span class="sxs-lookup"><span data-stu-id="6e34c-229">**fileName** and **fileFilter** cannot be used simultaneously.</span></span>

### <a name="use-the-partionedby-property"></a><span data-ttu-id="6e34c-230">Использование свойства partionedBy</span><span class="sxs-lookup"><span data-stu-id="6e34c-230">Use the partionedBy property</span></span>
<span data-ttu-id="6e34c-231">Как сказано выше, для данных временных рядов путь к папке (**folderPath**) и имя файла (**fileName**) можно указывать динамически. Это делается с помощью свойства **partitionedBy**.</span><span class="sxs-lookup"><span data-stu-id="6e34c-231">As mentioned in the previous section, you can specify a dynamic **folderPath** and **fileName** for time series data with the **partitionedBy** property.</span></span>

<span data-ttu-id="6e34c-232">Сведения о наборах данных временных рядов, планировании и срезах см. в разделах [Наборы данных в фабрике данных Azure](data-factory-create-datasets.md), [Планирование и исполнение с использованием фабрики данных](data-factory-scheduling-and-execution.md) и [Конвейеры и действия в фабрике данных Azure](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="6e34c-232">To learn about time series datasets, scheduling, and slices, see [Creating datasets](data-factory-create-datasets.md), [Scheduling and execution](data-factory-scheduling-and-execution.md), and [Creating pipelines](data-factory-create-pipelines.md).</span></span>

#### <a name="sample-1"></a><span data-ttu-id="6e34c-233">Пример 1</span><span class="sxs-lookup"><span data-stu-id="6e34c-233">Sample 1</span></span>

```json
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```
<span data-ttu-id="6e34c-234">В этом примере {Slice} заменяется значением SliceStart (системная переменная фабрики данных) в формате ГГГГММДДЧЧ.</span><span class="sxs-lookup"><span data-stu-id="6e34c-234">In this example, {Slice} is replaced with the value of Data Factory system variable SliceStart, in the format specified (YYYYMMDDHH).</span></span> <span data-ttu-id="6e34c-235">SliceStart указывает время начала среза.</span><span class="sxs-lookup"><span data-stu-id="6e34c-235">The SliceStart refers to start time of the slice.</span></span> <span data-ttu-id="6e34c-236">Путь к папке отличается для каждого среза.</span><span class="sxs-lookup"><span data-stu-id="6e34c-236">The folder path is different for each slice.</span></span> <span data-ttu-id="6e34c-237">(Пример: wikidatagateway/wikisampledataout/2014100103 или wikidatagateway/wikisampledataout/2014100104.)</span><span class="sxs-lookup"><span data-stu-id="6e34c-237">(For example, wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104.)</span></span>

#### <a name="sample-2"></a><span data-ttu-id="6e34c-238">Пример 2</span><span class="sxs-lookup"><span data-stu-id="6e34c-238">Sample 2</span></span>

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
<span data-ttu-id="6e34c-239">В этом примере год, месяц, день и время SliceStart извлекаются в отдельные переменные, используемые в свойствах **folderPath** и **fileName**.</span><span class="sxs-lookup"><span data-stu-id="6e34c-239">In this example, the year, month, day, and time of SliceStart are extracted into separate variables that are used by the **folderPath** and **fileName** properties.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="6e34c-240">Свойства действия копирования</span><span class="sxs-lookup"><span data-stu-id="6e34c-240">Copy activity properties</span></span>
<span data-ttu-id="6e34c-241">Полный список разделов и свойств, доступных для определения действий, см. в разделе [Конвейеры и действия в фабрике данных Azure](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="6e34c-241">For a full list of sections and properties available for defining activities, see [Creating pipelines](data-factory-create-pipelines.md).</span></span> <span data-ttu-id="6e34c-242">Свойства (такие как имя, описание, входные и выходные таблицы, политики и т. д.) доступны для всех типов действий.</span><span class="sxs-lookup"><span data-stu-id="6e34c-242">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="6e34c-243">С другой стороны, свойства, доступные в разделе **typeProperties** действия, зависят от конкретного типа действия.</span><span class="sxs-lookup"><span data-stu-id="6e34c-243">Properties available in the **typeProperties** section of the activity, on the other hand, vary with each activity type.</span></span> <span data-ttu-id="6e34c-244">Для действия копирования свойства типа различаются в зависимости от типов источников и приемников.</span><span class="sxs-lookup"><span data-stu-id="6e34c-244">For the copy activity, the type properties vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="6e34c-245">Если источник относится к типу **FileSystemSource**, в действии копирования в разделе **typeProperties** доступны указанные ниже свойства.</span><span class="sxs-lookup"><span data-stu-id="6e34c-245">In copy activity, when the source is of type **FileSystemSource**, the following property is available in **typeProperties** section:</span></span>

| <span data-ttu-id="6e34c-246">Свойство</span><span class="sxs-lookup"><span data-stu-id="6e34c-246">Property</span></span> | <span data-ttu-id="6e34c-247">Описание</span><span class="sxs-lookup"><span data-stu-id="6e34c-247">Description</span></span> | <span data-ttu-id="6e34c-248">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="6e34c-248">Allowed values</span></span> | <span data-ttu-id="6e34c-249">Обязательно</span><span class="sxs-lookup"><span data-stu-id="6e34c-249">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6e34c-250">recursive</span><span class="sxs-lookup"><span data-stu-id="6e34c-250">recursive</span></span> |<span data-ttu-id="6e34c-251">Указывает, следует ли читать данные рекурсивно из вложенных папок или только из указанной папки.</span><span class="sxs-lookup"><span data-stu-id="6e34c-251">Indicates whether the data is read recursively from the subfolders, or only from the specified folder.</span></span> |<span data-ttu-id="6e34c-252">True, False (по умолчанию)</span><span class="sxs-lookup"><span data-stu-id="6e34c-252">True, False (default)</span></span> |<span data-ttu-id="6e34c-253">Нет</span><span class="sxs-lookup"><span data-stu-id="6e34c-253">No</span></span> |

## <a name="json-example-copy-data-from-ftp-server-to-azure-blob"></a><span data-ttu-id="6e34c-254">Пример JSON. Копирование данных с FTP-сервера в большой двоичный объект Azure</span><span class="sxs-lookup"><span data-stu-id="6e34c-254">JSON example: Copy data from FTP server to Azure Blob</span></span>
<span data-ttu-id="6e34c-255">В этом примере показано, как скопировать данные с FTP-сервера в хранилище BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="6e34c-255">This sample shows how to copy data from an FTP server to Azure Blob storage.</span></span> <span data-ttu-id="6e34c-256">Однако данные можно напрямую копировать в любые приемники, указанные в статье [Поддерживаемые хранилища данных и форматы](data-factory-data-movement-activities.md#supported-data-stores-and-formats). Для этого применяется действие копирования в фабрике данных.</span><span class="sxs-lookup"><span data-stu-id="6e34c-256">However, data can be copied directly to any of the sinks stated in the [supported data stores and formats](data-factory-data-movement-activities.md#supported-data-stores-and-formats), by using the copy activity in Data Factory.</span></span>  

<span data-ttu-id="6e34c-257">Ниже приведены примеры с определениями JSON, которые можно использовать для создания конвейера с помощью [портала Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) или [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="6e34c-257">The following examples provide sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md):</span></span>

* <span data-ttu-id="6e34c-258">Связанная служба типа [FtpServer](#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="6e34c-258">A linked service of type [FtpServer](#linked-service-properties)</span></span>
* <span data-ttu-id="6e34c-259">Связанная служба типа [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="6e34c-259">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span></span>
* <span data-ttu-id="6e34c-260">Входной [набор данных](data-factory-create-datasets.md) типа [FileShare](#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="6e34c-260">An input [dataset](data-factory-create-datasets.md) of type [FileShare](#dataset-properties)</span></span>
* <span data-ttu-id="6e34c-261">Выходной [набор данных](data-factory-create-datasets.md) типа [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="6e34c-261">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span></span>
* <span data-ttu-id="6e34c-262">[Конвейер](data-factory-create-pipelines.md) с действием копирования, в котором используются [FileSystemSource](#copy-activity-properties) и [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)</span><span class="sxs-lookup"><span data-stu-id="6e34c-262">A [pipeline](data-factory-create-pipelines.md) with copy activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)</span></span>

<span data-ttu-id="6e34c-263">В этом примере данные с FTP-сервера каждый час копируются в большой двоичный объект Azure.</span><span class="sxs-lookup"><span data-stu-id="6e34c-263">The sample copies data from an FTP server to an Azure blob every hour.</span></span> <span data-ttu-id="6e34c-264">Используемые в этих примерах свойства JSON описаны в разделах, следующих за примерами.</span><span class="sxs-lookup"><span data-stu-id="6e34c-264">The JSON properties used in these samples are described in sections following the samples.</span></span>

### <a name="ftp-linked-service"></a><span data-ttu-id="6e34c-265">Связанная служба FTP</span><span class="sxs-lookup"><span data-stu-id="6e34c-265">FTP linked service</span></span>

<span data-ttu-id="6e34c-266">В этом примере используется обычная проверка подлинности на основе имени пользователя и пароля, которые передаются в виде обычного текста.</span><span class="sxs-lookup"><span data-stu-id="6e34c-266">This example uses basic authentication, with the user name and password in plain text.</span></span> <span data-ttu-id="6e34c-267">Кроме того, можно использовать любой из следующих способов:</span><span class="sxs-lookup"><span data-stu-id="6e34c-267">You can also use one of the following ways:</span></span>

* <span data-ttu-id="6e34c-268">анонимная аутентификация;</span><span class="sxs-lookup"><span data-stu-id="6e34c-268">Anonymous authentication</span></span>
* <span data-ttu-id="6e34c-269">обычная аутентификация и шифрование учетных данных;</span><span class="sxs-lookup"><span data-stu-id="6e34c-269">Basic authentication with encrypted credentials</span></span>
* <span data-ttu-id="6e34c-270">FTP через SSL или TLS (FTPS).</span><span class="sxs-lookup"><span data-stu-id="6e34c-270">FTP over SSL/TLS (FTPS)</span></span>

<span data-ttu-id="6e34c-271">Сведения о возможных типах проверки подлинности см. в разделе [Связанная служба FTP](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="6e34c-271">See the [FTP linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

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
### <a name="azure-storage-linked-service"></a><span data-ttu-id="6e34c-272">Связанная служба хранения Azure</span><span class="sxs-lookup"><span data-stu-id="6e34c-272">Azure Storage linked service</span></span>

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
### <a name="ftp-input-dataset"></a><span data-ttu-id="6e34c-273">Входной набор данных FTP</span><span class="sxs-lookup"><span data-stu-id="6e34c-273">FTP input dataset</span></span>

<span data-ttu-id="6e34c-274">Этот набор данных ссылается на папку FTP `mysharedfolder` и файл `test.csv`.</span><span class="sxs-lookup"><span data-stu-id="6e34c-274">This dataset refers to the FTP folder `mysharedfolder` and file `test.csv`.</span></span> <span data-ttu-id="6e34c-275">Конвейер копирует файл в место назначения.</span><span class="sxs-lookup"><span data-stu-id="6e34c-275">The pipeline copies the file to the destination.</span></span>

<span data-ttu-id="6e34c-276">Если параметру **external** присвоить значение **true**, то фабрика данных воспримет этот набор данных как внешний и созданный не в результате какого-либо действия в этой фабрике данных.</span><span class="sxs-lookup"><span data-stu-id="6e34c-276">Setting **external** to **true** informs the Data Factory service that the dataset is external to the data factory, and is not produced by an activity in the data factory.</span></span>

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

### <a name="azure-blob-output-dataset"></a><span data-ttu-id="6e34c-277">Выходной набор данных BLOB-объекта Azure</span><span class="sxs-lookup"><span data-stu-id="6e34c-277">Azure Blob output dataset</span></span>

<span data-ttu-id="6e34c-278">Данные записываются в новый BLOB-объект каждый час (frequency: hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="6e34c-278">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="6e34c-279">Путь к папке BLOB-объекта вычисляется динамически на основе времени начала обрабатываемого среза.</span><span class="sxs-lookup"><span data-stu-id="6e34c-279">The folder path for the blob is dynamically evaluated, based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="6e34c-280">В пути к папке используются год, месяц, день и час времени начала.</span><span class="sxs-lookup"><span data-stu-id="6e34c-280">The folder path uses the year, month, day, and hours parts of the start time.</span></span>

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


### <a name="a-copy-activity-in-a-pipeline-with-file-system-source-and-blob-sink"></a><span data-ttu-id="6e34c-281">Действие копирования в конвейере с файловой системой в качестве источника и BLOB-объектом в качестве приемника</span><span class="sxs-lookup"><span data-stu-id="6e34c-281">A copy activity in a pipeline with file system source and blob sink</span></span>

<span data-ttu-id="6e34c-282">Конвейер содержит действие копирования, которое использует входной и выходной наборы данных и выполняется каждый час.</span><span class="sxs-lookup"><span data-stu-id="6e34c-282">The pipeline contains a copy activity that is configured to use the input and output datasets, and is scheduled to run every hour.</span></span> <span data-ttu-id="6e34c-283">В определении JSON конвейера для типа **источника** установлено значение **FileSystemSource**, а для типа **приемника** — значение **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="6e34c-283">In the pipeline JSON definition, the **source** type is set to **FileSystemSource**, and the **sink** type is set to **BlobSink**.</span></span>

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
> <span data-ttu-id="6e34c-284">Сведения о сопоставлении столбцов в наборе данных, используемом в качестве источника, со столбцами в приемнике см. в [этой статье](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="6e34c-284">To map columns from source dataset to columns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6e34c-285">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6e34c-285">Next steps</span></span>
<span data-ttu-id="6e34c-286">Ознакомьтесь со следующими статьями:</span><span class="sxs-lookup"><span data-stu-id="6e34c-286">See the following articles:</span></span>

* <span data-ttu-id="6e34c-287">Сведения о ключевых факторах, влияющих на производительность перемещения данных (действие копирования) в фабрике данных, и различных способах оптимизации этого процесса см. в [руководстве по настройке производительности действия копирования](data-factory-copy-activity-performance.md).</span><span class="sxs-lookup"><span data-stu-id="6e34c-287">To learn about key factors that impact performance of data movement (copy activity) in Data Factory, and various ways to optimize it, see the [Copy activity performance and tuning guide](data-factory-copy-activity-performance.md).</span></span>

* <span data-ttu-id="6e34c-288">Пошаговые инструкции по созданию конвейера с действием копирования см. в [руководстве по действию копирования](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="6e34c-288">For step-by-step instructions for creating a pipeline with a copy activity, see the [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
