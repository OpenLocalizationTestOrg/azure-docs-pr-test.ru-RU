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
# <a name="create-contentkeys-with-net"></a><span data-ttu-id="2f9cd-103">Создание ContentKey с использованием .NET</span><span class="sxs-lookup"><span data-stu-id="2f9cd-103">Create ContentKeys with .NET</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2f9cd-104">REST</span><span class="sxs-lookup"><span data-stu-id="2f9cd-104">REST</span></span>](media-services-rest-create-contentkey.md)
> * [<span data-ttu-id="2f9cd-105">.NET</span><span class="sxs-lookup"><span data-stu-id="2f9cd-105">.NET</span></span>](media-services-dotnet-create-contentkey.md)
> 
> 

<span data-ttu-id="2f9cd-106">Media Services позволяет toocreate и доставка зашифрованные активы.</span><span class="sxs-lookup"><span data-stu-id="2f9cd-106">Media Services enables you toocreate and deliver encrypted assets.</span></span> <span data-ttu-id="2f9cd-107">Объект **ContentKey** обеспечивает безопасный доступ tooyour **активов**s.</span><span class="sxs-lookup"><span data-stu-id="2f9cd-107">A **ContentKey** provides secure access tooyour **Asset**s.</span></span> 

<span data-ttu-id="2f9cd-108">При создании нового средства (например, прежде чем [передачи файлов](media-services-dotnet-upload-files.md)), можно указать следующие параметры шифрования hello: **StorageEncrypted**, **CommonEncryptionProtected**, или **EnvelopeEncryptionProtected**.</span><span class="sxs-lookup"><span data-stu-id="2f9cd-108">When you create a new asset (for example, before you [upload files](media-services-dotnet-upload-files.md)), you can specify hello following encryption options: **StorageEncrypted**, **CommonEncryptionProtected**, or **EnvelopeEncryptionProtected**.</span></span> 

<span data-ttu-id="2f9cd-109">После доставки активов tooyour клиентов, вы можете [настройки для средств toobe динамически зашифрованные](media-services-dotnet-configure-asset-delivery-policy.md) с одним hello, следующие два шифрования: **DynamicEnvelopeEncryption** или  **DynamicCommonEncryption**.</span><span class="sxs-lookup"><span data-stu-id="2f9cd-109">When you deliver assets tooyour clients, you can [configure for assets toobe dynamically encrypted](media-services-dotnet-configure-asset-delivery-policy.md) with one of hello following two encryptions: **DynamicEnvelopeEncryption** or **DynamicCommonEncryption**.</span></span>

<span data-ttu-id="2f9cd-110">Зашифрованные активы имеют связанные с toobe **ContentKey**s.</span><span class="sxs-lookup"><span data-stu-id="2f9cd-110">Encrypted assets have toobe associated with **ContentKey**s.</span></span> <span data-ttu-id="2f9cd-111">В этой статье описывается как toocreate ключа содержимого.</span><span class="sxs-lookup"><span data-stu-id="2f9cd-111">This article describes how toocreate a content key.</span></span>

> [!NOTE]
> <span data-ttu-id="2f9cd-112">При создании нового **StorageEncrypted** активов с помощью hello Media Services .NET SDK hello **ContentKey** автоматически создается и связанный с активом hello.</span><span class="sxs-lookup"><span data-stu-id="2f9cd-112">When creating a new **StorageEncrypted** asset using hello Media Services .NET SDK , hello **ContentKey** is automatically created and linked with hello asset.</span></span>
> 
> 

## <a name="contentkeytype"></a><span data-ttu-id="2f9cd-113">ContentKeyType</span><span class="sxs-lookup"><span data-stu-id="2f9cd-113">ContentKeyType</span></span>
<span data-ttu-id="2f9cd-114">Одно из значений hello, необходимо задать при создании содержимого ключ является тип ключа контента hello.</span><span class="sxs-lookup"><span data-stu-id="2f9cd-114">One of hello values that you must set when create a content key is hello content key type.</span></span> <span data-ttu-id="2f9cd-115">Выберите один из hello следующие значения.</span><span class="sxs-lookup"><span data-stu-id="2f9cd-115">Choose from one of hello following values.</span></span> 

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

## <span data-ttu-id="2f9cd-116"><a id="envelope_contentkey"></a>Создание ContentKey конвертного типа</span><span class="sxs-lookup"><span data-stu-id="2f9cd-116"><a id="envelope_contentkey"></a>Create envelope type ContentKey</span></span>
<span data-ttu-id="2f9cd-117">Hello следующий фрагмент кода создает ключ содержимого для типа шифрования конвертов hello.</span><span class="sxs-lookup"><span data-stu-id="2f9cd-117">hello following code snippet creates a content key of hello envelope encryption type.</span></span> <span data-ttu-id="2f9cd-118">Затем он связывает hello ключ с указанным ресурсом hello.</span><span class="sxs-lookup"><span data-stu-id="2f9cd-118">It then associates hello key with hello specified asset.</span></span>

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

<span data-ttu-id="2f9cd-119">вызывает</span><span class="sxs-lookup"><span data-stu-id="2f9cd-119">call</span></span>

    IContentKey key = CreateEnvelopeTypeContentKey(encryptedsset);



## <span data-ttu-id="2f9cd-120"><a id="common_contentkey"></a>Создание ContentKey общего типа</span><span class="sxs-lookup"><span data-stu-id="2f9cd-120"><a id="common_contentkey"></a>Create common type ContentKey</span></span>
<span data-ttu-id="2f9cd-121">Hello следующий фрагмент кода создает ключ контента для общего типа шифрования hello.</span><span class="sxs-lookup"><span data-stu-id="2f9cd-121">hello following code snippet creates a content key of hello common encryption type.</span></span> <span data-ttu-id="2f9cd-122">Затем он связывает hello ключ с указанным ресурсом hello.</span><span class="sxs-lookup"><span data-stu-id="2f9cd-122">It then associates hello key with hello specified asset.</span></span>

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
<span data-ttu-id="2f9cd-123">вызывает</span><span class="sxs-lookup"><span data-stu-id="2f9cd-123">call</span></span>

    IContentKey key = CreateCommonTypeContentKey(encryptedsset); 


## <a name="media-services-learning-paths"></a><span data-ttu-id="2f9cd-124">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="2f9cd-124">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="2f9cd-125">Отзывы</span><span class="sxs-lookup"><span data-stu-id="2f9cd-125">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

