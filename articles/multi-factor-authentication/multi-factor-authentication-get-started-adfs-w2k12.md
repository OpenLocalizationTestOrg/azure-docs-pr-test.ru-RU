---
title: "aaaMFA сервера с AD FS в Windows Server | Документы Microsoft"
description: "В этой статье описывается, как tooget работу с Azure Multi-factor Authentication и AD FS в Windows Server 2012 R2 и 2016."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 57208068-1e55-45b6-840f-fdcd13723074
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/29/2017
ms.author: kgremban
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 656785abcc63a020add765a86670b488a3b84b51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-multi-factor-authentication-server-toowork-with-ad-fs-in-windows-server"></a>Настроить toowork сервера Azure Multi-factor Authentication с AD FS в Windows Server
Если использование служб федерации Active Directory (AD FS) и требуется toosecure облачные или локальные ресурсы, можно настроить toowork сервера Azure Multi-factor Authentication с AD FS. Эта конфигурация активирует двухфакторную проверку подлинности для важных конечных точек.

Эта статья содержит сведения об использовании сервера Многофакторной идентификации Azure с AD FS на платформе Windows Server 2012 R2 или Windows Server 2016. Дополнительные сведения, узнайте, как слишком[защита облачных и локальных ресурсов с помощью сервера Azure Multi-factor Authentication с AD FS 2.0](multi-factor-authentication-get-started-adfs-adfs2.md).

## <a name="secure-windows-server-ad-fs-with-azure-multi-factor-authentication-server"></a>Защита AD FS в Windows Server с помощью сервера Многофакторной идентификации Azure
При установке сервера Azure Multi-factor Authentication, имеются следующие варианты hello.

* Установите сервер Azure Multi-factor Authentication локально на hello сервере AD FS
* Установка адаптера Azure Multi-factor Authentication hello локально на приветствия сервера AD FS, а затем установите многофакторной проверки подлинности сервера на другой компьютер

Прежде чем начать, помните о hello следующую информацию:

* Не требуется tooinstall сервера Azure Multi-factor Authentication на сервере AD FS. Тем не менее необходимо установить адаптер hello многофакторной проверки подлинности для AD FS на Windows Server 2012 R2 или Windows Server 2016, на котором выполняется AD FS. Можно установить сервер hello на другом компьютере, если он является одной из поддерживаемых версий и установить адаптер AD FS hello отдельно на сервере федерации AD FS. В разделе hello следующие процедуры toolearn как tooinstall hello адаптера отдельно.
* Если ваша организация использует текстовое сообщение или способов проверки подлинности мобильного приложения, hello строки, определенные в параметрах компании содержать заполнитель, <$*имя_приложения*$>. На сервере MFA версии 7.1 вы можете указать имя приложения, которое заменит этот заполнитель. В v7.0 или старую этот заполнитель не заменяется автоматически при использовании hello AD FS-адаптера. Для этих более старых версий удалите заполнитель hello из hello соответствующие строки при защите AD FS.
* Hello учетной записи, используемой toosign в должен иметь права toocreate групп безопасности в службе Active Directory.
* Мастер установки адаптера Hello многофакторной проверки подлинности AD FS создает группу безопасности под названием PhoneFactor Admins в вашем экземпляре Active Directory. Затем добавляется учетная запись службы AD FS hello группы toothis службы федерации. Проверьте на контроллере домена, hello группы PhoneFactor Admins на самом деле создана и что учетной записи службы hello AD FS является членом этой группы. При необходимости вручную добавьте toohello учетной записи службы AD FS hello группы PhoneFactor Admins на контроллере домена.
* Сведения об установке hello Web Service SDK с пользовательского портала hello статье [развертывание hello пользовательского портала для сервера Azure Multi-factor Authentication.](multi-factor-authentication-get-started-portal.md)

