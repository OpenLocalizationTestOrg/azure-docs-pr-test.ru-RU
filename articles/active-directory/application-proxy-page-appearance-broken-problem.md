---
title: "aaaApplication страницы отображается неправильно, для приложения прокси приложения | Документы Microsoft"
description: "Рекомендации, когда страница hello не правильно отображаться в приложении прокси приложения, интегрированные с Azure AD"
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
ms.openlocfilehash: f4abaa4e94c512868f2085affe59cac443784a56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="application-page-does-not-display-correctly-for-an-application-proxy-application"></a>Неправильное отображение страницы приложения для приложения прокси приложения

В этой статье помогут tootroubleshoot проблем с приложениями прокси приложения Azure Active Directory перейдите toohello страницы, когда что-нибудь на странице приветствия выглядит правильно.

## <a name="overview"></a>Обзор
При публикации приложения прокси приложения только страницы в корневом каталоге, доступны при доступе к приложения hello. Если страница hello не отображаются правильно, hello корневой внутреннего URL-адреса для приложения hello могут отсутствовать некоторые ресурсы страницы. tooresolve, убедитесь, что вы опубликовали *все* hello ресурсы для hello страницы как части приложения.

Можно проверить это проблема hello, открыв tracker вашей сети (такие как Fiddler или F12 средства в Internet Explorer или Edge), загрузка страницы hello и поиск ошибки 404. Указывает, hello страниц, которые в настоящее время не удается найти, а также по-прежнему может потребоваться toobe публикации.

Например связи данного варианта, предположим, вы опубликовали приложения расходы с помощью внутреннего URL-адреса из <http://myapps/expenses>, но приложение hello использует таблицу стилей hello <http://myapps/style.css>. В этом случае hello таблицы стилей не публикуется в приложении, поэтому загрузка прибыли приложение hello выдавать ошибку 404, при попытке tooload style.css. В этом примере hello проблема может быть решена публикации приложения hello внутренний URL-адрес <http://myapp/> вместо него.

## <a name="problems-with-publishing-as-one-application"></a>Проблемы при публикации в качестве одного приложения

Если это не возможно toopublish всех ресурсов в Здравствуйте того же приложения, нужно toopublish несколько приложений и включить ссылки между ними.

toodo таким образом, мы рекомендуем использовать hello [пользовательских доменов](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains) решения. Тем не менее это решение требует владения hello сертификат для домена и приложениях используются полные доменные имена (FQDN). Другие варианты см. в разделе hello [Устранение неполадок неработающих ссылок документации](https://microsoft-my.sharepoint.com/personal/harshja_microsoft_com/_layouts/15/guestaccess.aspx?guestaccesstoken=IxuG3mFVbnPWI3Yn4Qi7wCNi8VIfHS5mwPt5quh8DMw%3d&docid=2_14558cd6ddea34c1c9887dc640feb5831&rev=1).

## <a name="next-steps"></a>Дальнейшие действия
[Публикация приложений с помощью прокси приложения Azure AD](application-proxy-publish-azure-portal.md)
