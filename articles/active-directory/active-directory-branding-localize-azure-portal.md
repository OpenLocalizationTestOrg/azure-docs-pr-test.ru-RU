---
title: "зависящие от языка фирменная tooyour на странице входа в Azure Active Directory hello aaaAdd | Документы Microsoft"
description: "Узнайте, как компании tooadd конкретного языка фирменной символики изображения и текст страницы tooan Azure вход"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: a0310d6a-aaa7-4ea0-991d-6d3135b4382a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: 1e33c31abc242e8455290beb1f03760be7b9ac42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="add-language-specific-company-branding-tooyour-sign-in-page-in-hello-azure-active-directory"></a>Добавление фирменной символики tooyour на странице входа в Azure Active Directory hello компании конкретного языка
tooavoid путаницы, многие компании хотят tooapply согласованного внешнего вида и поведения во всех веб-сайтов hello и службах, которыми они управляют. Azure Active Directory предоставляет эту возможность, позволяя toocustomize hello вида hello-на страницу входа с эмблемой компании и пользовательские цветовые схемы. Hello входа является страница hello, отображается при входе в tooOffice 365 или другие веб-приложения, использующие Azure AD как поставщика удостоверений. Взаимодействие с этой страницы tooenter учетные данные.

## <a name="customizing-hello-sign-in-page-for-another-language"></a>Настройка hello-на страницу входа для другого языка
Элементы языка tooyour пользовательской страницы входа можно добавить только в том случае, если вы уже создали пользовательской страницы входа в систему как описано в [добавить корпоративную фирменную символику страницы входа tooyour](active-directory-branding-custom-signon-azure-portal.md). Можно настроить по одному набору настраиваемых элементов по умолчанию для страницы входа каждого каталога. После настройки по умолчанию hello набор элементов страницы, можно настроить дополнительные версии для разных языков. Вы также можете смешивать разные элементы. Например, можно выполнить следующее.

* Создайте **изображение для страницы входа** по умолчанию, подходящее для всех языков, а затем создайте отдельные версии для английского и русского языков. При установке вашей tooone браузеров из этих двух языков hello конкретного языка изображение, а рисунке hello по умолчанию для всех языков.
* Настройте разные логотипы для организации (например, японскую и китайскую версии).

Рекомендуется сохранять hello количество вариантов языка низкое значение, по соображениям производительности и обслуживания.

**каталог tooadd компании фирменной символики tooyour:**

1. Войдите в toohello [портал Azure](https://portal.azure.com) с помощью учетной записи глобального администратора каталога hello.
2. Выберите **дополнительные службы**, введите **пользователей и групп** в hello текстовое поле, а затем выберите **ввод**.

   ![Открытие страницы "Управление пользователями"](./media/active-directory-branding-localize-azure-portal/user-management.png)
3. На hello **пользователей и групп** колонке выберите **фирменная символика компании**.
4. На hello **пользователей и групп - фирменная символика компании** колонки, выберите hello **добавить язык** команды.

    ![Добавление элементов фирменной символики для определенного языка](./media/active-directory-branding-localize-azure-portal/add-language.png)
5. Изменение элементов hello, требуется toocustomize. Все элементы необязательные.
6. Щелкните **Сохранить**.

Для изменения, внесенные toohello входа страницы фирменной символики tooappear может занять час tooan.

## <a name="next-steps"></a>Дальнейшие действия
[Добавить корпоративную фирменную символику страницы входа tooyour](active-directory-branding-custom-signon-azure-portal.md)