### <a name="install-azure-multi-factor-authentication-server-locally-on-hello-ad-fs-server"></a>Установите сервер Azure Multi-factor Authentication локально на сервере AD FS hello
1. Скачайте и установите сервер многофакторной идентификации Azure на сервере AD FS. Сведения об установке см. в статье [Приступая к работе с сервером многофакторной идентификации Azure](multi-factor-authentication-get-started-server.md).
2. В консоли управления hello сервера Azure Multi-factor Authentication щелкните hello **AD FS** значок. Выберите параметры hello **разрешить регистрацию пользователей** и **пользователи tooselect метод**.
3. Выберите любые дополнительные параметры, которые вы хотите toospecify для вашей организации.
4. Щелкните **Установить AD FS-адаптер**.
   
   <center>![Облако](./media/multi-factor-authentication-get-started-adfs-w2k12/server.png)</center>

5. Если откроется окно hello Active Directory, это означает следующее. Добавление компьютера домена tooa присоединены к домену, и hello Настройка Active Directory для обеспечения безопасной связи между адаптером hello AD FS и службой многофакторной проверки подлинности hello не была завершена. Нажмите кнопку **Далее** tooautomatically выполнить эту настройку, или выберите hello **пропустить автоматическую настройку Active Directory и настроить параметры вручную** флажок. Щелкните **Далее**.
6. Если локальная группа windows hello отображается, значит две вещи. Компьютер не присоединены к домену tooa домена и настройка локальной группы hello для обеспечения безопасной связи между адаптером hello AD FS и службой многофакторной проверки подлинности hello не была завершена. Нажмите кнопку **Далее** tooautomatically выполнить эту настройку, или выберите hello **пропустить автоматическую настройку локальной группы и настроить параметры вручную** флажок. Щелкните **Далее**.
7. В мастере установки hello, нажмите кнопку **Далее**. Сервер Azure Multi-factor Authentication создает группы PhoneFactor Admins hello и добавляет toohello учетной записи службы AD FS hello группы PhoneFactor Admins.
   <center>![Облако](./media/multi-factor-authentication-get-started-adfs-w2k12/adapter.png)</center>
8. На hello **запуска установщика** щелкните **Далее**.
9. В установщике адаптера hello многофакторной проверки подлинности AD FS щелкните **Далее**.
10. Нажмите кнопку **закрыть** после завершения установки hello.
11. После установки адаптера hello, необходимо зарегистрировать его с AD FS. Откройте Windows PowerShell и выполните следующую команду hello:<br>
    `C:\Program Files\Multi-Factor Authentication Server\Register-MultiFactorAuthenticationAdfsAdapter.ps1`
    <center>![Облако](./media/multi-factor-authentication-get-started-adfs-w2k12/pshell.png)</center>
12. toouse только что зарегистрированный адаптер, изменить hello глобальной политики поверки подлинности в AD FS. В консоли управления hello AD FS, перейдите toohello **политики проверки подлинности** узла. В hello **многофакторной проверки подлинности** щелкните hello **изменить** ссылку Далее toohello **глобальные параметры** раздела. В hello **изменение глобальной политики проверки подлинности** выберите **многофакторной проверки подлинности** качестве дополнительного метода проверки подлинности, а затем щелкните **ОК**. Hello адаптер регистрируется как WindowsAzureMultiFactorAuthentication. Перезапустите службу hello AD FS для эффекта tootake регистрации hello.

<center>![Облако](./media/multi-factor-authentication-get-started-adfs-w2k12/global.png)</center>

На этом этапе сервер Multi-factor Authentication настраивается toobe toouse поставщика дополнительной проверки подлинности с AD FS.

## <a name="install-a-standalone-instance-of-hello-ad-fs-adapter-by-using-hello-web-service-sdk"></a>Установка с помощью отдельного экземпляра адаптера hello AD FS с помощью hello Web Service SDK
1. Установите hello Web Service SDK на приветствия сервера, на котором работает сервер Multi-factor Authentication.
2. Следующие hello копирования файлов из hello \Program Files\Multi-Factor Authentication Server каталог toohello server плана tooinstall hello AD FS-адаптер:
   * MultiFactorAuthenticationAdfsAdapterSetup64.msi
   * Register-MultiFactorAuthenticationAdfsAdapter.ps1
   * Unregister-MultiFactorAuthenticationAdfsAdapter.ps1
   * MultiFactorAuthenticationAdfsAdapter.config
