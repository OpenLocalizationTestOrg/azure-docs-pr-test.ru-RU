---
title: "aaaAzure управляемого приложения в hello Marketplace | Документы Microsoft"
description: "Описывает Azure управляемых приложений, доступных через hello Marketplace."
services: azure-resource-manager
author: ravbhatnagar
manager: rjmax
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/09/2017
ms.author: gauravbh; tomfitz
ms.openlocfilehash: b3cdf3f1fccdd47db699e4892ae8bce35118bfd8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-managed-applications-in-hello-marketplace"></a>Azure управляемого приложения в hello Marketplace

 MSPs, независимые поставщики программного обеспечения и системным интеграторам (копий SIs) могут использовать Azure управляемых приложений toooffer своим клиентам решения tooall Azure Marketplace. Такие решения сократить обслуживания hello и необходимость обновления для клиентов. Издатели могут продавать инфраструктуры и программное обеспечение с помощью hello Marketplace. Их можно присоединить службы и приложения toomanaged оперативного обслуживания. Дополнительные сведения см. в разделе [Обзор управляемых приложений Azure](managed-application-overview.md).

В этой статье объясняется, как MSP, ISV или удостоверения службы можно опубликовать приложение toohello Marketplace и сделать его toocustomers широко доступны.

## <a name="prerequisites-for-publishing-a-managed-application"></a>Предварительные требования для публикации управляемого приложения

Предварительные требования toolisting в hello Marketplace:

