---
title: "Создание клиента Azure Active Directory B2C | Документация Майкрософт"
description: "Инструкции по созданию клиента Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: mtillman
editor: patricka
ms.assetid: eec4d418-453f-4755-8b30-5ed997841b56
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 06/07/2017
ms.author: parja
ms.openlocfilehash: afca6cf8f19c9b96de292881582e27133e35f096
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2017
---
# <a name="create-an-azure-active-directory-b2c-tenant-in-the-azure-portal"></a>Создание клиента Azure Active Directory B2C на портале Azure

Из этого краткого руководства вы узнаете, как создать клиент Microsoft Azure Active Directory (Azure AD) B2C за несколько минут. По завершении у вас будет клиент B2C (каталог) для регистрации приложений B2C.

## <a name="prerequisites"></a>Технические условия

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="log-in-to-azure"></a>Вход в Azure

Войдите на [портал Azure](https://portal.azure.com/).

## <a name="create-an-azure-ad-b2c-tenant"></a>Создание клиента Azure AD B2C

Возможности B2C невозможно включить в имеющихся клиентах. Нужно создать клиент Azure AD B2C.

[!INCLUDE [active-directory-b2c-create-tenant](../../includes/active-directory-b2c-create-tenant.md)]

Поздравляем! Вы создали клиент Azure Active Directory B2C. Теперь вы — глобальный администратор клиента. При необходимости можно добавить других глобальных администраторов. Чтобы переключиться к новому клиенту, щелкните *ссылку для управления новым клиентом*.

![Ссылка для управления новым клиентом](./media/active-directory-b2c-get-started/manage-new-b2c-tenant-link.png)

> [!IMPORTANT]
> Если вы планируете использовать B2C клиент для рабочего приложения, см. статью, в которой [сравниваются рабочая версия и предварительная версия клиента B2C](active-directory-b2c-reference-tenant-type.md). При удалении существующего клиента B2C и его повторном создании с тем же доменным именем могут возникнуть известные проблемы. Создавайте клиент B2C с другим доменным именем.
>
>

## <a name="link-your-tenant-to-your-subscription"></a>Привязка клиента к подписке

Клиент Azure AD B2C нужно связать с подпиской Azure, чтобы включить все возможности B2C и вносить плату за использование. Дополнительные сведения см. в [этой статье](active-directory-b2c-how-to-enable-billing.md). Если не связать клиент Azure AD B2C с подпиской Azure, некоторые возможности будут заблокированы, а в колонке параметров B2C отобразится предупреждение No Subscription linked to this B2C tenant or the Subscription needs your attention (С этим клиентом B2C не связана ни одна подписка, или подписка требует вашего внимания). Важно выполнить этот шаг, прежде чем переводить приложения в рабочую среду.

## <a name="easy-access-to-settings"></a>Простой доступ к параметрам

[!INCLUDE [active-directory-b2c-find-service-settings](../../includes/active-directory-b2c-find-service-settings.md)]

Чтобы получить доступ к колонке, можно также ввести `Azure AD B2C` в поле **Поиск ресурсов** в верхней части портала. В списке результатов выберите **Azure AD B2C** для доступа к колонке параметров B2C.

## <a name="next-steps"></a>Дальнейшие действия

> [!div class="nextstepaction"]
> [Azure Active Directory B2C: регистрация приложения](active-directory-b2c-app-registration.md)