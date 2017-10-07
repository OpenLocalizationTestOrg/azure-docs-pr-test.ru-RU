---
title: "Руководство по настройке LinkedIn Lookup для автоматической подготовки пользователей с помощью Azure Active Directory | Документация Майкрософт"
description: "Узнайте, как tooconfigure Azure Active Directory tooautomatically подготовки и Отмена подготовки учетных записей пользователей tooLinkedIn уточняющего запроса."
services: active-directory
documentationcenter: 
author: asmalser-msft
writer: asmalser-msft
manager: stevenpo
ms.assetid: d4ca2365-6729-48f7-bb7f-c0f5ffe740a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/15/2017
ms.author: asmalser-msft
ms.openlocfilehash: 3e41abb8af00715f70e5a14d9d26ff600c10f492
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-linkedin-lookup-for-automatic-user-provisioning"></a>Руководство по настройке LinkedIn Lookup для автоматической подготовки пользователей


Цель этого учебника Hello — tooshow hello действия, которые следует tooperform в подстановки LinkedIn и Azure AD tooautomatically подготовки и Отмена подготовки учетных записей пользователей из Azure AD tooLinkedIn уточняющего запроса. 

## <a name="prerequisites"></a>Предварительные требования

Hello сценарий, описанный в этом руководстве предполагается, что уже hello следующих элементов:

*   Клиент Azure Active Directory.
*   Клиент LinkedIn Lookup. 
*   Учетной записи администратора в уточняющем запросе LinkedIn с toohello доступа LinkedIn центр учетных записей

> [!NOTE]
> Azure Active Directory интегрируется с LinkedIn уточняющего запроса с помощью hello [SCIM](http://www.simplecloud.info/) протокола.

## <a name="assigning-users-toolinkedin-lookup"></a>Назначение пользователей tooLinkedIn уточняющего запроса

Azure Active Directory использует называемый «назначения» toodetermine пользователей, которые должны получать доступ tooselected приложений. В контексте hello автоматический подготовки пользователей. учетной записи будут синхронизированы только hello пользователей и групп, назначенных» «tooan приложения в Azure AD. 

Для настройки и включения hello подготовки службы, вам потребуется toodecide какие пользователи или группы в Azure AD представляют Привет пользователей, которым требуется доступ tooLinkedIn уточняющего запроса. После приняла решение, можно назначить эти пользователи tooLinkedIn уточняющего запроса в соответствии с инструкциями hello здесь:

[Назначить пользователю или группе tooan корпоративного приложения](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toolinkedin-lookup"></a>Важные советы для назначения пользователей tooLinkedIn уточняющего запроса

*   Рекомендуется один назначить tooLinkedIn уточняющего запроса tootest hello настройки подготовки пользователя Azure AD. Дополнительные пользователи и/или группы можно назначить позднее.

*   При присвоении пользователя tooLinkedIn уточняющего запроса, необходимо выбирать hello **пользователя** роли в диалоговом окне приветствия назначения. роль «Доступ по умолчанию» Hello не работает для подготовки.


## <a name="configuring-user-provisioning-toolinkedin-lookup"></a>Настройка подготовки tooLinkedIn уточняющего запроса пользователя

Этот раздел поможет выполнить подключение учетной записи пользователя SCIM подстановки tooLinkedIn Azure AD подготовки API и настройке подготовки службы toocreate hello, обновления и отключения пользователей, назначенные учетные записи в уточняющем запросе LinkedIn на основе пользователей и группы Назначение в Azure AD.

> [!TIP]
> Можно также выбрать для поиска LinkedIn, следуя инструкциям hello в tooenabled на основе SAML Single Sign-On [портал Azure](https://portal.azure.com). Единый вход можно настроить независимо от автоматической подготовки, хотя две эти функции дополняют друг друга.


### <a name="tooconfigure-automatic-user-account-provisioning-toolinkedin-lookup-in-azure-ad"></a>tooconfigure автоматическая учетная запись подготовки tooLinkedIn уточняющего запроса в Azure AD:


Hello первым шагом является tooretrieve LinkedIn маркер доступа. Если вы являетесь администратором предприятия, то можете самостоятельно подготовить токен доступа. В ваш центр учетной записи перейдите слишком**параметры &gt; глобальные параметры** и откройте hello **SCIM установки** панель.

> [!NOTE]
> При доступе к центру учетных записей hello напрямую, а не через ссылку, может получить доступ с помощью hello следующие шаги.

1)  Войдите в центр tooAccount.

2)  Выберите **Администратор &gt; Параметры администратора**.

3)  Нажмите кнопку **Advanced интеграций** на hello левой боковой панели. Вы являетесь направленной toohello центр учетных записей.

