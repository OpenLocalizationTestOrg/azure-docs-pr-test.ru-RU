---
title: "стили aaaCustomize hello портал разработчиков в службе управления API Azure | Документы Microsoft"
description: "Узнайте, как стили hello toomodify используется для любой страницы hello портал разработчиков в службе управления API Azure."
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
ms.openlocfilehash: aaaa86527992ba43e64eab5fd35c7f57b573c812
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="customize-hello-styling-of-hello-developer-portal-in-azure-api-management"></a>Настроить стиль hello hello портал разработчиков в службе управления API Azure
Существует три основных способа toocustomize hello разработчика портала управления API Azure:

* [Изменить содержимое hello статические страницы и элементы макета страницы][modify-content-layout]
* [Обновить стили hello, используются для элементов страницы через портал разработчиков hello] [ customize-styles] (как описано в данном руководстве)
* [Изменить шаблоны hello для страниц, созданных портала hello] [ portal-templates] (например API документы, продукты, проверка подлинности пользователя, и т. д.)

## <a name="change-headers-styling"></a>Изменить стиль hello элементы страницы

Hello цвета, шрифты, размеры, расстояние между и другие элементы, связанные со стилем любой странице портала hello определяются правила стилей. 

Изменение правил стиля hello выполняется из hello **портал разработчиков** при войти качестве администратора. существует tooget сначала открыть hello портала Azure и нажмите кнопку **портал издателя** из инструментов hello службы управления API экземпляра.

![Портал издателя][api-management-management-console]

Нажмите кнопку на **портал разработчиков** на верхний правый hello. 

![Ссылка на портал разработчиков на портал издателя hello][api-management-pp-dp-link]

панель инструментов настройки hello tooopen наведите указатель мыши на значок настройки hello (или выберите его) и затем нажмите кнопку «стили» из панели инструментов hello.

![Кнопка на панели инструментов настройки][api-management-customization-toolbar-button]

Существует два основных способа редактирования правил стиля — можно просмотреть все правила стиля hello, используемые в любом список hello, который отображается по умолчанию и при необходимости измените стиль или можно выбрать **Выбор элемента на странице приветствия** и затем Щелкните в любом месте hello страницы toosee только hello стили для этого элемента.

![Панель инструментов настройки][api-management-customization-toolbar]

Нажмите кнопку hello **Выбор элемента на странице приветствия** параметр для этого примера.  Элементы, теперь становятся выделяются при наведении на них с toosignify мыши hello стили какой элемент будет начинаться редактирования, если вы нажали кнопку. Перемещение hello наведите указатель мыши текст hello в заголовок hello (обычно требуется название компании hello здесь), а затем щелкните его. В стилях hello в редакторе отображается набор правил стиля именованные и по категориям. Каждое правило представляет свойство стиля hello выбранного элемента. Например, для выбранной выше заголовок текста hello hello размер текста hello находится в @font-size-h1 во время hello имя шрифта hello предлагает альтернативы @headings-font-family.

> Если вы знакомы с [начальной загрузки][bootstrap], эти правила являются на самом деле [переменные LESS] [ LESS variables] внутри hello начальной загрузки темы hello портал разработчиков.
> 
> 

Изменим цвет текста заголовка hello hello. Выберите запись hello в hello  **@headings-color**  и введите **#000000**. Это hello шестнадцатеричный код для черный цвет hello. После этого вы видите, индикатор квадратный цветов отображается в конце hello hello текстовое поле. Если щелкнуть этот индикатор, палитра цветов позволяет toochoose цвет.

![Выбор цвета][api-management-customization-toolbar-color-picker]

Изменения предварительного просмотра в режиме реального времени, как сделать их, но являются видимыми только tooadministrators. toomake эти изменения видны tooeveryone, нажмите кнопку hello **публикации** кнопку в редактор стилей hello и Подтверждение изменений hello.

![Меню публикации][api-management-customization-toolbar-publish-form]

> toochange hello правил стилей, применимые tooany другого элемента на странице приветствия, выполните hello же процедуру, как можно было сделано для заголовка hello. Нажмите кнопку **Выбор элемента на странице приветствия** из Редактор стилей hello, вы заинтересованы в элемент select hello и запуска, изменив значения hello hello правила стилей, отображается на экране приветствия.
> 
> 


## <a name="next-steps"> </a>Дальнейшие действия
* Узнайте, как содержимое hello toocustomize портал разработчиков страниц с помощью [шаблонами портала разработчиков](api-management-developer-portal-templates.md).

[Change hello styling of hello headers]: #change-headers-styling
[Next steps]: #next-steps

[Azure Classic Portal]: https://manage.windowsazure.com/

[api-management-management-console]: ./media/api-management-customize-styles/api-management-management-console.png
[api-management-pp-dp-link]: ./media/api-management-customize-styles/api-management-pp-dp-link.png
[api-management-customization-toolbar-button]: ./media/api-management-customize-styles/api-management-customization-toolbar-button.png
[api-management-customization-toolbar]: ./media/api-management-customize-styles/api-management-customization-toolbar.png
[api-management-customization-toolbar-color-picker]: ./media/api-management-customize-styles/api-management-customization-toolbar-color-picker.png
[api-management-customization-toolbar-publish-form]: ./media/api-management-customize-styles/api-management-customization-toolbar-publish-form.png

[modify-content-layout]: api-management-modify-content-layout.md
[customize-styles]: api-management-customize-styles.md
[portal-templates]: api-management-developer-portal-templates.md

[bootstrap]: http://getbootstrap.com/
[LESS variables]: http://getbootstrap.com/css/
