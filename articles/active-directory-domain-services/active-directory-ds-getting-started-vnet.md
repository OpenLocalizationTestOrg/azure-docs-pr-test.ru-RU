---
title: "Доменные службы Azure Active Directory: создание или выбор виртуальной сети | Документация Майкрософт"
description: "Включение Azure доменных служб Active Directory с помощью hello классический портал Azure"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 13ab1608-e3d8-40de-9f7b-9b5b42199af4
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/28/2017
ms.author: maheshu
ms.openlocfilehash: 212c741b20e846742d94f70342c4263ce8984153
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-or-select-a-virtual-network-for-azure-active-directory-domain-services"></a>Создание или выбор виртуальной сети для доменных служб Azure Active Directory
## <a name="before-you-begin"></a>Перед началом работы
См. слишком[сетевые аспекты для доменных служб Active Directory Azure](active-directory-ds-networking.md).

## <a name="task-2-create-an-azure-virtual-network"></a>Задача 2. Создание виртуальной сети Azure
Следующая задача конфигурации Hello является toocreate виртуальной сети Azure и подсеть внутри него. Вам потребуется включить доменные службы Azure Active Directory в этой подсети. Если вы предпочитаете toouse существующей виртуальной сети, этот шаг можно пропустить.

> [!NOTE]
> Убедитесь, что hello виртуальной сети Azure можно создать или выбрать toouse с доменными службами Active Directory Azure, принадлежащий tooan регионе Azure, которая поддерживается Azure доменными службами Active Directory. tooascertain hello регионах Azure, в которых доступен доменных служб Active Directory Azure см. в разделе [служб Azure по регионам](https://azure.microsoft.com/regions/#services/).
>
>Запишите имя hello tooensure hello виртуальной сети, при включении доменных служб Active Directory Azure на шаге дальнейшей настройки выбрать hello справа виртуальной сети.


toocreate Azure виртуальной сети, в которой будет tooenable Azure доменных служб Active Directory, выполните эти инструкции по настройке:

1. Go toohello [классический портал Azure](https://manage.windowsazure.com).
2. Выберите в левой области hello **сетей**.

    ![Узел "Сети"](./media/active-directory-domain-services-getting-started/networks-node.png)  
    Hello **виртуальных сетей** открывается окно.
3. В области задач hello hello нижней части окна hello, выберите **New**.

    ![Окно виртуальных сетей](./media/active-directory-domain-services-getting-started/virtual-networks.png)
4. Щелкните **Сетевые службы**, а затем выберите **Виртуальная сеть**.

    ![Виртуальная сеть — быстрое создание](./media/active-directory-domain-services-getting-started/virtual-network-quickcreate.png)
5. Нажмите кнопку toocreate виртуальной сети, **быстрое создание**.

6. Укажите **имя** для виртуальной сети и рассмотрите возможность выполнения следующих hello:
    * Вы можете tooconfigure **адресное пространство** или **максимальное число виртуальных Машин** для этой сети.
    * Можно оставить hello **DNS-сервер** в **нет** сейчас. После включения доменных служб Active Directory Azure, вы можете обновить приветствия.
7. В hello **расположение** раскрывающегося списка выберите поддерживаемом регионе Azure.  
    tooascertain hello регионах Azure, в которых доступен доменных служб Active Directory Azure см. в разделе [служб Azure по регионам](https://azure.microsoft.com/regions/#services/).
8. toocreate виртуальной сети, нажмите кнопку **Создание виртуальной сети**.

    ![Создание виртуальной сети для доменных служб Azure Active Directory](./media/active-directory-domain-services-getting-started/create-vnet.png)
9. После создания виртуальной сети, выберите имя hello hello виртуальной сети и нажмите кнопку hello **Настройка** вкладки.

    ![Создание подсети](./media/active-directory-domain-services-getting-started/create-vnet-properties.png)
10. В разделе **адресное пространство виртуальной сети**, нажмите кнопку **добавить подсеть**, а затем укажите подсеть с именем hello **AaddsSubnet**.

    ![Создание подсети для доменных служб Azure Active Directory](./media/active-directory-domain-services-getting-started/create-vnet-add-subnet.png)

11. toocreate Здравствуйте подсети, щелкните **Сохранить**.


## <a name="next-step"></a>Дальнейшие действия
[Задача 3. Включение доменных служб Azure Active Directory](active-directory-ds-getting-started-enableaadds.md)
