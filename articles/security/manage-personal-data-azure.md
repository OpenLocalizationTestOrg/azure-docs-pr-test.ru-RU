---
title: "aaaManage персональные данные в Microsoft Azure | Документы Microsoft"
description: "рекомендации по как toocorrect, обновление, удаление и Экспорт личных данных в Azure Active Directory и база данных SQL Azure"
services: security
documentationcenter: na
author: barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: barclayn
ms.openlocfilehash: 032f70d32377cb9395cb2c35c27dad05001537c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-personal-data-in-microsoft-azure"></a>Управление персональными данными в Microsoft Azure

Эта статья содержит инструкции о том, как toocorrect, обновление, удаление и Экспорт личных данных в Azure Active Directory и база данных SQL Azure.

## <a name="scenario"></a>Сценарий

Компании, на основе Dublin предоставляет комплексное для высокопроизводительной назначения свадьбы Ирландии и вокруг hello world для локальных и международных клиента базы. Они имеют офисов, клиенты, сотрудников и поставщиков, которые расположены по всему hello world toofully службы hello местоположения они предоставляют.

Среди множества других товаров hello компания хранит информацию о ответов на приглашение, включающие аллергией пищевых продуктов и предпочтения по запросу. Гости свадьбу можно зарегистрировать для выполнения различных действий, таких как boat страниц, horseback «riding», и, в т. д. и даже взаимодействовать друг с другом на центральном веб-странице месяцы hello привели toohello событий. Компания Hello собирает личные данные из сотрудников, поставщиков, клиентов и Гости свадьбу. Из-за hello международного характер hello бизнеса hello компании должны соответствовать несколько уровней регулирование.

## <a name="problem-statement"></a>Проблема

- Администраторы данных должны быть может toocorrect неточной личных сведений и неполные или изменяющиеся персональные данные.

- Необходимого Администраторы данных должны быть личные данные могут toodelete по запросу hello данных субъекта.

- Администраторы данных требуется tooexport данных и предоставить ему tooa данных субъекта в формате общего, структурированная по запросу или ее.

## <a name="company-goals"></a>Цели компании

- Компания должна реализовать возможность исправлять или обновлять неточные или неполные персональные данные клиентов, гостей свадьбы, сотрудников и поставщиков в Azure Active Directory и базе данных SQL Azure.

- Персональные данные должны быть удалены по запросу hello данных субъекта в Azure Active Directory и база данных SQL Azure.

- Персональные данные необходимо экспортировать в формате общего, структурированная по запросу hello данных субъекта.

## <a name="solutions"></a>Решения

### <a name="azure-active-directory-rectifycorrect-inaccurate-or-incomplete-personal-data-and-erasedelete-personal-datauser-profiles"></a>Изменение неверных или неполных персональных данных и удаление персональных данных и профилей пользователей в Azure Active Directory

