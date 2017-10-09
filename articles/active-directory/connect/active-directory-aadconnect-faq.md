---
title: "Часто задаваемые вопросы по Azure Active Directory Connect | Документация Майкрософт"
description: "На этой странице изложены часто задаваемые вопросы об Azure AD Connect."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
ms.assetid: 4e47a087-ebcd-4b63-9574-0c31907a39a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 39c0b127d3dcf6f45607ad8b4647a9ad79dfc732
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-for-azure-active-directory-connect"></a>Часто задаваемые вопросы по Azure Active Directory Connect

## <a name="general-installation"></a>Общая установка
**Вопрос установки работает, если hello Azure AD глобального администратора имеет 2FA включено?**  
Со сборками hello с февраля 2016 г. Эта функция поддерживается.

**Вопрос. есть ли способ tooinstall автоматической Azure AD Connect?**  
Это только поддерживаемые tooinstall Azure AD Connect с помощью мастера установки hello. Автоматическая и "тихая" установка не поддерживается.

**Вопрос. В лесу есть один домен, с которым нельзя связаться. Как я могу установить Azure AD Connect?**  
Со сборками hello с февраля 2016 г. Эта функция поддерживается.

**Вопрос выполняет hello AD DS работу агента работоспособности на server core?**  
Да. После установки агента hello, необходимо выполнить процесс регистрации hello, используя hello, выполнив командлет PowerShell. 

`Register-AzureADConnectHealthADDSAgent -Credentials $cred`

## <a name="network"></a>Сеть
**Вопрос. у меня брандмауэр, сетевое устройство или то, что ограничивает максимальное время подключения hello может оставаться открытым в моей сети. Каким должно быть пороговое значение времени ожидания на стороне клиента при использовании Azure AD Connect?**  
Все сетевое программное обеспечение, физических устройств или все, что ограничения соединения могут оставаться открытым hello максимальное время следует использовать пороговое значение хотя бы 5 минут (300 секунд) для связи между hello сервера, где hello Azure AD Connect установки клиента и Azure Active Directory. Это также касается средства синхронизации Microsoft Identity tooall ранее были выпущены.

**Вопрос. Поддерживаются ли одноуровневые домены (SLD)?**  
Нет. Azure AD Connect не поддерживает локальные леса и домены, использующие SLD.

**Вопрос. Поддерживаются ли имена NetBIOS "с точками"?**  
"Нет", "Azure AD Connect не поддерживает локального леса и домены где hello NetBIOS-имя содержит точку «.» в имени hello.

## <a name="federation"></a>Федерация
**Вопрос. что делать, если я получаю сообщение электронной почты, спрашивать меня toorenew сертификатов Office 365**  
С помощью руководства по hello, описанных в hello [обновить сертификаты](active-directory-aadconnect-o365-certs.md) раздела справки по как toorenew hello сертификата.

**Вопрос. У меня задан параметр "Automatically update relying party" (Автоматически обновлять проверяющую сторону) для проверяющей стороны Office 365. Нужно ли tootake какие-либо действия при перейдет my автоматически сертификат для подписи маркера?**  
С помощью руководства по hello, описанные в статье hello [обновить сертификаты](active-directory-aadconnect-o365-certs.md).

## <a name="environment"></a>Среда
**Вопрос. есть ИТ поддерживается toorename hello server после установки Azure AD Connect?**  
Нет. Изменение имени сервера hello toonot механизм синхронизации hello причина будет базы данных SQL может tooconnect toohello и hello службы не будет возможности toostart.

## <a name="identity-data"></a>Данные удостоверений
**Вопрос атрибут имени участника-пользователя (userPrincipalName) hello в Azure AD не соответствует hello локального имени участника-пользователя — почему?**  
См. следующие статьи:

* [Имена пользователей не совпадают в Office 365, Azure или Intune hello локального имени участника-пользователя или альтернативному имени пользователя](https://support.microsoft.com/en-us/kb/2523192)
* [Изменения не синхронизированы hello средство синхронизации Azure Active Directory после изменения hello UPN toouse учетной записи пользователя другой федеративный домен](https://support.microsoft.com/en-us/kb/2669550)

Можно также настроить Azure AD tooallow hello синхронизации ядра tooupdate hello userPrincipalName, как описано в [функции службы синхронизации Azure AD Connect](active-directory-aadconnectsyncservice-features.md).

**Вопрос. есть ИТ поддерживается toosoft соответствия локальных объектов AD группы или контакта с существующими объектами Azure AD группы или контакта?**  
Нет, в настоящее время такая возможность не поддерживается.

**Вопрос. есть toomanually ИТ поддерживается атрибуту ImmutableId на существующего Azure AD группы или контакта toohard объекты соответствующим образом tooon локальные объекты "Контакт" / группы AD?**  
Нет, в настоящее время такая возможность не поддерживается.



## <a name="custom-configuration"></a>Настраиваемая конфигурация
**Вопрос. где являются hello командлеты PowerShell для Azure AD Connect задокументированы?**  
За исключением hello hello командлетов, описанных на этом сайте другие командлеты PowerShell в Azure AD Connect не поддерживается для пользователей.

**Вопрос. можно ли использовать сервер или сервер экспорта «Импорт» в *Synchronization Service Manager* toomove конфигурации между серверами?**  
Нет. Этот параметр не получает все параметры конфигурации; его использование не рекомендуется. Вместо этого следует использовать приветствия мастера toocreate hello базовой конфигурации на втором сервере hello и использовать любое настраиваемое правило, между серверами hello редактор правил синхронизации toogenerate toomove сценариев PowerShell. Дополнительные сведения см. в разделе [Обновление со сменой сервера](active-directory-aadconnect-upgrade-previous-version.md#swing-migration).

**Вопрос. можно кэшировать пароли для hello Azure вход страницы и можно это не так как в нем элемент ввода пароля с помощью автозаполнения hello = «false» атрибут?**</br>
Изменение атрибутов HTML hello hello пароль поля ввода, включая hello автозаполнения тег в настоящее время не поддерживается. Настоящий момент мы работаем на функцию, которая позволит пользовательским кодом Javascript, которая допускает tooadd любое поле атрибута toohello пароль. Она должна быть доступна к концу 2017 года.

**Вопрос на hello Azure на странице входа отображаются имена пользователей для пользователей, которые ранее успешного входа.  Можно ли отключить эту функцию?**</br>
Изменение атрибутов hello HTML страницы входа hello в настоящее время не поддерживается. Настоящий момент мы работаем на функцию, которая позволит пользовательским кодом Javascript, которая допускает tooadd любое поле атрибута toohello пароль. Она должна быть доступна к концу 2017 года.

**Вопрос. есть ли способ tooprevent одновременных сеансов?**</br>
Нет.



## <a name="troubleshooting"></a>Устранение неполадок
**Вопрос. Как получить справку по Azure AD Connect?**

[Поиск hello базы знаний Майкрософт (KB)](https://www.microsoft.com/en-us/Search/result.aspx?q=azure%20active%20directory%20connect&form=mssupport)

* Поиск hello базы знаний Майкрософт (KB) для технические решения toocommon устранения неполадок о поддержке Azure AD Connect.

[Форумы по Microsoft Azure Active Directory](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=WindowsAzureAD)

* Можно выполнять поиск и просмотр для технические вопросы и ответы от сообщества hello или задать собственный вопрос, щелкнув [здесь](https://social.msdn.microsoft.com/Forums/azure/en-US/newthread?category=windowsazureplatform&forum=WindowsAzureAD&prof=required).

[Служба поддержки клиентов Azure AD Connect](https://manage.windowsazure.com/?getsupport=true)

* Использование этой поддержки tooget связь через портал Azure hello.

