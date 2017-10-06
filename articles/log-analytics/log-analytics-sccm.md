---
title: "Аналитика Configuration Manager tooLog aaaConnect | Документы Microsoft"
description: "В этой статье показано hello действия tooconnect tooLog Configuration Manager, аналитики и начала анализа данных."
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
ms.openlocfilehash: dc50ebc46020a806d99d1a3e3d0e91fd09ad2c32
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-configuration-manager-toolog-analytics"></a>Аналитика Configuration Manager tooLog Connect
Вы можете подключиться к System Center Configuration Manager tooLog аналитика в OMS toosync устройство сбора данных. Так данные из иерархии Configuration Manager можно сделать доступными в OMS.

## <a name="prerequisites"></a>Предварительные требования

Поддержка в Log Analytics текущей версии System Center Configuration Manager, версии 1606 или более поздних версий.  

## <a name="configuration-overview"></a>Общие сведения о настройке
Здравствуй, следующие шаги перечислены tooconnect процесса hello Analytics tooLog Configuration Manager.  

1. В hello портала управления Azure регистрация Configuration Manager в качестве веб-приложение или веб-API приложения и убедитесь, что hello идентификатор и клиент секретный ключ клиента из hello регистрации из Azure Active Directory. В разделе [использовать приложение портала toocreate Active Directory и участника-службы, могут обращаться к ресурсам](../azure-resource-manager/resource-group-create-service-principal-portal.md) подробные сведения о том, как выполнить этот шаг.
2. В hello портала управления Azure [предоставить разрешение tooaccess OMS Configuration Manager (hello зарегистрированных веб-приложение)](#provide-configuration-manager-with-permissions-to-oms).
3. В Configuration Manager [добавить соединения с помощью приветствия мастера установки подключения OMS](#add-an-oms-connection-to-configuration-manager).
4. В Configuration Manager [обновить свойства соединения hello](#update-oms-connection-properties) Если hello пароль или клиент секретный ключ никогда не истекает, или теряется.
5. С данными из портала OMS hello [загрузить и установить Microsoft Monitoring Agent hello](#download-and-install-the-agent) роли системы сайта точки на компьютере hello hello подключения службы Configuration Manager. Hello агент отправляет данные tooOMS Configuration Manager.
6. В Log Analytics [импортируйте коллекции из Configuration Manager](#import-collections) как группы компьютеров.
7. В Log Analytics просмотрите данные из Configuration Manager как [группы компьютеров](log-analytics-computer-groups.md).

Дополнительные сведения о подключении tooOMS Configuration Manager на [синхронизации данных из Configuration Manager toohello Microsoft Operations Management Suite](https://technet.microsoft.com/library/mt757374.aspx).

## <a name="provide-configuration-manager-with-permissions-toooms"></a>Предоставить разрешения tooOMS Configuration Manager
Hello следующая процедура описывает hello портала управления Azure с tooaccess разрешения OMS. В частности, необходимо предоставить hello *роль участника* toousers в группе ресурсов hello в порядке tooallow hello портала управления Azure tooconnect tooOMS Configuration Manager.

> [!NOTE]
> Необходимо указать разрешения на доступ к OMS для Configuration Manager. В противном случае появится сообщение об ошибке при использовании мастера конфигурации hello в Configuration Manager.
>
>

1. Откройте hello [портал Azure](https://portal.azure.com/) и нажмите кнопку **Обзор** > **аналитика журналов (OMS)** tooopen hello аналитика журналов (OMS) колонки.  
2. На hello **аналитика журналов (OMS)** колонка, щелкните **добавить** tooopen hello **рабочей области OMS** колонку.  
   ![Колонка OMS](./media/log-analytics-sccm/sccm-azure01.png)
3. На hello **рабочей области OMS** колонке укажите hello следующую информацию и нажмите кнопку **ОК**.

   * **рабочая область OMS**;
   * **Подписка**
   * **Группа ресурсов**
   * **Расположение**
   * **ценовая категория**.  
     ![Колонка OMS](./media/log-analytics-sccm/sccm-azure02.png)  

     > [!NOTE]
     > приведенном выше примере Hello создает новую группу ресурсов. Группа ресурсов Hello находится только используемые tooprovide Configuration Manager с рабочей областью OMS toohello разрешения в этом примере.
     >
     >
4. Нажмите кнопку **Обзор** > **групп ресурсов** tooopen hello **групп ресурсов** колонку.
5. В hello **групп ресурсов** колонка, щелкните группу ресурсов hello, созданной ранее tooopen hello &lt;имя группы ресурсов&gt; колонку параметров.  
   ![Колонка с параметрами группы ресурсов](./media/log-analytics-sccm/sccm-azure03.png)
6. В hello &lt;имя группы ресурсов&gt; колонку параметров щелкните hello tooopen доступа элемента управления (IAM) &lt;имя группы ресурсов&gt; колонка "пользователи".  
   ![Колонка "Пользователи" для группы ресурсов](./media/log-analytics-sccm/sccm-azure04.png)  
7. В hello &lt;имя группы ресурсов&gt; колонка "пользователи", нажмите кнопку **добавить** tooopen hello **добавить доступ** колонку.
8. В hello **добавить доступ** колонке нажмите кнопку **выберите роль**, а затем выберите hello **участника** роли.  
   ![Выбор роли](./media/log-analytics-sccm/sccm-azure05.png)  
9. Нажмите кнопку **добавить пользователей**выберите hello пользователя Configuration Manager, нажмите кнопку **выберите**, а затем нажмите кнопку **ОК**.  
   ![Добавление пользователей](./media/log-analytics-sccm/sccm-azure06.png)  

## <a name="add-an-oms-connection-tooconfiguration-manager"></a>Добавить tooConfiguration подключение OMS Manager
В порядке tooadd подключение к OMS, должен иметь свою среду Configuration Manager [точка подключения службы](https://technet.microsoft.com/library/mt627781.aspx) работающем в режиме online.

1. В hello **администрирования** Configuration Manager, выберите рабочую область **соединитель OMS**. При этом откроется hello **мастер подключения OMS**. Щелкните **Далее**.
2. На hello **Общие** Подтвердите, что выполнены следующие действия hello и содержать подробные сведения для каждого элемента, затем выберите, **Далее**.

   1. В hello портала управления Azure, веб-приложение или веб-API приложение как зарегистрированное Configuration Manager и что имеют hello [идентификатор клиента из регистрации hello](../active-directory/active-directory-integrating-applications.md).
   2. Hello портала управления Azure вы создали секретный ключ приложения для зарегистрированного приложения hello в Azure Active Directory.  
   3. В hello портала управления Azure с разрешением tooaccess OMS предоставили hello зарегистрированных веб-приложения.  
      ![Страница мастера общие tooOMS подключения](./media/log-analytics-sccm/sccm-console-general01.png)
3. На hello **Azure Active Directory** экрана, настройте ваш tooOMS параметры подключения, предоставляя вашей **клиента** , **идентификатор клиента** , и **секретный ключ клиента**  , а затем выберите **Далее**.  
   ![Страница мастера Azure Active Directory tooOMS подключения](./media/log-analytics-sccm/sccm-wizard-tenant-filled03.png)
4. Если вы выполнили все hello других процедур успешно, затем hello сведения о hello **Настройка подключения к OMS** экрана, автоматически отобразятся на этой странице. Сведения для настройки подключения hello должен появляться для вашего **подписки Azure** , **группы ресурсов Azure** , и **рабочая область Operations Management Suite**.  
   ![Страница мастера подключения к OMS tooOMS подключения](./media/log-analytics-sccm/sccm-wizard-configure04.png)
5. Мастер Hello подключается службой OMS toohello помощью ввода информации hello. Выберите коллекции устройств hello toosync с OMS и нажмите кнопку **добавить**.  
   ![Выбор коллекций](./media/log-analytics-sccm/sccm-wizard-add-collections05.png)
6. Проверьте параметры подключения на hello **Сводка** экрана, а затем выберите **Далее**. Hello **выполняется** экрана показано состояние подключения hello, то следует **завершить**.

> [!NOTE]
> Сайт верхнего уровня toohello OMS необходимо подключиться в иерархии. При подключении OMS tooa автономного первичного сайта и затем добавить среду tooyour сайта центра администрирования, будет иметь toodelete и повторно создайте подключение OMS hello в новой иерархии hello.
>
>

После связали tooOMS Configuration Manager, можно добавить или удалить коллекции и просмотра свойств hello hello подключение OMS.

## <a name="update-oms-connection-properties"></a>Обновление свойств подключения к OMS
Если пароль или клиент секретный ключ никогда не истекает срок действия или теряется, вам потребуется обновление hello toomanually OMS-свойства соединения.

1. В диспетчере конфигурации перейдите слишком**облачные службы** , а затем выберите **соединитель OMS** tooopen hello **свойства подключения OMS** страницы.
2. На этой странице щелкните hello **Azure Active Directory** вкладке tooview вашей **клиента**, **идентификатор клиента**, **срок действия секретного ключа клиента**. **Проверьте** **секретный ключ клиента**, если срок его действия истек.

## <a name="download-and-install-hello-agent"></a>Загрузка и установка агента hello
1. На портале OMS hello [загрузки hello файла установки агента с OMS](log-analytics-windows-agents.md#download-the-agent-setup-file-from-oms).
2. Используйте один из следующих методов tooinstall hello и настроить hello агент на компьютере hello hello Configuration Manager роль точки подключения службы сайта системы:
   * [Установка агента hello, с помощью программы установки](log-analytics-windows-agents.md#install-the-agent-using-setup)
   * [Установка агента hello, с помощью командной строки hello](log-analytics-windows-agents.md#install-the-agent-using-the-command-line)
   * [Установка агента hello, с помощью DSC службы автоматизации Azure](log-analytics-windows-agents.md#install-the-agent-using-dsc-in-azure-automation)

## <a name="import-collections"></a>Импорт коллекций
После установленного агента hello и добавлены tooConfiguration подключение OMS Manager на компьютере hello подключения службы Configuration Manager hello роли системы сайта точки, hello следующим шагом является tooimport коллекций в Configuration Manager в OMS как группы компьютеров.

После включения импорта hello сведения о членстве в коллекции извлекается каждые 3 часа tookeep hello членство в коллекции текущего. Вы можете toodisable импорта в любое время.

1. На портале OMS hello щелкните **параметры**.
2. Нажмите кнопку hello **групп компьютеров** и нажмите кнопку hello **SCCM** вкладки.
3. Выберите **Импортировать членства в коллекциях Configuration Manager** и нажмите кнопку **Сохранить**.  
   ![Вкладка "SCCM" на вкладке "Группы компьютеров"](./media/log-analytics-sccm/sccm-computer-groups01.png)

## <a name="view-data-from-configuration-manager"></a>Просмотр данных из Configuration Manager
После добавлены tooConfiguration подключение OMS Manager и установки hello агента на компьютере hello hello Configuration Manager роль точки подключения службы сайта системы данные от агента hello отправляются tooOMS. В OMS коллекции из Configuration Manager будут отображаться как [группы компьютеров](log-analytics-computer-groups.md). Вы можете посмотреть группы hello из hello **Configuration Manager** в разделе **групп компьютеров** в **параметры**.

После hello коллекций будут импортированы можно увидеть, сколько компьютеров с помощью членства в коллекции обнаружено. Кроме того, вы увидите номер hello коллекций, которые были импортированы.

![Вкладка "SCCM" на вкладке "Группы компьютеров"](./media/log-analytics-sccm/sccm-computer-groups02.png)

Если щелкнуть любой из них, откроется поиска отображение либо все hello импортировать группы или для всех компьютеров, принадлежащих группе tooeach. С помощью [поиска по журналам](log-analytics-log-searches.md) можно выполнить подробный анализ данных Configuration Manager.

## <a name="next-steps"></a>Дальнейшие действия
* Используйте [поиска журналов](log-analytics-log-searches.md) tooview подробные сведения о данных Configuration Manager.
