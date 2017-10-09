---
title: "aaaConfigure многофакторной проверки подлинности — Azure SQL | Документы Microsoft"
description: "Использование Многофакторной идентификации с SSMS для базы данных SQL и хранилища данных SQL."
services: sql-database
documentationcenter: 
author: BYHAM
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: sql-database
ms.custom: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/17/2017
ms.author: rickbyh
ms.openlocfilehash: acb275965f4199f7d5e1378d5077824a9bbc80e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-multi-factor-authentication-for-sql-server-management-studio-and-azure-ad"></a>Настройка Многофакторной идентификации для SQL Server Management Studio и Azure AD

В этом разделе показано, как toouse Azure Active Directory многофакторной проверки подлинности (MFA) с SQL Server Management Studio. Многофакторной проверки Подлинности Azure AD может использоваться при подключении SSMS или SqlPackage.exe tooAzure базы данных SQL и хранилищем данных SQL Azure.

Обзор Многофакторной идентификации базы данных SQL Azure приведен в разделе [Универсальная проверка подлинности для Базы данных SQL и хранилища данных SQL (поддержка SSMS для MFA)](sql-database-ssms-mfa-authentication.md).

## <a name="configuration-steps"></a>Этапы настройки

1. **Настройка Azure Active Directory** — Дополнительные сведения см. в разделе [администрирование каталога Azure AD](https://msdn.microsoft.com/library/azure/hh967611.aspx), [интеграция локальных удостоверений с Azure Active Directory](../active-directory/active-directory-aadconnect.md), [Добавить собственные tooAzure имя домена AD](https://azure.microsoft.com/blog/2012/11/28/windows-azure-now-supports-federation-with-windows-server-active-directory/), [Microsoft Azure теперь поддерживает федерацию с Windows Server Active Directory](https://azure.microsoft.com/blog/2012/11/28/windows-azure-now-supports-federation-with-windows-server-active-directory/), и [управление Azure AD с помощью Windows PowerShell ](https://msdn.microsoft.com/library/azure/jj151815.aspx).
2. **Настройка MFA.** Пошаговые инструкции см. в разделах [Что такое Azure Multi-factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md) и [Условный доступ (MFA) и база данных SQL Azure и хранилище данных](sql-database-conditional-access.md). (Для полнофункционального условного доступа требуется Azure Active Directory (Azure AD) Premium. Azure AD Standard обеспечивает ограниченные возможности MFA).
3. **Настройка базы данных SQL или хранилище данных SQL для проверки подлинности Azure AD** — пошаговые инструкции см. в разделе [tooSQL подключение базы данных или SQL данные хранилища с использованием Azure Active Directory проверки подлинности](sql-database-aad-authentication.md).
4. **Скачать SSMS** — на клиентском компьютере hello, загрузите hello последняя версия SSMS из [загрузить SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/mt238290.aspx). Для всех функций hello в этом разделе используйте по крайней мере июля 2017 г., версия 17,2.  

## <a name="connecting-by-using-universal-authentication-with-ssms"></a>Подключение с помощью универсальной аутентификации и SSMS

Привет, следующие шаги показывают, как tooconnect tooSQL базы данных или хранилища данных SQL с помощью hello последняя версия SSMS.

1. с помощью универсальной проверкой подлинности на hello tooconnect **подключения tooServer** выберите **Active Directory — универсальная с поддержкой многофакторной проверки Подлинности**. (Если вы видите **универсальной проверки подлинности Active Directory** не являются hello последнюю версию SSMS.)  
   ![1mfa-universal-connect][1]  
2. Полный hello **имя пользователя** поле с учетными данными hello Azure Active Directory, в формате hello `user_name@domain.com`.  
   ![1mfa-universal-connect-user](./media/sql-database-ssms-mfa-auth/1mfa-universal-connect-user.png)   
3. При подключении как существование пользователя guest, необходимо нажать кнопку **параметры**и на hello **свойство соединения** диалоговое окно, полный hello **код домена имя или клиента AD** поле. Дополнительные сведения см. в разделе [Универсальная проверка подлинности для Базы данных SQL и хранилища данных SQL (поддержка SSMS для MFA)](sql-database-ssms-mfa-authentication.md).
   ![mfa-tenant-ssms](./media/sql-database-ssms-mfa-auth/mfa-tenant-ssms.png)   
4. В обычном режиме для базы данных SQL и хранилищем данных SQL, необходимо нажать кнопку **параметры** и указать базу данных hello в hello **параметры** диалоговое окно. (Если подключен hello пользователь является гостем (т. е. joe@outlook.com), необходимо установите флажок "hello" и добавить код hello текущего AD домена имя или клиента как часть параметров. Ознакомьтесь с разделом [Универсальная проверка подлинности для Базы данных SQL и хранилища данных SQL (поддержка SSMS для MFA)]()(sql-database-ssms-mfa-authentication.md). Щелкните **Подключить**.  
5. Здравствуйте, когда **tooyour учетная запись для входа** диалоговое окно, укажите учетную запись hello и пароль удостоверения Azure Active Directory. Пароль не требуется, если пользователь является частью домена в федерации с Azure AD.  
   ![2mfa-sign-in][2]  

   > [!NOTE]
   > Если для этой учетной записи не требуется MFA, то на этом этапе универсальной аутентификации устанавливается подключение. Для пользователей, которым нужен многофакторную проверку Подлинности выполните следующие шаги hello.
   >  
   
6. Могут отобразиться два диалоговых окна настройки MFA. Один раз операция зависит от многофакторной проверки Подлинности Здравствуйте, администратор задание и таким образом, может быть необязательным. Для домена включена многофакторной проверки Подлинности этот шаг иногда предварительно определенных (например, hello домена требуется пользователей toouse смарт-карты и ПИН-код).  
   ![3mfa-setup][3]  
7. Здравствуйте, второй можно один раз, диалоговое окно позволяет tooselect hello сведения о методе проверки подлинности. Возможные параметры Hello настраиваются администратором.  
   ![4mfa-verify-1][4]  
8. Hello Azure Active Directory отправляет подтверждение tooyou сведения hello. Получив код проверки hello, введите его в hello **введите код проверки** и нажмите кнопку **входа**.  
   ![5mfa-verify-2][5]  

Обычно по завершении проверки выполняется подключение SSMS при условии, что указаны действительные учетные данные и в брандмауэре разрешен доступ.

## <a name="next-steps"></a>Дальнейшие действия

* Обзор Многофакторной идентификации базы данных SQL Azure приведен в разделе [Универсальная проверка подлинности для Базы данных SQL и хранилища данных SQL (поддержка SSMS для MFA)](sql-database-ssms-mfa-authentication.md).
* Предоставление другим пользователям доступ к базе данных tooyour: [проверки подлинности базы данных SQL и авторизации: предоставление доступа](sql-database-manage-logins.md)  
Убедитесь, что другие пользователи могут подключаться через брандмауэр hello: [Настройка базы данных SQL Azure уровня сервера правило брандмауэра с помощью hello портал Azure](sql-database-configure-firewall-settings.md)


[1]: ./media/sql-database-ssms-mfa-auth/1mfa-universal-connect.png
[2]: ./media/sql-database-ssms-mfa-auth/2mfa-sign-in.png
[3]: ./media/sql-database-ssms-mfa-auth/3mfa-setup.png
[4]: ./media/sql-database-ssms-mfa-auth/4mfa-verify-1.png
[5]: ./media/sql-database-ssms-mfa-auth/5mfa-verify-2.png

