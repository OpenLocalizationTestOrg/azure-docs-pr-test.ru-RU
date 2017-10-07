---
title: "Azure AD Connect: Hello обновления SSL-сертификат для фермы службы федерации Active Directory (AD FS) | Документы Microsoft"
description: "Этот документ сведения hello действия tooupdate hello SSL-сертификат фермы AD FS с помощью Azure AD Connect."
services: active-directory
keywords: "azure ad connect, обновление ssl adfs, обновление сертификата adfs, изменение сертификата adfs, новый сертификат adfs, сертификат adfs, обновление ssl-сертификата adfs, обновление ssl-сертификата adfs, настройка ssl-сертификата adfs, adfs, ssl, сертификат, сертификат взаимодействия со службой adfs, обновление федерации, настройка федерации, aad connect"
authors: anandyadavmsft
manager: femila
editor: billmath
ms.assetid: 7c781f61-848a-48ad-9863-eb29da78f53c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: anandy
ms.openlocfilehash: bce7f75aab83b6abacb8472a6895054d137e10e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="update-hello-ssl-certificate-for-an-active-directory-federation-services-ad-fs-farm"></a>Обновить сертификат SSL hello для фермы службы федерации Active Directory (AD FS)

## <a name="overview"></a>Обзор
В этой статье описывается, как можно использовать Azure AD Connect tooupdate hello SSL-сертификат для фермы службы федерации Active Directory (AD FS). Можно использовать hello Azure AD Connect tooeasily средство обновления hello SSL-сертификат для фермы hello AD FS, даже если hello пользователя войти выбранного метода не AD FS.

Можно выполнить hello всей операции обновления SSL-сертификат для фермы hello AD FS для всех федерации и прокси-сервера веб-приложения (WAP) серверов три простых шагов.

![Три шага](./media/active-directory-aadconnectfed-ssl-update/threesteps.png)


