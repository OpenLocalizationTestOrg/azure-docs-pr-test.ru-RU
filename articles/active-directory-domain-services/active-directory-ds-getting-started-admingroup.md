---
title: "Доменные службы Azure Active Directory: начало работы | Документы Майкрософт"
description: "Включение Azure доменных служб Active Directory с помощью hello портал Azure (Предварительная версия)"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: ace1ed4a-bf7f-43c1-a64a-6b51a2202473
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/15/2017
ms.author: maheshu
ms.openlocfilehash: 8bde872a13bc9960d1e62c74017ff78a8953a0a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-using-hello-azure-portal-preview"></a>Включение Azure доменных служб Active Directory с помощью hello портал Azure (Предварительная версия)


## <a name="task-3-configure-administrative-group"></a>Задача 3. Настройка административной группы
В рамках этой задачи конфигурации вы создадите административную группу в каталоге Azure AD. Эта специальная административная группа называется *Администраторы контроллера домена AAD*. Члены этой группы предоставляются права администратора на компьютерах, присоединенных к домену toohello управляемый домен. На компьютерах, присоединенных к домену эта группа добавляется toohello группы «Администраторы». Кроме того члены этой группы можно использовать машины удаленно присоединенных toodomain tooconnect удаленного рабочего стола.

> [!NOTE]
> Нет разрешений администратора домена или администратора предприятия на hello управляемый домен, созданный с помощью доменных служб Active Directory Azure. На управляемые домены эти разрешения защищены службой hello и не становятся доступны toousers в рамках клиента hello. Тем не менее, можно использовать hello специальных административных Создание группы в этой конфигурации задачи tooperform некоторые привилегированные операции. Эти операции включают toohello компьютеров к домену, принадлежащий группы администрирования toohello на присоединенных к домену компьютерах и Настройка групповой политики.
>

Hello мастер автоматически создаст hello административную группу в каталоге Azure AD. Эта группа называется "Администраторы AAD DC". При наличии существующей группы с таким именем в каталоге Azure AD hello мастер выбирает эту группу. Можно настроить с помощью hello членство в группе **группу администраторов** страницу мастера.

1. членство в группе tooconfigure, нажмите кнопку **Администраторы контроллера домена AAD**.

    ![Настройка членства в группе](./media/getting-started/domain-services-blade-admingroup.png)

2. Нажмите кнопку hello **добавление членов** кнопку tooadd пользователей из вашей группы администраторов toohello каталог Azure AD.

3. Закончив, нажмите кнопку **ОК** toomove на toohello **Сводка** на странице приветствия мастера.

4. На hello **Сводка** приветствия мастера просмотрите параметры конфигурации hello hello управляемый домен. Можно вернуться к нему tooany шаге мастера toomake hello изменяется, если это необходимо. Закончив, нажмите кнопку **ОК** toocreate hello создать управляемого домена.

    ![Сводка](./media/getting-started/domain-services-blade-summary.png)

5. Вы увидите уведомление, которое отображает hello ход выполнения развертывания доменные службы Azure AD. Щелкните уведомление hello toosee подробные ход выполнения развертывания hello.

    ![Уведомление — выполняется развертывание](./media/getting-started/domain-services-blade-deployment-in-progress.png)


## <a name="provision-your-managed-domain"></a>Подготовка управляемого домена
Hello процесс подготовки управляемого домена может занять час tooan.

1. Во время развертывания можно выполнить поиск «доменных служб» hello **Найдите ресурсы** поле поиска. Выберите **доменные службы Azure AD** из результатов поиска hello. Hello **доменные службы Azure AD** колонке перечислены hello управляемый домен, который подготавливается в настоящий момент.

    ![Поиск подготавливаемого управляемого домена](./media/getting-started/domain-services-provisioning-state-find-resource.png)

2. Щелкните имя hello toosee hello управляемого домена (например, «contoso100.com») Дополнительные сведения о домене hello.

    ![Доменные службы — состояние подготовки](./media/getting-started/domain-services-provisioning-state.png)

3. Hello **Обзор** вкладке отображается в настоящее время идет подготовка домена hello. Не удается настроить hello управляемого домена до полной инициализации. Это может потребоваться до часа tooan вашей toobe управляемый домен полностью подготовлены.

    ![Доменные службы - вкладка обзора во время hello состояние подготовки ](./media/getting-started/domain-services-provisioning-state-details.png)

4. Здравствуйте, когда управляемый домен hello полностью подготовлены, **Обзор** вкладке отображается состояние домена hello как **под управлением**.

    ![Доменные службы — вкладка "Обзор" после полной подготовки](./media/getting-started/domain-services-provisioned.png)

5. На hello **свойства** вкладке появится два IP-адреса, в какой домен контроллеров доступны для hello виртуальной сети.

    ![Доменные службы — вкладка "Свойства" после полной подготовки](./media/getting-started/domain-services-provisioned-properties.png)


## <a name="next-step"></a>Дальнейшие действия
[Задача 4: обновите параметры DNS hello для hello виртуальной сети Azure](active-directory-ds-getting-started-dns.md)
