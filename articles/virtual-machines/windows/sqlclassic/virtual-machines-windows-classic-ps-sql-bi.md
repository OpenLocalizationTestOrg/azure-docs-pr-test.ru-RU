---
title: "aaaSQL Server Business Intelligence | Документы Microsoft"
description: "В этом разделе использует ресурсы, созданные с помощью hello классической модели развертывания и описываются функции hello бизнес-аналитики (BI), доступные для SQL Server, работающий на виртуальных машинах Azure (ВМ)."
services: virtual-machines-windows
documentationcenter: na
author: guyinacube
manager: erikre
editor: monicar
tags: azure-service-management
ms.assetid: c681e7a7-eeda-48aa-bc35-6277f4828244
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/30/2017
ms.author: asaxton
ms.openlocfilehash: e3288f0835d6c4a19baeeea5f6b65fec16cd751f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="sql-server-business-intelligence-in-azure-virtual-machines"></a>Бизнес-аналитика SQL Server на виртуальных машинах Azure
> [!IMPORTANT] 
> В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../../../azure-resource-manager/resource-manager-deployment-model.md). В этой статье описан с помощью hello классической модели развертывания. Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов.

Галерея Hello виртуальной машине Microsoft Azure имеет образы, содержащие установки SQL Server. Здравствуйте, поддерживаются в образах коллекции hello выпуски SQL Server hello и те же файлы установки, можно установить tooon локальные компьютеры и виртуальные машины. В этом разделе обобщены hello SQL Server Business Intelligence (BI) компоненты, установленные на изображениях hello и шагов по настройке после подготовки виртуальной машины. Кроме того, в этом разделе описаны поддерживаемые топологии развертывания для компонентов бизнес-аналитики и рекомендации.

## <a name="license-considerations"></a>Рекомендации по лицензированию
Существует два способа toolicense SQL Server в виртуальных машинах Microsoft Azure.

