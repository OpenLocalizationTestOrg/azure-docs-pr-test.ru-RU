---
title: "aaaMigrate active DNS имя tooAzure службы приложений | Документы Microsoft"
description: "Узнайте, как toomigrate настраиваемого доменного имени DNS, уже назначенный tooa live tooAzure узла служб приложений без простоев."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: jimbe
tags: top-support-issue
ms.assetid: 10da5b8a-1823-41a3-a2ff-a0717c2b5c2d
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: cephalin
ms.openlocfilehash: fbc4cc30dcb87efb2e867cb65c5404b667661e62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-an-active-dns-name-tooazure-app-service"></a>Перенос active tooAzure имя DNS службы приложений

В этой статье показано, как toomigrate active DNS имя слишком[службе приложений Azure](../app-service/app-service-value-prop-what-is.md) без простоев.

При миграции действующем сайте и его tooApp имя домена DNS службы DNS-имени уже обслуживает реального трафика. Можно избежать простоя при разрешении DNS во время миграции hello, предварительно привязки hello active DNS имя tooyour приложением служб приложений.

Если вы не сомневаетесь время простоя при разрешении DNS, см. раздел [сопоставления существующих пользовательских DNS имя tooAzure веб-приложений](app-service-web-tutorial-custom-domain.md).

## <a name="prerequisites"></a>Предварительные требования

toocomplete этом руководства:

- [Убедитесь, что приложение службы приложений не находится в ценовой категории "Бесплатный"](app-service-web-tutorial-custom-domain.md#checkpricing).

## <a name="bind-hello-domain-name-preemptively"></a>Предварительно привязки имени домена hello

При связывании пользовательского домена предварительно выполнить оба следующих hello перед внесением любых изменений в записи DNS.

- проверка принадлежности домена;
- Включить hello имя домена приложения.

При переносе пользовательской DNS-имя и, наконец из hello старого узла toohello приложением служб приложений во время разрешения DNS будет без простоев.

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-domain-verification-record"></a>Создание записи для проверки домена

владение tooverify домена, запишите добавить TXT. Сопоставляет Hello TXT-запись из _awverify.&lt; дочерний домен >_ too_&lt;appname >. azurewebsites.net_. 

Hello TXT-записи, необходимые зависит от DNS-записей, которые требуется toomigrate hello. Примеры см. в следующей таблице hello (`@` обычно представляет hello корневой домен):  

| Пример записи DNS | Узел, для которого задается TXT | Значение TXT |
| - | - | - |
| @ (корневой домен) | _awverify_ | _&lt;имя_приложения>.azurewebsites.net_ |
| www (поддомен) | _awverify.www_ | _&lt;имя_приложения>.azurewebsites.net_ |
| \* (с подстановочным знаком) | _awverify.\*_ | _&lt;имя_приложения>.azurewebsites.net_ |

На странице записей DNS Обратите внимание, hello тип записи для hello требуется toomigrate DNS-имя. Служба приложений поддерживает сопоставление из записей CNAME и записей A.

### <a name="enable-hello-domain-for-your-app"></a>Включить hello домена приложения

В hello [портал Azure](https://portal.azure.com)в левой области навигации страницы приложения hello hello, выберите **пользовательские домены**. 

![Меню личных доменов](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

В hello **пользовательские домены** страницу, выберите hello  **+**  значок Далее слишком**добавить имя узла**.

![Добавление имени узла](./media/app-service-web-tutorial-custom-domain/add-host-name-cname.png)

Полное доменное имя типа hello, добавлены hello TXT-записи, такие как `www.contoso.com`. Для домена подстановочный знак (например \*. contoso.com), можно использовать любое имя DNS, которое совпадает с именем домена hello подстановочный знак. 

Выберите **Проверка**.

Hello **добавить имя узла** кнопка активна. 

Убедитесь, что **тип записи имени узла** задается тип записи DNS toohello требуется toomigrate.

Выберите **Добавить имя узла**.

![Добавить приложение toohello имя DNS](./media/app-service-web-tutorial-custom-domain/validate-domain-name-cname.png)

Он может занять некоторое время для нового узла toobe hello отражаются в приложение hello **пользовательские домены** страницы. Попробуйте обновить tooupdate hello hello обозревателя данных.

![Запись CNAME добавлена](./media/app-service-web-tutorial-custom-domain/cname-record-added.png)

Теперь DNS-имя включено в приложении Azure. 

## <a name="remap-hello-active-dns-name"></a>Изменить сопоставление hello active DNS-имя

Hello toodo самое левой изменение сопоставления вашей active tooApp toopoint записей DNS службы. Право, он по-прежнему указывает tooyour старого веб-сайта.

<a name="info"></a>

### <a name="copy-hello-apps-ip-address-a-record-only"></a>Скопируйте приложение hello IP-адрес (только запись)

Если выполняется сопоставление записи CNAME, пропустите этот раздел. 

запись A tooremap требуется внешний IP-адрес службы приложений приложение hello, как показано на hello **пользовательские домены** страницы.

Закрыть hello **добавить имя узла** страницу, выбрав **X** в правом верхнем углу hello. 

В hello **пользовательские домены** скопируйте приложение hello IP-адрес.

![Приложение портала навигации tooAzure](./media/app-service-web-tutorial-custom-domain/mapping-information.png)

### <a name="update-hello-dns-record"></a>Обновление записи DNS hello

Hello странице записей DNS вашего домена поставщика выберите tooremap записей DNS hello.

Для hello `contoso.com` корневого домена примере, повторно сопоставить hello A или запись CNAME как примеры hello в hello в следующей таблице: 

| Пример полного доменного имени | Тип записи | Узел | Значение |
| - | - | - | - |
| contoso.com (корневой домен) | A | `@` | IP-адрес из [приложение hello копирования IP-адрес](#info) |
| www.contoso.com (поддомен) | CNAME | `www` | _&lt;имя_приложения>.azurewebsites.net_ |
| \*.contoso.com (с подстановочным знаком) | CNAME | _\*_ | _&lt;имя_приложения>.azurewebsites.net_ |

Сохраните параметры.

Запросы DNS следует приступить к устранению tooyour приложением служб приложений, сразу после распространения DNS происходит.

## <a name="next-steps"></a>Дальнейшие действия

Узнайте, как toobind пользовательские SSL-сертификат tooApp службы.

> [!div class="nextstepaction"]
> [Привязать существующий пользовательский SSL сертификат tooAzure веб-приложений](app-service-web-tutorial-custom-ssl.md)
