---
title: "aaaUsing Office Azure RemoteApp. | Документы Microsoft"
description: "Узнайте, как Office и Azure RemoteApp работают вместе"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: f1773baf-8aa1-423c-a2f9-e4679e0463d3
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: d065c1a0a2191c9e2e405264a835cecf791d6ab7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="using-office-with-azure-remoteapp"></a>Использование Office с Azure RemoteApp
> [!IMPORTANT]
> Мы выводим службу Azure RemoteApp из эксплуатации 31 августа 2017 года. Чтение hello [объявления](https://go.microsoft.com/fwlink/?linkid=821148) подробные сведения.
> 
> 

Существует два способа разместить приложения Office в Azure RemoteApp: с помощью пакета Office 365 профессиональный плюс или пробной версии Office 2013 профессиональный плюс.

**А вы знали, что в ближайшее время мы заменим эту статью новой, более информативной статьей? Извлечение [как toouse подписки Office 365 в Azure RemoteApp](remoteapp-officesubscription.md). Она охватывает все hello сведения, необходимые для использования в Office 365 + Azure RemoteApp.**

## <a name="office-365-proplus"></a>Office 365 профессиональный плюс.
Можно создать с помощью hello Office 365 профессиональный плюс образа шаблона коллекции RemoteApp. Этот параметр позволяет tooextend вашей tooRemoteApp службы Office 365. Необходимо иметь существующий план подписки и пользователи должны иметь лицензию для Office 365 профессиональный плюс службы, автономная hello или с помощью планов обслуживания hello Office 365.

RemoteApp поддерживает активацию на общедоступном компьютере для Office 365. Если включить общий активацию компьютера, а также используется hello [средство развертывания Office](http://www.microsoft.com/download/details.aspx?id=36778) для установки, Office 365 профессиональный плюс устанавливает без активации. Когда пользователь входит в коллекцию, которая содержит Office 365, Microsoft Office проверяет toosee hello пользователь подготовлен для Office 365 профессиональный плюс. Если Да, Office временно активирует Office 365 профессиональный плюс - активацию сохраняется до этого признаки пользователей hello обслуживания.

toouse активации общих компьютера Office 365 требуется toocreate [пользовательский шаблон](remoteapp-create-custom-image.md) и установить Office 365 профессиональный плюс, следуя [этим указаниям](https://technet.microsoft.com/library/dn782858.aspx).

Вы можете управлять лицензии пользователей Office 365 в hello [портал администрирования Office 365](https://portal.office365.com/). Узнайте больше о [планах обслуживания Office 365](http://technet.microsoft.com/library/office-365-plan-options.aspx).  

## <a name="office-2013-professional-plus-trial"></a>Пробная версия Office 2013 профессиональный плюс
Во время 30-дневную пробную версию RemoteApp можно использовать образ шаблона toocreate коллекции RemoteApp для hello Office 2013 профессиональный плюс (ознакомительная версия). Можно назначить toothis пользователи пробной версии коллекции, с помощью их рабочих учетных записей Azure Active Directory или учетные записи Майкрософт. Дополнительная подписка не требуется.

Это отличная возможность tookick hello шины и хорошо почувствовать Office в RemoteApp. Тем не менее, этот вариант предназначен исключительно для оценки и тестирования. Коллекции RemoteApp, созданного с помощью шаблона образа hello Office 2013 профессиональный плюс (ознакомительная версия) не может быть перенесен tooproduction режиме и в конце hello hello пробный период будет отключена.

## <a name="switching-from-trial-tooproduction"></a>Переключение с пробной версии tooproduction
При запуске 30-дневной бесплатной пробной версии Примечание в раздел RemoteApp портала hello hello будет указано, сколько осталось в пробной версии hello, прежде чем выполнить tooa tootransition платной учетной записи. Вы можете активировать tooproduction вашей учетной записи и ключ режимом с помощью ссылки hello в этой заметке.

При активации учетной записи, это повлияет на всем коллекциям RemoteApp hello в вашей учетной записи.

* Коллекции, которые работают с приветствия Windows Server 2012 R2 и Office 365 профессиональный плюс образы шаблонов hello перейдет tooproduction без проблем. Все данные и параметры пользователей, включая текущие сеансы, останутся без изменений.
* При наличии пользовательских образов шаблонов коллекции, использующие эти образы, также переносятся без изменений.
* образ шаблона Hello Office 2013 профессиональный плюс (ознакомительная версия) предназначен для только для оценки. Коллекции, выполнив этот образ шаблона не может быть перенесен tooproduction. Их состояние изменится на "Отключено".

Если не перевести tooproduction режиме, hello истечение срока действия пробной версии, коллекциям RemoteApp будет отключена. Не беспокойтесь — параметры и данные пользователей сохраняются для другого 90 дней, по-прежнему можно активировать режим tooproduction службы и коммутатор без потери данных.