[Azure Active Directory](https://azure.microsoft.com/services/active-directory/) — это мультитенантный облачный каталог и служба управления удостоверениями Майкрософт.
Исправления, обновления или удаления клиентов и профилей пользователей и информация о работы пользователя, содержат личные данные, такие как имя пользователя, должность, адрес или номер телефона в вашей [Azure Active Directory](https://azure.microsoft.com/services/active-directory/) (AAD) среды с помощью hello [портал Azure](https://portal.azure.com/).

Необходимо войти с учетной записью глобального администратора каталога hello.

#### <a name="how-do-i-correct-or-update-user-profile-and-work-information-in-azure-active-directory"></a>Исправление или обновление профиля пользователя и сведений о работе в Azure Active Directory

1. Войдите в toohello [портал Azure](https://portal.azure.com) с помощью учетной записи глобального администратора каталога hello.

2. Выберите **дополнительные службы**, введите **пользователей и групп** в hello текстовое поле, а затем выберите **ввод**.

    ![media/image1.png](media/manage-personal-data-azure/image001.png)

3. На hello **пользователей и групп** колонке выберите **пользователей**.

    ![media/image2.png](media/manage-personal-data-azure/image003.png)

4. На hello **пользователей и групп - Пользователи** колонке выберите пользователя из списка hello и выберите в колонке hello для выбранного пользователя hello, **профиль** tooview hello сведений профиля, необходимо исправить toobe или обновленный.

    ![media/image3.png](media/manage-personal-data-azure/image005.png)

5. Исправьте или обновить сведения о hello и выберите на панели команд hello, **сохранить.**

6.  В колонке hello для выбранного пользователя hello, выберите **сведения о работе** tooview пользователя рабочие данные, необходимые toobe Исправлено или обновлен.

    ![media/image4.png](media/manage-personal-data-azure/image007.png)

7. Исправьте или обновить сведения о рабочих пользователя hello и выберите на панели команд hello, **сохранить.**

#### <a name="how-do-i-delete-a-user-profile-in-azure-active-directory"></a>Удаление профиля пользователя в Azure Active Directory

1. Войдите в toohello [портал Azure](https://portal.azure.com) с помощью учетной записи глобального администратора каталога hello.

2. Выберите **дополнительные службы**, введите **пользователей и групп** в hello текстовое поле, а затем выберите **ввод**.

    ![](media/manage-personal-data-azure/image001.png)

3. На hello **пользователей и групп** колонке выберите **пользователей**.

    ![media/image2.png](media/manage-personal-data-azure/image003.png)

4. На hello **пользователей и групп — пользователей** колонке выберите пользователя из списка hello.

    ![media/image3.png](media/manage-personal-data-azure/image007.png)

5. В колонке hello для выбранного пользователя hello, выберите **Обзор**и выберите в панели команд hello, **удалить**.

    ![](media/manage-personal-data-azure/image013.png)

### <a name="sql-database-rectifycorrect-inaccurate-or-incomplete-personal-data-erasedelete-personal-data-export-personal-data"></a>Удаление, экспорт и изменение неверных или неполных персональных данных в базе данных SQL 

[База данных SQL Azure](https://azure.microsoft.com/services/sql-database/?v=16.50) — это облачная база данных, позволяющая разработчикам создавать приложения и управлять ими.

Персональные данные в [базе данных SQL Azure](https://azure.microsoft.com/services/sql-database/?v=16.50) можно обновить с помощью стандартных запросов SQL, а также удалить. Кроме того персональные данные можно экспортировать из базы данных SQL с помощью различных методов, включая hello импорта Azure SQL Server и мастер экспорта и в различных форматах, включая файл BACPAC.

#### <a name="how-do-i-correct-update-or-erase-personal-data-in-sql-database"></a>Исправление, обновление и удаление персональных данных в базе данных SQL

toolearn как toocorrect или обновление персональные данные в базе данных SQL, посетите hello [обновления (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/queries/update-transact-sql), [обновить текст](https://docs.microsoft.com/sql/t-sql/queries/updatetext-transact-sql), [обновление обобщенного табличного выражения with](https://docs.microsoft.com/sql/t-sql/queries/with-common-table-expression-transact-sql), или [ Обновление записи текста](https://docs.microsoft.com/sql/t-sql/queries/writetext-transact-sql) документации.

toolearn как toodelete персональные данные в базе данных SQL, посетите hello [удалить (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/statements/delete-transact-sql) документации.

#### <a name="how-do-i-export-personal-data-tooa-bacpac-file-in-sql-database"></a>Экспорт файла BACPAC tooa персональные данные в базе данных SQL

BACPAC-файл включает hello SQL базы данных и метаданных и ZIP-файл с расширением BACPAC. Это можно сделать с помощью hello [портал Azure](https://portal.azure.com/), hello SQLPackage программы командной строки, SQL Server Management Studio (SSMS) или PowerShell.

toolearn как tooexport данных tooa BACPAC-файл, посетите hello [Экспорт файла BACPAC tooa базы данных Azure SQL](https://docs.microsoft.com/azure/sql-database/sql-database-export) страницу, содержащую подробные инструкции для каждого из перечисленных выше методов.

Экспорт персональные данные из базы данных SQL с SQL Server Import hello и мастер экспорта

Этот мастер помогает скопировать данные из источника tooa назначения. Общие сведения мастера toohello, включая как tooget ее, сведения о разрешениях и помощь tooget с помощью средства hello посетите hello [и экспорт данных с SQL Server Import hello мастер импорта и экспорта](https://docs.microsoft.com/sql/integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard) веб-страницы.

Общие сведения о стадии приветствия мастера посетите hello [шагов в hello импорта SQL Server и мастер экспорта](https://docs.microsoft.com/sql/integration-services/import-export-data/steps-in-the-sql-server-import-and-export-wizard) веб-страницы.

## <a name="next-steps"></a>Дальнейшие действия

[База данных SQL Azure;](https://azure.microsoft.com/services/sql-database/?v=16.50) 

[Azure Active Directory](https://azure.microsoft.com/services/active-directory/)

