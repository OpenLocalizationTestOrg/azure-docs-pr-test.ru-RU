---
title: "Установка заданий обработки эластичных баз данных | Документация Майкрософт"
description: "Пошаговые инструкции по установке компонента заданий обработки эластичных баз данных."
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
ms.openlocfilehash: 71a5aa4da32e76ff02e4a4dae0d47cf03e323688
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/11/2017
---
# <a name="installing-elastic-database-jobs-overview"></a>Обзор установки заданий обработки эластичных баз данных
[**Задания эластичных баз данных**](sql-database-elastic-jobs-overview.md) можно установить с помощью PowerShell или классического портала Azure. Чтобы создавать задания и управлять ими только с помощью API PowerShell, необходимо установить пакет PowerShell. Кроме того, в настоящий момент API-интерфейсы PowerShell предоставляют намного больше возможностей, чем портал.

Если вы уже установили **задания эластичных баз данных** с помощью портала из существующего **эластичного пула**, последняя предварительная версия Powershell будет включать в себя сценарии для обновления существующей установки. Настоятельно рекомендуется обновить установку до последней версии компонентов **заданий обработки эластичных баз данных** , чтобы воспользоваться новыми возможностями, доступными через API-интерфейсы PowerShell.

## <a name="prerequisites"></a>Предварительные требования
* Подписка Azure. Бесплатная пробная версия доступна [здесь](https://azure.microsoft.com/pricing/free-trial/).
* Azure PowerShell. Установите последнюю версию с помощью [установщика веб-платформы](http://go.microsoft.com/fwlink/p/?linkid=320376). Дополнительные сведения можно узнать в статье [Установка и настройка Azure PowerShell](/powershell/azure/overview).
* [Служебная программа командной строки NuGet](https://nuget.org/nuget.exe) используется для установки пакета заданий эластичных баз данных. Дополнительные сведения см. по адресу http://docs.nuget.org/docs/start-here/installing-nuget.

## <a name="download-and-import-the-elastic-database-jobs-powershell-package"></a>Загрузка и импорт пакета PowerShell службы заданий обработки эластичных баз данных
1. Откройте командную строку Microsoft Azure PowerShell и перейдите в каталог, куда была загружена служебная программа командной строки NuGet (nuget.exe).
2. Скачайте и импортируйте пакет **заданий обработки эластичных баз данных** в текущий каталог с помощью следующей команды:
   
        PS C:\>.\nuget install Microsoft.Azure.SqlDatabase.Jobs -prerelease
   
    Файлы **заданий эластичных баз данных** помещаются в локальный каталог в папке **Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x**, где *x.x.xxxx.x* — это номер версии. Командлеты PowerShell (включая необходимые клиентские DLL-файлы) находятся в подкаталоге **tools\ElasticDatabaseJobs**, а сценарии PowerShell для установки, обновления и удаления также находятся в подкаталоге **tools**.
3. Перейдите в подкаталог tools в папке Microsoft.Azure.SqlDatabase.Jobs.x.x.xxx.x с помощью команды cd tools, например:
   
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*>cd tools

4. Запустите сценарий .\InstallElasticDatabaseJobsCmdlets.ps1, чтобы скопировать каталог ElasticDatabaseJobs в папку $home\Documents\WindowsPowerShell\Modules. При этом также будет автоматически импортирован используемый модуль, например:
   
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>Unblock-File .\InstallElasticDatabaseJobsCmdlets.ps1
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>.\InstallElasticDatabaseJobsCmdlets.ps1

## <a name="install-the-elastic-database-jobs-components-using-powershell"></a>Установка компонентов заданий обработки эластичных баз данных с помощью PowerShell
1. Откройте командную строку Microsoft Azure PowerShell и перейдите в подкаталог \tools в папке Microsoft.Azure.SqlDatabase.Jobs.x.x.xxx.x: введите команду cd \tools
   
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*>cd tools

2. Запустите сценарий .\InstallElasticDatabaseJobs.ps1 PowerShell и укажите значения необходимых переменных. Этот сценарий создаст компоненты, описанные в статье [Компоненты службы заданий обработки эластичных баз данных и цены](sql-database-elastic-jobs-overview.md#components-and-pricing) , и настроит облачную службу Azure для надлежащего использования зависящих компонентов.

        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>Unblock-File .\InstallElasticDatabaseJobs.ps1
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>.\InstallElasticDatabaseJobs.ps1

При выполнении этой команды появится окно с запросом **имени пользователя** и **пароля**. Это не учетные данные Azure; введите имя пользователя и пароль, которые станут учетными данными администратора нового сервера.

Параметры, указанные при вызове этого примера, можно заменить на необходимые. Ниже предоставлены дополнительные сведения о поведении каждого параметра:

<table style="width:100%">
  <tr>
    <th>Параметр</th>
    <th>Описание</th>
  </tr>

<tr>
    <td>ResourceGroupName</td>
    <td>Указывает имя группы ресурсов Azure, созданной для хранения новых компонентов Azure. Значение по умолчанию: "__ElasticDatabaseJob". Менять это значение не рекомендуется.</td>
    </tr>

</tr>

    <tr>
    <td>ResourceGroupLocation</td>
    <td>Указывает расположение Azure, используемое для новых компонентов Azure. По умолчанию в этом параметре указан центр США.</td>
</tr>

<tr>
    <td>ServiceWorkerCount</td>
    <td>Указывает число устанавливаемых рабочих процессов службы. Значение по умолчанию: 1. Повышая число рабочих процессов, можно расширять службу и обеспечивать высокую доступность. Значение "2" рекомендуется использовать для развертываний, требующих высокой доступности службы.</td>
    </tr>

</tr>
    <tr>
    <td>ServiceVmSize</td>
    <td>Указывает размер виртуальной машины для использования в облачной службе. Значение по умолчанию: A0. Допускаются значения параметра A0/A1/A2/A3, которые указывают рабочей роли использовать размер ExtraSmall/Small/Medium/Large, соответственно. Чтобы узнать больше о размерах рабочей роли, ознакомьтесь с [компонентами службы заданий эластичных баз данных и ценами](sql-database-elastic-jobs-overview.md#components-and-pricing).</td>
</tr>

</tr>
    <tr>
    <td>SqlServerDatabaseSlo</td>
    <td>Указывает цель уровня обслуживания для стандартного выпуска. Значение по умолчанию: S0. Допускаются значения S0/S1/S2/S3/S4/S6/S9/S12, которые указывают базе данных SQL Azure использовать соответствующую цель уровня обслуживания (SLO). Чтобы узнать больше о размерах рабочей роли, ознакомьтесь с [компонентами службы заданий эластичных баз данных и ценами](sql-database-elastic-jobs-overview.md#components-and-pricing).</td>
</tr>

</tr>
    <tr>
    <td>SqlServerAdministratorUserName</td>
    <td>Указывает имя пользователя администратора для нового сервера Базы данных SQL Azure. Если этот параметр не указан, откроется окно PowerShell с запросом учетных данных.</td>
</tr>

</tr>
    <tr>
    <td>SqlServerAdministratorPassword</td>
    <td>Указывает пароль администратора для нового сервера Базы данных SQL Azure. Если этот параметр не указан, откроется окно PowerShell с запросом учетных данных.</td>
</tr>
</table>

Для систем, рассчитанных на параллельное выполнение больших количеств заданий для большого числа баз данных, рекомендуется указывать такие параметры: -ServiceWorkerCount 2 -ServiceVmSize A2 -SqlServerDatabaseSlo S2.

    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>Unblock-File .\InstallElasticDatabaseJobs.ps1
    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>.\InstallElasticDatabaseJobs.ps1 -ServiceWorkerCount 2 -ServiceVmSize A2 -SqlServerDatabaseSlo S2

## <a name="update-an-existing-elastic-database-jobs-components-installation-using-powershell"></a>Обновление существующей установки компонентов заданий обработки эластичных баз данных с помощью PowerShell
**Задания обработки эластичных баз данных** в существующей установке можно обновить для масштабирования и высокой доступности. Этот процесс позволяет обновлять код службы в будущем без необходимости удаления и повторного создания управляющей базы данных. Этот процесс также можно использовать в той же версии, чтобы изменить размер виртуальных машин или число рабочих процессов сервера.

Чтобы изменить размер виртуальных машин в установке, запустите следующий сценарий, заменив значения параметров на нужные вам.

    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>Unblock-File .\UpdateElasticDatabaseJobs.ps1
    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>.\UpdateElasticDatabaseJobs.ps1 -ServiceVmSize A1 -ServiceWorkerCount 2

<table style="width:100%">
  <tr>
  <th>Параметр</th>
  <th>Описание</th>
</tr>

  <tr>
    <td>ResourceGroupName</td>
    <td>Указывает имя группы ресурсов Azure, используемой при изначальной установке компонентов заданий обработки эластичных баз данных. Значение по умолчанию: "__ElasticDatabaseJob". Так как менять это значение не рекомендуется, скорее всего, указывать этот параметр не потребуется.</td>
    </tr>
</tr>

</tr>

  <tr>
    <td>ServiceWorkerCount</td>
    <td>Указывает число устанавливаемых рабочих процессов службы.  Значение по умолчанию: 1.  Повышая число рабочих процессов, можно расширять службу и обеспечивать высокую доступность.  Значение "2" рекомендуется использовать для развертываний, требующих высокой доступности службы.</td>
</tr>

</tr>

    <tr>
    <td>ServiceVmSize</td>
    <td>Указывает размер виртуальной машины для использования в облачной службе. Значение по умолчанию: A0. Допускаются значения параметра A0/A1/A2/A3, которые указывают рабочей роли использовать размер ExtraSmall/Small/Medium/Large, соответственно. Чтобы узнать больше о размерах рабочей роли, ознакомьтесь с [компонентами службы заданий эластичных баз данных и ценами](sql-database-elastic-jobs-overview.md#components-and-pricing).</td>
</tr>

</table>

## <a name="install-the-elastic-database-jobs-components-using-the-portal"></a>Установка компонентов заданий обработки эластичных баз данных с помощью портала
[Создав эластичный пул](sql-database-elastic-pool-manage-portal.md), вы можете установить компоненты **заданий обработки эластичных баз данных**, которые позволят выполнять административные задачи для каждой базы данных в эластичном пуле. В отличие от API-интерфейсов PowerShell **заданий обработки эластичных баз данных** , интерфейс портала в данный момент позволяет выполнять задания только для существующего пула.

**Предполагаемое время выполнения:** 10 минут.

1. В представлении панели мониторинга эластичного пула на [портале Azure](https://portal.azure.com/#) щелкните **Создать задание**.
2. Если вы создаете задание впервые, вам необходимо установить **задания эластичных баз данных**, выбрав **УСЛОВИЯ ПРЕДВАРИТЕЛЬНОЙ ВЕРСИИ**.
3. Примите условия, установив соответствующий флажок.
4. В представлении «Установка служб» щелкните **УЧЕТНЫЕ ДАННЫЕ ДЛЯ ЗАДАНИЯ**.
   
    ![Установка служб][1]
5. Введите имя пользователя и пароль администратора базы данных. В процессе установки создается сервер базы данных SQL Azure. На этом сервере создается новая база данных, известная также как управляющая база данных, в которой хранятся метаданные для заданий обработки эластичных баз данных. Созданные здесь имя пользователя и пароль используются для входа в управляющую базу данных. Для выполнения сценариев на базах данных в пуле используются отдельные учетные данные.
   
    ![Создание имени пользователя и пароля][2]
6. Нажмите кнопку «ОК». Компоненты будут созданы через несколько минут в новой [группе ресурсов](../azure-resource-manager/resource-group-overview.md). Новая группа ресурсов закрепляется на начальной доске, как показано на рисунке ниже. После создания компонентов в группе будут созданы задания обработки эластичных баз данных (облачная служба, база данных SQL, служебная шина и хранилище).
   
    ![Группа ресурсов на начальной доске][3]
7. Если во время установки службы заданий эластичной базы данных вы попытаетесь создать или изменить какое-то задание, после ввода **учетных данных** появится следующее сообщение.
   
    ![Развертывание еще не завершено][4]

Если требуется удаление, удалите группу ресурсов. Ознакомьтесь со статьей [Удаление компонентов заданий обработки эластичных баз данных](sql-database-elastic-jobs-uninstall.md).

## <a name="next-steps"></a>Дальнейшие действия
Убедитесь, что в каждой базе данных группы созданы учетные данные с правами на выполнение сценариев. Дополнительные сведения см. в статье [Защита базы данных SQL](sql-database-manage-logins.md).
Чтобы приступить к работе, прочитайте статью [Создание заданий обработки эластичных баз данных и управление ими](sql-database-elastic-jobs-create-and-manage.md).

<!--Image references-->
[1]: ./media/sql-database-elastic-jobs-service-installation/screen-1.png
[2]: ./media/sql-database-elastic-jobs-service-installation/credentials.png
[3]: ./media/sql-database-elastic-jobs-service-installation/start-board.png
[4]: ./media/sql-database-elastic-jobs-service-installation/not-done.png