3. Запустите файл установки файлы MultiFactorAuthenticationAdfsAdapterSetup64.msi hello.
4. В установщике адаптера hello многофакторной проверки подлинности AD FS щелкните **Далее** toostart hello установки.
5. Нажмите кнопку **закрыть** после завершения установки hello.

## <a name="edit-hello-multifactorauthenticationadfsadapterconfig-file"></a>Отредактируйте файл MultiFactorAuthenticationAdfsAdapter.config hello
Выполните эти шаги файл MultiFactorAuthenticationAdfsAdapter.config hello tooedit.

1. Набор hello **UseWebServiceSdk** узла слишком**true**.  
2. Задайте значение hello **WebServiceSdkUrl** toohello URL-адрес hello SDK многофакторной проверки подлинности веб-службы. Например: *https://contoso.com/&lt;certificatename&gt;/MultiFactorAuthWebServiceSdk/PfWsSdk.asmx*, где *certificatename* hello имя сертификата.  
3. Измените скрипт hello Register-MultiFactorAuthenticationAdfsAdapter.ps1, добавив *параметр - ConfigurationFilePath &lt;путь&gt;*  toohello конец hello `Register-AdfsAuthenticationProvider` команду, где  *&lt;путь&gt;*  toohello MultiFactorAuthenticationAdfsAdapter.config hello полный путь файла.

### <a name="configure-hello-web-service-sdk-with-a-username-and-password"></a>Настройка hello Web Service SDK с помощью имени пользователя и пароля
Существует два варианта для настройки hello Web Service SDK. Hello сначала с помощью имени пользователя и пароля, hello, второй — с помощью сертификата клиента. Выполните следующие действия для первого параметра hello, или сразу перейти для hello секунды.  

1. Задайте значение hello **параметра WebServiceSdkUsername** tooan учетную запись, которая является членом группы безопасности PhoneFactor Admins hello. Используйте hello &lt;домена&gt;&#92;&lt; имя пользователя&gt; формат.  
2. Задайте значение hello **WebServiceSdkPassword** toohello пароль соответствующей учетной записи.

### <a name="configure-hello-web-service-sdk-with-a-client-certificate"></a>Настройка hello Web Service SDK с помощью сертификата клиента
Если вы не хотите toouse имя пользователя и пароль, выполните эти шаги tooconfigure hello Web Service SDK с помощью сертификата клиента.

