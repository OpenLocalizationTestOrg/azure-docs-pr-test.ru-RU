---
title: "aaaUse сервера Azure MFA с AD FS 2.0 | Документы Microsoft"
description: "Это страница hello Azure многофакторной проверки подлинности, описывающий, как tooget работу с Azure MFA и AD FS 2.0."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 96168849-241a-4499-a224-d829913caa7e
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/14/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: H1Hack27Feb2017, it-pro
ms.openlocfilehash: 15011a94ca69dc6e51aa3edf74f5db6cd44d697a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-multi-factor-authentication-server-toowork-with-ad-fs-20"></a>Настроить toowork сервера Azure Multi-factor Authentication с AD FS 2.0
Эта статья предназначена для организаций, которые включаются в федерацию с Azure Active Directory, а также toosecure ресурсы, которые находятся в локальной среде или в облаке hello. Защитить ресурсы, с помощью сервера Azure Multi-factor Authentication hello и настроить его toowork с AD FS, чтобы выполнялась двухшаговую проверку для ценных конечных точек.

Использование hello сервера Azure Multi-factor Authentication с AD FS 2.0 входит в эту документацию. Дополнительные сведения о службах AD FS см. в статье [Защита облачных и локальных ресурсов с помощью сервера Многофакторной идентификации Azure со службами федерации Active Directory в Windows Server 2012 R2](multi-factor-authentication-get-started-adfs-w2k12.md).

## <a name="secure-ad-fs-20-with-a-proxy"></a>Защита AD FS 2.0 с помощью прокси-сервера
toosecure AD FS 2.0 с помощью прокси-сервера, установите hello сервера Azure Multi-factor Authentication на прокси-сервер hello AD FS.

### <a name="configure-iis-authentication"></a>Настройка проверки подлинности IIS
1. В hello Azure многофакторной проверки подлинности сервера, щелкните hello **проверки подлинности IIS** значок в левом меню hello.
2. Нажмите кнопку hello **форм** вкладки.
3. Щелкните **Добавить**.

   <center>![Настройка](./media/multi-factor-authentication-get-started-adfs-adfs2/setup1.png)</center>

