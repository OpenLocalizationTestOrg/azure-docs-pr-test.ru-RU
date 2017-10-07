---
title: "aaaMove данные из SFTP-сервере, с помощью фабрики данных Azure | Документы Microsoft"
description: "Дополнительные сведения о том, как toomove данные из локальной или сервером SFTP облака, с помощью фабрики данных Azure."
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
ms.date: 06/05/2017
ms.author: jingwang
ms.openlocfilehash: b976289e2c1b1899634bb5565b375499077fa554
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-an-sftp-server-using-azure-data-factory"></a><span data-ttu-id="3e472-103">Перемещение данных с SFTP-сервера с использованием фабрики данных Azure</span><span class="sxs-lookup"><span data-stu-id="3e472-103">Move data from an SFTP server using Azure Data Factory</span></span>
<span data-ttu-id="3e472-104">В этой статье рассматриваются как hello toouse действие копирования в данных toomove фабрики данных Azure из tooa сервера на локальные и облачные SFTP поддерживается приемника хранилища данных.</span><span class="sxs-lookup"><span data-stu-id="3e472-104">This article outlines how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises/cloud SFTP server tooa supported sink data store.</span></span> <span data-ttu-id="3e472-105">Эта статья основана на hello [действия перемещения данных](data-factory-data-movement-activities.md) статьи, дан обзор перемещения данных на копии действия и hello список хранилищ данных, поддерживаемые в качестве источников и приемников.</span><span class="sxs-lookup"><span data-stu-id="3e472-105">This article builds on hello [data movement activities](data-factory-data-movement-activities.md) article that presents a general overview of data movement with copy activity and hello list of data stores supported as sources/sinks.</span></span>

<span data-ttu-id="3e472-106">Фабрика данных в настоящее время поддерживает только для перемещения данных из объекта данных tooother сервера SFTP хранятся, но не для перемещения данных из других данных хранит tooan SFTP-сервере.</span><span class="sxs-lookup"><span data-stu-id="3e472-106">Data factory currently supports only moving data from an SFTP server tooother data stores, but not for moving data from other data stores tooan SFTP server.</span></span> <span data-ttu-id="3e472-107">Она поддерживает локальные и облачные SFTP-серверы.</span><span class="sxs-lookup"><span data-stu-id="3e472-107">It supports both on-premises and cloud SFTP servers.</span></span>

> [!NOTE]
> <span data-ttu-id="3e472-108">Действие копирования не удаляет исходный файл hello после назначения успешно скопированного toohello.</span><span class="sxs-lookup"><span data-stu-id="3e472-108">Copy Activity does not delete hello source file after it is successfully copied toohello destination.</span></span> <span data-ttu-id="3e472-109">Если вам требуется toodelete hello исходного файла после успешным копированием, создайте файл hello toodelete пользовательское действие и действие hello используется в конвейере hello.</span><span class="sxs-lookup"><span data-stu-id="3e472-109">If you need toodelete hello source file after a successful copy, create a custom activity toodelete hello file and use hello activity in hello pipeline.</span></span> 

## <a name="supported-scenarios-and-authentication-types"></a><span data-ttu-id="3e472-110">Поддерживаемые сценарии и типы аутентификации</span><span class="sxs-lookup"><span data-stu-id="3e472-110">Supported scenarios and authentication types</span></span>
<span data-ttu-id="3e472-111">Можно использовать эти данные toocopy SFTP соединителя с **облачные SFTP серверов и локальных серверов SFTP**.</span><span class="sxs-lookup"><span data-stu-id="3e472-111">You can use this SFTP connector toocopy data from **both cloud SFTP servers and on-premises SFTP servers**.</span></span> <span data-ttu-id="3e472-112">**Основные** и **параметры SshPublicKey** , поддерживаются типы проверки подлинности при подключении toohello SFTP-сервере.</span><span class="sxs-lookup"><span data-stu-id="3e472-112">**Basic** and **SshPublicKey** authentication types are supported when connecting toohello SFTP server.</span></span>

<span data-ttu-id="3e472-113">При копировании данных из локальной SFTP-сервере, необходимо установить шлюз управления данными в hello в локальной среде и ВМ Azure.</span><span class="sxs-lookup"><span data-stu-id="3e472-113">When copying data from an on-premises SFTP server, you need install a Data Management Gateway in hello on-premises environment/Azure VM.</span></span> <span data-ttu-id="3e472-114">В разделе [шлюз управления данными](data-factory-data-management-gateway.md) сведения о шлюзе hello.</span><span class="sxs-lookup"><span data-stu-id="3e472-114">See [Data Management Gateway](data-factory-data-management-gateway.md) for details on hello gateway.</span></span> <span data-ttu-id="3e472-115">В разделе [перемещение данных между расположениями локальных и облачных](data-factory-move-data-between-onprem-and-cloud.md) статье пошаговые инструкции по настройке шлюза hello и его использования.</span><span class="sxs-lookup"><span data-stu-id="3e472-115">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions on setting up hello gateway and using it.</span></span>

## <a name="getting-started"></a><span data-ttu-id="3e472-116">Приступая к работе</span><span class="sxs-lookup"><span data-stu-id="3e472-116">Getting started</span></span>
<span data-ttu-id="3e472-117">Вы можете создать конвейер с действием копирования, которое перемещает данные с SFTP-сервера с помощью разных инструментов и API-интерфейсов.</span><span class="sxs-lookup"><span data-stu-id="3e472-117">You can create a pipeline with a copy activity that moves data from an SFTP source by using different tools/APIs.</span></span>

- <span data-ttu-id="3e472-118">toocreate простым способом Hello конвейера — toouse hello **мастер копирования**.</span><span class="sxs-lookup"><span data-stu-id="3e472-118">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="3e472-119">В разделе [учебника: создать конвейер, с помощью мастера копирования](data-factory-copy-data-wizard-tutorial.md) краткое Пошаговое руководство по создание с помощью мастера данных копирования hello конвейера.</span><span class="sxs-lookup"><span data-stu-id="3e472-119">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

