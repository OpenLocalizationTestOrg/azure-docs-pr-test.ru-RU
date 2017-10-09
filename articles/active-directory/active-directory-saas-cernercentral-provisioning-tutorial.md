---
title: "Руководство по настройке Cerner Central для автоматической подготовки пользователей с помощью Azure Active Directory | Документация Майкрософт"
description: "Узнайте, как Azure Active Directory tooautomatically tooconfigure подготовить список tooa пользователей в центральный Cerner."
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
ms.date: 05/26/2017
ms.author: asmalser-msft
ms.openlocfilehash: e96da98e783d24e7f34ae924824f909eead75f54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-cerner-central-for-automatic-user-provisioning"></a>Руководство по настройке Cerner Central для автоматической подготовки пользователей

Цель этого учебника Hello — hello действия, которые следует tooperform в центральный Cerner и Azure AD tooautomatically подготовки и Отмена подготовки учетных записей пользователей из списка пользователей Azure AD tooa в центральный Cerner tooshow. 


## <a name="prerequisites"></a>Предварительные требования

Hello сценарий, описанный в этом руководстве предполагается, что уже hello следующих элементов:

*   Клиент Azure Active Directory.
*   Клиент Cerner Central. 

> [!NOTE]
> Azure Active Directory интегрируется с с помощью hello центральный Cerner [SCIM](http://www.simplecloud.info/) протокола.

## <a name="assigning-users-toocerner-central"></a>Назначение пользователей tooCerner центральный

Azure Active Directory использует называемый «назначения» toodetermine пользователей, которые должны получать доступ tooselected приложений. В контексте hello автоматический подготовки пользователей. учетной записи синхронизируются только hello пользователей и групп, назначенных» «tooan приложения в Azure AD. 

Прежде чем настройка и включение hello подготовки службы, необходимо решить, какие пользователи или группы в Azure AD представляют Привет пользователей, которым требуется доступ tooCerner центральный. После приняла решение, можно назначить эти пользователи tooCerner центральный, следуя инструкциям hello:

[Назначить пользователю или группе tooan корпоративного приложения](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toocerner-central"></a>Важные советы для назначения пользователей tooCerner центральный

*   Рекомендуется один назначить hello центра tootest tooCerner настройки подготовки пользователя Azure AD. Дополнительные пользователи и/или группы можно назначить позднее.

* По завершении первоначального тестирования для одного пользователя, центральный Cerner рекомендует назначение hello весь список пользователей предназначен tooaccess любой Cerner решения (не только центр Cerner) toobe подготовить tooCerner в список пользователя.  Другие решения Cerner использовать этот список пользователей в список пользователей hello.

*   При присвоении пользователя tooCerner центральный, необходимо выбирать hello **пользователя** роли в диалоговом окне приветствия назначения. Пользователи с ролью «Доступ по умолчанию» hello, исключаются из подготовки.


## <a name="configuring-user-provisioning-toocerner-central"></a>Настройка подготовки tooCerner центральный пользователей

Этот раздел поможет выполнить подключение список пользователей центральный tooCerner Azure AD с помощью учетной записи пользователя Cerner SCIM подготовки API и настройке подготовки службы toocreate hello, обновления и отключить назначенный пользователь, на основе учетных записей в центральный Cerner для назначения пользователей и групп в Azure AD.

> [!TIP]
> Можно также выбрать tooenabled на основе SAML Single Sign-On для центрального Cerner, следуя hello следуйте инструкциям в [портал Azure (https://portal.azure.com). Единый вход можно настроить независимо от автоматической подготовки, хотя две эти функции дополняют друг друга. Дополнительные сведения см. в разделе hello [Cerner центральный единого входа учебника](active-directory-saas-cernercentral-tutorial.md).


### <a name="tooconfigure-automatic-user-account-provisioning-toocerner-central-in-azure-ad"></a>tooconfigure автоматическая учетная запись подготовки tooCerner центральный в Azure AD:


В tooCerner учетных записей пользователя tooprovision порядок центральный вы требуется toorequest центральный Cerner системную учетную запись из Cerner, а также создания токена носителя OAuth, Azure AD можно использовать конечную точку SCIM tooconnect tooCerner. Также рекомендуется выполнить интеграцию hello в изолированной среды Cerner перед развертыванием tooproduction.

1.  Hello первым шагом является управление hello Cerner людей hello tooensure и интеграция Azure AD учетная запись CernerCare, являющийся обязательным tooaccess hello документации необходимые toocomplete hello инструкции. При необходимости используйте URL-адреса hello ниже учетные записи CernerCare toocreate в каждой среде применимо.

   * Песочница: https://sandboxcernercare.com/accounts/create

   * Производственная среда: https://cernercare.com/accounts/create  

2.  Далее создайте для Azure AD системную учетную запись. Используйте инструкции hello ниже toorequest системной учетной записи для "песочницы" и рабочей сред.

   * Инструкции: https://wiki.ucern.com/display/CernerCentral/Requesting+A+System+Account

   * Песочница: https://sandboxcernercentral.com/system-accounts/

   * Производственная среда: https://cernercentral.com/system-accounts/

3.  Далее создайте токен носителя OAuth для каждой системной учетной записи. toodo это, выполните hello инструкциям ниже.

   * Инструкции: https://wiki.ucern.com/display/public/reference/Accessing+Cerner%27s+Web+Services+Using+A+System+Account+Bearer+Token

   * Песочница: https://sandboxcernercentral.com/system-accounts/

   * Производственная среда: https://cernercentral.com/system-accounts/

4. Наконец вам нужно идентификаторы области списка tooacquire пользователей для обеих hello "песочницы" и рабочей сред в Cerner toocomplete hello конфигурации. Сведения о том, как tooacquire, см.: https://wiki.ucern.com/display/public/reference/Publishing+Identity+Data+Using+SCIM. 

5. Теперь можно настроить tooCerner учетных записей пользователя tooprovision Azure AD. Войдите в toohello [портал Azure](https://portal.azure.com)и найдите toohello **Azure Active Directory > корпоративных приложений > все приложения** раздела.

6. Если вы уже настроили центральный Cerner для единого входа, поиск экземпляра с помощью поля поиска hello центральный Cerner. В противном случае выберите **добавить** и выполните поиск **Cerner центральный** в галерее приложения hello. Выберите центральный Cerner из результатов поиска hello и добавить его в список tooyour приложений.

7.  Выберите свой экземпляр центральный Cerner, а затем выберите hello **Provisioning** вкладки.

8.  Набор hello **режим подготовки** слишком**автоматического**.

   ![Подготовка Cerner Central](./media/active-directory-saas-cernercentral-provisioning-tutorial/Cerner.PNG)

9.  Заполните следующие поля в группе hello **учетные данные администратора**:

   * В hello **URL-адрес клиента** введите URL-адрес в формате hello ниже, заменив «User-списка-область-ID» с Идентификатором hello сферы, полученного в шаге #4.

> Песочница: https://user-roster-api.sandboxcernercentral.com/scim/v1/Realms/User-Roster-Realm-ID/ 

> Рабочая среда: https://user-roster-api.cernercentral.com/scim/v1/Realms/User-Roster-Realm-ID/ 

   * В hello **секрет маркера** токена носителя OAuth hello, созданного на шаге #3 введите и нажмите кнопку **проверить подключение**.

   * Вы увидите уведомление об успехе hello upperright части портала.

10. Введите адрес электронной почты hello пользователя или группы, которые должны получить уведомления о подготовке ошибки в hello **уведомление по электронной почте** поле и установите флажок "hello" ниже.

11. Щелкните **Сохранить**. 

12. В hello **сопоставления атрибутов** просмотрите пользователя hello и синхронизированы с Azure AD tooCerner центральный toobe атрибуты группы. Здравствуйте, атрибуты, выбранные в качестве **сопоставление** свойства, используемые toomatch hello учетных записей и групп в центральный Cerner для операций обновления. Выберите toocommit кнопку hello сохранить все изменения.

13. tooenable hello подготовки службы Azure AD для центрального Cerner, изменение hello **состояние подготовки** слишком**на** в hello **параметры** раздела

14. Щелкните **Сохранить**. 

Запустится hello Первоначальная синхронизация всех пользователей и/или группам назначается tooCerner центральный в разделе hello пользователей и групп. Начальная синхронизация Hello принимает tooperform больше времени, чем последующие синхронизации, которые происходят примерно каждые 20 минут до тех пор, пока выполняется hello подготовки службы Azure AD. Можно использовать hello **сведения о синхронизации** статьи toomonitor хода выполнения и следуйте ссылки tooprovisioning отчеты о действиях, описывающих все действия, выполненные программой подготовки службы на центральный Cerner приложения hello.

Дополнительные сведения о способ подготовки tooread hello Azure AD использует для входа см. в разделе [отчеты о автоматический подготовки пользователей. учетной записи](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Cerner Central: публикация данных удостоверений с помощью Azure AD](https://wiki.ucern.com/display/public/reference/Publishing+Identity+Data+Using+Azure+AD)
* [Руководство. Интеграция Azure Active Directory с Cerner Central](active-directory-saas-cernercentral-tutorial.md)
* [Управление подготовкой учетных записей пользователей для корпоративных приложений](active-directory-enterprise-apps-manage-provisioning.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a>Дальнейшие действия
* [Узнайте, каким образом ведет журнал tooreview и get сообщает о действиях по подготовке](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).
