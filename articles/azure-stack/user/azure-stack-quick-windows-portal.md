---
title: "Краткое руководство по Azure Stack. Создание виртуальной машины Windows"
description: "Краткое руководство по Azure Stack. Создание виртуальной машины Windows с помощью портала"
services: azure-stack
author: ErikjeMS
manager: byronr
ms.service: azure-stack
ms.topic: quickstart
ms.date: 09/15/2017
ms.author: erikje
ms.custom: mvc
ms.openlocfilehash: 64a623b3f5cb443e0676e7d89d7040837be95737
ms.sourcegitcommit: 7136d06474dd20bb8ef6a821c8d7e31edf3a2820
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/05/2017
---
# <a name="create-a-windows-virtual-machine-with-the-azure-stack-portal"></a>Создание виртуальной машины Windows с помощью портала Azure Stack

Вы можете создать виртуальную машину Windows с помощью портала Azure Stack. Портал — это интерфейс пользователя на основе браузера, с помощью которого вы можете создавать, настраивать и администрировать ресурсы.

## <a name="sign-in-to-the-azure-stack-portal"></a>Вход на портал Azure Stack

Войдите на портал Azure Stack. Адрес портала Azure Stack зависит от того, к какому продукту Azure Stack вы подключаетесь:

* При работе с пакетом SDK для Azure Stack (ASDK), перейдите по адресу https://portal.local.azurestack.external.
* При работе с интегрированной системой Azure Stack используйте URL-адрес, предоставленный оператором Azure Stack.

## <a name="create-a-virtual-machine"></a>Создание виртуальной машины

1. Щелкните **Создать** > **Вычисления** > **Windows Server 2016 Datacenter Eval** > **Создать**. Если вы не видите вариант **Windows Server 2016 Datacenter Eval**, обратитесь к оператору Azure Stack. Этот вариант необходимо добавить в Marketplace, как описано в руководстве по [добавлению образа виртуальной машины Windows Server 2016 в Azure Stack Marketplace](../azure-stack-add-default-image.md). 
    ![](media/azure-stack-quick-windows-portal/image01.png)
2. В колонке **Основные сведения** введите **имя**, **имя пользователя** и **пароль**. Выберите **подписку**. Создайте **группу ресурсов** или выберите существующую, укажите **расположение**, а затем нажмите **ОК**.

    ![](media/azure-stack-quick-windows-portal/image02.png)
3. В разделе **Выбор размера**, щелкните **D1 Standard** > **Выбрать**.
    ![](media/azure-stack-quick-windows-portal/image03.png)
4. В разделе **Параметры** оставьте значения по умолчанию и нажмите кнопку **ОК**.
    ![](media/azure-stack-quick-windows-portal/image04.png)
5. В колонке **Сводка** нажмите кнопку **ОК**, чтобы создать виртуальную машину. 
    ![](media/azure-stack-quick-windows-portal/image05.png)
6. Чтобы просмотреть новую виртуальную машину, щелкните **All resources** (Все ресурсы), а затем найдите виртуальную машину и щелкните ее имя.
    ![](media/azure-stack-quick-windows-portal/image06.png)

## <a name="clean-up-resources"></a>Очистка ресурсов

Вы можете удалить виртуальную машину, группу ресурсов и все связанные ресурсы. Для этого выберите группу ресурсов на странице виртуальной машины и нажмите кнопку **Удалить**.

## <a name="next-steps"></a>Дальнейшие действия
В этом кратком руководстве вы развернули простую виртуальную машину Windows. Дополнительные сведения о виртуальных машинах Azure Stack см. в [рекомендациях по работе с виртуальными машинами в Azure Stack](azure-stack-vm-considerations.md).
