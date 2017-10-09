---
title: "aaaManage учетную запись Azure Cosmos DB через hello портал Azure | Документы Microsoft"
description: "Узнайте, как toomanage базы данных Azure Cosmos учетной записи через портал Azure hello. Найти руководство по использованию tooview hello портал Azure, копирования, удаления и доступа учетных записей."
keywords: "Портал Azure, DocumentDB, Azure, Microsoft Azure"
services: cosmos-db
documentationcenter: 
author: kirillg
manager: jhubbard
editor: cgronlun
ms.assetid: 00fc172f-f86c-44ca-8336-11998dcab45c
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: kirillg
ms.openlocfilehash: 77ad953cf558a519674be08ad913a12202f69496
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-an-azure-cosmos-db-account"></a>Как toomanage учетную запись Azure Cosmos DB
Узнайте, как работать с ключами tooset глобальной согласованности и удалить учетную запись Azure Cosmos DB в hello портал Azure.

## <a id="consistency"></a>Управление параметрами согласованности Azure Cosmos DB
При выборе уровня согласованности правой hello зависит от hello семантику приложения. Следует ознакомиться с уровнями hello доступных согласованности в базе данных Azure Cosmos, считывая [согласованности с помощью уровней toomaximize доступности и производительности в базе данных Azure Cosmos][consistency]. Azure Cosmos DB предоставляет гарантии согласованности, доступности и производительности для любого уровня согласованности, доступного учетной записи базы данных. Настройка учетной записи базы данных с уровнем достоверности строгих требует данных пропущенные tooa один регион Azure, но не глобально доступны. На Здравствуйте другой стороны, hello уровни согласованности ослабленной - ограниченным устареванием, session или окончательной enable вы tooassociate любое количество областей Azure с вашей учетной записи базы данных. Привет, выполнив простые действия показывают, как tooselect hello уровень согласованности по умолчанию для учетной записи базы данных. 

