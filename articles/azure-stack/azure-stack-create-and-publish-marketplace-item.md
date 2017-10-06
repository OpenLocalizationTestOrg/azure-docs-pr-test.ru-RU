---
title: "aaaCreate и публикации Marketplace элемента в стек Azure | Документы Microsoft"
description: "Создание и публикация элементов Marketplace Azure стека."
services: azure-stack
documentationcenter: 
author: ErikjeMS
manager: byronr
editor: 
ms.assetid: 77e5f60c-a86e-4d54-aa8d-288e9a889386
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: erikje
ms.openlocfilehash: 6f6a7af96f9d8de9098ac7eee4ba2ac9bc3d6a50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-publish-a-marketplace-item"></a>Создание и публикация элемента Marketplace
## <a name="create-a-marketplace-item"></a>Создание элемента Marketplace
1. [Загрузить](http://www.aka.ms/azurestackmarketplaceitem) средство упаковщик Azure коллекции hello и Azure Marketplace стека пример hello элемента.
2. Откройте элемент Marketplace образец hello и переименовать hello **SimpleVMTemplate** папки. (Используйте hello точно такое же имя как элемент Marketplace — например, **Contoso.TodoList**.) Эта папка содержит:
   
       /Contoso.TodoList/
       /Contoso.TodoList/Manifest.json
       /Contoso.TodoList/UIDefinition.json
       /Contoso.TodoList/Icons/
       /Contoso.TodoList/Strings/
       /Contoso.TodoList/DeploymentTemplates/
3. [Создание шаблона Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) или выберите шаблон из GitHub. элемент Marketplace Hello использует этот шаблон toocreate ресурса.
4. toomake том, что ресурс hello успешно развернуто, проверка шаблона hello с hello интерфейсов API стека Microsoft Azure.
5. Если шаблон использует образ виртуальной машины, следуйте инструкциям hello слишком[добавьте tooAzure образа виртуальной машины стека](azure-stack-add-vm-image.md).
6. Сохранить шаблон диспетчера ресурсов Azure в hello **/Contoso.TodoList/DeploymentTemplates/** папки.
7. Выберите hello значки и текст для элемента Marketplace. Добавление значков toohello **значки** папки и добавьте текст toohello **ресурсов** файла в hello **строки** папки. Используйте hello малый, средний, большой и расширенными соглашение об именовании для значков. В разделе [элемент Marketplace Справочник по пользовательскому Интерфейсу](#reference-marketplace-item-ui) подробное описание.
   
   > [!NOTE]
   > Все размеры четыре значка (небольшой, средний, большой, широкий) являются обязательными для построение элемента Marketplace hello правильно.
   > 
   > 
8. В hello **manifest.json** измените **имя** toohello имя вашего элемента Marketplace. Кроме того, изменить **издатель** tooyour имя или название компании.
9. В разделе **артефакты**, изменить **имя** и **путь** toohello правильные сведения для шаблона диспетчера ресурсов Azure hello, которую вы включили.
   
         "artifacts": [
            {
                "name": "Type your template name",
                "type": "Template",
                "path": "DeploymentTemplates\\Type your path",
                "isDefault": true
            }
10. Замените **Мои элементы Marketplace** со списком категорий hello, которой должен отображаться элемент Marketplace.
    
             "categories":[
                 "My Marketplace Items"
              ],
11. Дальнейшая toomanifest.json изменения, см. в разделе слишком[ссылка: Marketplace элемента manifest.json](#reference-marketplace-item-manifestjson).
12. папки toopackage hello в файл .azpkg откройте командную строку и выполните следующую команду hello:
    
        AzureGalleryPackager.exe package –m <path toomanifest.json> -o <output location for hello package>
    
    > [!NOTE]
    > Hello полный путь toohello выходных данных должен существовать пакет. Например если выходной путь hello C:\MarketPlaceItem\yourpackage.azpkg, папка hello C:\MarketPlaceItem должна существовать.
    > 
    > 

## <a name="publish-a-marketplace-item"></a>Публикация элемента Marketplace
1. Используйте PowerShell или обозреватель хранилищ Azure tooupload ваш Marketplace элемента (.azpkg) tooAzure хранилища больших двоичных объектов. Можно передать хранилища Azure стека toolocal или отправить tooAzure хранилища. (Это временное местоположение для hello пакета). Убедитесь, что этот hello большой двоичный объект является общедоступным.
2. Hello клиентской виртуальной машины в среде Microsoft Azure стека hello убедитесь в том, что сеанс PowerShell настраиваются с учетными данными администратора службы. Инструкции можно найти tooauthenticate PowerShell Azure стека в [развертывания шаблона с помощью PowerShell](azure-stack-deploy-template-powershell.md).
3. Используйте hello **AzureRMGalleryItem добавить** элемента PowerShell командлет toopublish hello Marketplace tooAzure стека. Например:
   
       Add-AzureRMGalleryItem -GalleryItemUri `
       https://sample.blob.core.windows.net/gallerypackages/Microsoft.SimpleTemplate.1.0.0.azpkg –Verbose
   
   | Параметр | Описание |
   | --- | --- |
   | SubscriptionID |Идентификатор подписки администратора. Его можно получить с помощью PowerShell. Если вы предпочитаете tooget его портале hello go toohello поставщик подписки и скопируйте идентификатор подписки hello. |
   | GalleryItemUri |URI большого двоичного объекта для пакета, уже загруженные toostorage коллекции. |
   | Apiversion |Установить в качестве **2015-04-01**. |
4. Go toohello портала. Теперь вы можете просмотреть элемент Marketplace hello hello портале — в качестве администратора или клиента.
   
   > [!NOTE]
   > Hello пакета может занять несколько минут tooappear.
   > 
   > 
5. Ваш Marketplace элемент теперь сохранить toohello стека Azure Marketplace. Вы можете toodelete его из хранилища больших двоичных объектов.
6. Элемент Marketplace можно удалить с помощью hello **AzureRMGalleryItem удаление** командлета. Пример:
   
        Remove-AzureRMGalleryItem -Name Microsoft.SimpleTemplate.1.0.0  –Verbose
   
   > [!NOTE]
   > Hello Marketplace пользовательского интерфейса может показывать ошибку, после удаления элемента. Ошибка toofix hello, нажмите кнопку **параметры** hello портала. Выберите **отменить изменения** под **настройки портала**.
   > 
   > 

## <a name="reference-marketplace-item-manifestjson"></a>Справочные материалы: Manifest.json элемент Marketplace
### <a name="identity-information"></a>Сведения об удостоверении
| Имя | Обязательно | Тип | Ограничения | Описание |
| --- | --- | --- | --- | --- |
| Имя |X |Строка |[A–Z, a–z, 0–9] + | |
| Издатель |X |Строка |[A–Z, a–z, 0–9] + | |
| Version (версия) |X |Строка |[SemVer v2](http://semver.org/) | |

### <a name="metadata"></a>Метаданные
| Имя | Обязательно | Тип | Ограничения | Описание |
| --- | --- | --- | --- | --- |
| DisplayName |X |Строка |Рекомендация 80 знаков |Hello портала могут отображаться ваше имя элемента корректно, если превышает 80 символов. |
| PublisherDisplayName |X |Строка |Рекомендация 30 символов |Hello портала могут отображаться ваше имя издателя корректно, если больше 30 символов. |
| PublisherLegalName |X |Строка |Более 256 символов | |
| Сводка |X |Строка |too100 60 символов. | |
| LongSummary |X |Строка |140 символов too256 |Еще неприменимо в стек Azure. |
| Описание |X |[HTML](https://auxdocs.azurewebsites.net/en-us/documentation/articles/gallery-metadata#html-sanitization) |500 too5, 000 символов. | |

### <a name="images"></a>Образы
Hello Marketplace использует hello следующие значки:

| Имя | Ширина | Высота: | Примечания |
| --- | --- | --- | --- |
| Расширенный |255 пкс |115 пкс |Требуется всегда |
| Крупный |115 пкс |115 пкс |Требуется всегда |
| Средний |90 пикселей |90 пикселей |Требуется всегда |
| Малый |40 пикселей |40 пикселей |Требуется всегда |
| Снимок экрана |533 пкс |32 пикселей |Необязательно |

### <a name="categories"></a>Категории
Каждый элемент Marketplace должны быть снабжены категории, которая указывает, где hello элемента отображается в пользовательском Интерфейсе портала hello. Можно выбрать один из существующих категорий hello Azure стека (вычислений, данные + хранилище, т. д.) или выбрать новый.

### <a name="links"></a>Ссылки
Каждый элемент Marketplace могут включать различные ссылки tooadditional содержимого. Hello ссылки задаются в виде списка имена и идентификаторы URI.

| Имя | Обязательно | Тип | Ограничения | Описание |
| --- | --- | --- | --- | --- |
| DisplayName |X |Строка |Не более 64 символов | |
| URI |X |URI | | |

### <a name="additional-properties"></a>Дополнительные свойства
В добавление toohello предшествующий метаданных Marketplace авторы могут предоставлять данные пары пользовательский ключ значение в hello следующие формы:

| Имя | Обязательно | Тип | Ограничения | Описание |
| --- | --- | --- | --- | --- |
| DisplayName |X |Строка |Более 25 символов. | |
| Значение |X |Строка |Максимум 30 символов | |

### <a name="html-sanitization"></a>Очистка HTML
Для любого поля, которое позволяет HTML hello следующие элементы и атрибуты допустимы:

h1, h2, h3, h4, h5, p, ol, ul, li, [целевой | href], br, strong, em, b, я

## <a name="reference-marketplace-item-ui"></a>Ссылки: Элемент Marketplace пользовательского интерфейса
Значки и текст для элементы Marketplace, как показано на портале Azure стека hello, как показано ниже.

### <a name="create-blade"></a>Колонка "Создание"
![Колонка "Создание"](media/azure-stack-marketplace-item-ui-reference/image1.png)

### <a name="marketplace-item-details-blade"></a>Колонка информации об элементе Marketplace
![Колонка информации об элементе Marketplace](media/azure-stack-marketplace-item-ui-reference/image3.png)

