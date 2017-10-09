---
title: "aaaHow toosecure доступа tooAzure данных каталога | Документы Microsoft"
description: "В этой статье объясняется, как toosecure данных каталога и его ресурсы данных."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/17/2017
ms.author: maroche
ms.openlocfilehash: d7c35fd57d8add1cdc152b75f111879288e1548f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosecure-access-toodata-catalog-and-data-assets"></a>Как toosecure доступ к ресурсам каталога toodata
> [!IMPORTANT]
> Эта функция доступна только в выпуске standard hello каталога данных Azure.

Каталог данных Azure позволяет toospecify, кто имеет доступ к каталогу данных hello и что операций (регистрировать, аннотировать, стать владельцем) они могут выполнять на метаданные в каталоге hello. 

## <a name="catalog-users-and-permissions"></a>Пользователи каталога и разрешения
toogive пользователем или hello группы доступа к каталогу данных tooa и задайте разрешения:

1. На hello [Домашняя страница данных каталога](http://www.azuredatacatalog.com), нажмите кнопку **параметры** на панели инструментов hello.

    ![Каталог данных: параметры](media/data-catalog-how-to-secure-catalog/data-catalog-settings.png)
2. На странице "Параметры" hello раскройте hello **пользователей каталога** раздела.
    ![Пользователи каталога - Добавление](media/data-catalog-how-to-secure-catalog/data-catalog-add-button.png)
3. Щелкните **Добавить**.
4. Введите полное hello **имя пользователя** или имя hello **группы безопасности** в Azure Active Directory (AAD) связанные с каталогом hello hello. Используйте запятую (",") в качестве разделителя при добавлении нескольких пользователей или групп.
    ![Пользователи каталога: пользователи или группы](media/data-catalog-how-to-secure-catalog/data-catalog-users-groups.png)
5. Нажмите клавишу **ввод** или **ВКЛАДКЕ** за пределы hello текстовое поле. 
6.  Убедитесь, что все разрешения (**заметки**, **зарегистрировать**, и **Take Ownership**) назначаются toothese пользователям или группам по умолчанию. То есть можно hello пользователю или группе [зарегистрировать ресурсов данных]( data-catalog-how-to-register.md), [заметки ресурсов данных]( data-catalog-how-to-annotate.md), и [распоряжаться ресурсами данных]( data-catalog-how-to-manage.md). 
    ![Пользователи каталога: разрешения по умолчанию](media/data-catalog-how-to-secure-catalog/data-catalog-default-permissions.png)
7.  toogive пользователя или группы, только на hello чтение каталога toohello доступ, снимите hello **заметки** параметр для этого пользователя или группы. При этом hello пользователь или группа не может пометить ресурсов данных в каталоге hello, но они могут просматривать их. 
8.  toodeny пользователя или группы из регистрация данных ресурсов, снимите hello **зарегистрировать** параметр для этого пользователя или группы.
9.  toodeny пользователю изменять владельца ресурса данных, снимите флажок hello **распоряжаться** параметр для этого пользователя или группы. 
10. Щелкните пользователя или группу из каталога пользователей, toodelete **x** для пользователя или группы hello hello нижней части списка hello. 
    ![Каталог пользователей: удаление пользователя](media/data-catalog-how-to-secure-catalog/data-catalog-delete-user.png)

    > [!IMPORTANT]
    > Рекомендуется добавить пользователей toocatalog группы безопасности вместо добавления пользователей непосредственно и назначить разрешения. Затем добавьте группы безопасности toohello пользователей, которые соответствуют их ролей и их каталогов toohello необходимый уровень доступа.

## <a name="special-considerations"></a>Специальные рекомендации

- Hello разрешения назначены toosecurity группы являются аддитивными. Предположим, что пользователь входит в две группы. Одна группа имеет разрешение на добавление заметок, а другая группа — нет. Тогда у пользователя будет разрешение на добавление заметок. 
- Hello разрешения явно tooa пользователя переопределение hello разрешения, назначенные toogroups toowhich hello пользователь принадлежит. В предыдущем примере hello, скажем, явно добавленные пользователи toocatalog пользователя hello и не предоставляйте разрешения заметки. Несмотря на то, что пользователь hello является членом группы, которая имеет аннотировать разрешения пользователя Hello невозможно добавить заметки к ресурсов данных.

## <a name="next-steps"></a>Дальнейшие действия
- [Начало работы с каталогом данных Azure](data-catalog-get-started.md)

