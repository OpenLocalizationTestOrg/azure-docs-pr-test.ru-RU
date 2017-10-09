---
title: "aaaKey различия между Azure и Azure стека при использовании службы и создание приложений | Документы Microsoft"
description: "Что необходимо tooknow при использовании служб или создание приложений для Azure стека."
services: azure-stack
documentationcenter: 
author: twooley
manager: byronr
editor: 
ms.assetid: c81f551d-c13e-47d9-a5c2-eb1ea4806228
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/2/2017
ms.author: twooley
ms.openlocfilehash: e302f20aeb3c74f944cb3daaee7e0db073ab5bfa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="key-considerations-using-services-or-building-apps-for-azure-stack"></a>Основные особенности: с помощью служб или создание приложений для Azure стека

При использовании служб или создание приложений для Azure стека, необходимо понимать, что существуют различия между стек Azure и Azure. В этой статье содержатся рекомендации по ключа Обзор hello, при ориентировании стек Azure в гибридной облачной среды разработки.

## <a name="overview"></a>Обзор

Azure Stack ― это гибридная облачная платформа, позволяющая использовать службы Azure из центра обработки данных вашей компании или поставщика услуг. Как разработчик можно создавать приложения, работающих на стек Azure. Можно использовать для развертывания этих приложений tooAzure стека, tooAzure, или можно действительно построения гибридного приложения, использующие подключения hello облака стек Azure и Azure.

Администратору облака Azure стека или поставщика услуг сообщит службы, которые доступны для вас toouse и поддержке tooget. Они предлагают эти службы с помощью настраиваемого планы и предложения.

Hello Azure техническое содержимое предполагается, что приложения разрабатываются для службы Azure вместо Azure стека. При построении и развертывании приложений tooAzure стека, необходимо понять ключевые различия, такие как:

* Стек Azure предоставляет подмножество hello служб и функций, доступных в Azure.
* Вашей компании или поставщикам услуг можно выбрать службы, которые они хотят toooffer. Сюда входят настраиваемые службы или приложения.
* Необходимо использовать hello исправить Azure стека конечную точку (например, hello URL-адреса портала адрес hello и конечную точку диспетчера ресурсов Azure hello).
* Необходимо использовать версии PowerShell и API, которые поддерживаются Azure стека. Это гарантирует, что приложения будут работать в стек Azure и Azure.

## <a name="cheat-sheet-high-level-differences"></a>Памятка: различия высокого уровня

Hello следующей таблице описаны hello высокоуровневые различия между стек Azure и Azure. Имейте в виду при разработке для Azure стека или использование служб Azure стека.

