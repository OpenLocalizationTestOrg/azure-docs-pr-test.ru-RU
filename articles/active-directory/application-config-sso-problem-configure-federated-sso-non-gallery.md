---
title: "Настройка федеративного единого входа для приложения не коллекции aaaProblem | Документы Microsoft"
description: "Адрес hello распространенных проблем, которые могут возникнуть при настройке федеративного единого входа tooyour SAML прикладной, отсутствующих в hello коллекции приложений Azure AD."
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
ms.openlocfilehash: 8c80f0001de01cbc9930ef0441cd804082ee8578
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="problem-configuring-federated-single-sign-on-for-a-non-gallery-application"></a>Проблема при настройке федеративного единого входа для приложения не из коллекции

Если при настройке приложения возникла проблема, выполните следующие действия. Проверка выполнения всех шагов hello в статье hello [Настройка одной tooapplications входа, которых нет в коллекции приложений Azure Active Directory hello.](https://docs.microsoft.com/azure/active-directory/active-directory-saas-custom-apps)

## <a name="cant-add-another-instance-of-hello-application"></a>Не удается добавить другой экземпляр приложения hello

tooadd второй экземпляр приложения необходимые toobe возможность.

-   Настройте уникальный идентификатор для второго экземпляра hello. Не будет возможности tooconfigure приветствия же идентификатор, используемый для первого экземпляра hello.

-   Настройте другой сертификат hello, другая — для первого экземпляра hello.

Если hello приложение не предоставляет поддержку hello выше. Затем не будет возможности tooconfigure второй экземпляр.

## <a name="where-do-i-set-hello-entityid-user-identifier-format"></a>Устанавливаемый формат hello EntityID (идентификатор пользователя)

Его нельзя будет tooselect hello EntityID (идентификатор пользователя) формат, Azure AD отправляет toohello приложения hello ответа после проверки подлинности пользователя.

Azure AD выберите hello формат hello идентификатора имени атрибута (идентификатор пользователя) на основе выбранного значения hello или hello формат, запрошенный приложением hello в hello SAML AuthRequest. Дополнительные сведения можно найти в статье hello [протокола SAML](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) в разделе "hello" необязательного,

## <a name="where-do-i-get-hello-application-metadata-or-certificate-from-azure-ad"></a>Где получить метаданные приложения hello, или сертификат из Azure AD

метаданные приложения hello toodownload или сертификат от Azure AD, следуйте инструкциям hello:

1.  Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора** или **Co-администратору.**

2.  Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.

3.  Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.

4.  Нажмите кнопку **корпоративных приложений** из Azure Active Directory hello левого меню навигации.

5.  Нажмите кнопку **все приложения** tooview список всех приложений.

   * Используйте hello, если нужно показать здесь приложения hello не отображается, **фильтра** управления вверху hello hello **список всех приложений** и набор hello **Показать** параметр слишком **Все приложения.**

6.  Выберите приложение hello настройки единого входа.

7.  После загрузки приложения hello щелкните hello **единого входа** из приложения hello левого меню навигации.

8.  Go слишком**сертификат подписи SAML** статьи, а затем нажмите кнопку **загрузки** значение столбца. В зависимости от того, какое приложение hello требуется настроить единый вход вы увидите либо параметр toodownload hello hello метаданные в формате XML или hello сертификата.

Azure AD не предоставляет метаданных hello tooget URL-адрес. Hello метаданные могут быть получены только как XML-файл.

## <a name="dont-know-how-toocustomize-saml-claims-sent-tooan-application"></a>Не знаете, как утверждения SAML toocustomize отправлено tooan приложения

toolearn toocustomize hello SAML атрибут отправлять утверждений приложения tooyour разделе [утверждения сопоставления в Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) для получения дополнительной информации.

## <a name="next-steps"></a>Дальнейшие действия
[Управление приложениями с помощью Azure Active Directory](active-directory-enable-sso-scenario.md)
