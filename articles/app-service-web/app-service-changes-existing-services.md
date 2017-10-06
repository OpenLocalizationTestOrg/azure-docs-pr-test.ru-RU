---
title: "aaaAzure приложения службы и ее влияние на существующие службы Azure"
description: "Объясняет, как hello новые службы приложений Azure и его возможности повлиять на существующие службы в Azure."
services: app-service
documentationcenter: 
author: yochay
manager: nirma
editor: 
ms.assetid: 86c6a292-3c33-49f4-890c-89cc0321b397
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/12/2016
ms.author: yochaykk
ms.openlocfilehash: a831a88fee38465e5b0b7c2c2340cf8a0d64c864
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-and-existing-azure-services"></a>Служба приложений Azure и существующие службы Azure
В этой статье рассматриваются службы Azure в рамках toobring изменение hello вместе несколько служб Azure в tooexisting изменения hello [службе приложений Azure](https://azure.microsoft.com/services/app-service/), новое предложение интеграции.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="overview"></a>Обзор
[Служба приложений Azure](https://azure.microsoft.com/services/app-service/) — это новыми и уникальными облачная служба, которая позволяет разработчикам toocreate web и мобильных приложений для любых платформ и с любого устройства. Служба приложений — toostreamline интегрированного решения предназначены повторные кодирования функции, интегрировать с enterprise и системой SaaS и автоматизации бизнес-процессов, обеспечивая соответствие требованиям к безопасности, надежность и масштабируемость.

Службы приложений объединяет в себе hello следующие существующие Azure службы - [веб-сайтов](https://azure.microsoft.com/services/websites/), [мобильных служб](https://azure.microsoft.com/services/mobile-services/), и [службы Biztalk](https://azure.microsoft.com/services/biztalk-services/) в одном сочетании службы, во время Добавление новой возможности.  Службы приложений позволяет hello toohost следующие типы приложения:

* Веб-приложения
* Мобильные приложения
* Приложения API
* Logic Apps

Hello следующей таблице объясняется, как существующие Azure службы сопоставления tooApp службы и hello приложения типы, доступные в нем.

<table>
<thead>
<tr class="header">
<th align="left", style="width:10%">Существующая служба Azure</th>
<th align="left", style="width:10%">Служба приложений Azure</th>
<th align="left", style="width:80%">Изменения</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">Веб-сайты Azure</td>
<td align="left">Веб-приложения</td>
<td align="left"><li>Для веб-сайтов Azure службы приложений — строго ограниченный toochanging hello имя веб-сайтов tooWeb приложений.
<p><li>Это касается всех существующих экземпляров веб-сайтов в службе приложений.</p>
<p><li>Можно открыть существующий веб-сайтов через hello <a href="http://go.microsoft.com/fwlink/?LinkId=529715">портала Azure</a>, где вы найдете всех существующих узлов под <em>веб-приложений</em>.</p>
<p><li><em>Веб-план хостинга</em> теперь <em>план служб приложений</em>. <em>План службы приложений</em> может размещать любые типы приложений службы приложений, такие как веб-приложения, мобильные приложения, приложения логики или приложения API.</p>
<p><li>Веб-приложения службы приложений Azure находятся в состоянии общедоступной версии.</p>
<p><li><a href="http://azure.microsoft.com/services/app-service/web/">Дополнительные сведения о веб-приложений</a>.</p></td>
</tr>
<tr class="even">
<td align="left">Мобильные службы Azure</td>
<td align="left">Мобильные приложения</td>
<td align="left"><p><li>Мобильные службы продолжить toobe доступен в качестве автономной службы и остаются полностью поддерживается.</p>
<p><li>Мобильные приложения — это тип приложения в службе приложений, который интегрирует все функции hello мобильных служб и многое другое.</p>
<p><li>Можно легко слишком<a href="http://go.microsoft.com/fwlink/?LinkID=724279&clcid=0x409">миграции из мобильных служб tooMobile приложения</a>.</p>
<p><li>В составе службы приложений мобильные приложения получили новые возможности за рамками мобильных служб, такие как интеграция с локальной системой и системой SaaS, промежуточные слоты, веб-задания, улучшенные варианты масштабирования и многое другое.</p>
<p><li><a href="http://azure.microsoft.com/services/app-service/mobile/">Дополнительные сведения о мобильных приложениях</a>.</p>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left">Приложения API</td>
<td align="left">
<p><li>Приложения API — это новый тип приложения, в службе приложений, который позволяет легко создавать и использовать интерфейсы API в облаке hello.</p>
<p><li><a href="http://azure.microsoft.com/services/app-service/api/">Узнайте больше о приложениях API</a>.</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left">Logic Apps</td>
<td align="left">
<p><li>Приложения логики представляют новый тип приложений в службе приложений, позволяющий легко автоматизировать бизнес-процесс.</p>
<p><li><a href="http://azure.microsoft.com/services/app-service/logic/">Дополнительные сведения о приложении логики</a>.</p></td>
</tr>
<tr class="odd">
<td align="left">Службы Azure BizTalk</td>
<td align="left">Приложения API BizTalk</td>
<td align="left">
<li><p>Службы BizTalk продолжить toobe доступен в качестве автономной службы и остаются полностью поддерживается.</p>
<li><p>Все возможности hello служб BizTalk интегрированы в службы приложения как приложения API Включение пользователей tooperform интеграция приложений и сценариев интеграции B2B с одним из типов приложения hello в службе приложений.</p>
<li><p>С приложениями логики теперь можно автоматизировать бизнес-процессов с помощью рабочих процессов toocreate визуального проектирования качества.</p></td>
</tr>
</tbody>
</table>

toolearn более, перейдите на страницу [документации службы приложений](https://azure.microsoft.com/documentation/services/app-service/).

