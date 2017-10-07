---
title: "базы данных aaaUse MySQL как PaaS стек Azure | Документы Microsoft"
description: "Узнайте, как развернуть hello поставщик ресурсов MySQL и предоставить баз данных MySQL в качестве службы на стек Azure"
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
ms.openlocfilehash: 634e408eae9f3d8257a8610c60def0978ce333c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-mysql-databases-on-microsoft-azure-stack"></a>Использование базы данных MySQL в стеке Microsoft Azure


Вы можете развернуть поставщик ресурсов MySQL в Azure стек. После развертывания hello поставщика ресурсов, можно создать MySQL серверов и баз данных с помощью шаблонов развертывания диспетчера ресурсов Azure и предоставить баз данных MySQL в качестве службы. Базы данных MySQL, которые используются на веб-сайтах, поддерживают множество платформ веб-сайта. Например после развертывания hello поставщика ресурсов, можно создать веб-сайты WordPress с платформы Azure веб-приложения hello как дополнительный компонент службы (PaaS) стек Azure.

Поставщик MySQL toodeploy hello в системе, которая не имеет доступа к Интернету, можно скопировать файл hello [mysql соединитель net 6.9.9.msi](https://dev.mysql.com/get/Download/sConnector-Net/mysql-connector-net-6.9.9.msi) tooa локального совместное использование и предоставлять этим сетевым именем при появлении запроса (см. ниже). Необходимо также установить hello Azure и Azure стека модули PowerShell.


## <a name="mysql-server-resource-provider-adapter-architecture"></a>Архитектура адаптера поставщика ресурсов MySQL Server

поставщик ресурсов Hello состоит из трех компонентов:

- **поставщик ресурсов адаптера виртуальной Машины для Hello MySQL**, который является виртуальной машине под управлением служб поставщика hello.
- **поставщик ресурсов Hello сам**, который обрабатывает запросы на подготовку, и предоставляет доступ к базе данных ресурсов.
- **Серверы, на которых размещены сервер MySQL**, предоставляющие емкости для баз данных, называемые серверами размещения. 

Этот выпуск больше не создает экземпляр MySQL. Необходимо создать их и/или предоставления доступа tooexternal экземпляров SQL. Вы можете посетить hello [коллекции быстрый запуск Azure стека](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/master/mysql-standalone-server-windows) для шаблона пример, который можно создать сервер MySQL для вас или загрузить и установить сервер MySQL из hello Marketplace.

## <a name="deploy-hello-resource-provider"></a>Разверните hello поставщик ресурсов

1. Если вы еще не сделали зарегистрировать ваш пакет средств разработки и загрузите hello Windows Server 2016 Datacenter - Eval образа загрузки через Marketplace управления. Можно также использовать сценарий toocreate [образа Windows Server 2016](https://docs.microsoft.com/azure/azure-stack/azure-stack-add-default-image).

2. [Загрузите файл двоичных файлов поставщика ресурсов MySQL hello](https://aka.ms/azurestackmysqlrp) и извлеките его на узел комплект средств для разработки hello.

3. Войдите в узел комплект средств для разработки toohello и извлечь hello временный каталог файла установщика tooa MySQL RP.

4. Hello Azure стека корневой сертификат извлекается и самозаверяющий сертификат создается как часть этого процесса. 

    __Необязательно:__ при необходимости tooprovide на собственные, подготовьте сертификаты hello и копирования tooa локальный каталог при желании toocustomize сертификаты hello (сценарий установки переданный toohello). Требуется hello следующее:

    а. Сертификатом с подстановочными символами для *.dbadapter. \<область\>.\< полного доменного имени\>. Этот сертификат должен быть доверенным, такие как будет выдан центром сертификации (то есть hello цепочка доверия должен существовать без промежуточных сертификатов.) (Можно использовать сертификат один сайт с именем виртуальной Машины явную hello, предоставленные во время установки.)

    b. Hello корневой сертификат, используемый hello Azure Resource Manager для конкретного экземпляра Azure стека. Если он не найден, извлекается hello корневой сертификат.

5. Откройте **новый** повышенными PowerShell консоли и измените toohello каталог, где были извлечены файлы hello. Используйте новые проблемы tooavoid окна, которые могут быть вызваны неверные модули PowerShell, которые уже загружены в системе hello.

6. После установки любой версии hello AzureRm или модули AzureStack PowerShell 1.2.9 или 1.2.10 будет запрашиваемые tooremove их или hello установка не продолжится. Сюда входят версии 1.3 или выше.

7. Запустите DeployMySqlProvider.ps1.

Этот скрипт выполняет следующие действия.

* При необходимости, загрузите совместимую версию Azure PowerShell.
* Загрузите hello MySQL соединителя двоичный (это может быть предоставлен вне сети).
* Отправьте сертификат hello и все другие артефакты tooan учетной записи хранилища Azure стека.
* Опубликуйте пакеты коллекции, чтобы выполнить развертывание баз данных MySQL с помощью коллекции hello.
* Развертывание виртуальной машины (VM), на котором размещена поставщика ресурсов.
* Зарегистрируйте локальный DNS-запись сопоставляет tooyour поставщика ресурсов виртуальной Машины.
* Регистрация поставщика ресурсов с hello локального диспетчера ресурсов Azure.

Либо укажите хотя бы hello обязательных параметров в командной строке hello, так и в, если выполняется без параметров, запрашиваемые tooenter их. 

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
$vmLocalAdminCreds = New-Object System.Management.Automation.PSCredential ("mysqlrpadmin", $vmLocalAdminPass)

$AdminPass = ConvertTo-SecureString "P@ssw0rd1" -AsPlainText -Force
$AdminCreds = New-Object System.Management.Automation.PSCredential ("admin@mydomain.onmicrosoft.com", $AdminPass)

# change this as appropriate
$PfxPass = ConvertTo-SecureString "P@ssw0rd1" -AsPlainText -Force

# Change directory toohello folder where you extracted hello installation files 
# and adjust hello endpoints
<extracted file directory>\DeployMySQLProvider.ps1 -DirectoryTenantID $tenantID -AzCredential $AdminCreds -VMLocalCredential $vmLocalAdminCreds -ResourceGroupName "MySqlRG" -VmName "MySQLRP" -ArmEndpoint "https://adminmanagement.local.azurestack.external" -TenantArmEndpoint "https://management.local.azurestack.external" -DefaultSSLCertificatePassword $PfxPass -DependencyFilesLocalPath
 ```

### <a name="deploymysqlproviderps1-parameters"></a>Параметры DeployMySqlProvider.ps1

Эти параметры можно указать в командной строке hello. Если этого не сделать, или происходит сбой проверки параметров, будет предложено tooprovide hello необходимые объекты.

| Имя параметра | Описание | Комментарий или значение по умолчанию |
| --- | --- | --- |
| **DirectoryTenantID** | Hello Azure или каталог служб федерации Active Directory с Идентификатором (guid) | _обязательный параметр_ |
| **ArmEndpoint** | Hello Azure стека администратора Azure конечную точку диспетчера ресурсов | _обязательный параметр_ |
| **TenantArmEndpoint** | Hello Azure стек Azure Resource Manager конечной точки клиента | _обязательный параметр_ |
| **AzCredential** | Azure учетных данных учетной записи администратора службы стека (hello используйте учетную запись как предназначенная для развертывания Azure стека) | _обязательный параметр_ |
| **VMLocalCredential** | Hello учетной записи локального администратора поставщика ресурсов MySQL hello виртуальной Машины | _обязательный параметр_ |
| **ResourceGroupName** | Группа ресурсов для элементов hello, созданный этим сценарием |  _обязательный параметр_ |
| **VmName** | Имя виртуальной Машины вместимость hello hello поставщика ресурсов |  _обязательный параметр_ |
| **AcceptLicense** | Пропускает запрос tooaccept hello hello лицензии GPL (http://www.gnu.org/licenses/old-licenses/gpl-2.0.html) | |
| **DependencyFilesLocalPath** | Путь tooa локальной общей папкой, содержащий [mysql соединитель net 6.9.9.msi](https://dev.mysql.com/get/Downloads/Connector-Net/mysql-connector-net-6.9.9.msi). Если указать их в этот каталог также должны находиться файлы сертификатов. | _необязательный параметр_ |
| **DefaultSSLCertificatePassword** | Hello пароль для PFX-файл сертификата hello | _обязательный параметр_ |
| **Значение параметра MaxRetryCount** | Каждая операция повторяется, если происходит сбой | 2 |
| **RetryDuration** | Время ожидания между повторными попытками в секундах | 120 |
| **Удаление** | Удалить поставщик ресурсов hello | Нет |
| **DebugMode** | Предотвращает автоматическую очистку в случае ошибки | Нет |


В зависимости от скорости производительности и загрузки системы hello установка может занять всего 20 минут или долго как несколько часов. Если колонке MySQLAdapter hello не доступен, необходимо обновить портал администрирования hello.

> [!NOTE]
> Если установка hello занимает более 90 минут, может произойти сбой и появится сообщение об ошибке на экране приветствия и в файле журнала hello. из hello сбой шаг развертывания Hello будет предпринята повторная попытка. Систем, которые не соответствуют hello Рекомендуемый объем памяти и основных характеристик может оказаться может toodeploy hello MySQL RP.


## <a name="provide-capacity-by-connecting-tooa-mysql-hosting-server"></a>Предоставляют емкость, подключив tooa сервер размещения MySQL

1. Войдите в toohello портала Azure стека администратором службы.

2. Нажмите кнопку **поставщиков ресурсов** &gt; **MySQLAdapter** &gt; **серверы размещения** &gt; **+ добавить**.

    Hello **серверы размещения MySQL** колонка находится где могут подключаться hello поставщик ресурсов MySQL Server tooactual экземпляры MySQL Server, выступающие в качестве hello серверной части поставщик ресурсов.

    ![Серверы размещения](./media/azure-stack-mysql-rp-deploy/mysql-add-hosting-server-2.png)

3. Заполнение формы hello hello сведения о подключении экземпляра сервера MySQL. Укажите hello полное доменное имя (FQDN) или допустимый IPv4-адрес и не hello короткое имя виртуальной Машины. Данная установка больше не содержит экземпляр MySQL по умолчанию. Здравствуйте, размеры помогает поставщика ресурсов hello управление емкостью hello базы данных. Его необходимо закрыть toohello физический объем hello сервера базы данных.

    > [!NOTE]
    > При условии, что экземпляр MySQL hello может осуществляться hello клиента и администратора диспетчера ресурсов Azure, можно поместить в группе управления hello поставщика ресурсов. экземпляр MySQL Hello __должен__ выделить исключительно toohello RP.

4. При добавлении серверов, необходимо назначить их tooa новый или существующий SKU tooallow дифференцированных предложений услуг. Например может иметь установленный экземпляр enterprise, предоставляя объем базы данных и автоматическое резервное копирование, зарезервировать высокопроизводительных серверов для каждого конкретного отдела, т. д. имя SKU hello должны отражать hello свойства, чтобы клиентов можно размещать свои базы данных соответствующим образом и должны иметь все серверы размещения в номере SKU hello те же возможности.

    ![Создание MySQL SKU](./media/azure-stack-mysql-rp-deploy/mysql-new-sku.png)


>[!NOTE]
Номера SKU может занять toobe час tooan видны на портале hello. Невозможно создать базу данных до создания SKU hello.


## <a name="create-your-first-mysql-database-tootest-your-deployment"></a>Создайте развертывание вашего первого tootest базы данных MySQL


1. Войдите в toohello портала Azure стека учетной записью администратора службы.

2. Нажмите кнопку hello **+ создать** кнопку &gt; **данные + хранилище** &gt; **базы данных MySQL (Предварительная версия)**.

3. Заполните форму hello с hello сведения о базе данных.

    ![Создание теста базы данных MySQL](./media/azure-stack-mysql-rp-deploy/mysql-create-db.png)

4. Выберите SKU.

    ![Выберите SKU](./media/azure-stack-mysql-rp-deploy/mysql-select-a-sku.png)

5. Создание параметра имени входа. можно повторно использовать имя входа приветствия или создать новую публикацию. Оно содержит hello имя пользователя и пароль для базы данных hello.

    ![Создать новое имя входа базы данных](./media/azure-stack-mysql-rp-deploy/create-new-login.png)

    Строка подключения Hello включает имя сервера hello реальной базы данных. Скопируйте его с портала hello.

    ![Получить строку hello подключения для базы данных MySQL hello](./media/azure-stack-mysql-rp-deploy/mysql-db-created.png)

> [!NOTE]
> Длина Hello hello имена пользователей не может превышать 32 символов с MySQL 5.7 или 16 символов в более ранних версий. Это ограничение реализаций MySQL hello.


## <a name="add-capacity"></a>Добавить емкость

Добавьте емкости путем добавления новых серверов MySQL в портале Azure стека hello. Toouse другой экземпляр MySQL, нажмите кнопку **поставщиков ресурсов** &gt; **MySQLAdapter** &gt; **серверы размещения MySQL** &gt; **+ Добавить**.


## <a name="making-mysql-databases-available-tootenants"></a>Сделать доступной tootenants баз данных MySQL
Создайте планы и предложения toomake баз данных MySQL, доступных для клиентов. Добавление службы Microsoft.MySqlAdapter hello, добавьте квоты, и т. д.

![Создание планов и предложения tooinclude баз данных](./media/azure-stack-mysql-rp-deploy/mysql-new-plan.png)

## <a name="removing-hello-mysql-adapter-resource-provider"></a>Удаление hello поставщик ресурсов MySQL адаптера

поставщик ресурсов tooremove hello, очень важно toofirst удалите все зависимости.

1. Убедитесь, что у вас есть hello исходного развертывания пакет, загруженный для этой версии hello поставщика ресурсов.

2. Все базы данных клиента, необходимо удалить из поставщика ресурсов hello (это не удалит данные hello). Это следует выполнять с сами клиенты hello.

3. Клиентам необходимо отменить регистрацию имен hello.

4. Администратор должен удалить серверы из hello адаптера MySQL размещения hello

5. Администратор должен удалить все планы, ссылающиеся на hello адаптера MySQL.

6. Администратор должен удалить любой связанный toohello квот MySQL адаптера.

7. Снова запустите скрипт развертывания hello с hello - удалить параметр, конечные точки диспетчера ресурсов Azure, DirectoryTenantID и учетные данные для учетной записи администратора службы hello.




## <a name="next-steps"></a>Дальнейшие действия


Попробуйте другой [служб PaaS](azure-stack-tools-paas-services.md) как hello [поставщик ресурсов SQL Server](azure-stack-sql-resource-provider-deploy.md) и hello [поставщик ресурсов службы приложений](azure-stack-app-service-overview.md).
