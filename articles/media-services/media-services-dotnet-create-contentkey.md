---
title: "aaaCreate ContentKeys в .NET Framework"
description: "Узнайте, как toocreate содержимого ключи, которые обеспечивают безопасный доступ к tooAssets."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 225b05e5-7d30-409c-b5b7-3ef0634310c7
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako
ms.openlocfilehash: 35909c64e8393e228be75c464a034ffc40122952
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-contentkeys-with-net"></a>Создание ContentKey с использованием .NET
> [!div class="op_single_selector"]
> * [REST](media-services-rest-create-contentkey.md)
> * [.NET](media-services-dotnet-create-contentkey.md)
> 
> 

Media Services позволяет toocreate и доставка зашифрованные активы. Объект **ContentKey** обеспечивает безопасный доступ tooyour **активов**s. 

При создании нового средства (например, прежде чем [передачи файлов](media-services-dotnet-upload-files.md)), можно указать следующие параметры шифрования hello: **StorageEncrypted**, **CommonEncryptionProtected**, или **EnvelopeEncryptionProtected**. 

После доставки активов tooyour клиентов, вы можете [настройки для средств toobe динамически зашифрованные](media-services-dotnet-configure-asset-delivery-policy.md) с одним hello, следующие два шифрования: **DynamicEnvelopeEncryption** или  **DynamicCommonEncryption**.

Зашифрованные активы имеют связанные с toobe **ContentKey**s. В этой статье описывается как toocreate ключа содержимого.

> [!NOTE]
> При создании нового **StorageEncrypted** активов с помощью hello Media Services .NET SDK hello **ContentKey** автоматически создается и связанный с активом hello.
> 
> 

## <a name="contentkeytype"></a>ContentKeyType
Одно из значений hello, необходимо задать при создании содержимого ключ является тип ключа контента hello. Выберите один из hello следующие значения. 

    public enum ContentKeyType
    {
        /// <summary>
        /// Specifies a content key for common encryption.
        /// </summary>
        /// <remarks>This is hello default value.</remarks>
        CommonEncryption = 0,

        /// <summary>
        /// Specifies a content key for storage encryption.
        /// </summary>
        StorageEncryption = 1,

        /// <summary>
        /// Specifies a content key for configuration encryption.
        /// </summary>
        ConfigurationEncryption = 2,

        /// <summary>
        /// Specifies a content key for Envelope encryption.  Only used internally.
        /// </summary>
        EnvelopeEncryption = 4
    }

## <a id="envelope_contentkey"></a>Создание ContentKey конвертного типа
Hello следующий фрагмент кода создает ключ содержимого для типа шифрования конвертов hello. Затем он связывает hello ключ с указанным ресурсом hello.

    static public IContentKey CreateEnvelopeTypeContentKey(IAsset asset)
    {
        // Create envelope encryption content key
        Guid keyId = Guid.NewGuid();
        byte[] contentKey = GetRandomBuffer(16);

        IContentKey key = _context.ContentKeys.Create(
                                keyId,
                                contentKey,
                                "ContentKey",
                                ContentKeyType.EnvelopeEncryption);

        asset.ContentKeys.Add(key);

        return key;
    }

    static private byte[] GetRandomBuffer(int size)
    {
        byte[] randomBytes = new byte[size];
        using (RNGCryptoServiceProvider rng = new RNGCryptoServiceProvider())
        {
            rng.GetBytes(randomBytes);
        }

        return randomBytes;
    }

вызывает

    IContentKey key = CreateEnvelopeTypeContentKey(encryptedsset);



## <a id="common_contentkey"></a>Создание ContentKey общего типа
Hello следующий фрагмент кода создает ключ контента для общего типа шифрования hello. Затем он связывает hello ключ с указанным ресурсом hello.

    static public IContentKey CreateCommonTypeContentKey(IAsset asset)
    {
        // Create common encryption content key
        Guid keyId = Guid.NewGuid();
        byte[] contentKey = GetRandomBuffer(16);

        IContentKey key = _context.ContentKeys.Create(
                                keyId,
                                contentKey,
                                "ContentKey",
                                ContentKeyType.CommonEncryption);

        // Associate hello key with hello asset.
        asset.ContentKeys.Add(key);

        return key;
    }

    static private byte[] GetRandomBuffer(int length)
    {
        var returnValue = new byte[length];

        using (var rng =
            new System.Security.Cryptography.RNGCryptoServiceProvider())
        {
            rng.GetBytes(returnValue);
        }

        return returnValue;
    }
вызывает

    IContentKey key = CreateCommonTypeContentKey(encryptedsset); 


## <a name="media-services-learning-paths"></a>Схемы обучения работе со службами мультимедиа
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Отзывы
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

