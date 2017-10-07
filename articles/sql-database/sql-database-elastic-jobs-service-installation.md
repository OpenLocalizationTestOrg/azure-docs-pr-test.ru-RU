---
title: "aaaInstalling заданий эластичных баз данных | Документы Microsoft"
description: "Показывает, как установить компонент эластичного задания hello."
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: cbe0aa2b-17e3-4b6f-a16f-6ebc1f5a66af
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 0349f66a4428f81d00d43681d7f2177f273ec032
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="installing-elastic-database-jobs-overview"></a>Обзор установки заданий обработки эластичных баз данных
[**Заданий эластичных баз данных** ](sql-database-elastic-jobs-overview.md) может быть выполнена с помощью PowerShell или с помощью hello классический Portal.You Azure можно получить доступ к toocreate задания и управлять ими с помощью API-интерфейса PowerShell hello только в том случае, если установить пакет PowerShell hello. Кроме того API-интерфейсов PowerShell hello предоставляют значительно больше возможностей, чем hello портала на данный момент времени.

Если вы уже установили **заданий эластичных баз данных** через hello портала из существующей **эластичного пула**, hello последней предварительной версии Powershell включает в себя сценарии tooupgrade существующей установки. Это настоятельно рекомендуется tooupgrade toohello вашей установки последних **заданий эластичных баз данных** компонентов в порядке tootake преимуществами новых функциональных возможностей, предоставляемых через hello API-интерфейсов PowerShell.

