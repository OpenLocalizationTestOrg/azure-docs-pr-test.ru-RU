---
title: "Управление разрешениями к ресурсам на пользователя в Azure стека (администратор службы и клиента) | Документы Microsoft"
description: "Администратор службы или клиента Узнайте, как для управления разрешениями RBAC."
services: azure-stack
documentationcenter: 
author: Heathl17
manager: byronr
editor: 
ms.assetid: cccac19a-e1bf-4e36-8ac8-2228e8487646
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: helaw
ms.openlocfilehash: 95bdc83351acdec352620feaea3b1e50c0dabad4
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="manage-role-based-access-control"></a>Управление доступом на основе ролей
Пользователь в Azure Stack может быть читателем, владельцем или участником каждого экземпляра подписки, группы ресурсов или службы. Например, пользователь A может иметь разрешения на чтение подписки 1, но иметь права владельца виртуальной машины 7.

* Читатель: пользователь может все просматривать, но не может вносить изменения.
* Участник: пользователь может управлять всем, кроме доступа к ресурсам.
* Владелец: пользователь может управлять всем, включая доступ к ресурсам.

## <a name="set-access-permissions-for-a-user"></a>Настройка прав доступа для пользователя
1. Выполните вход с помощью с учетной записью с разрешениями владельца ресурса, которым вы хотите управлять.
2. В колонке для ресурса, нажмите кнопку **доступа** значок ![](media/azure-stack-manage-permissions/image1.png).
3. В **пользователей** колонка, щелкните **ролей**.
4. В **ролей** колонка, щелкните **добавить** для добавления разрешений для пользователя.

## <a name="next-steps"></a>Дальнейшие действия
[Добавление клиента Azure Stack](azure-stack-add-new-user-aad.md)

