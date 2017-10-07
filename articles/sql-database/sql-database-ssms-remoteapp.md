---
title: "aaaConnect tooSQL базы данных с помощью SQL Server Management Studio в Azure RemoteApp | Документы Microsoft"
description: "Как использовать этот учебник toolearn toouse SQL Server Management Studio в Azure RemoteApp для обеспечения безопасности и производительности при подключении tooSQL базы данных"
services: sql-database
documentationcenter: 
author: adhurwit
manager: jhubbard
ms.assetid: 1052c83c-e7f5-4736-922f-216194d8874b
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/01/2016
ms.author: adhurwit
ms.openlocfilehash: 73994f9a1eb3e48efa5d7c4f976b00cfcbc88d75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-sql-server-management-studio-in-azure-remoteapp-tooconnect-toosql-database"></a>Используйте SQL Server Management Studio в Azure RemoteApp tooconnect tooSQL базы данных

> [!IMPORTANT]
> Мы выводим удаленное приложение Azure RemoteApp из эксплуатации. Чтение hello [объявления](https://go.microsoft.com/fwlink/?linkid=821148) подробные сведения.
>

## <a name="introduction"></a>Введение
В этом учебнике показано как toouse SQL Server Management Studio (SSMS) в Azure RemoteApp tooconnect tooSQL базы данных. Пошаговое описание процесса настройки SQL Server Management Studio в Azure RemoteApp hello, объясняет преимущества hello и показывает средства безопасности, которые можно использовать в Azure Active Directory.

**Предполагаемое время toocomplete:** 45 минут

## <a name="ssms-in-azure-remoteapp"></a>SSMS в Azure RemoteApp
Azure RemoteApp — это служба удаленных рабочих столов в Azure, предоставляющая приложения. Узнать о ней больше можно здесь: [Что такое Azure RemoteApp?](../remoteapp/remoteapp-whatis.md)

Среда SSMS, работающих в Azure RemoteApp позволяет hello такие же возможности, как при запуске среда SSMS локально.

![Снимок экрана: выполнение SSMS в Azure RemoteApp][1]

## <a name="benefits"></a>Преимущества
Существует много преимуществ toousing SSMS в Azure RemoteApp, включая:

* Порт 1433 для Azure SQL server не поддерживает toobe предоставляется извне (за пределами Azure).
* Нет необходимости tookeep, добавлять и удалять IP-адреса в брандмауэр сервера Azure SQL hello.
* Все подключения к Azure RemoteApp выполняются по протоколу HTTPS к порту 443 с помощью зашифрованного протокола удаленного рабочего стола.
* Предусмотрена возможность масштабирования и поддержка многопользовательского режима.
* Нет выигрыш от необходимости SSMS в hello в одном регионе hello базы данных SQL.
* Можно проводить аудит использования Azure RemoteApp на выпуск Premium hello Azure Active Directory, которая содержит отчеты о действиях пользователя.
* Можно включить многофакторную проверку подлинности (MFA).
* Доступ SSMS в любом месте в любом из hello поддерживается Azure RemoteApp клиентов, включая Android, Mac, Windows Phone, iOS и ПК Windows.

## <a name="create-hello-azure-remoteapp-collection"></a>Создайте коллекцию Azure RemoteApp hello
Ниже приведены шаги toocreate hello вашей коллекции Azure RemoteApp с помощью SSMS.

### <a name="1-create-a-new-windows-vm-from-image"></a>1. Создание новой виртуальной машины Windows из образа
Используйте hello «Windows Server удаленного рабочего стола сеанса узла Windows Server 2012 R2» образ из коллекции toomake hello вашей новой виртуальной Машины.

### <a name="2-install-ssms-from-sql-express"></a>2. Установка SSMS из SQL Express
Перейдите на hello новой виртуальной Машины и перейдите на страницу загрузки toothis: [Microsoft® SQL Server® 2014 Express](https://www.microsoft.com/download/details.aspx?id=42299)

Отсутствует параметр tooonly загрузки SSMS. После загрузки перейдите в каталог установки hello и запустите программу установки tooinstall SSMS.

Необходимо также tooinstall SQL Server 2014 с пакетом обновления 1. Файл для скачивания доступен здесь: [Microsoft SQL Server 2014 с пакетом обновления 1 (SP1)](https://www.microsoft.com/download/details.aspx?id=46694).

SQL Server 2014 с пакетом обновления 1 включает основные функциональные возможности для работы с базой данных SQL Azure.

### <a name="3-run-validate-script-and-sysprep"></a>3. Запуск сценария проверки и средства SysPrep
Сценарий PowerShell с именем Validate hello является рабочий стол hello виртуальной Машины. Запустите его двойным щелчком мыши. Он будет проверить, hello виртуальной Машины готовы toobe, используемое для размещения удаленных приложений. После завершения проверки он запросит toorun sysprep - toorun выберите его.

По завершении работы программы sysprep завершается hello виртуальной Машины.

. в разделе toolearn Дополнительные сведения о создании образа Azure RemoteApp: [как toocreate шаблона RemoteApp образа в Azure](http://blogs.msdn.com/b/rds/archive/2015/03/17/how-to-create-a-remoteapp-template-image-in-azure.aspx)

### <a name="4-capture-image"></a>4. Запись образа
Когда hello, виртуальная машина остановлена, найдите ее в текущем портале hello и записать ее.

toolearn Дополнительные сведения о записи образа, в разделе [запись образа виртуальной машины Microsoft Azure, созданных с помощью hello классической модели развертывания](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

### <a name="5-add-tooazure-remoteapp-template-images"></a>5. Добавление изображений tooAzure шаблона RemoteApp
В hello раздел hello текущей версией портала Azure RemoteApp перейдите на вкладку toohello образы шаблона и нажмите кнопку Добавить. Во всплывающем окне приветствия выберите «Импортировать образ из библиотеки виртуальных машин» и выберите hello образ, который вы только что создали.

### <a name="6-create-cloud-collection"></a>6. Создание облачной коллекции
В текущем портале hello создайте новую коллекцию облако Azure RemoteApp. Выберите образ шаблона только что импортированный вами с помощью SSMS, установленными на нем hello.

![Создание облачной коллекции][2]

### <a name="7-publish-ssms"></a>7. Публикация SSMS
На hello публикации вкладка облачной коллекции, выберите опубликовать приложение из меню "Пуск" Здравствуйте и выберите из списка hello SSMS.

![Публикация приложения][5]

### <a name="8-add-users"></a>8. Добавление пользователей
На вкладке hello доступ пользователя можно выбрать hello пользователей, которые будут иметь коллекции Azure RemoteApp toothis доступа, которая включает только SSMS.

![Добавить пользователя][6]

### <a name="9-install-hello-azure-remoteapp-client-application"></a>9. Установить клиентское приложение hello Azure RemoteApp
Клиент Azure RemoteApp можно скачать и установить отсюда: [Скачивание | Azure RemoteApp](https://www.remoteapp.windowsazure.com/en/clients.aspx)

## <a name="configure-azure-sql-server"></a>Настройка Azure SQL Server
Hello только tooensure, которая обслуживает Azure — требуется настройка включено для hello брандмауэра. При использовании этого решения, то вам не требуется tooadd любом брандмауэре hello tooopen адресов IP. Hello сетевой трафик, который может быть toohello SQL Server — от других служб Azure.

![Разрешение Azure][4]

## <a name="multi-factor-authentication-mfa"></a>Многофакторная проверка подлинности (MFA)
Многофакторную проверку подлинности можно включить специально для этого приложения. Go toohello вкладке приложений в Azure Active Directory. Здесь вы найдете запись для Microsoft Azure RemoteApp. Если щелкнуть это приложение и затем настройте, вы увидите hello страницу под которой вы можете включить многофакторную проверку Подлинности для этого приложения.

![Включение MFA][3]

## <a name="audit-user-activity-with-azure-active-directory-premium"></a>Аудит действий пользователей с помощью Azure Active Directory Premium
Если у вас Azure AD Premium, то у вас есть tooturn его на в hello лицензий раздела каталога. С помощью Premium включена можно назначать пользователей toohello уровня Premium.

При переходе пользователя tooa в Azure Active Directory можно переходить tooAzure входа сведения для действия вкладку toohello toosee RemoteApp.

## <a name="next-steps"></a>Дальнейшие действия
После выполнения всех hello выше действия, необходимо будет toorun hello Azure RemoteApp клиента и в журнал с назначенный пользователь. Откроется с помощью SSMS как одно из приложений и запустить его как если бы она была установлена на компьютере с SQL server tooAzure доступа.

Дополнительные сведения о как toomake hello tooSQL подключения базы данных см. в разделе [подключать tooSQL базы данных SQL Server Management Studio и выполнить пробный запрос T-SQL](sql-database-connect-query-ssms.md).

Пока что у нас всё. Вот и все!

<!--Image references-->
[1]: ./media/sql-database-ssms-remoteapp/ssms.png
[2]: ./media/sql-database-ssms-remoteapp/newcloudcollection.png
[3]: ./media/sql-database-ssms-remoteapp/mfa.png
[4]: ./media/sql-database-ssms-remoteapp/allowazure.png
[5]: ./media/sql-database-ssms-remoteapp/publish.png
[6]: ./media/sql-database-ssms-remoteapp/user.png