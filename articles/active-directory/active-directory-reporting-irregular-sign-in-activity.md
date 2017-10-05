---
title: "Нестандартные действия при входе"
description: "В этом отчете содержится информация об операциях входа, которые алгоритмы машинного обучения идентифицировали как аномальные."
services: active-directory
documentationcenter: 
author: SSalahAhmed
manager: gchander
editor: 
ms.assetid: a5a270a9-a0eb-4a99-b04c-ccde3829ffe4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/04/2016
ms.author: saah;kenhoff
ms.openlocfilehash: 565321b6f3ad5988f383a701cb9d8bd5c9937795
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="irregular-sign-in-activity"></a>Нестандартные действия при входе
Нестандартные входы — это входы, которые определяет алгоритм машинного обучения, исходя из невозможности путешествия, а также аномального расположения входа и устройства, используемого для входа. Это может означать, что в эту учетную запись успешно вошел хакер.
В случае возникновения 10 или более аномальных событий входа в течение периода до 30 дней мы отправим уведомление по почте глобальным администраторам. Обязательно включите адрес aad-alerts-noreply@mail.windowsazure.com в список надежных отправителей.

