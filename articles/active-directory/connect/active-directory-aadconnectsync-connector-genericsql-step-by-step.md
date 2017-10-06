---
title: "шаг aaaGeneric шаг по соединителя SQL | Документы Microsoft"
description: "В этой статье пошагового прохода через простую систему HR пошаговые с помощью hello универсальный соединитель SQL."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 28c1cc60-24fd-4d0d-a36d-b4aba6de86e7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: b1b5f89ab588de6f92f173a7bc00f97180067669
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="generic-sql-connector-step-by-step"></a>Универсальный соединитель SQL: пошаговое руководство
Эта статья является пошаговым руководством. Она поможет вам создать простую базу данных для отдела кадров, которая предназначена для импорта некоторых пользователей и их членства в группе.

## <a name="prepare-hello-sample-database"></a>Подготовка базы данных образец hello
На сервер SQL Server, выполните сценарий SQL hello в [приложение A](#appendix-a). Этот скрипт создает образец базы данных с именем hello GSQLDEMO. Hello объектная модель для hello создания базы данных выглядит на этом рисунке:  
![Объектная модель](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/objectmodel.png)

Также можно создайте пользователя базы данных toohello tooconnect toouse. В этом пошаговом руководстве пользователя hello вызывается FABRIKAM\SQLUser и находиться в домене, hello.

## <a name="create-hello-odbc-connection-file"></a>Создание файла соединения ODBC hello
Hello универсальный соединитель SQL использует ODBC tooconnect toohello удаленного сервера. Сначала нужно toocreate файл, содержащий сведения о соединении ODBC hello.

1. Запуск программы управления hello ODBC на сервере:  
   ![ODBC](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc.png)
2. Выберите hello вкладку **файловый DSN**. Щелкните **Add...**(Добавить).  
   ![ODBC 1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc1.png)
3. Hello работает драйвер out-of-box прекрасная, поэтому выберите его и щелкните **Далее >**.  
   ![ODBC 2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc2.png)
4. Имя файла hello, таких как **GenericSQL**.  
   ![ODBC 3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc3.png)
5. Нажмите кнопку **Finish**(Готово).  
   ![ODBC 4](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc4.png)
6. Соединения hello tooconfigure времени. Укажите источник данных hello Хорошее описание и укажите имя hello hello сервера SQL Server.  
   ![ODBC 5](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc5.png)
7. Выбор метода tooauthenticate с SQL. В нашем примере используется проверка подлинности Windows.  
   ![ODBC 6](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc6.png)
8. Укажите имя hello hello образца базы данных, **GSQLDEMO**.  
   ![ODBC 7](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc7.png)
9. На этом экране оставьте настройки по умолчанию. Нажмите кнопку **Finish**(Готово).  
   ![ODBC 8](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc8.png)
10. Щелкните tooverify все работает, как ожидалось, **тестового источника данных**.  
    ![ODBC 9](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc9.png)
11. Убедитесь, что hello проверка прошла успешно.  
    ![ODBC 10](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc10.png)
12. файл конфигурации ODBC Hello, теперь должны быть видимыми в файловый DSN.  
    ![ODBC 11](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc11.png)

Теперь у нас есть файл hello нам нужна и можно приступить к созданию hello соединителя.

## <a name="create-hello-generic-sql-connector"></a>Создать hello универсальный соединитель SQL
1. В hello пользовательского интерфейса диспетчера службы синхронизации, выберите **соединители** и **создать**. Выберите **Generic SQL (Microsoft)** (Универсальный SQL (Майкрософт)) и присвойте описательное имя.  
   ![Соединитель 1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector1.png)
2. Найдите файл DSN hello, созданный в предыдущем разделе hello и выгрузить его toohello сервера. Укажите учетные данные tooconnect hello toohello-базы данных.  
   ![Соединитель 2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector2.png)
3. В этом пошаговом руководстве мы упростим процесс и предположим, что существует два типа объектов: **User** и **Group**.
   ![Соединитель 3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector3.png)
4. атрибуты toofind hello, мы хотим hello соединитель toodetect те атрибуты, посмотрев на саму таблицу hello. Поскольку **пользователей** является зарезервированным словом в SQL, нам нужно tooprovide его в квадратные скобки [].  
   ![Соединитель 4](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector4.png)
5. Время toodefine hello привязки атрибута и атрибута DN hello. Для **пользователей**, мы используем hello сочетание имени пользователя hello двух атрибутов и EmployeeID. Для **Group**мы используем GroupName (не слишком реалистично для обычной жизни, но подойдет для этого руководства).
   ![Соединитель 5](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector5.png)
6. В базе данных SQL могут быть обнаружены только некоторые типы атрибутов. в частности невозможно Hello ссылочного типа атрибута. Тип объекта группы hello нам нужна toochange hello OwnerID и MemberID tooreference.  
   ![Соединитель 6](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector6.png)
7. атрибуты Hello мы выбрали как атрибуты этих ссылок на предыдущем шаге hello требуются эти значения являются ссылку на объект типа hello. В нашем случае hello тип объекта пользователя.  
   ![Соединитель 7](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector7.png)
8. На странице приветствия глобальные параметры, выберите **водяной знак** в рамках стратегии дельта hello. Также вводить в формате даты и времени hello **гггг мм дд чч**.
   ![Соединитель 8](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector8.png)
9. На hello **Настройка разделов и иерархий** выберите оба типа объектов.
   ![Соединитель 9](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector9.png)
10. На hello **Выбор типов объектов** и **Выбор атрибутов**, выберите типы объектов и атрибуты. На hello **Настройка привязки** щелкните **Готово**.

## <a name="create-run-profiles"></a>Создание профилей выполнения
1. В hello пользовательского интерфейса диспетчера службы синхронизации, выберите **соединители**, и **Настройка профилей выполнения**. Щелкните **New Profile**(Новый профиль). Мы начнем с профиля **Full Import**(Полный импорт).  
   ![Профиль выполнения 1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile1.png)
2. Выберите тип hello **полный импорт (только для этапа)**.  
   ![Профиль выполнения 2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile2.png)
3. Выберите секцию hello **объект = пользователь**.  
   ![Профиль выполнения 3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile3.png)
4. Выберите **Table** и введите **[USERS]**. Прокрутите вниз toohello разделе типа объекта с несколькими значениями и ввод данных hello как hello следующий рисунок. Выберите **Готово** toosave hello шаг.  
   ![Профиль выполнения 4а](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4a.png)  
   ![Профиль выполнения 4б](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4b.png)  
5. Выберите **New Step**(Новый шаг). На этот раз выберите **OBJECT=Group**. На последней странице hello используйте конфигурации hello как hello следующий рисунок. Нажмите кнопку **Готово**  
   ![Профиль выполнения 5а](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5a.png)  
   ![Профиль выполнения 5б](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5b.png)  
6. Можно настроить дополнительные профили выполнения, но это необязательно. В этом пошаговом руководстве используется только hello полный импорт.
7. Нажмите кнопку **ОК** toofinish изменение профилей выполнения.

## <a name="add-some-test-data-and-test-hello-import"></a>Добавить некоторые Импорт теста данные и тестирования hello
Введите тестовые данные в образец базы данных. Когда будете готовы, щелкните **Run** (Выполнить) и **Full import** (Полный импорт).

Здесь мы видим пользователя с двумя телефонными номерами и группу с несколькими участниками.  
![Пространство соединителя 1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/cs1.png)  
![Пространство соединителя 2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/cs2.png)  

## <a name="appendix-a"></a>Приложении A
**Сценарий toocreate hello образцы базы данных SQL**

```SQL
---Creating hello Database---------
Create Database GSQLDEMO
Go
-------Using hello Database-----------
Use [GSQLDEMO]
Go
-------------------------------------
USE [GSQLDEMO]
GO
/****** Object:  Table [dbo].[GroupMembers]   ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[GroupMembers](
    [MemberID] [int] NOT NULL,
    [Group_ID] [int] NOT NULL
) ON [PRIMARY]

GO
/****** Object:  Table [dbo].[GROUPS]   ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[GROUPS](
    [GroupID] [int] NOT NULL,
    [GROUPNAME] [nvarchar](200) NOT NULL,
    [DESCRIPTION] [nvarchar](200) NULL,
    [WATERMARK] [datetime] NULL,
    [OwnerID] [int] NULL,
PRIMARY KEY CLUSTERED
(
    [GroupID] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]
) ON [PRIMARY]

GO
/****** Object:  Table [dbo].[USERPHONE]   ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
SET ANSI_PADDING ON
GO
CREATE TABLE [dbo].[USERPHONE](
    [USER_ID] [int] NULL,
    [Phone] [varchar](20) NULL
) ON [PRIMARY]

GO
SET ANSI_PADDING OFF
GO
/****** Object:  Table [dbo].[USERS]   ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[USERS](
    [USERID] [int] NOT NULL,
    [USERNAME] [nvarchar](200) NOT NULL,
    [FirstName] [nvarchar](100) NULL,
    [LastName] [nvarchar](100) NULL,
    [DisplayName] [nvarchar](100) NULL,
    [ACCOUNTDISABLED] [bit] NULL,
    [EMPLOYEEID] [int] NOT NULL,
    [WATERMARK] [datetime] NULL,
PRIMARY KEY CLUSTERED
(
    [USERID] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]
) ON [PRIMARY]

GO
ALTER TABLE [dbo].[GroupMembers]  WITH CHECK ADD  CONSTRAINT [FK_GroupMembers_GROUPS] FOREIGN KEY([Group_ID])
REFERENCES [dbo].[GROUPS] ([GroupID])
GO
ALTER TABLE [dbo].[GroupMembers] CHECK CONSTRAINT [FK_GroupMembers_GROUPS]
GO
ALTER TABLE [dbo].[GroupMembers]  WITH CHECK ADD  CONSTRAINT [FK_GroupMembers_USERS] FOREIGN KEY([MemberID])
REFERENCES [dbo].[USERS] ([USERID])
GO
ALTER TABLE [dbo].[GroupMembers] CHECK CONSTRAINT [FK_GroupMembers_USERS]
GO
ALTER TABLE [dbo].[GROUPS]  WITH CHECK ADD  CONSTRAINT [FK_GROUPS_USERS] FOREIGN KEY([OwnerID])
REFERENCES [dbo].[USERS] ([USERID])
GO
ALTER TABLE [dbo].[GROUPS] CHECK CONSTRAINT [FK_GROUPS_USERS]
GO
ALTER TABLE [dbo].[USERPHONE]  WITH CHECK ADD  CONSTRAINT [FK_USERPHONE_USER] FOREIGN KEY([USER_ID])
REFERENCES [dbo].[USERS] ([USERID])
GO
ALTER TABLE [dbo].[USERPHONE] CHECK CONSTRAINT [FK_USERPHONE_USER]
GO
```
