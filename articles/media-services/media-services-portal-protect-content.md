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
# <a name="configuring-content-protection-policies-using-hello-azure-portal"></a>Настройка политик защиты содержимого с помощью портала Azure hello
> [!NOTE]
> toocomplete этого учебника необходима учетная запись Azure. Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/).
> 
> 

## <a name="overview"></a>Обзор
Службы мультимедиа Microsoft Azure (AMS) позволяет вам toosecure мультимедиа из hello раз, когда он покидает вашему компьютеру посредством хранения, обработки и доставки. Media Services позволяет toodeliver содержимого зашифрованы динамически с помощью Advanced Encryption Standard (AES) (с помощью 128-битные ключи шифрования), общее шифрование (CENC) с помощью PlayReady и/или Widevine DRM Apple FairPlay. 

AMS предоставляет услугу для доставки лицензий DRM и очистки клиентов tooauthorized ключей AES. Hello Azure портал позволяет toocreate один **политики авторизации ключа лицензии** для всех типов шифрования.

В этой статье показано, как tooconfigure содержимого политики защиты с hello портал Azure. Hello статьи также показано как активы tooyour tooapply динамического шифрования.


> [!NOTE]
> При использовании политики защиты hello Azure классического портала toocreate hello политики не может использоваться в hello [портал Azure](https://portal.azure.com/). Тем не менее, все hello старого политик по-прежнему существует. Их можно проверить с помощью hello Azure Media Services .NET SDK или hello [-мультимедиа-обозреватель служб Azure](https://github.com/Azure/Azure-Media-Services-Explorer/releases) средства (toosee hello политики, щелкните правой кнопкой мыши в активе hello -> отображения информации (F4) -> щелкните здесь ключей контента, вкладка "->" Щелкните ключ hello). 
> 
> Если вы хотите tooencrypt ресурсом, используя новые политики, hello портал Azure, настройте, нажмите кнопку Сохранить и заново динамического шифрования. 
> 
> 

## <a name="start-configuring-content-protection"></a>Начало настройки защиты содержимого
toouse hello портала toostart настройки защиты содержимого, учетная запись глобального tooyour AMS, hello следующие:

1. В hello [портал Azure](https://portal.azure.com/), выберите учетную запись служб мультимедиа Azure.
2. Выберите **Параметры** > **Защита контента**.

![Защита содержимого](./media/media-services-portal-content-protection/media-services-content-protection001.png)

## <a name="keylicense-authorization-policy"></a>политику авторизации ключей и лицензий
Службы AMS поддерживают несколько способов аутентификации пользователей, запрашивающих ключи или лицензии. политики авторизации ключа контента Hello должно быть настроена вами и ваш клиент, чтобы клиент delived toohello toobe ключ/лицензии hello. Hello политики авторизации ключа контента может иметь одно или несколько ограничений авторизации: **откройте** или **маркера** ограниченного использования программ.

Hello Azure портал позволяет toocreate один **политики авторизации ключа лицензии** для всех типов шифрования.

### <a name="open"></a>Открыть
Ограничение Open означает, что система hello будет предоставлять tooanyone ключа hello, выполняющий запрос ключа. Это ограничение подходит для тестирования. 

### <a name="token"></a>Маркер
политика с ограничением токенов Hello должны сопровождаться маркера, выданного по токенов безопасности службы (STS). Службы мультимедиа поддерживают только токены в формате JSON Web Token (JWT) и формат hello простой веб-токены (SWT). Службы мультимедиа не предоставляют службы маркеров безопасности. Можно создать настраиваемую STS или использовать токены tooissue Microsoft Azure ACS. Hello STS должна быть настроенный toocreate токен, подписанным с hello указанный ключ и выдачи утверждений, которые указаны в конфигурации ограничения токенов hello. Службы мультимедиа Hello службы доставки ключей, то возвращается hello запрошенную ключей (или лицензий) клиента toohello, если токен hello действителен и hello утверждений в hello маркера соответствует настроенным ключей hello (или лицензий).

При настройке политики с ограничением токенов hello, необходимо указать hello основной ключ проверки, издателя и аудитории параметров. Hello основной ключ проверки содержит hello ключа, что был подписан токен hello, издателем является hello службой маркеров безопасности, выдает маркер hello. аудитория Hello (иногда называется область) описывает намерение hello hello маркера или hello ресурсов hello токен разрешает доступ. Hello служба доставки ключей Media Services проверяет, эти значения в токене hello соответствуют значениям hello в шаблоне hello.

![Защита содержимого](./media/media-services-portal-content-protection/media-services-content-protection002.png)

## <a name="playready-rights-template"></a>Шаблон прав PlayReady
Подробные сведения о шаблон прав hello PlayReady см. в разделе [Обзор шаблона лицензий PlayReady служб мультимедиа](media-services-playready-license-template-overview.md).

### <a name="non-persistent"></a>Временный
При настройке лицензии как непостоянные только удерживается в памяти пока игрок hello использует hello лицензии.  

![Защита содержимого](./media/media-services-portal-content-protection/media-services-content-protection003.png)

### <a name="persistent"></a>Постоянный
Если настроить лицензии hello как постоянные, он будет сохранен в постоянном хранилище на приветствия клиента.

![Защита содержимого](./media/media-services-portal-content-protection/media-services-content-protection004.png)

## <a name="widevine-rights-template"></a>Шаблон прав Widevine
Подробные сведения о шаблоне права Widevine hello. в разделе [Обзор шаблона лицензий Widevine](media-services-widevine-license-template-overview.md).

### <a name="basic"></a>Basic
При выборе **основные**, hello шаблон будет создан со всеми значениями по умолчанию.

### <a name="advanced"></a>Расширенная
Подробное описание параметра "Дополнительно" в настройках Widevine см. в [этой статье](media-services-widevine-license-template-overview.md).

![Защита содержимого](./media/media-services-portal-content-protection/media-services-content-protection005.png)

## <a name="fairplay-configuration"></a>Настройка FairPlay
tooenable FairPlay шифрования, необходимо tooprovide hello сертификат приложения и секретный ключ приложения (ASK) через параметр конфигурации FairPlay hello. Подробные сведения о настройке и требованиях FairPlay см. в [этой статье](media-services-protect-hls-with-fairplay.md).

![Защита содержимого](./media/media-services-portal-content-protection/media-services-content-protection006.png)

## <a name="apply-dynamic-encryption-tooyour-asset"></a>Применение динамического шифрования tooyour активов
преимущества tootake динамического шифрования требуется tooencode файла исходного кода в набор файлов MP4 с адаптивной скоростью.

### <a name="select-an-asset-that-you-want-tooencrypt"></a>Выберите ресурс, которые должны tooencrypt
Выберите все ресурсы, toosee **параметры** > **активы**.

![Защита содержимого](./media/media-services-portal-content-protection/media-services-content-protection007.png)

### <a name="encrypt-with-aes-or-drm"></a>Шифрование с помощью AES или DRM
При нажатии кнопки **Зашифровать** появятся два варианта: **AES** или **DRM**. 

#### <a name="aes"></a>AES
Шифрование с помощью открытого ключа AES будет включено для всех протоколов потоковой передачи: Smooth Streaming, HLS и MPEG-DASH.

![Защита содержимого](./media/media-services-portal-content-protection/media-services-content-protection008.png)

#### <a name="drm"></a>DRM
При выборе вкладки DRM hello, представлены различные варианты политики защиты содержимого (что необходимо настроить моменту) + набор потоковых протоколов.

* **PlayReady and Widevine with MPEG-DASH** (PlayReady и Widevine с MPEG-DASH): будет динамически шифровать поток MPEG-DASH, используя системы DRM PlayReady и Widevine.
* **PlayReady and Widevine with MPEG-DASH + FairPlay with HLS** (PlayReady и Widevine с MPEG-DASH + FairPlay с HLS): будет динамически шифровать поток MPEG-DASH, используя системы DRM PlayReady и Widevine. Также будет шифровать потоки HLS, используя FairPlay.
* **PlayReady only with Smooth Streaming, HLS and MPEG-DASH** (PlayReady только с Smooth Streaming, HLS и MPEG-DASH): будет динамически шифровать потоки Smooth Streaming, HLS и MPEG-DASH, используя систему DRM PlayReady.
* **Widevine only with MPEG-DASH** (Widevine только с MPEG-DASH): будет динамически шифровать поток MPEG-DASH, используя систему DRM Widevine.
* **FairPlay only with HLS** (FairPlay только с HLS): будет динамически шифровать поток HLS, используя FairPlay.

tooenable FairPlay шифрования, необходимо tooprovide hello сертификат приложения и секретный ключ приложения (ASK) через hello параметр конфигурации FairPlay hello колонку параметров защиты содержимого.

![Защита содержимого](./media/media-services-portal-content-protection/media-services-content-protection009.png)

После выбора hello шифрования клавишу **применить**.

>[!NOTE] 
>При планировании tooplay AES шифрования HLS в Safari см. в разделе [этот блог](https://azure.microsoft.com/blog/how-to-make-token-authorized-aes-encrypted-hls-stream-working-in-safari/).

## <a name="next-steps"></a>Дальнейшие действия
Просмотрите схемы обучения работе со службами мультимедиа.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Отзывы
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