4)  Нажмите кнопку **+ добавить новую конфигурацию SCIM** и выполните процедуру hello, заполнив каждого поля.

> Если автоматическое назначение лицензии отключено, синхронизируются только данные пользователя.

![Подготовка LinkedIn Lookup](./media/active-directory-saas-linkedinlookup-provisioning-tutorial/linkedin_1.PNG)

> При включении назначения autolicense требуется toonote экземпляр приложения и типа лицензии. По мере назначения лицензий, сначала служат основой пока взяты все лицензии hello.

![Подготовка LinkedIn Lookup](./media/active-directory-saas-linkedinlookup-provisioning-tutorial/linkedin_2.PNG)

5)  Щелкните **Создать токен**. Вы увидите экрана маркера доступа в разделе hello **маркер доступа** поля.

6)  Сохраните буфер обмена tooyour токена доступа или компьютер перед выходом из страницы приветствия.

7) Затем войдите в toohello [портал Azure](https://portal.azure.com)и найдите toohello **Azure Active Directory > корпоративных приложений > все приложения** раздела.

8) Если вы уже настроили LinkedIn Уточняющий запрос для единого входа, поиск экземпляра LinkedIn уточняющего запроса с помощью поля поиска hello. В противном случае выберите **добавить** и выполните поиск **уточняющего запроса LinkedIn** в галерее приложения hello. Выберите LinkedIn подстановки из результатов поиска hello и добавить его в список tooyour приложений.

9)  Выберите свой экземпляр LinkedIn уточняющего запроса, а затем выберите hello **Provisioning** вкладки.

10) Набор hello **режим подготовки** слишком**автоматического**.

![Подготовка LinkedIn Lookup](./media/active-directory-saas-linkedinlookup-provisioning-tutorial/linkedin_3.PNG)

11)  Заполните следующие поля в группе hello **учетные данные администратора** :

* В hello **URL-адрес клиента** введите https://api.linkedin.com.

* В hello **секрет маркера** введите hello маркер доступа, созданный на шаге 1 и нажмите кнопку **проверить подключение** .

* Вы увидите уведомление об успехе hello upperright части портала.

12) Введите адрес электронной почты hello пользователя или группы, которые должны получить уведомления о подготовке ошибки в hello **уведомление по электронной почте** поле и установите флажок "hello" ниже.

13) Щелкните **Сохранить**. 

14) В hello **сопоставления атрибутов** просмотрите hello атрибуты пользователя и группы, которые будут синхронизированы с Azure AD tooLinkedIn уточняющего запроса. Обратите внимание, что атрибуты, выбранные в качестве hello **сопоставление** свойства будут использоваться toomatch hello учетных записей и групп в уточняющем запросе LinkedIn для операций обновления. Выберите toocommit кнопку hello сохранить все изменения.

![Подготовка LinkedIn Lookup](./media/active-directory-saas-linkedinlookup-provisioning-tutorial/linkedin_4.PNG)

15) tooenable hello подготовки службы Azure AD для LinkedIn Просмотр, изменение hello **состояние подготовки** слишком**на** в hello **параметры** раздела

16) Щелкните **Сохранить**. 

Это приведет к запуску hello Первоначальная синхронизация всех пользователей и/или группам назначается tooLinkedIn уточняющего запроса в разделе hello пользователей и групп. Обратите внимание, что hello начальной синхронизации будет иметь tooperform больше времени, чем последующие синхронизации, которые происходят примерно каждые 20 минут при условии, что запущена служба hello. Можно использовать hello **сведения о синхронизации** статьи toomonitor хода выполнения и следуйте ссылки tooprovisioning отчеты о действиях, описывающих все действия, выполняемые hello подготовки службы в приложении просмотра LinkedIn.


## <a name="additional-resources"></a>Дополнительные ресурсы

* [Управление подготовкой учетных записей пользователей для корпоративных приложений](active-directory-enterprise-apps-manage-provisioning.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)
