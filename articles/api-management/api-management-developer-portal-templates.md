---
title: "aaaCustomize портал для разработчиков hello API управления с помощью шаблонов-Azure | Документы Microsoft"
description: "Узнайте, как toocustomize hello портал разработчика управления API Azure, с помощью шаблонов."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: a195675b-f7d0-4fc9-90bf-860e6f17ccf7
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: b00d5f1534e9466f30ff3920e7aae048feb8b8c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocustomize-hello-azure-api-management-developer-portal-using-templates"></a>Как toocustomize hello портал разработчика управления API Azure, с помощью шаблонов

Существует три основных способа toocustomize hello разработчика портала управления API Azure:

* [Изменить содержимое hello статические страницы и элементы макета страницы][modify-content-layout]
* [Стили hello обновления используются для элементов страницы через портал разработчиков hello][customize-styles]
* [Изменить шаблоны hello для страниц, созданных портала hello] [ portal-templates] (как описано в данном руководстве)

Шаблоны, используемые toocustomize hello содержимого страниц портала разработчика, созданные системой (например API документы, продукты, проверка подлинности пользователя, и т. д.). С помощью [DotLiquid](http://dotliquidmarkup.org/) синтаксис и указанном наборе ресурсов локализованную строку, значков и элементов управления на странице имеют большую гибкость tooconfigure hello содержимого hello страниц по своему усмотрению.

## <a name="developer-portal-templates-overview"></a>Обзор шаблонов портала разработчика
Редактирование шаблонов выполняется из hello **портал разработчиков** при войти качестве администратора. существует tooget сначала открыть hello портала Azure и нажмите кнопку **портал издателя** из инструментов hello службы управления API экземпляра.

![Портал издателя][api-management-management-console]

Нажмите кнопку на **портал разработчиков** на верхний правый hello. 

![Меню портала разработчика][api-management-developer-portal-menu]

tooaccess Здравствуйте шаблоны портала разработчика, щелкните hello настроить значок меню настройки hello левой toodisplay hello и нажмите кнопку **шаблоны**.

![Шаблоны портала разработчика][api-management-customize-menu]

Список шаблонов Hello отображается несколько категорий шаблонов, которые охватывают различные страницы приветствия портал разработчиков hello. Каждый шаблон отличается, но tooedit действия hello их и опубликовать изменения hello являются одинаковыми hello. tooedit шаблона, щелкните имя hello hello шаблона.

![Шаблоны портала разработчика][api-management-templates-menu]

Если выбрать шаблон принимает toohello разработчика страницы портала, настроенные для шаблона. В этом примере hello **список продуктов** отображается шаблон. Hello **список продуктов** области экрана приветствия обозначается hello красный прямоугольник hello шаблона элементов управления. 

![Шаблон "Список продуктов"][api-management-developer-portal-templates-overview]

Некоторые шаблоны, такие как hello **профиля пользователя** шаблонов, настраивать различные части hello одной страницы. 

![Шаблоны "Профиль пользователя"][api-management-user-profile-templates]

Hello редактора для каждого шаблона портала разработчиков состоит из двух разделов hello нижней части страницы приветствия. Левая часть Hello отображает hello редактирования области для шаблона hello, и правой стороны hello hello модели данных для шаблона hello. 

области редактирования шаблона, Hello содержит hello разметку, которая управляет hello внешний вид и поведение соответствующей страницы приветствия на портале разработчиков hello. Разметка Hello в шаблоне hello использует hello [DotLiquid](http://dotliquidmarkup.org/) синтаксиса. Один из популярных редакторов для DotLiquid — [DotLiquid для конструкторов](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers). Шаблон toohello любые изменения, внесенные во время редактирования, отображаются в в режиме реального времени в браузере hello, но tooyour скрыт от клиентов только после [Сохранить](#to-save-a-template) и [публикации](#to-publish-a-template) hello шаблона.

![Разметка шаблона][api-management-template]

Hello **данные шаблона** панели содержится руководство toohello данных модели для hello сущностей, которые доступны для использования в одном шаблоне. В этом руководстве он предоставляет, отображая hello актуальные данные, отображаемые в настоящее время на портале разработчиков hello. Можно развернуть шаблон панелей hello, щелкнув прямоугольник hello в правом верхнем углу hello hello **данные шаблона** области.

![Модель данных шаблона][api-management-template-data]

В предыдущем примере hello существуют два продукта, которые отображаются на портале разработчиков hello, полученные из hello данные, отображаемые в hello **данные шаблона** области, как показано в следующий пример hello.

```json
{
    "Paging": {
        "Page": 1,
        "PageSize": 10,
        "TotalItemCount": 2,
        "ShowAll": false,
        "PageCount": 1
    },
    "Filtering": {
        "Pattern": null,
        "Placeholder": "Search products"
    },
    "Products": [
        {
            "Id": "56ec64c380ed850042060001",
            "Title": "Starter",
            "Description": "Subscribers will be able toorun 5 calls/minute up tooa maximum of 100 calls/week.",
            "Terms": "",
            "ProductState": 1,
            "AllowMultipleSubscriptions": false,
            "MultipleSubscriptionsCount": 1
        },
        {
            "Id": "56ec64c380ed850042060002",
            "Title": "Unlimited",
            "Description": "Subscribers have completely unlimited access toohello API. Administrator approval is required.",
            "Terms": null,
            "ProductState": 1,
            "AllowMultipleSubscriptions": false,
            "MultipleSubscriptionsCount": 1
        }
    ]
}
```

Hello разметки в hello **список продуктов** шаблон процессов hello hello требуемого выходные данные tooprovide путем прохода по коллекции hello продуктов toodisplay сведения и ссылки продукт отдельных tooeach. Примечание hello `<search-control>` и `<page-control>` элементы в разметке hello. Они управляют отображением hello hello поиска и разбиение по страницам элементов управления на странице приветствия. `ProductsStrings|PageTitleProducts`Представляет ссылку на локализованную строку, которая содержит hello `h2` текст заголовка для страницы приветствия. Список строковых ресурсов, элементов управления страницы и значков, которые доступны для использования в шаблонах портала разработчиков, см. в статье [Azure API Management Templates](api-management-developer-portal-templates-reference.md) (Шаблоны в службе управления API).

```html
<search-control></search-control>
<div class="row">
    <div class="col-md-9">
        <h2>{% localized "ProductsStrings|PageTitleProducts" %}</h2>
    </div>
</div>
<div class="row">
    <div class="col-md-12">
    {% if products.size > 0 %}
    <ul class="list-unstyled">
    {% for product in products %}
        <li>
            <h3><a href="/products/{{product.id}}">{{product.title}}</a></h3>
            {{product.description}}
        </li>    
    {% endfor %}
    </ul>
    <paging-control></paging-control>
    {% else %}
    {% localized "CommonResources|NoItemsToDisplay" %}
    {% endif %}
    </div>
</div>
```

## <a name="toosave-a-template"></a>toosave шаблона
toosave шаблон, нажмите кнопку Сохранить в редакторе шаблона hello.

![Сохранение шаблона][api-management-save-template]

Изменения сохранены не в активном состоянии в портал разработчиков hello, пока будут опубликованы.

## <a name="toopublish-a-template"></a>toopublish шаблона
Сохраненные шаблоны могут быть опубликованы по отдельности или все вместе. toopublish отдельного шаблона нажмите кнопку Опубликовать в редакторе шаблона hello.

![Публикация шаблона][api-management-publish-template]

Нажмите кнопку **Да** tooconfirm и сделать шаблон hello live на портале для разработчиков hello.

![Подтверждение публикации][api-management-publish-template-confirm]

toopublish неопубликованных все текущие версии шаблона, щелкните **публикации** в списке шаблонов hello. Неопубликованные шаблоны обозначаются звездочку после имени шаблона hello. В этом примере hello **список продуктов** и **продукта** шаблоны публикуются.

![Публикация шаблонов][api-management-publish-templates]

Нажмите кнопку **опубликовать настройки** tooconfirm.

![Подтверждение публикации][api-management-publish-customizations]

Недавно опубликованные шаблоны вступают в силу немедленно в портал разработчиков hello.

## <a name="toorevert-a-template-toohello-previous-version"></a>toorevert предыдущая версия toohello шаблона
toorevert toohello предыдущей опубликованной версии шаблона, щелкните вернуться в редактор шаблонов hello.

![Отмена изменений шаблона][api-management-revert-template]

Нажмите кнопку **Да** tooconfirm.

![Подтверждение][api-management-revert-template-confirm]

выполнена Hello ранее опубликованной версии шаблона live на портале разработчиков hello, после hello отменить операцию.

## <a name="toorestore-a-template-toohello-default-version"></a>версия шаблона по умолчанию toohello toorestore
Версия по умолчанию tootheir восстановления шаблонов состоит из двух этапов. Первый шаблоны hello должна быть восстановлена и затем восстановить hello версии должны быть опубликованы.

toorestore версия по умолчанию toohello один шаблон щелкните восстановления редактор шаблонов hello.

![Отмена изменений шаблона][api-management-reset-template]

Нажмите кнопку **Да** tooconfirm.

![Подтверждение][api-management-reset-template-confirm]

toorestore версии по умолчанию все шаблоны tootheir, щелкните **восстановление шаблонов по умолчанию** hello шаблона списка.

![Восстановление шаблонов][api-management-restore-templates]

Hello восстановленной шаблонов необходимо затем можно опубликовать все сразу или по отдельности с помощью инструкции hello в [toopublish шаблона](#to-publish-a-template).

## <a name="next-steps"></a>Дальнейшие действия
Справочную информацию о шаблонах портала разработчика, строковых ресурсах, значках и элементах управления страницы см. в разделе [Azure API Management Templates](api-management-developer-portal-templates-reference.md) (Шаблоны в службе управления API).

[modify-content-layout]: api-management-modify-content-layout.md
[customize-styles]: api-management-customize-styles.md
[portal-templates]: api-management-developer-portal-templates.md

[api-management-customize-menu]: ./media/api-management-developer-portal-templates/api-management-customize-menu.png
[api-management-templates-menu]: ./media/api-management-developer-portal-templates/api-management-templates-menu.png
[api-management-developer-portal-templates-overview]: ./media/api-management-developer-portal-templates/api-management-developer-portal-templates-overview.png
[api-management-template]: ./media/api-management-developer-portal-templates/api-management-template.png
[api-management-template-data]: ./media/api-management-developer-portal-templates/api-management-template-data.png
[api-management-developer-portal-menu]: ./media/api-management-developer-portal-templates/api-management-developer-portal-menu.png
[api-management-management-console]: ./media/api-management-developer-portal-templates/api-management-management-console.png
[api-management-browse]: ./media/api-management-developer-portal-templates/api-management-browse.png
[api-management-user-profile-templates]: ./media/api-management-developer-portal-templates/api-management-user-profile-templates.png
[api-management-save-template]: ./media/api-management-developer-portal-templates/api-management-save-template.png
[api-management-publish-template]: ./media/api-management-developer-portal-templates/api-management-publish-template.png
[api-management-publish-template-confirm]: ./media/api-management-developer-portal-templates/api-management-publish-template-confirm.png
[api-management-publish-templates]: ./media/api-management-developer-portal-templates/api-management-publish-templates.png
[api-management-publish-customizations]: ./media/api-management-developer-portal-templates/api-management-publish-customizations.png
[api-management-revert-template]: ./media/api-management-developer-portal-templates/api-management-revert-template.png
[api-management-revert-template-confirm]: ./media/api-management-developer-portal-templates/api-management-revert-template-confirm.png
[api-management-reset-template]: ./media/api-management-developer-portal-templates/api-management-reset-template.png
[api-management-reset-template-confirm]: ./media/api-management-developer-portal-templates/api-management-reset-template-confirm.png
[api-management-restore-templates]: ./media/api-management-developer-portal-templates/api-management-restore-templates.png







