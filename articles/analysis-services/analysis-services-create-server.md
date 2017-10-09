---
title: "aaaCreate серверу служб Analysis Services в Azure | Документы Microsoft"
description: "Узнайте, как экземпляр toocreate серверу служб Analysis Services в Azure."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 7f560216-8a9a-4d06-852e-48cf24deab19
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: 3668f659039f79f3dd71498d1066e8682bf33228
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-analysis-services-server-in-azure-portal"></a>Создание сервера Azure Analysis Services на портале Azure
В этой статье приведено пошаговое руководство по созданию ресурса сервера служб Analysis Services в подписке Azure.

## <a name="before-you-begin"></a>Перед началом работы
toocomplete краткого руководства, необходимо:

* **Подписка Azure**: посетите [бесплатная пробная версия](https://azure.microsoft.com/offers/ms-azr-0044p/) toocreate учетную запись.
* **Azure Active Directory**: ваша подписка должна быть связана с клиентом Azure Active Directory. И требуется toobe вход tooAzure с учетной записью в Azure Active Directory. Учетные записи Майкрософт не поддерживаются. toolearn более, в разделе [проверки подлинности и пользовательские разрешения](analysis-services-manage-users.md).
* **Группа ресурсов**: используйте уже имеющуюся группу ресурсов или [создайте новую](../azure-resource-manager/resource-group-overview.md).

> [!NOTE]
> При создании сервера вам могут выставляться счета за новую службу. toolearn более, в разделе [цены служб Analysis Services](https://azure.microsoft.com/pricing/details/analysis-services/).
> 
> 

## <a name="toocreate-a-server-in-azure-portal"></a>toocreate сервера на портале Azure
1. Войдите в toohello [портал Azure](https://portal.azure.com).  
2. Щелкните **+ Создать** > **Данные и аналитика** > **Службы Analysis Services**.
3. В hello **служб Analysis Services** колонки, заполните поля требуется hello и нажмите клавишу **создать**.
   
    ![Создание сервера](./media/analysis-services-create-server/aas-create-server-blade.png)
   
   * **Имя сервера**: Введите уникальное имя, используемое tooreference hello сервер.
   * **Подписки**: выберите подписку hello выставляет счет этого сервера для.
   * **Группа ресурсов**: эти контейнеры являются спроектированный toohelp управлять коллекцией ресурсов Azure. toolearn более, в разделе [групп ресурсов](../azure-resource-manager/resource-group-overview.md).
   * **Расположение**: узлы расположение центра обработки данных Azure этот hello server. Выберите расположение, ближайшее к крупнейшей имеющейся базе пользователей.
   * **Ценовая категория**: выберите ценовую категорию. Поддерживаются табличные модели too400 Гбайт. toolearn более, в разделе [ценообразования Azure Analysis Services](https://azure.microsoft.com/pricing/details/analysis-services/).
4. Щелкните **Создать**.

Создание обычно занимает меньше минуты, чаще всего несколько секунд. Если вы выбрали **добавить tooPortal**, перейти на новый сервер портала toosee tooyour. Или перейдите слишком**дополнительные службы** > **служб Analysis Services** toosee, если сервер готов.

 ![Панель мониторинга](./media/analysis-services-create-server/aas-create-server-dashboard.png)


## <a name="next-steps"></a>Дальнейшие действия
После создания сервера, вы можете [развернуть модель](analysis-services-deploy.md) tooit посредством SSDT или с помощью среды SSMS.

При развертывании сервера tooyour модель подключается tooon локальные источники данных, необходимо tooinstall [локального шлюза данных](analysis-services-gateway.md) на компьютере в сети.

