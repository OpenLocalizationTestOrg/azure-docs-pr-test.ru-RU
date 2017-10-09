---
title: "сертификаты aaaManage федерации в Azure AD | Документы Microsoft"
description: "Узнайте, как toocustomize hello срок действия сертификатов федерации, а также как toorenew сертификатов, которые скоро истекает."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: f516f7f0-b25a-4901-8247-f5964666ce23
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/09/2017
ms.author: jeedes
ms.openlocfilehash: e17622d25c9babfa295cc0bb68c24e21b8c574d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-certificates-for-federated-single-sign-on-in-azure-active-directory"></a>Управление сертификатами для федеративного единого входа в Azure Active Directory
В этой статье рассматриваются распространенные вопросы и сведения о связанных toohello сертификатов, что Azure Active Directory (Azure AD) создает tooestablish федеративного единого входа (SSO) tooyour приложений SaaS. Добавление приложения из коллекции приложений Azure AD hello или с помощью шаблона приложения не коллекции. Настройте приложение hello с помощью параметра hello федеративного единого входа.

В этой статье — применимо только tooapps, которые настроенное toouse единого входа Azure AD через федерацию SAML, как показано в следующий пример hello:

![Единый вход в Azure AD](./media/active-directory-sso-certs/saml_sso.PNG)

## <a name="auto-generated-certificate-for-gallery-and-non-gallery-applications"></a>Автоматически созданный сертификат для приложений из коллекции и не из коллекции
При добавлении нового приложения из коллекции hello и настроить SAML входа на основе, Azure AD создает сертификат для приложения hello, действителен в течение трех лет. Этот сертификат можно загрузить из hello **сертификат подписи SAML** раздела. Для приложений, коллекции в этом разделе могут отображаться параметр toodownload hello сертификата или метаданные, в зависимости от требований hello приложения hello.

![Единый вход Azure AD](./media/active-directory-sso-certs/saml_certificate_download.png)

## <a name="customize-hello-expiration-date-for-your-federation-certificate-and-roll-it-over-tooa-new-certificate"></a>Настроить срок действия вашего сертификата федерации hello и Смена tooa новый сертификат
По умолчанию сертификаты устанавливаются tooexpire после трех лет. Можно выбрать другой срок действия вашего сертификата, выполнив следующие шаги hello.
снимки экрана приветствия использовать Salesforce ради hello примера, но эти действия можно применить tooany федеративных приложений SaaS.

1. В hello [портал Azure](https://aad.portal.azure.com), нажмите кнопку **корпоративного приложения** в hello левой панели, а затем нажмите кнопку **новое приложение** на hello **Обзор** страница:

   ![Привет открыть мастер настройки единого входа](./media/active-directory-sso-certs/enterprise_application_new_application.png)

2. Найти приложение hello коллекции, а затем выберите требуемый tooadd приложения hello. Если не удается найти hello необходимые приложения, добавить hello приложения с помощью hello **приложения без коллекции** параметр. Эта функция доступна только в hello SKU Azure AD Premium (P1 и P2).

    ![Единый вход Azure AD](./media/active-directory-sso-certs/add_gallery_application.png)

3. Щелкните hello **единого входа** ссылку в hello слева области и изменение **режим-** слишком**входа на базе SAML**. При этом для вашего приложения будет создан сертификат со сроком действия 3 года.

4. toocreate новый сертификат, нажмите кнопку hello **Создание нового сертификата** ссылку в hello **сертификат подписи SAML** раздела.

    ![Создание нового сертификата](./media/active-directory-sso-certs/create_new_certficate.png)

5. Hello **создать новый сертификат** ссылка открывает hello управления calendar. Можно задать любой даты и времени вверх toothree лет от hello текущую дату. Hello даты и времени задан hello новую дату окончания срока действия и время ваш новый сертификат. Щелкните **Сохранить**.

    ![Загрузить, а затем отправить сертификат hello](./media/active-directory-sso-certs/certifcate_date_selection.PNG)

6. Теперь новый сертификат hello доступных toodownload. Нажмите кнопку hello **сертификат** ссылку toodownload его. На этом этапе сертификат еще не активен. Tooroll над toothis сертификат, выберите hello **активировать новый сертификат** флажок и нажмите кнопку **Сохранить**. С этого момента Azure AD запускается hello новый сертификат для подписи ответа hello.

7.  toolearn tooupload hello сертификатов tooyour определенному приложению SaaS, нажмите кнопку hello **просмотреть учебник конфигурации приложения** ссылку.

## <a name="renew-a-certificate-that-will-soon-expire"></a>Обновление сертификата с истекающим сроком действия
Hello следующие шаги обновления должны появиться без значительного простоя, необходимого для пользователей. снимки экрана приветствия в этот раздел компонент Salesforce пример, но эти действия можно применить tooany федеративных приложений SaaS.

1. На hello **Azure Active Directory** приложения **единого входа** страницы, создание hello новый сертификат для вашего приложения. Это можно сделать, щелкнув hello **Создание нового сертификата** ссылку в hello **сертификат подписи SAML** раздела.

    ![Создание нового сертификата](./media/active-directory-sso-certs/create_new_certficate.png)

2. Выберите hello требуемого Дата окончания срока действия и время для нового сертификата и нажмите кнопку **Сохранить**.

3. Загрузите сертификат hello в hello **сертификат подписи SAML** параметр. Экран настройки единого входа для передачи hello новый сертификат toohello SaaS приложения. toolearn как toodo для определенного приложения SaaS, нажимайте hello **просмотреть учебник конфигурации приложения** ссылку.
   
4. новый сертификат tooactivate hello в Azure AD, выберите hello **активировать новый сертификат** флажок и нажмите кнопку hello **Сохранить** кнопку вверху hello страницы приветствия. Это перейдет hello нового сертификата на стороне Azure AD hello. Изменение состояния Hello hello сертификата с **New** слишком**Active**. С этого момента Azure AD запускается hello новый сертификат для подписи ответа hello. 
   
    ![Создание нового сертификата](./media/active-directory-sso-certs/new_certificate_download.png)

## <a name="related-articles"></a>Связанные статьи
* [Список учебников по toointegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Указатель статей по управлению приложениями в Azure Active Directory](active-directory-apps-index.md)
* [Доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md)
* [Устранение неполадок единого входа на основе SAML](active-directory-saml-debugging.md)
