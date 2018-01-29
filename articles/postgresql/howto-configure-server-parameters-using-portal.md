---
title: "Настройка параметров сервера в базе данных Azure для PostgreSQL с помощью портала Azure | Документация Майкрософт"
description: "В этой статье объясняется, как настроить параметры сервера в базе данных Azure для PostgreSQL с помощью портала Azure."
services: postgresql
author: rachel-msft
ms.author: raagyema
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 11/08/2017
ms.openlocfilehash: 9e8262fbfcde2e69a656e356a7ab241f2d5043ad
ms.sourcegitcommit: 93902ffcb7c8550dcb65a2a5e711919bd1d09df9
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/09/2017
---
# <a name="configure-server-parameters-in-azure-portal"></a>Настройка параметров сервера на портале Azure
С помощью портала Azure можно вывести список параметров конфигурации для сервера базы данных Azure для PostgreSQL, а также отобразить и обновить их.

## <a name="prerequisites"></a>Предварительные требования
Чтобы приступить к выполнению этого руководства, вам потребуются следующие компоненты:
- [сервер базы данных Azure для PostgreSQL](quickstart-create-server-database-portal.md).

## <a name="viewing-and-editing-parameters"></a>Просмотр и изменение параметров
1. Откройте [портал Azure](https://portal.azure.com).

2. Выберите сервер базы данных Azure для PostgreSQL.

3. В разделе **Параметры** выберите **Параметры сервера**. На странице отобразится список параметров, их значения и описания.
![Страница общих сведений для параметров](./media/howto-configure-server-parameters-in-portal/3-overview-of-parameters.png)

4. Нажмите кнопку **раскрывающегося списка**, чтобы просмотреть возможные значения параметров перечисляемого типа, например client_min_messages.
![Раскрывающийся список для перечисляемого типа](./media/howto-configure-server-parameters-in-portal/4-enum-drop-down.png)

5. Выберите кнопку с буквой **i** (информация) или наведите на нее указатель мыши, чтобы просмотреть диапазон возможных значений числовых параметров, например cpu_index_tuple_cost.
![Кнопка информации](./media/howto-configure-server-parameters-in-portal/4-information-button.png)

6. При необходимости воспользуйтесь **полем поиска**, чтобы сузить область поиска до определенного параметра. Поиск выполняется по имени и описанию параметров.
![Результаты поиска](./media/howto-configure-server-parameters-in-portal/5-search.png)

7. Измените значения требуемых параметров. Все изменения, вносимые в этом сеансе, выделены фиолетовым цветом. Изменив значения, можно нажать кнопку **Сохранить**. Также вы можете нажать кнопку **Отменить**, чтобы отменить изменения.
![Сохранение или отмена изменений](./media/howto-configure-server-parameters-in-portal/6-save-and-discard-buttons.png)

8. Если вы сохранили новые значения параметров, всегда можно восстановить значения по умолчанию, выбрав **Сбросить все к значениям по умолчанию**.
![Сбросить все к значениям по умолчанию](./media/howto-configure-server-parameters-in-portal/7-reset-to-default-button.png)

## <a name="next-steps"></a>Дальнейшие действия
Кроме того, вы узнаете о таких возможностях, как:
- [Серверы базы данных Azure для PostgreSQL](concepts-servers.md)
- [Настройка параметров конфигурации сервера с помощью Azure CLI](howto-configure-server-parameters-using-cli.md)
