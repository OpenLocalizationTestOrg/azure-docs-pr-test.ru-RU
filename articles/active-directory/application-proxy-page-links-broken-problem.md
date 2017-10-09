---
title: "aaaLinks на странице приветствия не поддерживаются для приложения прокси приложения | Документы Microsoft"
description: "Как tootroubleshoot проблемы с неработающие ссылки на приложения прокси приложения, которые интегрированы с Azure AD"
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
ms.openlocfilehash: 77c1e22d27c7a6436d8e57e105037c2328180481
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="links-on-hello-page-dont-work-for-an-application-proxy-application"></a>Не поддерживаются ссылки на странице приветствия для приложения прокси приложения

В этой статье помогут tootroubleshoot, почему ссылки на приложение прокси приложения Azure Active Directory не работают правильно.

## <a name="overview"></a>Обзор 
После публикации приложения прокси приложения, hello только ссылки, toodestinations ссылок, содержащихся в hello работы по умолчанию в приложение hello опубликованы корневой URL-адрес. Hello ссылки внутри приложения hello не работают, hello внутренний URL-адрес для приложения hello, скорее всего, не включает все назначения hello ссылок в приложение hello.

**Почему это происходит?** При ссылке в приложение, попытками URL-адрес tooresolve hello как внутренний URL в пределах прокси приложения hello же приложения, так и внешним доступом URL-адрес. Если ссылка hello указывает tooan внутренний URL-адрес, не находится в hello же приложений, не принадлежит tooeither этих контейнеров и привести к ошибке не найдено.

## <a name="ways-you-can-resolve-broken-links"></a>Способы решения проблемы с неработающими ссылками

Существует три способа tooresolve эту проблему. Hello ниже доступны перечисленные в возрастающей сложности.

1.  Убедитесь, что hello внутренний URL-адрес является корневым элементом, который содержит все соответствующие ссылки hello для приложения hello. Это позволяет toobe все ссылки, разрешены в процессе публикации содержимого в пределах hello же приложения.

    Если вы измените hello внутренний URL-адрес, но не хотите toochange hello стартовая страница для пользователей, изменение hello URL-адрес домашней страницы toohello публиковалась внутренний URL-адрес. Это можно сделать, перейдя слишком «Azure Active Directory» —&gt; регистрации приложения -&gt; выберите приложение hello -&gt; свойства. На этой вкладке свойств разделе hello поле «URL домашней страницы», это значение можно изменить toobe hello требуемого стартовой страницы.

2.  Если в приложениях используются полные доменные имена (FQDN), используйте [пользовательских доменов](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains) toopublish приложений. Эта функция позволяет hello toobe же URL-адрес используется как внутри, так и извне.

    Этот параметр обеспечивает доступном через прокси-сервер приложения hello ссылки в приложении с момента hello ссылки в URL-адреса toointernal приложения hello также распознаются извне. Обратите внимание, что все ссылки по-прежнему toobelong tooa опубликованное приложение. Тем не менее, с помощью этого параметра hello ссылки не обязательно toobelong toohello того же приложения и могут принадлежать toomultiple приложений.

3.  Если ни один из этих параметров осуществимы присоединения hello Предварительный просмотр нового компонента, перезаписи URL-адрес преобразования /. Этот параметр внутреннего URL-адреса или ссылки, которые существуют в тексте hello HTML приложений будет преобразовать или «сопоставить», toohello опубликованные внешние URL-адреса прокси-сервера приложения. Это работает только для ссылок в hello HTML и CSS, и это не поможет, если ссылка на созданный с помощью JS. 

Поэтому настоятельно рекомендуется использовать hello [пользовательских доменов](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains) решение, если это возможно. Если требуется предварительная версия hello toojoin отправить < aadapfeedback@microsoft.com > с hello applicationId(s).

## <a name="next-steps"></a>Дальнейшие действия
[Работа с имеющимися локальными прокси-серверами](application-proxy-working-with-proxy-servers.md)