| Область | (Глобальная) Azure | Azure Stack |
| -------- | ------------- | ----------|
| Кто работает его? | Microsoft | Поставщик вашей компании или службы.|
| Кому можно обращаться для получения поддержки? | Microsoft | Для пакета средств разработки Azure стека посетите hello [форумы Майкрософт](https://social.msdn.microsoft.com/Forums/home?forum=azurestack). Так как пакет средств разработки hello среды оценки, не поддерживается официальный доступным через службы поддержки клиентов Майкрософт (CSS).
| Доступные службы | Просмотреть список hello [продуктах Azure](https://azure.microsoft.com/services/?b=17.04b). Доступные службы зависят от региона Azure. | Стек Azure поддерживает подмножество функций служб Azure. <br><br>Набор служб зависит toooffer что выбирает вашей компании или поставщикам услуг.
| Azure конечную точку диспетчера ресурсов * | https://management.azure.com | Для пакета средств разработки hello: https://management.local.azurestack.external
| Портал URL-адрес * | [https://portal.azure.com](https://portal.azure.com) | Для пакета средств разработки hello: https://portal.local.azurestack.external
| Регион | Можно выбрать область, которая требуется toodeploy для. | Для пакета средств разработки hello, всегда будет иметь область **локальной**. <br><br>пакет средств разработки Hello поддерживает только одну область.
| Группы ресурсов | Группа ресурсов может охватывать несколько регионов. | Для пакета средств разработки hello есть только один регион.
|Поддерживаемых пространств имен, типов ресурсов и версии API | Здравствуйте, последняя версия (или более ранних версий, которые еще не рекомендуется к использованию). | Стек Azure поддерживает конкретных версий. См. раздел «Требования к версии» hello данной статьи.
| | |

* Если вы являетесь оператором облако Azure стека, см. раздел [использование hello порталы администратора и пользователя в Azure стека](azure-stack-manage-portals.md) сведения о hello администратора портала и администратора диспетчера ресурсов конечной точки URL-адреса.

## <a name="helpful-tools-and-best-practices"></a>Полезные средства и рекомендации
 
 Корпорация Майкрософт предлагает несколько средств и рекомендации, которые позволяет разрабатывать приложения для Azure стека.

| Рекомендации | Ссылки | 
| -------- | ------------- | 
| Установите необходимые инструментальные средства hello на рабочей станции разработчика. | - [Установка PowerShell](azure-stack-powershell-install.md)<br>- [Загрузка средств](azure-stack-powershell-download.md)<br>- [Настройка PowerShell](azure-stack-powershell-configure-user.md)<br>- [Установка Visual Studio](azure-stack-install-visual-studio.md) 
| Просмотрите сведения о следующих hello.<br>-Рекомендации по шаблонам azure Resource Manager<br>-Как шаблоны toofind краткое руководство<br>-Используйте toohelp модуль политики, используйте Azure toodevelop стек Azure | [Разработка для Azure Stack](azure-stack-developer.md) | 
| Просмотрите и выполните hello рекомендации для шаблонов. | [Примеры использования шаблонов диспетчера ресурсов](https://github.com/Azure/azure-quickstart-templates/blob/master/1-CONTRIBUTION-GUIDE/best-practices.md#best-practices)
| | |

## <a name="version-requirements"></a>Требования к версии

Стек Azure поддерживает конкретных версий Azure PowerShell и Azure API службы. Поддерживаемые версии tooensure, приложение можно развернуть tooboth стека Azure и tooAzure необходимо использовать.

необходимо использовать правильную версию Azure PowerShell, используйте toomake [профили версии API](azure-stack-version-profiles.md). toodetermine hello последнего API версии профиля, который можно использовать, необходимо знать, какие сборки стек Azure, вы используете. Эти сведения можно получить у администратора Azure стека.

>[!NOTE]
 Если вы используете hello Azure стека Development Kit и иметь административный доступ, в разделе hello «Определение текущей версии hello» [управления обновлениями](https://docs.microsoft.com/azure/azure-stack/azure-stack-updates#determine-the-current-version) toodetermine hello Azure стека сборки.

Для других API-интерфейсов запустите PowerShell команды toooutput hello, пространства имен, типов ресурсов и версии API, которые поддерживаются в вашей подписке Azure стека hello. Заметьте, что по-прежнему могут быть различия на уровне свойств. (Для этого toowork команды уже должны быть [установлен](azure-stack-powershell-install.md) и [настроен](azure-stack-powershell-configure-user.md) PowerShell для Azure стека среды. Необходимо также иметь на предложение подписки tooan стека Azure.)

 ```powershell
Get-AzureRmResourceProvider | Select ProviderNamespace -Expand ResourceTypes | Select * -Expand ApiVersions | `
Select ProviderNamespace, ResourceTypeName, @{Name="ApiVersion"; Expression={$_}} 
```

Пример выходных данных (усечение): ![пример выходных данных команды Get-AzureRmResourceProvider](media/azure-stack-considerations/image1.png)
 
## <a name="next-steps"></a>Дальнейшие действия

Более подробные сведения о различиях на уровне службы см.

* [Рекомендации для виртуальных машин в стек Azure](azure-stack-vm-considerations.md)
* [Рекомендации для хранилища в стек Azure](azure-stack-acs-differences.md)
* [Рекомендации по сети стек Azure](azure-stack-network-differences.md)

