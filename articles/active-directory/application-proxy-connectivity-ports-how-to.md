---
title: "брандмауэр aaaHow tooopen hello порты, необходимые для приложения прокси приложения | Документы Microsoft"
description: "Правильно определить какие порты tooopen для toowork прокси приложения hello Azure AD"
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
ms.openlocfilehash: cdc7badb7c15591689a3bfd6bb26da182b00fb3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooopen-hello-firewall-ports-required-for-an-application-proxy-application"></a>Как tooopen hello порты брандмауэра, необходимые для приложения прокси приложения

Полный список hello необходимые порты и функции hello каждого порта toosee разделе hello необходимые компоненты hello [документации прокси-сервера приложения](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-enable). Обратите внимание, что прокси приложения использует только исходящие порты.

Можно также проверить, имеют ли все открытые порты hello необходимые путем открытия hello [средство тестирования порты соединитель](https://aadap-portcheck.connectorporttest.msappproxy.net/) из локальной сети. Большее число зеленых флажков означает большую устойчивость. 

## <a name="app-proxy-regions"></a>Регионы прокси приложения

Мы работаем над toolet можно узнать, какие из этих областей требуется toobe зеленый для вас образом. Пока убедитесь, что все регионы выделены зеленым цветом. Регион "Центральная часть США" должен быть выделен зеленым цветом независимо от того, в каком регионе вы находитесь.

предоставляет hello средство toomake для убедиться, что hello правильные результаты быть убедитесь, что:

-   Откройте средство hello в браузере с сервера hello, где установлен соединитель hello.

-   Убедитесь, что все прокси-серверы или брандмауэры tooyour применимо, соединитель, также применены toothis страницы. Это можно сделать в Internet Explorer, перейдя слишком**параметры**  - &gt; **обозревателя**  - &gt; **подключений**  - &gt; **Параметры локальной сети**. На этой странице вы видите hello поле «Использовать прокси-сервера сервера для ЛС». Установите этот флажок и поместите hello адрес прокси-сервера в поле «Адрес» hello.

## <a name="next-steps"></a>Дальнейшие действия
[Сведения о соединителях прокси приложения Azure AD](application-proxy-understand-connectors.md)
