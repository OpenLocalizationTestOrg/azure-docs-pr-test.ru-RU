---
title: "aaaHow toofind определенный интерфейс API, необходимые для приложения, разработанного | Документы Microsoft"
description: "Как требуется tooaccess конкретный API в пользовательских разрешений hello tooconfigure разработала приложение Azure AD"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 7331129204d8b34b4ef9671749bd702f893768ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toofind-a-specific-api-needed-for-a-custom-developed-application"></a>Как toofind определенный интерфейс API, необходимые для приложения, разработанного

TooAPIs доступа требуют настройки области доступа и ролей. Если требуется tooexpose tooclient ресурсов приложения веб-API-интерфейсов приложений требуется tooconfigure области доступа и роли для hello API. Если вы хотите tooaccess приложения клиента веб-API, необходимо API tooconfigure разрешения tooaccess hello в регистрации приложения hello.

## <a name="configuring-a-resource-application-tooexpose-web-apis"></a>Настройка ресурсов приложения tooexpose веб-API

При предоставлении доступа к веб-API, hello API отображаемый в hello **выберите API** список при добавлении регистрации приложения tooan разрешения. tooadd области доступа, следуйте hello действия, описанные в [Добавление доступа к области tooyour ресурсов приложения](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#adding-access-scopes-to-your-resource-application).

## <a name="configuring-a-client-application-tooaccess-web-apis"></a>Настройка клиентского приложения tooaccess веб-API

При добавлении регистрации приложения tooyour разрешения, вы можете **добавить доступ к API** tooexposed веб-API. tooaccess веб-API, выполните hello действия, описанные в [добавить учетные данные или разрешения tooaccess веб-API](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#to-add-credentials-or-permissions-to-access-web-apis).

## <a name="next-steps"></a>Дальнейшие действия

-   [Интеграция приложений с Azure Active Directory](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications)

-   [Основные сведения о манифесте приложения hello Azure Active Directory](https://docs.microsoft.com/azure/active-directory/develop/active-directory-application-manifest)


