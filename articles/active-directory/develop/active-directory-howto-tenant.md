---
title: "aaaHow tooget клиент Azure AD | Документы Microsoft"
description: "Как tooget Azure Active Directory клиента для регистрации и создания приложений."
services: active-directory
documentationcenter: 
author: bryanla
manager: mbaldwin
editor: 
ms.assetid: 1f4b24eb-ab4d-4baa-a717-2a0e5b8d27cd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/19/2017
ms.author: bryanla
ms.custom: aaddev
ms.openlocfilehash: dcc6b3109528cf763bda9bd527344ea9ab5c0d69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooget-an-azure-active-directory-tenant"></a>Как клиент tooget Azure Active Directory
В Azure Active Directory (Azure AD) [клиент](https://msdn.microsoft.com/library/azure/jj573650.aspx#BKMK_WhatIsAnAzureADTenant) представляет организацию.  Это отдельный экземпляр службы Azure AD, которое организация получает и становится владельцем при подписке на облачную службу Майкрософт, например Azure, Microsoft Intune или Office 365 hello.  Каждый клиент Azure AD отделен от остальных клиентов Azure AD.  

Клиент размещаются hello пользователи в организации и hello сведениям о них - свои пароли, данные профиля пользователя, разрешения и т. д.  Он также содержит группы, приложения и другие данные, касающиеся tooan организации и систему безопасности.

tooallow toosign пользователей Azure AD в приложении tooyour, необходимо зарегистрировать приложение в клиентом.  Публикация приложения в клиенте Azure AD **абсолютно бесплатна**.  На самом деле, большинство разработчиков создают несколько клиентов и приложений для экспериментов, разработки, промежуточного хранения и тестирования.  Организаций, которые зарегистрироваться в службе и используют приложения при необходимости можно выбрать toopurchase лицензии, по желанию tootake преимущества дополнительных каталогов.

Как вы хотите получить клиент Azure AD?  Hello процесс может быть немного другой Если вы:

* [Наличие существующей подписки Office 365](#use-an-existing-office-365-subscription)
* [Наличие существующей подписки Azure, связанной с учетной записью Майкрософт](#use-an-msa-azure-subscription)
* [Наличие существующей подписки Azure, связанной с учетной записью организации](#use-an-organizational-azure-subscription)
* [Установлен ни один из hello выше & требуется toostart с нуля](#start-from-scratch)

## <a name="use-an-existing-office-365-subscription"></a>Использование существующей подписки Office 365
Если у вас есть подписка Office 365, у вас также есть клиент Azure AD. Вы можете войти в toohello [портал Azure](https://portal.azure.com) с вашей Office 365 учетную запись и приступить к использованию Azure AD.

## <a name="use-an-msa-azure-subscription"></a>Использование подписки Azure, связанной с учетной записью Майкрософт
Если ранее вы уже зарегистрировались для получения подписки Azure с помощью своей учетной записи Майкрософт, у вас уже есть клиент!  При входе в toohello [портала Azure](https://portal.azure.com), вы автоматически войти в tooyour клиента по умолчанию. Являются свободного toouse, этот клиент как можно видеть размеру -, но вы можете toocreate учетной записью администратора организации.

toodo таким образом, выполните следующие действия.  Кроме того может обратиться toocreate новый клиент и создать администратора в клиенте, что следующие аналогичный процесс.

1. Войти в hello [портала Azure](https://portal.azure.com) с учетной записью отдельных
2. Перейдите в раздел «Azure Active Directory» toohello портала hello (найдено в строке приветствия (левая панель), в разделе **более служб**)
3. Вы должны автоматически входить в toohello «Каталог по умолчанию», если не могут переключаться между каталогами, щелкнув имя учетной записи в правом верхнем углу hello.
4. Из hello **быстрого задачи** выберите **Добавление пользователя**.
5. В hello добавить форму пользователя, предоставляют hello, приведенные ниже сведения:

   * имя — выберите соответствующие значения;
   * «Имя пользователя» — выберите имя пользователя для этого администратора;
   * Профиль: (заполните hello соответствующие значения для имени, фамилии, должность и отдел)
   * «Роль» — «Глобальный администратор»;
6. Когда Вы завершили hello добавить форму пользователя и получать hello временный пароль для нового администратора hello, быть toorecord убедиться, что этот пароль, как он потребуется toologin с помощью этого нового пользователя в порядке toochange hello пароль. Вы также можете отправить пароль hello непосредственно toohello пользователя, с помощью альтернативных сообщения электронной почты.
7. Щелкните **создать** toocreate hello нового пользователя.
8. toochange hello временный пароль, войдите [https://login.microsoftonline.com](https://login.microsoftonline.com) с помощью этого нового пользователя учетную запись и измените пароль hello при запросе.

## <a name="use-an-organizational-azure-subscription"></a>Использование подписки организации Azure
Если вы уже ранее выполнили подписку Azure с помощью своей учетной записи организации, у вас уже есть клиент!  В hello [портала Azure](https://portal.azure.com), вы должны найти клиента, при переходе слишком «Более Services» и «Azure Active Directory».  Все бесплатные toouse этого клиента, как можно увидеть помещаются.

## <a name="start-from-scratch"></a>Создание клиента с нуля
Если все hello выше непонятен tooyou, не беспокойтесь.  Просто посетите [https://account.windowsazure.com/organization](https://account.windowsazure.com/organization) toosign для использования Azure с новой организации.  После завершения процесса hello, будет иметь собственный клиент Azure AD с hello доменное имя, выбранное во время входа вверх.  В hello [портала Azure](https://portal.azure.com), вашего клиента можно найти, перейдя по слишком «Azure Active Directory» в левом нижнем nav. hello

В рамках процесса hello подписки на Azure будет tooprovide необходимые сведения кредитной карты.  Не беспокойтесь, плата за публикацию приложений в Azure AD или создание новых клиентов не взимается.