* Технические требования

    *  Сведения о hello базовая структура и синтаксис шаблонов диспетчера ресурсов Azure см. в разделе [шаблоны Azure Resource Manager](resource-group-authoring-templates.md).
    *  tooview завершения и шаблонов, в разделе [шаблоны быстрый запуск Azure](https://azure.microsoft.com/en-us/documentation/templates/) или hello [шаблон репозитория краткое руководство](https://github.com/azure/azure-quickstart-templates).
    *  Сведения о том, как toocreate hello интерфейс пользователям для развертывания приложения через hello Marketplace см. в разделе [создать файл определения интерфейса пользователя](managed-application-createuidefinition-overview.md).

* Требования нетехнического характера (бизнес-требования)

    *   Ваша компания или его дочерним подразделением должен быть расположен в стране, где продажи поддерживаются hello Marketplace.
    *   Способом, совместимый с моделями выставления счетов, поддерживаемые hello Marketplace должны иметь лицензию на продукт.
    *   Вы ответственным за обеспечение разумные образом доступных toocustomers технической поддержки. Поддержка Hello можно бесплатно, оплачен, или сообществе поддержки.
    *   Вы несете ответственность за лицензирование программного обеспечения, а также любых зависимостей от стороннего программного обеспечения.
    *   Необходимо предоставить содержимое, которое не отвечает требованиям вашего предложения toobe, перечисленных в hello Marketplace и hello портал Azure.
    *   Необходимо принять условия toohello hello Azure Marketplace участие политик и соглашение для издателей.
    *   Toocomply hello условия использования, заявление о конфиденциальности и соглашение Microsoft Azure Certified программы должны быть согласованы.

## <a name="create-a-new-azure-application-offer"></a>Создание предложения приложения Azure

После требованиям hello вы будете готовы toocreate ваше предложение управляемого приложения. Давайте ознакомимся с кратким обзором предложения и SKU.

### <a name="offer"></a>ПРЕДЛОЖЕНИЕ

предложение Hello управляемого приложения соответствует класс tooa продукта предложения от издателя. Если новый тип решения или приложения, которые должны toomake в hello Marketplace, можно настроить его как новое предложение. Предложение — это коллекция SKU. Каждый предложение отображается как свой собственный сущности в hello Marketplace.

### <a name="sku"></a>SKU

SKU — hello наименьший предлагаемые для продажи Единица предложения. Можно использовать SKU внутри hello же toodifferentiate продукта класс (предложение) между:

* указывать различные функции, которые поддерживаются;
* Является ли предложение hello управляемым или неуправляемым.
* указывать разные модели выставления счетов, которые поддерживаются.

В рамках предложения родительского hello в hello Marketplace появляется SKU. Он отображается как свой собственный предлагаемые для продажи сущности в hello портал Azure.

### <a name="set-up-an-offer"></a>Настройка предложения

1. Войдите в toohello [портал Cloud Partner](https://cloudpartner.azure.com/).

2. В области навигации hello hello левой части окна выберите **+ новое предложение** > **приложений Azure**.

    ![Новое предложение](./media/managed-application-author-marketplace/newOffer.png)

3. Заполнение форм hello, отображаемые на оставшийся hello hello **редактор** представления. Обязательные для заполнения поля отмечены красной звездочкой (*).

    ![Параметры предложения](./media/managed-application-author-marketplace/newOffer_OfferSettings.png)

    Четыре основные формы являются используется toocreate управляемого приложения.

    а. Параметры предложения

    b. Номера SKU

    c. Marketplace

    d. Поддержка

Эти формы описаны более подробно в следующих разделах hello.

## <a name="offer-settings-form"></a>Форма параметров предложения
С помощью этой базовой форме toospecify hello предложение параметров.

1. Заполните hello **предоставляют параметры** формы. Hello различные поля являются:

    а. **Код предложения**: предложение hello в профиле издателя идентифицирует этот уникальный идентификатор. Он отображается в URL-адресах продукта, шаблонах Resource Manager и отчетах о выставлении счетов. Идентификатор может содержать только строчные буквы, цифры или дефисы (-). Идентификатор Hello не может заканчиваться дефисом. Это ограниченное tooa более 50 символов. После активации предложения это поле блокируется.

    b. **Идентификатор издателя**: использовать конфигурацию издателя раскрывающегося списка toochoose hello требуется toopublish это предложение в группе. После активации предложения это поле блокируется.

    c. **Имя**: это отображаемое имя для вашего предложения отображается в hello Marketplace и hello портала. Его длина не должна превышать 50 символов. Укажите для своего продукта узнаваемое название торговой марки. Не включайте в него название своей организации, если только это не требуется для продвижения продукта. Если маркетинг это предложение на собственных веб-сайте убедитесь, что это имя hello именно ее отображение на веб-сайте.

2. Выберите **Сохранить** toosave хода выполнения. 

## <a name="skus-form"></a>Форма номеров SKU
Hello следующим шагом является tooadd SKU для вашего предложения.

1. Выберите **Номера SKU** > **Новый код SKU**. 

    ![Выбор нового номера SKU](./media/managed-application-author-marketplace/newOffer_skus.png)

2. Введите **идентификатор SKU**. Идентификатор SKU — это уникальный идентификатор для hello SKU внутри предложения. Он отображается в URL-адресах продукта, шаблонах Resource Manager и отчетах о выставлении счетов. Идентификатор может содержать только строчные буквы, цифры или дефисы (-). Идентификатор Hello не может заканчиваться дефисом и является ограниченной tooa более 50 символов. После активации предложения это поле блокируется. В предложении можно использовать несколько SKU. Требуется SKU для каждого изображения планирование toopublish.

3. Заполните hello **подробности номера SKU** раздела, посвященного hello следующие формы:

    ![Указание нового номера SKU](./media/managed-application-author-marketplace/newOffer_newsku.png)

    Заполните следующие поля hello:
    
    а. **Название**. Введите название для номера SKU. Этот заголовок отображается в галерее hello для этого элемента.

    b. **Сводка**. Введите краткое описание номера SKU. Этот текст отображается под заголовок hello.

    c. **Описание**: Введите подробное описание hello SKU.

    d. **Тип SKU**: hello допустимые значения: **управляемые приложения** и **шаблоны решений**. В этом случае выберите **Managed Application** (Управляемое приложение).

4. Заполните hello **сведения о пакете** раздела, посвященного hello следующие формы:

    ![Package](./media/managed-application-author-marketplace/newOffer_newsku_package.png)

    Заполните следующие поля hello:

    а. **Текущая версия**: введите версию для отправки пакета hello. Он должен быть в формате hello `{number}.{number}.{number}{number}`.

    b. **Выберите файл пакета**: этот пакет содержит следующие файлы, которые сжимаются в ZIP-файл hello:
    * **applianceMainTemplate.json**: файл шаблона развертывания hello, применяющее toodeploy hello решения или приложения. Сведения о том, как файлы шаблона toocreate развертывания, в разделе [создать свой первый диспетчера ресурсов Azure](resource-manager-create-first-template.md).
    * **appliancecreateUIDefinition.json**: этот файл используется hello Azure портала toogenerate hello пользовательский интерфейс, который использовал tooprovision решений/приложения. Дополнительные сведения см. в статье [Начало работы с CreateUiDefinition](managed-application-createuidefinition-overview.md).
    * **mainTemplate.json**: этот файл шаблона содержит только hello Microsoft.Solution/appliances ресурсов. файл mainTemplate Hello включает hello следующие свойства:

        *  **Тип**: использование **Marketplace** для управляемых приложений в hello Marketplace.
        *  **ManagedResourceGroupId**: Эта группа ресурсов в подписке клиента hello — где развернуты все ресурсы hello, определенные в applianceMainTemplate.json.
        *  **PublisherPackageId**: Эта строка, однозначно определяющее hello пакета. Укажите значение hello в формат hello `{publisherId}.{OfferId}.{SKUID}.{PackageVersion}`.

Получить hello **предлагают идентификатор** и **идентификатор издателя** из hello публикации портала, как показано в hello после изображения:

![Offer ID (Идентификатор предложения)](./media/managed-application-author-marketplace/UniqueString_pubid_offerid.png)
        
Получить hello **SKU ID**, как показано в hello после изображения:

![Идентификатор SKU](./media/managed-application-author-marketplace/UniqueString_skuid.png)
        
Получить пакет hello **версии**, как показано в hello после изображения:

![Версия пакета](./media/managed-application-author-marketplace/UniqueString_packageversion.png)
    
  На основании hello в предыдущих примерах, hello значение **PublisherPackageId** — `azureappliance-test.ravmanagedapptest.ravpreviewmanagedsku.1.0.0`.

  Пример mainTemplate.json:

  ```json
  {
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
      "storageAccountNamePrefix": {
        "type": "string",
        "metadata": {
          "description": "Specify hello name of hello storage account"
        }
      },
      "storageAccountType": {
        "type": "string"
      }
    },
    "variables": {
      "managedResourceGroup": "[concat(resourceGroup().id,uniquestring(resourceGroup().id))]"
    },
    "resources": [{
      "type": "Microsoft.Solutions/appliances",
      "apiVersion": "2016-09-01-preview",
      "name": "[concat(parameters('storageAccountNamePrefix'), '-', 'managed')]",
      "location": "[resourceGroup().location]",
      "kind": "marketplace",
      "properties": {
        "managedResourceGroupId": "[variables('managedResourceGroup')]",
        "PublisherPackageId":"azureappliancetest.ravmanagedapptest.ravpreviewmanagedsku.1.0.0",
        "parameters": {
          "storageAccountName": {
            "value": "[parameters('storageAccountNamePrefix')]"
          },
          "storageAccountType": {
            "value": "[parameters('storageAccountType')]"
          }
        }
      }
    }],
    "outputs": {

    }
  }
  ```

Этот пакет должен содержать вложенные шаблоны или скрипты, необходимые toosuccessfully подготовки этого приложения. Hello mainTemplate.json, applianceMainTemplate.json и applianceCreateUIDefinition.json файла должны находиться в корневой папке hello.

* **Параметры авторизации**: это свойство определяет, кто получает доступ и hello уровень доступа toohello ресурсы в подписках клиентов. Hello publisher можно использовать приложение hello toomanage от имени клиента hello.
* **PrincipalId**: это свойство является hello Azure Active Directory (Azure AD) идентификатор пользователя, группы пользователей или приложение, которое предоставляет определенные разрешения на ресурсы hello в подписке клиента hello. Hello определение роли описывает hello разрешения. 
* **Определение роли**: это свойство является всех hello встроенных управление доступом на основе ролей (RBAC) роли, предоставляемые Azure AD. Вы можете выбрать роли hello, наиболее подходящий toouse toomanage hello ресурсам от имени клиента hello.

Можно добавить несколько разрешений. Рекомендуется создать группу пользователей AD и указать ее идентификатор в свойстве **PrincipalId**. Таким образом, можно добавить дополнительные группы пользователей toohello пользователей без hello необходимость tooupdate hello SKU.

Дополнительные сведения о ролевой Авторизации см. в разделе [Приступая к работе с RBAC в hello портал Azure](../active-directory/role-based-access-control-what-is.md).

## <a name="marketplace-form"></a>Форма Marketplace

запрашивает у Hello Marketplace формы поля, которые отображаются на hello [Azure Marketplace](https://azuremarketplace.microsoft.com) и на hello [портал Azure](https://portal.azure.com/).

### <a name="preview-subscription-ids"></a>Идентификаторы подписок для предварительного просмотра

Введите список подписки Azure идентификаторы, которые могут обращаться к предложению hello после его публикации. Прежде чем сделать ее можно использовать эти предложения hello предварительного просмотра tootest белого списка подписок live. Можно скомпилировать белый список too100 подписки на портале партнера hello.

### <a name="suggested-categories"></a>Предлагаемые категории

Выберите категории toofive из списка hello, ваше предложение может быть лучше всего связан. Эти категории являются вашего предложения toohello категории продуктов, доступных в hello используется toomap [Azure Marketplace](https://azuremarketplace.microsoft.com) и hello [портал Azure](https://portal.azure.com/).

#### <a name="azure-marketplace"></a>Azure Marketplace

Сводка Hello приложение отображает hello следующие поля:

![Сводка Marketplace](./media/managed-application-author-marketplace/publishvm10.png)

Hello **Обзор** вкладке приложение отображает hello следующие поля:

![Обзор Marketplace](./media/managed-application-author-marketplace/publishvm11.png)

Hello **планы + цены** вкладке приложение отображает hello следующие поля:

![Планы Marketplace](./media/managed-application-author-marketplace/publishvm15.png)

#### <a name="azure-portal"></a>Портал Azure

Сводка Hello приложение отображает hello следующие поля:

![Сводка на портале](./media/managed-application-author-marketplace/publishvm12.png)

Общие сведения о Hello для управляемого приложения отображает hello следующие поля:

![Общие сведения на портале](./media/managed-application-author-marketplace/publishvm13.png)

#### <a name="logo-guidelines"></a>Рекомендации по логотипам

Руководствуйтесь следующими рекомендациями для любого логотипа, загруженный на портале Cloud Partner hello.

*   Hello проектирования Azure имеет простой цветовой палитры. Ограничение числа hello первичной и вторичными цветами на ваш логотип.
*   цвета темы Hello портала hello белого и черного. Не используйте эти цвета как hello цвет фона вашей эмблемы. Используйте цвет, который делает ваш логотип Показательным hello портала. Мы рекомендуем простые основные цвета. *При использовании прозрачности фона, убедитесь, что не белый, текстом и hello черный или синий.*
*   Не используйте градиента фона на эмблеме hello.
*   Не разместить текст hello логотип, даже вашей компании или собственное имя. Hello внешний вид и поведение логотип должен быть плоским и избежать градиентов.
*   Убедитесь, что не растягивается логотип hello.

#### <a name="hero-logo"></a>Имиджевый логотип

Эмблема героя Hello не является обязательным. Издатель Hello можно выбрать не tooupload героя эмблему. После передачи значок героя hello, его нельзя удалить. В этот момент hello партнера должно следовать правилам Marketplace hello героя значков.

Руководствуйтесь следующими рекомендациями для значка логотипа героя hello.

*   отображаемое имя издателя Hello, Название плана hello и предложение hello длинными сводными отображаются в белый. Таким образом не используйте светлый цвет фона hello hello героя значка. Фон имиджевого значка не может быть черным, белым или прозрачным.
*   После указано предложение hello, издателю hello отображаются имя, заголовок hello плана, предложение hello длинными сводными и hello **создать** кнопку внедренные программными средствами в логотип героя hello. Следовательно не ввести текст в процессе разработки логотип героя hello. Оставьте пустое место hello вправо так, как программным образом включается текст hello в этой области. Hello пустое место для текста hello следует 415 x 100 пикселей на hello вправо. Смещением 370 пикселей от левого края hello.

    ![Пример имиджевого логотипа](./media/managed-application-author-marketplace/publishvm14.png)

## <a name="support-form"></a>Форма службы поддержки

Заполните hello **поддерживает** формы с поддержкой контактов из вашей компании. Это могут быть контактные данные технического отдела или службы поддержки клиентов.

## <a name="publish-an-offer"></a>Публикация предложения

После заполнения всех разделов hello выберите **публикации** toostart hello процесс, который делает доступными toocustomers вашего предложения.

## <a name="next-steps"></a>Дальнейшие действия

* Введение toomanaged приложений, в разделе [Обзор управляемого приложения](managed-application-overview.md).
* Сведения о использование управляемого приложения из hello Marketplace в разделе [использовать Azure управляемого приложения в hello Marketplace](managed-application-consume-marketplace.md).
* Сведения о публикации управляемых приложений в каталоге услуг см. в разделе [Создание и публикация управляемого приложения Azure](managed-application-publishing.md).
* Дополнительные сведения об использовании управляемых приложений из каталога услуг см. в разделе [Использование управляемого приложения Azure](managed-application-consumption.md).
