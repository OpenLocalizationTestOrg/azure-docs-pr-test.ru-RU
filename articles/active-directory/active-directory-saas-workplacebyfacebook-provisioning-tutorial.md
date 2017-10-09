---
title: "Руководство по интеграции Azure Active Directory с Workplace by Facebook | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и рабочей области с Facebook."
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
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 551ec353a5ec1da936373587688c299a6f4acca7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-workplace-by-facebook-for-user-provisioning"></a>Руководство по настройке Workplace by Facebook для подготовки пользователей

Цель этого учебника Hello — tooshow hello действия, которые следует tooperform в рабочей области с Facebook и Azure AD tooautomatically подготовки и Отмена подготовки учетных записей пользователей из Azure AD tooWorkplace с Facebook.

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD в рабочей области с Facebook, требуется hello следующих элементов:

- подписка Azure AD;
- подписка Workplace by Facebook с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="assigning-users-tooworkplace-by-facebook"></a>Назначение пользователей tooWorkplace с Facebook

Azure Active Directory использует называемый «назначения» toodetermine пользователей, которые должны получать доступ tooselected приложений. В контексте hello автоматический подготовки пользователей. учетной записи синхронизируются только hello пользователей и групп, назначенных» «tooan приложения в Azure AD.

Для настройки и включения hello подготовки службы, требуется toodecide какие пользователи или группы в Azure AD представляют Привет пользователей, которым требуется доступ tooyour рабочей области приложения Facebook. После приняла решение, можно назначить эти пользователи tooyour рабочей области, приложением Facebook в соответствии с инструкциями hello здесь:

[Назначить пользователю или группе tooan корпоративного приложения](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-tooworkplace-by-facebook"></a>Важные советы для назначения пользователей tooWorkplace с Facebook

*   Рекомендуется один tooWorkplace назначен пользователь Azure AD путем настройки подготовки hello tootest Facebook. Дополнительные пользователи и/или группы можно назначить позднее.

*   При назначении tooWorkplace пользователя с Facebook, необходимо выбрать допустимой роли пользователя. роль «Доступ по умолчанию» Hello не работает для подготовки.

## <a name="enable-user-provisioning"></a>Включение подготовки пользователей

Этот раздел поможет выполнить подключение к Azure AD tooWorkplace учетной записью Facebook подготовки API и настройке подготовки службы toocreate hello, обновления и отключить учетные записи пользователей, назначенные в рабочей области с Facebook, на основе пользователя и группы Назначение в Azure AD.

>[!Tip]
>Можно также выбрать tooenabled на основе SAML Single Sign-On для рабочей области с Facebook, следуя инструкциям hello в [портал Azure](https://portal.azure.com). Единый вход можно настроить независимо от автоматической подготовки, хотя эти две возможности дополняют друг друга.

### <a name="tooconfigure-user-account-provisioning-tooworkplace-by-facebook-in-azure-ad"></a>tooconfigure учетная запись подготовки tooWorkplace с Facebook в Azure AD:

Цель этого раздела Hello является toooutline как tooenable Подготовка пользователя Active Directory учетных записей tooWorkplace с Facebook.

Azure AD поддерживается tooautomatically hello возможность синхронизировать данные для учетной записи hello назначить пользователей tooWorkplace с Facebook. Автоматический процесс синхронизации включает рабочей области по Facebook tooget hello данных tooauthorize пользователей для доступа, необходимые перед их выполнением toosign в для hello в первый раз. Она также отменяет подготовку пользователей для Workplace by Facebook, если доступ для них отозван в Azure AD.

1. В hello [портал Azure](https://portal.azure.com), Обзор toohello **Azure Active Directory** > **корпоративных приложений** > **всех приложений** раздела.

2. Если вы уже настроили рабочему месту с Facebook для единого входа, поиск экземпляра рабочей области с Facebook с помощью поля поиска hello. В противном случае выберите **добавить** и выполните поиск **рабочему месту с Facebook** в галерее приложения hello. Выбор рабочей области с Facebook из результатов поиска hello и добавьте его tooyour список приложений.

3. Выберите свой экземпляр рабочему месту с Facebook, а затем выберите hello **Provisioning** вкладки.

4. Набор hello **режим подготовки** слишком**автоматического**. 

    ![подготовка](./media/active-directory-saas-workplacebyfacebook-provisioning-tutorial/provisioning.png)

5. В разделе hello **учетные данные администратора** статьи, введите секрет маркера hello и hello URL-адрес клиента рабочего места администратора Facebook.

6. В hello портал Azure, щелкните **проверить подключение** tooensure Azure AD могут подключаться tooyour рабочей области приложения Facebook. При сбое подключения hello, убедитесь, что рабочую область с учетной записью Facebook имеет разрешения администратора команды.

7. Введите адрес электронной почты hello пользователя или группы, которые должны получить уведомления о подготовке ошибки в hello **уведомление по электронной почте** поле и установите флажок "hello".

8. Нажмите кнопку **Сохранить**.

9. Установите hello сопоставлений **tooWorkplace синхронизации Azure Active Directory-пользователи с Facebook.**

10. В hello **сопоставления атрибутов** просмотрите hello атрибутов пользователей, которые синхронизируются из tooWorkplace Azure AD с Facebook. Здравствуйте, атрибуты, выбранные в качестве **сопоставление** свойства, используемые toomatch hello учетных записей пользователей в рабочей области с Facebook для операций обновления. Выберите toocommit кнопку hello сохранить все изменения.

11. tooenable hello подготовки службы Azure AD для рабочей области с Facebook, изменение hello **состояние подготовки** слишком**на** в hello **параметры** раздела

12. Нажмите кнопку **Сохранить**.

Дополнительные сведения о том, как tooconfigure автоматической подготовки, в разделе [https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers](https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers)

Теперь можно создать тестовую учетную запись. Дождитесь копирование минут too20 tooverify, hello учетная запись была синхронизирована tooWorkplace с Facebook.

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Управление подготовкой учетных записей пользователей для корпоративных приложений](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Настройка единого входа](active-directory-saas-workplacebyfacebook-tutorial.md)

