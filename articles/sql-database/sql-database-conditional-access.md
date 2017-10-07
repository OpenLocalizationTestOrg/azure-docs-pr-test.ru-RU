---
title: "aaaConditional доступ — база данных SQL Azure и хранилище данных | Документ Microsoft"
description: "Дополнительные сведения о том, как tooconfigure условный доступ для базы данных SQL Azure и хранилища данных."
services: sql-database
author: BYHAM
manager: jhubbard
ms.custom: security
ms.service: sql-database
ms.topic: article
ms.date: 06/07/2017
ms.author: rickbyh
ms.openlocfilehash: f49f4708c0f1b3cad1539d630c2efd919f8ece68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="conditional-access-mfa-with-azure-sql-database-and-data-warehouse"></a>Условный доступ (MFA) и база данных SQL Azure и хранилище данных  

База данных SQL и хранилище данных SQL поддерживают условный доступ Майкрософт. Здравствуйте, следующие шаги Показать как база данных SQL tooconfigure tooenforce политику условного доступа.  

## <a name="prerequisites"></a>Предварительные требования  
- Необходимо настроить базу данных SQL или хранилище данных SQL Azure Active Directory аутентификация toosupport. Дополнительные сведения см. в статье [Настройка аутентификации Azure Active Directory и управление ею с использованием базы данных SQL или хранилища данных SQL](sql-database-aad-authentication-configure.md).  
- При включении многофакторной проверки подлинности, необходимо подключиться с в поддерживается в качестве средства, такие как hello последняя версия SSMS. Дополнительные сведения см. в статье [Настройка Многофакторной идентификации Базы данных SQL Azure для SQL Server Management Studio](sql-database-ssms-mfa-authentication-configure.md).  

## <a name="configure-ca-for-azure-sql-dbdw"></a>Настройка центра сертификации для базы данных или хранилища данных SQL Azure  
1.  Вход toohello портала, выберите **Azure Active Directory**, а затем выберите **условного доступа**. Дополнительные сведения см. в статье [Техническая информация об условном доступе в Azure Active Directory](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-conditional-access-technical-reference).  
  ![колонка условного доступа](./media/sql-database-conditional-access/conditional-access-blade.png) 
     
2.  В hello **политики условного доступа** колонка, щелкните **новая политика**, укажите имя и нажмите кнопку **Настройка правил**.  
3.  В разделе **назначения**выберите **пользователей и групп**, проверьте **выберите пользователей и группы**и затем выберите hello пользователя или группу для условного доступа. Нажмите кнопку **выберите**, а затем нажмите кнопку **сделать** tooaccept выбора.  
  ![выбор пользователей и групп](./media/sql-database-conditional-access/select-users-and-groups.png)  

4.  Выберите **Облачные приложения** и щелкните **Выбрать приложения**. Вы увидите все приложения, доступные для условного доступа. Выберите **базы данных SQL Azure**, внизу hello щелкните **выберите**и нажмите кнопку **сделать**.  
  ![выбор базы данных SQL](./media/sql-database-conditional-access/select-sql-database.png)  
  Если не удается найти **базы данных SQL Azure** перечислены в следующих третий снимок экрана приветствия, завершения hello следующие шаги:   
  - Войдите в экземпляр SQL Azure DB/DW tooyour с помощью среды SSMS с учетной записью администратора AAD.  
  - Выполните `CREATE USER [user@yourtenant.com] FROM EXTERNAL PROVIDER`.  
  - Войдите в tooAAD и убедитесь, что база данных SQL Azure и хранилище данных в приложениях hello в службу AAD.  

5.  Выберите **доступа к элементам управления**выберите **Grant**и проверьте hello политику tooapply. Для этого примера мы выберем **Требовать многофакторную проверку подлинности**.  
  ![выбор предоставления доступа](./media/sql-database-conditional-access/grant-access.png)  

## <a name="summary"></a>Сводка  
приложения Hello выбран (база данных SQL Azure), включая tooconnect tooAzure базы данных или хранилища данных SQL с помощью Azure AD Premium теперь реализуется hello выбранной политики условного доступа, **требования многофакторной проверки подлинности.**  
Если у вас есть вопросы о базе данных SQL Azure и хранилище данных в отношении многофакторной проверки подлинности, используйте MFAforSQLDB@microsoft.com.  

## <a name="next-steps"></a>Дальнейшие действия  

Ознакомьтесь с руководством [Защита базы данных SQL Azure](sql-database-security-tutorial.md).
