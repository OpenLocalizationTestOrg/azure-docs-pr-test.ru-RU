---
title: "aaaConfigure пользовательское доменное имя в службе приложений Azure (GoDaddy)"
description: "Узнайте, как имя toouse домена GoDaddy с веб-приложениях Azure"
services: app-service
documentationcenter: 
author: erikre
manager: erikre
editor: jimbe
ms.assetid: 33233e30-5846-488f-83f3-b32e5c114564
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/12/2016
ms.author: cephalin
ms.openlocfilehash: 48158ee752f9833249bbf85adf80f572d1c68486
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-custom-domain-name-in-azure-app-service-purchased-directly-from-godaddy"></a>Настройка личного доменного имени в службе приложений Azure (приобретенного непосредственно у GoDaddy)
[!INCLUDE [web-selector](../../includes/websites-custom-domain-selector.md)]

[!INCLUDE [intro](../../includes/custom-dns-web-site-intro.md)]

Если приобрели домен через веб-приложениях службы приложений Azure, а затем ссылаться на последнем этапе toohello работы [купить домена для веб-приложений](custom-dns-web-site-buydomains-web-app.md).

В этой статье вы найдете указания по использованию личного доменного имени, приобретенного у [GoDaddy](https://godaddy.com), с использованием [веб-приложений службы приложений](http://go.microsoft.com/fwlink/?LinkId=529714).

[!INCLUDE [introfooter](../../includes/custom-dns-web-site-intro-notes.md)]

<a name="understanding-records"></a>

## <a name="understanding-dns-records"></a>Общие сведения о записях DNS
[!INCLUDE [understandingdns](../../includes/custom-dns-web-site-understanding-dns-raw.md)]

<a name="bkmk_configurecname"></a>

## <a name="add-a-dns-record-for-your-custom-domain"></a>Добавление записи DNS для пользовательского домена
tooassociate свой домен с веб-приложения в службе приложений, необходимо добавить новую запись в таблице hello DNS для личного домена с помощью средств, предоставляемых GoDaddy. Используйте следующие шаги toolocate hello DNS средства для GoDaddy.com hello

1. Войдите в систему учетной записи tooyour с GoDaddy.com и выберите **Моя учетная запись** и затем **управление Мои домены**. Выберите hello раскрывающееся меню для имени домена hello обратиться toouse с Azure веб-приложения и выберите **Управление DNS**.
   
    ![страница пользовательского домена для GoDaddy](./media/web-sites-godaddy-custom-domain-name/godaddy-customdomain.png)
2. Из hello **сведения о домене** перейдите toohello **файла зоны DNS** вкладки. Это раздел hello, используются для добавления и изменения записей DNS для имени домена.
   
    ![Вкладка файла зоны DNS](./media/web-sites-godaddy-custom-domain-name/godaddy-zonetab.png)
   
    Выберите **добавить запись** tooadd существующей записи.
   
    слишком**изменить** существующую запись, выберите hello перо и бумага значок рядом с записью hello.
   
   > [!NOTE]
   > Перед добавлением новых записей обратите внимание, что GoDaddy уже создал записи DNS для таких популярных поддоменов (**Узел** в редакторе), как **email**, **files**, **mail** и др. Если вы хотите toouse имя hello существует, измените существующую запись hello вместо создания нового.
   > 
   > 
3. Добавление записи, необходимо сначала выбрать тип записи hello.
   
    ![выберите тип записи](./media/web-sites-godaddy-custom-domain-name/godaddy-selectrecordtype.png)
   
    Затем необходимо указать hello **узла** (hello пользовательский домен или дочерний домен) и что он **указывает**.
   
    ![добавление записи о зоне](./media/web-sites-godaddy-custom-domain-name/godaddy-addzonerecord.png)
   
   * При добавлении **запись (узла)** -необходимо задать hello **узла** tooeither поле  **@**  (представляет имя корневого домена, такие как  **Contoso.com**,) * (шаблон для сопоставления нескольких поддоменов) или hello дочерний домен, нужно toouse (например, **www**.) Необходимо задать hello **указывает** поле toohello IP-адрес вашего веб-приложение Azure.
   * При добавлении **запись CNAME (псевдоним)** -необходимо задать hello **узла** поле toohello поддомене нужно toouse. Например, **www**. Необходимо задать hello **указывает** toohello поле **. azurewebsites.net** доменное имя вашего веб-приложение Azure. Например, **contoso.azurewebsites.net**.
4. Нажмите **Добавить еще одну запись**.
5. Выберите **TXT** как тип записи hello, затем укажите **узла** значение  **@**  и **указывает** значение  **&lt;yourwebappname&gt;. azurewebsites.net**.
   
   > [!NOTE]
   > TXT-запись используется Azure toovalidate, что вы являетесь владельцем, что домен hello описываемого hello hello или записи первая запись TXT. После домена hello сопоставленных toohello веб-приложения в hello портал Azure, этой записи TXT-записи можно удалить.
   > 
   > 
6. Когда закончите добавлять или изменение записей, нажмите кнопку **Готово** toosave изменений.

<a name="enabledomain"></a>

## <a name="enable-hello-domain-name-on-your-web-app"></a>Включить hello доменного имени на веб-приложения
[!INCLUDE [modes](../../includes/custom-dns-web-site-enable-on-web-site.md)]

> [!NOTE]
> Tooget работы в службе приложений Azure перед регистрацией учетную запись Azure, перейдите слишком[повторите служб приложений](https://azure.microsoft.com/try/app-service/), в котором можно немедленно создать кратковременных начальный веб-приложения в службе приложений. Никаких кредитных карт и обязательств.
> 
> 

## <a name="whats-changed"></a>Изменения
* Toohello руководство изменений из tooApp веб-сайтов службы. в разделе: [службе приложений Azure и ее влияние на существующие службы Azure](http://go.microsoft.com/fwlink/?LinkId=529714)

