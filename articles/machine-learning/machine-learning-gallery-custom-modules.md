---
title: "пользовательские модули коллекции аналитики aaaCortana | Документы Microsoft"
description: "Изучение пользовательских модулей машинного обучения в коллекции Cortana Intelligence."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 16037a84-dad0-4a8c-9874-a1d3bd551cf0
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/14/2017
ms.author: roopalik;garye
ms.openlocfilehash: e2a2d39935e6d367eb192de723fb82318d04e2be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="discover-custom-machine-learning-modules-in-cortana-intelligence-gallery"></a>Изучение пользовательских модулей машинного обучения в коллекции Cortana Intelligence
[!INCLUDE [machine-learning-gallery-item-selector](../../includes/machine-learning-gallery-item-selector.md)]

## <a name="custom-modules-for-machine-learning-studio"></a>Пользовательские модули для Студии машинного обучения
Коллекции аналитики Cortana предлагает несколько вариантов [пользовательские модули](https://gallery.cortanaintelligence.com/customModules) , расширить возможности hello из студии машинного обучения Azure. Для разработки даже более современные решения прогнозирующего анализа можно импортировать в эксперименты, toouse модули hello.

В настоящее время коллекции hello предлагает модули на *временных рядов analytics*, *правил взаимосвязей*, *алгоритмы кластеризации* (помимо тех, к средних) и  *визуализации*и другие модули workhorse программы.


## <a name="discover"></a>Поиск
пользовательские модули toobrowse [в hello коллекции](http://gallery.cortanaintelligence.com)в разделе **дополнительные**выберите **пользовательские модули**.

![Выберите настраиваемые модули на домашней странице hello коллекции](media/machine-learning-gallery-custom-modules/select-custom-modules-in-gallery.png)

Hello  **[настраиваемые модули](https://gallery.cortanaintelligence.com/customModules)**  странице отображается список недавно добавленных и популярные модули. Выберите все пользовательские модули tooview hello **все** кнопки. Выберите toosearch для настраиваемого модуля, **все**и условия фильтра, а затем выберите. Условия поиска можно ввести в hello **поиска** поле вверху hello коллекции страницы приветствия.

![Выберите «Просмотреть все» toobrowse все пользовательские модули](media/machine-learning-gallery-custom-modules/click-see-all-for-all-custom-modules.png)

### <a name="understand"></a>Общие сведения

toounderstand, как работает опубликованных пользовательский модуль, выберите страницу сведений о модуле hello tooopen hello пользовательский модуль. страница сведений о Hello обеспечивает удобство работы согласованное и информативных обучения. Например страница сведений о hello иллюстрирует hello назначение модуля "hello", а перечисляются ожидаемый входов, выходов и параметры. страница сведений о Hello также имеет ссылку toohello основной исходный код, который можно проверить и настроить.

### <a name="comment-and-share"></a>Комментарии и общий доступ
На странице сведений пользовательского модуля, в hello **комментарии** разделе можно комментарий, отправить отзыв или задать вопросы о модуле hello. Можно даже предоставить модуль hello друзей или сотрудников в Twitter и LinkedIn. Также можно направлять страница сведений о модуле toohello ссылку, tooinvite страница hello tooview других пользователей.

![Расскажите друзьям о том, что вы нашли](media/machine-learning-gallery-how-to-use-contribute-publish/share-links.png)

![Добавляйте свои комментарии](media/machine-learning-gallery-how-to-use-contribute-publish/comments.png)

## <a name="import"></a>Импорт
Любые пользовательские модули можно импортировать из собственных экспериментов hello коллекции tooyour.

Коллекции аналитики Cortana предлагает два способа tooimport копию модуля hello:

* **Из коллекции hello**. При импорте пользовательского модуля из hello коллекции можно также получить примере эксперимента, возникшей примером как toouse hello модуля.
* **Из Студии машинного обучения Azure**. Можно импортировать любые пользовательские модули во время работы в студии машинного обучения (в этом случае не получить эксперимента образец hello).

### <a name="from-hello-gallery"></a>Из коллекции hello

1. Откройте страницу сведений модуля hello в hello коллекции. 
2. Выберите **Open in Studio** (Открыть в Студии).
   
    ![Откройте пользовательский модуль из коллекции hello](media/machine-learning-gallery-custom-modules/open-custom-module-from-gallery.png)
   
Каждый пользовательский модуль включает эксперимента образец, демонстрирующий, как toouse hello модуля. При выборе **в Studio**, открывается hello примере эксперимента в рабочую область студии машинного обучения. (Если вы еще не вошли в tooStudio, появится toofirst входа с использованием учетной записи Майкрософт.)

Кроме toohello образцы экспериментов, настраиваемый модуль hello скопированный tooyour рабочей области. Он также размещается на палитре модулей со всеми встроенными и пользовательскими модулями Студии машинного обучения. Теперь вы можете использовать его в своих экспериментах так же, как любой другой модуль в рабочей области.

### <a name="from-within-machine-learning-studio"></a>Из Студии машинного обучения Azure

1. В Студии машинного обучения выберите **New** (Создать).
2. Выберите **Модуль**. Можно выбрать из списка модулей коллекции или поиска конкретного модуля с помощью hello **поиска** поле.
3. Укажите мышью модуль, а затем выберите **Импортировать модуль**. (выберите tooget сведения о модуле hello **представление в галерее**. Откроется страница сведений о toohello модуля в коллекции hello.)
   
    ![Импорт пользовательского модуля в Студию машинного обучения](media/machine-learning-gallery-custom-modules/add-custom-module-in-studio.png)

пользовательский модуль Hello скопированный tooyour рабочей области и помещается в палитре модуль, с помощью встроенных или пользовательских модулей студии машинного обучения. Теперь вы можете использовать его в своих экспериментах так же, как любой другой модуль в рабочей области.

## <a name="use"></a>Использование

Независимо от того, какой метод выберите tooimport пользовательского модуля, при импорте модуля hello, модуль hello, помещены в палитре модуля в студии машинного обучения. Из палитры модуля можно использовать пользовательский модуль hello в любой эксперимента в рабочей области, так же, как и любой другой модуль.

toouse импортированного модуля:

1. Создайте эксперимент или откройте существующий.
2. Выберите список hello tooexpand пользовательских модулей в рабочей области в палитре модуля hello, **пользовательские**. Палитра модуля Hello — toohello левой части холст эксперимента hello.
   
    ![Список пользовательских модулей на палитре Студии](media/machine-learning-gallery-custom-modules/custom-module-in-studio-palette.png)
3. Выберите модуль hello импортированного и перетащите его tooyour эксперимента.


**[Доступен toohello коллекции](http://gallery.cortanaintelligence.com)**

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

