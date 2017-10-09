---
title: "aaaCreate концентратор событий Azure | Документы Microsoft"
description: "Создать пространство имен концентраторов событий Azure и концентратор событий с помощью портала Azure hello"
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: ff99e327-c8db-4354-9040-9c60c51a2191
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2017
ms.author: sethm
ms.openlocfilehash: 9a8b7711e2ca7d112e24be19353d43c365ff6935
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-event-hubs-namespace-and-an-event-hub-using-hello-azure-portal"></a>Создать пространство имен концентраторов событий и концентратор событий с помощью портала Azure hello

## <a name="create-an-event-hubs-namespace"></a>Создание пространства имен концентраторов событий
1. Войдите на toohello [портал Azure][Azure portal]и нажмите кнопку **New** на hello верхнего левого угла экрана приветствия.
1. Последовательно выберите **Интернет вещей** и **Концентраторы событий**.
   
    ![](./media/event-hubs-create/create-event-hub9.png)
1. В hello **создать пространство имен** колонки, введите имя пространства имен. система Hello немедленно проверяет toosee, доступно ли имя hello.
   
    ![](./media/event-hubs-create/create-event-hub1.png)
1. После внесения убедиться, что имя пространства имен hello недоступна, выберите hello ценовой категории (Basic или Standard). Кроме того, в какой ресурс hello toocreate выберите подписки Azure, группа ресурсов и расположение. 
1. Нажмите кнопку **создать** toocreate приветствия имен. Вы можете иметь toowait hello системных toofully подготовки hello ресурсов в течение нескольких минут.
2. В hello портала пространств имен выберите hello вновь создано и пространство имен.
2. В колонке **Политики общего доступа** щелкните **RootManageSharedAccessKey**.
    
    ![](./media/event-hubs-create/create-event-hub7.png)

3. Нажмите кнопку toocopy hello копирования hello **RootManageSharedAccessKey** буфер обмена toohello строку соединения. Сохраните эту строку подключения во временной папке, например в блокноте, toouse более поздней версии.
    
    ![](./media/event-hubs-create/create-event-hub8.png)

## <a name="create-an-event-hub"></a>Создание концентратора событий

1. В списке пространство имен hello концентраторов событий выберите только что созданный hello пространства имен.      
   
    ![](./media/event-hubs-create/create-event-hub2.png) 

2. В колонке приветствия имен щелкните **концентраторов событий**.
   
    ![](./media/event-hubs-create/create-event-hub3.png)

1. Hello верхней части колонки hello, нажмите кнопку **добавить концентратор событий**.
   
    ![](./media/event-hubs-create/create-event-hub4.png)
1. Введите имя концентратора событий, а затем щелкните **Создать**.
   
    ![](./media/event-hubs-create/create-event-hub5.png)

Теперь создается концентратора событий и hello строки подключения требуется toosend и получения событий.

## <a name="next-steps"></a>Дальнейшие действия
toolearn Дополнительные сведения о концентраторах событий в следующих статьях:

* [Обзор концентраторов событий](event-hubs-what-is-event-hubs.md)
* [Общие сведения об API концентраторов событий](event-hubs-api-overview.md)

[Azure portal]: https://portal.azure.com/