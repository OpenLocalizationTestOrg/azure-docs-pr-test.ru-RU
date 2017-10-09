---
title: "aaaWhat находится в образах шаблона hello Azure RemoteApp? | Документация Майкрософт"
description: "Дополнительные сведения об образах шаблона hello, входящий в состав Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 7f8442b2-81da-421e-a453-aa53ba2066b7
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: ea012cec8dc581a8bd4a5a138ce302de19d5c6af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-in-hello-azure-remoteapp-template-images"></a>Что такое hello образы шаблонов Azure RemoteApp?
> [!IMPORTANT]
> Мы выводим службу Azure RemoteApp из эксплуатации 31 августа 2017 года. Чтение hello [объявления](https://go.microsoft.com/fwlink/?linkid=821148) подробные сведения.
> 
> 

Подписка на Azure RemoteApp включает три образа шаблонов:

* Windows Server 2012
* Microsoft Office 365 профессиональный плюс (необходима подписка на Office 365);
* Microsoft Office 2013 профессиональный плюс (только пробная версия)

> [!IMPORTANT]
> Подписки Azure RemoteApp предоставляет вам доступ к программному обеспечению toohello в образах hello, за исключением hello Office 365 профессиональный плюс, требующий отдельной подписки, и Office 2013, который не может использоваться в производственной среде. Это означает, что могут обмениваться hello программ или приложений на образы шаблонов hello с пользователями. Например при создании коллекции, использующего образ Windows Server 2012 R2 hello, System Center Endpoint Protection можно опубликовать для пользователей tooaccess через RemoteApp.
> 
> Извлечение hello [сведения о лицензировании удаленных приложений RemoteApp](remoteapp-licensing.md) для получения дополнительной информации. И [Office с помощью Azure RemoteApp.](remoteapp-o365.md) для hello сведения о лицензировании Office.
> 
> 

Ниже описывает содержимое каждого образа.

## <a name="windows-server-2012-r2--hello-vanilla-image"></a>Windows Server 2012 R2 («hello соответствующего ванили образ»)
Этот образ основан на операционной системе Microsoft Windows Server 2012 R2 Datacenter и имеет hello установлены следующие роли и компоненты toomeet hello требованиям к образам шаблона Azure RemoteApp:

* .NET Framework 4.5, 3.5.1, 3.5
* Возможности рабочего стола
* Службы рукописного ввода
* Media Foundation
* Узел сеансов удаленных рабочих столов
* Windows PowerShell 4.0
* Windows PowerShell ISE
* Поддержка WoW64

Этот образ также имеет следующие приложения, установленные hello:

* Adobe Flash Player
* Microsoft Silverlight
* Microsoft System Center 2012 Endpoint Protection
* Проигрыватель Windows Media (Microsoft)

## <a name="microsoft-office-365-proplus-subscription-required"></a>Microsoft Office 365 профессиональный плюс (необходима подписка)
Office 365 hello наиболее запрошенное приложение, поэтому мы создали «custom» образ для вас toowork с.

Этот образ является расширением соответствующего ванили изображения hello и hello следующие компоненты Microsoft Office 365 профессиональный плюс; установлен в дополнение к этому toohello компонентами, описанными в образ Windows Server 2012 R2 hello:

* Access
* Excel
* Lync
* OneNote
* OneDrive для бизнеса (Обратите внимание, что агент синхронизации hello не поддерживается для использования с Azure RemoteApp)
* Outlook
* PowerPoint
* Word
* Средства проверки правописания Microsoft Office

изображение Hello также Visio Pro и Pro проекта.

И hello приложений, а также следующие:

* SQL Native Client
* Драйвер ODBC
* Клиент интеллектуального анализа данных SQL Server
* Клиент MasterDataServices
* Microsoft Publisher
* PowerQuery
* PowerMap

Полный набор функций приложений Office 365 профессиональный плюс доступен только пользователям плана Office 365 профессиональный плюс. Дополнительные сведения о подписке Office 365 hello планов в разделе [планы службы Office 365](http://technet.microsoft.com/library/office-365-plan-options.aspx). У вас еще остались вопросы? Извлечение hello [Office 365 + RemoteApp](remoteapp-o365.md) сведения. Прочитайте статью hello [как toouse подписки Office 365 в Azure RemoteApp](remoteapp-officesubscription.md).

Обратите внимание, что Office 365 профессиональный плюс toolicense Visio Pro и проект Pro отдельно - все их собственной лицензии.

## <a name="microsoft-office-2013-professional-plus-trial-only"></a>Microsoft Office 2013 профессиональный плюс (только пробная версия)
Во время hello бесплатного пробного периода можно протестировать службу hello с изображением hello Office 2013.

Этот образ является расширением соответствующего ванили изображения hello и hello следующие компоненты Microsoft Office 2013 профессиональный плюс установлен в дополнение к этому toohello компонентами, описанными в образ Windows Server 2012 R2 hello:

* Access
* Excel
* Lync
* OneNote
* OneDrive для бизнеса (Обратите внимание, что агент синхронизации hello не поддерживается для использования с Azure RemoteApp)
* Outlook
* PowerPoint
* Project
* Visio
* Word
* Средства проверки правописания Microsoft Office

> [!IMPORTANT]
> **Юридическая информация**. Этот образ не включает в себя лицензию Microsoft Office и *не может использоваться в производственных целях*. изображение Office 2013 профессиональный плюс Hello предназначено только для пробного использования. Следует toouse приложений Office в Azure RemoteApp для рабочей среды необходимо toouse hello Office 365 профессиональный плюс изображения. Дополнительные сведения о лицензировании Office см. в статье [Использование Office с Azure RemoteApp](remoteapp-o365.md).
> 
> 

