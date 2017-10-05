---
title: "Шифрование содержимого с помощью шифрования хранилища посредством REST API AMS"
description: "Узнайте, как шифровать содержимое с шифрованием хранилища, используя API REST AMS."
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
ms.openlocfilehash: 1979f5bf5e8cab88dab5fba49018afacf24504b3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="encrypting-your-content-with-storage-encryption"></a><span data-ttu-id="94a5c-103">Шифрование содержимого с помощью шифрования хранилища</span><span class="sxs-lookup"><span data-stu-id="94a5c-103">Encrypting your content with storage encryption</span></span>

<span data-ttu-id="94a5c-104">Настоятельно рекомендуется шифровать содержимое локально, используя 256-битное шифрование AES, а затем передавать его в хранилище Azure, где оно будет храниться в зашифрованном виде.</span><span class="sxs-lookup"><span data-stu-id="94a5c-104">It is highly recommended to encrypt your content locally using AES-256 bit encryption and then upload it to Azure Storage where it will be stored encrypted at rest.</span></span>

<span data-ttu-id="94a5c-105">В этой статье приводятся общие сведения о шифровании хранилища AMS и показывается, как передавать зашифрованное содержимое хранилища.</span><span class="sxs-lookup"><span data-stu-id="94a5c-105">This article gives an overview of AMS storage encryption and shows you how to upload the storage encrypted content:</span></span>

* <span data-ttu-id="94a5c-106">Создайте ключ содержимого.</span><span class="sxs-lookup"><span data-stu-id="94a5c-106">Create a content key.</span></span>
* <span data-ttu-id="94a5c-107">Создайте ресурс.</span><span class="sxs-lookup"><span data-stu-id="94a5c-107">Create an Asset.</span></span> <span data-ttu-id="94a5c-108">При создании ресурса задайте для параметра AssetCreationOption значение StorageEncryption.</span><span class="sxs-lookup"><span data-stu-id="94a5c-108">Set the AssetCreationOption to StorageEncryption when creating the Asset.</span></span>
  
     <span data-ttu-id="94a5c-109">Зашифрованные ресурсы-контейнеры должны быть связаны с типами содержимого.</span><span class="sxs-lookup"><span data-stu-id="94a5c-109">Encrypted assets have to be associated with content keys.</span></span>
* <span data-ttu-id="94a5c-110">Привяжите ключ содержимого к ресурсу.</span><span class="sxs-lookup"><span data-stu-id="94a5c-110">Link the content key to the asset.</span></span>  
* <span data-ttu-id="94a5c-111">Настройте связанные с шифрованием параметры в сущностях AssetFile.</span><span class="sxs-lookup"><span data-stu-id="94a5c-111">Set the encryption related parameters on the AssetFile entities.</span></span>

## <a name="considerations"></a><span data-ttu-id="94a5c-112">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="94a5c-112">Considerations</span></span> 

<span data-ttu-id="94a5c-113">Если необходимо доставить зашифрованный в хранилище ресурс-контейнер, необходимо настроить его политику доставки.</span><span class="sxs-lookup"><span data-stu-id="94a5c-113">If you want to deliver a storage encrypted asset, you must configure the asset’s delivery policy.</span></span> <span data-ttu-id="94a5c-114">Перед выполнением потоковой передачи ресурса сервер потоковой передачи удаляет шифрование хранилища и осуществляет потоковую передачу содержимого с помощью указанной политики доставки.</span><span class="sxs-lookup"><span data-stu-id="94a5c-114">Before your asset can be streamed, the streaming server removes the storage encryption and streams your content using the specified delivery policy.</span></span> <span data-ttu-id="94a5c-115">Дополнительные сведения см. в статье [Настройка политик доставки ресурсов](media-services-rest-configure-asset-delivery-policy.md).</span><span class="sxs-lookup"><span data-stu-id="94a5c-115">For more information, see [Configuring Asset Delivery Policies](media-services-rest-configure-asset-delivery-policy.md).</span></span>