4. имя пользователя, пароль и домен переменные toodetect автоматически, введите hello URL-адрес входа (например, https://sso.contoso.com/adfs/ls) в диалоговом окне приветствия Автонастройка веб-сайта и нажмите кнопку **ОК**.
5. Проверьте hello **сопоставление пользователей требуется многофакторная проверка подлинности Azure** поле, если все пользователи были или будут импортированы в hello сервера и проверки tootwo шаг субъекта. Если значительное число пользователей еще не были импортированы в сервер hello или будут исключены из двухшаговую проверку, не hello флажок.
6. Если переменные страницы приветствия не определяются автоматически, нажмите кнопку hello **вручную указать...** Кнопка в диалоговом окне приветствия Автонастройка веб-сайта.
7. В основе форм веб-сайт диалоговое окно «hello» введите страницы входа toohello AD FS для hello URL-адрес в поле URL-адреса отправки hello (например, https://sso.contoso.com/adfs/ls) и введите имя приложения (необязательно). Имя приложения Hello отображается в отчетах Azure Multi-factor Authentication и может отображаться в SMS или мобильное приложение проверки подлинности сообщений.
8. Задать формат запроса hello слишком**POST или GET**.
9. Введите переменную Username hello (ctl00$ ContentPlaceHolder1$ UsernameTextBox) и переменную Password (ctl00$ ContentPlaceHolder1$ PasswordTextBox). Если страница входа на основе форм отображается текстовое поле для домена, введите также hello локальных переменных. имена hello toofind hello полей ввода на странице входа hello перейдите toohello страницы входа в веб-браузере, щелкните правой кнопкой мыши на странице приветствия и выберите **Просмотр исходного кода**.
10. Проверьте hello **сопоставление пользователей требуется многофакторная проверка подлинности Azure** поле, если все пользователи были или будут импортированы в hello сервера и проверки tootwo шаг субъекта. Если значительное число пользователей еще не были импортированы в сервер hello или будут исключены из двухшаговую проверку, не hello флажок.
    <center>![Настройка](./media/multi-factor-authentication-get-started-adfs-adfs2/manual.png)</center>
11. Нажмите кнопку **Дополнительно…**, tooreview Дополнительные параметры. Вы можете сделать следующие настройки:

    - выбрать специальный файл страницы отказа;
    - Веб-кэша успешных проверок подлинности toohello сайта с помощью файлов cookie
    - Выберите, каким образом tooauthenticate hello основных учетных данных

12. Поскольку hello AD FS прокси-сервер не скорее всего toobe присоединен к домену toohello, контроллер домена tooyour tooconnect LDAP можно использовать для импорта пользователей и предварительной проверки подлинности. В веб-сайт на диалоговое окно «hello», щелкните hello **основной проверки подлинности** и выберите **LDAP Bind** для hello тип предварительной проверки подлинности.
13. По завершении нажмите кнопку **ОК** tooreturn toohello основе форм веб-сайт диалоговое окно «».
14. Нажмите кнопку **ОК** hello tooclose-диалоговое окно.
15. Один раз hello URL-адрес и обнаружения или ввода переменные страницы, данные hello веб-сайта отображается в hello панели на основе форм.
16. Нажмите кнопку hello **собственный модуль** вкладку и выберите сервер hello, hello веб-сайт, на котором hello AD FS прокси-сервер работает в группе (такие как «Default Web Site»), или hello AD FS прокси-сервера (например, «ls» под «adfs») tooenable hello подключаемый модуль на приветствия IIS требуемый уровень.
17. Нажмите кнопку hello **проверки подлинности IIS включить** поле вверху hello экран приветствия.

Теперь включена проверка подлинности IIS Hello.

### <a name="configure-directory-integration"></a>Настройка интеграции каталогов
После включения проверки подлинности IIS, но tooyour предварительной проверки подлинности Active Directory (AD) посредством LDAP необходимо настроить для tooperform hello hello контроллер домена toohello подключения LDAP.

1. Нажмите кнопку hello **Интеграция каталогов** значок.
2. На вкладке Параметры hello выберите hello **использовать определенную конфигурацию LDAP** переключатель.

   <center>![Настройка](./media/multi-factor-authentication-get-started-adfs-adfs2/ldap1.png)</center>

3. Нажмите кнопку **Изменить**.
4. В диалоговом окне изменения конфигурации LDAP hello заполните поля hello с контроллером домена toohello AD tooconnect необходимые сведения hello. Описания полей hello включаются в файл справки сервера Azure Multi-factor Authentication hello.
5. Проверьте подключение LDAP hello, щелкнув hello **тест** кнопки.

   <center>![Настройка](./media/multi-factor-authentication-get-started-adfs-adfs2/ldap2.png)</center>

6. Если проверка подключения LDAP hello выполнена успешно, нажмите кнопку **ОК**.

### <a name="configure-company-settings"></a>Настройка параметров организации
1. Затем щелкните hello **параметры компании** значок и выберите hello **разрешение имени пользователя** вкладки.
2. Выберите hello **атрибут уникального идентификатора LDAP используется для сопоставления имен пользователей** переключатель.
3. Если пользователь введет свое имя пользователя в формате «домен\имя_пользователя», hello Server должен домена hello может toostrip toobe сеанса имя_пользователя hello при создании запроса LDAP hello. Это можно сделать с помощью параметра реестра.
4. Откройте редактор реестра hello и перейти tooHKEY_LOCAL_MACHINE/SOFTWARE/Wow6432Node/Positive сетей/PhoneFactor на 64-разрядном сервере. Если 32-разрядном сервере, отключите hello «Wow6432Node» из пути hello. Создайте значение DWORD реестра называется «UsernameCxz_stripPrefixDomain» и задайте значение too1 hello. Azure Multi-factor Authentication теперь обеспечивает безопасность прокси-сервера AD FS hello.

Убедитесь, что пользователи были импортированы из Active Directory в hello Server. . В разделе hello [раздел надежных IP-адресов](#trusted-ips) Если вы хотите toowhitelist внутренние IP-адреса, чтобы при входе в веб-сайт toohello таким образом двухшаговую проверку не требуется.

<center>![Настройка](./media/multi-factor-authentication-get-started-adfs-adfs2/reg.png)</center>

## <a name="ad-fs-20-direct-without-a-proxy"></a>AD FS 2.0 без прокси-сервера (напрямую)
Если не используется прокси-сервера hello AD FS можно защитить службы федерации Active Directory. Установка hello сервера Azure Multi-factor Authentication на сервере AD FS hello и настройка приветствия сервера на приветствия следующие шаги:

1. В рамках hello Azure многофакторной проверки подлинности сервера, щелкните hello **проверки подлинности IIS** значок в левом меню hello.
2. Нажмите кнопку hello **HTTP** вкладки.
3. Щелкните **Добавить**.
4. В диалоговое окно приветствия добавить базовый URL-адрес введите URL-адрес hello hello AD FS веб-сайта, где выполняется проверка подлинности HTTP (например, https://sso.domain.com/adfs/ls/auth/integrated) в поле hello базовый URL-адрес. Затем введите имя приложения (необязательно). Имя приложения Hello отображается в отчетах Azure Multi-factor Authentication и может отображаться в SMS или мобильное приложение проверки подлинности сообщений.
5. При желании задайте время ожидания простоя hello и максимальное время сеанса.
6. Проверьте hello **сопоставление пользователей требуется многофакторная проверка подлинности Azure** поле, если все пользователи были или будут импортированы в hello сервера и проверки tootwo шаг субъекта. Если значительное число пользователей еще не были импортированы в сервер hello или будут исключены из двухшаговую проверку, не hello флажок.
7. Установите флажок кэша cookie hello, при необходимости.

   <center>![Настройка](./media/multi-factor-authentication-get-started-adfs-adfs2/noproxy.png)</center>

8. Нажмите кнопку **ОК**.
9. Нажмите кнопку hello **собственный модуль** вкладку и выберите hello server, hello веб-сайта (такие как «Default Web Site») или hello службы федерации Active Directory (например, «ls» под «adfs») tooenable hello подключаемый модуль на приветствия IIS требуемого уровня.
10. Нажмите кнопку hello **проверки подлинности IIS включить** поле вверху hello экран приветствия.

После этого Многофакторная идентификация Azure будет защищать AD FS.

Убедитесь, что пользователи были импортированы из Active Directory в hello Server. В разделе hello разделе надежных IP-адресов, если вы хотите toowhitelist внутренний IP-адрес адреса, чтобы при входе в веб-сайт toohello таким образом двухшаговую проверку не требуется.

## <a name="trusted-ips"></a>Надежные IP-адреса
Надежные IP-адреса позволяют пользователям toobypass Azure Multi-factor Authentication для запросов веб-сайтов, исходящих от определенных IP-адресов или подсетей. Например вы можете tooexempt пользователям двухшаговую проверку при входе из офиса hello. Для этого следует указать подсети hello office как запись надежных IP-адресов.

### <a name="tooconfigure-trusted-ips"></a>tooconfigure надежных IP-адресов
1. В hello разделе проверки подлинности IIS, выберите hello **надежных IP-адресов** вкладки.
2. Нажмите кнопку hello **добавить...** .
3. Когда откроется диалоговое окно Добавить надежных IP-адресов hello, выберите один из hello **один IP-адрес**, **диапазон IP-адресов**, или **подсети** переключатели.
4. Введите hello IP-адрес, диапазон IP-адреса или подсети, следует включить в список разрешенных. При вводе подсети выберите hello соответствующие hello маска подсети и нажмите кнопку **ОК** кнопки. Hello доверенных IP был добавлен.

<center>![Настройка](./media/multi-factor-authentication-get-started-adfs-adfs2/trusted.png)</center>
