---
title: "aaaHow tooretain постоянного виртуального IP-адреса облачной службы Azure | Документы Microsoft"
description: "Узнайте, как tooensure, hello виртуальный IP-адрес (VIP) облачной службы Azure не изменяется."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 4a58e2c6-7a79-4051-8a2c-99182ff8b881
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/21/2017
ms.author: kraigb
ms.openlocfilehash: 9e27121797ffb61517b8d2c2661ec44ff7298968
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="retain-a-constant-virtual-ip-address-for-an-azure-cloud-service"></a>Сохранение постоянного виртуального IP-адреса для облачной службы Azure
При обновлении облачной службы, размещенной в Azure, может потребоваться tooensure, hello виртуальный IP-адрес (VIP) hello службы не изменяется. Многие службы управления доменом используют hello доменных имен (DNS) для регистрации доменных имен. DNS работает только в том случае, если hello hello виртуальный IP-адрес остается таким же. Можно использовать hello **мастер публикации** в tooensure инструментов Azure, hello виртуальный IP-адрес облачной службы не изменяется при обновлении. Дополнительные сведения о том, как toouse управления доменами DNS для облачных служб в разделе [Настройка имени пользовательского домена для облачной службы Azure](cloud-services/cloud-services-custom-domain-name.md).

## <a name="publish-a-cloud-service-without-changing-its-vip"></a>Публикация облачной службы без изменения ее виртуального IP-адреса
При первом развертывании tooAzure в конкретной среде, например hello рабочей среде, выделяется Hello виртуальный IP-адрес облачной службы. Hello изменения только в том случае, если явно удалить hello развертывания или развертывания hello неявно удаляется hello развертывания процесса обновления. hello tooretain виртуальных IP-адресов, не требуется удалять развертывание и убедитесь, что Visual Studio не удаляет развертывание автоматически. 

Можно указать параметры развертывания в hello **мастер публикации**, который поддерживает несколько вариантов развертывания. Можно указать новое развертывание или развертывание обновления, которое может быть добавочным или одновременным. Оба вида развертывания обновлений сохраняют hello виртуальных IP-адресов. Определение разных типов развертывания см. в статье [Мастер публикации приложений Azure](vs-azure-tools-publish-azure-application-wizard.md). Кроме того можно управлять, удаляется ли hello предыдущего развертывания облачной службы при возникновении ошибки. Если этот параметр не установлен правильно, hello виртуального IP-адреса могут измениться неожиданно.

## <a name="update-a-cloud-service-without-changing-its-vip"></a>Обновление облачной службы без изменения ее виртуального IP-адреса
1. Создайте или откройте проект облачной службы Azure в среде Visual Studio. 

2. В **обозревателе решений**, щелкните правой кнопкой мыши проект hello. Выберите hello контекстное меню **публикации**.

    ![Меню публикации](./media/vs-azure-tools-cloud-service-retain-a-constant-virtual-ip-address/solution-explorer-publish-menu.png)

3. В hello **публикации приложения Azure** диалоговое окно, выберите hello toowhich подписки Azure, требуется toodeploy. При необходимости войдите в систему и нажмите кнопку **Далее**.

    ![Публикация приложения Azure: страница входа](./media/vs-azure-tools-cloud-service-retain-a-constant-virtual-ip-address/azure-publish-signin.png)

4. На hello **Общие параметры** убедитесь в существовании hello hello облачной службы toowhich вы развертываете, hello **среды**, hello **конфигурации построения**и hello **Конфигурации службы** заданы правильно.

    ![Публикация приложения Azure: вкладка "Общие параметры"](./media/vs-azure-tools-cloud-service-retain-a-constant-virtual-ip-address/azure-publish-common-settings.png)

5. На hello **Дополнительные параметры** убедитесь, что hello **метка развертывания** и hello **учетной записи хранилища** заданы правильно. Убедитесь, что hello **удалить развертывание при сбое** флажок снят и убедитесь, что hello **обновление развертывания** установлен флажок. При очистке hello **удалить развертывание при сбое** флажок, вы убедитесь, что VIP-адрес не будет потерян при возникновении ошибки во время развертывания. Выбрав hello **обновление развертывания** флажок, вы убедитесь, что развертывание не было удалено и VIP-адрес не будет потерян при повторной публикации приложения. 

    ![Публикация приложения Azure: вкладка "Дополнительные параметры"](./media/vs-azure-tools-cloud-service-retain-a-constant-virtual-ip-address/azure-publish-advanced-settings.png)

6. toofurther указать, как будет обновлен toobe ролей hello, выберите **параметры** Далее слишком**обновление развертывания**. Затем выберите **Добавочное обновление** или **Одновременное обновление**. Нажмите кнопку **ОК**. Выберите **добавочное обновление** tooupdate каждого экземпляра приложения, один за другим, так что hello приложения доступна всегда. Выберите **одновременное обновление** tooupdate все экземпляры приложения в hello то же время. Одновременное обновление выполняется быстрее, но службы могут быть недоступны во время процесса обновления hello. По завершении нажмите кнопку **Далее**.

    ![Публикация приложения Azure: страница "Параметры развертывания"](./media/vs-azure-tools-cloud-service-retain-a-constant-virtual-ip-address/azure-publish-deployment-update-settings.png)

7. В hello **публикации приложения Azure** выберите **Далее** до hello **Сводка** -страница. Проверьте параметры и нажмите кнопку **Опубликовать**.
   
    ![Публикация приложения Azure: страница "Сводка"](./media/vs-azure-tools-cloud-service-retain-a-constant-virtual-ip-address/azure-publish-summary.png)

## <a name="next-steps"></a>Дальнейшие действия
- [Используя мастер публикации Visual Studio Azure приложения hello](vs-azure-tools-publish-azure-application-wizard.md)

