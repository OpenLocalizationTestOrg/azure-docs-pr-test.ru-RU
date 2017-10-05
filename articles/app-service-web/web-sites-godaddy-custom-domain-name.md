---
title: "Настройка личного доменного имени в службе приложений Azure (GoDaddy)"
description: "Узнайте, как использовать доменное имя из GoDaddy с веб-приложениями Azure"
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
ms.openlocfilehash: 158c5dc06f83e16633d3c2fbb4eb27d3e8af030c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="configure-a-custom-domain-name-in-azure-app-service-purchased-directly-from-godaddy"></a>Настройка личного доменного имени в службе приложений Azure (приобретенного непосредственно у GoDaddy)
[!INCLUDE [web-selector](../../includes/websites-custom-domain-selector.md)]

[!INCLUDE [intro](../../includes/custom-dns-web-site-intro.md)]

Если вы приобрели домен через веб-приложения службы приложений Azure, см. последний шаг процесса [Покупка домена для веб-приложений](custom-dns-web-site-buydomains-web-app.md).

В этой статье вы найдете указания по использованию личного доменного имени, приобретенного у [GoDaddy](https://godaddy.com), с использованием [веб-приложений службы приложений](http://go.microsoft.com/fwlink/?LinkId=529714).

[!INCLUDE [introfooter](../../includes/custom-dns-web-site-intro-notes.md)]

<a name="understanding-records"></a>

## <a name="understanding-dns-records"></a>Общие сведения о записях DNS
[!INCLUDE [understandingdns](../../includes/custom-dns-web-site-understanding-dns-raw.md)]

<a name="bkmk_configurecname"></a>

## <a name="add-a-dns-record-for-your-custom-domain"></a>Добавление записи DNS для пользовательского домена
Чтобы сопоставить личный домен с веб-приложением в службе приложений, добавьте новую запись в таблицу DNS для этого домена с помощью средств, предоставляемых GoDaddy. Выполните следующие действия, чтобы найти средства DNS для GoDaddy.com.

1. Выполните вход на GoDaddy.com с использованием своей учетной записи и выберите **Моя учетная запись**, а затем — **Управление доменами**. Выберите в раскрывающемся меню доменное имя, которое вы хотите использовать для своего веб-приложения Azure, и откройте **Диспетчер DNS**.
   
    ![страница пользовательского домена для GoDaddy](./media/web-sites-godaddy-custom-domain-name/godaddy-customdomain.png)
2. На странице **Сведения о домене** откройте вкладку **Файл зоны DNS**. Этот раздел используется в целях добавления и изменения записей DNS для доменного имени.
   
    ![Вкладка файла зоны DNS](./media/web-sites-godaddy-custom-domain-name/godaddy-zonetab.png)
   
    Выберите **Добавить запись** , чтобы добавить существующую запись.
   
    Чтобы **отредактировать** существующую запись, выберите значок с изображением карандаша и бумаги рядом с записью.
   
   > [!NOTE]
   > Перед добавлением новых записей обратите внимание, что GoDaddy уже создал записи DNS для таких популярных поддоменов (**Узел** в редакторе), как **email**, **files**, **mail** и др. Если имя, которое вы хотите использовать, уже существует, измените существующую запись вместо того, чтобы создавать новую.
   > 
   > 
3. При добавлении записи необходимо сначала выбрать тип записи.
   
    ![выберите тип записи](./media/web-sites-godaddy-custom-domain-name/godaddy-selectrecordtype.png)
   
    Далее вы должны ввести **Узел** (личный домен или поддомен) и то, что будет значиться в поле **Указывает на**.
   
    ![добавление записи о зоне](./media/web-sites-godaddy-custom-domain-name/godaddy-addzonerecord.png)
   
   * При добавлении **записи A (узел)** нужно указать в поле **Узел** символ **@** (представляющий имя корневого домена, например **contoso.com**), * (подстановочный знак для сопоставления с несколькими поддоменами) либо поддомен, который вы хотите использовать (например, **www**.) Задайте в поле **Указывает на** IP-адрес вашего веб-приложения Azure.
   * При добавлении **записи (псевдонима) CNAME** необходимо задать в поле **Узел** тот поддомен, который вы хотите использовать. Например, **www**. Задайте в поле **Указывает на** доменное имя **.azurewebsites.net** вашего веб-приложения Azure. Например, **contoso.azurewebsites.net**.
4. Нажмите **Добавить еще одну запись**.
5. Выберите **TXT** в качестве типа записи, укажите для параметра **Узел** значение **@**, а для параметра **Указывает на** значение **&lt;имя_вашего_веб_приложения&gt;.azurewebsites.net**.
   
   > [!NOTE]
   > Запись типа TXT позволяет Azure убедиться, что именно вы являетесь владельцем домена, описанного в записи A или первой записи типа TXT. После сопоставления домена с веб-приложением на портале Azure можно удалить запись типа TXT.
   > 
   > 
6. По завершении добавления или изменения записей нажмите кнопку **Завершить** для сохранения изменений.

<a name="enabledomain"></a>

## <a name="enable-the-domain-name-on-your-web-app"></a>Включение доменного имени в веб-приложении
[!INCLUDE [modes](../../includes/custom-dns-web-site-enable-on-web-site.md)]

> [!NOTE]
> Чтобы приступить к работе со службой приложений Azure до создания учетной записи Azure, перейдите к разделу [Пробное использование службы приложений](https://azure.microsoft.com/try/app-service/), где вы можете быстро создать кратковременное веб-приложение начального уровня в службе приложений. Никаких кредитных карт и обязательств.
> 
> 

## <a name="whats-changed"></a>Изменения
* Руководство по переходу от веб-сайтов к службе приложений см. в статье [Служба приложений Azure и существующие службы Azure](http://go.microsoft.com/fwlink/?LinkId=529714).

