---
title: "aaaCreate частного реестра Docker - портал Azure | Документы Microsoft"
description: "Начать создание и управление ими частных реестрах контейнера Docker с hello портал Azure"
services: container-registry
documentationcenter: 
author: stevelas
manager: balans
editor: dlepow
tags: 
keywords: 
ms.assetid: 53a3b3cb-ab4b-4560-bc00-366e2759f1a1
ms.service: container-registry
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2017
ms.author: stevelas
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 40f3ce44fea26e5fbeca865c9da6df55c2df9511
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-private-docker-container-registry-using-hello-azure-portal"></a>Создание частного реестра контейнера Docker, с помощью портала Azure hello
Использование hello Azure портала toocreate реестре контейнеров и управления его параметры. Можно также создать и управлять контейнера реестры с помощью hello [команды Azure CLI 2.0](container-registry-get-started-azure-cli.md), [Azure PowerShell](container-registry-get-started-powershell.md) или программным путем с контейнер реестра hello [API-интерфейса REST](https://go.microsoft.com/fwlink/p/?linkid=834376).

Сведения и основные понятия, в разделе [hello Обзор](container-registry-intro.md).

## <a name="create-a-container-registry"></a>Создание реестра контейнеров
1. В hello [портал Azure](https://portal.azure.com), нажмите кнопку **+ создать**.
2. Поиск hello marketplace для **контейнер Azure реестра**.
3. Выберите **реестр контейнеров Azure** (издатель — корпорация **Майкрософт**).
    ![Служба реестра контейнеров в Azure Marketplace](./media/container-registry-get-started-portal/container-registry-marketplace.png)
4. Щелкните **Создать**. Hello **реестра контейнера Azure** колонке отображается.

    ![Параметры реестра контейнеров](./media/container-registry-get-started-portal/container-registry-settings.png)
5. В hello **реестра контейнера Azure** колонки, введите следующую информацию hello. Закончив, нажмите кнопку **Создать**.

    а. **Имя реестра** — глобальное уникальное доменное имя верхнего уровня для определенного реестра. В этом примере — имя реестра hello *myRegistry01*, но заменить собственным уникальное имя. Hello имя может содержать только буквы и цифры.

    b. **Группа ресурсов**: выберите существующую [группы ресурсов](../azure-resource-manager/resource-group-overview.md#resource-groups) или имя типа hello новую.

    c. **Расположение**: Выбор расположения центра обработки данных Azure, где hello службы [доступных](https://azure.microsoft.com/regions/services/), такие как **центральных штатах юга США**.

    d. **Пользователю с правами администратора**: следует включить в реестре hello tooaccess пользователя администратора. Можно изменить этот параметр после создания hello реестра.

      > [!IMPORTANT]
      > В дополнение к этому tooproviding доступ через учетную запись пользователя admin, контейнера реестры поддержки проверки подлинности, поддерживаемый субъекты-службы Azure Active Directory. Дополнительные сведения и рекомендации см. в статье [Authenticate with the container registry](container-registry-authentication.md) (Проверка подлинности с помощью реестра контейнеров).
      >

    д. **Учетная запись хранения**: используйте toocreate параметр по умолчанию hello [учетной записи хранилища](../storage/common/storage-introduction.md), или выберите существующую учетную запись хранения в hello местоположения. Хранилище класса Premium сейчас не поддерживается.

## <a name="manage-registry-settings"></a>Управление параметрами реестра
После создания реестра hello, найти hello параметры реестра, начиная с hello **контейнера реестры** колонке hello портала. Например может потребоваться hello toolog параметры в реестре tooyour или может требуется tooenable или отключает hello пользователя с правами администратора.

1. На hello **контейнера реестры** колонка, щелкните имя hello реестра.

    ![Колонка "Container Registry (предварительная версия)"](./media/container-registry-get-started-portal/container-registry-blade.png)
2. параметры доступа к toomanage, нажмите кнопку **ключ доступа**.

    ![Доступ к реестру контейнеров](./media/container-registry-get-started-portal/container-registry-access.png)
3. Обратите внимание, hello следующие параметры:

   * **Сервер входа в систему** -использовать toolog в реестре toohello полное имя hello. В нашем примере поисковый запрос будет выглядеть так: `myregistry01.azurecr.io`.
   * **Пользователю с правами администратора** - переключение tooenable или отключение учетной записи пользователя admin hello реестра.
   * **Имя пользователя** и **пароль** -hello учетные данные учетной записи пользователя admin hello (если он включен) можно использовать в реестре toohello toolog. При необходимости можно создать повторно hello пароли. Двух паролей создаются, чтобы сохранить подключения toohello реестра, используя один пароль, при повторном создании hello другим паролем. tooauthenticate с субъектом-службой. Вместо этого в разделе [аутентификация с помощью частного реестра контейнера Docker](container-registry-authentication.md).

## <a name="next-steps"></a>Дальнейшие действия
* [Принудительная первый образ с помощью hello Docker CLI](container-registry-get-started-docker-cli.md)