1. Получите клиентский сертификат из центра сертификации для hello сервера, на котором выполняется hello Web Service SDK. Узнайте, каким образом слишком[получать сертификаты клиента](https://technet.microsoft.com/library/cc770328.aspx).  
2. Импорт hello хранилище сертификатов клиента toohello локального компьютера личных сертификатов на сервере hello, на котором выполняется hello Web Service SDK. Убедитесь, что этот центр сертификации hello открытый сертификат находится в хранилище сертификатов доверенных корневых сертификатов.  
3. Экспорт hello открытый и закрытый ключи hello клиентского сертификата tooa PFX-файла.  
4. Экспортируйте открытый ключ hello в файл .cer tooa формат Base64.  
5. В диспетчере серверов убедитесь, что установлена, функция проверки подлинности с сопоставлением сертификата клиента hello \Web Server\Security\IIS веб-сервер (IIS). Если он не установлен, установите **Добавить роли и компоненты** tooadd эту функцию.  
6. В диспетчере служб IIS дважды щелкните **редактор конфигурации** hello веб-сайте, который содержит виртуальный каталог Web Service SDK hello. Веб-сайт важные tooselect hello, hello виртуального каталога.  
7. Go toohello **system.webServer/security/authentication/iisClientCertificateMappingAuthentication** раздела.  
8. Набор включены слишком**true**.  
9. Установите параметр oneToOneCertificateMappingsEnabled слишком**true**.  
10. Нажмите кнопку hello **...**  toooneToOneMappings Далее, а затем нажмите hello **добавить** ссылку.  
11. Откройте hello Base64 CER-файл, экспортированный ранее. Удалите *-----BEGIN CERTIFICATE-----*, *-----END CERTIFICATE-----* и все разрывы строк. Скопируйте результирующую строку hello.  
12. Строка сертификата toohello набор скопированному предшествующего шаг hello.  
13. Набор включены слишком**true**.  
14. Задать tooan имя пользователя учетной записи, которая является членом группы безопасности PhoneFactor Admins hello. Используйте hello &lt;домена&gt;&#92;&lt; имя пользователя&gt; формат.  
15. Задать toohello hello пароль соответствующей учетной записи, а затем закройте редактор конфигурации.  
16. Нажмите кнопку hello **применить** ссылку.  
17. Дважды щелкните в виртуальный каталог Web Service SDK hello **проверки подлинности**.  
18. Убедитесь, что олицетворение ASP.NET и обычную проверку подлинности выбрано слишком**включено**, и все прочие элементы заданы слишком**отключено**.  
19. Дважды щелкните в виртуальный каталог Web Service SDK hello **параметры SSL**.  
20. Задать сертификаты клиентов слишком**Accept**, а затем нажмите кнопку **применить**.  
21. Скопируйте hello PFX-файл, экспортированный ранее toohello сервера, на котором работает адаптер AD FS hello.  
22. Импортировать в хранилище личных сертификатов локального компьютера toohello файл hello PFX-файл.  
23. Щелкните правой кнопкой мыши и выберите **управление закрытыми ключами**и затем предоставьте доступ на чтение toohello использованная учетная запись toosign в службе toohello AD FS.  
24. Откройте hello сертификата и скопируйте hello отпечаток клиента из hello **сведения** вкладки.  
25. В файле MultiFactorAuthenticationAdfsAdapter.config hello присвойте **параметра WebServiceSdkCertificateThumbprint** toohello строки копируются в предыдущем шаге hello.  

Наконец, tooregister hello адаптера, запустите hello \Program Files\Multi-Factor Authentication Server\Register-MultiFactorAuthenticationAdfsAdapter.ps1 сценарий в PowerShell. Hello адаптер регистрируется как WindowsAzureMultiFactorAuthentication. Перезапустите службу hello AD FS для эффекта tootake регистрации hello.

## <a name="secure-azure-ad-resources-using-ad-fs"></a>Защита ресурсов Azure AD с помощью AD FS
toosecure ресурса облака, настроить правило для утверждений, чтобы службы федерации Active Directory выдает утверждение multipleauthn hello, когда пользователь успешно выполняет двухшаговую проверку. Это утверждение будет передано в tooAzure AD. Выполните это процедура toowalk шаги hello.

1. Откройте оснастку управления AD FS.
2. В левой части экрана приветствия выберите **доверия с проверяющей стороной**.
3. Щелкните правой кнопкой мыши **Microsoft Office 365 Identity Platform** (Платформа удостоверений Microsoft Office 365) и выберите **Изменить правила утверждений...**.

   ![Облако](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip1.png)

4. На вкладке "Правила преобразования выдачи" выберите **Добавить правило**.

   ![Облако](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip2.png)

5. На Здравствуйте преобразования мастера добавления правила утверждения, выберите **пропуск или Фильтрация входящего утверждения** из hello раскрывающегося списка и нажмите кнопку **Далее**.

   ![Облако](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip3.png)

6. Укажите имя правила.
7. Выберите **ссылки на методы проверки подлинности** тип hello входящего утверждения.
8. Щелкните **Пройти по всем значениям утверждений**.
    ![Мастер добавления правила преобразования утверждений](./media/multi-factor-authentication-get-started-adfs-cloud/configurewizard.png)
9. Нажмите кнопку **Готово** Закройте консоль управления FS hello AD.

## <a name="related-topics"></a>Связанные разделы
Справка по устранению неполадок в разделе hello [Azure многофакторной проверки подлинности, часто задаваемые вопросы](multi-factor-authentication-faq.md)
