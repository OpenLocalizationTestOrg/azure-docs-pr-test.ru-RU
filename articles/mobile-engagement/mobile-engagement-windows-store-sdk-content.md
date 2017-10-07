---
title: "aaaWindows содержимое пакета SDK для универсальных приложений"
description: "Дополнительные сведения о hello содержимое пакета SDK универсальных приложений Windows hello для Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 8fa1b701-1c2b-4aec-940c-06c974ef5405
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: a8013d2433c0be62d737c8bc6e8360ed79bbe532
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="windows-universal-apps-sdk-content"></a>Содержимое пакета SDK для универсальных приложений для Windows
В этом документе перечислены и описаны hello содержимого, развернутого с hello SDK в приложении.

## <a name="hello-resources-folder"></a>Hello `/Resources` папки
Эта папка содержит все hello ресурсы, необходимые для мобильного охвата. Также можно настроить их toofit приложения.

* `EngagementConfiguration.xml`: hello файла конфигурации мобильного охвата, это настройки параметров мобильного охвата (строка подключения мобильного охвата, сбой отчет...).

### <a name="html-folder"></a>Папка /html
* `EngagementNotification.html`: hello `Notification` веб-представлении конструктора html для ленты в приложении.
* `EngagementAnnouncement.html`: hello `Announcement` веб-представление конструктора html для представления interstitial в приложении.

### <a name="images-folder"></a>Папка /images
* `EngagementIconNotification.png`: hello фирменной символики значка, отображаемого в hello слева уведомления — заменить этот значок вашей торговой марки.
* `EngagementIconOk.png`: hello `Ok` значок hello reach содержимого страниц для кнопки действия или проверки hello.
* `EngagementIconNOK.png`: hello `NOK` значок, используемый при отключении кнопка проверки hello hello reach содержимого страниц.
* `EngagementIconClose.png`: hello `Close` значок hello достичь уведомления и содержимое для hello пропустить кнопки.

### <a name="overlay-folder"></a>Папка /overlay
* `EngagementPageOverlay.cs`: hello наложения страницы должен добавлять hello Engagement reach дочерних tooits пользовательского интерфейса в приложении.

