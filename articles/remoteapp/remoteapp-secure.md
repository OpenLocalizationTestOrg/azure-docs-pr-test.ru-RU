---
title: "aaaSecure приложениям и ресурсам в Azure RemoteApp | Документы Microsoft"
description: "Узнайте, как toolock работу приложения и ресурсы в Azure RemoteApp"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 7fbade87-a453-426d-bfa5-c72227ea83cd
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 26325826e92855a12a0087f19a3e32cbe1116449
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="secure-apps-and-resources-in-azure-remoteapp"></a>Защита приложений и ресурсов в Azure RemoteApp
> [!IMPORTANT]
> Мы выводим службу Azure RemoteApp из эксплуатации 31 августа 2017 года. Чтение hello [объявления](https://go.microsoft.com/fwlink/?linkid=821148) подробные сведения.
> 
> 

Azure RemoteApp предоставляет пользователям доступ toocentrally приложений под управлением Windows, который позволяет контролировать, какие пользователи могут и не поддерживается.  Это особенно полезно в тех случаях, когда hello пользователь подключается из неуправляемых устройств (например, их личных Macbook) и хотите toocontrol hello пользователю доступ или столкнуться.

Например если вы используете Active Directory для проверки подлинности пользователя, и требуется tooprevent пользователей копировать данные из приложения, можно настроить пользователям tooblock групповой политики удаленного рабочего стола копирование данных.

Другой пример — Если требуется доступ к Интернету tooblock для конкретного приложения в коллекции. Можно создать правило брандмауэра Windows, что блоки hello доступа при создании образа hello для коллекции.

## <a name="implementation-options"></a>Варианты реализации
  Ниже приведены параметры ключа реализации hello, которые можно использовать отдельно или вместе при необходимости.

1. Если в коллекции RemoteApp присоединенных к домену можно применять любой [групповой политики](https://technet.microsoft.com/library/cc725828.aspx) (за исключением hello hello Idle отключить время ожидания политик и описано [здесь](../azure-subscription-service-limits.md)).
2. В качестве альтернативного tooGroup политика (если коллекции не присоединен к домену, или у вас нет необходимых прав hello в AD), можно настроить [локальной политики](https://technet.microsoft.com/library/cc775702.aspx) в вашем образе шаблона.  Обратите внимание, что в случае конфликта групповые политики имеют более высокий приоритет, чем локальные политики.
3. Некоторые параметры операционной системы или приложения не могут быть изменены через политику, но может быть через раздел реестра, используя hello [средство RegEdit](remoteapp-hybridtrouble.md) во время настройки образа шаблона.
4. Можно использовать [брандмауэра Windows](http://windows.microsoft.com/en-US/windows-8/Windows-Firewall-from-start-to-finish) toocontrol tooand доступа к сети с компьютера hello, где выполняется приложение hello. Убедитесь, что не блокируют hello URL-адреса и порты, определенные здесь.
5. Можно использовать [AppLocker](https://technet.microsoft.com/library/hh831440.aspx) toocontrol, который пользователи приложений и файлов может выполняться. Например пользователям можно понять, как toorun приложения, не публиковались, но доступны в hello изображения вы использовали toocreate hello коллекции - AppLocker можно заблокировать это.

## <a name="detailed-information"></a>Подробные сведения
* Hello следующими политиками служб удаленных рабочих СТОЛОВ, скорее всего, toobe наиболее полезен:
  * [Перенаправление устройств и ресурсов](https://technet.microsoft.com/library/ee791794.aspx)
  * [Перенаправление принтеров](https://technet.microsoft.com/library/ee791784.aspx)
  * [Профили](https://technet.microsoft.com/library/ee791865.aspx).
* Здравствуйте, Настройка перенаправлений через модуль RemoteApp PowerShell Примечание (как показано [здесь](remoteapp-redirection.md)) зависит от политики hello tooenforce машины клиента hello, поэтому если безопасность является основной целью hello нужно tooenforce hello политику с помощью Здравствуйте, локальная политика образ шаблона или с помощью групповой политики.
* [Политики Windows Server 2012 R2](https://technet.microsoft.com/library/hh831791.aspx).
* [Office 2013 политики](https://technet.microsoft.com/library/cc178969.aspx) (включая [как toocustomize hello инструментов Office](https://technet.microsoft.com/library/cc179143.aspx)).

