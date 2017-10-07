---
title: "базы данных aaaUsing SQL стек Azure | Документы Microsoft"
description: "Дополнительные сведения о развертывании баз данных SQL как служба в Azure стека и hello hello toodeploy Быстрые действия SQL Server адаптер поставщика ресурсов"
services: azure-stack
documentationCenter: 
author: JeffGoldner
manager: bradleyb
editor: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: JeffGo
ms.openlocfilehash: 01418ce7cd708ca8f9e302d6bcd2a43ad33df93f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-sql-databases-on-microsoft-azure-stack"></a>Использование баз данных SQL Microsoft Azure стеке


Используйте hello ресурсов поставщика адаптера tooexpose SQL базы данных SQL Server в качестве службы Azure стека. После установки поставщика ресурсов hello и подключите его tooone или более экземпляров SQL Server, вас и ваших пользователей можно создавать базы данных для рабочих нагрузок, основанных на SQL без необходимости виртуальной tooprovision, облако в собственном коде приложений и веб-сайтов, которые основаны на SQL машины (VM), на котором размещается SQL Server каждый раз.

поставщик ресурсов Hello не поддерживает все возможности управления базами данных hello объекта [базы данных SQL Azure](https://azure.microsoft.com/services/sql-database/). Например пулы эластичных баз данных и производительность базы данных tooscale hello возможности не поддерживаются. Hello API не совместим с баз данных SQL Server.


## <a name="sql-server-resource-provider-adapter-architecture"></a>Архитектура адаптера поставщика ресурсов SQL Server
поставщик ресурсов Hello не основан на, а также предоставляют все возможности управления базами данных hello базы данных SQL Azure. Например пулы эластичных баз данных и производительность базы данных hello возможность toodial вверх и вниз автоматически недоступны. Тем не менее hello ресурсов поставщик поддерживает аналогичные создания, чтения, обновления и удаления (CRUD).

поставщик ресурсов Hello состоит из трех компонентов:

- **поставщик ресурсов адаптера виртуальной Машины для Hello SQL**, который является виртуальной машине под управлением служб поставщика hello.
- **поставщик ресурсов Hello сам**, который обрабатывает запросы на подготовку, и предоставляет доступ к базе данных ресурсов.
- **Серверы, на которых размещаются SQL Server**, предоставляющие емкости для баз данных, называемые серверами размещения. 

Этот выпуск больше не создает экземпляр SQL Server. Необходимо создать один (или несколько) и/или предоставления доступа tooexternal экземпляров SQL. Существует ряд tooyou доступные параметры, включая шаблоны в hello [коллекции быстрый запуск Azure стека](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/master/mysql-standalone-server-windows) и элементы Marketplace. 

>[!NOTE]
Если вы загрузили какие-либо элементы SQL Marketplace, убедитесь, что также загрузить расширения SQL IaaS hello, или они не будут развернуты.


## <a name="deploy-hello-resource-provider"></a>Разверните hello поставщик ресурсов

1. Если вы еще не сделали регистрации вашего пакета средств разработки и загрузите образ Windows Server 2016 EVAL hello загружаемых посредством управления Marketplace. Можно также использовать сценарий toocreate [образа Windows Server 2016](https://docs.microsoft.com/azure/azure-stack/azure-stack-add-default-image). Среда выполнения Hello .NET 3.5 больше не требуется.

2. [Загрузите файл двоичных файлов поставщика ресурсов SQL hello](https://aka.ms/azurestacksqlrp) и извлеките его на узел комплект средств для разработки hello.

3. Войдите в узел комплект средств для разработки toohello и извлечь hello временный каталог файла установщика tooa SQL RP.

4. Hello Azure стека корневой сертификат извлекается и самозаверяющий сертификат создается как часть этого процесса. 

    __Необязательно:__ при необходимости tooprovide на собственные, подготовьте сертификаты hello и копирования tooa локальный каталог при желании toocustomize сертификаты hello (сценарий установки переданный toohello). Требуется hello следующие сертификаты:

    а. Сертификатом с подстановочными символами для *.dbadapter. \<область\>.\< полного доменного имени\>. Этот сертификат должен быть доверенным, такие как будет выдан центром сертификации (то есть hello цепочка доверия должен существовать без промежуточных сертификатов.) (Можно использовать сертификат один сайт с именем виртуальной Машины явную hello, предоставленные во время установки.)

    b. Hello корневой сертификат, используемый hello Azure Resource Manager для конкретного экземпляра Azure стека. Если он не найден, извлекается hello корневой сертификат.


5. Откройте **новый** повышенными PowerShell консоли и измените toohello каталог, где были извлечены файлы hello. Используйте новые проблемы tooavoid окна, которые могут быть вызваны неверные модули PowerShell, которые уже загружены в системе hello.

6. После установки любой версии hello AzureRm или модули AzureStack PowerShell 1.2.9 или 1.2.10 будет запрашиваемые tooremove их или hello установка не продолжится. Сюда входят версии 1.3 или выше.

7. Запустите hello DeploySqlProvider.ps1 сценария с параметрами hello перечисленные ниже.

Hello скрипт выполняет следующие действия.

* При необходимости, загрузите совместимую версию Azure PowerShell.
* Передача сертификатов hello и другим учетным записям хранения артефактов tooa в комплекте Azure.
* Опубликуйте пакеты коллекции, чтобы выполнить развертывание баз данных SQL с помощью коллекции hello.
* Развертывание виртуальной Машины с помощью образа Windows Server 2016 hello, созданной на шаге 1 и установить поставщик ресурсов hello.
* Зарегистрируйте локальный DNS-запись сопоставляет tooyour поставщика ресурсов виртуальной Машины.
* Регистрация поставщика ресурсов с hello локального диспетчера ресурсов Azure (клиента и администратора).

> [!NOTE]
> Если установка hello занимает более 90 минут, может произойти сбой вы видите сообщение об ошибке на экране приветствия и в файле журнала hello, а развертывания hello повторяется с ошибками шаг hello. Систем, которые не соответствуют hello Рекомендуемый объем памяти и основных характеристик может оказаться может toodeploy hello SQL RP.
>

Ниже приведен пример, можно запустить из hello PowerShell запрашивать (но при необходимости изменить конечные точки сведения и портала учетной записи hello):

```
# Install hello AzureRM.Bootstrapper module
Install-Module -Name AzureRm.BootStrapper -Force

# Installs and imports hello API Version Profile required by Azure Stack into hello current PowerShell session.
Use-AzureRmProfile -Profile 2017-03-09-profile
Install-Module -Name AzureStack -RequiredVersion 1.2.10 -Force

# Download hello Azure Stack Tools from GitHub and set hello environment
cd c:\
Invoke-Webrequest https://github.com/Azure/AzureStack-Tools/archive/master.zip -OutFile master.zip
Expand-Archive master.zip -DestinationPath . -Force

# This endpoint may be different for your installation
Import-Module C:\AzureStack-Tools-master\Connect\AzureStack.Connect.psm1
Add-AzureRmEnvironment -Name AzureStackAdmin -ArmEndpoint "https://adminmanagement.local.azurestack.external" 

# For AAD, use hello following
$tenantID = Get-AzsDirectoryTenantID -AADTenantName "<your directory name>" -EnvironmentName AzureStackAdmin

# For ADFS, replace hello previous line with
# $tenantID = Get-AzsDirectoryTenantID -ADFS -EnvironmentName AzureStackAdmin

$vmLocalAdminPass = ConvertTo-SecureString "P@ssw0rd1" -AsPlainText -Force
$vmLocalAdminCreds = New-Object System.Management.Automation.PSCredential ("sqlrpadmin", $vmLocalAdminPass)

$AdminPass = ConvertTo-SecureString "P@ssw0rd1" -AsPlainText -Force
$AdminCreds = New-Object System.Management.Automation.PSCredential ("admin@mydomain.onmicrosoft.com", $AdminPass)

# change this as appropriate
$PfxPass = ConvertTo-SecureString "P@ssw0rd1" -AsPlainText -Force

# Change directory toohello folder where you extracted hello installation files 
# and adjust hello endpoints
<extracted file directory>\DeploySQLProvider.ps1 -DirectoryTenantID $tenantID -AzCredential $AdminCreds -VMLocalCredential $vmLocalAdminCreds -ResourceGroupName "SqlRPRG" -VmName "SqlVM" -ArmEndpoint "https://adminmanagement.local.azurestack.external" -TenantArmEndpoint "https://management.local.azurestack.external" -DefaultSSLCertificatePassword $PfxPass
 ```

### <a name="deploysqlproviderps1-parameters"></a>Параметры DeploySqlProvider.ps1
Эти параметры можно указать в командной строке hello. Если этого не сделать, или происходит сбой проверки параметров, будет предложено tooprovide hello необходимые объекты.

| Имя параметра | Описание | Комментарий или значение по умолчанию |
| --- | --- | --- |
| **DirectoryTenantID** | Hello Azure или каталог служб федерации Active Directory с Идентификатором (guid). | _обязательный параметр_ |
| **AzCredential** | Укажите hello учетные данные для учетной записи администратора служб Azure стека hello. Необходимо использовать hello же учетные данные используются для развертывания Azure стека). | _обязательный параметр_ |
| **VMLocalCredential** | Укажите учетные данные hello hello учетной записи локального администратора поставщика ресурсов SQL hello виртуальной Машины. Этот пароль также используется для hello SQL **sa** учетной записи. | _обязательный параметр_ |
| **ResourceGroupName** | Определите имя для группы ресурсов, в котором будут храниться элементы, созданный этим сценарием. Например *SqlRPRG*. |  _обязательный параметр_ |
| **VmName** | Определите имя hello hello виртуальной машины на какой поставщик ресурсов tooinstall hello. Например *SqlVM*. |  _обязательный параметр_ |
| **DependencyFilesLocalPath** | Файлы сертификата должен быть помещен в этот каталог также. | _необязательный параметр_ |
| **DefaultSSLCertificatePassword** | Hello пароль для PFX-файл сертификата hello | _обязательный параметр_ |
| **Значение параметра MaxRetryCount** | Определите количество повторений tooretry каждой операции при наличии сбоя.| 2 |
| **RetryDuration** | Определите hello время ожидания между повторными попытками в секундах. | 120 |
| **Удаление** | Удалить поставщик ресурсов hello и все связанные ресурсы (см. примечания ниже) | Нет |
| **DebugMode** | Предотвращает автоматическую очистку в случае ошибки | Нет |


## <a name="verify-hello-deployment-using-hello-azure-stack-portal"></a>Проверка развертывания hello, с помощью портала Azure стека hello

> [!NOTE]
>  После завершения сценария установки hello, вам потребуется toorefresh hello портала toosee hello admin колонку.


1. На рабочем столе hello консоли виртуальной Машины, нажмите кнопку **стека портал Microsoft Azure** и войдите в портал toohello как Здравствуйте, администратор службы.

2. Проверьте успешность развертывания hello. Нажмите кнопку **групп ресурсов** &gt; щелкните hello группы ресурсов, можно использовать и убедитесь, часть essentials hello hello колонке (верхняя половина) считывает  **_даты_ (успешноевыполнение)**.

      ![Проверка развертывания hello SQL RP](./media/azure-stack-sql-rp-deploy/sqlrp-verify.png)


## <a name="provide-capacity-by-connecting-tooa-hosting-sql-server"></a>Предоставляют емкость, подключив tooa, где размещен SQL server

1. Войдите в toohello портал администрирования стек Azure как администратор службы

2. Создание виртуальной машины SQL, если таковая имеется уже доступны. Marketplace управления предлагает некоторые возможности для развертывания виртуальных машин SQL.

3. Нажмите кнопку **поставщиков ресурсов** &gt; **SQLAdapter** &gt; **серверы размещения** &gt; **+ добавить**.

    Hello **серверов размещения SQL** колонка находится где могут подключаться hello поставщика ресурсов SQL Server tooactual экземпляров SQL Server, выступающие в качестве hello серверной части поставщик ресурсов.

    ![Серверы размещения](./media/azure-stack-sql-rp-deploy/sqlrp-hostingserver.PNG)

4. Заполнение формы hello hello сведения о подключении вашего экземпляра SQL Server.

    ![Новый сервер размещения](./media/azure-stack-sql-rp-deploy/sqlrp-newhostingserver.PNG)

    > [!NOTE]
    > До тех пор, пока экземпляр SQL hello может осуществляться hello клиента и администратора диспетчера ресурсов Azure, можно поместить в группе управления hello поставщика ресурсов. экземпляр SQL Hello __должен__ выделить исключительно toohello RP.

5. При добавлении серверов, их необходимо назначить tooa новый или существующий SKU toodifferentiate предложения услуг. Например может иметь экземпляр SQL Enterprise, предоставляя объем базы данных и автоматическое резервное копирование, зарезервировать высокопроизводительных серверов для каждого конкретного отдела, т. д. имя SKU hello должны отражать hello свойства, чтобы клиентов можно размещать свои базы данных соответствующим образом и должны иметь все серверы размещения в номере SKU hello те же возможности.

    Пример:

    ![Номера SKU](./media/azure-stack-sql-rp-deploy/sqlrp-newsku.png)

>[!NOTE]
Номера SKU может занять toobe час tooan видны на портале hello. Невозможно создать базу данных до создания SKU hello.


## <a name="create-your-first-sql-database-tootest-your-deployment"></a>Создайте развертывание вашего первого tootest базы данных SQL

1. Войдите в toohello портала администратора Azure стека учетной записью администратора службы.

2. Нажмите кнопку **+ создать** &gt; **данные + хранилище»** &gt; **базы данных SQL Server (Предварительная версия)** &gt; **добавить**.

3. Заполните форму hello с сведения о базе данных, включая **имя базы данных**, **максимальный размер**, и изменения других параметров hello при необходимости. Вы просили toopick SKU базы данных. По мере добавления серверов размещения они назначаются SKU и базы данных создаются в этом пуле размещения серверов, которые составляют hello SKU.

    ![Новая база данных](./media/azure-stack-sql-rp-deploy/newsqldb.png)


4. Заполните параметры входа hello: **входа базы данных**, и **пароль**. Это учетные данные проверки подлинности SQL, создается только базы данных access toothis. Привет, имя пользователя должно быть глобально уникальным. Создайте новый параметр имени входа или выберите существующий. Параметры входа можно использовать для других баз данных с помощью hello одним SKU.

    ![Создать новое имя входа базы данных](./media/azure-stack-sql-rp-deploy/create-new-login.png)


5. Отправьте форму hello и дождитесь toocomplete развертывания hello.

    В колонке полученный hello Обратите внимание, поле «Строка подключения» hello. В комплекте Azure можно использовать этой строки в любое приложение, которое требуется доступ к SQL Server (например, веб-приложение).

    ![Получить строку подключения hello](./media/azure-stack-sql-rp-deploy/sql-db-settings.png)

## <a name="add-capacity"></a>Добавить емкость

Добавление емкости путем добавления дополнительных узлов SQL на портале Azure стека hello и связать их с соответствующий номер SKU. Toouse другой экземпляр SQL Server вместо hello установлена на поставщик hello виртуальной Машины, нажмите кнопку **поставщиков ресурсов** &gt; **SQLAdapter** &gt; **размещения SQL Серверы** &gt; **+ добавить**.

## <a name="making-sql-databases-available-tootenants"></a>Сделать доступной tootenants баз данных SQL

Создайте планы и предложения toomake баз данных SQL, доступных для клиентов. Необходимо создать план, добавить план toohello службы Microsoft.SqlAdapter hello и добавить существующую квоту или создать новую. При создании квоты, клиент можно указать hello емкость tooallow hello.
    ![Создание планов и предложения tooinclude баз данных](./media/azure-stack-sql-rp-deploy/sqlrp-newplan.png)

## <a name="tenant-usage-of-hello-resource-provider"></a>Использование клиента hello поставщика ресурсов

Самообслуживания баз данных обеспечивается взаимодействие портала клиента hello.

## <a name="removing-hello-sql-adapter-resource-provider"></a>Удаление hello поставщика ресурсов адаптера SQL

В поставщике ресурсов hello tooremove заказа, очень важно toofirst удалите все зависимости.

1. Убедитесь, что у вас есть hello исходного развертывания пакет, загруженный для этой версии hello поставщика ресурсов.

2. Все базы данных клиента, необходимо удалить из поставщика ресурсов hello (это не удалит данные hello). Это следует выполнять с сами клиенты hello.

3. Администратор должен удалить серверы из hello адаптера SQL размещения hello

4. Администратор должен удалить все планы, которые ссылаются на hello адаптера SQL.

5. Администратор должен удалить номера SKU и квоты связанные toohello адаптера SQL.

6. Снова запустите скрипт развертывания hello с hello - удалить параметр, конечные точки диспетчера ресурсов Azure, DirectoryTenantID и учетные данные для учетной записи администратора службы hello.



## <a name="next-steps"></a>Дальнейшие действия


Попробуйте другой [служб PaaS](azure-stack-tools-paas-services.md) как hello [поставщик ресурсов MySQL Server](azure-stack-mysql-resource-provider-deploy.md) и hello [поставщик ресурсов службы приложений](azure-stack-app-service-overview.md).
