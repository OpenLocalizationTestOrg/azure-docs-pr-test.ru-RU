---
title: "каталог hello aaaManage для подписки Office 365 в Azure | Документы Microsoft"
description: "Управление каталогом подписки Office 365 с помощью Azure Active Directory и hello классический портал Azure"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 746987b7-2dfd-4b35-819d-37c1b65c5c81
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/25/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
ms.openlocfilehash: 4faf9936d7e94b85356a18adfcf3d2a48e5b025f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hello-directory-for-your-office-365-subscription-in-azure"></a>Управление каталогом hello для подписки Office 365 в Azure
В этой статье описывается как toomanage каталогом, созданным для подписки на Office 365 с помощью hello классический портал Azure. Должен быть hello администратора службы или соадминистратором подписки Azure toosign в toohello классический портал Azure. Если у вас нет подписки Azure, вы можете зарегистрироваться прямо сейчас, чтобы использовать [бесплатную пробную версию в течение 30 дней](https://azure.microsoft.com/trial/get-started-active-directory/) и развернуть первое облачное решение в течение 5 минут, применив эту ссылку. Убедиться, что toouse hello работы или рабочую учетную запись, используемая toosign в tooOffice 365.

> [!IMPORTANT]
> Корпорация Майкрософт рекомендует управлять Azure AD, используя hello [Центр администрирования Azure AD](https://aad.portal.azure.com) в hello портал Azure, вместо использования hello классический портал Azure, в этой статье.

После завершения hello подписки Azure, можно войти в toohello классический портал Azure и доступа к службам Azure. Щелкните расширение Active Directory hello toomanage hello же каталог, выполняющий проверку подлинности пользователей Office 365.

Если уже имеется подписка Azure, toomanage процесс hello дополнительным каталогом также нетрудно. Например, у пользователя Michael Smith может быть подписка Office 365 для Contoso.com. У него также есть подписка Azure, оформленная с помощью учетной записи Майкрософт (msmith@hotmail.com). В этом случае он управляет двумя каталогами.

| Подписки | Office 365 | Таблицы Azure |
| --- | --- | --- |
|   Отображаемое имя |Contoso |Каталог по умолчанию Azure Active Directory (Azure AD) |
|   Доменное имя |contoso.com |msmithhotmail.onmicrosoft.com |

Ему удостоверения пользователей toomanage hello в каталоге Contoso hello, выполнив вход в tooAzure под своей учетной записью Майкрософт, чтобы он может включить функции Azure AD, такие как многофакторная проверка подлинности. Следующая схема Hello может помочь tooillustrate hello процесса.

![Схема двух независимых каталогов toomanage](./media/active-directory-manage-o365-subscription/AAD_O365_03.png)

В этом случае два каталога hello независимо друг от друга.

## <a name="toomanage-two-independent-directories"></a>toomanage двух независимых каталоги
В порядок toomanage Майкл Смит обоих каталоги войдя в tooAzure как msmith@hotmail.com, ему необходимо выполнить следующие шаги hello:

> [!NOTE]
> Эти действия можно выполнить только в том случае, если пользователь вошел систему с помощью учетной записи Майкрософт. Если hello пользователь выполняет вход с рабочей или учебной учетной записи, hello параметр слишком**использовать существующий каталог** недоступна. Рабочей или учебной учетной записи может пройти проверку подлинности только ее исходным каталогом (то есть hello каталог hello рабочей учетной записи хранения, куда, hello компании или учебного заведения, которому принадлежит).
>
>

1. Войдите в toohello [классический портал Azure](https://manage.windowsazure.com) как msmith@hotmail.com.
2. Щелкните **Создать** > **Службы приложений** > **Active Directory** > **Каталог** > **Настраиваемое создание**.
3. Выберите параметр использовать существующий каталог и выберите hello **я готов toobe выходу из системы** флажок.
4. Войдите в toohello классический портал Azure как глобальный администратор Contoso.onmicrosoft.com (например, msmith@contoso.com).
5. При появлении запроса слишком**использовать каталог Contoso hello с Azure?**, нажмите кнопку **Продолжить**.
6. Щелкните **Выйти сейчас**.
7. Войдите в toohello классический портал Azure как msmith@hotmail.com. hello каталог Contoso и каталог по умолчанию hello появляются в hello расширение Active Directory.

После выполнения этих действий msmith@hotmail.com является глобальным администратором в каталоге Contoso hello.

## <a name="tooadminister-resources-as-hello-global-admin"></a>ресурсы tooadminister как hello глобального администратора
Теперь давайте предположим, что требуется Jane Doe Администрирование веб-сайтов и ресурсы баз данных, которые связаны с hello подписки Azure для msmith@hotmail.com. Прежде чем она может сделать это, Майкл Смит должен toocomplete следующие дополнительные действия:

1. Войдите в toohello [классический портал Azure](https://manage.windowsazure.com) с использованием учетной записи администратора службы hello hello подписки Azure (в данном примере msmith@hotmail.com).
2. Передача каталог Contoso toohello подписки hello: щелкните **параметры** > **подписки** > выберите подписку hello > **изменить каталог** > выберите **Contoso (Contoso.com)**. Учетные записи соадминистраторов подписки hello удаляются в процессе передачи hello любой рабочего или учебного заведения.
3. Добавить в качестве соадминистратора подписки hello Jane Doe: щелкните **параметры** > **Администраторы** > выберите подписку hello > **добавить** > тип **JohnDoe@Contoso.com**.

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения об отношениях hello, подписками и каталогами см. в разделе [как подписка связывается с каталогом](active-directory-how-subscriptions-associated-directory.md).
