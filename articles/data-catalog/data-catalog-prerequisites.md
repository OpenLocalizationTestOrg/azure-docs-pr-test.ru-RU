---
title: "Необходимые условия для каталога данных aaaAzure | Документы Microsoft"
description: "Дополнительные сведения о предварительных требованиях hello, необходимые tooget работы с помощью каталога данных Azure."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: ef497a54-dc4d-4820-b5bf-c361b64b964d
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 0c8e768e5846c61b542b746d7ad80121725a9ec7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-catalog-prerequisites"></a>Предварительные условия для работы с каталогом данных Azure

Перед настройкой каталога данных Azure необходимо tootake заботиться о несколько вещей. Не беспокойтесь, этот процесс не займет много времени.

## <a name="azure-subscription"></a>Подписка Azure.
tooset копирование каталога данных, необходимо быть hello владелец или совладелец подписки Azure.

Azure подписки позволяют упорядочивать доступ службы toocloud ресурсы, такие как каталог данных. Они также позволяют управлять составлением отчетов об использовании ресурса, выставлением счетов за использование и их оплатой. Каждая подписка может иметь отдельные настройки для выставления счетов и их оплаты, поэтому у вас могут быть разные подписки и тарифные планы для разных отделов, проектов, региональных офисов и т. д. Каждая облачная служба привязана tooa подписки и необходимость toohave подписки перед настройкой каталога данных. toolearn более, в разделе [управление учетными записями, подписками и административные роли](../active-directory/active-directory-assign-admin-roles.md).

## <a name="azure-active-directory"></a>Azure Active Directory
tooset копирование каталога данных, необходимо войти с учетной записью пользователя Azure Active Directory (Azure AD).

Azure AD предоставляет простой способ для вашего бизнеса toomanage удостоверениями и доступом в облаке hello и локальных. Пользователи могут использовать одну рабочую или учебную учетную запись для одной tooany облака и локальных веб-приложения. Каталог данных использует Azure AD tooauthenticate вход. toolearn более, в разделе [что такое Azure Active Directory?](../active-directory/active-directory-whatis.md).

> [!NOTE]
> С помощью hello [портал Azure](http://portal.azure.com/), вы можете войти с использованием личную учетную запись Майкрософт или Azure Active Directory рабочая или учебная учетная запись. либо hello tooset копию данных каталога с помощью портала Azure или hello [портала каталога данных](http://www.azuredatacatalog.com), необходимо войти в систему с учетной записью Azure Active Directory не личную учетную запись.
>
>

## <a name="active-directory-policy-configuration"></a>Настройка политики Active Directory
Может возникнуть ситуация, где вы сможете войти в портал toohello каталога данных, но при попытке toosign в средство регистрации источника данных toohello, возникает сообщение об ошибке, которая запрещает вход. Это проблема может произойти только в том случае, если вы в сети компании hello или возможны только при подключении из hello вне корпоративной сети.

Средство регистрации источника данных Hello использует toovalidate форм проверки подлинности учетных данных пользователя в Active Directory. toohelp при входе в успешно, администратор Active Directory необходимо включить проверку подлинности форм в hello глобальной политики проверки подлинности.

Hello глобальной политики проверки подлинности методы проверки подлинности может быть отдельно для интрасети и экстрасети подключения, как показано на следующий снимок экрана приветствия. Если не включена проверка подлинности форм для hello сети, из которого вы подключаетесь, могут возникать ошибки входа.

 ![Глобальная политика аутентификации AD FS](./media/data-catalog-prerequisites/global-auth-policy.png)

## <a name="next-steps"></a>Дальнейшие действия
Подробнее: [Настройка политик проверки подлинности](https://technet.microsoft.com/library/dn486781.aspx).
