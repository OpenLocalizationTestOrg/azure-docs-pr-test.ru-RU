---
title: "Администраторы серверов aaaManage в Azure Analysis Services | Документы Microsoft"
description: "Узнайте, как администраторы серверов toomanage для сервера служб Analysis Services в Azure."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: e04387e48e9b9483c382ee5cc9fd65f8331fb2a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-server-administrators"></a>Управление администраторами серверов
Администраторы сервера необходимо быть допустимого пользователя или группы в Azure Active Directory (Azure AD) hello hello клиента, в которой hello находится сервер. Можно использовать **Analysis Services Администраторы** в колонке управления hello для сервера на портале Azure или свойств сервера в SSMS toomanage администраторам. 

## <a name="tooadd-server-administrators-by-using-azure-portal"></a>Администраторы сервера tooadd с помощью портала Azure
1. В колонке управления hello для сервера, щелкните **Analysis Services Администраторы**.
2. В hello  **\<имя_сервера >-Администраторы служб Analysis** колонка, щелкните **добавить**.
3. В hello **добавления администраторов сервера** колонке выберите учетные записи пользователей из Azure AD или Пригласите внешних пользователей, адреса электронной почты.

    ![Администраторы сервера на портале Azure](./media/analysis-services-server-admins/aas-manage-users-admins.png)

## <a name="tooadd-server-administrators-by-using-ssms"></a>Администраторы сервера tooadd с помощью среды SSMS
1. Щелкните правой кнопкой мыши сервер hello > **свойства**.
2. В разделе **Свойства сервера анализа данных** выберите **Безопасность**.
3. Нажмите кнопку **добавить**, а затем введите адрес электронной почты hello для пользователя или группы в Azure AD.
   
    ![Добавление администраторов сервера в SSMS](./media/analysis-services-server-admins/aas-manage-users-ssms.png)

## <a name="next-steps"></a>Дальнейшие действия 
[Аутентификация и пользовательские разрешения](analysis-services-manage-users.md)  
[Управление ролями и пользователями базы данных](analysis-services-database-users.md)  
[Контроль доступа на основе ролей](../active-directory/role-based-access-control-what-is.md)  

