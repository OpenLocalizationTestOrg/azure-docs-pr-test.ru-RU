---
title: "элементы marketplace aaaDownload из Azure | Документы Microsoft"
description: "Элементы marketplace можно загрузить из Azure toomy развертывания Azure стека."
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
ms.openlocfilehash: 734470fbacc09617908a2f6db9107ffa9c39e51d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="download-marketplace-items-from-azure-tooazure-stack"></a>Загрузить элементы marketplace из Azure tooAzure стека

Как вы решите какие tooinclude содержимого в вашей стек Azure marketplace, рассмотрите возможность hello содержимого, доступного из hello Azure marketplace. Можно загрузить из проверенного список элементов Azure marketplace, которые были заранее протестированных toorun стек Azure. Список toothis часто добавляются новые элементы, поэтому убедитесь, что следите за новым содержимым.

элементы marketplace toodownload, сначала необходимо выполнить [Azure стеком регистров с помощью Azure](azure-stack-register.md). 

## <a name="download"></a>Загрузить
1. Войдите в систему toohello портала администратора Azure стека (https://portal.local.azurestack.external).
2. Некоторые элементы marketplace может быть очень большим.  Проверьте toomake убедиться, что имеется достаточно места на компьютере, щелкнув **поставщиков ресурсов** > **хранения**.

    ![](media/azure-stack-download-azure-marketplace-item/image01.png)

3. Нажмите кнопку **дополнительные службы** > **управления Marketplace**.

    ![](media/azure-stack-download-azure-marketplace-item/image02.png)

4. Нажмите кнопку **добавить из Azure** toosee список элементов, доступных для загрузки. Можно щелкнуть ее описание каждого элемента в списке tooview hello и размер загружаемого файла.

    ![](media/azure-stack-download-azure-marketplace-item/image03.png)

5. Элемент SELECT hello hello списка и нажмите кнопку **загрузить**. Запустится загрузка образа виртуальной Машины hello для выбранного элемента hello. Время загрузки различаются.

    ![](media/azure-stack-download-azure-marketplace-item/image04.png)

6. После завершения загрузки hello, вы можете развернуть новый элемент marketplace как оператор облака или пользователь клиента. Нажмите кнопку **+ создать**, поиск среди hello категории для hello создать элемент marketplace, а затем выберите элемент hello.
7. Нажмите кнопку **создать** tooopen копирование hello возможности создания для hello вновь загружена элемента. Выполните пошаговые инструкции toodeploy hello ваш элемент.

## <a name="next-steps"></a>Дальнейшие действия

[Создание и публикация элемента Marketplace](azure-stack-create-and-publish-marketplace-item.md)
