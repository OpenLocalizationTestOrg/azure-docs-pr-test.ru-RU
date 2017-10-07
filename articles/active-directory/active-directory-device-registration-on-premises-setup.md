---
title: "aaaSetting локального условного доступа с помощью службы регистрации устройств Azure Active Directory | Документы Microsoft"
description: "Пошаговое руководство по tooenabling условного доступа tooon локальные приложения с помощью служб федерации Active Directory (AD FS) в Windows Server 2012 R2."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 6ae9df8b-31fe-4d72-9181-cf50cfebbf05
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 808e3b96873102aebae667153f588dcdb205e884
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="setting-up-on-premises-conditional-access-by-using-azure-active-directory-device-registration"></a>Настройка локального условного доступа с помощью регистрации устройств в Azure Active Directory
Когда потребуется tooworkplace соединения пользователей своих личных устройств toohello службы регистрации устройств Azure Active Directory (Azure AD), устройствах может быть помечен как известные tooyour организации. Ниже приведено пошаговое руководство для включения условного доступа tooon локальные приложения с помощью служб федерации Active Directory (AD FS) в Windows Server 2012 R2.

> [!NOTE]
> При использовании устройств, зарегистрированных в политиках условного доступа службы регистрации устройств Azure Active Directory, требуется лицензия Office 365 или Azure AD Premium. К ним относятся политики, применяемые службами AD FS к локальным ресурсам.
> 
> Дополнительные сведения о сценариях hello условным доступом для локальных ресурсов см. в разделе [подключение tooworkplace с любого устройства для единого входа и эффективная двухфакторная проверка подлинности в корпоративных приложениях](https://technet.microsoft.com/library/dn280945.aspx).

Эти возможности будут доступны toocustomers, которые приобрели лицензию Azure Active Directory Premium.

## <a name="supported-devices"></a>Поддерживаемые устройства
* Присоединенные к домену устройства Windows 7.
* Личные и присоединенные к домену устройства Windows 8.1.
* iOS 6 и более поздних версий для обозревателя Safari hello
* Устройства Android 4.0 или более поздней версии, Samsung GS3 или телефоны более поздней версии, Samsung Galaxy Note 2 или планшеты более поздней версии.

## <a name="scenario-prerequisites"></a>Предварительные условия для сценария
* Подписки tooOffice 365 или Azure Active Directory Premium
* Клиент Azure Active Directory.
* Windows Server Active Directory (Windows Server 2008 или более поздней версии).
* Обновленная схема в Windows Server 2012 R2.
* Лицензия на Azure Active Directory Premium.
* Windows Server 2012 R2 служб федерации, настроенного для единого входа tooAzure AD
* Прокси-служба веб-приложения Windows Server 2012 R2. 
* Microsoft Azure Active Directory Connect [(Скачать Azure AD Connect)](http://www.microsoft.com/en-us/download/details.aspx?id=47594).
* Проверенный домен.

## <a name="known-issues-in-this-release"></a>Известные проблемы в этом выпуске
* Политики условного доступа на основе устройств требуется tooActive обратной записи устройства объектов каталога из Azure Active Directory. Может потребоваться toothree часов для обратной записи tooActive Directory toobe объектов устройств.
* устройства iOS 7 всегда запрашивать пользователя hello tooselect сертификат во время проверки подлинности сертификата клиента.
* Некоторые версии iOS 8, предшествующие iOS 8.3, не работают.

## <a name="scenario-assumptions"></a>Принятые в сценарии допущения
Данный сценарий предполагает, что у вас есть гибридная среда, состоящая из клиента Azure AD и локальной службы Active Directory. Эти клиенты должны быть подключены с использованием Azure AD Connect, а также проверенного домена и AD FS для единого входа. Используйте следующий контрольный список toohelp настроить среду в соответствии с требованиями toohello hello.

## <a name="checklist-prerequisites-for-conditional-access-scenario"></a>Контрольный список: предварительные условия для сценария условного доступа
Подключите клиент Azure AD к экземпляру локальной службы Active Directory.

## <a name="configure-azure-active-directory-device-registration-service"></a>Настройка службы регистрации устройств Azure Active Directory
Используйте это руководство по toodeploy и настройка службы регистрации устройств Azure Active Directory hello для вашей организации.

В этом руководстве предполагается, что настройки Windows Server Active Directory и подписались tooMicrosoft Azure Active Directory. См. предварительные требования hello описано выше.

hello toodeploy службы регистрации устройств Azure Active Directory с Azure Active Directory клиента задачи завершения hello в следующий контрольный список в порядке hello. В случае перехода по ссылке tooa раздел общих понятий, вернитесь toothis контрольный список после этого, чтобы можно было перейти hello оставшихся задач. Некоторые задачи включают шаг проверки сценарий, который поможет подтвердить hello действие выполнено успешно.

## <a name="part-1-enable-azure-active-directory-device-registration"></a>Часть 1. Включение регистрации устройств в Azure Active Directory
Выполните действия hello в контрольном списке tooenable hello и настройка службы регистрации устройств Azure Active Directory hello.

| Задача | Справочные материалы | 
| --- | --- |
| Включите регистрацию устройств в Azure Active Directory клиента tooallow устройств toojoin hello рабочую область. По умолчанию многофакторная проверка подлинности Azure не включен для службы hello. Тем не менее мы рекомендуем использовать Многофакторную идентификацию при регистрации устройства. Перед включением Многофакторной идентификации в службе регистрации Active Directory убедитесь в том, что для AD FS настроен поставщик Многофакторной идентификации. |[Включение регистрации устройств в Azure Active Directory](active-directory-device-registration-get-started.md)| 
|Устройства будут обнаруживать вашу службу регистрации устройств в Azure Active Directory, просматривая хорошо известные записи DNS. Настройте DNS своей организации таким образом, чтобы устройства могли обнаруживать вашу службу регистрации устройств Azure Active Directory. |[Настройка обнаружения службы регистрации устройств Azure Active Directory](active-directory-device-registration-get-started.md)| 


## <a name="part-2-deploy-and-configure-windows-server-2012-r2-active-directory-federation-services-and-set-up-a-federation-relationship-with-azure-ad"></a>Часть 2. Развертывание и настройка служб федерации Windows Server 2012 R2 Active Directory и настройка отношений федерации с Azure AD

| Задача | Справочные материалы |
| --- | --- |
| Развертывание доменных служб Active Directory с помощью расширений схемы Windows Server 2012 R2 hello. Вы не обязательно tooupgrade любой из вашего tooWindows контроллеры домена Server 2012 R2. hello единственное требование — обновление схемы Hello. |[Обновление схемы доменных служб Active Directory](#upgrade-your-active-directory-domain-services-schema) |
| Устройства будут обнаруживать вашу службу регистрации устройств в Azure Active Directory, просматривая хорошо известные записи DNS. Настройте DNS своей организации таким образом, чтобы устройства могли обнаруживать вашу службу регистрации устройств Azure Active Directory. |[Подготовка Active Directory к поддержке устройств](#prepare-your-active-directory-to-support-devices) |

## <a name="part-3-enable-device-writeback-in-azure-ad"></a>Часть 3. Включение обратной записи устройств в Azure AD
| Задача | Справочные материалы |
| --- | --- |
| Выполните часть 2 включения обратной записи устройств в службе Azure AD Connect. После его завершения, возвращаемый toothis руководства. |[Включение обратной записи устройств в службе Azure AD Connect](#upgrade-your-active-directory-domain-services-schema) |

## <a name="optional-part-4-enable-multi-factor-authentication"></a>[Необязательно.] Часть 4. Включение Многофакторной идентификации
Настоятельно рекомендуется настроить одну hello несколько параметров для многофакторной проверки подлинности. Если toorequire многофакторной проверки подлинности, см. [выбрать решение безопасности hello многофакторной проверки подлинности для вас](../multi-factor-authentication/multi-factor-authentication-get-started.md). Он включает в себя описание каждого решения, а также ссылки toohelp настроить решение hello по вашему выбору.

## <a name="part-5-verification"></a>Часть 5. Проверка
Hello развертывания уже выполнено и можно опробовать некоторые сценарии. Используйте hello следующие ссылки tooexperiment со службой hello и ознакомиться с его функциями.

| Задача | Справочные материалы |
| --- | --- |
| Присоединение рабочей области tooyour некоторых устройств с помощью службы регистрации устройств Azure Active Directory. Присоединять можно устройства iOS, Windows и Android. |[Присоединение рабочей сети tooyour устройства, с помощью службы регистрации устройств Azure Active Directory](#join-devices-to-your-workplace-using-azure-active-directory-device-registration) |
| Просмотреть и включить или отключить для зарегистрированных устройств с помощью портала администрирования hello. В этой задаче вы просмотрите несколько зарегистрированных устройств с помощью портала администрирования hello. |[Обзор службы регистрации устройств Azure Active Directory](active-directory-device-registration-get-started.md) |
| Убедитесь, что объекты устройств записываются из Azure Active Directory tooWindows Server Active Directory. |[Убедитесь, что зарегистрированные устройства записываются обратно tooActive каталога](#verify-registered-devices-are-written-back-to-active-directory) |
| Теперь, когда у пользователей появилась возможность регистрировать устройства, можно создать политики доступа к приложениям в AD FS, позволяющие использовать только зарегистрированные устройства. В этой задаче вы создадите правило доступа к приложениям и пользовательское сообщение об отказе в доступе. |[Создание политики доступа к приложениям и пользовательского сообщения об отказе в доступе](#create-an-application-access-policy-and-custom-access-denied-message) |

## <a name="integrate-azure-active-directory-with-on-premises-active-directory"></a>Интеграция Azure Active Directory с локальной службой Active Directory
Данный раздел поможет вам интегрировать клиент Azure AD с локальной службой Active Directory, используя Azure AD Connect. Несмотря на то, что hello действия доступны в hello классический портал Azure, запишите какие-либо специальные инструкции, приведенные в этом разделе.

1. Войти в toohello классический портал Azure, используя учетную запись, которая является глобальным администратором в Azure AD.
2. Выберите на левой панели hello **Active Directory**.
3. На hello **каталога** вкладке, выберите свой каталог.
4. Выберите hello **Интеграция каталогов** вкладки.
5. В разделе hello **развертывание и управление ими** статьи, выполните шаги с 1 по 3 toointegrate Azure Active Directory с локальным каталогом.
   
   1. Добавьте домены.
   2. Установите и запустите Azure AD Connect с помощью инструкций hello в [выборочной установки из Azure AD Connect](connect/active-directory-aadconnect-get-started-custom.md).
   3. Выполните проверку и управление синхронизацией каталогов. Инструкции по единому входу доступны на этом шаге.
   
   Кроме того, настройте федерацию с AD FS, как описано в разделе [Выборочная установка Azure AD Connect](connect/active-directory-aadconnect-get-started-custom.md).

## <a name="upgrade-your-active-directory-domain-services-schema"></a>Обновление схемы доменных служб Active Directory
> [!NOTE]
> После обновления схемы Active Directory hello процесс необратим. Рекомендуется сначала выполнить обновление hello в тестовой среде.
> 

1. Войдите в контроллер домена tooyour с учетной записью с правами администратора схемы и администратора предприятия.
2. Копировать hello **[media] \support\adprep** tooone и вложенные папки из контроллеров домена Active Directory (где **[media]** — hello путь toohello Windows Server 2012 R2 установочного носителя ).
4. В командной строке последовательно toohello **adprep** каталога и выполнения **adprep.exe/forestprep**. Выполните обновление схемы hello toocomplete инструкциям на экране приветствия.

## <a name="prepare-your-active-directory-toosupport-devices"></a>Подготовка устройства toosupport Active Directory
> [!NOTE]
> Это одноразовая операция, что необходимо запустить tooprepare устройств toosupport леса Active Directory. toocomplete этой процедуры необходимо войти в систему с правами администратора предприятия, и ваш лес Active Directory должен иметь схему Windows Server 2012 R2 hello.
> 


### <a name="prepare-your-active-directory-forest"></a>Подготовка леса Active Directory
1. На своем сервере федерации откройте командное окно Windows PowerShell и введите следующую команду: **Initialize-ADDeviceRegistration**. 
2. При появлении запроса о **ServiceAccountName**, введите имя hello hello учетной записи службы, выбранный в hello учетной записи службы для служб AD FS. Если групповой управляемой учетной записи, введите учетную запись hello в hello **domain\accountname$** формат. Для учетной записи домена, используйте формат hello **domain\accountname**.

### <a name="enable-device-authentication-in-ad-fs"></a>Включение аутентификации устройств в AD FS
1. На сервере федерации откройте консоль управления AD FS hello и перейти слишком**AD FS** > **политики проверки подлинности**.
2. На hello **действия** выберите **редактировать глобальную первичную аутентификацию**.
3. Установите флажок **Включить аутентификацию устройства** и нажмите кнопку **ОК**.
4. По умолчанию AD FS периодически удаляет неиспользуемые устройства из Active Directory. Отключите эту задачу во время использования службы регистрации устройств Azure Active Directory, чтобы устройствами можно было управлять в Azure.

### <a name="disable-unused-device-cleanup"></a>Отключение удаления неиспользуемых устройств
На своем сервере федерации откройте командное окно Windows PowerShell и введите следующую команду: **Set-AdfsDeviceRegistration -MaximumInactiveDays 0**.

### <a name="prepare-azure-ad-connect-for-device-writeback"></a>Подготовка Azure AD Connect к обратной записи устройства
Завершите часть 1 — подготовьте Azure AD Connect.

## <a name="join-devices-tooyour-workplace-by-using-azure-active-directory-device-registration-service"></a>Присоединение рабочей области tooyour устройств с помощью службы регистрации устройств Azure Active Directory

### <a name="join-an-ios-device-by-using-azure-active-directory-device-registration"></a>Присоединение устройства iOS с помощью службы регистрации устройств Active Directory Azure
Регистрация устройств Azure Active Directory использует процесс регистрации hello беспроводного профиля для устройств iOS. Этот процесс начинается при подключении пользователя hello URL-адрес toohello профиль регистрации с помощью Safari. Hello URL-адрес имеет следующий формат:

    https://enterpriseregistration.windows.net/enrollmentserver/otaprofile/"yourdomainname"

В этом случае `yourdomainname` — hello доменное имя, которое вы настроили в Azure Active Directory. Например если имя домена contoso.com, URL-адрес hello таков:

    https://enterpriseregistration.windows.net/enrollmentserver/otaprofile/contoso.com

Существует много различных способов toocommunicate пользователей tooyour этот URL-адрес. Например, один из рекомендуемых способов — опубликовать этот URL-адрес в пользовательском сообщении об отказе в доступе в AD FS. Эти сведения, описанные в следующем разделе hello [Создание политики доступа к приложениям и пользовательское сообщение об отказе в доступе](#create-an-application-access-policy-and-custom-access-denied-message).

### <a name="join-a-windows-81-device-by-using-azure-active-directory-device-registration"></a>Присоединение устройства Windows 8.1 с помощью службы регистрации устройств Active Directory Azure
1. На устройстве Windows 8.1 последовательно выберите **Параметры компьютера** > **Сеть** > **Рабочая область**.
2. Введите свое имя пользователя в формате имени участника-пользователя. Пример: **dan@contoso.com**.
3. Выберите **Присоединиться**.
4. При появлении запроса введите свои учетные данные и выполните вход. Теперь присоединено устройство Hello.

### <a name="join-a-windows-7-device-by-using-azure-active-directory-device-registration"></a>Присоединение устройства Windows 7 с помощью службы регистрации устройств Active Directory Azure
tooregister Windows 7 к домену устройства, необходимо программного пакета регистрации устройств toodeploy hello. Hello пакета программного обеспечения называется рабочему месту Join для Windows 7 и его доступны для загрузки в hello [веб-сайте Microsoft Connect](https://connect.microsoft.com/site1164). 

Инструкции о как toouse hello пакета можно найти в [как tooconfigure Автоматическая регистрация Windows, присоединенных к домену устройствами с помощью Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md).

## <a name="verify-that-registered-devices-are-written-back-tooactive-directory"></a>Убедитесь, что зарегистрированные устройства записываются обратно tooActive каталога
Можно просмотреть и проверить, что объекты устройств были записаны tooyour Active Directory с помощью LDP.exe и ADSI Edit. Оба доступны с помощью средства администрирования Active Directory hello.

По умолчанию объекты устройств, которые записаны из Azure Active Directory, помещаются в hello же домене, что и ваша ферма AD FS.

    CN=RegisteredDevices,defaultNamingContext

## <a name="create-an-application-access-policy-and-custom-access-denied-message"></a>Создание политики доступа к приложениям и пользовательского сообщения об отказе в доступе
Рассмотрим следующие сценарии hello: Создание приложения доверия с проверяющей стороной в AD FS и настроить правило авторизации выдачи, позволяющий только для зарегистрированных устройств. Теперь только устройства, зарегистрированные разрешены tooaccess приложения hello. 

toomake легко приложения toohello toogain доступ пользователи, настройте пользовательское сообщение об отказе в доступе, содержит инструкции по toojoin своего устройства. Теперь пользователи имеют tooregister возможность легко свои устройства для доступа к приложению.

Hello следующие шаги показывают, как tooimplement этот сценарий.

> [!NOTE]
> В этом разделе предполагается, что вы уже настроили отношение доверия с проверяющей стороной для приложения в AD FS.
> 

1. Откройте средство AD FS MMC hello, а затем выберите **AD FS** > **отношения доверия** > **доверия с проверяющей стороной**.
2. Найдите toowhich приложения hello, это новое правило доступа применяется. Щелкните правой кнопкой мыши приложение hello, а затем выберите **изменение правил для утверждений**.
3. Выберите hello **правила авторизации выдачи** , а затем выберите **добавить правило**.
4. Из hello **правило для утверждений** шаблона раскрывающегося списка, выберите **разрешать или запрещать пользователям на основании входящего утверждения**. Затем нажмите кнопку **Далее**.
5. В hello **имени правила утверждения** введите **разрешают доступ из зарегистрированных устройств**.
6. Из hello **тип входящего утверждения** раскрывающемся списке выберите **— пользователь зарегистрирован**.
7. В hello **значение входящего утверждения** введите **true**.
8. Выберите hello **toousers разрешить доступ с данным входящим утверждением** переключатель.
9. Нажмите кнопку **Готово**, а затем **Применить**.
10. Удалите все правила, которые разрешают больше, чем созданное правило hello. Например, удалите правило по умолчанию hello **tooall разрешить доступ пользователей**.

Приложение будет теперь настроенный tooallow доступ только в том случае, если пользователь hello поступает с устройства, зарегистрированного и присоединенного toohello рабочей области. Более сложные политики доступа описаны в разделе об [управлении рисками с помощью дополнительной Многофакторной идентификации для критически важных приложений](https://technet.microsoft.com/library/dn280949.aspx).

Далее вы настроите пользовательское сообщение об ошибке для своего приложения. сообщение об ошибке Hello сообщает пользователям, что они должны присоединить их рабочему месту toohello устройства, прежде чем они могут получить доступ приложения hello. Вы можете создать пользовательское сообщение об отказе в доступе с помощью пользовательского кода HTML и PowerShell.

На сервере федерации откройте командное окно PowerShell и введите следующую команду hello. Замените части команды hello с элементами, которые задаются для конкретного tooyour системы:

    Set-AdfsRelyingPartyWebContent -Name "relying party trust name" -ErrorPageAuthorizationErrorMessage
Для доступа к этому приложению необходимо зарегистрировать устройство.

**Если вы используете устройство iOS, выберите этот toojoin ссылку устройство**:

    a href='https://enterpriseregistration.windows.net/enrollmentserver/otaprofile/yourdomain.com

Присоединение этой рабочей tooyour устройства iOS.

Если вы используете устройство Windows 8.1, то для присоединения устройства выберите **Параметры компьютера**> **Сеть** > **Рабочая область**.

В команды, предшествующие hello **имя доверия проверяющей стороны** является именем hello объекта доверия с проверяющей стороной вашего приложения в AD FS.
И **yourdomain.com** hello доменное имя, которое вы настроили в Azure Active Directory (например, contoso.com).
Быть убедиться, что tooremove все разрывы строк (если имеется) из hello HTML содержимого, передаваемый toohello **Set-AdfsRelyingPartyWebContent** командлета.

Теперь, когда пользователи обращаются к приложению с устройств, которые не зарегистрированы hello службы регистрации устройств Azure Active Directory, они видят страницу, которая выглядит примерно toohello следующий снимок экрана.

![Снимок экрана с ошибкой, возникающей, если пользователь еще не зарегистрировал свое устройство в Azure AD](./media/active-directory-conditional-access/error-azureDRS-device-not-registered.gif)


