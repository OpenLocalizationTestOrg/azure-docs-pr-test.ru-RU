---
title: "aaaGet работы с условным доступом в Azure Active Directory | Документы Microsoft"
description: "Тестирование условного доступа с помощью условия расположения."
services: active-directory
keywords: "tooapps условного доступа, условного доступа с Azure AD, защита доступа к ресурсам toocompany, политики условного доступа"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/31/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: 4521f5a34f5882e026f5e58a7127d8c55cba2f0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-conditional-access-in-azure-active-directory"></a>Начало работы с условным доступом в Azure Active Directory

Условный доступ — это компонент Azure Active Directory, который позволяет вам toodefine условия при которых несанкционированный доступ приложений. 

Эта статья содержит инструкции для тестирования условного доступа на основе условия расположения в среде.  


## <a name="scenario-description"></a>Описание сценария

Одно общее требование во многих организациях — tooonly требовать многофакторную проверку подлинности для доступа tooapps, выполняется не из hello корпоративной интрасети. Вы легко можете реализовать это с помощью Azure Active Directory, настроив политику условного доступа на основе расположения. В этой статье вы найдете подробные инструкции по настройке соответствующей политики. Здравствуйте, использует политику [надежных IP-адресов](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips) toodistinguish между попытками доступа из корпоративной hello в интрасети и все остальные.


## <a name="prerequisites"></a>Предварительные требования

Hello сценарии, описанные в этом разделе предполагается, что вы знакомы с основными понятиями hello, описанные в [условного доступа Azure Active Directory](active-directory-conditional-access-azure-portal.md).

tootest этот сценарий, необходимо:

- Создать тестового пользователя. 

- Назначить Azure AD Premium лицензирования toohello тестового пользователя

- Настройка управляемого приложения и назначение вашей tooit тестового пользователя

- Настроить надежные IP-адреса.

Дополнительные сведения о надежных IP-адресах см. в разделе [Надежные IP-адреса](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).


## <a name="policy-configuration-steps"></a>Настройка политики

**tooconfigure политику условного доступа, выполните:**

1. В hello портал Azure, на левой переходов hello, щелкните **Azure Active Directory**. 

    ![Условный доступ](./media/active-directory-conditional-access-azure-portal-get-started/01.png)

2. На hello **Azure Active Directory** колонки в hello **управление** щелкните **условного доступа**.

    ![Условный доступ](./media/active-directory-conditional-access-azure-portal-get-started/02.png)
 
3. На hello **условного доступа** колонки, tooopen hello **New** колонки в верхней части экрана приветствия hello инструментов щелкните **добавить**.

    ![Условный доступ](./media/active-directory-conditional-access-azure-portal-get-started/03.png)

4. На hello **New** колонки в hello **имя** текстовом поле введите имя для политики.

    ![Условный доступ](./media/active-directory-conditional-access-azure-portal-get-started/04.png)

5. В hello **назначения** щелкните **пользователей и групп**.

    ![Условный доступ](./media/active-directory-conditional-access-azure-portal-get-started/05.png)

6. На hello **пользователей и групп** колонки, выполните следующие шаги hello:

    ![Условный доступ](./media/active-directory-conditional-access-azure-portal-get-started/06.png)

    а. Щелкните **Выбрать пользователей и группы**.

    b. Нажмите кнопку **Выбрать**.

    c. На hello **выберите** колонке выберите тестового пользователя и нажмите кнопку **выберите**.

    d. На hello **пользователей и групп** колонка, щелкните **сделать**.

7. На hello **New** колонки, tooopen hello **облачные приложения** колонки в hello **назначения** щелкните **облачные приложения**.

    ![Условный доступ](./media/active-directory-conditional-access-azure-portal-get-started/07.png)

8. На hello **облачные приложения** колонки, выполните следующие шаги hello:

    ![Условный доступ](./media/active-directory-conditional-access-azure-portal-get-started/08.png)

    а. Щелкните **Выбрать приложения**.

    b. Нажмите кнопку **Выбрать**.

    c. На hello **выберите** колонке выберите облачные приложения и нажмите кнопку **выберите**.

    d. На hello **облачные приложения** колонка, щелкните **сделать**.

9. На hello **New** колонки, tooopen hello **условия** колонки в hello **назначения** щелкните **условия**.

    ![Условный доступ](./media/active-directory-conditional-access-azure-portal-get-started/09.png)

10. На hello **условия** колонки, tooopen hello **расположения** колонка, щелкните **расположения**.

    ![Условный доступ](./media/active-directory-conditional-access-azure-portal-get-started/10.png)

11. На hello **расположения** колонки, выполните следующие шаги hello:

    ![Условный доступ](./media/active-directory-conditional-access-azure-portal-get-started/11.png)

    а. Под параметром **Настройка** нажмите кнопку **Да**.

    b. На вкладке **Включить** выберите **Все расположения**.

    c. Откройте вкладку **Исключить** и выберите **All trusted IPs** (Все надежные IP-адреса).

    ![Условный доступ](./media/active-directory-conditional-access-azure-portal-get-started/12.png)

    d. Нажмите кнопку **Done**(Готово).

12. На hello **условия** колонка, щелкните **сделать**.

13. На hello **New** колонки, tooopen hello **Grant** колонки в hello **элементов управления** щелкните **Grant**.

    ![Условный доступ](./media/active-directory-conditional-access-azure-portal-get-started/13.png)

14. На hello **Grant** колонки, выполните следующие шаги hello:

    ![Условный доступ](./media/active-directory-conditional-access-azure-portal-get-started/14.png)

    а. Выберите **Требовать многофакторную проверку подлинности**.

    b. Нажмите кнопку **Выбрать**.

15. На hello **New** колонки в разделе **включить политику**, нажмите кнопку **на**.

    ![Условный доступ](./media/active-directory-conditional-access-azure-portal-get-started/15.png)

16. На hello **New** колонка, щелкните **создать**.


## <a name="testing-hello-policy"></a>Политика тестирования hello

tootest политики следует доступ к вашему приложению с устройств: 

1. IP-адрес устройства входит в диапазон настроенных надежных IP-адресов. 

1. IP-адрес устройства не входит в диапазон настроенных надежных IP-адресов.

Многофакторная идентификация должна требоваться только во время попытки подключения с устройства, IP-адрес которого не входит в диапазон настроенных надежных IP-адресов. 


## <a name="next-steps"></a>Дальнейшие действия

При желании toolearn Дополнительные сведения о условного доступа в разделе [условного доступа Azure Active Directory](active-directory-conditional-access-azure-portal.md).

