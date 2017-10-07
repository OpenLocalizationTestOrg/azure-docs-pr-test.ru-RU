---
title: "Конечная точка v2.0 Active Directory aaaAzure | Документы Microsoft"
description: "Приложения toobuilding введение учетной записи Майкрософт и Azure Active Directory входа в систему."
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 2dee579f-fdf6-474b-bc2c-016c931eaa27
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/01/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: ae5946b02c50ae5a6137dc1decae66c96647e875
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="sign-in-microsoft-account--azure-ad-users-in-a-single-app"></a>Вход для пользователей учетных записей Майкрософт и Azure AD в одном приложении
В hello за разработчик приложения, которые хотели toosupport оба личные учетные записи Майкрософт и рабочих учетных записей из Azure Active Directory была необходимые toointegrate с двумя отдельными системами.  Hello **конечная точка Azure AD v2.0** предлагает новый вариант проверки подлинности API, позволяющая toosign в обоих типов учетных записей с помощью одной простой интеграции.  Приложения, использующие конечной точки v2.0 hello также может использовать API-интерфейс REST из hello [Microsoft Graph](https://graph.microsoft.io) с помощью любого типа учетной записи.

## <a name="getting-started"></a>Приступая к работе
Выберите избранные платформу из hello после списка toobuild приложения с помощью наших библиотеки с открытым исходным кодом и платформ.  Кроме того можно использовать наши toosend документации протокола OAuth 2.0 и OpenID Connect & принимают сообщения протокола напрямую без использования библиотеки проверки подлинности.

<br />

[!INCLUDE [active-directory-v2-quickstart-table](../../../includes/active-directory-v2-quickstart-table.md)]

## <a name="whats-new"></a>Новые возможности
здесь сведения Hello будет полезен для понимания, что такое & что невозможна с конечной точкой v2.0 hello.

* Дополнительные сведения о hello [типов приложений, можно построить с конечной точкой v2.0 hello](active-directory-v2-flows.md).
* Понимать hello [ограничения, ограничения и ограничения](active-directory-v2-limitations.md) с конечной точкой v2.0 hello.
* См. в этом обзоре видео для конечной точки v2.0 hello.

>[!VIDEO https://channel9.msdn.com/Events/Build/2017/P4031/player]

## <a name="reference"></a>Справочные материалы
Эти ссылки будут использоваться для изучения платформы hello подробно:

* [Справочник по протоколу версии 2.0](active-directory-v2-protocols.md)
* [Справочник по маркерам версии 2.0](active-directory-v2-tokens.md)
* [Справочник по библиотеке версии 2.0](active-directory-v2-libraries.md)
* [Области и согласие в конечной точке v2.0 hello](active-directory-v2-scopes.md)
* [Hello Microsoft Graph](https://graph.microsoft.io)

## <a name="help--support"></a>Справка и поддержка
Это hello наиболее местах tooget справки по разработке в Azure Active Directory.

* [Stack Overflow`azure-active-directory` и `adal`теги](http://stackoverflow.com/questions/tagged/azure-active-directory+or+adal)
* [Отзывы об Azure Active Directory](https://feedback.azure.com/forums/169401-azure-active-directory/category/164757-developer-experiences)


> [!NOTE]
> Если требуется только toosign в работу и учебную учетные записи из Azure Active Directory, следует начать с нашей [руководство разработчика Azure AD](active-directory-developers-guide.md).  Конечная точка v2.0 Hello предназначен для использования разработчиками, которые явно требуется toosign в личные учетные записи Майкрософт.

