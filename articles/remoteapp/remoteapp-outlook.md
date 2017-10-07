---
title: "aaaUsing Outlook в Azure RemoteApp | Документы Microsoft"
description: "Узнайте, как tooconfigure и использовать Outlook в Azure RemoteApp | Microsoft Azure"
services: remoteapp
documentationcenter: 
author: pavithir
manager: mbaldwin
ms.assetid: cb2a498f-9539-4522-a874-542114926a61
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 119d2629ac47bd8d20d617985a9b488068aa959f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="using-microsoft-outlook-in-azure-remoteapp"></a>Использование Microsoft Outlook в Azure RemoteApp
> [!IMPORTANT]
> Мы выводим службу Azure RemoteApp из эксплуатации 31 августа 2017 года. Чтение hello [объявления](https://go.microsoft.com/fwlink/?linkid=821148) подробные сведения.
> 
> 

Azure RemoteApp поддерживает Microsoft Outlook O365. Дополнительные сведения см. в статье об [использовании Office в Azure RemoteApp](remoteapp-officesubscription.md). Есть несколько рекомендаций, касающихся настроек Outlook при использовании в Azure RemoteApp.

## <a name="cached-mode"></a>Режим кэширования данных
Режим кэширования данных является рекомендуемой конфигурацией при использовании Outlook в Azure RemoteApp. При настройке учетной записи Outlook 2013 toouse кэширования сервера Exchange, Outlook 2013 работает с локальной копии hello Microsoft почтовый ящик Exchange пользователя, хранящиеся в файле данные в автономном режиме (OST-файл) на компьютере пользователя hello, вместе с hello автономную адресную книгу (АВТОНОМНОЙ АДРЕСНОЙ КНИГИ). кэшированный почтовый ящик Hello и автономной адресной книги периодически обновляются из hello службы Office 365. Дополнительные сведения о [hello различий между режимами кэшированных и online](https://technet.microsoft.com/library/jj683103.aspx).

Hello пользователь может выбрать **хранятся на сервере** или **оперативный режим** во время установки учетная запись, или путем изменения параметров учетной записи hello. Также можно развернуть один режим или hello других с помощью hello развертывания Office (OCT) или групповой политики.  

См. [пошаговые инструкции по включению режима кэширования данных](https://technet.microsoft.com/library/c6f4cad9-c918-420e-bab3-8b49e1885034#proc).

## <a name="search"></a>Поиск
Использование поиска в Outlook имеет определенные ограничения в Azure RemoteApp. Azure RemoteApp использует сеансы пользователей tooaccommodate пула виртуальных машин. Индексирование поиска зависит от идентификатора компьютера hello, отличается для разных виртуальных машин. Возможна ситуация, при каждом входе пользователя в Azure RemoteApp, являясь направленной tooa новой виртуальной Машины. Это будет означать, если мы включили локального поиска, hello индексатор будет запускаться при каждом изменении идентификатор компьютера hello (когда hello пользователя находится в другой виртуальной Машины). В зависимости от размера hello hello. Файл OST hello индексатор может занять длительное время toocomplete и использовать ресурсы, необходимые для других приложений. Поиск не только будет медленным, но и может оказаться безрезультатным. С помощью профиля оперативного режима учетной записи будет обойти эту проблему, но общая производительность бы упала из-за отсутствия toohello локальный кэш (см. ссылку выше, Дополнительные сведения о hello различие между режимом кэширования и online hello). К сожалению, в Outlook 2013 индексированный или локальный поиск нельзя отключить, а поиск в Интернете нельзя включить по умолчанию.

