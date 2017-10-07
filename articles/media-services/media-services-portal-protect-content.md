---
title: "с помощью политик защиты содержимого aaaConfiguring hello портал Azure | Документы Microsoft"
description: "В этой статье показано, как toouse hello Azure портала tooconfigure политики защиты содержимого. Hello статьи также показан способ динамического шифрования tooenable средств."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 270b3272-7411-40a9-ad42-5acdbba31154
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: juliako
ms.openlocfilehash: 3e7ce6ddaa0e738b5a1e26dafe9eef2df221f039
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-content-protection-policies-using-hello-azure-portal"></a><span data-ttu-id="c2e5b-104">Настройка политик защиты содержимого с помощью портала Azure hello</span><span class="sxs-lookup"><span data-stu-id="c2e5b-104">Configuring content protection policies using hello Azure portal</span></span>
> [!NOTE]
> <span data-ttu-id="c2e5b-105">toocomplete этого учебника необходима учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="c2e5b-105">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="c2e5b-106">Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c2e5b-106">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
> 
> 

## <a name="overview"></a><span data-ttu-id="c2e5b-107">Обзор</span><span class="sxs-lookup"><span data-stu-id="c2e5b-107">Overview</span></span>
<span data-ttu-id="c2e5b-108">Службы мультимедиа Microsoft Azure (AMS) позволяет вам toosecure мультимедиа из hello раз, когда он покидает вашему компьютеру посредством хранения, обработки и доставки.</span><span class="sxs-lookup"><span data-stu-id="c2e5b-108">Microsoft Azure Media Services (AMS) enables you toosecure your media from hello time it leaves your computer through storage, processing, and delivery.</span></span> <span data-ttu-id="c2e5b-109">Media Services позволяет toodeliver содержимого зашифрованы динамически с помощью Advanced Encryption Standard (AES) (с помощью 128-битные ключи шифрования), общее шифрование (CENC) с помощью PlayReady и/или Widevine DRM Apple FairPlay.</span><span class="sxs-lookup"><span data-stu-id="c2e5b-109">Media Services allows you toodeliver your content encrypted dynamically with Advanced Encryption Standard (AES) (using 128-bit encryption keys), common encryption (CENC) using PlayReady and/or Widevine DRM, and Apple FairPlay.</span></span> 

<span data-ttu-id="c2e5b-110">AMS предоставляет услугу для доставки лицензий DRM и очистки клиентов tooauthorized ключей AES.</span><span class="sxs-lookup"><span data-stu-id="c2e5b-110">AMS provides a service for delivering DRM licenses and AES clear keys tooauthorized clients.</span></span> <span data-ttu-id="c2e5b-111">Hello Azure портал позволяет toocreate один **политики авторизации ключа лицензии** для всех типов шифрования.</span><span class="sxs-lookup"><span data-stu-id="c2e5b-111">hello Azure portal enables you toocreate one **key/license authorization policy** for all types of encryptions.</span></span>

<span data-ttu-id="c2e5b-112">В этой статье показано, как tooconfigure содержимого политики защиты с hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="c2e5b-112">This article demonstrates how tooconfigure content protection policies with hello Azure portal.</span></span> <span data-ttu-id="c2e5b-113">Hello статьи также показано как активы tooyour tooapply динамического шифрования.</span><span class="sxs-lookup"><span data-stu-id="c2e5b-113">hello article also shows how tooapply dynamic encryption tooyour assets.</span></span>