>[!NOTE]
>toolearn Дополнительные сведения о сертификаты, используемые службами AD FS в разделе [основные сведения о сертификатах, используемых службами AD FS](https://technet.microsoft.com/library/cc730660.aspx).

## <a name="prerequisites"></a>Предварительные требования

* **Ферма AD FS.** Убедитесь, что ферма AD FS работает под управлением Windows Server 2012 R2 или более поздней версии.
* **Azure AD Connect**: Убедитесь, что hello версия Azure AD Connect — 1.1.443.0 или более поздней версии. Будем использовать задачу hello **обновления AD FS SSL-сертификат**.

![Задача обновления SSL](./media/active-directory-aadconnectfed-ssl-update/updatessltask.png)

## <a name="step-1-provide-ad-fs-farm-information"></a>Шаг 1. Предоставление сведений о ферме AD FS

Azure AD Connect автоматически предпримет tooobtain сведения о ферме hello AD FS.
1. Запроса сведений о ферме hello из службы федерации Active Directory (Windows Server 2016 или более поздней версии).
2. Ссылка на сведения hello из предыдущего выполнения, в котором хранятся локально с Azure AD Connect.

Вы можете изменить hello список серверов, которые отображаются, добавив или удалив hello серверов tooreflect hello текущей конфигурации фермы hello AD FS. Как только сведения о сервере hello предоставляется, Azure AD Connect отображает hello подключения и текущее состояние сертификата SSL.

![Сведения о сервере AD FS](./media/active-directory-aadconnectfed-ssl-update/adfsserverinfo.png)

Если список hello содержит сервера, который больше не является частью фермы hello AD FS, щелкните **удалить** toodelete hello сервер из списка серверов в ферме AD FS hello.

![Автономный сервер в списке](./media/active-directory-aadconnectfed-ssl-update/offlineserverlist.png)

>[!NOTE]
> Удаление сервера из списка hello серверов AD FS фермы в Azure AD Connect локального операция и обновления hello сведения для hello фермы AD FS, который поддерживает Azure AD Connect, локально. Azure AD Connect не изменяет конфигурации hello при изменении hello tooreflect AD FS.    

## <a name="step-2-provide-a-new-ssl-certificate"></a>Шаг 2. Указание нового SSL-сертификата

После подтверждения hello сведения о серверах фермы AD FS, Azure AD Connect запрашивает hello новый SSL-сертификат. Укажите защищенный паролем PFX toocontinue hello установки сертификата.

![SSL-сертификат](./media/active-directory-aadconnectfed-ssl-update/certificate.png)

После ввода hello сертификат Azure AD Connect проходит через ряд необходимых компонентов. Проверьте правильность tooensure сертификат hello, hello сертификат фермы hello AD FS:

-   Hello субъекта имени или альтернативного имени субъекта для hello сертификат может быть Здравствуйте таким же, как имя службы федерации hello, или он представляет собой групповой сертификат.
-   Hello сертификат действителен в течение более 30 дней.
-   цепь доверия сертификатов Hello является допустимым.
-   Hello сертификат, защищен паролем.

## <a name="step-3-select-servers-for-hello-update"></a>Шаг 3: Выбор серверов для обновления hello

В следующем шаге hello выберите hello серверам, нуждающимся toohave hello SSL-сертификат обновлен. Серверы, которые находятся в автономном режиме нельзя выбрать для обновления hello.

![Выберите серверы tooupdate](./media/active-directory-aadconnectfed-ssl-update/selectservers.png)

После завершения настройки hello Azure AD Connect отображает приветственное сообщение, указывающее состояние обновления hello hello и предоставляет параметр tooverify hello AD FS вход.

![Завершение настройки](./media/active-directory-aadconnectfed-ssl-update/configurecomplete.png)   

## <a name="faqs"></a>Часто задаваемые вопросы

* **Что должны быть hello. имя субъекта сертификата hello hello новый сертификат AD FS SSL?**

    Azure AD Connect проверяет, содержит ли имя субъекта имени или альтернативного hello субъекта сертификата hello hello имя службы федерации. Например если имя службы федерации fs.contoso.com, hello субъекта имени или альтернативного субъекта имя должно быть fs.contoso.com.  Поддерживаются также групповые сертификаты.

* **Почему появляется учетные данные снова на странице сервера WAP hello?**

    Если hello учетные данные, предоставленные для подключения серверов федерации Active Directory tooAD также нет hello прав toomanage hello WAP-серверах, затем Azure AD Connect запрашивает учетные данные, имеющие административные привилегии на hello WAP-серверах.

* **Hello сервер отображается как отключенный. Что делать?**

    Azure AD Connect не может выполнить любую операцию, если сервер hello отключен. Если hello server является частью hello фермы AD FS, проверьте сервер toohello hello подключения. После разрешения проблемы hello, нажмите клавишу состояние hello tooupdate значок обновления hello в мастере hello. Если сервер hello входила в состав из hello фермы ранее, но теперь больше не существует, щелкните **удалить** toodelete поддерживает его из списка серверов, Azure AD Connect hello. Удаление сервера hello из списка hello в Azure AD Connect не изменяет hello сама конфигурация AD FS. Если вы используете службы федерации Active Directory в Windows Server 2016 или более поздней версии, hello server остается в параметрах конфигурации hello и отображается снова hello при очередном hello выполнения задачи.

* **Можно обновить подмножество моей ферме серверов с hello новый SSL-сертификат?**

    Да. Всегда иметь возможность выполнить задачу hello **обновления SSL-сертификат** снова tooupdate hello оставшихся серверов. На hello **обновления сертификатов выберите серверы для использования SSL** страницы, можно выполнить сортировку hello список серверов по **даты истечения срока действия SSL** tooeasily доступа hello серверы, которые еще не обновлены.

* **Я удалил сервера hello в hello предыдущего запуска, но она по-прежнему показывается как вне сети и перечисленные на странице приветствия AD FS серверы. Почему необходимо hello автономный сервер по-прежнему существует, даже после того, она удалена?**

    Удаление сервера hello из списка hello в Azure AD Connect не удаляет его в hello конфигурации AD FS. Azure AD Connect ссылается на AD FS (Windows Server 2016 или более поздней версии), все сведения о ферме hello. Если hello server по-прежнему присутствует в hello конфигурации AD FS, отображаются в списке hello.  

## <a name="next-steps"></a>Дальнейшие действия

- [Azure AD Connect и федерация](active-directory-aadconnectfed-whatis.md)
- [Управление службами федерации Active Directory и их настройка с помощью Azure AD Connect](active-directory-aadconnect-federation-management.md)
