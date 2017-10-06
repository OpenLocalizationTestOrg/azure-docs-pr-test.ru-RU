---
title: "Azure Active Directory B2C: создание клиента Azure Active Directory B2C | Документация Майкрософт"
description: "Как для клиента Azure Active Directory B2C toocreate на раздел"
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: patricka
ms.assetid: eec4d418-453f-4755-8b30-5ed997841b56
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 06/07/2017
ms.author: swkrish
ms.openlocfilehash: e8b257d66c1f66ffb84f5d3d21b30b42eddcbac9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-active-directory-b2c-tenant-in-hello-azure-portal"></a>Создание клиента Azure Active Directory B2C в hello портал Azure

Редактировать Sipi.

Из этого краткого руководства вы узнаете, как создать клиент Microsoft Azure Active Directory (Azure AD) B2C за несколько минут. Когда закончите, у вас toouse клиента B2C для регистрации приложений B2C.

## <a name="prerequisites"></a>Предварительные требования

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

##  <a name="log-in-tooazure"></a>Войдите в tooAzure

Войдите в toohello [портал Azure](https://portal.azure.com/).

## <a name="create-an-azure-ad-b2c-tenant"></a>Создание клиента Azure AD B2C

Возможности B2C невозможно включить в имеющихся клиентах. Необходимо toocreate клиент Azure AD B2C.

[!INCLUDE [active-directory-b2c-create-tenant](../../includes/active-directory-b2c-create-tenant.md)]

Поздравляем! Вы создали клиент Azure Active Directory B2C. Вы являетесь глобальным администратором клиента hello. При необходимости можно добавить других глобальных администраторов. tooswitch tooyour нового клиента, щелкните hello *управлять вашей новой связи клиента*.

![Ссылка для управления новым клиентом](./media/active-directory-b2c-get-started/manage-new-b2c-tenant-link.png)

> [!IMPORTANT]
> Если вы планируете toouse клиента B2C для рабочего приложения, прочтите статью hello на [Масштабирование рабочей и предварительной версии B2C клиентов](active-directory-b2c-reference-tenant-type.md). Существуют известные проблемы при удалении существующей B2C клиента и создать его повторно с hello таким же именем домена. Необходимо toocreate клиента B2C с именем другого домена.
>
>

## <a name="link-your-tenant-tooyour-subscription"></a>Связи подписки tooyour клиента

Требуется toolink к Azure AD B2C клиента все функциональные возможности B2C tooenable tooyour подписки Azure и платить за сборам за использование. лучше, ознакомьтесь с toolearn [в этой статье](active-directory-b2c-how-to-enable-billing.md). Если не связать ваш tooyour клиента Azure AD B2C подписки Azure, заблокированы некоторые функциональные возможности, и вы увидите предупреждение («подписка, не связанный toothis B2C клиента или hello подписки должен внимания.») в параметрах hello B2C. Важно выполнить этот шаг, прежде чем переводить приложения в рабочую среду.

## <a name="easy-access-toosettings"></a>Простой доступ toosettings

[!INCLUDE [active-directory-b2c-find-service-settings](../../includes/active-directory-b2c-find-service-settings.md)]

Можно также доступ к колонке hello, введя `Azure AD B2C` в **Найдите ресурсы** hello верхней части портала hello. В списке результатов hello выберите **Azure AD B2C** tooaccess hello колонку параметров B2C.

## <a name="next-steps"></a>Дальнейшие действия

> [!div class="nextstepaction"]
> [Azure Active Directory B2C: регистрация приложения](active-directory-b2c-app-registration.md)
