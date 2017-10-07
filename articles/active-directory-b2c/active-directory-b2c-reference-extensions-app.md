---
title: "Приложения расширений Azure Active Directory B2C | Документация Майкрософт"
description: "Восстановление b2c-расширений приложение hello"
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: f0392e32-0771-473c-a799-81438ca2bcff
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/17/2017
ms.author: parja
ms.openlocfilehash: b36410c18314bd893dc669b49814fdcd77fae054
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-extensions-app"></a>Azure AD B2C: приложение расширений

Вызывается при создании каталога Azure AD B2C приложения `b2c-extensions-app. Do not modify. Used by AADB2C for storing user data.` автоматически создается внутри нового каталога hello. Этого приложения, который ссылается tooas hello **b2c расширения приложения**, отображается в *регистрации приложения*. Он используется hello Azure AD B2C службы toostore сведения о пользователях и настраиваемых атрибутов. При удалении приложения hello Azure AD B2C не будет работать правильно, и повлияет на рабочую среду.

> [!IMPORTANT]
> Не удаляется b2c-расширений приложение hello, если вы планируете удалить tooimmediately вашего клиента. Если приложение hello остается удаленные более 30 дней, сведения о пользователе будет безвозвратно потеряно.

## <a name="verifying-that-hello-extensions-app-is-present"></a>Проверка того, приложение hello расширения присутствует

присутствует tooverify, hello b2c расширения приложения:

1. В клиенте Azure AD B2C щелкните **больше услуг** в меню навигации слева hello.
1. Найдите и откройте элемент **Регистрация приложений**.
1. Найдите приложение, имя которого начинается с **b2c-extensions-app**

## <a name="recover-hello-extensions-app"></a>Восстановить приложение hello расширения

Если вы случайно удалены b2c-расширений приложение hello, у вас есть 30 дней toorecover его. Вы сможете восстановить приложения hello, с помощью Graph API hello.

1. Обзор слишком[https://graphexplorer.azurewebsites.net/](https://graphexplorer.azurewebsites.net/).
1. Войдите в toohello сайта как глобальный администратор для каталога Azure AD B2C hello нужного приложения hello удален toorestore для.
1. Выдача HTTP GET к URL-адрес hello `https://graph.windows.net/{tenantName}.onmicrosoft.com/deletedApplications` с api-version = 1.6. Убедитесь, что tooreplace `{tenantName}` на имя вашего клиента. Эта операция отображает список всех приложений hello, которые были удалены в течение hello за последние 30 дней.
1. Найдите приложение hello в списке hello, где hello имя начинается с «b2c расширение приложения» и скопируйте его `objectid` значение свойства.
1. Выдача HTTP POST от hello URL-адрес `https://graph.windows.net/myorganization/deletedApplications/{OBJECTID}/restore`. Замените hello `{OBJECTID}` часть URL-адреса hello с hello `objectid` из предыдущего шага hello. 

Теперь можно будет слишком[разделе приложение hello восстановить](#verifying-that-the-extensions-app-is-present) в hello портал Azure.

> [!NOTE]
> Приложение можно восстановить только в том случае, если он был удален в рамках hello последние 30 дней. Если прошло более 30 дней, данные будут утеряны. Для получения дополнительной помощи отправьте запрос в службу поддержки.
