---
title: "Учебник группы доступности сервера - виртуальных машинах Azure - aaaSQL | Документы Microsoft"
description: "В этом учебнике показано как toocreate всегда на группы доступности SQL Server на виртуальных машинах Azure."
services: virtual-machines
documentationCenter: na
authors: MikeRayMSFT
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: 08a00342-fee2-4afe-8824-0db1ed4b8fca
ms.service: virtual-machines-sql
ms.devlang: na
ms.custom: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/09/2017
ms.author: mikeray
ms.openlocfilehash: 65b4210b0f851828a32a02053b03e4b8d469ba4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-always-on-availability-group-in-azure-vm-manually"></a>Настройка группы доступности AlwaysOn на виртуальной машине Azure вручную

В этом учебнике показано как toocreate всегда на группы доступности SQL Server на виртуальных машинах Azure. весь учебник Hello создается группа доступности с репликой базы данных на двух серверах SQL Server.

**Примерное время**: занимает около 30 минут toocomplete после hello предварительных условий.

Hello диаграмме построения в учебнике hello.

![Группа доступности](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/00-EndstateSampleNoELB.png)

## <a name="prerequisites"></a>Предварительные требования

Hello учебнике предполагается, что у вас есть базовое представление о SQL Server группы доступности AlwaysOn. Если вы хотите узнать больше, ознакомьтесь с разделом [Группы доступности AlwaysOn (SQL Server)](http://msdn.microsoft.com/library/ff877884.aspx).

Hello следующей таблице перечислены необходимые условия hello необходимые toocomplete перед запуском этого учебника.

|  |Требование |Описание |
|----- |----- |----- |
|![Маркер](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png) | Два сервера SQL Server | В группе доступности Azure. <br/> В отдельном домене. <br/> С установленным компонентом отказоустойчивой кластеризации. |
|![Маркер](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)| Windows Server | Файловый ресурс для свидетеля кластера. |  
|![Маркер](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|Учетная запись службы SQL Server | Доменная учетная запись. |
|![Маркер](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|Учетная запись службы агента SQL Server | Доменная учетная запись. |  
|![Маркер](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|Открытые порты брандмауэра | SQL Server: порт **1433** для экземпляра по умолчанию. <br/> Конечная точка зеркального отображения базы данных: порт **5022** или любой доступный порт. <br/> Проба Azure Load Balancer: порт **59999** или любой доступный порт. |
|![Маркер](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|Добавление компонента отказоустойчивой кластеризации | Этот компонент нужен на обоих серверах SQL Server. |
|![Маркер](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|Доменная учетная запись для установки | Локальный администратор на каждом сервере SQL Server. <br/> Участник фиксированной роли сервера SQL Server sysadmin для каждого экземпляра SQL Server.  |


Перед началом hello учебника необходимо слишком[выполните предварительные требования для создания группы доступности AlwaysOn в виртуальных машинах Azure](virtual-machines-windows-portal-sql-availability-group-prereq.md). Если эти условия являются уже завершена, можно легко слишком[создания кластеров](#CreateCluster).


<!--**Procedure**: *This is hello first “step”. Make titles H2’s and short and clear – H2’s appear in hello right pane on hello web page and are important for navigation.*-->

<a name="CreateCluster"></a>
##Создание кластера hello

После приветствия необходимые условия выполнены hello первым шагом является toocreate отказоустойчивый кластер Windows Server с двумя серверами SQL Sever и следящего сервера.  

1. RDP toohello первого SQL Server, используя учетную запись домена с правами администратора на серверах SQL и hello следящий сервер.

   >[!TIP]
   >Если вы следовали hello [документ необходимых компонентов](virtual-machines-windows-portal-sql-availability-group-prereq.md), вы создали учетную запись называется **CORP\Install**. Используйте ее.

2. В hello **диспетчера сервера** панели мониторинга, выберите **средства**, а затем нажмите кнопку **Диспетчер отказоустойчивости кластеров**.
3. Hello левой панели щелкните правой кнопкой мыши **Диспетчер отказоустойчивости кластеров**, а затем нажмите кнопку **создать кластер**.
   ![Создание кластера](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/40-createcluster.png)
4. В hello мастера создания кластера, создайте кластер с одним узлом, настроив hello страницы с параметрами hello в hello в следующей таблице:

   | Страница | Параметры |
   | --- | --- |
   | Перед началом работы |По умолчанию |
   | Выбор серверов |Тип hello, имя первого SQL Server в **введите имя сервера** и нажмите кнопку **добавить**. |
   | Предупреждение проверки |Выберите **проверяет, но мне не требуется поддержка Майкрософт для этого кластера, а не требуется проверка toorun hello. После нажатия кнопки Далее продолжить создание кластера hello**. |
   | Точка доступа для hello администрирование кластера |Введите имя кластера, например **SQLAGCluster1**, в поле **Имя кластера**.|
   | Подтверждение |Используйте параметры по умолчанию, если вы не используете дисковые пространства. См. Примечание hello после этой таблицы. |

### <a name="set-hello-cluster-ip-address"></a>Настройка IP-адреса кластера hello

1. В **Диспетчер отказоустойчивости кластеров**, прокрутите вниз слишком**основные ресурсы кластера** и разверните hello сведения о кластере. Вы увидите обоих hello **имя** и hello **IP-адрес** ресурсы hello **сбой** состояния. Hello ресурс IP-адреса не удается подключить из-за hello кластеру назначен hello же IP-адрес как самой машины hello, поэтому очень повторяющийся адрес.

2. Щелкните правой кнопкой мыши hello сбой **IP-адрес** ресурсов, а затем щелкните **свойства**.

   ![Свойства кластера](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/42_IPProperties.png)

3. Выберите **статический IP-адрес** и укажите доступный адрес из подсети, где hello SQL Server в текстовом поле адрес hello. Затем нажмите кнопку **ОК**.
4. В hello **основные ресурсы кластера** щелкните правой кнопкой мыши имя кластера, щелкните **перевести в оперативный режим**. Подождите, пока оба ресурса будут подключены. Когда ресурс имени кластера hello станет доступной, hello сервер DC обновится новой учетной записи компьютера AD. Используйте этот AD hello toorun учетной записи службы кластерные группы доступности в более поздней версии.

### <a name="addNode"></a>Добавить hello других toocluster SQL Server

Добавить hello других toohello кластера SQL Server.

1. В дереве обозревателя hello, щелкните правой кнопкой мыши кластер hello и нажмите кнопку **добавления узла**.

    ![Добавить toohello узла кластера](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/44-addnode.png)

1. В hello **мастер добавления узла**, нажмите кнопку **Далее**. В hello **Выбор серверов** добавьте hello второго SQL Server. Имя сервера типа hello в **введите имя сервера** и нажмите кнопку **добавить**. Когда будете готовы, нажмите кнопку **Далее**.

1. В hello **предупреждение проверки** щелкните **нет** (в рабочем сценарии необходимо выполнить проверочные тесты hello). Затем щелкните **Далее**.

8. В hello **Подтверждение** страницы при использовании дисковых пространств, hello снимите флажок **Добавление всех допустимых хранилищ toohello кластера.**

   ![Подтверждение добавления узла](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/46-addnodeconfirmation.png)

    >[!WARNING]
   >Если вы используете дисковые пространства и не снимите флажок **Добавление всех допустимых хранилищ toohello кластера**, Windows hello виртуальные диски отсоединяет во время процесса кластеризации hello. В результате они не отображаются в диспетчере дисков или проводнике только после удаления из кластера hello hello дисковых пространств и повторно подключены с помощью PowerShell. Дисковые пространства группируют несколько дисков в пулы toostorage. Дополнительные сведения см. в статье [Обзор дисковых пространств](https://technet.microsoft.com/library/hh831739).

1. Щелкните **Далее**.

1. Нажмите кнопку **Готово**

   Диспетчер отказоустойчивости кластеров показывает, что кластер имеет новый узел и указанный в hello **узлы** контейнера.

10. Выйдите из сеанса удаленного рабочего стола hello.

### <a name="add-a-cluster-quorum-file-share"></a>Добавление файлового ресурса кворума кластера

В этом примере кластера Windows hello использует файл общего ресурса toocreate кворума кластера. В этом руководстве используется кворум "Большинство узлов и общих файловых ресурсов". Дополнительные сведения см. в разделе [Общее представление о конфигурациях кворума в отказоустойчивом кластере](http://technet.microsoft.com/library/cc731739.aspx).

1. Подключите следящий сервер toohello файл общий ресурс элемента с сеанс удаленного рабочего стола.

1. В **диспетчере сервера** щелкните **Инструменты**. Щелкните **Управление компьютером**.

1. Щелкните **Общие папки**.

1. Щелкните правой кнопкой мыши **Общие ресурсы** и выберите **Создать папку…**.

   ![Новый общий ресурс](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/48-newshare.png)

   Используйте **общих мастер создания папки** toocreate общую папку.

1. На **путь к папке**, нажмите кнопку **Обзор** и найдите или создайте путь к общей папке hello. Щелкните **Далее**.

1. В **имя, описание и параметры** проверьте hello сетевое имя и путь. Щелкните **Далее**.

1. В окне **Разрешения для общей папки** выберите **Настройка разрешений доступа**. Щелкните **Настраиваемые…**.

1. В окне **Настройка разрешений доступа** нажмите кнопку **Добавить**.

1. Убедитесь, что данный кластер hello hello toocreate учетная запись, используемая имеет полный доступ.

   ![Новый общий ресурс](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/50-filesharepermissions.png)

1. Нажмите кнопку **ОК**.

1. В окне **Разрешения для общей папки** нажмите кнопку **Готово**. Еще раз нажмите кнопку **Готово**.  

1. Выйдите из сервера hello

### <a name="configure-cluster-quorum"></a>Настройка кворума кластера

Затем задайте hello кворума кластера.

1. Первый узел кластера toohello подключения удаленного рабочего стола.

1. В **Диспетчер отказоустойчивости кластеров**, щелкните правой кнопкой мыши кластер hello, откройте пункт слишком**дополнительные действия**и нажмите кнопку **настроить параметры кворума кластера...** .

   ![Новый общий ресурс](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/52-configurequorum.png)

1. В **мастере настройки кворума кластера** нажмите кнопку **Далее**.

1. В **Выбор параметра конфигурации кворума**, выберите **Выбор свидетеля кворума hello**и нажмите кнопку **Далее**.

1. В окне **Выбрать свидетель кворума** щелкните **Настроить файловый ресурс-свидетель**.

   >[!TIP]
   >Windows Server 2016 поддерживает облако-свидетель. При выборе этого типа свидетеля файловый ресурс-свидетель не требуется. Дополнительные сведения см. в разделе [Развертывание облачного следящего сервера для отказоустойчивого кластера](http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness). В этом руководстве используется файловый ресурс-свидетель, который поддерживается в предыдущих операционных системах.

1. На **Настройка файлового ресурса-свидетеля**, тип hello путь к общей папке hello, вы создали. Щелкните **Далее**.

1. Проверьте параметры hello на **Подтверждение**. Щелкните **Далее**.

1. Нажмите кнопку **Готово**

Основные ресурсы кластера Hello настроены файловый ресурс-свидетель.

## <a name="enable-availability-groups"></a>Включение групп доступности

Затем включите hello **группы доступности AlwaysOn** компонентов. Выполните эти шаги для обоих серверов SQL Server.

1. Из hello **запустить** экрана, запустить **диспетчер конфигурации SQL Server**.
2. В дереве обозревателя hello выберите **служб SQL Server**, щелкните правой кнопкой мыши hello **SQL Server (MSSQLSERVER)** службы и нажмите кнопку **свойства**.
3. Нажмите кнопку hello **высокий уровень доступности AlwaysOn** , затем выберите **включить группы доступности AlwaysOn**, как показано ниже:

    ![Включение групп доступности AlwaysOn](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/54-enableAlwaysOn.png)

4. Нажмите кнопку **Применить**. Нажмите кнопку **ОК** в всплывающем диалоговом окне приветствия.

5. Перезапустите службу SQL Server hello.

Повторите эти действия на hello другие серверы SQL Server.

<!-----------------
## <a name="endpoint-firewall"></a>Open firewall for hello database mirroring endpoint

Each instance of SQL Server that participates in an Availability Group requires a database mirroring endpoint. This endpoint is a TCP port for hello instance of SQL Server that is used toosynchronize hello database replicas in hello Availability Groups on that instance.

On both SQL Servers, open hello firewall for hello TCP port for hello database mirroring endpoint.

1. On hello first SQL Server **Start** screen, launch **Windows Firewall with Advanced Security**.
2. In hello left pane, select **Inbound Rules**. On hello right pane, click **New Rule**.
3. For **Rule Type**, choose **Port**.
1. For hello port, specify TCP and choose an unused TCP port number. For example, type *5022* and click **Next**.

   >[!NOTE]
   >For this example, we're using TCP port 5022. You can use any available port.

5. In hello **Action** page, keep **Allow hello connection** selected and click **Next**.
6. In hello **Profile** page, accept hello default settings and click **Next**.
7. In hello **Name** page, specify a rule name, such as **Default Instance Mirroring Endpoint** in hello **Name** text box, then click **Finish**.

Repeat these steps on hello second SQL Server.
-------------------------->

## <a name="create-a-database-on-hello-first-sql-server"></a>Создание базы данных на hello первого SQL Server

1. Запустите RDP hello файл toohello первого SQL Server в домене учетной записи, то есть членом роли sysadmin предопределенной роли сервера.
1. Откройте среду SQL Server Management Studio и подключитесь toohello первого SQL Server.
7. В **обозревателе объектов** щелкните правой кнопкой мыши **Базы данных** и выберите пункт **Новая база данных**.
8. В поле **Имя базы данных** введите **MyDB1**, а затем нажмите кнопку **ОК**.

### <a name="backupshare"></a>Создание общего ресурса для резервных копий

1. На hello первого SQL Server в **диспетчера сервера**, нажмите кнопку **средства**. Щелкните **Управление компьютером**.

1. Щелкните **Общие папки**.

1. Щелкните правой кнопкой мыши **Общие ресурсы** и выберите **Создать папку…**.

   ![Новый общий ресурс](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/48-newshare.png)

   Используйте **общих мастер создания папки** toocreate общую папку.

1. На **путь к папке**, нажмите кнопку **Обзор** и найдите или создайте путь к общей папке с резервной копии hello базы данных. Щелкните **Далее**.

1. В **имя, описание и параметры** проверьте hello сетевое имя и путь. Щелкните **Далее**.

1. В окне **Разрешения для общей папки** выберите **Настройка разрешений доступа**. Щелкните **Настраиваемые…**.

1. В окне **Настройка разрешений доступа** нажмите кнопку **Добавить**.

1. Убедитесь, что hello SQL Server и агент SQL Server учетные записи служб для обоих серверов имеют полный доступ.

   ![Новый общий ресурс](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/68-backupsharepermission.png)

1. Нажмите кнопку **ОК**.

1. В окне **Разрешения для общей папки** нажмите кнопку **Готово**. Еще раз нажмите кнопку **Готово**.  

### <a name="take-a-full-backup-of-hello-database"></a>Создайте полную резервную копию базы данных hello

Необходимо tooback копирование hello новую базу данных tooinitialize hello цепочку журналов. Если резервная копия hello новой базы данных не выполняется, он не включен в группу доступности.

1. В **обозревателя объектов**щелкните hello базы данных, укажите слишком**задач...** , нажмите кнопку **резервное копирование**.

1. Нажмите кнопку **ОК** tootake местоположение резервных копий по умолчанию toohello полного резервного копирования.

## <a name="create-hello-availability-group"></a>Создание группы доступности hello
Теперь будут готовы tooconfigure, группу доступности с помощью hello следующие шаги:

* Создание базы данных на hello первого SQL Server.
* Отключите полной резервной копии и резервной копии журнала транзакций базы данных hello
* Hello восстановление полной и второй сервер SQL с hello toohello резервные копии журналов **NORECOVERY** параметр
* Создание группы доступности hello (**AG1**) с синхронной фиксацией, автоматической отработки отказа и вторичные реплики для чтения

### <a name="create-hello-availability-group"></a>Создание группы доступности hello:

1. В сеансе удаленного рабочего стола toohello первого SQL Server. В **обозревателе объектов** в SSMS щелкните правой кнопкой мыши **Высокая доступность AlwaysOn** и выберите пункт **Мастер создания групп доступности**.

    ![Запуск мастера создания групп доступности](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/56-newagwiz.png)

2. В hello **Введение** щелкните **Далее**. В hello **Указание имени группы доступности** введите имя для hello группы доступности, например **AG1**в **имя группы доступности**. Щелкните **Далее**.

    ![Мастер создания групп доступности, ввод имени групп доступности](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/58-newagname.png)

3. В hello **Выбор баз данных** , выберите вашу базу данных и нажмите кнопку **Далее**.

   >[!NOTE]
   >Hello базы данных предварительным требованиям hello для группы доступности из-за выполнения по крайней мере одну полную резервную копию на hello целевой первичной реплики.

   ![Мастер создания групп доступности, выбор баз данных](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/60-newagselectdatabase.png)
4. В hello **Выбор реплик** щелкните **добавления реплики**.

   ![Мастер создания групп доступности, указание реплик](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/62-newagaddreplica.png)
5. Hello **подключения tooServer** появится диалоговое окно. Имя типа hello hello второго сервера в **имя сервера**. Щелкните **Подключить**.

   Вернитесь в hello **Выбор реплик** страницы, вы увидите hello второго сервера, перечисленные в **реплик доступности**. Настройте hello реплики следующим образом.

   ![Мастер создания групп доступности, указание реплик (завершено)](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/64-newagreplica.png)

6. Нажмите кнопку **конечные точки** toosee hello конечную точку зеркального отображения для этой группы доступности. Используйте hello же порт использовался при установке hello [правило брандмауэра для конечных точек зеркального отображения базы данных](virtual-machines-windows-portal-sql-availability-group-prereq.md#endpoint-firewall).

    ![Мастер создания групп доступности, выбор начальной синхронизации данных](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/66-endpoint.png)

8. В hello **Выбор начальной синхронизации данных** выберите **полного** и укажите общую сетевую папку. Для расположения hello использовать hello [резервном ресурсе, который вы создали](#backupshare). В примере hello, он был **\\\\\<первого SQL Server\>\Backup\**. Щелкните **Далее**.

   >[!NOTE]
   >Полная синхронизация принимает полную резервную копию базы данных hello на hello первого экземпляра SQL Server и его восстановления toohello второй экземпляр. Полная синхронизация не рекомендуется для больших баз данных, так как может занимать много времени. Это время можно уменьшить, вручную создается резервная копия базы данных hello и их восстановление с `NO RECOVERY`. Если база данных hello уже восстановлена с `NO RECOVERY` на hello второй сервер SQL перед настройкой hello группы доступности, выберите **только присоединение**. Резервное копирование hello tootake после настройки hello группы доступности, выберите **пропустить начальную синхронизацию данных**.

    ![Мастер создания групп доступности, выбор начальной синхронизации данных](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/70-datasynchronization.png)

9. В hello **проверки** щелкните **Далее**. Эта страница должна выглядеть примерно toohello после изображения:

    ![Мастер создания групп доступности, проверка](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/72-validation.png)

    >[!NOTE]
    >Имеется предупреждение для конфигурации прослушивателя hello, так как вы не настроили прослушиватель группы доступности. Можно игнорировать это предупреждение, поскольку на виртуальных машинах Azure создать прослушиватель hello после создания hello балансировки нагрузки Azure.

10. В hello **Сводка** щелкните **Готово**, а затем подождите, пока мастер hello настраивает hello новой группы доступности. В hello **выполняется** страницы, можно щелкнуть **Дополнительные сведения о** tooview hello подробные хода выполнения. После завершения работы мастера hello, проверять hello **результатов** tooverify страницы, hello группа доступности успешно создана.

     ![Мастер создания групп доступности, результаты](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/74-results.png)
11. Нажмите кнопку **закрыть** tooexit приветствия мастера.

### <a name="check-hello-availability-group"></a>Проверьте hello группы доступности

1. В **обозревателе объектов** разверните элемент **Высокая доступность AlwaysOn**, а затем — элемент **Группы доступности**. Теперь вы увидите hello новой группы доступности в этом контейнере. Щелкните правой кнопкой мыши hello группы доступности и нажмите кнопку **Показать панель мониторинга**.

   ![Отображение панели мониторинга группы доступности](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/76-showdashboard.png)

   Ваш **панели мониторинга AlwaysOn** должен выглядеть примерно toothis.

   ![Панель мониторинга группы доступности](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/78-agdashboard.png)

   Вы увидите реплики hello, режим отработки отказа hello каждого состояния синхронизации реплики и hello.

2. В **диспетчере отказоустойчивости кластеров** щелкните свой кластер. Выберите **Роли**. Имя группы доступности Hello, которая использовалась — это роль в кластере hello. Так как вы не настроили прослушиватель, у этой группы доступности нет IP-адреса для подключений клиентов. После создания балансировки нагрузки Azure, вы настроите hello прослушивателя.

   ![Группа доступности в диспетчере отказоустойчивости кластеров](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/80-clustermanager.png)

   > [!WARNING]
   > Не предпринимайте toofail через hello группы доступности из hello диспетчера отказоустойчивости кластеров. Все операции отработки отказов следует выполнять через **панель мониторинга AlwaysOn** в SSMS. Дополнительные сведения см. в разделе [ограничения на использование hello Диспетчер отказоустойчивости кластеров с группами доступности](https://msdn.microsoft.com/library/ff929171.aspx).
    >

На этом этапе имеется группа доступности с репликами в двух экземплярах SQL Server. Hello группы доступности можно перемещать между экземплярами. Не удается подключиться toohello группы доступности еще, так как у вас прослушивателя. В виртуальных машинах Azure hello прослушивателя необходимо подсистемы балансировки нагрузки. Hello следующим шагом является toocreate hello подсистемы балансировки нагрузки в Azure.

<a name="configure-internal-load-balancer"></a>

## <a name="create-an-azure-load-balancer"></a>Создание Azure Load Balancer

Для группы доступности SQL Server на виртуальных машинах Azure необходима подсистема балансировки нагрузки. Подсистема балансировки нагрузки Hello содержит hello IP-адрес для прослушивателя группы доступности hello. В этом разделе перечислены как toocreate hello Подсистема балансировки загрузки в hello портал Azure.

1. В hello портал Azure, перейдите в группу ресурсов toohello где экземпляры SQL Server и нажмите кнопку **+ добавить**.
2. Найдите **балансировщик нагрузки**. Выберите подсистемы балансировки нагрузки hello, опубликованные корпорацией Майкрософт.

   ![Группа доступности в диспетчере отказоустойчивости кластеров](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/82-azureloadbalancer.png)

1.  Щелкните **Создать**.
3. Настройте следующие параметры для балансировки нагрузки hello hello.

   | Настройка | Поле |
   | --- | --- |
   | **Имя** |Используйте имя текст hello балансировки нагрузки, например **sqlLB**. |
   | **Тип** |Внутренний |
   | **Виртуальная сеть** |Используйте имя hello hello виртуальной сети Azure. |
   | **Подсеть** |Используйте имя hello hello подсети, hello виртуальной машины находится в.  |
   | **Назначение IP-адресов** |Статическое |
   | **IP-адрес** |Используйте доступный адрес из подсети. |
   | **Подписка** |Используйте hello же подписке, что hello виртуальной машины. |
   | **Расположение** |Используйте hello же расположении, что hello виртуальной машины. |

   Hello Azure — колонка портала должен выглядеть следующим образом:

   ![Создание балансировщика нагрузки](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/84-createloadbalancer.png)

1. Нажмите кнопку **создать**, балансировки нагрузки toocreate hello.

Подсистема балансировки нагрузки hello tooconfigure, необходимо toocreate внутреннего пула, проверки и набор правил балансировки нагрузки, hello. Выполните следующие действия в hello портал Azure.

### <a name="add-backend-pool"></a>Добавление внутреннего пула

1. В hello портал Azure перейдите tooyour группы доступности. Может потребоваться только что созданный hello toorefresh hello представление toosee балансировки нагрузки.

   ![Поиск подсистемы балансировки нагрузки в группе ресурсов](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/86-findloadbalancer.png)

1. Выберите hello подсистему балансировки нагрузки, нажмите кнопку **внутренние пулы**и нажмите кнопку **+ добавить**. Задайте hello внутренний пул следующим образом:

   | Настройка | Описание | Пример
   | --- | --- |---
   | **Имя** | Введите текстовое имя. | SQLLBBE
   | **Сопоставлено с** | Выберите из списка | Группа доступности
   | **группа доступности;** | Используйте имя набора доступности hello, что виртуальные машины SQL Server находятся в | sqlAvailabilitySet |
   | **Виртуальные машины** |Здравствуйте, два имени виртуальной Машины сервера SQL Azure | sqlserver-0, sqlserver-1

1. Введите имя пула серверной части hello hello.

1. Щелкните **+ Добавить виртуальную машину**.

1. Для группы доступности hello выберите группу доступности hello, hello, в которых находятся серверы SQL Server.

1. Для виртуальных машин включают оба hello серверов SQL Server. Не включайте hello файл общей папке следящего сервера.

1. Нажмите кнопку **ОК** toocreate hello внутренний пул.

### <a name="set-hello-probe"></a>Зонд hello наборов

1. Выберите hello подсистему балансировки нагрузки, нажмите кнопку **зонды работоспособности**и нажмите кнопку **+ добавить**.

1. Настройте пробу работоспособности hello следующим образом:

   | Настройка | Описание | Пример
   | --- | --- |---
   | **Имя** | текст | SQLAlwaysOnEndPointProbe |
   | **Протокол** | Выберите протокол TCP. | TCP |
   | **Порт** | Любой неиспользуемый порт. | 59999 |
   | **Интервал**  | пытается Hello промежуток времени между проверки в секундах |5 |
   | **Пороговое значение сбоя** | число последовательных сбоев пробы, которое должно происходить для виртуальной машины toobe, считаются неисправное Hello  | 2 |

1. Нажмите кнопку **ОК** проверки работоспособности tooset hello.

### <a name="set-hello-load-balancing-rules"></a>Задайте правила подсистемы балансировки нагрузки hello

1. Выберите hello подсистему балансировки нагрузки, нажмите кнопку **правила подсистемы балансировки нагрузки**и нажмите кнопку **+ добавить**.

1. Задайте следующим правила балансировки нагрузки hello.
   | Настройка | Описание | Пример
   | --- | --- |---
   | **Имя** | текст | SQLAlwaysOnEndPointListener |
   | **Frontend IP address** (Интерфейсный IP-адрес) | Выберите адрес. |Используйте адрес hello, созданный при создании hello подсистемы балансировки нагрузки. |
   | **Протокол** | Выберите протокол TCP. |TCP |
   | **Порт** | Использовать hello порт для экземпляра SQL Server hello | 1433 |
   | **Серверный порт** | Это поле не используется, если задан плавающий IP-адрес для прямого ответа от сервера. | 1433 |
   | **Проба** |Hello имя, указанное для пробы hello | SQLAlwaysOnEndPointProbe |
   | **Сохранение сеанса** | Раскрывающийся список. | **None** |
   | **Время ожидания простоя** | Откройте TCP-подключение tookeep минут | 4. |
   | **Плавающий IP-адрес (прямой ответ от сервера)** | |Включено |

   > [!WARNING]
   > Параметры прямого ответа от сервера задаются во время создания. Их невозможно изменить.

1. Нажмите кнопку **ОК** правила подсистемы балансировки нагрузки tooset hello.

## <a name="configure-listener"></a>Настройте прослушиватель hello

Далее самое toodo Hello — tooconfigure прослушивателя группы доступности в отказоустойчивом кластере hello.

> [!NOTE]
> В этом учебнике показано, как toocreate прослушиватель один - один ILB IP-адресов. один или несколько прослушивателей, с помощью одного или нескольких IP-адресов в разделе toocreate [прослушивателя Создание группы доступности и балансировки нагрузки | Azure](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
>
>

[!INCLUDE [ag-listener-configure](../../../../includes/virtual-machines-ag-listener-configure.md)]

## <a name="set-listener-port"></a>Настройка порта прослушивателя

В SQL Server Management Studio установите hello прослушиваемый порт.

1. Запустите SQL Server Management Studio и подключитесь toohello первичной реплики.

1. Перейдите в слишком**высокий уровень доступности AlwaysOn** | **группы доступности** | **прослушиватели группы доступности**.

1. Теперь вы увидите имя прослушивателя hello, созданный в диспетчере отказоустойчивости кластеров. Щелкните правой кнопкой мыши имя прослушивателя hello и нажмите кнопку **свойства**.

1. В hello **порт** укажите hello номер порта для прослушивателя группы доступности hello $EndpointPort ранее с помощью hello (по умолчанию hello — 1433), затем нажмите кнопку **ОК**.

Теперь у вас есть группа доступности SQL Server на виртуальных машинах Azure в режиме Resource Manager.

## <a name="test-connection-toolistener"></a>Toolistener тестирования подключения

подключение к tootest hello:

1. Tooa RDP сервера SQL в hello виртуальных сетевых, но не собственные hello реплики. Можно использовать другие серверы SQL Server в кластере hello hello.

1. Используйте **sqlcmd** программа tootest hello соединения. Например, следующий скрипт hello устанавливает **sqlcmd** toohello первичной подключения через прослушиватель hello с проверкой подлинности Windows:

    ```
    sqlcmd -S <listenerName> -E
    ```

    Если прослушиватель hello не использует порт hello по умолчанию порт (1433), укажите порт hello в строке подключения hello. Например hello следующие команды sqlcmd подключается tooa прослушивания по порту 1435:

    ```
    sqlcmd -S <listenerName>,1435 -E
    ```

Hello SQLCMD подключения автоматически подключается toowhichever экземпляра SQL Server узлов hello первичной реплики.

> [!TIP]
> Убедитесь, что открыт порт hello, указываемые на брандмауэре hello и серверов SQL. Оба сервера требуют входящее правило для hello TCP-порт, который можно использовать. Дополнительные сведения см. в статье [Добавление и изменение правила брандмауэра](http://technet.microsoft.com/library/cc753558.aspx).
>
>



<!--**Notes**: *Notes provide just-in-time info: A Note is “by hello way” info, an Important is info users need toocomplete a task, Tip is for shortcuts. Don’t overdo*.-->


<!--**Procedures**: *This is hello second “step." They often include substeps. Again, use a short title that tells users what they’ll do*. *("Configure a new web project.")*-->

<!--**UI**: *Note hello format for documenting hello UI: bold for UI elements and arrow keys for sequence. (Ex. Click **File > New > Project**.)*-->

<!--**Screenshot**: *Screenshots really help users. But don’t include too many since they’re difficult toomaintain. Highlight areas you are referring tooin red.*-->

<!--**No. of steps**: *Make sure hello number of steps within a procedure is 10 or fewer. Seven steps is ideal. Break up long procedure logically.*-->


<!--**Next steps**: *Reiterate what users have done, and give them interesting and useful next steps so they want toogo on.*-->

## <a name="next-steps"></a>Дальнейшие действия

- [Добавление IP адрес tooa подсистемы балансировки нагрузки для второй группы доступности](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md#Add-IP).