- <span data-ttu-id="3e472-120">Также можно использовать следующие средства toocreate конвейера hello: **портал Azure**, **Visual Studio**, **Azure PowerShell**, **шаблона диспетчера ресурсов Azure** , **.NET API**, и **API-интерфейса REST**.</span><span class="sxs-lookup"><span data-stu-id="3e472-120">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="3e472-121">В разделе [учебника действия копирования](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) для toocreate пошаговые инструкции конвейера с помощью операции копирования.</span><span class="sxs-lookup"><span data-stu-id="3e472-121">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> <span data-ttu-id="3e472-122">JSON образцы данных toocopy из tooAzure сервера SFTP хранилища больших двоичных объектов, см. в разделе [пример JSON: копирование данных из большого двоичного объекта tooAzure сервера SFTP](#json-example-copy-data-from-sftp-server-to-azure-blob) этой статьи.</span><span class="sxs-lookup"><span data-stu-id="3e472-122">For JSON samples toocopy data from SFTP server tooAzure Blob Storage, see [JSON Example: Copy data from SFTP server tooAzure blob](#json-example-copy-data-from-sftp-server-to-azure-blob) section of this article.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="3e472-123">Свойства связанной службы</span><span class="sxs-lookup"><span data-stu-id="3e472-123">Linked service properties</span></span>
<span data-ttu-id="3e472-124">Hello в следующей таблице приводится описание службы конкретных tooFTP связанные элементы JSON.</span><span class="sxs-lookup"><span data-stu-id="3e472-124">hello following table provides description for JSON elements specific tooFTP linked service.</span></span>

| <span data-ttu-id="3e472-125">Свойство</span><span class="sxs-lookup"><span data-stu-id="3e472-125">Property</span></span> | <span data-ttu-id="3e472-126">Описание</span><span class="sxs-lookup"><span data-stu-id="3e472-126">Description</span></span> | <span data-ttu-id="3e472-127">Обязательно</span><span class="sxs-lookup"><span data-stu-id="3e472-127">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3e472-128">type</span><span class="sxs-lookup"><span data-stu-id="3e472-128">type</span></span> | <span data-ttu-id="3e472-129">свойство типа Hello должно быть задано слишком`Sftp`.</span><span class="sxs-lookup"><span data-stu-id="3e472-129">hello type property must be set too`Sftp`.</span></span> |<span data-ttu-id="3e472-130">Да</span><span class="sxs-lookup"><span data-stu-id="3e472-130">Yes</span></span> |
| <span data-ttu-id="3e472-131">host</span><span class="sxs-lookup"><span data-stu-id="3e472-131">host</span></span> | <span data-ttu-id="3e472-132">Имя или IP-адрес SFTP-сервере hello.</span><span class="sxs-lookup"><span data-stu-id="3e472-132">Name or IP address of hello SFTP server.</span></span> |<span data-ttu-id="3e472-133">Да</span><span class="sxs-lookup"><span data-stu-id="3e472-133">Yes</span></span> |
| <span data-ttu-id="3e472-134">порт</span><span class="sxs-lookup"><span data-stu-id="3e472-134">port</span></span> |<span data-ttu-id="3e472-135">Какие hello SFTP сервера прослушивает порт.</span><span class="sxs-lookup"><span data-stu-id="3e472-135">Port on which hello SFTP server is listening.</span></span> <span data-ttu-id="3e472-136">значение по умолчанию Hello: 21</span><span class="sxs-lookup"><span data-stu-id="3e472-136">hello default value is: 21</span></span> |<span data-ttu-id="3e472-137">Нет</span><span class="sxs-lookup"><span data-stu-id="3e472-137">No</span></span> |
| <span data-ttu-id="3e472-138">authenticationType</span><span class="sxs-lookup"><span data-stu-id="3e472-138">authenticationType</span></span> |<span data-ttu-id="3e472-139">Укажите тип аутентификации.</span><span class="sxs-lookup"><span data-stu-id="3e472-139">Specify authentication type.</span></span> <span data-ttu-id="3e472-140">Допустимые значения: **Basic**, **SshPublicKey**.</span><span class="sxs-lookup"><span data-stu-id="3e472-140">Allowed values: **Basic**, **SshPublicKey**.</span></span> <br><br> <span data-ttu-id="3e472-141">См. слишком[использование обычной проверки подлинности](#using-basic-authentication) и [с помощью открытого ключа проверки подлинности SSH](#using-ssh-public-key-authentication) разделы в дополнительные свойства и примерами JSON, соответственно.</span><span class="sxs-lookup"><span data-stu-id="3e472-141">Refer too[Using basic authentication](#using-basic-authentication) and [Using SSH public key authentication](#using-ssh-public-key-authentication) sections on more properties and JSON samples respectively.</span></span> |<span data-ttu-id="3e472-142">Да</span><span class="sxs-lookup"><span data-stu-id="3e472-142">Yes</span></span> |
| <span data-ttu-id="3e472-143">skipHostKeyValidation</span><span class="sxs-lookup"><span data-stu-id="3e472-143">skipHostKeyValidation</span></span> | <span data-ttu-id="3e472-144">Укажите, размещена ли tooskip ключа проверки.</span><span class="sxs-lookup"><span data-stu-id="3e472-144">Specify whether tooskip host key validation.</span></span> | <span data-ttu-id="3e472-145">Нет.</span><span class="sxs-lookup"><span data-stu-id="3e472-145">No.</span></span> <span data-ttu-id="3e472-146">Здравствуйте, значение по умолчанию: false</span><span class="sxs-lookup"><span data-stu-id="3e472-146">hello default value: false</span></span> |
| <span data-ttu-id="3e472-147">hostKeyFingerprint</span><span class="sxs-lookup"><span data-stu-id="3e472-147">hostKeyFingerprint</span></span> | <span data-ttu-id="3e472-148">Укажите отпечаток пальца hello hello узла ключа.</span><span class="sxs-lookup"><span data-stu-id="3e472-148">Specify hello finger print of hello host key.</span></span> | <span data-ttu-id="3e472-149">Да, если hello `skipHostKeyValidation` имеет значение toofalse.</span><span class="sxs-lookup"><span data-stu-id="3e472-149">Yes if hello `skipHostKeyValidation` is set toofalse.</span></span>  |
| <span data-ttu-id="3e472-150">gatewayName</span><span class="sxs-lookup"><span data-stu-id="3e472-150">gatewayName</span></span> |<span data-ttu-id="3e472-151">Имя tooan tooconnect шлюз управления данными hello локальной SFTP-сервере.</span><span class="sxs-lookup"><span data-stu-id="3e472-151">Name of hello Data Management Gateway tooconnect tooan on-premises SFTP server.</span></span> | <span data-ttu-id="3e472-152">Да, если копирование выполняется с локального SFTP-сервера.</span><span class="sxs-lookup"><span data-stu-id="3e472-152">Yes if copying data from an on-premises SFTP server.</span></span> |
| <span data-ttu-id="3e472-153">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="3e472-153">encryptedCredential</span></span> | <span data-ttu-id="3e472-154">Сервер SFTP hello tooaccess зашифрованных учетных данных.</span><span class="sxs-lookup"><span data-stu-id="3e472-154">Encrypted credential tooaccess hello SFTP server.</span></span> <span data-ttu-id="3e472-155">Формируется автоматически при указании обычной проверки подлинности (имя пользователя + пароль) или параметры SshPublicKey проверки подлинности (имя пользователя + пути закрытого ключа или содержимое) в копирования мастера или hello ClickOnce всплывающее диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="3e472-155">Auto-generated when you specify basic authentication (username + password) or SshPublicKey authentication (username + private key path or content) in copy wizard or hello ClickOnce popup dialog.</span></span> | <span data-ttu-id="3e472-156">Нет.</span><span class="sxs-lookup"><span data-stu-id="3e472-156">No.</span></span> <span data-ttu-id="3e472-157">Применимо, только если копирование выполняется с локального SFTP-сервера.</span><span class="sxs-lookup"><span data-stu-id="3e472-157">Apply only when copying data from an on-premises SFTP server.</span></span> |

### <a name="using-basic-authentication"></a><span data-ttu-id="3e472-158">Использование обычной аутентификации</span><span class="sxs-lookup"><span data-stu-id="3e472-158">Using basic authentication</span></span>

<span data-ttu-id="3e472-159">Задайте обычную проверку подлинности toouse `authenticationType` как `Basic`и укажите следующие свойства, кроме hello SFTP соединителя универсального из них, представленные в последнем разделе hello hello:</span><span class="sxs-lookup"><span data-stu-id="3e472-159">toouse basic authentication, set `authenticationType` as `Basic`, and specify hello following properties besides hello SFTP connector generic ones introduced in hello last section:</span></span>

| <span data-ttu-id="3e472-160">Свойство</span><span class="sxs-lookup"><span data-stu-id="3e472-160">Property</span></span> | <span data-ttu-id="3e472-161">Описание</span><span class="sxs-lookup"><span data-stu-id="3e472-161">Description</span></span> | <span data-ttu-id="3e472-162">Обязательно</span><span class="sxs-lookup"><span data-stu-id="3e472-162">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3e472-163">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="3e472-163">username</span></span> | <span data-ttu-id="3e472-164">Пользователь, обладающий доступом toohello SFTP-сервере.</span><span class="sxs-lookup"><span data-stu-id="3e472-164">User who has access toohello SFTP server.</span></span> |<span data-ttu-id="3e472-165">Да</span><span class="sxs-lookup"><span data-stu-id="3e472-165">Yes</span></span> |
| <span data-ttu-id="3e472-166">пароль</span><span class="sxs-lookup"><span data-stu-id="3e472-166">password</span></span> | <span data-ttu-id="3e472-167">Пароль для пользователя hello (имя пользователя).</span><span class="sxs-lookup"><span data-stu-id="3e472-167">Password for hello user (username).</span></span> | <span data-ttu-id="3e472-168">Да</span><span class="sxs-lookup"><span data-stu-id="3e472-168">Yes</span></span> |

#### <a name="example-basic-authentication"></a><span data-ttu-id="3e472-169">Пример обычной аутентификации</span><span class="sxs-lookup"><span data-stu-id="3e472-169">Example: Basic authentication</span></span>
```json
{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver",
            "port": 22,
            "authenticationType": "Basic",
            "username": "xxx",
            "password": "xxx",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "mygateway"
        }
    }
}
```

#### <a name="example-basic-authentication-with-encrypted-credential"></a><span data-ttu-id="3e472-170">Пример обычной аутентификации с шифрованием учетных данных</span><span class="sxs-lookup"><span data-stu-id="3e472-170">Example: Basic authentication with encrypted credential</span></span>

```JSON
{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver",
            "port": 22,
            "authenticationType": "Basic",
            "username": "xxx",
            "encryptedCredential": "xxxxxxxxxxxxxxxxx",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "mygateway"
        }
      }
}
```

### <a name="using-ssh-public-key-authentication"></a><span data-ttu-id="3e472-171">Использование аутентификации с открытым ключом SSH</span><span class="sxs-lookup"><span data-stu-id="3e472-171">Using SSH public key authentication</span></span>

<span data-ttu-id="3e472-172">задать toouse открытого ключа проверки подлинности SSH, `authenticationType` как `SshPublicKey`и укажите следующие свойства, кроме hello SFTP соединителя универсального из них, представленные в последнем разделе hello hello:</span><span class="sxs-lookup"><span data-stu-id="3e472-172">toouse SSH public key authentication, set `authenticationType` as `SshPublicKey`, and specify hello following properties besides hello SFTP connector generic ones introduced in hello last section:</span></span>

| <span data-ttu-id="3e472-173">Свойство</span><span class="sxs-lookup"><span data-stu-id="3e472-173">Property</span></span> | <span data-ttu-id="3e472-174">Описание</span><span class="sxs-lookup"><span data-stu-id="3e472-174">Description</span></span> | <span data-ttu-id="3e472-175">Обязательно</span><span class="sxs-lookup"><span data-stu-id="3e472-175">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3e472-176">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="3e472-176">username</span></span> |<span data-ttu-id="3e472-177">Пользователь, имеющий доступ toohello SFTP-сервера</span><span class="sxs-lookup"><span data-stu-id="3e472-177">User who has access toohello SFTP server</span></span> |<span data-ttu-id="3e472-178">Да</span><span class="sxs-lookup"><span data-stu-id="3e472-178">Yes</span></span> |
| <span data-ttu-id="3e472-179">privateKeyPath</span><span class="sxs-lookup"><span data-stu-id="3e472-179">privateKeyPath</span></span> | <span data-ttu-id="3e472-180">Укажите абсолютный путь toohello можно получить доступ к файлу закрытого ключа этого шлюза.</span><span class="sxs-lookup"><span data-stu-id="3e472-180">Specify absolute path toohello private key file that gateway can access.</span></span> | <span data-ttu-id="3e472-181">Укажите либо hello `privateKeyPath` или `privateKeyContent`.</span><span class="sxs-lookup"><span data-stu-id="3e472-181">Specify either hello `privateKeyPath` or `privateKeyContent`.</span></span> <br><br> <span data-ttu-id="3e472-182">Применимо, только если копирование выполняется с локального SFTP-сервера.</span><span class="sxs-lookup"><span data-stu-id="3e472-182">Apply only when copying data from an on-premises SFTP server.</span></span> |
| <span data-ttu-id="3e472-183">privateKeyContent</span><span class="sxs-lookup"><span data-stu-id="3e472-183">privateKeyContent</span></span> | <span data-ttu-id="3e472-184">Сериализованная строка hello закрытого ключа содержимого.</span><span class="sxs-lookup"><span data-stu-id="3e472-184">A serialized string of hello private key content.</span></span> <span data-ttu-id="3e472-185">Hello мастер копирования можно считать файл закрытого ключа hello и автоматически извлекать hello закрытого ключа содержимого.</span><span class="sxs-lookup"><span data-stu-id="3e472-185">hello Copy Wizard can read hello private key file and extract hello private key content automatically.</span></span> <span data-ttu-id="3e472-186">При использовании любой другой инструмент и SDK, используйте свойство privateKeyPath hello.</span><span class="sxs-lookup"><span data-stu-id="3e472-186">If you are using any other tool/SDK, use hello privateKeyPath property instead.</span></span> | <span data-ttu-id="3e472-187">Укажите либо hello `privateKeyPath` или `privateKeyContent`.</span><span class="sxs-lookup"><span data-stu-id="3e472-187">Specify either hello `privateKeyPath` or `privateKeyContent`.</span></span> |
| <span data-ttu-id="3e472-188">passPhrase</span><span class="sxs-lookup"><span data-stu-id="3e472-188">passPhrase</span></span> | <span data-ttu-id="3e472-189">Укажите фразу пароль toodecrypt hello hello закрытый ключ, если hello файл ключа защищен парольную фразу.</span><span class="sxs-lookup"><span data-stu-id="3e472-189">Specify hello pass phrase/password toodecrypt hello private key if hello key file is protected by a pass phrase.</span></span> | <span data-ttu-id="3e472-190">Да, если файл закрытого ключа hello защищен парольную фразу.</span><span class="sxs-lookup"><span data-stu-id="3e472-190">Yes if hello private key file is protected by a pass phrase.</span></span> |

> [!NOTE]
> <span data-ttu-id="3e472-191">Соединитель SFTP поддерживает только ключ OpenSSH.</span><span class="sxs-lookup"><span data-stu-id="3e472-191">SFTP connector only support OpenSSH key.</span></span> <span data-ttu-id="3e472-192">Убедитесь, что файл ключа находится в правильном формате hello.</span><span class="sxs-lookup"><span data-stu-id="3e472-192">Make sure your key file is in hello proper format.</span></span> <span data-ttu-id="3e472-193">Можно использовать средство Putty tooconvert из .ppk tooOpenSSH формата.</span><span class="sxs-lookup"><span data-stu-id="3e472-193">You can use Putty tool tooconvert from .ppk tooOpenSSH format.</span></span>

#### <a name="example-sshpublickey-authentication-using-private-key-filepath"></a><span data-ttu-id="3e472-194">Пример аутентификации с закрытым ключом SSH, для которого указан путь к файлу</span><span class="sxs-lookup"><span data-stu-id="3e472-194">Example: SshPublicKey authentication using private key filePath</span></span>

```json
{
    "name": "SftpLinkedServiceWithPrivateKeyPath",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver",
            "port": 22,
            "authenticationType": "SshPublicKey",
            "username": "xxx",
            "privateKeyPath": "D:\\privatekey_openssh",
            "passPhrase": "xxx",
            "skipHostKeyValidation": true,
            "gatewayName": "mygateway"
        }
    }
}
```

#### <a name="example-sshpublickey-authentication-using-private-key-content"></a><span data-ttu-id="3e472-195">Пример аутентификации с закрытым ключом SSH, для которого указано содержимое</span><span class="sxs-lookup"><span data-stu-id="3e472-195">Example: SshPublicKey authentication using private key content</span></span>

```json
{
    "name": "SftpLinkedServiceWithPrivateKeyContent",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver.westus.cloudapp.azure.com",
            "port": 22,
            "authenticationType": "SshPublicKey",
            "username": "xxx",
            "privateKeyContent": "<base64 string of hello private key content>",
            "passPhrase": "xxx",
            "skipHostKeyValidation": true
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="3e472-196">Свойства набора данных</span><span class="sxs-lookup"><span data-stu-id="3e472-196">Dataset properties</span></span>
<span data-ttu-id="3e472-197">Полный список разделов и свойства, доступные для определения наборов данных, см. в разделе hello [Создание наборов данных](data-factory-create-datasets.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="3e472-197">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="3e472-198">Разделы структуры, доступности и политики JSON набора данных одинаковы для всех типов наборов данных.</span><span class="sxs-lookup"><span data-stu-id="3e472-198">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types.</span></span>

<span data-ttu-id="3e472-199">Hello **typeProperties** раздела отличается для каждого типа набора данных.</span><span class="sxs-lookup"><span data-stu-id="3e472-199">hello **typeProperties** section is different for each type of dataset.</span></span> <span data-ttu-id="3e472-200">Он предоставляет сведения о, тип toohello конкретного набора данных.</span><span class="sxs-lookup"><span data-stu-id="3e472-200">It provides information that is specific toohello dataset type.</span></span> <span data-ttu-id="3e472-201">Hello typeProperties статьи для набора данных типа **FileShare** набор данных имеет следующие свойства hello:</span><span class="sxs-lookup"><span data-stu-id="3e472-201">hello typeProperties section for a dataset of type **FileShare** dataset has hello following properties:</span></span>

| <span data-ttu-id="3e472-202">Свойство</span><span class="sxs-lookup"><span data-stu-id="3e472-202">Property</span></span> | <span data-ttu-id="3e472-203">Описание</span><span class="sxs-lookup"><span data-stu-id="3e472-203">Description</span></span> | <span data-ttu-id="3e472-204">Обязательно</span><span class="sxs-lookup"><span data-stu-id="3e472-204">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3e472-205">folderPath</span><span class="sxs-lookup"><span data-stu-id="3e472-205">folderPath</span></span> |<span data-ttu-id="3e472-206">Путь toohello вложенной папкой.</span><span class="sxs-lookup"><span data-stu-id="3e472-206">Sub path toohello folder.</span></span> <span data-ttu-id="3e472-207">Использовать escape-символ "\" для специальных символов в строке приветствия.</span><span class="sxs-lookup"><span data-stu-id="3e472-207">Use escape character ‘ \ ’ for special characters in hello string.</span></span> <span data-ttu-id="3e472-208">Примеры приведены в разделе [Примеры определений связанной службы и набора данных](#sample-linked-service-and-dataset-definitions).</span><span class="sxs-lookup"><span data-stu-id="3e472-208">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="3e472-209">Можно объединять с помощью этого свойства **partitionBy** toohave пути к папке зависимости среза дат начала и окончания.</span><span class="sxs-lookup"><span data-stu-id="3e472-209">You can combine this property with **partitionBy** toohave folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="3e472-210">Да</span><span class="sxs-lookup"><span data-stu-id="3e472-210">Yes</span></span> |
| <span data-ttu-id="3e472-211">fileName</span><span class="sxs-lookup"><span data-stu-id="3e472-211">fileName</span></span> |<span data-ttu-id="3e472-212">Укажите имя файла hello hello в hello **folderPath** Если hello таблицы toorefer tooa конкретный файл в папку hello.</span><span class="sxs-lookup"><span data-stu-id="3e472-212">Specify hello name of hello file in hello **folderPath** if you want hello table toorefer tooa specific file in hello folder.</span></span> <span data-ttu-id="3e472-213">Если не указано значение для этого свойства, таблица hello указывает tooall файлы в папке hello.</span><span class="sxs-lookup"><span data-stu-id="3e472-213">If you do not specify any value for this property, hello table points tooall files in hello folder.</span></span><br/><br/><span data-ttu-id="3e472-214">Если имя файла не указано для выходной набор данных, имя hello hello созданный файл может быть в hello в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="3e472-214">When fileName is not specified for an output dataset, hello name of hello generated file would be in hello following this format:</span></span> <br/><br/><span data-ttu-id="3e472-215">Data.<Guid>.txt (например, Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="3e472-215">Data.<Guid>.txt (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="3e472-216">Нет</span><span class="sxs-lookup"><span data-stu-id="3e472-216">No</span></span> |
| <span data-ttu-id="3e472-217">fileFilter</span><span class="sxs-lookup"><span data-stu-id="3e472-217">fileFilter</span></span> |<span data-ttu-id="3e472-218">Укажите toobe фильтра используется tooselect подмножества файлов в hello folderPath, а не всех файлов.</span><span class="sxs-lookup"><span data-stu-id="3e472-218">Specify a filter toobe used tooselect a subset of files in hello folderPath rather than all files.</span></span><br/><br/><span data-ttu-id="3e472-219">Допустимые значения: `*` (несколько знаков) и `?` (один знак).</span><span class="sxs-lookup"><span data-stu-id="3e472-219">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="3e472-220">Пример 1: `"fileFilter": "*.log"`</span><span class="sxs-lookup"><span data-stu-id="3e472-220">Examples 1: `"fileFilter": "*.log"`</span></span><br/><span data-ttu-id="3e472-221">Пример 2: `"fileFilter": 2014-1-?.txt"`</span><span class="sxs-lookup"><span data-stu-id="3e472-221">Example 2: `"fileFilter": 2014-1-?.txt"`</span></span><br/><br/> <span data-ttu-id="3e472-222">Свойство fileFilter применяется к входному набору данных FileShare.</span><span class="sxs-lookup"><span data-stu-id="3e472-222">fileFilter is applicable for an input FileShare dataset.</span></span> <span data-ttu-id="3e472-223">HDFS не поддерживает это свойство.</span><span class="sxs-lookup"><span data-stu-id="3e472-223">This property is not supported with HDFS.</span></span> |<span data-ttu-id="3e472-224">Нет</span><span class="sxs-lookup"><span data-stu-id="3e472-224">No</span></span> |
| <span data-ttu-id="3e472-225">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="3e472-225">partitionedBy</span></span> |<span data-ttu-id="3e472-226">partitionedBy можно использовать toospecify динамического folderPath, имя файла для временного ряда данных.</span><span class="sxs-lookup"><span data-stu-id="3e472-226">partitionedBy can be used toospecify a dynamic folderPath, filename for time series data.</span></span> <span data-ttu-id="3e472-227">Например, путь к папке folderPath каждый час будет другим.</span><span class="sxs-lookup"><span data-stu-id="3e472-227">For example, folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="3e472-228">Нет</span><span class="sxs-lookup"><span data-stu-id="3e472-228">No</span></span> |
| <span data-ttu-id="3e472-229">свойства</span><span class="sxs-lookup"><span data-stu-id="3e472-229">format</span></span> | <span data-ttu-id="3e472-230">поддерживаются следующие типы формата Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="3e472-230">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="3e472-231">Набор hello **тип** свойства в формате tooone из следующих значений.</span><span class="sxs-lookup"><span data-stu-id="3e472-231">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="3e472-232">Дополнительные сведения см. в разделах о [текстовом формате](data-factory-supported-file-and-compression-formats.md#text-format), [формате Json](data-factory-supported-file-and-compression-formats.md#json-format), [формате Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [формате Orc](data-factory-supported-file-and-compression-formats.md#orc-format) и [ формате Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="3e472-232">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="3e472-233">Если требуется слишком**скопируйте файлы как-является** между файловых хранилищ (двоичный копия), пропустите раздел формат hello в оба определения набора входных и выходных данных.</span><span class="sxs-lookup"><span data-stu-id="3e472-233">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="3e472-234">Нет</span><span class="sxs-lookup"><span data-stu-id="3e472-234">No</span></span> |
| <span data-ttu-id="3e472-235">compression</span><span class="sxs-lookup"><span data-stu-id="3e472-235">compression</span></span> | <span data-ttu-id="3e472-236">Укажите тип hello и уровень сжатия данных hello.</span><span class="sxs-lookup"><span data-stu-id="3e472-236">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="3e472-237">Поддерживаемые типы: **GZip**, **Deflate**, **BZip2** и **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="3e472-237">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="3e472-238">Поддерживаемые уровни: **Optimal** и **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="3e472-238">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="3e472-239">См. дополнительные сведения о [форматах файлов и сжатия данных в фабрике данных Azure](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="3e472-239">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="3e472-240">Нет</span><span class="sxs-lookup"><span data-stu-id="3e472-240">No</span></span> |
| <span data-ttu-id="3e472-241">useBinaryTransfer</span><span class="sxs-lookup"><span data-stu-id="3e472-241">useBinaryTransfer</span></span> |<span data-ttu-id="3e472-242">Укажите, использовать ли режим передачи в двоичном формате.</span><span class="sxs-lookup"><span data-stu-id="3e472-242">Specify whether use Binary transfer mode.</span></span> <span data-ttu-id="3e472-243">Значение true, если использовать двоичный режим, и false, если ASCII.</span><span class="sxs-lookup"><span data-stu-id="3e472-243">True for binary mode and false ASCII.</span></span> <span data-ttu-id="3e472-244">Значение по умолчанию: True.</span><span class="sxs-lookup"><span data-stu-id="3e472-244">Default value: True.</span></span> <span data-ttu-id="3e472-245">Это свойство можно использовать, только когда тип связанной службы является FTP-сервер.</span><span class="sxs-lookup"><span data-stu-id="3e472-245">This property can only be used when associated linked service type is of type: FtpServer.</span></span> |<span data-ttu-id="3e472-246">Нет</span><span class="sxs-lookup"><span data-stu-id="3e472-246">No</span></span> |

> [!NOTE]
> <span data-ttu-id="3e472-247">Свойства filename и fileFilter нельзя использовать одновременно.</span><span class="sxs-lookup"><span data-stu-id="3e472-247">filename and fileFilter cannot be used simultaneously.</span></span>

### <a name="using-partionedby-property"></a><span data-ttu-id="3e472-248">Использование свойства partionedBy</span><span class="sxs-lookup"><span data-stu-id="3e472-248">Using partionedBy property</span></span>
<span data-ttu-id="3e472-249">Как упоминалось в предыдущем разделе hello, можно указать динамический folderPath, имя файла для временного ряда данных с partitionedBy.</span><span class="sxs-lookup"><span data-stu-id="3e472-249">As mentioned in hello previous section, you can specify a dynamic folderPath, filename for time series data with partitionedBy.</span></span> <span data-ttu-id="3e472-250">Это можно сделать с макросы фабрики данных hello и hello системной переменной SliceStart, SliceEnd, указывающие hello логических период для среза данных.</span><span class="sxs-lookup"><span data-stu-id="3e472-250">You can do so with hello Data Factory macros and hello system variable SliceStart, SliceEnd that indicate hello logical time period for a given data slice.</span></span>

<span data-ttu-id="3e472-251">toolearn о наборы данных для ряда времени, планирования и срезов, в разделе [Создание наборов данных](data-factory-create-datasets.md), [планирования и исполнение](data-factory-scheduling-and-execution.md), и [создания конвейеров](data-factory-create-pipelines.md) статей.</span><span class="sxs-lookup"><span data-stu-id="3e472-251">toolearn about time series datasets, scheduling, and slices, See [Creating Datasets](data-factory-create-datasets.md), [Scheduling & Execution](data-factory-scheduling-and-execution.md), and [Creating Pipelines](data-factory-create-pipelines.md) articles.</span></span>

#### <a name="sample-1"></a><span data-ttu-id="3e472-252">Пример 1</span><span class="sxs-lookup"><span data-stu-id="3e472-252">Sample 1:</span></span>

```json
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```
<span data-ttu-id="3e472-253">В этом примере {Slice} заменяется hello значение системной переменной фабрики данных SliceStart в формате hello (ГГГГММДДЧЧ) указан.</span><span class="sxs-lookup"><span data-stu-id="3e472-253">In this example {Slice} is replaced with hello value of Data Factory system variable SliceStart in hello format (YYYYMMDDHH) specified.</span></span> <span data-ttu-id="3e472-254">Hello SliceStart ссылается toostart время hello среза.</span><span class="sxs-lookup"><span data-stu-id="3e472-254">hello SliceStart refers toostart time of hello slice.</span></span> <span data-ttu-id="3e472-255">Hello folderPath отличается для каждого среза.</span><span class="sxs-lookup"><span data-stu-id="3e472-255">hello folderPath is different for each slice.</span></span> <span data-ttu-id="3e472-256">Например, wikidatagateway/wikisampledataout/2014100103 или wikidatagateway/wikisampledataout/2014100104.</span><span class="sxs-lookup"><span data-stu-id="3e472-256">Example: wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104.</span></span>

#### <a name="sample-2"></a><span data-ttu-id="3e472-257">Пример 2</span><span class="sxs-lookup"><span data-stu-id="3e472-257">Sample 2:</span></span>

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
<span data-ttu-id="3e472-258">В этом примере год, месяц, день и время SliceStart извлекаются в отдельные переменные, используемые в свойствах folderPath и fileName.</span><span class="sxs-lookup"><span data-stu-id="3e472-258">In this example, year, month, day, and time of SliceStart are extracted into separate variables that are used by folderPath and fileName properties.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="3e472-259">Свойства действия копирования</span><span class="sxs-lookup"><span data-stu-id="3e472-259">Copy activity properties</span></span>
<span data-ttu-id="3e472-260">Полный список разделов и свойства, доступные для определения действий см. в разделе hello [Создание конвейеры](data-factory-create-pipelines.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="3e472-260">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="3e472-261">Свойства (такие как имя, описание, входные и выходные таблицы, политики и т. д.) доступны для всех типов действий.</span><span class="sxs-lookup"><span data-stu-id="3e472-261">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="3e472-262">В то время как hello свойства раздела typeProperties hello hello действия зависят от типа каждого действия.</span><span class="sxs-lookup"><span data-stu-id="3e472-262">Whereas, hello properties available in hello typeProperties section of hello activity vary with each activity type.</span></span> <span data-ttu-id="3e472-263">Для действия копирования hello тип свойства зависят от типов hello источники и приемники.</span><span class="sxs-lookup"><span data-stu-id="3e472-263">For Copy activity, hello type properties vary depending on hello types of sources and sinks.</span></span>

[!INCLUDE [data-factory-file-system-source](../../includes/data-factory-file-system-source.md)]

## <a name="supported-file-and-compression-formats"></a><span data-ttu-id="3e472-264">Поддерживаемые форматы файлов и сжатия</span><span class="sxs-lookup"><span data-stu-id="3e472-264">Supported file and compression formats</span></span>
<span data-ttu-id="3e472-265">Дополнительные сведения см. в статье [Форматы файлов и сжатия данных, поддерживаемые фабрикой данных Azure](data-factory-supported-file-and-compression-formats.md).</span><span class="sxs-lookup"><span data-stu-id="3e472-265">See [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article on details.</span></span>

## <a name="json-example-copy-data-from-sftp-server-tooazure-blob"></a><span data-ttu-id="3e472-266">Пример JSON: Копирование данных из большого двоичного объекта tooAzure сервера SFTP</span><span class="sxs-lookup"><span data-stu-id="3e472-266">JSON Example: Copy data from SFTP server tooAzure blob</span></span>
<span data-ttu-id="3e472-267">Hello ниже приведен пример определения JSON можно использовать toocreate конвейера с помощью [портал Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) или [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) или [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="3e472-267">hello following example provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="3e472-268">Они показывают, как toocopy из SFTP источника tooAzure хранилища больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="3e472-268">They show how toocopy data from SFTP source tooAzure Blob Storage.</span></span> <span data-ttu-id="3e472-269">Тем не менее, данные можно скопировать **непосредственно** из любых источников tooany приемников hello указано [здесь](data-factory-data-movement-activities.md#supported-data-stores-and-formats) с помощью hello действие копирования в фабрике данных Azure.</span><span class="sxs-lookup"><span data-stu-id="3e472-269">However, data can be copied **directly** from any of sources tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3e472-270">Этот пример содержит фрагменты кода JSON.</span><span class="sxs-lookup"><span data-stu-id="3e472-270">This sample provides JSON snippets.</span></span> <span data-ttu-id="3e472-271">Он не включает пошаговые инструкции по созданию фабрики данных hello.</span><span class="sxs-lookup"><span data-stu-id="3e472-271">It does not include step-by-step instructions for creating hello data factory.</span></span> <span data-ttu-id="3e472-272">Эти инструкции приведены в статье [Перемещение данных между локальными источниками и облаком с помощью шлюза управления данными](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="3e472-272">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="3e472-273">Образец Hello имеет hello, следуя сущностей фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="3e472-273">hello sample has hello following data factory entities:</span></span>

* <span data-ttu-id="3e472-274">Связанная служба типа [sftp](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="3e472-274">A linked service of type [sftp](#linked-service-properties).</span></span>
* <span data-ttu-id="3e472-275">Связанная служба типа [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="3e472-275">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="3e472-276">Входной [набор данных](data-factory-create-datasets.md) типа [FileShare](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="3e472-276">An input [dataset](data-factory-create-datasets.md) of type [FileShare](#dataset-properties).</span></span>
* <span data-ttu-id="3e472-277">Выходной [набор данных](data-factory-create-datasets.md) типа [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="3e472-277">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="3e472-278">[Конвейер](data-factory-create-pipelines.md) с действием копирования, в котором используются [FileSystemSource](#copy-activity-properties) и [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="3e472-278">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="3e472-279">Образец Hello копирует данные из tooan сервера SFTP BLOB-объектов Azure каждый час.</span><span class="sxs-lookup"><span data-stu-id="3e472-279">hello sample copies data from an SFTP server tooan Azure blob every hour.</span></span> <span data-ttu-id="3e472-280">свойства Hello JSON, используемые в этих примерах описаны в разделах, следующие примеры hello.</span><span class="sxs-lookup"><span data-stu-id="3e472-280">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="3e472-281">**Связанная служба SFTP**</span><span class="sxs-lookup"><span data-stu-id="3e472-281">**SFTP linked service**</span></span>

<span data-ttu-id="3e472-282">Этот пример использует обычную проверку подлинности hello с именем пользователя и пароль в виде обычного текста.</span><span class="sxs-lookup"><span data-stu-id="3e472-282">This example uses hello basic authentication with user name and password in plain text.</span></span> <span data-ttu-id="3e472-283">Также можно использовать один из следующих способов hello:</span><span class="sxs-lookup"><span data-stu-id="3e472-283">You can also use one of hello following ways:</span></span>

* <span data-ttu-id="3e472-284">обычная аутентификация и шифрование учетных данных;</span><span class="sxs-lookup"><span data-stu-id="3e472-284">Basic authentication with encrypted credentials</span></span>
* <span data-ttu-id="3e472-285">Аутентификация с открытым ключом SSH</span><span class="sxs-lookup"><span data-stu-id="3e472-285">SSH public key authentication</span></span>

<span data-ttu-id="3e472-286">Сведения о возможных типах аутентификации см. в разделе [Связанная служба FTP](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="3e472-286">See [FTP linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

```JSON

{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver",
            "port": 22,
            "authenticationType": "Basic",
            "username": "myuser",
            "password": "mypassword",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "mygateway"
        }
    }
}
```
<span data-ttu-id="3e472-287">**Связанная служба хранения Azure**</span><span class="sxs-lookup"><span data-stu-id="3e472-287">**Azure Storage linked service**</span></span>

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
<span data-ttu-id="3e472-288">**Входной набор данных SFTP**</span><span class="sxs-lookup"><span data-stu-id="3e472-288">**SFTP input dataset**</span></span>

<span data-ttu-id="3e472-289">Этот набор данных ссылается папки SFTP toohello `mysharedfolder` и файл `test.csv`.</span><span class="sxs-lookup"><span data-stu-id="3e472-289">This dataset refers toohello SFTP folder `mysharedfolder` and file `test.csv`.</span></span> <span data-ttu-id="3e472-290">конвейер Hello копирует hello файл toohello назначения.</span><span class="sxs-lookup"><span data-stu-id="3e472-290">hello pipeline copies hello file toohello destination.</span></span>

<span data-ttu-id="3e472-291">Параметр «external»: «true» уведомляет службу hello фабрики данных, что набор данных hello фабрики toohello внешних данных и не был создан из действия в фабрике данных hello.</span><span class="sxs-lookup"><span data-stu-id="3e472-291">Setting "external": "true" informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```JSON
{
  "name": "SFTPFileInput",
  "properties": {
    "type": "FileShare",
    "linkedServiceName": "SftpLinkedService",
    "typeProperties": {
      "folderPath": "mysharedfolder",
      "fileName": "test.csv"
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

<span data-ttu-id="3e472-292">**Выходной набор данных BLOB-объекта Azure**</span><span class="sxs-lookup"><span data-stu-id="3e472-292">**Azure Blob output dataset**</span></span>

<span data-ttu-id="3e472-293">Записывается новый большой двоичный объект tooa каждый час (частота: час, интервал: 1).</span><span class="sxs-lookup"><span data-stu-id="3e472-293">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="3e472-294">путь к папке Hello для большого двоичного объекта hello динамически вычисляется на основе времени начала hello hello среза, который обрабатывается.</span><span class="sxs-lookup"><span data-stu-id="3e472-294">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="3e472-295">путь к папке Hello использует года, месяца, дня и часа части времени начала hello.</span><span class="sxs-lookup"><span data-stu-id="3e472-295">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```JSON
{
    "name": "AzureBlobOutput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/sftp/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

<span data-ttu-id="3e472-296">**Конвейер с действием копирования**</span><span class="sxs-lookup"><span data-stu-id="3e472-296">**Pipeline with Copy activity**</span></span>

<span data-ttu-id="3e472-297">Hello конвейера содержит операции копирования, настроенные toouse hello входные и выходные наборы данных и является запланированных toorun каждый час.</span><span class="sxs-lookup"><span data-stu-id="3e472-297">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="3e472-298">В определении JSON конвейера hello, hello **источника** тип установлен слишком**FileSystemSource** и **приемник** тип установлен слишком**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="3e472-298">In hello pipeline JSON definition, hello **source** type is set too**FileSystemSource** and **sink** type is set too**BlobSink**.</span></span>

```JSON
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "SFTPToBlobCopy",
            "inputs": [{
                "name": "SFTPFileInput"
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
        "start": "2017-02-20T18:00:00Z",
        "end": "2017-02-20T19:00:00Z"
    }
}
```

## <a name="performance-and-tuning"></a><span data-ttu-id="3e472-299">Производительность и настройка</span><span class="sxs-lookup"><span data-stu-id="3e472-299">Performance and Tuning</span></span>
<span data-ttu-id="3e472-300">В разделе [производительности для действия копирования & руководство по настройке](data-factory-copy-activity-performance.md) toolearn о ключе факторы, оказывают влияние на производительность перемещения данных (действие копирования) в фабрике данных Azure и различных способов toooptimize его.</span><span class="sxs-lookup"><span data-stu-id="3e472-300">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3e472-301">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3e472-301">Next Steps</span></span>
<span data-ttu-id="3e472-302">См. следующие статьи hello.</span><span class="sxs-lookup"><span data-stu-id="3e472-302">See hello following articles:</span></span>

* <span data-ttu-id="3e472-303">[руководстве по действию копирования](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) .</span><span class="sxs-lookup"><span data-stu-id="3e472-303">[Copy Activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions for creating a pipeline with a Copy Activity.</span></span>
