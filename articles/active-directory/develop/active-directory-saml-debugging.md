---
title: "aaaHow toodebug на основе SAML единого входа tooapplications в Azure Active Directory | Документы Microsoft"
description: "Узнайте, как toodebug на основе SAML единого входа tooapplications в Azure Active Directory "
services: active-directory
author: asmalser-msft
documentationcenter: na
manager: femila
ms.assetid: edbe492b-1050-4fca-a48a-d1fa97d47815
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/20/2017
ms.author: asmalser
ms.custom: aaddev
ms.reviewer: dastrock
ms.openlocfilehash: 846c7b3497c8842947c5b406f4362b9e06785b14
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodebug-saml-based-single-sign-on-tooapplications-in-azure-active-directory"></a>Как toodebug на основе SAML единого входа tooapplications в Azure Active Directory
При отладке интеграции приложения на основе SAML, это часто полезно toouse средства, подобного [Fiddler](http://www.telerik.com/fiddler) toosee hello запрос SAML, ответ SAML hello и hello фактический маркер SAML выдаются toohello приложения. Изучив hello маркер SAML, убедитесь, что все hello обязательные атрибуты, Здравствуйте, имя пользователя в субъекта SAML hello и hello издателя URI поступающих через должным образом.

![][1]

Hello ответа от Azure AD, который содержит маркер SAML hello обычно является hello, происходит после перенаправления HTTP 302 с https://login.windows.net и настроен отправленных toohello **URL-адрес ответа** приложения hello. 

Маркер SAML hello можно просмотреть, выбрав эту строку, а затем выбрав hello **инспекторы > WebForms** вкладку на правой панели hello. После этого щелкните правой кнопкой мыши hello **SAMLResponse** значение и выберите **отправки tooTextWizard**. Выберите **Base64 из** из hello **преобразования** toodecode меню hello маркер и просмотреть его содержимое.

**Примечание**: toosee hello содержимое этого HTTP-запроса, Fiddler может запросить расшифровки tooconfigure трафик HTTPS, необходимо будет toodo.

## <a name="related-articles"></a>Связанные статьи
* [Указатель статьей по управлению приложениями в Azure Active Directory](../active-directory-apps-index.md)
* [Настройка одного tooapplications входа, которых нет в коллекции приложений Azure Active Directory hello](../active-directory-saas-custom-apps.md)
* [Как tooCustomize утверждений, выданных в hello токена SAML для Pre-Integrated приложений](active-directory-saml-claims-customization.md)

<!--Image references-->
[1]: ../media/active-directory-saml-debugging/fiddler.png