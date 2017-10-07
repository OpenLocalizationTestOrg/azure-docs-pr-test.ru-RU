---
title: "Руководство по настройке подготовки пользователей в Workplace by Facebook | Документация Майкрософт"
description: "Узнайте, как tooautomatically подготовки и Отмена подготовки учетные записи из Azure AD tooWorkplace с Facebook."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6341e67e-8ce6-42dc-a4ea-7295904a53ef
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 33d294dbc8f441b29138408b3c9ca41f2141f8af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configure-workplace-by-facebook-for-user-provisioning"></a>Руководство по настройке Workplace by Facebook для подготовки пользователей

Этот учебник показывает, hello tooautomatically необходимые действия предоставлять и отзывать учетные записи пользователей из Azure Active Directory (Azure AD) tooWorkplace с Facebook.

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD в рабочей области с Facebook, необходимы следующие hello.

- подписка Azure AD;
- подписка Workplace by Facebook с поддержкой единого входа.

tootest hello шаги в этом учебнике, придерживайтесь следующих рекомендаций:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).

## <a name="assign-users-tooworkplace-by-facebook"></a>Назначить пользователей tooWorkplace с Facebook

Azure AD использует называемый «назначения» toodetermine пользователей, которые должны получать доступ tooselected приложений. В контексте hello автоматический подготовки пользователей. учетной записи синхронизируются только hello пользователей и групп, которые были назначены tooan приложения в Azure AD.

Прежде чем решить, настройке и включении hello подготовки службы, какие пользователи и группы в Azure AD представляют Привет пользователей, которым требуется доступ tooyour рабочей области приложения Facebook. Вы можете назначить эти пользователи tooyour рабочей области, приложением Facebook, следуя инструкциям hello [назначить пользователю или группе tooan корпоративного приложения](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal).

>[!IMPORTANT]
>*   Hello тест инициализации конфигурации путем назначения одной tooWorkplace пользователя Azure AD с Facebook. Дополнительных пользователей и группы можно будет назначить позже.
>*   При назначении tooWorkplace пользователя с Facebook, необходимо выбрать допустимой роли пользователя. роли доступа по умолчанию Hello не работает для подготовки.

## <a name="enable-automated-user-provisioning"></a>Включение автоматической подготовки пользователей

Этот раздел поможет выполнить подключение учетной записи пользователя toohello Azure AD подготовки API из рабочей области с Facebook. Вы также узнаете, как обновить toocreate tooconfigure hello подготовки службы и отключить учетные записи пользователей, назначенные в рабочей области с Facebook. Это зависит от назначенных пользователей и групп в Azure AD.

>[!Tip]
>Вы также можете tooenabled SSO на основе SAML для рабочей области с Facebook, по следующие hello следуйте инструкциям в hello [портал Azure](https://portal.azure.com). Единый вход можно настроить независимо от автоматической подготовки, хотя две эти функции дополняют друг друга.

### <a name="configure-user-account-provisioning-tooworkplace-by-facebook-in-azure-ad"></a>Настройка учетной записи пользователя, подготовку tooWorkplace с Facebook в Azure AD

Azure AD поддерживается tooautomatically hello возможность синхронизировать данные для учетной записи hello назначить пользователей tooWorkplace с Facebook. Автоматический процесс синхронизации включает рабочей области по Facebook tooget hello данных tooauthorize пользователей для доступа, необходимые перед их выполнением toosign в для hello в первый раз. Она также отменяет подготовку пользователей для Workplace by Facebook, если доступ для них отозван в Azure AD.

1. В hello [портал Azure](https://portal.azure.com)выберите **Azure Active Directory** > **корпоративных приложений** > **все приложения**.

2. Если вы уже настроили рабочему месту с Facebook для единого входа, выполните поиск экземпляра рабочей области с Facebook с помощью поля поиска hello. В противном случае выберите **добавить** и выполните поиск **рабочему месту с Facebook** в галерее приложения hello. Выберите **рабочему месту с Facebook** из hello результаты поиска и добавьте его tooyour список приложений.

3. Выберите свой экземпляр рабочему месту с Facebook, а затем выберите hello **Provisioning** вкладки.

4. Задать **режим подготовки** слишком**автоматического**. 

    ![Снимок экрана параметров подготовки Workplace by Facebook](./media/active-directory-saas-facebook-at-work-provisioning-tutorial/provisioning.png)

5. В разделе hello **учетные данные администратора** введите hello **секрет маркера** и hello **URL-адрес клиента** рабочего места администратора Facebook.

6. В hello портал Azure, выберите **проверить подключение** tooensure Azure AD могут подключаться tooyour рабочей области приложения Facebook. При сбое подключения hello, убедитесь в наличии разрешения администратора команды в рабочую область с учетной записью Facebook.

7. Введите адрес электронной почты hello пользователя или группы, которые должны получить уведомления о подготовке ошибки в hello **уведомление по электронной почте** поля и приветствия установите флажок.

8. Щелкните **Сохранить**.

9. Установите hello сопоставлений **tooWorkplace синхронизации Azure Active Directory-пользователи с Facebook**.

10. В hello **сопоставления атрибутов** просмотрите hello атрибутов пользователей, которые синхронизируются из tooWorkplace Azure AD с Facebook. Здравствуйте, атрибуты, выбранные в качестве **сопоставление** свойства, используемые toomatch hello учетных записей пользователей в рабочей области с Facebook для операций обновления. Выберите любые изменения toocommit **Сохранить**.

11. tooenable hello подготовки службы Azure AD для рабочей области с Facebook, в hello **параметры** измените hello **состояние подготовки** слишком**на**.

12. Щелкните **Сохранить**.

Дополнительные сведения о том, как tooconfigure автоматической подготовки, в разделе [hello Facebook документации](https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers).

Теперь можно создать тестовую учетную запись. Дождитесь копирование минут too20 tooverify, hello учетная запись была синхронизирована tooWorkplace с Facebook.

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Управление подготовкой учетных записей пользователей для корпоративных приложений](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Настройка единого входа](active-directory-saas-facebook-at-work-tutorial.md)

