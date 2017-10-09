---
title: "приложения с конечной точкой v2.0 hello Azure AD, с помощью портала hello aaaRegister | Документы Microsoft"
description: "Как tooregister приложение с Microsoft для включения вход и доступ к Microsoft службы с помощью конечной точки v2.0 hello"
services: active-directory
documentationcenter: 
author: lnalepa
manager: mbaldwin
editor: 
ms.assetid: bb2f701f-3bc3-4759-94a5-8b9d53a8a0b6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/01/2017
ms.author: lenalepa
ms.custom: aaddev
ms.openlocfilehash: c56c98906656062435516e820cb318a04c03149c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooregister-an-app-with-hello-v20-endpoint"></a>Как tooregister приложения с конечной точкой v2.0 hello
приложение, которое принимает MSA & Azure AD toobuild входа в систему понадобится сначала tooregister приложение с Microsoft.  В настоящее время не будет иметь возможности toouse любые существующие приложения с Azure AD может быть или MSA - потребуется toocreate марку новый.

> [!NOTE]
> Не все сценарии Azure Active Directory и возможности поддерживаются hello v2.0 конечной точкой.  toodetermine, если необходимо использовать конечную точку v2.0 hello, прочтите сведения о [ограничения v2.0](active-directory-v2-limitations.md).
> 
> 

## <a name="visit-hello-microsoft-app-registration-portal"></a>Посетите портал регистрации приложения Microsoft hello
Начните сначала - перейдите слишком[https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList).  Это новый портал регистрации приложений, где вы можете управлять своими приложениями Майкрософт.

Войти с помощью личной, рабочей или учебной учетной записи Майкрософт.  Если у вас нет учетной записи, зарегистрируйтесь для получения личной учетной записи. Вперед, это не займет много времени.

Готово? Теперь вы должны увидеть список своих приложений Майкрософт, который, вероятно, пуст.  Изменим это.

Щелкните **Добавить приложение**и присвойте приложению имя.  Hello портала будет назначать глобальный уникальный идентификатор приложения, которое будет использоваться в коде приложения.  Если приложение включает в себя серверный компонент, требующий токены доступа для вызова API (подумать: Office, Azure или ваши собственные веб-API), вам потребуется toocreate **секрет приложения** таким же образом.

Затем добавьте hello платформы, используемые вашим приложением.

* Для веб-приложений укажите **универсальный код ресурса (URI) перенаправления** для отправки сообщений о входе.
* Для мобильных приложений uri, автоматически создается перенаправления копирования вниз по умолчанию hello.

При необходимости можно настроить hello внешний вид и поведение в hello профиля страницы входа.  Убедитесь, что tooclick **Сохранить** прежде чем продолжить.

> [!NOTE]
> При создании приложения с помощью [https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), в клиенте домашней hello hello учетной записи используется toosign hello портал будет зарегистрировано приложение hello.  Это означает, что нельзя зарегистрировать приложение в клиенте Azure AD с помощью личной учетной записи Майкрософт.  Если явно нужно tooregister приложения в конкретного клиента, войдите под учетной записью создан этого клиента.
> 
> 

## <a name="build-a-quick-start-app"></a>Создание приложения быстрого запуска
Теперь, когда у вас есть приложение Майкрософт, вы можете изучить один из кратких учебников по версии 2.0.  Вот несколько рекомендаций.

[!INCLUDE [active-directory-v2-quickstart-table](../../../includes/active-directory-v2-quickstart-table.md)]

