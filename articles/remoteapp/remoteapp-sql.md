---
title: "aaaSQL Azure Azure RemoteApp. | Документы Microsoft"
description: "Узнайте, как toouse SQL Azure с Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
editor: 
ms.assetid: 35f81d75-bfd7-4980-807e-00339f2cb2a4
ms.service: remoteapp
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: compute
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: fec4cb1f1ab3cde03b6ff613650e01bae3552824
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="sql-azure-with-azure-remoteapp"></a>Использование SQL Azure с Azure RemoteApp
> [!IMPORTANT]
> Мы выводим службу Azure RemoteApp из эксплуатации 31 августа 2017 года. Чтение hello [объявления](https://go.microsoft.com/fwlink/?linkid=821148) подробные сведения.
> 
> 

Часто в том случае, когда клиенты выбирают toohost с приложениями Windows в облаке hello Azure RemoteApp. также должен быть toomigrate облако свои данные, например серверы SQL Server в hello целое облако развертывания. Это позволяет создать полностью облачное решение, доступ к которому можно получить в любое время с любого устройства и из любого места с помощью Azure RemoteApp. Ниже приведены ссылки и ссылки на вместе с toohelp руководство ранее с этим процессом.  

## <a name="migrate-your-sql-data"></a>Перенос данных SQL
Начать с [миграция tooAzure базы данных SQL Server база данных SQL](../sql-database/sql-database-cloud-migrate.md). 

## <a name="configure-azure-remoteapp"></a>Настройка Azure RemoteApp
Разместите приложение Windows в Azure RemoteApp. Ниже приведено обобщенное пошаговое руководство.

1. Создать hello [Azure RemoteApp шаблона виртуальной Машины](remoteapp-imageoptions.md). 
2. Приложение hello требуется установите на hello виртуальной Машины.
3. Настройка приложения hello, он подключается toohello баз данных SQL Server и убедитесь, что он работает.
4. Hello Sysprep и завершите работу виртуальной Машины. Запишите образ этой виртуальной машины для использования с Azure. **Примечание:** потребуется tooensure, приложение hello находится может tooretain hello DB соединений со сведениями о процессе sysprep hello. Если приложение hello сведения о соединении hello DB tooretain не удается, может потребоваться поставщику hello tooengage toocheck приложения hello как можно указать строку подключения hello.
5. Импортировать hello пользовательского образа в Azure RemoteApp библиотеку при выборе hello правильную географическое расположение, находящийся в развертывании SQL Azure. 
6. Разверните коллекции RemoteApp в hello и те же данные центру как развертывание SQL Azure с помощью hello выше шаблона и публикация приложения hello. Развертывание Azure RemoteApp в hello же центре обработки данных с развертыванием SQL Azure помогает обеспечить максимальную скорость подключения hello и уменьшить задержку. 

## <a name="app-and-sql-configuration-considerations"></a>Рекомендации по конфигурации SQL и приложения
Существует несколько точек tooconsider при использовании Azure SQL RemoteApp:

Дополнительные сведения [как брандмауэр базы данных Azure SQL tooconfigure](../sql-database/sql-database-firewall-configure.md). Фрагмент кода из состояния статьи hello, «изначально все сервера базы данных SQL Azure tooyour доступа заблокирован брандмауэром hello. В порядке toobegin с помощью сервера базы данных SQL Azure необходимо перейдите toohello классический портал и укажите одно или несколько правил брандмауэра уровня сервера, позволяющие сервера базы данных SQL Azure tooyour доступа. Воспользуйтесь toospecify правила брандмауэра hello какой IP-адрес в диапазоне от Интернета разрешены hello и ли приложения Azure может попытаться выполнить tooconnect tooyour базы данных Azure SQL server».

Кроме того, когда компьютер пытается tooconnect tooyour базы данных сервера из hello Интернета, брандмауэр hello проверяет hello, рассчитанные на IP-адрес запроса hello к полному набору hello уровня сервера и (при необходимости) правила брандмауэра уровня базы данных. «Если в одном из диапазонов hello, указанных в правилах брандмауэра уровня сервера hello hello IP-адреса запроса hello, hello предоставляется возможность подключения сервера базы данных SQL Azure tooyour.» Следовательно, мы можем использовать диапазоны IP-адресов, а не только отдельные исходные IP-адреса.

Следуйте инструкциям в разделе шаг за шагом hello [как: Настройка параметров брандмауэра в базе данных SQL с помощью портала Azure hello](../sql-database/sql-database-configure-firewall-settings.md) toospecify hello, диапазон IP-адресов. При настройке правил брандмауэра SQL hello укажите hello диапазон IP-подсети hello, который указан для hello коллекции Azure RemoteApp. Это позволяет серверы hello ARA tooconnect toohello баз данных SQL Server несмотря на то, что они будут динамически назначаемый IP-адресов.

## <a name="troubleshooting"></a>Устранение неполадок
Возникают hello клиентское приложение, размещенное в Azure RemoteApp, которая подключается tooa SQL с помощью базы данных там, где размещен в Azure или локально является замедление может быть несколько причин почему.  

* Задержки сети для вашего устройства tooAzure высокого уровня. Переместите toohello лучшим и наиболее быстрый сетевое подключение, которое можно для достижения оптимальной производительности. Используйте [azurespeed.com](http://azurespeed.com/) как tootest общее средство центра обработки данных tooAzure задержки устройства.  
* Клиентское приложение, размещенное в Azure RemoteApp, перегружено. Выберите другой тарифный план, например «Премиум». Это повысит производительность. Другое приложение потребляет ресурсы hello toomonitor достаточно: во время активного сеанса выполнения сочетания клавиш ctrl-alt-end которой запустится hello SAS на экране, выберите диспетчер задач и следите за использованием ресурсов для вашего приложения.
* SQL Server сильно загружен или не оптимизирован. Следуйте рекомендациям SQL для устранения неполадок. 

