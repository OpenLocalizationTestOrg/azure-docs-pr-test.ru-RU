---
title: "Портал Azure: динамическое маскирование данных базы данных SQL | Документация Майкрософт"
description: "Как tooget работу с динамического маскирования в портале Azure hello данных базы данных SQL"
services: sql-database
documentationcenter: 
author: ronitr
manager: jhubbard
editor: 
ms.assetid: "2"
ms.service: sql-database
ms.custom: security
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 11/22/2016
ms.author: ronitr; ronmat
ms.openlocfilehash: 5c5f74682a15d42eceb78c3ca0705401e1ac0ae7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-sql-database-dynamic-data-masking-with-hello-azure-portal"></a>Приступая к работе с базой данных SQL с портала Azure hello маскировки данных

В этом разделе показано, как tooimplement [маскирование динамических данных](sql-database-dynamic-data-masking-get-started.md) с hello портал Azure. Также можно реализовать с помощью маскирования динамических данных [командлеты базы данных SQL Azure](https://msdn.microsoft.com/library/azure/mt574084.aspx) или hello [API-интерфейса REST](https://msdn.microsoft.com/library/dn505719.aspx).


## <a name="set-up-dynamic-data-masking-for-your-database-using-hello-azure-portal"></a>Настройка динамического маскирования данных для базы данных с помощью портала Azure hello
1. Здравствуйте, запустить портал Azure на [https://portal.azure.com](https://portal.azure.com).
2. Перейдите в колонку параметров toohello hello базы данных, которая включает в себя hello конфиденциальных данных, toomask.
3. Нажмите кнопку hello **динамической маскировки данных** плитку, которая запускает hello **динамической маскировки данных** колонке конфигурации.
   
   * Кроме того, может воспользоваться прокруткой вниз toohello **операции** и нажмите кнопку **динамической маскировки данных**.
     
     ![Область навигации](./media/sql-database-dynamic-data-masking-get-started/4_ddm_settings_tile.png)<br/><br/>
4. В hello **динамической маскировки данных** колонке конфигурации, вы можете увидеть некоторые столбцы базы данных, подсистемы рекомендаций hello отметила для маски. Чтобы tooaccept рекомендации hello, просто нажав кнопку **Добавить маску** для одного или нескольких столбцов и маски будет создана на основе типа hello по умолчанию для этого столбца. Вы можете изменить hello функции маскировки, щелкнув правило маскирования hello и редактирования hello маскирования другой формат поля формата tooa по своему усмотрению. Быть убедиться, что tooclick **Сохранить** toosave параметры.
   
    ![Область навигации](./media/sql-database-dynamic-data-masking-get-started/5_ddm_recommendations.png)<br/><br/>
5. Маска для любого столбца в базе данных, вверху hello hello tooadd **динамической маскировки данных** настройку колонке нажмите кнопку **Добавить маску** tooopen hello **добавить правило маскировки** колонке конфигурации
   
    ![Область навигации](./media/sql-database-dynamic-data-masking-get-started/6_ddm_add_mask.png)<br/><br/>
6. Выберите hello **схемы**, **таблицы** и **столбца** toodefine hello, назначенный полю, будут замаскированы.
7. Выберите **формат поля маскировки** из списка hello маскирования категории конфиденциальных данных.
   
    ![Область навигации](./media/sql-database-dynamic-data-masking-get-started/7_ddm_mask_field_format.png)<br/><br/>        
8. Нажмите кнопку **Сохранить** в маскировки правило колонке tooupdate hello набор правил в hello политики динамического маскирования данных маскировки данных hello.
9. Тип hello SQL пользователям или удостоверений AAD, которые должны быть исключены из маски и иметь доступ к конфиденциальным данным немаскированные toohello. Это должен быть список пользователей, разделенных точкой с запятой. Обратите внимание, что пользователи с правами администратора всегда доступа toohello исходного немаскированные данные.
   
    ![Область навигации](./media/sql-database-dynamic-data-masking-get-started/8_ddm_excluded_users.png)
   
   > [!TIP]
   > toomake, поэтому Здравствуйте, прикладной уровень может отобразить конфиденциальных данных для пользователей приложений, для работы в привилегированном режиме, hello SQL-пользователь или приложение hello удостоверений AAD используется база данных tooquery hello. Настоятельно рекомендуется, что этот список содержит минимальное количество привилегированных пользователей toominimize раскрытия конфиденциальных данных hello.
   > 
   > 
10. Нажмите кнопку **Сохранить** в hello политики маскирования данных конфигурации колонке toosave hello новых или обновленных маски.


## <a name="next-steps"></a>Дальнейшие действия

* Обзор динамического маскирования данных см. в разделе [Динамическое маскирование данных](sql-database-dynamic-data-masking-get-started.md).
* Также можно реализовать с помощью маскирования динамических данных [командлеты базы данных SQL Azure](https://msdn.microsoft.com/library/azure/mt574084.aspx) или hello [API-интерфейса REST](https://msdn.microsoft.com/library/dn505719.aspx).
