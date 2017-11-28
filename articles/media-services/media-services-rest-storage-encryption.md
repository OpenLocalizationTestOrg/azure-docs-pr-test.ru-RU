---
title: "aaaEncrypting содержимого с помощью шифрования хранилища с помощью API-интерфейса REST AMS"
description: "Узнайте, как tooencrypt содержимого с помощью шифрования хранилища с помощью API REST AMS."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: a0a79f3d-76a1-4994-9202-59b91a2230e0
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: d5f8cb8dd1dcded76c9fededccc772d8102ccbad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="encrypting-your-content-with-storage-encryption"></a><span data-ttu-id="6df3c-103">Шифрование содержимого с помощью шифрования хранилища</span><span class="sxs-lookup"><span data-stu-id="6df3c-103">Encrypting your content with storage encryption</span></span>

<span data-ttu-id="6df3c-104">Настоятельно рекомендуется tooencrypt-битное шифрование содержимого локально с помощью AES-256, а затем передать его tooAzure хранилища, где он будет храниться в зашифрованном виде.</span><span class="sxs-lookup"><span data-stu-id="6df3c-104">It is highly recommended tooencrypt your content locally using AES-256 bit encryption and then upload it tooAzure Storage where it will be stored encrypted at rest.</span></span>

<span data-ttu-id="6df3c-105">В этой статье приводится обзор AMS шифрование хранилища и показано, как хранилище hello tooupload зашифрованного содержимого:</span><span class="sxs-lookup"><span data-stu-id="6df3c-105">This article gives an overview of AMS storage encryption and shows you how tooupload hello storage encrypted content:</span></span>

* <span data-ttu-id="6df3c-106">Создайте ключ содержимого.</span><span class="sxs-lookup"><span data-stu-id="6df3c-106">Create a content key.</span></span>
* <span data-ttu-id="6df3c-107">Создайте ресурс.</span><span class="sxs-lookup"><span data-stu-id="6df3c-107">Create an Asset.</span></span> <span data-ttu-id="6df3c-108">Установка hello AssetCreationOption tooStorageEncryption при создании hello активов.</span><span class="sxs-lookup"><span data-stu-id="6df3c-108">Set hello AssetCreationOption tooStorageEncryption when creating hello Asset.</span></span>
  
     <span data-ttu-id="6df3c-109">Зашифрованные активы имеют toobe, связанные с ключами содержимого.</span><span class="sxs-lookup"><span data-stu-id="6df3c-109">Encrypted assets have toobe associated with content keys.</span></span>
* <span data-ttu-id="6df3c-110">Ссылка hello содержимого ключа toohello активов.</span><span class="sxs-lookup"><span data-stu-id="6df3c-110">Link hello content key toohello asset.</span></span>  
* <span data-ttu-id="6df3c-111">Задайте параметры для сущностей AssetFile hello, связанные с шифрованием hello.</span><span class="sxs-lookup"><span data-stu-id="6df3c-111">Set hello encryption related parameters on hello AssetFile entities.</span></span>

## <a name="considerations"></a><span data-ttu-id="6df3c-112">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="6df3c-112">Considerations</span></span> 

<span data-ttu-id="6df3c-113">Если вы хотите toodeliver зашифрованного актива хранилища, необходимо настроить политику доставки актива hello.</span><span class="sxs-lookup"><span data-stu-id="6df3c-113">If you want toodeliver a storage encrypted asset, you must configure hello asset’s delivery policy.</span></span> <span data-ttu-id="6df3c-114">Перед потоковой актива hello, потоковая передача контента с помощью hello шифрование хранилища сервера удаляет hello и потоки указан политики доставки.</span><span class="sxs-lookup"><span data-stu-id="6df3c-114">Before your asset can be streamed, hello streaming server removes hello storage encryption and streams your content using hello specified delivery policy.</span></span> <span data-ttu-id="6df3c-115">Дополнительные сведения см. в статье [Настройка политик доставки ресурсов](media-services-rest-configure-asset-delivery-policy.md).</span><span class="sxs-lookup"><span data-stu-id="6df3c-115">For more information, see [Configuring Asset Delivery Policies](media-services-rest-configure-asset-delivery-policy.md).</span></span>

