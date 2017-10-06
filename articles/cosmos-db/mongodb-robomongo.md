---
title: "aaaUse Robomongo для Azure Cosmos DB | Документы Microsoft"
description: "Узнайте, как toouse Robomongo с Azure DB Cosmos: API для MongoDB учетной записи"
keywords: Robomongo
services: cosmos-db
author: AndrewHoh
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: 352c5fb9-8772-4c5f-87ac-74885e63ecac
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: anhoh
ms.openlocfilehash: 3018243e904015426dc69a69b26fb53421e1fe4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-robomongo-with-an-azure-cosmos-db-api-for-mongodb-account"></a>Использование Robomongo с учетной записью API для MongoDB в Azure Cosmos DB
tooconnect tooan Azure Cosmos DB: API для MongoDB учетной записи, с помощью Robomongo необходимо:

* скачать и установить [Robomongo](https://robomongo.org/);
* Подготовить сведения о [строке подключения](connect-mongodb-account.md) для учетной записи API для MongoDB в Azure Cosmos DB.

## <a name="connect-using-robomongo"></a>Подключение с использованием Robomongo
tooadd Cosmos базы данных Azure: API для учетной записи MongoDB toohello Robomongo MongoDB подключений, выполнения hello следующие шаги.

1. Получить Cosmos базы данных Azure: API для MongoDB сведений о соединении учетной записи с помощью инструкций hello [здесь](connect-mongodb-account.md).

    ![Снимок экрана: колонка строка подключения hello](./media/mongodb-robomongo/connectionstringblade.png)
2. Запустите *Robomongo.exe*.

3. Нажмите кнопку подключения hello под **файл** toomanage подключений. Нажмите кнопку **создать** в hello **подключений MongoDB** окна, который будет открыть hello **параметры подключения** окна.

4. В hello **параметры подключения** окно, выберите имя. Найдите hello **узла** и **порт** из данные подключения в шаге 1 и введите их в **адрес** и **порт**соответственно .

    ![Снимок экрана: hello Robomongo Управление соединениями](./media/mongodb-robomongo/manageconnections.png)
5. На hello **проверки подлинности** щелкните **выполнение проверки подлинности**. Затем введите базу данных (по умолчанию — *Admin*), **имя пользователя** и **пароль**.
**Имя пользователя** и **пароль** можно найти в данных подключения, полученных на шаге 1.

    ![Снимок экрана: hello вкладку Robomongo проверки подлинности](./media/mongodb-robomongo/authentication.png)
6. На hello **SSL** установите флажок **протокол SSL используется**, затем измените hello **метод проверки подлинности** слишком**самозаверяющего сертификата**.

    ![Снимок экрана: hello вкладку Robomongo SSL](./media/mongodb-robomongo/SSL.png)
7. Наконец, нажмите кнопку **теста** tooverify, затем являются может tooconnect **Сохранить**.

## <a name="next-steps"></a>Дальнейшие действия
* Ознакомьтесь с [примерами](mongodb-samples.md) API для MongoDB в Azure Cosmos DB.
