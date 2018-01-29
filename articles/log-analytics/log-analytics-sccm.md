---
title: "Подключение Configuration Manager к Log Analytics | Документация Майкрософт"
description: "В этой статье описаны действия, с помощью которых можно подключить Configuration Manager к Log Analytics и начать анализ данных."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: f2298bd7-18d7-4371-b24a-7f9f15f06d66
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2017
ms.author: banders
ms.openlocfilehash: 7acf0cbd4f4cba885e6cc91dfe3cb68306a3649a
ms.sourcegitcommit: 719dd33d18cc25c719572cd67e4e6bce29b1d6e7
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/08/2018
---
# <a name="connect-configuration-manager-to-log-analytics"></a>Подключение Configuration Manager к Log Analytics
System Center Configuration Manager можно подключить к Log Analytics в OMS, чтобы синхронизировать данные коллекции устройств. Так данные из иерархии Configuration Manager можно сделать доступными в OMS.

## <a name="prerequisites"></a>Технические условия

Поддержка в Log Analytics текущей версии System Center Configuration Manager, версии 1606 или более поздних версий.  

## <a name="configuration-overview"></a>Общие сведения о настройке
Следующие шаги описывают процесс для подключения к службе анализа журналов Configuration Manager.  

1. На портале Azure зарегистрировать приложение веб-приложение или веб-API как Configuration Manager и убедитесь, что идентификатор клиента и секретный ключ клиента из регистрации из Azure Active Directory. В разделе [использовать портал для создания приложения и службы-участника, который имеет доступ к ресурсам Active Directory](../azure-resource-manager/resource-group-create-service-principal-portal.md) подробные сведения о том, как выполнить этот шаг.
2. На портале Azure [укажите Configuration Manager (зарегистрированные веб-приложения) с разрешениями на доступ к OMS](#provide-configuration-manager-with-permissions-to-oms).
3. В Configuration Manager [добавьте подключение с помощью мастера добавления подключений к OMS](#add-an-oms-connection-to-configuration-manager).
4. В случае утери пароля или секретного ключа клиента либо истечения срока их действия вы можете [обновить свойства подключения](#update-oms-connection-properties) в Configuration Manager.
5. Руководствуясь сведениями на портале OMS, [скачайте и установите Microsoft Monitoring Agent](#download-and-install-the-agent) на компьютере под управлением роли системы сайта для точки подключения службы Configuration Manager. Агент отправляет данные Configuration Manager в OMS.
6. В Log Analytics [импортируйте коллекции из Configuration Manager](#import-collections) как группы компьютеров.
7. В Log Analytics просмотрите данные из Configuration Manager как [группы компьютеров](log-analytics-computer-groups.md).

Дополнительные сведения о подключении Configuration Manager к OMS см. в статье [Sync data from Configuration Manager to the Microsoft Operations Management Suite](https://technet.microsoft.com/library/mt757374.aspx) (Синхронизация данных из Configuration Manager в Microsoft Operations Management Suite).

## <a name="provide-configuration-manager-with-permissions-to-oms"></a>Предоставление Configuration Manager разрешений в OMS
Следующая процедура предоставляет портал Azure с разрешениями на доступ к OMS. В частности, необходимо предоставить *роль участника* пользователям в группе ресурсов, чтобы разрешить порталу Azure для подключения Configuration Manager к OMS.

> [!NOTE]
> Необходимо указать разрешения на доступ к OMS для Configuration Manager. В противном случае появляется сообщение об ошибке при использовании мастера конфигурации в Configuration Manager.
>
>

1. Откройте [портал Azure](https://portal.azure.com/) и нажмите кнопку **Обзор** > **аналитика журналов (OMS)** Открытие аналитика журналов (OMS).  
2. На **аналитика журналов (OMS)**, нажмите кнопку **добавить** Открытие **рабочей области OMS**.  
   ![OMS](./media/log-analytics-sccm/sccm-azure01.png)
3. На **рабочей области OMS**, укажите следующие сведения и нажмите кнопку **ОК**.

   * **рабочая область OMS**;
   * **Подписка**
   * **Группа ресурсов**
   * **Местоположение.**
   * **Ценовая категория**  
     ![OMS](./media/log-analytics-sccm/sccm-azure02.png)  

     > [!NOTE]
     > В примере выше создается новая группа ресурсов. В нашем примере она нужна только для того, чтобы предоставить Configuration Manager разрешения для рабочей области OMS.
     >
     >
4. Нажмите кнопку **Обзор** > **групп ресурсов** Открытие **групп ресурсов**.
5. В **групп ресурсов**, щелкните имя группы ресурсов, созданной ранее, чтобы открыть &lt;имя группы ресурсов&gt; параметры.  
   ![Параметры группы ресурсов](./media/log-analytics-sccm/sccm-azure03.png)
6. В &lt;имя группы ресурсов&gt; параметры, щелкните элемент управления доступа (IAM), чтобы открыть &lt;имя группы ресурсов&gt; пользователей.  
   ![Группа ресурсов пользователей](./media/log-analytics-sccm/sccm-azure04.png)  
7. В &lt;имя группы ресурсов&gt; пользователей, нажмите кнопку **добавить** Открытие **добавить доступ**.
8. В **добавить доступ**, нажмите кнопку **выберите роль**, а затем выберите **участника** роли.  
   ![Выбор роли](./media/log-analytics-sccm/sccm-azure05.png)  
9. Щелкните **Добавить пользователей**, выберите пользователя Configuration Manager, щелкните **Выбрать** и нажмите кнопку **ОК**.  
   ![Добавление пользователей](./media/log-analytics-sccm/sccm-azure06.png)  

## <a name="add-an-oms-connection-to-configuration-manager"></a>Добавление подключения к OMS в Configuration Manager
Чтобы добавить подключение к OMS, необходимо настроить [точку подключения службы](https://technet.microsoft.com/library/mt627781.aspx) в среде Configuration Manager для работы в оперативном режиме.

1. В рабочей области **Администрирование** в Configuration Manager выберите **Соединитель OMS**. Откроется **мастер добавления подключений к OMS**. Щелкните **Далее**.
2. На экране **Общие** убедитесь, что вы выполнили следующие действия и указали сведения по каждому пункту, а затем щелкните **Далее**.

   1. На портале Azure Configuration Manager после регистрации веб-приложение или веб-API приложение как и у вас есть [идентификатор клиента из регистрации](../active-directory/active-directory-integrating-applications.md).
   2. На портале Azure вы создали секретный ключ приложения для зарегистрированного приложения в Azure Active Directory.  
   3. На портале Azure предоставили зарегистрированных веб-приложения с разрешением на доступ к OMS.  
      ![Страница "Общие" мастера подключений к OMS](./media/log-analytics-sccm/sccm-console-general01.png)
3. На **Azure Active Directory** экрана, настроить параметры подключения к OMS, предоставляя вашей **клиента**, **идентификатор клиента**, и **секретный ключ клиента** , а затем выберите **Далее**.  
   ![Страница "Azure Active Directory" мастера подключений к OMS](./media/log-analytics-sccm/sccm-wizard-tenant-filled03.png)
4. Если вы успешно выполнили все остальные процедуры, сведения, указанные на экране **OMS Connection Configuration** (Конфигурация подключения к OMS), автоматически появятся на этой странице. Данные параметры соединения должны отображаться для вашего **подписки Azure**, **группы ресурсов Azure**, и **рабочая область Operations Management Suite**.  
   ![Страница "Подключение" мастера подключений к OMS](./media/log-analytics-sccm/sccm-wizard-configure04.png)
5. Мастер подключится к службе OMS, используя указанные вами сведения. Выберите коллекции устройств, которые требуется синхронизировать с OMS, а затем нажмите кнопку **Добавить**.  
   ![Выбор коллекций](./media/log-analytics-sccm/sccm-wizard-add-collections05.png)
6. Проверьте параметры подключения на экране **Сводка**, а затем щелкните **Далее**. На экране **Ход выполнения** отображается состояние подключения (должно отобразиться состояние **Выполнено**).

> [!NOTE]
> OMS необходимо подключить к сайту верхнего уровня в иерархии. При подключении OMS к автономным первичным сайтом и затем добавить в среду на сайте центра администрирования, необходимо удалить и заново создать подключение OMS в новой иерархии.
>
>

Установив связь между Configuration Manager и OMS, можно добавить или удалить коллекции и просмотреть свойства подключения к OMS.

## <a name="update-oms-connection-properties"></a>Обновление свойств подключения к OMS
В случае утери пароля или секретного ключа клиента либо истечения срока их действия необходимо вручную обновить свойства подключения к OMS.

1. В диспетчере конфигурации перейдите **облачные службы**, а затем выберите **соединитель OMS** Открытие **свойства подключения OMS** страницы.
2. На этой странице щелкните **Azure Active Directory**, чтобы просмотреть сведения о **клиенте**, **идентификаторе клиента** и **сроке действия секретного ключа клиента**. **Проверьте** **секретный ключ клиента**, если срок его действия истек.

## <a name="download-and-install-the-agent"></a>Загрузка и установка агента
1. На портале OMS [скачайте файл установки агента из OMS](log-analytics-windows-agent.md).
2. Чтобы установить и настроить агент на компьютере под управлением роли системы сайта для точки подключения службы Configuration Manager, используйте один из следующих методов:
   * [установка агента с помощью программы установки](log-analytics-windows-agent.md);
   * [установка агента с помощью командной строки](log-analytics-windows-agent.md);
   * [установка агента с помощью DSC в службе автоматизации Azure](log-analytics-windows-agent.md).

## <a name="import-collections"></a>Импорт коллекций
Добавив подключение к OMS в Configuration Manager и установив агент на компьютере под управлением роли системы сайта для точки подключения службы Configuration Manager, можно переходить к следующему шагу — импорту коллекций из Configuration Manager в OMS как групп компьютеров.

После включения импорта данные о членстве в коллекциях извлекаются каждые 3 часа. Так обеспечивается актуальность сведений о членстве в коллекциях. Импорт можно отключить в любое время.

1. На портале OMS щелкните **Параметры**.
2. Перейдите на вкладку **Группы компьютеров**, а затем выберите вкладку **SCCM**.
3. Выберите **Импортировать членства в коллекциях Configuration Manager** и нажмите кнопку **Сохранить**.  
   ![Вкладка "SCCM" на вкладке "Группы компьютеров"](./media/log-analytics-sccm/sccm-computer-groups01.png)

## <a name="view-data-from-configuration-manager"></a>Просмотр данных из Configuration Manager
Когда вы добавите подключение к OMS в Configuration Manager и установите агент на компьютере под управлением роли системы сайта для точки подключения службы Configuration Manager, данные будут отправляться из агента в OMS. В OMS коллекции из Configuration Manager будут отображаться как [группы компьютеров](log-analytics-computer-groups.md). Группы можно просматривать на странице **Configuration Manager**, выбрав вкладку **Группы компьютеров** в разделе **Параметры**.

После импорта коллекций можно увидеть число обнаруженных компьютеров с членством в коллекциях. Также можно увидеть число импортированных коллекций.

![Вкладка "SCCM" на вкладке "Группы компьютеров"](./media/log-analytics-sccm/sccm-computer-groups02.png)

Если щелкнуть одну из них, откроется окно поиска, в котором отображаются либо все импортированные группы, либо все компьютеры, принадлежащие к каждой группе. С помощью [поиска по журналам](log-analytics-log-searches.md) можно выполнить подробный анализ данных Configuration Manager.

## <a name="next-steps"></a>Дальнейшие действия
* Воспользуйтесь [поиском по журналам](log-analytics-log-searches.md) для просмотра подробных сведений о данных Configuration Manager.