1. Преимущества перемещения лицензий, предоставляемые в рамках программы Software Assurance. Дополнительные сведения см. в статье [Перемещение лицензий в рамках программы Software Assurance в Azure](https://azure.microsoft.com/pricing/license-mobility/).
2. Оплата виртуальных машин Azure с установленным SQL Server по часовой ставке. В разделе hello «SQL Server» в разделе [расценки на виртуальные машины](https://azure.microsoft.com/pricing/details/virtual-machines/#Sql).

Дополнительные сведения о лицензировании и текущих тарифах см. на странице [Виртуальные машины. Вопросы и ответы по лицензированию](https://azure.microsoft.com/pricing/licensing-faq/%20/).

## <a name="sql-server-images-available-in-azure-virtual-machine-gallery"></a>Образы SQL Server, доступные в коллекции виртуальных машин Azure
Коллекция виртуальных машин Microsoft Azure Hello содержит несколько образов, содержащих Microsoft SQL Server. Hello программного обеспечения, установленного на образы виртуальных машин hello различается в зависимости от версии hello hello операционной системы и hello версии SQL Server. список изображений, доступных в коллекции виртуальных машин Azure hello Hello часто меняется.

<!--![SQL image in azure VM gallery](./media/virtual-machines-windows-classic-ps-sql-bi/IC741367.png)-->
![Образ SQL в коллекции виртуальных машин Azure](./media/virtual-machines-windows-classic-ps-sql-bi/vm-sql-images.png)

![PowerShell](./media/virtual-machines-windows-classic-ps-sql-bi/IC660119.gif) Hello следующий сценарий PowerShell возвращает список hello Azure изображений, которые содержат «SQL Server» в hello ImageName.

    # assumes you have already uploaded a management certificate tooyour Microsoft Azure Subscription. View hello thumbprint value from hello "Subscriptions" menu in Azure portal.

    $subscriptionID = ""    # REQUIRED: Provide your subscription ID.
    $subscriptionName = "" # REQUIRED: Provide your subscription name.
    $thumbPrint = "" # REQUIRED: Provide your certificate thumbprint.
    $certificate = Get-Item cert:\currentuser\my\$thumbPrint # REQUIRED: If your certificate is in a different store, provide it here.-Ser  store is hello one specified with hello -ss parameter on MakeCert

    Set-AzureSubscription -SubscriptionName $subscriptionName -Certificate $certificate -SubscriptionID $subscriptionID

    Write-Host -foregroundcolor green "List of available gallery images where imagename contains 2016"
    Write-Host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
    get-azurevmimage | where {$_.ImageName -Like "*SQL-Server-2016*"} | select imagename,category, location, label, description

    Write-Host -foregroundcolor green "List of available gallery images where imagename contains 2014"
    Write-Host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
    get-azurevmimage | where {$_.ImageName -Like "*SQL-Server-2014*"} | select imagename,category, location, label, description

Дополнительные сведения о выпусках и функций, поддерживаемых SQL Server см. в следующем hello:

* [Выпуски SQL Server](https://www.microsoft.com/server-cloud/products/sql-server-editions/#fbid=Zae0-E6r5oh)
* [Поддерживаемые возможности по hello выпусками SQL Server 2016](https://msdn.microsoft.com/library/cc645993.aspx)

### <a name="bi-features-installed-on-hello-sql-server-virtual-machine-gallery-images"></a>Бизнес-Аналитики компоненты установлены на hello образах коллекции виртуальных машин SQL Server
Hello следующей таблице перечислены компоненты бизнес-аналитики hello, установленные на hello общих образах коллекции виртуальной машины Microsoft Azure для SQL Server:

* SQL Server 2016 SP1 Enterprise
* SQL Server 2016 SP1 Standard
* SQL Server 2014 SP2 Enterprise
* SQL Server 2014 SP2 Standard
* SQL Server 2012 SP3 Enterprise
* SQL Server 2012 SP3 Standard

| Компонент бизнес-аналитики SQL Server | Установить в образ коллекции hello | Примечания |
| --- | --- | --- |
| **Собственный режим служб Reporting Services** |Да |Установлен, но требуется настройка, включая URL-адрес диспетчера отчетов hello. В разделе hello [настройки служб Reporting Services](#configure-reporting-services). |
| **Режим SharePoint служб Reporting Services** |Нет |Hello коллекции образов виртуальных машин Microsoft Azure не включает SharePoint или SharePoint установочных файлов. <sup>1</sup> |
| **Многомерный и интеллектуальный анализ данных в службах Analysis Services (OLAP)** |Да |Экземпляр служб Analysis Services по умолчанию установлена и настроена как hello |
| **Табличный режим служб Analysis Services** |Нет |Поддерживается в образах SQL Server 2012, 2014 и 2016, но не устанавливается по умолчанию. Установите другой экземпляр служб Analysis Services. В разделе hello установка других служб SQL Server и компонентов в этом разделе. |
| **Power Pivot служб Analysis Services для SharePoint** |Нет |Hello коллекции образов виртуальных машин Microsoft Azure не включает SharePoint или SharePoint установочных файлов. <sup>1</sup> |

<sup>1</sup> Дополнительные сведения о SharePoint и виртуальных машинах Azure см. в статьях [Архитектуры Microsoft Azure для SharePoint 2013](https://technet.microsoft.com/library/dn635309.aspx) и [Развертывание SharePoint на виртуальных машинах Microsoft Azure](https://www.microsoft.com/download/details.aspx?id=34598).

![PowerShell](./media/virtual-machines-windows-classic-ps-sql-bi/IC660119.gif) Запустите hello, следующая команда tooget PowerShell список установленных служб, которые содержат «SQL» в имени службы hello.

    get-service | Where-Object{ $_.DisplayName -like '*SQL*' } | Select DisplayName, status, servicetype, dependentservices | format-Table -AutoSize

## <a name="general-recommendations-and-best-practices"></a>Общие рекомендации
* Hello минимальный рекомендуемый размер виртуальной машины — **A3** при использовании SQL Server Enterprise Edition. Hello **A4** размер виртуальной машины рекомендуется использовать для развертывания бизнес-Аналитики SQL Server Analysis Services и Reporting Services.
  
    Сведения о текущих размерах виртуальных Машин hello см. в разделе [размеры виртуальных машин для Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* Для управления дисками рекомендуется toostore данных, журнала и файлы резервной копии на дисках, отличных от **C**: и **D**:. Например, создайте диски данных **E:** и **F:**.
  
  * политика кэширования для диска по умолчанию hello диска Hello **C**: не является оптимальным выбором для работы с данными.
  * Hello **D**: диск является временным диском, который используется главным образом для файла подкачки hello. Hello **D**: не сохраняется и не сохраняется в хранилище больших двоичных объектов. Задачи управления, такие как изменение размера виртуальной машины toohello Сброс hello **D**: диск. Рекомендуется слишком**не** использовать hello **D**: диск для файлов базы данных, включая базы данных tempdb.
    
    Дополнительные сведения о создании и присоединении дисков см. в разделе [как tooAttach tooa диска данных виртуальной машины](../classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).
* Остановите или удалите службы, вы не планируете toouse. Пример Если hello виртуальной машины используется только для служб Reporting Services, остановить или удалить службы Analysis Services и SQL Server Integration Services. Hello следующем рисунке приведен пример hello служб, которые запускаются по умолчанию.
  
    ![Службы SQL Server](./media/virtual-machines-windows-classic-ps-sql-bi/IC650107.gif)
  
  > [!NOTE]
  > в сценарии hello поддерживается бизнес-Аналитики требуется Hello ядро СУБД SQL Server. В топологии ВМ одного сервера требуется hello СУБД toobe ОС hello одной виртуальной Машины.
  
    Дополнительные сведения см. в разделе ниже hello: [удаление служб Reporting Services](https://msdn.microsoft.com/library/hh479745.aspx) и [удалить экземпляр служб Analysis Services](https://msdn.microsoft.com/library/ms143687.aspx).
* Просмотрите раздел «Важные обновления» **Центра обновления Windows** . часто обновляются Hello образов виртуальной машины Microsoft Azure; Тем не менее важные обновления могут поступать из **центра обновления Windows** после последнего обновления образа виртуальной Машины hello.

## <a name="example-deployment-topologies"></a>Пример топологий развертывания
Hello ниже приведены примеры развертывания, использующих виртуальные машины Microsoft Azure. Hello топологии на этих диаграммах являются лишь некоторые hello возможных топологий, которые можно использовать с функциями бизнес-Аналитики SQL Server и виртуальные машины Microsoft Azure.

### <a name="single-virtual-machine"></a>Одна виртуальная машина
Службы Analysis Services, Reporting Services, ядро СУБД SQL Server и источники данных на одной виртуальной машине.

![сценарий бизнес-аналитики iass с 1 виртуальной машиной](./media/virtual-machines-windows-classic-ps-sql-bi/IC650108.gif)

### <a name="two-virtual-machines"></a>Две виртуальные машины
* Службы Analysis Services, службы Reporting Services и hello SQL Server Database Engine на одной виртуальной машины. Это развертывание включает hello баз данных сервера отчетов.
* Источники данных на второй виртуальной машине. Hello второй ВМ есть компонент SQL Server Database Engine в качестве источника данных.

![сценарий бизнес-аналитики iass с двумя виртуальными машинами](./media/virtual-machines-windows-classic-ps-sql-bi/IC650109.gif)

### <a name="mixed-azure--data-on-azure-sql-database"></a>Смешанная среда Azure — данные в базе данных SQL Azure
* Службы Analysis Services, службы Reporting Services и hello SQL Server Database Engine на одной виртуальной машины. Это развертывание включает hello баз данных сервера отчетов.
* Источником данных является база данных SQL Azure.

![сценарии бизнес-аналитики iaas с виртуальной машиной и AzureSQL в качестве источника данных](./media/virtual-machines-windows-classic-ps-sql-bi/IC650110.gif)

### <a name="hybrid-data-on-premises"></a>Гибридная среда — локальные данные
* В этом примере развертывания служб Analysis Services, Reporting Services и SQL Server Database Engine hello запустите на одной виртуальной машины. узлы виртуальных машин Hello hello баз данных сервера отчетов. Виртуальная машина Hello — присоединены к домену tooan локальному домену через виртуальную сеть Azure или некоторое другое тоннельное решение VPN.
* Источник данных находится в локальной среде.

![сценарии бизнес-аналитики IaaS с виртуальной машиной и локальными источниками данных](./media/virtual-machines-windows-classic-ps-sql-bi/IC654384.gif)

## <a name="reporting-services-native-mode-configuration"></a>Конфигурация собственного режима служб Reporting Services
Hello коллекции образов виртуальных машин для SQL Server включает в себя службы основной режим служб Reporting установлены, однако hello сервер отчетов не настроен. Hello шаги в этом разделе настроить сервер отчетов служб Reporting Services hello. Дополнительные сведения о настройке собственного режима служб Reporting Services см. в разделе [Установка сервера отчетов служб Reporting Services в основном режиме](https://msdn.microsoft.com/library/ms143711.aspx).

> [!NOTE]
> Аналогичное содержимое, который использует сервер отчетов hello tooconfigure сценариев Windows PowerShell, в разделе [tooCreate с помощью PowerShell Azure виртуальной Машины с сервером в собственном режиме отчета](../classic/ps-sql-report.md).

### <a name="connect-toohello-virtual-machine-and-start-hello-reporting-services-configuration-manager"></a>Подключение toohello виртуальной машине и запуск hello диспетчер конфигурации служб Reporting Services
Есть два распространенных рабочих процесса для подключения tooan виртуальной машине Azure:

* tooconnect в hello, щелкните имя hello hello виртуальной машины и нажмите кнопку **Connect**. Откроется удаленное подключение рабочего стола и имя компьютера hello заполняется автоматически.
  
    ![подключение tooazure виртуальной машины](./media/virtual-machines-windows-classic-ps-sql-bi/IC650112.gif)
* Подключите toohello виртуальную машину с помощью удаленного рабочего стола Windows. В пользовательском интерфейсе hello hello удаленного рабочего стола:
  
  1. Тип hello **имя облачной службы** как имя компьютера hello.
  2. Введите двоеточие (:) и hello номер общего порта, настроенного для hello удаленного рабочего стола конечной точки TCP.
     
      Моя_служба.облачное_приложение.net:63133
     
      Дополнительные сведения см. в статье с информацией об [облачной службе](https://azure.microsoft.com/manage/services/cloud-services/what-is-a-cloud-service/).


**Запуск диспетчера конфигурации служб Reporting Services**

В **Windows Server 2012 или Windows Server 2016** выполните следующие действия.

1. Из hello **запустить** введите **служб Reporting Services** toosee список приложений.
2. Щелкните правой кнопкой мыши элемент **Диспетчер конфигурации служб Reporting Services** и выберите пункт **Запуск от имени администратора**.

В **Windows Server 2008 R2**выполните следующие действия.

1. Нажмите кнопку **Пуск** и выберите **Все программы**.
2. Выберите пункт **Microsoft SQL Server 2016**.
3. Выберите **Средства настройки**.
4. Щелкните правой кнопкой мыши элемент **Диспетчер конфигурации служб Reporting Services** и выберите пункт **Запуск от имени администратора**.

Или сделайте так:

1. Нажмите **Запуск**.
2. В hello **найти программы и файлы** тип диалога **службы reporting services**. Если hello виртуальная машина работает под управлением Windows Server 2012, введите **службы reporting services** на Windows Server 2012 запустить экран приветствия.
3. Щелкните правой кнопкой мыши элемент **Диспетчер конфигурации служб Reporting Services** и выберите пункт **Запуск от имени администратора**.
   
    ![поиск диспетчера конфигурации служб ssrs](./media/virtual-machines-windows-classic-ps-sql-bi/IC650113.gif)

### <a name="configure-reporting-services"></a>Настройка служб Reporting Services
**Учетная запись службы и URL-адрес веб-службы:**

1. Проверьте hello **имя сервера** hello имя локального сервера и нажмите кнопку **Connect**.
2. Примечание hello пустой **имя базы данных сервера отчетов**. Hello базы данных создается после завершения настройки hello.
3. Проверьте hello **состояние сервера отчетов** — **Started**. Если требуется, чтобы служба tooverify hello в диспетчере сервера, служба hello не hello **SQL Server Reporting Services** службы Windows.
4. Нажмите кнопку **учетной записи службы** и при необходимости измените учетную запись hello. При использовании hello виртуальной машины в среде присоединены к домену недоменных hello встроенные **ReportServer** достаточно получить учетную запись. Дополнительные сведения об учетной записи службы hello см. в разделе [учетной записи службы](https://msdn.microsoft.com/library/ms189964.aspx).
5. Нажмите кнопку **URL веб-службы** hello левой панели.
6. Нажмите кнопку **применить** tooconfigure значения по умолчанию hello.
7. Примечание hello **URL службы сервера отчетов**. Обратите внимание, что TCP-порт по умолчанию hello равна 80 и является частью URL-адрес hello. На более позднем этапе создания конечной точки виртуальной машины Microsoft Azure для порта hello.
8. В hello **результатов** области Проверка hello действий успешно завершено.

**База данных:**

1. Нажмите кнопку **базы данных** hello левой панели.
2. Щелкните элемент **Изменение базы данных**.
3. Убедитесь, что выбран параметр **Создать новую базу данных сервера отчетов** , и нажмите кнопку «Далее».
4. Проверьте значение параметра **Имя сервера** и щелкните **Проверка соединения**.
5. Если результат hello **Проверка соединения завершилась успешно**, нажмите кнопку **ОК** и нажмите кнопку **Далее**.
6. Имя базы данных hello Примечание **ReportServer** и hello **режим сервера отчетов** — **собственного** щелкните **Далее**.
7. Нажмите кнопку **Далее** на hello **учетные данные** страницы.
8. Нажмите кнопку **Далее** на hello **Сводка** страницы.
9. Нажмите кнопку **Далее** на hello **ход выполнения и завершение** страницы.

**URL-адрес веб-портала или URL-адрес диспетчера отчетов для выпусков 2012 и 2014:**

1. Нажмите кнопку **URL-адрес портала**, или **URL-адрес диспетчера отчетов** для 2014 и 2012 hello левой панели.
2. Нажмите кнопку **Применить**.
3. В hello **результатов** области Проверка hello действий успешно завершено.
4. Щелкните **Выход**.

Сведения о разрешениях сервера отчетов см. в разделе [Предоставление разрешений на сервер отчетов в собственном режиме](https://msdn.microsoft.com/library/ms156014.aspx).

### <a name="browse-toohello-local-report-manager"></a>Обзор toohello локального диспетчера отчетов
Конфигурация tooverify hello, диспетчер tooreport обзора на hello виртуальной Машины.

1. На hello виртуальных Машин запустите Internet Explorer с правами администратора.
2. Обзор toohttp://localhost/reports на hello виртуальной Машины.

### <a name="tooconnect-tooremote-web-portal-or-report-manager-for-2014-and-2012"></a>tooConnect tooRemote веб-портале или в диспетчере отчетов для 2014 и 2012
Tooconnect toohello веб-портала или диспетчер отчетов для 2014 и 2012 на виртуальной машине hello с удаленного компьютера, создайте новую виртуальную машину конечной точки TCP. По умолчанию hello сервер отчетов слушает HTTP-запросы на **порт 80**. При настройке URL-адреса сервера toouse другой порт для hello отчета должны указывать этот номер порта в hello, следуя инструкциям.

1. Создайте конечную точку для виртуальной машины из TCP порт 80 hello. Дополнительные сведения см. в разделе, hello [конечных точек виртуальной машины и порты брандмауэра](#virtual-machine-endpoints-and-firewall-ports) настоящего документа.
2. Открытие порта 80 в брандмауэре hello виртуальной машины.
3. Обзор toohello веб-портала или диспетчера отчетов в виртуальных машинах Azure **DNS-имя** как hello имя сервера в URL-АДРЕСЕ hello. Например:
   
    **Сервер отчетов**: http://uebi.cloudapp.net/reportserver  **Веб-портал**: http://uebi.cloudapp.net/reports
   
    [Настройка брандмауэра для доступа к серверу отчетов](https://msdn.microsoft.com/library/bb934283.aspx)

### <a name="toocreate-and-publish-reports-toohello-azure-virtual-machine"></a>tooCreate и публиковать отчеты toohello виртуальной машине Azure
Hello следующей таблице перечислены некоторые hello параметры доступные toopublish существующие отчеты с сервера отчетов toohello компьютера в локальной среде, размещенной на виртуальной машине Microsoft Azure hello:

* **Построитель отчетов**: hello виртуальной машины включает щелкните hello-версии ClickOnce построителя отчетов Microsoft SQL Server для SQL 2014 и 2012. hello построителя отчетов toostart впервые hello виртуальную машину с SQL 2016:
  
  1. Запустите браузер с правами администратора.
  2. Обзор toohello веб-портала, на виртуальной машине hello и выбор hello **загрузки** значок в правом верхнем углу hello.
  3. Выберите **Построитель отчетов**.
     
     Дополнительные сведения см. в разделе [Запуск построителя отчетов](https://msdn.microsoft.com/library/ms159221.aspx).
* **SQL Server Data Tools**: виртуальной Машины: SQL Server Data Tools, установленной на виртуальной машине hello и может принимать используется toocreate **проектов сервера отчетов** и отчетов на виртуальной машине hello. SQL Server Data Tools можно опубликовать сервер отчетов toohello hello отчетов на виртуальной машине hello.
* **SQL Server Data Tools: удаленно**. Создайте на локальном компьютере проект служб Reporting Services в SQL Server Data Tools, содержащий отчеты служб Reporting Services. Настройте URL hello проекта tooconnect toohello веб-службы.
  
    ![свойства проекта SSDT для проекта SSRS](./media/virtual-machines-windows-classic-ps-sql-bi/IC650114.gif)
* Создать. Жесткий диск VHD, содержащий отчеты и затем передайте и присоедините диск hello.
  
  1. Создайте на локальном компьютере жесткий диск VHD, содержащий ваши отчеты.
  2. Создайте и установите сертификат управления.
  3. Отправка файла tooAzure hello виртуального жесткого диска, с помощью командлета Add-AzureVHD hello [Создание и отправка Windows Server VHD tooAzure](../classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).
  4. Подключите hello диск toohello виртуальной машине.

## <a name="install-other-sql-server-services-and-features"></a>Установка других служб и компонентов SQL Server
tooinstall дополнительных служб SQL Server, такие как службы Analysis Services в табличном режиме, запустите мастер установки SQL server hello. Hello установочные файлы находятся на локальном диске виртуальной машины hello.

1. Нажмите кнопку **Пуск** и выберите **Все программы**.
2. Щелкните **Microsoft SQL Server 2016**, **Microsoft SQL Server 2014** или **Microsoft SQL Server 2012**, а затем выберите **Средства настройки**.
3. Щелкните **Центр установки SQL Server**.

Либо запустите файл C:\SQLServer_13.0_full\setup.exe, C:\SQLServer_12.0_full\setup.exe или C:\SQLServer_11.0_full\setup.exe.

> [!NOTE]
> Здравствуйте, первый раз при запуске программы установки SQL Server, дополнительные настройки, файлы могут быть загружены и требуют перезагрузки hello виртуальной машины и перезапуск программы установки SQL Server.
> 
> Если вам требуется toorepeatedly настройки образа hello, выбранных из hello виртуальной машине Microsoft Azure, рекомендуется создать собственный образ SQL Server. Функциональные возможности SysPrep служб Analysis Services были включены в SQL Server 2012 SP1 CU2. Дополнительные сведения см. в разделах [Вопросы по установке SQL Server с помощью SysPrep](https://msdn.microsoft.com/library/ee210754.aspx) и [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles) (Поддержка ролей сервера в Sysprep).
> 
> 

### <a name="tooinstall-analysis-services-tabular-mode"></a>tooInstall табличном режиме Analysis Services
Hello шагов в этом разделе **суммировать** hello установки служб Analysis Services, Табличный режим. Дополнительные сведения см. в разделе hello следующее:

* [Установка служб Analysis Services в табличном режиме](https://msdn.microsoft.com/library/hh231722.aspx)
* [Табличное моделирование (руководство по Adventure Works)](https://msdn.microsoft.com/library/140d0b43-9455-4907-9827-16564a904268)

**tooInstall табличном режиме Analysis Services:**

1. В мастере установки SQL Server hello, нажмите кнопку **установки** в hello левой панели, а затем нажмите кнопку **автономная установка нового SQL server или добавление компонентов tooan существующей установки**.
   
   * Если вы видите hello **Обзор папок**, Обзор tooc:\SQLServer_13.0_full, c:\SQLServer_12.0_full или c:\SQLServer_11.0_full и нажмите кнопку **ОК**.
2. Нажмите кнопку **Далее** на странице обновления продукта hello.
3. На hello **тип установки** выберите **выполнить новую установку SQL Server** и нажмите кнопку **Далее**.
4. На hello **роль установки** щелкните **Установка компонентов SQL Server**.
5. На hello **Выбор компонентов** щелкните **служб Analysis Services**.
6. На hello **конфигурации экземпляра** введите описательное имя, например **табличный** в **именованный экземпляр** и **идентификатор экземпляра** текста поля.
7. На hello **конфигурация служб Analysis Services** выберите **табличном режиме**. Добавьте hello текущего пользователя toohello административные разрешения списка.
8. Завершите и закройте приветствия мастера установки SQL Server.

## <a name="analysis-services-configuration"></a>Настройка служб Analysis Services
### <a name="remote-access-tooanalysis-services-server"></a>TooAnalysis удаленного доступа сервер служб
Сервер служб Analysis Services поддерживает только проверку подлинности Windows. tooaccess служб Analysis Services, удаленный из клиентских приложений, например SQL Server Management Studio или SQL Server Data Tools, hello виртуальная машина требует toobe tooyour присоединены к домену локального домена, используя виртуальную сеть Azure. Дополнительные сведения см. в статье [Обзор виртуальной сети](../../../virtual-network/virtual-networks-overview.md).

**Экземпляр по умолчанию** служб Analysis Services прослушивает TCP-порт **2383**. Привет открыть порт в брандмауэре виртуальной машины hello. Порт **2383**прослушивается также кластеризованным именованным экземпляром служб Analysis Services.

Для **именованный экземпляр** служб Analysis Services, hello службы обозревателя SQL Server не требуется доступ к портам toomanage. Конфигурация по умолчанию Hello обозревателя SQL Server — порт **2382**.

Откройте порт в брандмауэре виртуальной машины hello, **2382** и статический порт именованного экземпляра служб Analysis.

1. tooverify порты, которые уже находятся в использовать hello ВМ и что процесс использует порты hello, запустите следующую команду с правами администратора hello:
   
        netstat /ao
2. Использование среды SQL Server Management Studio toocreate статических служб Analysis Services порт именованного экземпляра, обновив «Порт» значение в табличных AS общие свойства экземпляра. Дополнительные сведения см. в разделе hello «Использование фиксированного порта по умолчанию или именованного экземпляра» в [Настройка брандмауэра Windows hello tooAllow доступа к службам Analysis Services](https://msdn.microsoft.com/library/ms174937.aspx#bkmk_fixed).
3. Перезагрузите табличный экземпляр служб Analysis Services hello hello.

Дополнительные сведения см. в разделе, hello **конечных точек виртуальной машины и порты брандмауэра** настоящего документа.

## <a name="virtual-machine-endpoints-and-firewall-ports"></a>Конечные точки виртуальной машины и порты брандмауэра
В этом разделе приведена сводка tooopen toocreate и порты конечных точек виртуальной машины Microsoft Azure в брандмауэрах виртуальных машин hello. Hello следующей таблице приведена сводка hello **TCP** порты toocreate конечные точки и tooopen hello порты в брандмауэре виртуальной машины hello.

* Если вы используете одной виртуальной Машины и hello следующие два пункта верны, конечные точки ВМ toocreate не требуется и tooopen hello порты в брандмауэре hello hello виртуальной Машины не требуется.
  
  * Компоненты SQL Server toohello на hello виртуальной Машины не подключиться удаленно. Установление подключения удаленного рабочего стола toohello ВМ и доступа к функциям SQL Server hello локально на hello ВМ не считается компонентов SQL Server toohello удаленного подключения.
  * Вам не требуется присоединять hello ВМ tooan локальному домену через виртуальную сеть Azure или другое тоннельное решение VPN.
* Если виртуальная машина hello не присоединены к домену tooa домена, но требуется tooremotely подключение toohello компонентов SQL Server на виртуальной Машине:
  
  * Привет открыть порты в брандмауэре hello на hello виртуальной Машины.
  * Создание конечных точек виртуальной машины для hello указаны порты (*).
* Если виртуальная машина hello домен tooa присоединены к домену, с помощью VPN-туннель, например виртуальную сеть Azure, конечные точки hello не являются обязательными. Однако откройте hello порты в брандмауэре hello на hello виртуальной Машины.
  
  | Порт | Тип | Описание |
  | --- | --- | --- |
  | **80** |TCP |Удаленный доступ к серверу отчетов (*). |
  | **1433** |TCP |SQL Server Management Studio (*). |
  | **1434** |UDP |Обозреватель SQL Server. Это необходимо, когда hello виртуальных Машин в домене tooa присоединены к домену. |
  | **2382** |TCP |Обозреватель SQL Server. |
  | **2383** |TCP |Экземпляр SQL Server Analysis Services по умолчанию и кластеризованные именованные экземпляры. |
  | **Определяется пользователем** |TCP |Создайте статические служб Analysis Services порт именованного экземпляра для выбранного номера порта, а затем разблокируйте hello номер порта в брандмауэре hello. |

Дополнительные сведения о создании конечных точек см. в следующем hello:

* Создайте конечные точки:[как tooa tooSet Настройка конечных точек виртуальной машины](../classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).
* SQL Server: См. раздел «Завершить настройку действия tooconnect toohello виртуальная машина с помощью SQL Server Management Studio» hello [подготовки виртуальной машины SQL Server в Azure](../sql/virtual-machines-windows-portal-sql-server-provision.md).

Hello следующей схеме показано tooopen порты hello в hello toofeatures удаленного доступа tooallow брандмауэра виртуальной Машины и компоненты на hello виртуальной Машины.

![порты tooopen приложения бизнес-аналитики в виртуальных машинах Azure](./media/virtual-machines-windows-classic-ps-sql-bi/IC654385.gif)

## <a name="resources"></a>Ресурсы
* Просмотрите политику поддержки серверного программного обеспечения Майкрософт, используемых в среде виртуальной машины Azure hello hello. Hello разделе приведены сведения о поддержке для функции, такие как BitLocker, отказоустойчивой кластеризации и балансировки сетевой нагрузки. [Поддержка серверного программного обеспечения Майкрософт для виртуальных машин Azure](http://support.microsoft.com/kb/2721672).
* [Обзор. SQL Server на виртуальных машинах Azure](../sql/virtual-machines-windows-sql-server-iaas-overview.md)
* [Виртуальные машины](https://azure.microsoft.com/documentation/services/virtual-machines/)
* [Подготовка виртуальной машины SQL Server в Azure](../sql/virtual-machines-windows-portal-sql-server-provision.md)
* [Как tooAttach tooa диска данных виртуальной машины](../classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [Миграция базы данных tooSQL Server на Виртуальной машине Azure](../sql/virtual-machines-windows-migrate-sql.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json)
* [Определить hello режим сервера экземпляра служб Analysis Services](https://msdn.microsoft.com/library/gg471594.aspx)
* [Многомерное моделирование (руководство по Adventure Works)](https://technet.microsoft.com/library/ms170208.aspx)
* [Центр документации Azure](https://azure.microsoft.com/documentation/)
* [Использование Power BI в гибридной среде](https://msdn.microsoft.com/library/dn798994.aspx)

> [!NOTE]
> [Отправьте отзыв и контактные данные через Microsoft SQL Server Connect](https://connect.microsoft.com/SQLServer/Feedback)

### <a name="community-content"></a>Материалы сообщества
* [Управление базой данных SQL Azure с помощью PowerShell](http://blogs.msdn.com/b/windowsazure/archive/2013/02/07/windows-azure-sql-database-management-with-powershell.aspx)