## <a name="prerequisites"></a>Предварительные требования
* Подписка Azure. Бесплатная пробная версия доступна [здесь](https://azure.microsoft.com/pricing/free-trial/).
* Azure PowerShell. Установить последнюю версию hello, с помощью hello [Web Platform Installer](http://go.microsoft.com/fwlink/p/?linkid=320376). Дополнительные сведения см. в разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview).
* [Программы командной строки NuGet](https://nuget.org/nuget.exe) — пакет эластичной базы данных заданий, используется tooinstall hello. Дополнительные сведения см. по адресу http://docs.nuget.org/docs/start-here/installing-nuget.

## <a name="download-and-import-hello-elastic-database-jobs-powershell-package"></a>Загрузите и импортируйте пакет PowerShell заданий эластичных баз данных hello
1. Запустите командное окно Microsoft Azure PowerShell и перейдите в каталог toohello, который вы загрузили служебной программы командной строки NuGet (nuget.exe).
2. Загрузите и импортируйте **заданий эластичных баз данных** пакета в текущем каталоге hello с hello следующую команду:
   
        PS C:\>.\nuget install Microsoft.Azure.SqlDatabase.Jobs -prerelease
   
    Hello **заданий эластичных баз данных** файлы помещаются в локальном каталоге hello в папку с именем **Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x** где *x.x.xxxx.x* Отображает номер версии hello. командлеты PowerShell Hello (включая необходимых клиентских библиотек) находятся в hello **tools\ElasticDatabaseJobs** вложенный каталог hello tooinstall сценариев PowerShell, а также удалить также находятся в hello  **средства** вложенный каталог.
3. Перейти toohello средства вложенный каталог в папке Microsoft.Azure.SqlDatabase.Jobs.x.x.xxx.x hello, введя средства компакт-диска, например:
   
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*>cd tools

4. Выполнение hello.\InstallElasticDatabaseJobsCmdlets.ps1 сценария toocopy hello ElasticDatabaseJobs каталог в $home\Documents\WindowsPowerShell\Modules. Это также автоматически импортирует hello модуль для использования, например:
   
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>Unblock-File .\InstallElasticDatabaseJobsCmdlets.ps1
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>.\InstallElasticDatabaseJobsCmdlets.ps1

## <a name="install-hello-elastic-database-jobs-components-using-powershell"></a>Установить компоненты задания hello эластичной базы данных, с помощью PowerShell
1. Запустите командную строку Microsoft Azure PowerShell и перейдите toohello \tools вложенный каталог в папке Microsoft.Azure.SqlDatabase.Jobs.x.x.xxx.x hello: Введите \tools компакт-диска
   
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*>cd tools

2. Выполнить сценарий PowerShell.\InstallElasticDatabaseJobs.ps1 hello и передают значения для запрошенного переменных. Этот скрипт создает hello компонентами, описанными в [заданий эластичных баз данных компонентов и цен](sql-database-elastic-jobs-overview.md#components-and-pricing) вместе с Настройка hello облачной службы Azure tooappropriately использовать hello зависимые компоненты.

        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>Unblock-File .\InstallElasticDatabaseJobs.ps1
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>.\InstallElasticDatabaseJobs.ps1

При выполнении этой команды появится окно с запросом **имени пользователя** и **пароля**. Это не учетные данные Azure, введите hello имя пользователя и пароль, который будет иметь учетные данные администратора hello, следует использовать toocreate для нового сервера hello.

можно изменять параметры Hello, предоставляемые на этот образец вызова для необходимые настройки. Hello ниже приведены дополнительные сведения на поведение hello каждого параметра:

<table style="width:100%">
  <tr>
    <th>Параметр</th>
    <th>Описание</th>
  </tr>

<tr>
    <td>ResourceGroupName</td>
    <td>Предоставляет имя группы ресурсов Azure hello, созданные toocontain hello вновь созданные компоненты Azure. Этот параметр по умолчанию слишком «__ElasticDatabaseJob». Это не рекомендуется toochange это значение.</td>
    </tr>

</tr>

    <tr>
    <td>ResourceGroupLocation</td>
    <td>Предоставляет toobe расположение Azure hello для hello в создаваемых компонентах Azure. Этот параметр по умолчанию toohello расположение центральной части США.</td>
</tr>

<tr>
    <td>ServiceWorkerCount</td>
    <td>Предоставляет номер hello tooinstall службы рабочих процессов. Этот параметр по умолчанию too1. Увеличение количества рабочих процессов может быть используется tooscale out hello службы и tooprovide высокого уровня доступности. Рекомендуется toouse «2» для развертываний, которые требуется высокий уровень доступности службы hello.</td>
    </tr>

</tr>
    <tr>
    <td>ServiceVmSize</td>
    <td>Предоставляет hello размер виртуальной Машины для использования в пределах hello облачной службы. Этот параметр по умолчанию tooA0. Допустимы значения параметров из A0/A1 и A2/A3 заставляющие hello рабочей роли toouse размер очень мелкий/малого и среднего и широкого соответственно. Чтобы узнать больше о размерах рабочей роли, ознакомьтесь с [компонентами службы заданий эластичных баз данных и ценами](sql-database-elastic-jobs-overview.md#components-and-pricing).</td>
</tr>

</tr>
    <tr>
    <td>SqlServerDatabaseSlo</td>
    <td>Предоставляет hello целевой уровень обслуживания Standard edition. Этот параметр по умолчанию tooS0. Значения параметров S0 или S1 и S2 и S3 принимаются заставляющие hello базы данных SQL Azure toouse Здравствуйте, соответствующего цели уровня Обслуживания. Чтобы узнать больше о размерах рабочей роли, ознакомьтесь с [компонентами службы заданий эластичных баз данных и ценами](sql-database-elastic-jobs-overview.md#components-and-pricing).</td>
</tr>

</tr>
    <tr>
    <td>SqlServerAdministratorUserName</td>
    <td>Содержит имя пользователя администратора hello для hello только что созданный сервер базы данных SQL Azure. Если не указан, в окне учетные данные PowerShell будет открыта tooprompt hello учетных данных.</td>
</tr>

</tr>
    <tr>
    <td>SqlServerAdministratorPassword</td>
    <td>Предоставляет пароль администратора hello hello только что созданный сервер базы данных SQL Azure. Если не указано, PowerShell учетных данных будет открыто окно tooprompt hello учетных данных.</td>
</tr>
</table>

Для систем, предназначенных для имеющих большое количество заданий, выполняемых параллельно с большим числом баз данных, рекомендуется toospecify параметров таких как: - ServiceWorkerCount 2 - ServiceVmSize A2 - SqlServerDatabaseSlo S2.

    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>Unblock-File .\InstallElasticDatabaseJobs.ps1
    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>.\InstallElasticDatabaseJobs.ps1 -ServiceWorkerCount 2 -ServiceVmSize A2 -SqlServerDatabaseSlo S2

## <a name="update-an-existing-elastic-database-jobs-components-installation-using-powershell"></a>Обновление существующей установки компонентов заданий обработки эластичных баз данных с помощью PowerShell
**Задания обработки эластичных баз данных** в существующей установке можно обновить для масштабирования и высокой доступности. Этот процесс позволяет для будущих обновлений кода службы без необходимости toodrop и повторного создания базы данных системы управления hello. Этот процесс также может использоваться внутри hello одной версии toomodify hello службы виртуальной Машины размера или hello server число рабочих.

размер виртуальной Машины hello tooupdate установки, выполнения hello, выполнив сценарий с параметрами обновленные значения toohello по своему усмотрению.

    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>Unblock-File .\UpdateElasticDatabaseJobs.ps1
    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>.\UpdateElasticDatabaseJobs.ps1 -ServiceVmSize A1 -ServiceWorkerCount 2

<table style="width:100%">
  <tr>
  <th>Параметр</th>
  <th>Описание</th>
</tr>

  <tr>
    <td>ResourceGroupName</td>
    <td>Указывает имя группы ресурсов Azure hello, используемое при первоначальной установке компонентов задания hello эластичной базы данных. Этот параметр по умолчанию слишком «__ElasticDatabaseJob». Поскольку это не рекомендуется toochange это значение не должен содержать toospecify этот параметр.</td>
    </tr>
</tr>

</tr>

  <tr>
    <td>ServiceWorkerCount</td>
    <td>Предоставляет номер hello tooinstall службы рабочих процессов.  Этот параметр по умолчанию too1.  Увеличение количества рабочих процессов может быть используется tooscale out hello службы и tooprovide высокого уровня доступности.  Рекомендуется toouse «2» для развертываний, которые требуется высокий уровень доступности службы hello.</td>
</tr>

</tr>

    <tr>
    <td>ServiceVmSize</td>
    <td>Предоставляет hello размер виртуальной Машины для использования в пределах hello облачной службы. Этот параметр по умолчанию tooA0. Допустимы значения параметров из A0/A1 и A2/A3 заставляющие hello рабочей роли toouse размер очень мелкий/малого и среднего и широкого соответственно. Чтобы узнать больше о размерах рабочей роли, ознакомьтесь с [компонентами службы заданий эластичных баз данных и ценами](sql-database-elastic-jobs-overview.md#components-and-pricing).</td>
</tr>

</table>

## <a name="install-hello-elastic-database-jobs-components-using-hello-portal"></a>Установить компоненты задания hello эластичной базы данных, с помощью портала hello
После получения [создан пул эластичных](sql-database-elastic-pool-manage-portal.md), можно установить **заданий эластичных баз данных** компоненты tooenable выполнения административных задач для каждой базы данных в эластичный пул hello. В отличие от, когда с помощью hello **заданий эластичных баз данных** API-интерфейсов PowerShell интерфейс портала hello является в настоящее время ограничены tooonly выполняет существующий пул.

**Предполагаемое время toocomplete:** 10 минут.

1. Из представления панели мониторинга hello hello пула эластичных БД через hello [портала Azure](https://portal.azure.com/#) , нажмите кнопку **создать задание**.
2. При создании задания для hello впервые, необходимо установить **заданий эластичных баз данных** , щелкнув **условия предварительной версии**.
3. Примите условия hello, щелкнув hello флажок.
4. В представлении hello» установите службы» щелкните **учетные данные задания**.
   
    ![Установка служб hello][1]
5. Введите имя пользователя и пароль администратора базы данных. В процессе установки hello создается новый сервер базы данных SQL Azure. В этом новом сервере новую базу данных, называемой базой данных управления hello и используется toocontain hello метаданные для заданий эластичных баз данных. Ведение журнала в базе данных системы управления toohello с целью hello используются Hello имя пользователя и пароль, созданные здесь. Отдельные учетные данные используются для выполнения скриптов для баз данных hello в пуле hello.
   
    ![Создание имени пользователя и пароля][2]
6. Нажмите кнопку "ОК" hello. компоненты Hello создаются автоматически через несколько минут, в новом [группы ресурсов](../azure-resource-manager/resource-group-overview.md). закрепленные Hello новую группу ресурсов toohello запуск доски, как показано ниже. После создания, эластичной базы данных заданий (облачной службы, базы данных SQL, Service Bus и хранилище) создаются в группе hello.
   
    ![Группа ресурсов на начальной доске][3]
7. Если попытка toocreate или управления заданием, пока выполняется установка заданий эластичных баз данных, при предоставлении **учетные данные** вы увидите следующие сообщение hello.
   
    ![Развертывание еще не завершено][4]

При необходимости отмены установки, удаления группы ресурсов hello. В разделе [как toouninstall hello эластичной базы данных задание компонентов](sql-database-elastic-jobs-uninstall.md).

## <a name="next-steps"></a>Дальнейшие действия
Убедитесь учетные данные с hello соответствующие права для выполнения скрипта создается для каждой базы данных в группе hello, Дополнительные сведения см. в разделе [защите базы данных SQL](sql-database-manage-logins.md).
В разделе [Создание и управление заданиями эластичной базы данных](sql-database-elastic-jobs-create-and-manage.md) tooget работы.

<!--Image references-->
[1]: ./media/sql-database-elastic-jobs-service-installation/screen-1.png
[2]: ./media/sql-database-elastic-jobs-service-installation/credentials.png
[3]: ./media/sql-database-elastic-jobs-service-installation/start-board.png
[4]: ./media/sql-database-elastic-jobs-service-installation/not-done.png