<span data-ttu-id="6df3c-116">При доступе к сущностям в службах мультимедиа необходимо задать определенные поля и значения заголовков в HTTP-запросах.</span><span class="sxs-lookup"><span data-stu-id="6df3c-116">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="6df3c-117">Дополнительную информацию см. в статье [Обзор интерфейса REST API служб мультимедиа](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="6df3c-117">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span> 

## <a name="connect-toomedia-services"></a><span data-ttu-id="6df3c-118">Подключение служб tooMedia</span><span class="sxs-lookup"><span data-stu-id="6df3c-118">Connect tooMedia Services</span></span>

<span data-ttu-id="6df3c-119">Сведения о tooconnect toohello AMS API, в статье [hello доступа к API служб мультимедиа Azure с проверкой подлинности Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="6df3c-119">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="6df3c-120">После успешного подключения toohttps://media.windows.net, будет получено перенаправление 301 указывающее другой URI служб Media Services.</span><span class="sxs-lookup"><span data-stu-id="6df3c-120">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="6df3c-121">Необходимо внести toohello последующих вызовов новый URI.</span><span class="sxs-lookup"><span data-stu-id="6df3c-121">You must make subsequent calls toohello new URI.</span></span>

## <a name="storage-encryption-overview"></a><span data-ttu-id="6df3c-122">Общие сведения о шифровании хранилища</span><span class="sxs-lookup"><span data-stu-id="6df3c-122">Storage encryption overview</span></span>
<span data-ttu-id="6df3c-123">применяет шифрование хранилища Hello AMS **AES CTR** режим шифрования toohello весь файл.</span><span class="sxs-lookup"><span data-stu-id="6df3c-123">hello AMS storage encryption applies **AES-CTR** mode encryption toohello entire file.</span></span>  <span data-ttu-id="6df3c-124">AES-CTR — это блочный шифр, который может шифровать данные произвольной длины и не требует заполнения.</span><span class="sxs-lookup"><span data-stu-id="6df3c-124">AES-CTR mode is a block cipher that can encrypt arbitrary length data without need for padding.</span></span> <span data-ttu-id="6df3c-125">Он работает путем шифрования блок счетчика с hello алгоритм AES, а затем оператор XOR hello выходные данные AES с tooencrypt данных hello или расшифровать.</span><span class="sxs-lookup"><span data-stu-id="6df3c-125">It operates by encrypting a counter block with hello AES algorithm and then XOR-ing hello output of AES with hello data tooencrypt or decrypt.</span></span>  <span data-ttu-id="6df3c-126">Счетчик блока Hello, используемой создается путем копирования hello значение hello InitializationVector toobytes 0 too7 значения счетчика hello и too15 8 байтов значения счетчика hello установлены toozero.</span><span class="sxs-lookup"><span data-stu-id="6df3c-126">hello counter block used is constructed by copying hello value of hello InitializationVector toobytes 0 too7 of hello counter value and bytes 8 too15 of hello counter value are set toozero.</span></span> <span data-ttu-id="6df3c-127">16-разрядный счетчик hello блока, too15 8 байт (т. е. наименее значащие байты hello) используются как простой 64-разрядное целое число без знака, увеличивается на единицу для каждого блока данных, обрабатываемая и хранится в сетевой порядок байтов.</span><span class="sxs-lookup"><span data-stu-id="6df3c-127">Of hello 16 byte counter block, bytes 8 too15 (i.e. hello least significant bytes) are used as a simple 64 bit unsigned integer that is incremented by one for each subsequent block of data processed and is kept in network byte order.</span></span> <span data-ttu-id="6df3c-128">Обратите внимание, что если это целое число достигает hello максимальное значение (0xFFFFFFFFFFFFFFFF) его увеличением сбрасывает hello блок счетчика toozero (8 байт too15) без влияния на другие hello 64 бита hello счетчика (т. е. too7 0 байт).</span><span class="sxs-lookup"><span data-stu-id="6df3c-128">Note that if this integer reaches hello maximum value (0xFFFFFFFFFFFFFFFF) then incrementing it resets hello block counter toozero (bytes 8 too15) without affecting hello other 64 bits of hello counter (i.e. bytes 0 too7).</span></span>   <span data-ttu-id="6df3c-129">В порядке toomaintain hello безопасность режим шифрования AES CTR hello hello InitializationVector значение для данного идентификатора ключа для каждого ключа контента должен быть уникальным для каждого файла и файлы должны быть меньше 2 ^ 64 блоков в длину.</span><span class="sxs-lookup"><span data-stu-id="6df3c-129">In order toomaintain hello security of hello AES-CTR mode encryption, hello InitializationVector value for a given Key Identifier for each content key shall be unique for each file and files shall be less than 2^64 blocks in length.</span></span>  <span data-ttu-id="6df3c-130">Это tooensure, значение счетчика не может повторно использовать с данным ключом.</span><span class="sxs-lookup"><span data-stu-id="6df3c-130">This is tooensure that a counter value is never reused with a given key.</span></span> <span data-ttu-id="6df3c-131">Дополнительные сведения о режиме CTR hello см. в разделе [этой странице вики-сайте](https://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#CTR) (статья wiki hello использует hello термин «Nonce» вместо «InitializationVector»).</span><span class="sxs-lookup"><span data-stu-id="6df3c-131">For more information about hello CTR mode, see [this wiki page](https://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#CTR) (hello wiki article uses hello term "Nonce" instead of "InitializationVector").</span></span>

<span data-ttu-id="6df3c-132">Используйте **шифрование хранилища** tooencrypt-битное шифрование незащищенного содержимого локально с помощью AES-256, а затем передать его tooAzure хранилища, где она хранится в зашифрованном виде.</span><span class="sxs-lookup"><span data-stu-id="6df3c-132">Use **Storage Encryption** tooencrypt your clear content locally using AES-256 bit encryption and then upload it tooAzure Storage where it is stored encrypted at rest.</span></span> <span data-ttu-id="6df3c-133">Активы, защищенные с помощью шифрования хранилища, автоматически дешифруются и помещаются в предыдущих tooencoding зашифрованный файл системы и при необходимости повторно зашифрован предыдущих toouploading возвращены в виде нового выходного актива.</span><span class="sxs-lookup"><span data-stu-id="6df3c-133">Assets protected with storage encryption are automatically unencrypted and placed in an encrypted file system prior tooencoding, and optionally re-encrypted prior toouploading back as a new output asset.</span></span> <span data-ttu-id="6df3c-134">Hello основным случаем использования шифрования хранилища удобно, если нужно toosecure rest вашей высококачественных входных файлов мультимедиа с помощью строгого шифрования на диске.</span><span class="sxs-lookup"><span data-stu-id="6df3c-134">hello primary use case for storage encryption is when you want toosecure your high quality input media files with strong encryption at rest on disk.</span></span>

<span data-ttu-id="6df3c-135">В порядке toodeliver зашифрованного актива хранилища необходимо настроить политику доставки актива hello, службы мультимедиа получили информацию о способе toodeliver контента.</span><span class="sxs-lookup"><span data-stu-id="6df3c-135">In order toodeliver a storage encrypted asset, you must configure hello asset’s delivery policy so Media Services knows how you want toodeliver your content.</span></span> <span data-ttu-id="6df3c-136">Перед потоковой актива hello, потоковая передача контента с помощью hello шифрование хранилища сервера удаляет hello и потоки указан политики доставки (например, AES, общее шифрование или шифрование).</span><span class="sxs-lookup"><span data-stu-id="6df3c-136">Before your asset can be streamed, hello streaming server removes hello storage encryption and streams your content using hello specified delivery policy (for example, AES, common encryption, or no encryption).</span></span>

## <a name="create-contentkeys-used-for-encryption"></a><span data-ttu-id="6df3c-137">Создание сущности ContentKeys, используемой для шифрования</span><span class="sxs-lookup"><span data-stu-id="6df3c-137">Create ContentKeys used for encryption</span></span>
<span data-ttu-id="6df3c-138">Зашифрованные активы имеют toobe, связанное с ключом шифрования хранилища.</span><span class="sxs-lookup"><span data-stu-id="6df3c-138">Encrypted assets have toobe associated with Storage Encryption key.</span></span> <span data-ttu-id="6df3c-139">Необходимо создать ключа toobe с содержимым hello используется для шифрования перед созданием hello файлов активов.</span><span class="sxs-lookup"><span data-stu-id="6df3c-139">You must create hello content key toobe used for encryption before creating hello asset files.</span></span> <span data-ttu-id="6df3c-140">В этом разделе описываются как toocreate ключа содержимого.</span><span class="sxs-lookup"><span data-stu-id="6df3c-140">This section describes how toocreate a content key.</span></span>

<span data-ttu-id="6df3c-141">Hello ниже приведены общие шаги для создания ключей контента будет связана с основные средства toobe зашифрованы.</span><span class="sxs-lookup"><span data-stu-id="6df3c-141">hello following are general steps for generating content keys that you will associate with assets that you want toobe encrypted.</span></span> 

1. <span data-ttu-id="6df3c-142">Для шифрования хранилища случайным образом формируется 32-разрядный ключ AES.</span><span class="sxs-lookup"><span data-stu-id="6df3c-142">For storage encryption, randomly generate a 32-byte AES key.</span></span> 
   
    <span data-ttu-id="6df3c-143">Это будет hello ключ содержимого для ресурса, что означает все файлы, связанные с этим ресурсом будет необходимо toouse hello один ключ содержимого во время расшифровки.</span><span class="sxs-lookup"><span data-stu-id="6df3c-143">This will be hello content key for your asset, which means all files associated with that asset will need toouse hello same content key during decryption.</span></span> 
2. <span data-ttu-id="6df3c-144">Вызовите hello [GetProtectionKeyId](https://docs.microsoft.com/rest/api/media/operations/rest-api-functions#getprotectionkeyid) и [GetProtectionKey](https://msdn.microsoft.com/library/azure/jj683097.aspx#getprotectionkey) tooget методы hello правильный сертификат X.509, который должен быть используется tooencrypt ключа содержимого.</span><span class="sxs-lookup"><span data-stu-id="6df3c-144">Call hello [GetProtectionKeyId](https://docs.microsoft.com/rest/api/media/operations/rest-api-functions#getprotectionkeyid) and [GetProtectionKey](https://msdn.microsoft.com/library/azure/jj683097.aspx#getprotectionkey) methods tooget hello correct X.509 Certificate that must be used tooencrypt your content key.</span></span>
3. <span data-ttu-id="6df3c-145">Шифрование ключа содержимого с помощью открытого ключа сертификата X.509 hello hello.</span><span class="sxs-lookup"><span data-stu-id="6df3c-145">Encrypt your content key with hello public key of hello X.509 Certificate.</span></span> 
   
   <span data-ttu-id="6df3c-146">Пакет SDK .NET служб мультимедиа использует алгоритм RSA с OAEP при выполнении шифрования hello.</span><span class="sxs-lookup"><span data-stu-id="6df3c-146">Media Services .NET SDK uses RSA with OAEP when doing hello encryption.</span></span>  <span data-ttu-id="6df3c-147">Вы увидите пример .NET в hello [EncryptSymmetricKeyData функция](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.FileEncryption/EncryptionUtils.cs).</span><span class="sxs-lookup"><span data-stu-id="6df3c-147">You can see a .NET example in hello [EncryptSymmetricKeyData function](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.FileEncryption/EncryptionUtils.cs).</span></span>
4. <span data-ttu-id="6df3c-148">Создайте значение контрольной суммы, вычисленных с помощью идентификатора ключа hello и ключа содержимого.</span><span class="sxs-lookup"><span data-stu-id="6df3c-148">Create a checksum value calculated using hello key identifier and content key.</span></span> <span data-ttu-id="6df3c-149">Следующий пример .NET Hello вычисляет контрольную hello, с помощью hello GUID части идентификатора ключа hello и hello снимите ключа содержимого.</span><span class="sxs-lookup"><span data-stu-id="6df3c-149">hello following .NET example calculates hello checksum using hello GUID part of hello key identifier and hello clear content key.</span></span>

        public static string CalculateChecksum(byte[] contentKey, Guid keyId)
        {
            const int ChecksumLength = 8;
            const int KeyIdLength = 16;

            byte[] encryptedKeyId = null;

            // Checksum is computed by AES-ECB encrypting hello KID
            // with hello content key.
            using (AesCryptoServiceProvider rijndael = new AesCryptoServiceProvider())
            {
                rijndael.Mode = CipherMode.ECB;
                rijndael.Key = contentKey;
                rijndael.Padding = PaddingMode.None;

                ICryptoTransform encryptor = rijndael.CreateEncryptor();
                encryptedKeyId = new byte[KeyIdLength];
                encryptor.TransformBlock(keyId.ToByteArray(), 0, KeyIdLength, encryptedKeyId, 0);
            }

            byte[] retVal = new byte[ChecksumLength];
            Array.Copy(encryptedKeyId, retVal, ChecksumLength);

            return Convert.ToBase64String(retVal);
        }

1. <span data-ttu-id="6df3c-150">Создание ключа контента hello с hello **EncryptedContentKey** (преобразовать строку в кодировке toobase64), **ProtectionKeyId**, **ProtectionKeyType**,  **ContentKeyType**, и **контрольной суммы** значений, получаемых в предыдущих шагах.</span><span class="sxs-lookup"><span data-stu-id="6df3c-150">Create hello Content key with hello **EncryptedContentKey** (converted toobase64-encoded string), **ProtectionKeyId**, **ProtectionKeyType**, **ContentKeyType**, and **Checksum** values you have received in previous steps.</span></span>

    <span data-ttu-id="6df3c-151">Для шифрования хранилища hello следующие свойства должны быть включены в текст запроса hello.</span><span class="sxs-lookup"><span data-stu-id="6df3c-151">For storage encryption, hello following properties should be included in hello request body.</span></span>

    <span data-ttu-id="6df3c-152">Свойство текста запроса</span><span class="sxs-lookup"><span data-stu-id="6df3c-152">Request body property</span></span>    | <span data-ttu-id="6df3c-153">Описание</span><span class="sxs-lookup"><span data-stu-id="6df3c-153">Description</span></span>
    ---|---
    <span data-ttu-id="6df3c-154">Идентификатор</span><span class="sxs-lookup"><span data-stu-id="6df3c-154">Id</span></span> | <span data-ttu-id="6df3c-155">Hello код ContentKey, который мы создаем сами с помощью следующих hello отформатировать, «nb:kid:UUID:<NEW GUID>».</span><span class="sxs-lookup"><span data-stu-id="6df3c-155">hello ContentKey Id which we generate ourselves using hello following format, “nb:kid:UUID:<NEW GUID>”.</span></span>
    <span data-ttu-id="6df3c-156">ContentKeyType</span><span class="sxs-lookup"><span data-stu-id="6df3c-156">ContentKeyType</span></span> | <span data-ttu-id="6df3c-157">Это тип ключа контента hello как целое число для этого ключа контента.</span><span class="sxs-lookup"><span data-stu-id="6df3c-157">This is hello content key type as an integer for this content key.</span></span> <span data-ttu-id="6df3c-158">Мы передаем hello значение 1 для шифрования хранилища.</span><span class="sxs-lookup"><span data-stu-id="6df3c-158">We pass hello value 1 for storage encryption.</span></span>
    <span data-ttu-id="6df3c-159">EncryptedContentKey</span><span class="sxs-lookup"><span data-stu-id="6df3c-159">EncryptedContentKey</span></span> | <span data-ttu-id="6df3c-160">Мы создаем новое значение ключа содержимого, которое представляет собой 256-битное (32-байтное) значение.</span><span class="sxs-lookup"><span data-stu-id="6df3c-160">We create a new content key value which is a 256-bit (32 byte) value.</span></span> <span data-ttu-id="6df3c-161">Hello ключ шифруется с помощью hello сертификата хранилища шифрования X.509 который получен из службы мультимедиа Microsoft Azure, выполнив запрос HTTP GET для hello GetProtectionKeyId и GetProtectionKey методов.</span><span class="sxs-lookup"><span data-stu-id="6df3c-161">hello key is encrypted using hello storage encryption X.509 certificate which we retrieve from Microsoft Azure Media Services by executing a HTTP GET request for hello GetProtectionKeyId and GetProtectionKey Methods.</span></span> <span data-ttu-id="6df3c-162">Например, в разделе hello после кода .NET: hello **EncryptSymmetricKeyData** определенный метод [здесь](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.FileEncryption/EncryptionUtils.cs).</span><span class="sxs-lookup"><span data-stu-id="6df3c-162">As an example, see hello following .NET code: hello  **EncryptSymmetricKeyData** method defined [here](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.FileEncryption/EncryptionUtils.cs).</span></span>
    <span data-ttu-id="6df3c-163">ProtectionKeyId</span><span class="sxs-lookup"><span data-stu-id="6df3c-163">ProtectionKeyId</span></span> | <span data-ttu-id="6df3c-164">Это является hello код ключа защиты для hello сертификата хранилища шифрования X.509, используемый tooencrypt ключа контента.</span><span class="sxs-lookup"><span data-stu-id="6df3c-164">This is hello protection key id for hello storage encryption X.509 certificate that was used tooencrypt our content key.</span></span>
    <span data-ttu-id="6df3c-165">ProtectionKeyType</span><span class="sxs-lookup"><span data-stu-id="6df3c-165">ProtectionKeyType</span></span> | <span data-ttu-id="6df3c-166">Это тип шифрования hello для hello защиты ключа, который был ключ содержимого используется tooencrypt hello.</span><span class="sxs-lookup"><span data-stu-id="6df3c-166">This is hello encryption type for hello protection key that was used tooencrypt hello content key.</span></span> <span data-ttu-id="6df3c-167">В нашем примере этим значением является StorageEncryption(1).</span><span class="sxs-lookup"><span data-stu-id="6df3c-167">This value is StorageEncryption(1) for our example.</span></span>
    <span data-ttu-id="6df3c-168">Checksum</span><span class="sxs-lookup"><span data-stu-id="6df3c-168">Checksum</span></span> |<span data-ttu-id="6df3c-169">Hello MD5 вычисленная контрольная сумма для ключа контента hello.</span><span class="sxs-lookup"><span data-stu-id="6df3c-169">hello MD5 calculated checksum for hello content key.</span></span> <span data-ttu-id="6df3c-170">Она рассчитывается при шифровании кода hello контента с помощью ключа содержимого hello.</span><span class="sxs-lookup"><span data-stu-id="6df3c-170">It is computed by encrypting hello content Id with hello content key.</span></span> <span data-ttu-id="6df3c-171">Hello примере кода показано, как toocalculate hello контрольной суммы.</span><span class="sxs-lookup"><span data-stu-id="6df3c-171">hello example code demonstrates how toocalculate hello checksum.</span></span>


### <a name="retrieve-hello-protectionkeyid"></a><span data-ttu-id="6df3c-172">Получить hello ProtectionKeyId</span><span class="sxs-lookup"><span data-stu-id="6df3c-172">Retrieve hello ProtectionKeyId</span></span>
<span data-ttu-id="6df3c-173">Hello в следующем примере показано, как tooretrieve hello ProtectionKeyId, отпечаток сертификата, для hello сертификат, который необходимо использовать при шифровании ключа содержимого.</span><span class="sxs-lookup"><span data-stu-id="6df3c-173">hello following example shows how tooretrieve hello ProtectionKeyId, a certificate thumbprint, for hello certificate you must use when encrypting your content key.</span></span> <span data-ttu-id="6df3c-174">Выполните этот шаг toomake, что уже имеется hello соответствующий сертификат на компьютере.</span><span class="sxs-lookup"><span data-stu-id="6df3c-174">Do this step toomake sure that you already have hello appropriate certificate on your machine.</span></span>

<span data-ttu-id="6df3c-175">Запрос:</span><span class="sxs-lookup"><span data-stu-id="6df3c-175">Request:</span></span>

    GET https://media.windows.net/api/GetProtectionKeyId?contentKeyType=0 HTTP/1.1
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423034908&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=7eSLe1GHnxgilr3F2FPCGxdL2%2bwy%2f39XhMPGY9IizfU%3d
    x-ms-version: 2.11
    Host: media.windows.net

<span data-ttu-id="6df3c-176">Ответ:</span><span class="sxs-lookup"><span data-stu-id="6df3c-176">Response:</span></span>

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 139
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Server: Microsoft-IIS/8.5
    request-id: 2b6aa7a4-3a09-4b08-b581-26b55667f817
    x-ms-request-id: 2b6aa7a4-3a09-4b08-b581-26b55667f817
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Wed, 04 Feb 2015 02:42:52 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Edm.String","value":"7D9BB04D9D0A4A24800CADBFEF232689E048F69C"}

### <a name="retrieve-hello-protectionkey-for-hello-protectionkeyid"></a><span data-ttu-id="6df3c-177">Получить hello ProtectionKey для hello ProtectionKeyId</span><span class="sxs-lookup"><span data-stu-id="6df3c-177">Retrieve hello ProtectionKey for hello ProtectionKeyId</span></span>
<span data-ttu-id="6df3c-178">Hello следующем примере показано, как сертификат X.509 hello tooretrieve, с помощью значения ProtectionKeyId hello полученный в предыдущем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="6df3c-178">hello following example shows how tooretrieve hello X.509 certificate using hello ProtectionKeyId you received in hello previous step.</span></span>

<span data-ttu-id="6df3c-179">Запрос:</span><span class="sxs-lookup"><span data-stu-id="6df3c-179">Request:</span></span>

    GET https://media.windows.net/api/GetProtectionKey?ProtectionKeyId='7D9BB04D9D0A4A24800CADBFEF232689E048F69C' HTTP/1.1
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-e769-2233-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423141026&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=lDBz5YXKiWe5L7eXOHsLHc9kKEUcUiFJvrNFFSksgkM%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 78d1247a-58d7-40e5-96cc-70ff0dfa7382
    Host: media.windows.net

<span data-ttu-id="6df3c-180">Ответ:</span><span class="sxs-lookup"><span data-stu-id="6df3c-180">Response:</span></span>

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 1227
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: 78d1247a-58d7-40e5-96cc-70ff0dfa7382
    request-id: 1523e8f3-8ed2-40fe-8a9a-5d81eb572cc8
    x-ms-request-id: 1523e8f3-8ed2-40fe-8a9a-5d81eb572cc8
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Thu, 05 Feb 2015 07:52:30 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Edm.String",
    "value":"MIIDSTCCAjGgAwIBAgIQqf92wku/HLJGCbMAU8GEnDANBgkqhkiG9w0BAQQFADAuMSwwKgYDVQQDEyN3YW1zYmx1cmVnMDAxZW5jcnlwdGFsbHNlY3JldHMtY2VydDAeFw0xMjA1MjkwNzAwMDBaFw0zMjA1MjkwNzAwMDBaMC4xLDAqBgNVBAMTI3dhbXNibHVyZWcwMDFlbmNyeXB0YWxsc2VjcmV0cy1jZXJ0MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAzR0SEbXefvUjb9wCUfkEiKtGQ5Gc328qFPrhMjSo+YHe0AVviZ9YaxPPb0m1AaaRV4dqWpST2+JtDhLOmGpWmmA60tbATJDdmRzKi2eYAyhhE76MgJgL3myCQLP42jDusWXWSMabui3/tMDQs+zfi1sJ4Ch/lm5EvksYsu6o8sCv29VRwxfDLJPBy2NlbV4GbWz5Qxp2tAmHoROnfaRhwp6WIbquk69tEtu2U50CpPN2goLAqx2PpXAqA+prxCZYGTHqfmFJEKtZHhizVBTFPGS3ncfnQC9QIEwFbPw6E5PO5yNaB68radWsp5uvDg33G1i8IT39GstMW6zaaG7cNQIDAQABo2MwYTBfBgNVHQEEWDBWgBCOGT2hPhsvQioZimw8M+jOoTAwLjEsMCoGA1UEAxMjd2Ftc2JsdXJlZzAwMWVuY3J5cHRhbGxzZWNyZXRzLWNlcnSCEKn/dsJLvxyyRgmzAFPBhJwwDQYJKoZIhvcNAQEEBQADggEBABcrQPma2ekNS3Wc5wGXL/aHyQaQRwFGymnUJ+VR8jVUZaC/U/f6lR98eTlwycjVwRL7D15BfClGEHw66QdHejaViJCjbEIJJ3p2c9fzBKhjLhzB3VVNiLIaH6RSI1bMPd2eddSCqhDIn3VBN605GcYXMzhYp+YA6g9+YMNeS1b+LxX3fqixMQIxSHOLFZ1G/H2xfNawv0VikH3djNui3EKT1w/8aRkUv/AAV0b3rYkP/jA1I0CPn0XFk7STYoiJ3gJoKq9EMXhit+Iwfz0sMkfhWG12/XO+TAWqsK1ZxEjuC9OzrY7pFnNxs4Mu4S8iinehduSpY+9mDd3dHynNwT4="}

### <a name="create-hello-content-key"></a><span data-ttu-id="6df3c-181">Создание ключа контента hello</span><span class="sxs-lookup"><span data-stu-id="6df3c-181">Create hello content key</span></span>
<span data-ttu-id="6df3c-182">После получения сертификата X.509 hello и использовать его открытого ключа tooencrypt ключа содержимого создайте **ContentKey** сущности и установите его свойство значений соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="6df3c-182">After you have retrieved hello X.509 certificate and used its public key tooencrypt your content key, create a **ContentKey** entity and set its property values accordingly.</span></span>

<span data-ttu-id="6df3c-183">Одно из значений hello, необходимо задать при создания содержимого, что ключ имеет тип hello hello.</span><span class="sxs-lookup"><span data-stu-id="6df3c-183">One of hello values that you must set when create hello content key is hello type.</span></span> <span data-ttu-id="6df3c-184">В случае шифрования хранилища hello hello равно "1".</span><span class="sxs-lookup"><span data-stu-id="6df3c-184">In case of hello storage encryption, hello value is '1'.</span></span> 

<span data-ttu-id="6df3c-185">Следующий пример показывает как Hello toocreate **ContentKey** с **ContentKeyType** для шифрования хранилища («1») и hello **ProtectionKeyType** значение слишком «0» tooindicate, hello идентификатор ключа защиты является отпечатком сертификата X.509 hello.</span><span class="sxs-lookup"><span data-stu-id="6df3c-185">hello following example shows how toocreate a **ContentKey** with a **ContentKeyType** set for storage encryption ("1") and hello **ProtectionKeyType** set too"0" tooindicate that hello protection key Id is hello X.509 certificate thumbprint.</span></span>  

<span data-ttu-id="6df3c-186">Запрос</span><span class="sxs-lookup"><span data-stu-id="6df3c-186">Request</span></span>

    POST https://media.windows.net/api/ContentKeys HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423034908&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=7eSLe1GHnxgilr3F2FPCGxdL2%2bwy%2f39XhMPGY9IizfU%3d
    x-ms-version: 2.11
    Host: media.windows.net
    {
    "Name":"ContentKey",
    "ProtectionKeyId":"7D9BB04D9D0A4A24800CADBFEF232689E048F69C", 
    "ContentKeyType":"1", 
    "ProtectionKeyType":"0",
    "EncryptedContentKey":"your encrypted content key",
    "Checksum":"calculated checksum"
    }

<span data-ttu-id="6df3c-187">Ответ:</span><span class="sxs-lookup"><span data-stu-id="6df3c-187">Response:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 777
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://media.windows.net/api/ContentKeys('nb%3Akid%3AUUID%3A9c8ea9c6-52bd-4232-8a43-8e43d8564a99')
    Server: Microsoft-IIS/8.5
    request-id: 76e85e0f-5cf1-44cb-b689-b3455888682c
    x-ms-request-id: 76e85e0f-5cf1-44cb-b689-b3455888682c
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Wed, 04 Feb 2015 02:37:46 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#ContentKeys/@Element",
    "Id":"nb:kid:UUID:9c8ea9c6-52bd-4232-8a43-8e43d8564a99","Created":"2015-02-04T02:37:46.9684379Z",
    "LastModified":"2015-02-04T02:37:46.9684379Z",
    "ContentKeyType":1,
    "EncryptedContentKey":"your encrypted content key",
    "Name":"ContentKey",
    "ProtectionKeyId":"7D9BB04D9D0A4A24800CADBFEF232689E048F69C",
    "ProtectionKeyType":0,
    "Checksum":"calculated checksum"}

## <a name="create-an-asset"></a><span data-ttu-id="6df3c-188">Создание ресурса</span><span class="sxs-lookup"><span data-stu-id="6df3c-188">Create an asset</span></span>
<span data-ttu-id="6df3c-189">Следующий пример показывает как Hello toocreate актива.</span><span class="sxs-lookup"><span data-stu-id="6df3c-189">hello following example shows how toocreate an asset.</span></span>

<span data-ttu-id="6df3c-190">**HTTP-запрос**</span><span class="sxs-lookup"><span data-stu-id="6df3c-190">**HTTP Request**</span></span>

    POST https://media.windows.net/api/Assets HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-2233-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: media.windows.net

    {"Name":"BigBuckBunny" "Options":1}

<span data-ttu-id="6df3c-191">**HTTP-ответ**</span><span class="sxs-lookup"><span data-stu-id="6df3c-191">**HTTP Response**</span></span>

<span data-ttu-id="6df3c-192">В случае успешного выполнения возвращается hello следующее:</span><span class="sxs-lookup"><span data-stu-id="6df3c-192">If successful, hello following is returned:</span></span>

    HTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 452
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/Assets('nb%3Acid%3AUUID%3A9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: c59de965-bc89-4295-9a57-75d897e5221e
    request-id: e98be122-ae09-473a-8072-0ccd234a0657
    x-ms-request-id: e98be122-ae09-473a-8072-0ccd234a0657
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sun, 18 Jan 2015 22:06:40 GMT
    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Assets/@Element",
       "Id":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "State":0,
       "Created":"2015-01-18T22:06:40.6010903Z",
       "LastModified":"2015-01-18T22:06:40.6010903Z",
       "AlternateId":null,
       "Name":"BigBuckBunny.mp4",
       "Options":1,
       "Uri":"https://storagetestaccount001.blob.core.windows.net/asset-9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "StorageAccountName":"storagetestaccount001"
    }

## <a name="associate-hello-contentkey-with-an-asset"></a><span data-ttu-id="6df3c-193">Связать с активом hello ContentKey</span><span class="sxs-lookup"><span data-stu-id="6df3c-193">Associate hello ContentKey with an Asset</span></span>
<span data-ttu-id="6df3c-194">После создания hello ContentKey, свяжите его с ресурсом, используя операцию hello $links, как показано в следующий пример hello:</span><span class="sxs-lookup"><span data-stu-id="6df3c-194">After creating hello ContentKey, associate it with your Asset using hello $links operation, as shown in hello following example:</span></span>

<span data-ttu-id="6df3c-195">Запрос:</span><span class="sxs-lookup"><span data-stu-id="6df3c-195">Request:</span></span>

    POST https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3Afbd7ce05-1087-401b-aaae-29f16383c801')/$links/ContentKeys HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Content-Type: application/json
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423141026&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=lDBz5YXKiWe5L7eXOHsLHc9kKEUcUiFJvrNFFSksgkM%3d
    x-ms-version: 2.11
    Host: media.windows.net

    {"uri":"https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeys('nb%3Akid%3AUUID%3A01e6ea36-2285-4562-91f1-82c45736047c')"}

<span data-ttu-id="6df3c-196">Ответ:</span><span class="sxs-lookup"><span data-stu-id="6df3c-196">Response:</span></span>

    HTTP/1.1 204 No Content 

## <a name="create-an-assetfile"></a><span data-ttu-id="6df3c-197">Создание сущности AssetFile</span><span class="sxs-lookup"><span data-stu-id="6df3c-197">Create an AssetFile</span></span>
<span data-ttu-id="6df3c-198">Hello [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) сущности представляет видео- или файл, хранящийся в контейнере больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="6df3c-198">hello [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) entity represents a video or audio file that is stored in a blob container.</span></span> <span data-ttu-id="6df3c-199">Файл ресурса всегда связан с ресурсом, который, в свою очередь, может содержать один или несколько файлов ресурса.</span><span class="sxs-lookup"><span data-stu-id="6df3c-199">An asset file is always associated with an asset, and an asset may contain one or many asset files.</span></span> <span data-ttu-id="6df3c-200">задачу Hello Media Services Encoder завершается ошибкой, если объект файла ресурса не связан с цифровым файлом в контейнере больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="6df3c-200">hello Media Services Encoder task fails if an asset file object is not associated with a digital file in a blob container.</span></span>

<span data-ttu-id="6df3c-201">Обратите внимание, что hello **AssetFile** экземпляра и hello фактический файл мультимедиа являются двумя отдельными объектами.</span><span class="sxs-lookup"><span data-stu-id="6df3c-201">Note that hello **AssetFile** instance and hello actual media file are two distinct objects.</span></span> <span data-ttu-id="6df3c-202">экземпляр AssetFile Hello содержит метаданные о файле мультимедиа hello, а файл мультимедиа hello hello фактический контент мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="6df3c-202">hello AssetFile instance contains metadata about hello media file, while hello media file contains hello actual media content.</span></span>

<span data-ttu-id="6df3c-203">После отправки файла мультимедиа в контейнер больших двоичных объектов, используется hello **СЛИЯНИЯ** hello tooupdate HTTP-запроса AssetFile со сведениями о файл (не показано в этом разделе).</span><span class="sxs-lookup"><span data-stu-id="6df3c-203">After you upload your digital media file into a blob container, you will use hello **MERGE** HTTP request tooupdate hello AssetFile with information about your media file (not shown in this topic).</span></span> 

<span data-ttu-id="6df3c-204">**HTTP-запрос**</span><span class="sxs-lookup"><span data-stu-id="6df3c-204">**HTTP Request**</span></span>

    POST https://media.windows.net/api/Files HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-4ca2-2233-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: media.windows.net
    Content-Length: 164

    {  
       "IsEncrypted":"true",
       "EncryptionScheme" : "StorageEncryption", 
       "EncryptionVersion" : "1.0",       
       "EncryptionKeyId" : "nb:kid:UUID:32e6efaf-5fba-4538-b115-9d1cefe43510",
       "InitializationVector" : "397304628502661816</d:InitializationVector",
       "Options":0,
       "IsPrimary":"false",
       "MimeType":"video/mp4",
       "Name":"BigBuckBunny.mp4",
       "ParentAssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1"
    }

<span data-ttu-id="6df3c-205">**HTTP-ответ**</span><span class="sxs-lookup"><span data-stu-id="6df3c-205">**HTTP Response**</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 535
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/Files('nb%3Acid%3AUUID%3Af13a0137-0a62-9d4c-b3b9-ca944b5142c5')
    Server: Microsoft-IIS/8.5
    request-id: 98a30e2d-f379-4495-988e-0b79edc9b80e
    x-ms-request-id: 98a30e2d-f379-4495-988e-0b79edc9b80e
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 19 Jan 2015 00:34:07 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Files/@Element",
       "Id":"nb:cid:UUID:f13a0137-0a62-9d4c-b3b9-ca944b5142c5",
       "Name":"BigBuckBunny.mp4",
       "ContentFileSize":"0",
       "ParentAssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "EncryptionVersion": "1.0",
       "EncryptionScheme": "StorageEncryption",
       "IsEncrypted":true,
       "EncryptionKeyId":"nb:kid:UUID:32e6efaf-5fba-4538-b115-9d1cefe43510",
       "InitializationVector":"397304628502661816</d:InitializationVector",
       "IsPrimary":false,
       "LastModified":"2015-01-19T00:34:08.1934137Z",
       "Created":"2015-01-19T00:34:08.1934137Z",
       "MimeType":"video/mp4",
       "ContentChecksum":null
    }