### <a name="toospecify-hello-default-consistency-for-an-azure-cosmos-db-account"></a>согласованность по умолчанию hello toospecify для учетной записи Azure Cosmos DB
1. В hello [портал Azure](https://portal.azure.com/), доступ к учетной записи Azure Cosmos DB.
2. В колонке hello учетной записи, нажмите кнопку **по умолчанию согласованности**.
3. В hello **согласованности по умолчанию** колонки, новый уровень согласованности выберите hello и нажмите кнопку **Сохранить**.
    ![Сеанс согласованности по умолчанию][5]

## <a id="keys"></a>Просмотр, копирование и повторное создание ключей доступа
При создании учетной записи Azure Cosmos DB hello service создает два ключа master доступа, которые могут использоваться для проверки подлинности при доступе к учетной записи Azure Cosmos DB hello. Предоставляя два ключа доступа, Azure Cosmos DB включает ключи hello tooregenerate с без прерывания tooyour учетная запись Azure Cosmos DB. 

В hello [портал Azure](https://portal.azure.com/), hello доступа **ключей** колонки ресурсов меню hello hello **учетная запись Azure Cosmos DB** tooview колонки, копирования и повторное создание hello ключей доступа — Это используемые tooaccess учетной записи Azure Cosmos DB.

![Снимок экрана портала Azure, колонка «Ключи»](./media/manage-account/keys.png)

> [!NOTE]
> Hello **ключей** колонке также включает первичный и строки соединения получателей, которые можно использовать tooconnect tooyour учетной записи из hello [средство переноса данных](import-data.md).
> 
> 

В этой колонке также доступны ключи только для чтения. Чтение и запросы являются операциями только для чтения, а создание, удаление и замена — нет.

### <a name="copy-an-access-key-in-hello-azure-portal"></a>Скопируйте ключ доступа в hello портала Azure
На hello **ключей** колонка, щелкните hello **копирования** toohello кнопку справа от ключа hello нужно toocopy.

![Просмотр и копирование клавиши доступа в hello портал Azure, ключи колонку](./media/manage-account/copykeys.png)

### <a name="regenerate-access-keys"></a>Повторное создание ключей доступа
Следует изменить учетную запись Azure Cosmos DB tooyour ключи доступа hello периодически toohelp безопасность подключений. Два ключа доступа, назначенные tooenable вы toomaintain подключений toohello с помощью одного ключа доступа при повторном создании учетной записи Azure Cosmos DB hello другого ключа доступа.

> [!WARNING]
> Повторное создание ключей доступа влияет на все приложения, которые зависят от текущего ключа hello. Все клиенты, использующие учетную запись Azure Cosmos DB hello hello доступа tooaccess ключа должен быть обновленные toouse hello новый ключ.
> 
> 

При наличии приложения или облачные службы с использованием учетной записи Azure Cosmos DB hello, будут потеряны hello подключений при повторном создании ключей, если откат ключей. Hello ниже описывается процесс hello, участвующих в развертывании вашего ключей.

1. Обновите ключ доступа hello в вашего приложения код tooreference hello вторичный ключ доступа для учетной записи Azure Cosmos DB hello.
2. Повторное создание hello первичный ключ доступа для учетной записи Azure Cosmos DB. В hello [портала Azure](https://portal.azure.com/), доступ к учетной записи Azure Cosmos DB.
3. В hello **учетную запись Azure Cosmos DB** колонка, щелкните **ключей**.
4. На hello **ключей** колонке нажмите кнопку повторное создание hello, а затем нажмите кнопку **ОК** tooconfirm, что требуется toogenerate новый ключ.
    ![Повторное создание ключей доступа](./media/manage-account/regenerate-keys.png)
5. После проверки того, что новый ключ, hello доступна для использования (около 5 минут после нее), обновить ключ доступа hello в приложение код tooreference hello новый первичный ключ доступа.
6. Повторное создание hello вторичный ключ доступа.
   
    ![Повторное создание ключей доступа](./media/manage-account/regenerate-secondary-key.png)

> [!NOTE]
> Он может занять несколько минут перед tooaccess используется вновь созданный ключ учетной записи Azure Cosmos DB.
> 
> 

## <a name="get-hello--connection-string"></a>Получить строку подключения hello
tooretrieve подключение строка, hello следующие: 

1. В hello [портал Azure](https://portal.azure.com), доступ к учетной записи Azure Cosmos DB.
2. В меню ресурса hello, щелкните **ключей**.
3. Щелкните hello **копирования** кнопку Далее toohello **основной строка подключения** или **вторичная строка подключения** поле. 

Если вы используете строку подключения hello hello [Миграция в Azure DB Cosmos базы данных](import-data.md), добавьте hello базы данных имя toohello конец строки подключения hello. `AccountEndpoint=< >;AccountKey=< >;Database=< >`.

## <a id="delete"></a>Удаление учетной записи Azure Cosmos DB
tooremove Cosmos Azure DB учетной записи из hello портал Azure, больше не используется, имя учетной записи щелкните правой кнопкой мыши hello и нажмите кнопку **удалить учетную запись**.

![Как toodelete Cosmos Azure DB учетной записи в hello портала Azure](./media/manage-account/deleteaccount.png)

1. В hello [портал Azure](https://portal.azure.com/), доступ к учетной записи Azure Cosmos DB hello, нужно toodelete.
2. На hello **учетная запись Azure Cosmos DB** колонка, щелкните правой кнопкой мыши учетную запись hello и нажмите кнопку **удаление учетной записи**. 
3. Hello полученный колонке подтверждения введите, требуется учетная запись hello toodelete имя tooconfirm hello Azure Cosmos DB учетной записи.
4. Нажмите кнопку hello **удалить** кнопки.

![Как toodelete Cosmos Azure DB учетной записи в hello портала Azure](./media/manage-account/delete-account-confirm.png)

## <a id="next"></a>Дальнейшие действия
Узнайте, каким образом слишком[приступить к работе с учетной записью Azure Cosmos DB](http://go.microsoft.com/fwlink/p/?LinkId=402364).

<!--Image references-->
[5]: ./media/manage-account/documentdb_change_consistency-1.png

<!--Reference style links - using these makes hello source content way more readable than using inline links-->
[bcdr]: https://azure.microsoft.com/documentation/articles/best-practices-availability-paired-regions/
[consistency]: consistency-levels.md
[azureregions]: https://azure.microsoft.com/regions/#services
[offers]: https://azure.microsoft.com/pricing/details/cosmos-db/
