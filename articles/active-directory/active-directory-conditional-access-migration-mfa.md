---
title: "Миграция классической политику, которая требует многофакторной проверки подлинности на портале Azure | Документы Microsoft"
description: "В этой статье показано, как перенести классический политику, которая требует многофакторной проверки подлинности на портале Azure."
services: active-directory
keywords: "условный доступ к приложениям, условный доступ посредством Azure Active Directory, безопасный доступ к ресурсам организации, политики условного доступа"
documentationcenter: 
author: MarkusVi
manager: mtillman
editor: 
ms.assetid: 8c1d978f-e80b-420e-853a-8bbddc4bcdad
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 12/11/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 77484dc3773736ea15c39ede5f9d49b6b694d960
ms.sourcegitcommit: aaba209b9cea87cb983e6f498e7a820616a77471
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/12/2017
---
# <a name="migrate-a-classic-policy-that-requires-multi-factor-authentication-in-the-azure-portal"></a>Миграция классической политику, которая требует многофакторной проверки подлинности на портале Azure 

В этой статье показано, как перенести классический политику, которая требует **многофакторной проверки подлинности** для облачного приложения. Несмотря на то, что он не является обязательным, рекомендуется ознакомиться с [миграции политик классического портала Azure](active-directory-conditional-access-migration.md) перед началом миграции классический политик.


 
## <a name="overview"></a>Обзор 

Сценарии в этой статье показано, как перенести классический политику, которая требует **многофакторной проверки подлинности** для облачного приложения. 

![Azure Active Directory](./media/active-directory-conditional-access-migration/33.png)


Процесс миграции состоит из следующих шагов:

1. [Откройте классическую политику](#open-a-classic-policy) для получения параметров конфигурации.
2. Создайте политику условного доступа Azure AD, чтобы заменить классическую политику. 
3. Отключите классическую политику.



## <a name="open-a-classic-policy"></a>Открытие классической политики

1. На [портале Azure](https://portal.azure.com) на панели навигации слева щелкните **Azure Active Directory**.

    ![Azure Active Directory](./media/active-directory-conditional-access-migration-mfa/01.png)

2. На странице **Azure Active Directory** в разделе **Управление** щелкните **Условный доступ**.

    ![Условный доступ](./media/active-directory-conditional-access-migration-mfa/02.png)

3. В **управление** щелкните **политики классический (Предварительная версия)**.

    ![Классические политики](./media/active-directory-conditional-access-migration-mfa/12.png)

4. В списке классический политик, щелкните политику, которая требует **многофакторной проверки подлинности** для облачного приложения.

    ![Классические политики](./media/active-directory-conditional-access-migration-mfa/13.png)


## <a name="create-a-new-conditional-access-policy"></a>Создание политики условного доступа


1. На [портале Azure](https://portal.azure.com) на панели навигации слева щелкните **Azure Active Directory**.

    ![Azure Active Directory](./media/active-directory-conditional-access-migration/01.png)

2. На странице **Azure Active Directory** в разделе **Управление** щелкните **Условный доступ**.

    ![Условный доступ](./media/active-directory-conditional-access-migration/02.png)



3. На странице **Условный доступ** на панели инструментов сверху нажмите кнопку **Добавить**, чтобы открыть страницу **Создать**.

    ![Условный доступ](./media/active-directory-conditional-access-migration/03.png)

4. На странице **Создать** в текстовом поле **Имя** введите имя политики.

    ![Условный доступ](./media/active-directory-conditional-access-migration/29.png)

5. В разделе **Назначения** щелкните **Пользователи и группы**.

    ![Условный доступ](./media/active-directory-conditional-access-migration/05.png)

    a. Если вы выбрали всех пользователей в классической политике, щелкните **Все пользователи**. 

    ![Условный доступ](./media/active-directory-conditional-access-migration/35.png)

    Б. Если вы выбрали группы в классической политике, щелкните **Выбрать пользователей и группы**, а затем выберите необходимых пользователей и группы.

    ![Условный доступ](./media/active-directory-conditional-access-migration/36.png)

    c. Если вы исключили какие-либо группы, щелкните вкладку **Исключить** и выберите необходимых пользователей и группы. 

    ![Условный доступ](./media/active-directory-conditional-access-migration/37.png)

6. На странице **Создать** в разделе **Назначения** щелкните **Облачные приложения**, чтобы открыть страницу **Облачные приложения**.

    ![Условный доступ](./media/active-directory-conditional-access-azure-portal-get-started/07.png)

8. На странице **Облачные приложения** выполните следующие действия.

    ![Условный доступ](./media/active-directory-conditional-access-migration/08.png)

    a. Щелкните **Выбрать приложения**.

    Б. Нажмите кнопку **Выбрать**.

    c. На странице **Выбор** выберите облачное приложение и нажмите кнопку **Выбрать**.

    d. На странице **Облачные приложения** нажмите кнопку **Готово**.



9. Если выбран параметр **Требовать многофакторную проверку подлинности**:

    ![Условный доступ](./media/active-directory-conditional-access-migration/26.png)

    a. В разделе **Элементы управления доступом** щелкните **Предоставить**.

    ![Условный доступ](./media/active-directory-conditional-access-migration/27.png)

    Б. На странице **Предоставление** щелкните **Разрешить доступ**, а затем щелкните **Требовать многофакторную проверку подлинности**.

    c. Нажмите кнопку **Выбрать**.


10. Щелкните **Включить**, чтобы включить политику.

    ![Условный доступ](./media/active-directory-conditional-access-migration/30.png)



## <a name="disable-the-classic-policy"></a>Классический политика отключена

Чтобы отключить классические политики, щелкните **отключить** в **сведения** представления.

![Классические политики](./media/active-directory-conditional-access-migration-mfa/14.png)



## <a name="next-steps"></a>Дальнейшие действия

- Дополнительные сведения о миграции классический политик см. в разделе [миграции политик классического портала Azure](active-directory-conditional-access-migration.md).


- Если вы хотите узнать, как настроить политику условного доступа, см. статью о том, как [начать работу с условным доступом в Azure Active Directory](active-directory-conditional-access-azure-portal-get-started.md).

- Если вы готовы к настройке политик условного доступа для своей среды, см. статью [Рекомендации по работе с условным доступом в Azure Active Directory](active-directory-conditional-access-best-practices.md). 
