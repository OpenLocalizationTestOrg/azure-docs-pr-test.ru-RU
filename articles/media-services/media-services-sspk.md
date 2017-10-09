---
title: "Microsoft® Smooth Streaming Client Porting Kit aaaLicensing"
description: "Дополнительные сведения о том, как toolicensing hello Microsoft® Smooth Streaming Client Porting Kit."
services: media-services
documentationcenter: 
author: xpouyat
manager: cfowler
editor: 
ms.assetid: e3b488e7-8428-4c10-a072-eb3af46c82ad
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: xpouyat
ms.openlocfilehash: 56c3dccda73dd02207bb4dbe8109ba6fda917a6b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="licensing-microsoft-smooth-streaming-client-porting-kit"></a>Лицензирование пакета для портирования клиента бесперебойной потоковой передачи Microsoft® Smooth Streaming
## <a name="overview"></a>Обзор
Microsoft Smooth Streaming Client Porting Kit (**SSPK** сокращенно) является реализация клиента Smooth Streaming оптимизированного toohelp внедренных производителя устройства, кабелей и операторам мобильной связи, поставщикам служб контента, переносные Изготовители, независимые поставщики (ISV) и решение поставщики toocreate продуктов и служб для адаптивной потоковой передачи содержимого в формат Smooth Streaming. SSPK — устройств и платформ независимых реализация клиента Smooth Streaming, который может быть перенесена с hello Лицензиат tooany устройств и платформ. 

Ниже приведены высокоуровневая архитектура и поле IIS Smooth Streaming Porting Kit реализации Smooth Streaming Client hello, предоставляемых корпорацией Майкрософт и включает в себя все hello основную логику для воспроизведения содержимого Smooth Streaming. Партнеры затем портируют его на конкретное устройство или платформу, создавая соответствующие интерфейсы. 

![SSPK](./media/media-services-sspk/sspk-arch.png)

## <a name="description"></a>Описание
Условия лицензирования SSPK повышают коммерческую ценность этого предложения. SSPK лицензия обеспечивает hello отрасли с:

* Исходный код пакета для портирования Smooth Streaming на языке C++, в котором: 
  * реализованы функции клиента Smooth Streaming;
  * добавлены возможности синтаксического и эвристического анализа, логика буферизации и другие функции.
* API-интерфейсы приложения проигрывателя. 
  * Программные интерфейсы для взаимодействия с приложением Проигрывателя мультимедиа.
* Интерфейс слоя платформенных абстракций (PAL). 
  * интерфейсы программирования для взаимодействия с операционной системой hello (потоки, сокеты)
* Интерфейс слоя аппаратных абстракций (HAL). 
  * Программные интерфейсы для взаимодействия с аппаратным оборудованием аудио- и видеодекодеров (декодирование, отрисовка).
