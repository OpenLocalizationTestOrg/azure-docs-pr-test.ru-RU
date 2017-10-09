---
title: "aaaConfigure пользовательское доменное имя для веб-приложения в службе приложений Azure, который использует диспетчер трафика для балансировки нагрузки."
description: "Используйте личное доменное имя для веб-приложения в службе приложений Azure, которая включает в себя диспетчер трафика."
services: app-service\web
documentationcenter: 
author: cephalin
manager: cfowler
editor: 
ms.assetid: 0f96c0e7-0901-489b-a95a-e3b66ca0a1c2
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2016
ms.author: cephalin
ms.openlocfilehash: dfde5fc6b445b30b10e03dcb03e8d072130d9377
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-a-custom-domain-name-for-a-web-app-in-azure-app-service-using-traffic-manager"></a>Настройка личного доменного имени для веб-приложения в службе приложений Azure, использующей диспетчер трафика
[!INCLUDE [web-selector](../../includes/websites-custom-domain-selector.md)]

[!INCLUDE [intro](../../includes/custom-dns-web-site-intro-traffic-manager.md)]

В этой статье содержатся общие инструкции по использованию личного доменного имени со службой приложений Azure, которая использует диспетчер трафика для балансировки нагрузки.

[!INCLUDE [tmwebsitefooter](../../includes/custom-dns-web-site-traffic-manager-notes.md)]

[!INCLUDE [introfooter](../../includes/custom-dns-web-site-intro-notes.md)]

<a name="understanding-records"></a>

## <a name="understanding-dns-records"></a>Общие сведения о записях DNS
[!INCLUDE [understandingdns](../../includes/custom-dns-web-site-understanding-dns-traffic-manager.md)]

<a name="bkmk_configsharedmode"></a>

## <a name="configure-your-web-apps-for-standard-mode"></a>Настройка веб-приложений для режима Standard
[!INCLUDE [modes](../../includes/custom-dns-web-site-modes-traffic-manager.md)]

<a name="bkmk_configurecname"></a>

## <a name="add-a-dns-record-for-your-custom-domain"></a>Добавление записи DNS для пользовательского домена
> [!NOTE]
> Если вы приобрели домен через веб-приложениях службы приложений Azure пропустите следующие шаги и toohello заключительном этапе см. [купить домена для веб-приложений](custom-dns-web-site-buydomains-web-app.md) статьи.
> 
> 

tooassociate свой домен с веб-приложения в службе приложений Azure, необходимо добавить новую запись в таблице hello DNS для личного домена с помощью средств, предоставляемых hello регистратора, который вы приобрели доменного имени из. Используйте следующие шаги toolocate hello и средства hello DNS.

1. Войдите в tooyour учетную запись на сайте регистратора домена и найти страницу управления DNS-записей. Найдите ссылки или области hello узла помечены как **доменное имя**, **DNS**, или **управление сервером имен**. Часто toothis страницы можно найти ссылку Просмотр сведений учетной записи и Отыскав ссылку например **Мои домены**.
2. После обнаружения hello страницы управления для имени домена найдите ссылку, которая позволяет вам tooedit hello DNS-записей. Она может иметь название **Файл зоны**, **Записи DNS** или **Дополнительно**.
   
   * Страница приветствия скорее всего будет иметь несколько записей, которые уже созданы, таких как операции сопоставления "**@**«или»\*" со страницей «парковки домена». Она также может содержать записи для распространенных поддоменов, таких как **www**.
   * Назовите страницу приветствия будет **записи CNAME**, или укажите tooselect раскрывающегося списка тип записи. На ней также могут упоминаться другие записи, такие как **записи A** и **записи MX**. В некоторых случаях записи CNAME могут называться по-другому, например **записью псевдонима**.
   * Страница приветствия также будет иметь поля, которые позволяют слишком**карты** из **имя узла** или **доменное имя** tooanother доменное имя.
3. Хотя отличаться hello особенности каждого регистратора, как правило сопоставления *из* пользовательское имя домена (например, **contoso.com**,) *для* имя домена диспетчера трафика hello (**contoso.trafficmanager.net**), используемый для веб-приложения.
   
   > [!NOTE]
   > Кроме того Если записи уже используется, и необходимости toopreemptively привязки tooit вашего приложения, можно создать дополнительные записи CNAME. Например, привязка toopreemptively **www.contoso.com** tooyour веб-приложения, создайте запись CNAME из **awverify.www** слишком**contoso.trafficmanager.net**. Затем можно добавить tooyour «www.contoso.com» веб-приложения без изменения записи CNAME hello «www». Дополнительные сведения см. в статье [Создание записей DNS для веб-приложения в пользовательском домене][CREATEDNS].
   > 
   > 
4. После завершения добавления или изменения записей DNS у регистратора, сохраните изменения hello.

<a name="enabledomain"></a>

## <a name="enable-traffic-manager"></a>Включение диспетчера трафика
[!INCLUDE [modes](../../includes/custom-dns-web-site-enable-on-traffic-manager.md)]

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения см. в разделе hello [Центр разработчика Node.js](/develop/nodejs/).

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- URL List -->

[CREATEDNS]: ../dns/dns-web-sites-custom-domain.md