> [!NOTE]
> <span data-ttu-id="c2e5b-114">При использовании политики защиты hello Azure классического портала toocreate hello политики не может использоваться в hello [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="c2e5b-114">If you used hello Azure classic portal toocreate protection policies, hello policies may not appear in hello [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="c2e5b-115">Тем не менее, все hello старого политик по-прежнему существует.</span><span class="sxs-lookup"><span data-stu-id="c2e5b-115">However, all hello old polices still exist.</span></span> <span data-ttu-id="c2e5b-116">Их можно проверить с помощью hello Azure Media Services .NET SDK или hello [-мультимедиа-обозреватель служб Azure](https://github.com/Azure/Azure-Media-Services-Explorer/releases) средства (toosee hello политики, щелкните правой кнопкой мыши в активе hello -> отображения информации (F4) -> щелкните здесь ключей контента, вкладка "->" Щелкните ключ hello).</span><span class="sxs-lookup"><span data-stu-id="c2e5b-116">You can examine them using hello Azure Media Services .NET SDK or hello [Azure-Media-Services-Explorer](https://github.com/Azure/Azure-Media-Services-Explorer/releases) tool (toosee hello policies, right-click on hello asset -> Display information (F4)->click on Content keys tab-> click on hello key).</span></span> 
> 
> <span data-ttu-id="c2e5b-117">Если вы хотите tooencrypt ресурсом, используя новые политики, hello портал Azure, настройте, нажмите кнопку Сохранить и заново динамического шифрования.</span><span class="sxs-lookup"><span data-stu-id="c2e5b-117">If you want tooencrypt your asset using new policies, configure them with hello Azure portal, click save, and reapply dynamic encryption.</span></span> 
> 
> 

## <a name="start-configuring-content-protection"></a><span data-ttu-id="c2e5b-118">Начало настройки защиты содержимого</span><span class="sxs-lookup"><span data-stu-id="c2e5b-118">Start configuring content protection</span></span>
<span data-ttu-id="c2e5b-119">toouse hello портала toostart настройки защиты содержимого, учетная запись глобального tooyour AMS, hello следующие:</span><span class="sxs-lookup"><span data-stu-id="c2e5b-119">toouse hello portal toostart configuring content protection, global tooyour AMS account, do hello following:</span></span>

1. <span data-ttu-id="c2e5b-120">В hello [портал Azure](https://portal.azure.com/), выберите учетную запись служб мультимедиа Azure.</span><span class="sxs-lookup"><span data-stu-id="c2e5b-120">In hello [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="c2e5b-121">Выберите **Параметры** > **Защита контента**.</span><span class="sxs-lookup"><span data-stu-id="c2e5b-121">Select **Settings** > **Content protection**.</span></span>

![Защита содержимого](./media/media-services-portal-content-protection/media-services-content-protection001.png)

## <a name="keylicense-authorization-policy"></a><span data-ttu-id="c2e5b-123">политику авторизации ключей и лицензий</span><span class="sxs-lookup"><span data-stu-id="c2e5b-123">Key/license authorization policy</span></span>
<span data-ttu-id="c2e5b-124">Службы AMS поддерживают несколько способов аутентификации пользователей, запрашивающих ключи или лицензии.</span><span class="sxs-lookup"><span data-stu-id="c2e5b-124">AMS supports multiple ways of authenticating users who make key or license requests.</span></span> <span data-ttu-id="c2e5b-125">политики авторизации ключа контента Hello должно быть настроена вами и ваш клиент, чтобы клиент delived toohello toobe ключ/лицензии hello.</span><span class="sxs-lookup"><span data-stu-id="c2e5b-125">hello content key authorization policy must be configured by you and met by your client in order for hello key/license toobe delived toohello client.</span></span> <span data-ttu-id="c2e5b-126">Hello политики авторизации ключа контента может иметь одно или несколько ограничений авторизации: **откройте** или **маркера** ограниченного использования программ.</span><span class="sxs-lookup"><span data-stu-id="c2e5b-126">hello content key authorization policy could have one or more authorization restrictions: **open** or **token** restriction.</span></span>

<span data-ttu-id="c2e5b-127">Hello Azure портал позволяет toocreate один **политики авторизации ключа лицензии** для всех типов шифрования.</span><span class="sxs-lookup"><span data-stu-id="c2e5b-127">hello Azure portal enables you toocreate one **key/license authorization policy** for all types of encryptions.</span></span>

### <a name="open"></a><span data-ttu-id="c2e5b-128">Открыть</span><span class="sxs-lookup"><span data-stu-id="c2e5b-128">Open</span></span>
<span data-ttu-id="c2e5b-129">Ограничение Open означает, что система hello будет предоставлять tooanyone ключа hello, выполняющий запрос ключа.</span><span class="sxs-lookup"><span data-stu-id="c2e5b-129">Open restriction means that hello system will deliver hello key tooanyone who makes a key request.</span></span> <span data-ttu-id="c2e5b-130">Это ограничение подходит для тестирования.</span><span class="sxs-lookup"><span data-stu-id="c2e5b-130">This restriction might be useful for test purposes.</span></span> 

### <a name="token"></a><span data-ttu-id="c2e5b-131">Маркер</span><span class="sxs-lookup"><span data-stu-id="c2e5b-131">Token</span></span>
<span data-ttu-id="c2e5b-132">политика с ограничением токенов Hello должны сопровождаться маркера, выданного по токенов безопасности службы (STS).</span><span class="sxs-lookup"><span data-stu-id="c2e5b-132">hello token restricted policy must be accompanied by a token issued by a Secure Token Service (STS).</span></span> <span data-ttu-id="c2e5b-133">Службы мультимедиа поддерживают только токены в формате JSON Web Token (JWT) и формат hello простой веб-токены (SWT).</span><span class="sxs-lookup"><span data-stu-id="c2e5b-133">Media Services supports tokens in hello Simple Web Tokens (SWT) format and JSON Web Token (JWT) format.</span></span> <span data-ttu-id="c2e5b-134">Службы мультимедиа не предоставляют службы маркеров безопасности.</span><span class="sxs-lookup"><span data-stu-id="c2e5b-134">Media Services does not provide Secure Token Services.</span></span> <span data-ttu-id="c2e5b-135">Можно создать настраиваемую STS или использовать токены tooissue Microsoft Azure ACS.</span><span class="sxs-lookup"><span data-stu-id="c2e5b-135">You can create a custom STS or leverage Microsoft Azure ACS tooissue tokens.</span></span> <span data-ttu-id="c2e5b-136">Hello STS должна быть настроенный toocreate токен, подписанным с hello указанный ключ и выдачи утверждений, которые указаны в конфигурации ограничения токенов hello.</span><span class="sxs-lookup"><span data-stu-id="c2e5b-136">hello STS must be configured toocreate a token signed with hello specified key and issue claims that you specified in hello token restriction configuration.</span></span> <span data-ttu-id="c2e5b-137">Службы мультимедиа Hello службы доставки ключей, то возвращается hello запрошенную ключей (или лицензий) клиента toohello, если токен hello действителен и hello утверждений в hello маркера соответствует настроенным ключей hello (или лицензий).</span><span class="sxs-lookup"><span data-stu-id="c2e5b-137">hello Media Services key delivery service will return hello requested key (or license) toohello client if hello token is valid and hello claims in hello token match those configured for hello key (or license).</span></span>

<span data-ttu-id="c2e5b-138">При настройке политики с ограничением токенов hello, необходимо указать hello основной ключ проверки, издателя и аудитории параметров.</span><span class="sxs-lookup"><span data-stu-id="c2e5b-138">When configuring hello token restricted policy, you must specify hello primary verification key, issuer, and audience parameters.</span></span> <span data-ttu-id="c2e5b-139">Hello основной ключ проверки содержит hello ключа, что был подписан токен hello, издателем является hello службой маркеров безопасности, выдает маркер hello.</span><span class="sxs-lookup"><span data-stu-id="c2e5b-139">hello primary verification key contains hello key that hello token was signed with, issuer is hello secure token service that issues hello token.</span></span> <span data-ttu-id="c2e5b-140">аудитория Hello (иногда называется область) описывает намерение hello hello маркера или hello ресурсов hello токен разрешает доступ.</span><span class="sxs-lookup"><span data-stu-id="c2e5b-140">hello audience (sometimes called scope) describes hello intent of hello token or hello resource hello token authorizes access to.</span></span> <span data-ttu-id="c2e5b-141">Hello служба доставки ключей Media Services проверяет, эти значения в токене hello соответствуют значениям hello в шаблоне hello.</span><span class="sxs-lookup"><span data-stu-id="c2e5b-141">hello Media Services key delivery service validates that these values in hello token match hello values in hello template.</span></span>

![Защита содержимого](./media/media-services-portal-content-protection/media-services-content-protection002.png)

## <a name="playready-rights-template"></a><span data-ttu-id="c2e5b-143">Шаблон прав PlayReady</span><span class="sxs-lookup"><span data-stu-id="c2e5b-143">PlayReady rights template</span></span>
<span data-ttu-id="c2e5b-144">Подробные сведения о шаблон прав hello PlayReady см. в разделе [Обзор шаблона лицензий PlayReady служб мультимедиа](media-services-playready-license-template-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c2e5b-144">For detailed information about hello PlayReady rights template, see [Media Services PlayReady License Template Overview](media-services-playready-license-template-overview.md).</span></span>

### <a name="non-persistent"></a><span data-ttu-id="c2e5b-145">Временный</span><span class="sxs-lookup"><span data-stu-id="c2e5b-145">Non persistent</span></span>
<span data-ttu-id="c2e5b-146">При настройке лицензии как непостоянные только удерживается в памяти пока игрок hello использует hello лицензии.</span><span class="sxs-lookup"><span data-stu-id="c2e5b-146">If you configure license as non-persistent, it is only held in memory while hello player is using hello license.</span></span>  

![Защита содержимого](./media/media-services-portal-content-protection/media-services-content-protection003.png)

### <a name="persistent"></a><span data-ttu-id="c2e5b-148">Постоянный</span><span class="sxs-lookup"><span data-stu-id="c2e5b-148">Persistent</span></span>
<span data-ttu-id="c2e5b-149">Если настроить лицензии hello как постоянные, он будет сохранен в постоянном хранилище на приветствия клиента.</span><span class="sxs-lookup"><span data-stu-id="c2e5b-149">If you configure hello license  as persistent, it is saved in persistent storage on hello client.</span></span>

![Защита содержимого](./media/media-services-portal-content-protection/media-services-content-protection004.png)

## <a name="widevine-rights-template"></a><span data-ttu-id="c2e5b-151">Шаблон прав Widevine</span><span class="sxs-lookup"><span data-stu-id="c2e5b-151">Widevine rights template</span></span>
<span data-ttu-id="c2e5b-152">Подробные сведения о шаблоне права Widevine hello. в разделе [Обзор шаблона лицензий Widevine](media-services-widevine-license-template-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c2e5b-152">For detailed information about hello Widevine rights template, see [Widevine License Template Overview](media-services-widevine-license-template-overview.md).</span></span>

### <a name="basic"></a><span data-ttu-id="c2e5b-153">Basic</span><span class="sxs-lookup"><span data-stu-id="c2e5b-153">Basic</span></span>
<span data-ttu-id="c2e5b-154">При выборе **основные**, hello шаблон будет создан со всеми значениями по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="c2e5b-154">When you select **Basic**, hello template will be created with all defaults values.</span></span>

### <a name="advanced"></a><span data-ttu-id="c2e5b-155">Расширенная</span><span class="sxs-lookup"><span data-stu-id="c2e5b-155">Advanced</span></span>
<span data-ttu-id="c2e5b-156">Подробное описание параметра "Дополнительно" в настройках Widevine см. в [этой статье](media-services-widevine-license-template-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c2e5b-156">For detailed explanation about advance option of Widevine configurations, see [this](media-services-widevine-license-template-overview.md) topic.</span></span>

![Защита содержимого](./media/media-services-portal-content-protection/media-services-content-protection005.png)

## <a name="fairplay-configuration"></a><span data-ttu-id="c2e5b-158">Настройка FairPlay</span><span class="sxs-lookup"><span data-stu-id="c2e5b-158">FairPlay configuration</span></span>
<span data-ttu-id="c2e5b-159">tooenable FairPlay шифрования, необходимо tooprovide hello сертификат приложения и секретный ключ приложения (ASK) через параметр конфигурации FairPlay hello.</span><span class="sxs-lookup"><span data-stu-id="c2e5b-159">tooenable FairPlay encryption, you need tooprovide hello App Certificate and Application Secret Key (ASK) through hello FairPlay Configuration option.</span></span> <span data-ttu-id="c2e5b-160">Подробные сведения о настройке и требованиях FairPlay см. в [этой статье](media-services-protect-hls-with-fairplay.md).</span><span class="sxs-lookup"><span data-stu-id="c2e5b-160">For detailed information about FairPlay configuration and requirements, see [this](media-services-protect-hls-with-fairplay.md) article.</span></span>

![Защита содержимого](./media/media-services-portal-content-protection/media-services-content-protection006.png)

## <a name="apply-dynamic-encryption-tooyour-asset"></a><span data-ttu-id="c2e5b-162">Применение динамического шифрования tooyour активов</span><span class="sxs-lookup"><span data-stu-id="c2e5b-162">Apply dynamic encryption tooyour asset</span></span>
<span data-ttu-id="c2e5b-163">преимущества tootake динамического шифрования требуется tooencode файла исходного кода в набор файлов MP4 с адаптивной скоростью.</span><span class="sxs-lookup"><span data-stu-id="c2e5b-163">tootake advantage of dynamic encryption, you need tooencode your source file into a set of adaptive-bitrate MP4 files.</span></span>

### <a name="select-an-asset-that-you-want-tooencrypt"></a><span data-ttu-id="c2e5b-164">Выберите ресурс, которые должны tooencrypt</span><span class="sxs-lookup"><span data-stu-id="c2e5b-164">Select an asset that you want tooencrypt</span></span>
<span data-ttu-id="c2e5b-165">Выберите все ресурсы, toosee **параметры** > **активы**.</span><span class="sxs-lookup"><span data-stu-id="c2e5b-165">toosee all your assets, select **Settings** > **Assets**.</span></span>

![Защита содержимого](./media/media-services-portal-content-protection/media-services-content-protection007.png)

### <a name="encrypt-with-aes-or-drm"></a><span data-ttu-id="c2e5b-167">Шифрование с помощью AES или DRM</span><span class="sxs-lookup"><span data-stu-id="c2e5b-167">Encrypt with AES or DRM</span></span>
<span data-ttu-id="c2e5b-168">При нажатии кнопки **Зашифровать** появятся два варианта: **AES** или **DRM**.</span><span class="sxs-lookup"><span data-stu-id="c2e5b-168">Once you press **Encrypt** on an asset, you are presented wtih two choices: **AES** or **DRM**.</span></span> 

#### <a name="aes"></a><span data-ttu-id="c2e5b-169">AES</span><span class="sxs-lookup"><span data-stu-id="c2e5b-169">AES</span></span>
<span data-ttu-id="c2e5b-170">Шифрование с помощью открытого ключа AES будет включено для всех протоколов потоковой передачи: Smooth Streaming, HLS и MPEG-DASH.</span><span class="sxs-lookup"><span data-stu-id="c2e5b-170">AES clear key encryption will be enabled on all streaming protocols: Smooth Streaming, HLS, and MPEG-DASH.</span></span>

![Защита содержимого](./media/media-services-portal-content-protection/media-services-content-protection008.png)

#### <a name="drm"></a><span data-ttu-id="c2e5b-172">DRM</span><span class="sxs-lookup"><span data-stu-id="c2e5b-172">DRM</span></span>
<span data-ttu-id="c2e5b-173">При выборе вкладки DRM hello, представлены различные варианты политики защиты содержимого (что необходимо настроить моменту) + набор потоковых протоколов.</span><span class="sxs-lookup"><span data-stu-id="c2e5b-173">When you select hello DRM tab, you are presented with different choices of content protection policies (which you must have configured by now) + a set of streaming protocols.</span></span>

* <span data-ttu-id="c2e5b-174">**PlayReady and Widevine with MPEG-DASH** (PlayReady и Widevine с MPEG-DASH): будет динамически шифровать поток MPEG-DASH, используя системы DRM PlayReady и Widevine.</span><span class="sxs-lookup"><span data-stu-id="c2e5b-174">**PlayReady and Widevine with MPEG-DASH** - will dynamically encrypt your MPEG-DASH stream with PlayReady and Widevine DRMs.</span></span>
* <span data-ttu-id="c2e5b-175">**PlayReady and Widevine with MPEG-DASH + FairPlay with HLS** (PlayReady и Widevine с MPEG-DASH + FairPlay с HLS): будет динамически шифровать поток MPEG-DASH, используя системы DRM PlayReady и Widevine.</span><span class="sxs-lookup"><span data-stu-id="c2e5b-175">**PlayReady and Widevine with MPEG-DASH + FairPlay with HLS** - will dynamically encrypt you MPEG-DASH stream with PlayReady and Widevine DRMs.</span></span> <span data-ttu-id="c2e5b-176">Также будет шифровать потоки HLS, используя FairPlay.</span><span class="sxs-lookup"><span data-stu-id="c2e5b-176">Will also encrypt your HLS streams with FairPlay.</span></span>
* <span data-ttu-id="c2e5b-177">**PlayReady only with Smooth Streaming, HLS and MPEG-DASH** (PlayReady только с Smooth Streaming, HLS и MPEG-DASH): будет динамически шифровать потоки Smooth Streaming, HLS и MPEG-DASH, используя систему DRM PlayReady.</span><span class="sxs-lookup"><span data-stu-id="c2e5b-177">**PlayReady only with Smooth Streaming, HLS and MPEG-DASH** - will dynamically encrypt Smooth Streaming, HLS, MPEG-DASH streams with PlayReady DRM.</span></span>
* <span data-ttu-id="c2e5b-178">**Widevine only with MPEG-DASH** (Widevine только с MPEG-DASH): будет динамически шифровать поток MPEG-DASH, используя систему DRM Widevine.</span><span class="sxs-lookup"><span data-stu-id="c2e5b-178">**Widevine only with MPEG-DASH** - will dynamically encrypt you MPEG-DASH with Widevine DRM.</span></span>
* <span data-ttu-id="c2e5b-179">**FairPlay only with HLS** (FairPlay только с HLS): будет динамически шифровать поток HLS, используя FairPlay.</span><span class="sxs-lookup"><span data-stu-id="c2e5b-179">**FairPlay only with HLS** - will dynamically encrypt your HLS stream with FairPlay.</span></span>

<span data-ttu-id="c2e5b-180">tooenable FairPlay шифрования, необходимо tooprovide hello сертификат приложения и секретный ключ приложения (ASK) через hello параметр конфигурации FairPlay hello колонку параметров защиты содержимого.</span><span class="sxs-lookup"><span data-stu-id="c2e5b-180">tooenable FairPlay encryption, you need tooprovide hello App Certificate and Application Secret Key (ASK) through hello FairPlay Configuration option of hello Content Protection settings blade.</span></span>

![Защита содержимого](./media/media-services-portal-content-protection/media-services-content-protection009.png)

<span data-ttu-id="c2e5b-182">После выбора hello шифрования клавишу **применить**.</span><span class="sxs-lookup"><span data-stu-id="c2e5b-182">Once you make hello encryption selection, press **Apply**.</span></span>

>[!NOTE] 
><span data-ttu-id="c2e5b-183">При планировании tooplay AES шифрования HLS в Safari см. в разделе [этот блог](https://azure.microsoft.com/blog/how-to-make-token-authorized-aes-encrypted-hls-stream-working-in-safari/).</span><span class="sxs-lookup"><span data-stu-id="c2e5b-183">If you are planning tooplay an AES encrypted HLS in Safari, see [this blog](https://azure.microsoft.com/blog/how-to-make-token-authorized-aes-encrypted-hls-stream-working-in-safari/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c2e5b-184">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c2e5b-184">Next steps</span></span>
<span data-ttu-id="c2e5b-185">Просмотрите схемы обучения работе со службами мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="c2e5b-185">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="c2e5b-186">Отзывы</span><span class="sxs-lookup"><span data-stu-id="c2e5b-186">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

