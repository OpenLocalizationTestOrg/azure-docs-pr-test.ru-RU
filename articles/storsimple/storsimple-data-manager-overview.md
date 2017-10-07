---
title: "Обзор диспетчера данных Azure StorSimple aaaMicrosoft | Документы Microsoft"
description: "Общие сведения о hello службы диспетчера StorSimple данных (личной предварительной версии)"
services: storsimple
documentationcenter: NA
author: vidarmsft
manager: syadav
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 11/22/2016
ms.author: vidarmsft
ms.openlocfilehash: 5d29f7d26be9f2b36857526bdea770d991cece6c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-data-manager-overview-private-preview"></a>Общие сведения о диспетчере данных StorSimple (закрытая предварительная версия)

## <a name="overview"></a>Обзор

Microsoft Azure StorSimple — это гибридное Облачное решение хранилища, адреса hello сложности неструктурированные данные, обычно связанные с общими файловыми ресурсами. StorSimple использует облачного хранилища, как локальное решение расширение hello и автоматически уровнями данных через hello локальное хранилище и Облачное хранилище. Интегрируется с локальной защиты данных и облачных моментальных снимков, устраняет необходимость hello sprawling инфраструктуры. Архивация и аварийного восстановления также не вызывает затруднений с облаком hello, выступающего в качестве удаленного расположения.

Hello службы DTS, мы представляем в этом документе, позволяет вам tooseamlessly доступа hello StorSimple данных в облаке hello. Эта служба предоставляет API-интерфейсы tooextract данные из StorSimple и представлять их tooother Azure служб в форматах, которые могут быть сразу использованы. Hello форматы, поддерживаемые в этой предварительной версии — BLOB-объекты Azure и средств служб мультимедиа Azure. Это преобразование позволяет вам tooeasily подключения службы, такие как данные toooperate служб мультимедиа Azure, Azure HDInsight, машинного обучения Azure и поиска Azure на локального устройства серии StorSimple 8000.

Ниже представлена общая блок-схема, иллюстрирующая этот процесс.

![Общая схема](./media//storsimple-data-manager-overview/high-level-diagram.png)

В этом документе объясняется, как можно зарегистрироваться для получения закрытой предварительной версии этой службы. Также объясняется, как можно использовать это приложение toowrite службы, использующие StorSimple данных и другими службами Azure в облаке hello.

## <a name="sign-up-for-data-manager-preview"></a>Регистрация для получения предварительной версии диспетчера данных
Перед регистрацией для службы данных Manager hello просмотрите hello следующие необходимые условия.

### <a name="prerequisites"></a>Предварительные требования

В этом упражнении предполагается, что у вас есть:
* активная подписка Azure;
* tooa доступа зарегистрированные устройства серии StorSimple 8000
* Здравствуйте, все ключи, связанные с устройства серии StorSimple 8000 hello.

### <a name="sign-up"></a>Регистрация

Hello данных StorSimple Manager находится в личной ознакомительной учетной записи. Выполните следующие шаги toosign для частной предварительной версии этой службы hello.

1.  Войдите на hello портал Azure с расширением hello данных StorSimple Manager в: [https://aka.ms/HybridDataManager](https://aka.ms/HybridDataManager). Используйте ваш toolog учетных данных Azure в.

2.  Нажмите кнопку hello  **+**  toocreate значок службы. Нажмите кнопку **хранения** и нажмите кнопку **разделе все** в колонке hello, открывающемся.

    ![Поиск значка диспетчера данных StorSimple](./media/storsimple-data-manager-overview/search-data-manager-icon.png)

3. Значок hello данных StorSimple Manager.

    ![Выбор значка диспетчера данных StorSimple](./media/storsimple-data-manager-overview/select-data-manager-icon.png)

4. Щелкните значок диспетчера данных StorSimple и нажмите кнопку **Создать**. Выбор подписки hello должны tooenable для получения личной предварительной версии hello и нажмите кнопку **зарегистрироваться me!**

    ![Кнопка "Зарегистрироваться"](./media/storsimple-data-manager-overview/sign-me-up.png)

5. Эта команда отправляет запрос tooonboard вы. Мы выполним эту операцию в кратчайшие сроки. После включения подписки можно создать службу диспетчера данных StorSimple.

6. tooeasily доступа к службе диспетчера StorSimple данных hello, щелкните значок toopin hello его tooyour "Избранное".

    ![Доступ к диспетчеру данных StorSimple](./media/storsimple-data-manager-overview/access-data-managers.png)


## <a name="next-steps"></a>Дальнейшие действия

[Использовать пользовательский Интерфейс диспетчера данных StorSimple tootransform данные](storsimple-data-manager-ui.md).