* Интерфейс управления цифровыми правами (DRM). 
  * интерфейсы программирования для обработки DRM через hello DRM Abstraction Layer (DAL)
  * Пакет для портирования Microsoft PlayReady поставляется отдельно, но интегрируется через этот интерфейс. Дополнительные сведения о лицензировании устройств Microsoft PlayReady приводятся [здесь](http://www.microsoft.com/playready/licensing/device_technology.mspx#pddipdl).
* Примеры реализации 
  * Пример реализации PAL для Linux
  * Пример реализации HAL для GStreamer

## <a name="licensing-options"></a>Варианты лицензирования
Microsoft Smooth Streaming Client Porting Kit выполняется через два различных соглашения доступны toolicensees: один для разработки Smooth Streaming в промежуточный клиенты, а другой для распространения пользователи tooend Smooth Streaming клиента готовой продукции.

* Для изготовителей микросхем, системных интеграторов или независимые поставщики (ISV), которым требуется перенос кода источника комплект toodevelop продуктов промежуточная Microsoft Smooth Streaming Client Porting Kit **лицензии продукта промежуточная** должны быть выполнены.
* Для производителей и независимые поставщики программного обеспечения, которым требуются права распространения для пользователей tooend Smooth Streaming клиента готовой продукции, hello Microsoft Smooth Streaming Client Porting Kit **лицензии конечного продукта** должны быть выполнены.

### <a name="microsoft-smooth-streaming-client-porting-kit-interim-product-license"></a>Лицензия на промежуточный продукт пакета портирования клиента Microsoft Smooth Streaming.
В рамках данной лицензии Microsoft предлагает Smooth Streaming Client Porting Kit и hello toodevelop необходимые авторских прав и распространять Лицензиаты устройства Smooth Streaming Client Porting Kit для Smooth Streaming в промежуточный клиенты tooother, Распространите Smooth Streaming клиента готовой продукции.

#### <a name="fee-structure"></a>Структура выплат
Сбор разовой лицензии 50 000 долларов предоставляет доступ toohello Smooth Streaming Client Porting Kit. 

### <a name="microsoft-smooth-streaming-client-porting-kit-final-product-license"></a>Лицензия на конечный продукт пакета портирования клиента Microsoft Smooth Streaming.
В рамках данной лицензии Корпорация Майкрософт предлагает все необходимые tooreceive права интеллектуальной собственности Smooth Streaming в промежуточный клиенты из других Smooth Streaming Client Porting Kit Лицензиатов и toodistribute фирменной символикой Smooth Streaming клиента окончательный Пользователи tooend продуктов.

#### <a name="fee-structure"></a>Структура выплат
в разделе авторских отчислений модель, что и в разделе предлагается Hello Smooth Streaming клиента окончательной версии продукта:

* По 0,10 доллара США за каждое отправленное устройство, в котором используется конечный продукт.
* прямые Hello ограничен $ 50 000 каждый год
* Отсутствие отчислений за первые 10 000 устройств в течение каждого года. 

## <a name="licensing-procedure-and-sspk-access"></a>Процедура лицензирования и доступ к SSPK.
Все запросы на лицензирование отправляйте по электронной почте на адрес [sspkinfo@microsoft.com](mailto:sspkinfo@microsoft.com) .

Hello [SSPK распространения портала](https://microsoft.sharepoint.com/teams/SSPKDOWNLOAD/) — доступны tooregistered промежуточная Лицензиаты.

Промежуточные и окончательный SSPK Лицензиаты могут отправлять технические вопросы слишком[smoothpk@microsoft.com](mailto:smoothpk@microsoft.com).

## <a name="microsoft-smooth-streaming-client-interim-product-agreement-licensees"></a>Обладатели лицензий на промежуточный продукт пакета для портирования клиента Microsoft Smooth Streaming.
* Adroit Business Solutions, Inc
* Advanced Digital Broadcast SA
* AirTies Kablosuz Iletism Sanayive Dis Ticaret A.S.
* Albis Technologies Ltd.
* Alticast Corporation
* Amazon Digital Services, Inc.
* Arion Technology, Inc.
* AVC Multimedia Software Co., Ltd.
* Cavium, Inc.
* EchoStar Purchasing Corporation
* Enseo, Inc.
* Fluendo S.A.
* HANDAN BroadInfoCom Co., Ltd.
* Infomir GMBH
* Irdeto USA Inc.
* iWEDIA S.A. 
* Liberty Global Services BV
* MediaTek Inc.
* MStar Co, Ltd
* Nintendo Co., Ltd.
* OpenTV, Inc.
* Saffron Digital Limited
* Sichuan Changhong Electric Co., Ltd
* SoftAtHome
* Sony Corporation
* Tatung Technology Inc.
* TCL Technoly Electronics (Huizhou) Co., Ltd.
* Top Victory Investments, Ltd.
* Vestel Elektronik Sanayi ve Ticaret A.S.
* VisualOn, Inc.
* ZTE Corporation

## <a name="microsoft-smooth-streaming-client-final-product-agreement-licensees"></a>Обладатели лицензий на конечный продукт пакета для портирования клиента Microsoft Smooth Streaming
* Advanced Digital Broadcast SA
* AirTies Kablosuz Iletism Sanayive Dis Ticaret A.S.
* Albis Technologies Ltd.
* Amazon Digital Services, Inc.
* AmTRAN Technology Co., Ltd.
* Arcadyan Technology Corporation
* Arion Technology, Inc.
* ATMACA ELEKTRONİK SAN. VE TİC. A.Ş
* British Sky Broadcasting Limited
* CastPal Technology Inc., Shenzhen
* Compal Electronics, Inc.
* Dongguan Digital AV Technology Corp., Ltd.
* EchoStar Purchasing Corporation
* Enseo, Inc.
* Filmflex Movies Limited
* Fluendo S.A.
* Gibson Innovations Limited
* Haier Information Applicantion S.R.L
* HANDAN BroadInfoCom Co., Ltd.
* Hisense International Co., Ltd. 
* Homecast Co.,Ltd
* Hon Hai Precision Industry Co., Ltd.
* Infomir GMBH
* Kaonmedia Co., Ltd.
* KDDI Corporation
* Nintendo Co., Ltd.
* Orange SA
* Saffron Digital Limited
* Sagemcom Broadband SAS
* Shenzhen Coship Electronics CO., LTD
* Shenzhen Jiuzhou Electric Co.,Ltd
* Shenzhen Skyworth Digital Technology Co., Ltd
* Sichuan Changhong Electric Co., Ltd.
* Skardin Industrial Corp.
* Sky Deutschland Fernsehen GmbH & Co. KG
* SmarDTV S.A.
* SoftAtHome
* Sony Corporation
* TCL Overseas Marketing (Macao Commercial Offshore) Limited
* Technicolor Delivery Technologies, SAS
* Tongfang Global Ltd.
* Top Victory Investments, Ltd.
* Toshiba Lifestyle Products & Services Corporation
* Universal Media Corporation /Slovakia/ s.r.o.
* VIZIO, Inc.
* Wistron Corporation
* ZTE Corporation


## <a name="media-services-learning-paths"></a>Схемы обучения работе со службами мультимедиа
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Отзывы
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

