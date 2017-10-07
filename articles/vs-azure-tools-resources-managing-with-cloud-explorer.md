---
title: "aaaManaging Azure ресурсы с Cloud Explorer | Документы Microsoft"
description: "Узнайте, как toobrowse Cloud Explorer toouse и настраивать ресурсы Azure в Visual Studio."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 6347dc53-f497-49d5-b29b-e8b9f0e939d7
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/25/2017
ms.author: kraigb
ms.openlocfilehash: 8a81660074d5d04be063df9e25076b7a97586514
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hello-resources-associated-with-your-azure-accounts-in-visual-studio-cloud-explorer"></a>Управление hello ресурсы, связанные с учетными записями Azure в Visual Studio Cloud Explorer
Cloud Explorer позволяет вам tooview ресурсами Azure и группы ресурсов, проверьте их свойства и выполнять действия диагностики ключа разработчика в Visual Studio. 

Как hello [портал Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040), Cloud Explorer строится hello стеке диспетчера ресурсов Azure. Благодаря этому Cloud Explorer распознает ресурсы (например, группы ресурсов Azure) и службы Azure (например, Logic Apps и API-приложения), а также поддерживает [управление доступом на основе ролей](active-directory/role-based-access-control-configure.md) (RBAC). 

## <a name="prerequisites"></a>Предварительные требования
- [Visual Studio 2017 г](https://www.visualstudio.com/downloads/) с hello **рабочей нагрузки Azure** выбран, или более ранней версии Visual Studio с hello [Microsoft Azure SDK для .NET 2.9](https://www.microsoft.com/en-us/download/details.aspx?id=51657).
- Учетная запись Azure. Если у вас ее нет, [зарегистрируйтесь для работы с бесплатной пробной версией](http://go.microsoft.com/fwlink/?LinkId=623901) или [активируйте преимущества для подписчиков Visual Studio](http://go.microsoft.com/fwlink/?LinkId=623901).

> [!NOTE]
> Выберите tooview Cloud Explorer **представление** > **Cloud Explorer** hello меню.   
> 
> 

## <a name="add-an-azure-account-toocloud-explorer"></a>Добавьте учетную запись Azure tooCloud обозревателя
tooview hello ресурсы, связанные с учетной записью Azure, необходимо сначала добавить tooCloud учетной записи hello обозревателя. 

1. В **Cloud Explorer** выберите раздел **Параметры учетной записи Azure**.

    ![Значок параметров учетной записи Azure в Cloud Explorer](media/vs-azure-tools-resources-managing-with-cloud-explorer/azure-account-settings.png)

1. Выберите **Добавить новую учетную запись**. 

    ![Ссылка для добавления учетной записи в Cloud Explorer](media/vs-azure-tools-resources-managing-with-cloud-explorer/add-account-link.png)

1. Вход toohello учетная запись Azure, ресурсы которого вы хотите toobrowse. 

1. После входа в учетную запись Azure tooan отображения hello подписок, связанных с этой учетной записи. Здравствуйте, установите флажки для подписок hello toobrowse и затем выберите **применить**. 
 
    ![Cloud Explorer: выберите toodisplay подписок Azure](media/vs-azure-tools-resources-managing-with-cloud-explorer/select-subscriptions.png)

1. После выбора подписки hello, ресурсы которого требуется toobrowse, эти подписки и ресурсы отображения в Cloud Explorer hello.

    ![Список ресурсов для учетной записи Azure в Cloud Explorer](media/vs-azure-tools-resources-managing-with-cloud-explorer/resources-listed.png)

## <a name="remove-an-azure-account-from-cloud-explorer"></a>Удаление учетной записи Azure в Cloud Explorer 

1. В **Cloud Explorer** выберите раздел **Параметры учетной записи Azure**.

    ![Значок параметров учетной записи Azure в Cloud Explorer](media/vs-azure-tools-resources-managing-with-cloud-explorer/azure-account-settings.png)

1. Выберите Далее toohello счета, tooremove, **удалить**.

    ![Значок параметров учетной записи Azure в Cloud Explorer](media/vs-azure-tools-resources-managing-with-cloud-explorer/remove-account.png)

## <a name="view-resource-types-or-resource-groups"></a>Просмотр типов или групп ресурсов
tooview ресурсы Azure, вы также можете выбрать **типов ресурсов** или **групп ресурсов** представления.

1. В **Cloud Explorer**, выберите hello раскрывающийся список представление ресурса.

    ![Облако раскрывающемся списке tooselect hello требуемого ресурсы обозревателя](media/vs-azure-tools-resources-managing-with-cloud-explorer/resources-view-dropdown.png)

1. Hello контекстном меню выберите представление требуемого hello: 

    - **Типы ресурсов** представление — используется на hello общее представление hello [портал Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040), показывает ресурсов Azure категории по своему типу, например веб-приложений, учетные записи хранилища и виртуальных машин. 
    - **Группы ресурсов** представление - Azure распределяет ресурсы по hello группы ресурсов Azure, с которым они связаны. Группа ресурсов представляет собой набор ресурсов Azure, обычно используемых в конкретном приложении. toolearn Дополнительные сведения о группах ресурсов Azure в разделе [Обзор диспетчера ресурсов Azure](./azure-resource-manager/resource-group-overview.md).

    Hello следующий рисунок показывает сравнение hello два представления ресурсов:

    ![Сравнение представлений ресурсов в Cloud Explorer](media/vs-azure-tools-resources-managing-with-cloud-explorer/resource-views-comparison.png)

## <a name="view-and-navigate-resources-in-cloud-explorer"></a>Просмотр и поиск ресурсов в Cloud Explorer
toonavigate tooan ресурсов Azure и просмотра его информации в Cloud Explorer разверните hello элемента типа или группы связанных ресурсов и затем выберите hello ресурсов. При выборе ресурса информация отображается на вкладках hello двух - **действия** и **свойства** - внизу hello Cloud Explorer. 

- **Действия** вкладке - списки hello действия в Cloud Explorer для hello выбранного ресурса. Можно также просмотреть этих параметров щелкните правой кнопкой мыши ресурс tooview hello его контекстное меню.

- **Свойства** вкладке - показывает свойства hello hello ресурсов, например его тип, языкового стандарта и ресурсов группы, с которым он связан.

Hello иллюстрации показан пример сравнение отображаемые на каждой вкладке для приложения службы.

![](./media/vs-azure-tools-resources-managing-with-cloud-explorer/actions-and-properties.png)

Каждый ресурс имеет действие hello **открыть на портале**. При выборе этого действия Cloud Explorer отображает hello выбранных ресурсов в hello [портал Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040). Hello **открыть на портале** функция удобно для перемещения по toodeeply вложенных ресурсов.

Дополнительные действия и значения свойств, также появляются основании hello ресурсов Azure. Например, веб-приложений и логика приложения также необходим hello действия **открыть в браузере** и **присоединить отладчик** Кроме слишком**открыть на портале**. Редакторы tooopen действия появляются, если выбрать BLOB-объекта учетной записи хранилища, очередей или таблиц. У приложений Azure есть свойства **URL-адрес** и **Состояние**, а для ресурсов хранилища в свойствах указаны ключ доступа и строка подключения.

## <a name="find-resources-in-cloud-explorer"></a>Поиск ресурсов в Cloud Explorer
ресурсы toolocate с определенным именем в подписках Azure учетной записи, введите имя hello в hello **поиска** поле в Cloud Explorer.

![Поиск ресурсов в обозревателе облака](./media/vs-azure-tools-resources-managing-with-cloud-explorer/search-for-resources.png)

По мере ввода символов в hello **поиска** поле только те ресурсы, которые соответствуют эти символы отображаются в дереве ресурсов hello.