<span data-ttu-id="94a5c-116">При доступе к сущностям в службах мультимедиа необходимо задать определенные поля и значения заголовков в HTTP-запросах.</span><span class="sxs-lookup"><span data-stu-id="94a5c-116">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="94a5c-117">Дополнительную информацию см. в статье [Обзор интерфейса REST API служб мультимедиа](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="94a5c-117">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span> 

## <a name="connect-to-media-services"></a><span data-ttu-id="94a5c-118">Подключение к службам мультимедиа</span><span class="sxs-lookup"><span data-stu-id="94a5c-118">Connect to Media Services</span></span>

<span data-ttu-id="94a5c-119">Сведения о подключении к API AMS см. в разделе [Доступ к API служб мультимедиа Azure с помощью аутентификации Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="94a5c-119">For information on how to connect to the AMS API, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="94a5c-120">После успешного подключения к https://media.windows.net вы получите ошибку 301 (перенаправление), в которой будет указан другой URI служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="94a5c-120">After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="94a5c-121">Используйте для последующих вызовов новый URI.</span><span class="sxs-lookup"><span data-stu-id="94a5c-121">You must make subsequent calls to the new URI.</span></span>

## <a name="storage-encryption-overview"></a><span data-ttu-id="94a5c-122">Общие сведения о шифровании хранилища</span><span class="sxs-lookup"><span data-stu-id="94a5c-122">Storage encryption overview</span></span>
<span data-ttu-id="94a5c-123">Шифрование хранилища AMS применяет режим шифрования **AES-CTR** ко всему файлу.</span><span class="sxs-lookup"><span data-stu-id="94a5c-123">The AMS storage encryption applies **AES-CTR** mode encryption to the entire file.</span></span>  <span data-ttu-id="94a5c-124">AES-CTR — это блочный шифр, который может шифровать данные произвольной длины и не требует заполнения.</span><span class="sxs-lookup"><span data-stu-id="94a5c-124">AES-CTR mode is a block cipher that can encrypt arbitrary length data without need for padding.</span></span> <span data-ttu-id="94a5c-125">Он шифрует блок счетчика, используя алгоритм AES, а затем применяет XOR к выходным данным AES, содержащим данные для шифрования или расшифровки.</span><span class="sxs-lookup"><span data-stu-id="94a5c-125">It operates by encrypting a counter block with the AES algorithm and then XOR-ing the output of AES with the data to encrypt or decrypt.</span></span>  <span data-ttu-id="94a5c-126">Используемый блок счетчика формируется путем копирования значения InitializationVector в байты 0–7 значения счетчика и присвоения байтам 8–15 нулевого значения.</span><span class="sxs-lookup"><span data-stu-id="94a5c-126">The counter block used is constructed by copying the value of the InitializationVector to bytes 0 to 7 of the counter value and bytes 8 to 15 of the counter value are set to zero.</span></span> <span data-ttu-id="94a5c-127">Байты 8–15 в 16-байтовом блоке счетчика (т. е. наименее значимые) используются как простое 64-разрядное целое число без знака, увеличивающееся на единицу с каждым последующим блоком данных, которые обрабатываются и хранятся в соответствии с порядком байтов в сети.</span><span class="sxs-lookup"><span data-stu-id="94a5c-127">Of the 16 byte counter block, bytes 8 to 15 (i.e. the least significant bytes) are used as a simple 64 bit unsigned integer that is incremented by one for each subsequent block of data processed and is kept in network byte order.</span></span> <span data-ttu-id="94a5c-128">Если это число достигает максимального значения (0xFFFFFFFFFFFFFFFF), при следующем приращении счетчик блока сбрасывается до нуля (байты 8–15) и не влияет на другие 64 разряда в счетчика (байты 0–7).</span><span class="sxs-lookup"><span data-stu-id="94a5c-128">Note that if this integer reaches the maximum value (0xFFFFFFFFFFFFFFFF) then incrementing it resets the block counter to zero (bytes 8 to 15) without affecting the other 64 bits of the counter (i.e. bytes 0 to 7).</span></span>   <span data-ttu-id="94a5c-129">Для обеспечения безопасности шифрования в режиме AES-CTR значение InitializationVector для соответствующего идентификатора ключа должно быть уникальным для каждого файла содержимого, а длина файлов должна быть меньше 2^64 блоков.</span><span class="sxs-lookup"><span data-stu-id="94a5c-129">In order to maintain the security of the AES-CTR mode encryption, the InitializationVector value for a given Key Identifier for each content key shall be unique for each file and files shall be less than 2^64 blocks in length.</span></span>  <span data-ttu-id="94a5c-130">Это гарантирует, что значение счетчика не будет использоваться с данным ключом повторно.</span><span class="sxs-lookup"><span data-stu-id="94a5c-130">This is to ensure that a counter value is never reused with a given key.</span></span> <span data-ttu-id="94a5c-131">Дополнительные сведения о режиме CTR см. на [этой вики-странице](https://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#CTR) (в вики-статье вместо InitializationVector используется термин Nonce).</span><span class="sxs-lookup"><span data-stu-id="94a5c-131">For more information about the CTR mode, see [this wiki page](https://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#CTR) (the wiki article uses the term "Nonce" instead of "InitializationVector").</span></span>

<span data-ttu-id="94a5c-132">Параметр **Storage Encryption** используется для локального удаления незашифрованного содержимого с помощью AES 256 и его добавления в хранилище Azure, где оно хранится в зашифрованном виде.</span><span class="sxs-lookup"><span data-stu-id="94a5c-132">Use **Storage Encryption** to encrypt your clear content locally using AES-256 bit encryption and then upload it to Azure Storage where it is stored encrypted at rest.</span></span> <span data-ttu-id="94a5c-133">Ресурсы, защищенные с помощью шифрования хранилища, автоматически расшифровываются и помещаются в зашифрованную файловую систему до кодирования, а затем при необходимости повторно кодируются перед добавлением в виде нового выходного актива.</span><span class="sxs-lookup"><span data-stu-id="94a5c-133">Assets protected with storage encryption are automatically unencrypted and placed in an encrypted file system prior to encoding, and optionally re-encrypted prior to uploading back as a new output asset.</span></span> <span data-ttu-id="94a5c-134">Основная причина использования шифрования хранилища — для защиты входных файлов мультимедиа высокого качества с помощью стойкого шифрования при хранении на диске.</span><span class="sxs-lookup"><span data-stu-id="94a5c-134">The primary use case for storage encryption is when you want to secure your high quality input media files with strong encryption at rest on disk.</span></span>

<span data-ttu-id="94a5c-135">Для доставки ресурса из зашифрованного хранилища необходимо настроить политику доставки ресурсов, чтобы службы мультимедиа могли определить, как вы хотите доставлять содержимое.</span><span class="sxs-lookup"><span data-stu-id="94a5c-135">In order to deliver a storage encrypted asset, you must configure the asset’s delivery policy so Media Services knows how you want to deliver your content.</span></span> <span data-ttu-id="94a5c-136">Перед выполнением потоковой передачи ресурса-контейнера сервер потоковой передачи удаляет шифрование хранилища и осуществляет потоковую передачу содержимого с помощью указанной политики доставки (например, AES, общее шифрование или без шифрования).</span><span class="sxs-lookup"><span data-stu-id="94a5c-136">Before your asset can be streamed, the streaming server removes the storage encryption and streams your content using the specified delivery policy (for example, AES, common encryption, or no encryption).</span></span>

## <a name="create-contentkeys-used-for-encryption"></a><span data-ttu-id="94a5c-137">Создание сущности ContentKeys, используемой для шифрования</span><span class="sxs-lookup"><span data-stu-id="94a5c-137">Create ContentKeys used for encryption</span></span>
<span data-ttu-id="94a5c-138">Зашифрованные ресурсы должны быть связаны с ключом шифрования хранилища.</span><span class="sxs-lookup"><span data-stu-id="94a5c-138">Encrypted assets have to be associated with Storage Encryption key.</span></span> <span data-ttu-id="94a5c-139">Прежде чем создавать файлы ресурсов, необходимо создать ключ содержимого, который будет использоваться для шифрования.</span><span class="sxs-lookup"><span data-stu-id="94a5c-139">You must create the content key to be used for encryption before creating the asset files.</span></span> <span data-ttu-id="94a5c-140">В этой статье описывается, как создать ключ содержимого.</span><span class="sxs-lookup"><span data-stu-id="94a5c-140">This section describes how to create a content key.</span></span>

<span data-ttu-id="94a5c-141">Ниже приведены общие шаги создания ключей содержимого, которые нужно связать с ресурсами, подлежащими шифрованию.</span><span class="sxs-lookup"><span data-stu-id="94a5c-141">The following are general steps for generating content keys that you will associate with assets that you want to be encrypted.</span></span> 

1. <span data-ttu-id="94a5c-142">Для шифрования хранилища случайным образом формируется 32-разрядный ключ AES.</span><span class="sxs-lookup"><span data-stu-id="94a5c-142">For storage encryption, randomly generate a 32-byte AES key.</span></span> 
   
    <span data-ttu-id="94a5c-143">Это будет ключ содержимого для ресурса, то есть для всех файлов, связанных с этим ресурсом, при расшифровке будет использоваться один и тот же ключ содержимого.</span><span class="sxs-lookup"><span data-stu-id="94a5c-143">This will be the content key for your asset, which means all files associated with that asset will need to use the same content key during decryption.</span></span> 
2. <span data-ttu-id="94a5c-144">Вызовите методы [GetProtectionKeyId](https://docs.microsoft.com/rest/api/media/operations/rest-api-functions#getprotectionkeyid) и [GetProtectionKey](https://msdn.microsoft.com/library/azure/jj683097.aspx#getprotectionkey), чтобы получить правильный сертификат X.509, который должен использоваться для шифрования ключа содержимого.</span><span class="sxs-lookup"><span data-stu-id="94a5c-144">Call the [GetProtectionKeyId](https://docs.microsoft.com/rest/api/media/operations/rest-api-functions#getprotectionkeyid) and [GetProtectionKey](https://msdn.microsoft.com/library/azure/jj683097.aspx#getprotectionkey) methods to get the correct X.509 Certificate that must be used to encrypt your content key.</span></span>
3. <span data-ttu-id="94a5c-145">Зашифруйте ключ содержимого с помощью открытого ключа сертификата X.509.</span><span class="sxs-lookup"><span data-stu-id="94a5c-145">Encrypt your content key with the public key of the X.509 Certificate.</span></span> 
   
   <span data-ttu-id="94a5c-146">Пакет SDK служб мультимедиа для .NET использует при выполнении шифрования RSA с OAEP.</span><span class="sxs-lookup"><span data-stu-id="94a5c-146">Media Services .NET SDK uses RSA with OAEP when doing the encryption.</span></span>  <span data-ttu-id="94a5c-147">Примером .NETможет служить [функция EncryptSymmetricKeyData](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.FileEncryption/EncryptionUtils.cs).</span><span class="sxs-lookup"><span data-stu-id="94a5c-147">You can see a .NET example in the [EncryptSymmetricKeyData function](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.FileEncryption/EncryptionUtils.cs).</span></span>
4. <span data-ttu-id="94a5c-148">Создайте значение контрольной суммы, вычисленное с помощью идентификатора ключа и ключа содержимого.</span><span class="sxs-lookup"><span data-stu-id="94a5c-148">Create a checksum value calculated using the key identifier and content key.</span></span> <span data-ttu-id="94a5c-149">В следующем примере .NET контрольная сумма вычисляется с помощью части "GUID" идентификатора ключа и незащищенного ключа содержимого.</span><span class="sxs-lookup"><span data-stu-id="94a5c-149">The following .NET example calculates the checksum using the GUID part of the key identifier and the clear content key.</span></span>

        public static string CalculateChecksum(byte[] contentKey, Guid keyId)
        {
            const int ChecksumLength = 8;
            const int KeyIdLength = 16;

            byte[] encryptedKeyId = null;

            // Checksum is computed by AES-ECB encrypting the KID
            // with the content key.
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

1. <span data-ttu-id="94a5c-150">Создайте ключ содержимого, используя значения **EncryptedContentKey** (преобразуется в строку с кодировкой base64), **ProtectionKeyId**, **ProtectionKeyType**, **ContentKeyType** и **Checksum**, полученные на предыдущих шагах.</span><span class="sxs-lookup"><span data-stu-id="94a5c-150">Create the Content key with the **EncryptedContentKey** (converted to base64-encoded string), **ProtectionKeyId**, **ProtectionKeyType**, **ContentKeyType**, and **Checksum** values you have received in previous steps.</span></span>

    <span data-ttu-id="94a5c-151">Для шифрования хранилища в текст запроса необходимо включить указанные ниже свойства.</span><span class="sxs-lookup"><span data-stu-id="94a5c-151">For storage encryption, the following properties should be included in the request body.</span></span>

    <span data-ttu-id="94a5c-152">Свойство текста запроса</span><span class="sxs-lookup"><span data-stu-id="94a5c-152">Request body property</span></span>    | <span data-ttu-id="94a5c-153">Описание</span><span class="sxs-lookup"><span data-stu-id="94a5c-153">Description</span></span>
    ---|---
    <span data-ttu-id="94a5c-154">Идентификатор</span><span class="sxs-lookup"><span data-stu-id="94a5c-154">Id</span></span> | <span data-ttu-id="94a5c-155">Идентификатор ContentKey, созданный нами в следующем формате "nb:kid:UUID:<NEW GUID>".</span><span class="sxs-lookup"><span data-stu-id="94a5c-155">The ContentKey Id which we generate ourselves using the following format, “nb:kid:UUID:<NEW GUID>”.</span></span>
    <span data-ttu-id="94a5c-156">ContentKeyType</span><span class="sxs-lookup"><span data-stu-id="94a5c-156">ContentKeyType</span></span> | <span data-ttu-id="94a5c-157">Тип ключа содержимого, который в данном случае выражается целым числом.</span><span class="sxs-lookup"><span data-stu-id="94a5c-157">This is the content key type as an integer for this content key.</span></span> <span data-ttu-id="94a5c-158">Для шифрования хранилища передается значение 1.</span><span class="sxs-lookup"><span data-stu-id="94a5c-158">We pass the value 1 for storage encryption.</span></span>
    <span data-ttu-id="94a5c-159">EncryptedContentKey</span><span class="sxs-lookup"><span data-stu-id="94a5c-159">EncryptedContentKey</span></span> | <span data-ttu-id="94a5c-160">Мы создаем новое значение ключа содержимого, которое представляет собой 256-битное (32-байтное) значение.</span><span class="sxs-lookup"><span data-stu-id="94a5c-160">We create a new content key value which is a 256-bit (32 byte) value.</span></span> <span data-ttu-id="94a5c-161">Ключ шифруется с помощью сертификата шифрования хранилища X.509, полученного из служб мультимедиа Microsoft Azure с помощью HTTP- запроса GET для методов GetProtectionKeyId и GetProtectionKey.</span><span class="sxs-lookup"><span data-stu-id="94a5c-161">The key is encrypted using the storage encryption X.509 certificate which we retrieve from Microsoft Azure Media Services by executing a HTTP GET request for the GetProtectionKeyId and GetProtectionKey Methods.</span></span> <span data-ttu-id="94a5c-162">Например, см. следующий код .NET: метод **EncryptSymmetricKeyData**, определенный [здесь](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.FileEncryption/EncryptionUtils.cs).</span><span class="sxs-lookup"><span data-stu-id="94a5c-162">As an example, see the following .NET code: the  **EncryptSymmetricKeyData** method defined [here](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.FileEncryption/EncryptionUtils.cs).</span></span>
    <span data-ttu-id="94a5c-163">ProtectionKeyId</span><span class="sxs-lookup"><span data-stu-id="94a5c-163">ProtectionKeyId</span></span> | <span data-ttu-id="94a5c-164">Идентификатор ключа защиты для сертификата шифрования хранилища X.509, который использовался для шифрования ключа содержимого.</span><span class="sxs-lookup"><span data-stu-id="94a5c-164">This is the protection key id for the storage encryption X.509 certificate that was used to encrypt our content key.</span></span>
    <span data-ttu-id="94a5c-165">ProtectionKeyType</span><span class="sxs-lookup"><span data-stu-id="94a5c-165">ProtectionKeyType</span></span> | <span data-ttu-id="94a5c-166">Тип шифрования для защиты ключа, который использовался для шифрования ключа содержимого.</span><span class="sxs-lookup"><span data-stu-id="94a5c-166">This is the encryption type for the protection key that was used to encrypt the content key.</span></span> <span data-ttu-id="94a5c-167">В нашем примере этим значением является StorageEncryption(1).</span><span class="sxs-lookup"><span data-stu-id="94a5c-167">This value is StorageEncryption(1) for our example.</span></span>
    <span data-ttu-id="94a5c-168">Checksum</span><span class="sxs-lookup"><span data-stu-id="94a5c-168">Checksum</span></span> |<span data-ttu-id="94a5c-169">Контрольная сумма, рассчитанная для ключа содержимого с помощью MD5.</span><span class="sxs-lookup"><span data-stu-id="94a5c-169">The MD5 calculated checksum for the content key.</span></span> <span data-ttu-id="94a5c-170">Она вычисляется путем шифрования идентификатора содержимого с использованием ключа содержимого.</span><span class="sxs-lookup"><span data-stu-id="94a5c-170">It is computed by encrypting the content Id with the content key.</span></span> <span data-ttu-id="94a5c-171">В примере кода показано, как вычислить контрольную сумму.</span><span class="sxs-lookup"><span data-stu-id="94a5c-171">The example code demonstrates how to calculate the checksum.</span></span>


### <a name="retrieve-the-protectionkeyid"></a><span data-ttu-id="94a5c-172">Получение ProtectionKeyId</span><span class="sxs-lookup"><span data-stu-id="94a5c-172">Retrieve the ProtectionKeyId</span></span>
<span data-ttu-id="94a5c-173">В следующем примере показано, как получить ProtectionKeyId (отпечаток сертификата) для сертификата, который необходимо использовать при шифровании ключа содержимого.</span><span class="sxs-lookup"><span data-stu-id="94a5c-173">The following example shows how to retrieve the ProtectionKeyId, a certificate thumbprint, for the certificate you must use when encrypting your content key.</span></span> <span data-ttu-id="94a5c-174">Выполните этот шаг, чтобы проверить наличие соответствующего сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="94a5c-174">Do this step to make sure that you already have the appropriate certificate on your machine.</span></span>

<span data-ttu-id="94a5c-175">Запрос:</span><span class="sxs-lookup"><span data-stu-id="94a5c-175">Request:</span></span>

    GET https://media.windows.net/api/GetProtectionKeyId?contentKeyType=0 HTTP/1.1
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423034908&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=7eSLe1GHnxgilr3F2FPCGxdL2%2bwy%2f39XhMPGY9IizfU%3d
    x-ms-version: 2.11
    Host: media.windows.net

<span data-ttu-id="94a5c-176">Ответ:</span><span class="sxs-lookup"><span data-stu-id="94a5c-176">Response:</span></span>

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

### <a name="retrieve-the-protectionkey-for-the-protectionkeyid"></a><span data-ttu-id="94a5c-177">Получение ProtectionKey для ProtectionKeyId</span><span class="sxs-lookup"><span data-stu-id="94a5c-177">Retrieve the ProtectionKey for the ProtectionKeyId</span></span>
<span data-ttu-id="94a5c-178">В следующем примере показано, как получить сертификат X.509, используя значение ProtectionKeyId, полученное на предыдущем шаге.</span><span class="sxs-lookup"><span data-stu-id="94a5c-178">The following example shows how to retrieve the X.509 certificate using the ProtectionKeyId you received in the previous step.</span></span>

<span data-ttu-id="94a5c-179">Запрос:</span><span class="sxs-lookup"><span data-stu-id="94a5c-179">Request:</span></span>

    GET https://media.windows.net/api/GetProtectionKey?ProtectionKeyId='7D9BB04D9D0A4A24800CADBFEF232689E048F69C' HTTP/1.1
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-e769-2233-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423141026&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=lDBz5YXKiWe5L7eXOHsLHc9kKEUcUiFJvrNFFSksgkM%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 78d1247a-58d7-40e5-96cc-70ff0dfa7382
    Host: media.windows.net

<span data-ttu-id="94a5c-180">Ответ:</span><span class="sxs-lookup"><span data-stu-id="94a5c-180">Response:</span></span>

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

### <a name="create-the-content-key"></a><span data-ttu-id="94a5c-181">Создание ключа содержимого</span><span class="sxs-lookup"><span data-stu-id="94a5c-181">Create the content key</span></span>
<span data-ttu-id="94a5c-182">После получения сертификата X.509 и использования его открытого ключа для шифрования ключа содержимого создайте сущность **ContentKey** и задайте для нее соответствующие свойства.</span><span class="sxs-lookup"><span data-stu-id="94a5c-182">After you have retrieved the X.509 certificate and used its public key to encrypt your content key, create a **ContentKey** entity and set its property values accordingly.</span></span>

<span data-ttu-id="94a5c-183">Одно из значений, которые необходимо задать при создания ключа содержимого — это тип.</span><span class="sxs-lookup"><span data-stu-id="94a5c-183">One of the values that you must set when create the content key is the type.</span></span> <span data-ttu-id="94a5c-184">Для шифрования хранилища используется значение "1".</span><span class="sxs-lookup"><span data-stu-id="94a5c-184">In case of the storage encryption, the value is '1'.</span></span> 

<span data-ttu-id="94a5c-185">В следующем примере показано, как создать **ContentKey**, когда для параметра **ContentKeyType** задано шифрование в хранилище (значение 1), а для параметра **ProtectionKeyType** — значение 0, указывающее на то, что идентификатор ключа защиты является отпечатком сертификата X.509.</span><span class="sxs-lookup"><span data-stu-id="94a5c-185">The following example shows how to create a **ContentKey** with a **ContentKeyType** set for storage encryption ("1") and the **ProtectionKeyType** set to "0" to indicate that the protection key Id is the X.509 certificate thumbprint.</span></span>  

<span data-ttu-id="94a5c-186">Запрос</span><span class="sxs-lookup"><span data-stu-id="94a5c-186">Request</span></span>

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

<span data-ttu-id="94a5c-187">Ответ:</span><span class="sxs-lookup"><span data-stu-id="94a5c-187">Response:</span></span>

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

## <a name="create-an-asset"></a><span data-ttu-id="94a5c-188">Создание ресурса</span><span class="sxs-lookup"><span data-stu-id="94a5c-188">Create an asset</span></span>
<span data-ttu-id="94a5c-189">В следующем примере показано, как создать ресурс.</span><span class="sxs-lookup"><span data-stu-id="94a5c-189">The following example shows how to create an asset.</span></span>

<span data-ttu-id="94a5c-190">**HTTP-запрос**</span><span class="sxs-lookup"><span data-stu-id="94a5c-190">**HTTP Request**</span></span>

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

<span data-ttu-id="94a5c-191">**HTTP-ответ**</span><span class="sxs-lookup"><span data-stu-id="94a5c-191">**HTTP Response**</span></span>

<span data-ttu-id="94a5c-192">При успешном выполнении возвращается следующий результат:</span><span class="sxs-lookup"><span data-stu-id="94a5c-192">If successful, the following is returned:</span></span>

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

## <a name="associate-the-contentkey-with-an-asset"></a><span data-ttu-id="94a5c-193">Связывание сущности ContentKey с сущностью Asset</span><span class="sxs-lookup"><span data-stu-id="94a5c-193">Associate the ContentKey with an Asset</span></span>
<span data-ttu-id="94a5c-194">После создания сущности ContentKey свяжите ее с сущностью Asset, используя операцию $links, как показано в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="94a5c-194">After creating the ContentKey, associate it with your Asset using the $links operation, as shown in the following example:</span></span>

<span data-ttu-id="94a5c-195">Запрос:</span><span class="sxs-lookup"><span data-stu-id="94a5c-195">Request:</span></span>

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

<span data-ttu-id="94a5c-196">Ответ:</span><span class="sxs-lookup"><span data-stu-id="94a5c-196">Response:</span></span>

    HTTP/1.1 204 No Content 

## <a name="create-an-assetfile"></a><span data-ttu-id="94a5c-197">Создание сущности AssetFile</span><span class="sxs-lookup"><span data-stu-id="94a5c-197">Create an AssetFile</span></span>
<span data-ttu-id="94a5c-198">Сущность [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) представляет собой аудио- или видеофайл, который хранится в контейнере больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="94a5c-198">The [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) entity represents a video or audio file that is stored in a blob container.</span></span> <span data-ttu-id="94a5c-199">Файл ресурса всегда связан с ресурсом, который, в свою очередь, может содержать один или несколько файлов ресурса.</span><span class="sxs-lookup"><span data-stu-id="94a5c-199">An asset file is always associated with an asset, and an asset may contain one or many asset files.</span></span> <span data-ttu-id="94a5c-200">Задача кодировщика служб мультимедиа завершится с ошибкой, если объект файла ресурса не связан с цифровым файлом в контейнере больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="94a5c-200">The Media Services Encoder task fails if an asset file object is not associated with a digital file in a blob container.</span></span>

<span data-ttu-id="94a5c-201">Обратите внимание, что экземпляр **AssetFile** и фактический файл мультимедиа – это два разных объекта.</span><span class="sxs-lookup"><span data-stu-id="94a5c-201">Note that the **AssetFile** instance and the actual media file are two distinct objects.</span></span> <span data-ttu-id="94a5c-202">Экземпляр AssetFile содержит метаданные о файле мультимедиа, а сам файл мультимедиа — фактическое мультимедийное содержимое.</span><span class="sxs-lookup"><span data-stu-id="94a5c-202">The AssetFile instance contains metadata about the media file, while the media file contains the actual media content.</span></span>

<span data-ttu-id="94a5c-203">После отправки цифрового файла мультимедиа в контейнер больших двоичных объектов будет использоваться HTTP-запрос **MERGE** , чтобы обновить сущность AssetFile информацией о файле мультимедиа (не показано в этом разделе).</span><span class="sxs-lookup"><span data-stu-id="94a5c-203">After you upload your digital media file into a blob container, you will use the **MERGE** HTTP request to update the AssetFile with information about your media file (not shown in this topic).</span></span> 

<span data-ttu-id="94a5c-204">**HTTP-запрос**</span><span class="sxs-lookup"><span data-stu-id="94a5c-204">**HTTP Request**</span></span>

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

<span data-ttu-id="94a5c-205">**HTTP-ответ**</span><span class="sxs-lookup"><span data-stu-id="94a5c-205">**HTTP Response**</span></span>

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
