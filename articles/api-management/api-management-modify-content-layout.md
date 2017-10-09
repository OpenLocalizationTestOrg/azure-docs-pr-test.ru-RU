---
title: "содержимое страницы aaaModify hello портал разработчиков в службе управления API Azure | Документы Microsoft"
description: "Узнайте, как содержимое страницы tooedit, на портал разработчиков hello в службе управления API Azure."
services: api-management
documentationcenter: 
author: antonba
manager: vlvinogr
editor: 
ms.assetid: 186128fe-41c0-4efb-9efe-2478ad4d103f
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 02/09/2017
ms.author: antonba
ms.openlocfilehash: fd5a854e900d9512518643e593b1b59a0952621f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="modify-hello-content-and-layout-of-pages-on-hello-developer-portal-in-azure-api-management"></a>Изменить содержимое hello и макет страницы на портал разработчиков hello в службе управления API Azure
Существует три основных способа toocustomize hello разработчика портала управления API Azure:

* [Изменить содержимое hello статические страницы и элементы макета страницы] [ modify-content-layout] (как описано в данном руководстве)
* [Стили hello обновления используются для элементов страницы через портал разработчиков hello][customize-styles]
* [Изменить шаблоны hello для страниц, созданных портала hello] [ portal-templates] (например API документы, продукты, проверка подлинности пользователя, и т. д.)

## <a name="page-structure"> </a>Структура страниц портала разработчика

портал разработчиков Hello зависит от системы управления контентом. Макет Hello каждой странице будет построен на основе набора элементов небольшой страницы, называется мини-приложения:

![Структура страницы портала разработчика][api-management-customization-widget-structure]

Все мини-приложения можно изменять. 
* в мини-приложении «Содержимое» hello находиться Hello core содержимое определенных tooeach отдельную страницу. Изменения страницы означает редактирования hello содержимое этого мини-приложения.
* Содержатся все элементы макета страницы с hello оставшиеся мини-приложения. Изменения, внесенные toothese мини-приложений будет применить tooall страницы. Они будут tooas ссылка «макет мини-приложения».

В повседневной страницы только изменение одного обычно изменяет hello содержимого графического элемента, имеющих различное содержимое для каждой отдельной страницы.

## <a name="modify-layout-widget"></a>Изменение содержимого hello элемента «макет»

Содержимое в портал разработчиков hello изменяется через портал издателя hello, доступное из hello портала Azure. tooreach его, нажмите кнопку **портал издателя** из инструментов hello службы управления API экземпляра.

![Портал издателя][api-management-management-console]

содержимое tooedit hello, мини-приложение, нажмите кнопку **мини-приложения** из hello **портал разработчиков** меню слева hello. Для этого примера позволяет измените содержимое hello hello Заголовок мини-приложения. Выберите hello **заголовок** мини-приложение из списка hello.

![Заголовок мини-приложения][api-management-widgets-header]

для редактирования из внутри hello Hello содержимое заголовка hello **текст** поля. Изменить текст hello в случае необходимости, а затем нажмите кнопку **Сохранить** hello нижней части страницы приветствия.

Теперь можно будет toosee hello новый заголовок на каждой странице на портале разработчика hello.

> портал разработчиков tooopen hello в портал издателя hello, нажмите кнопку **портал разработчиков** hello верхней панели.
> 
> 

## <a name="edit-page-contents"></a>Изменить содержимое страницы приветствия

Щелкните список всех существующих страниц содержимого toosee hello **содержимого** из hello **портал разработчиков** меню портала издателя hello.

![Управление содержимым][api-management-customization-manage-content]

Нажмите кнопку hello **приветствия** страница tooedit сведения, отображаемые на домашней странице портала разработчиков hello hello. Внесите изменения hello, предварительного просмотра их при необходимости и нажмите кнопку **Опубликовать сейчас** toomake их tooeveryone видимым.

> Домашняя страница Hello использует специальный макет, который позволяет toodisplay заголовка вверху hello. Этот заголовок не может быть изменено из hello **содержимого** раздела. tooedit этом логотипа, нажмите кнопку **мини-приложения** из hello **портал разработчиков** последовательно выберите пункты **Домашняя страница** из hello **текущего слоя** раскрывающегося списка список, а затем откройте hello **баннер** кусте hello **избранные раздел**. Это мини-приложение Hello содержимое можно редактировать так же, как и любой другой страницы.
> 
> 

## <a name="next-steps"> </a>Дальнейшие действия
* [Стили hello обновления используются для элементов страницы через портал разработчиков hello][customize-styles]
* [Изменить шаблоны hello для страниц, созданных портала hello] [ portal-templates] (например API документы, продукты, проверка подлинности пользователя, и т. д.)

[Structure of developer portal pages]: #page-structure
[Modifying hello contents of a layout widget]: #modify-layout-widget
[Edit hello contents of a page]: #edit-page-contents
[Next steps]: #next-steps

[modify-content-layout]: api-management-modify-content-layout.md
[customize-styles]: api-management-customize-styles.md
[portal-templates]: api-management-developer-portal-templates.md

[api-management-customization-widget-structure]: ./media/api-management-modify-content-layout/portal-widget-structure.png
[api-management-management-console]: ./media/api-management-modify-content-layout/api-management-management-console.png
[api-management-widgets-header]: ./media/api-management-modify-content-layout/api-management-widgets-header.png
[api-management-customization-manage-content]: ./media/api-management-modify-content-layout/api-management-customization-manage-content.png
