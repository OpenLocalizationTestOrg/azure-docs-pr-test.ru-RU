---
title: "Загрузить элементы marketplace из Azure | Документы Microsoft"
description: "Мои развертывание стека Azure можно загрузить элементы marketplace из Azure."
services: azure-stack
documentationcenter: 
author: ErikjeMS
manager: byronr
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/03/2017
ms.author: erikje
ms.openlocfilehash: 4d7c335a3c68cc9bb8cb0c823883716a3dd6620a
ms.sourcegitcommit: 90e2cced6a773b1b52f999ba73cd8877305d270b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="download-marketplace-items-from-azure-to-azure-stack"></a>Загрузить элементы marketplace из Azure в стек Azure

*Применяется к: стек Azure интегрированных систем и пакет средств разработки стек Azure*

Как вы решите, какое содержимое для включения в ваш стек Azure marketplace, рассмотрите возможность содержимое из Azure marketplace. Можно загрузить из списка проверенного Azure marketplace элементов, которые были заранее протестированных для запуска на Azure стека. Часто новые элементы добавляются в этот список, поэтому убедитесь, что следите за новым содержимым.

Чтобы загрузить элементы marketplace, сначала необходимо выполнить [Azure стеком регистров с помощью Azure](azure-stack-register.md). 

## <a name="download"></a>Загрузить
1. Войдите в портал администратора Azure стека (https://portal.local.azurestack.external).
2. Некоторые элементы marketplace может быть очень большим.  Убедитесь, что имеется достаточно места на компьютере, щелкнув **поставщиков ресурсов** > **хранения**.

    ![](media/azure-stack-download-azure-marketplace-item/image01.png)

3. Нажмите кнопку **дополнительные службы** > **управления Marketplace**.

    ![](media/azure-stack-download-azure-marketplace-item/image02.png)

4. Нажмите кнопку **добавить из Azure** для просмотра списка элементов, доступных для загрузки. Можно щелкнуть каждый элемент в списке, чтобы просмотреть ее описание и размер загружаемого файла.

    ![](media/azure-stack-download-azure-marketplace-item/image03.png)

5. Выберите элемент в списке и нажмите кнопку **загрузить**. Запустится загрузка образа виртуальной Машины для выбранного элемента. Время загрузки различаются.

    ![](media/azure-stack-download-azure-marketplace-item/image04.png)

6. После завершения загрузки, можно развернуть новый элемент marketplace как оператор стек Azure или пользователя. Нажмите кнопку **+ создать**, поиск среди категории для нового элемента marketplace, а затем выберите элемент.
7. Нажмите кнопку **создать** открывая процесс создания для вновь загруженного элемента. Выполните пошаговые инструкции для развертывания вашего элемента.

## <a name="next-steps"></a>Дальнейшие действия

[Создание и публикация элемента Marketplace](azure-stack-create-and-publish-marketplace-item.md)
