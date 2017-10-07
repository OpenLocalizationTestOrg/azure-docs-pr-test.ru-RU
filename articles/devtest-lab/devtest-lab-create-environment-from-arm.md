---
title: "aaaCreate средах нескольких виртуальных Машин и PaaS ресурсы с помощью шаблонов диспетчера ресурсов Azure | Документы Microsoft"
description: "Узнайте, как toocreate средах нескольких виртуальных Машин и PaaS ресурсы в Azure DevTest Labs на основе шаблона диспетчера ресурсов Azure"
services: devtest-lab,virtual-machines,visual-studio-online
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/31/2017
ms.author: tarcher
ms.openlocfilehash: ab8628f6cb5a666435258efb93921ec69ad3a13a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-multi-vm-environments-and-paas-resources-with-azure-resource-manager-templates"></a>Создание сред со множеством виртуальных машин и ресурсов PaaS с помощью шаблонов Azure Resource Manager

Hello [портал Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040) позволяет tooeasily [создания и добавления виртуальных Машин лаборатории tooa](https://docs.microsoft.com/en-us/azure/devtest-lab/devtest-lab-add-vm). Этот вариант хорошо подходит, если одновременно создается только одна виртуальная машина. Тем не менее если среда hello содержит несколько виртуальных машин, каждая Виртуальная машина имеет toobe создан по отдельности. Для сценариев, например многоуровневые веб-приложения или фермы SharePoint механизм является tooallow, необходимые для создания hello несколько виртуальных машин за один шаг. С помощью шаблонов диспетчера ресурсов Azure, можно определить hello инфраструктурой и настройкой решение Azure и постоянно развертывать несколько виртуальных машин в согласованном состоянии. Эта функция обеспечивает hello следующие преимущества:

- Шаблоны Azure Resource Manager загружаются непосредственно из репозитория системы управления версиями (GitHub или Team Services Git).
- После настройки пользователей можно создать среду, Выбор шаблона диспетчера ресурсов Azure из hello портал управления Azure как что можно делать с другими типами [базовых классов виртуальной Машины](./devtest-lab-comparing-vm-base-image-types.md).
- В среде на основе шаблона диспетчера ресурсов Azure в дополнение tooIaaS виртуальные машины можно подготовить ресурсы Azure PaaS.
- стоимость Hello сред можно отслеживать в лаборатории hello в tooindividual сложения виртуальные машины, созданные другими типами базовых классов.
- Ресурсы PaaS создаются и будет отображаться в стоимость трассировки; Завершение работы виртуальной Машины автоматически не применяется tooPaaS ресурсов.
- Пользователи имеют hello же Управление политикой виртуальных Машин для среды, у них для виртуальных машин в одной лаборатории.

Дополнительные сведения о hello многие [преимущества использования шаблонов диспетчера ресурсов](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#the-benefits-of-using-resource-manager) toodeploy, обновить или удалить все лабораторные ресурсы в одной операции.

> [!NOTE]
> При использовании шаблона диспетчера ресурсов как toocreate основой лаборатории дополнительные виртуальные машины, существуют tookeep некоторые различия в виду, независимо от типа создаваемого Multi-виртуальных машин или виртуальные машины одной. При использовании шаблона Azure Resource Manager для виртуальной машины эти различия описываются более подробно.
>
>

## <a name="configure-azure-resource-manager-template-repositories"></a>Настройка репозиториев шаблонов Azure Resource Manager

Как один из hello рекомендации с инфраструктурой как код и как код конфигурации, шаблонов среды должны управляться в системе управления версиями. Служба Azure DevTest Labs следует этой рекомендации и загружает все шаблоны Azure Resource Manager непосредственно из репозиториев GitHub или VSTS Git. В результате можно использовать шаблоны диспетчера ресурсов через цикла всей выпуска hello, от hello теста toohello рабочей среды.

Существует ряд правил toofollow tooorganize шаблонов диспетчера ресурсов Azure в репозитории.

- Hello главного шаблона файл должен называться `azuredeploy.json`. 

    ![Основные файлы шаблонов Azure Resource Manager](./media/devtest-lab-create-environment-from-arm/master-template.png)

- Если требуется toouse значения параметров, определенные в файле параметров hello параметр файл должен называться `azuredeploy.parameters.json`.
- Можно использовать параметры hello `_artifactsLocation` и `_artifactsLocationSasToken` tooconstruct hello parametersLink значение URI, позволяя управлять tooautomatically DevTest Labs вложенных шаблонов. Дополнительные сведения см. в статье [Как служба Azure DevTest Labs упрощает развертывание вложенных шаблонов Resource Manager в тестовых средах](https://blogs.msdn.microsoft.com/devtestlab/2017/05/23/how-azure-devtest-labs-makes-nested-arm-template-deployments-easier-for-testing-environments/).
- Метаданные могут быть определенным toospecify hello отображаемое имя и описание шаблона. Эти метаданные должны находиться в файле с именем `metadata.json`. Hello следующий файл метаданных показано, как toospecify hello отображаемое имя и описание. 

```json
{
 
"itemDisplayName": "<your template name>",
 
"description": "<description of hello template>"
 
}
```

Hello следующие действия позволят вам добавить лаборатории tooyour репозитория с помощью портала Azure hello. 

1. Войдите в toohello [портал Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
1. Выберите **более служб**, а затем выберите **DevTest Labs** из списка hello.
1. Выберите из списка hello лабораториям hello требуемой лаборатории.   
1. В колонке hello лаборатории выберите **конфигурации и политиках**.

    ![Configuration and Policies (Конфигурация и политики)](./media/devtest-lab-create-environment-from-arm/configuration-and-policies-menu.png)

1. Из hello **конфигурации и политиках** выберите параметры **репозиториев**. Hello **репозиториев** колонке перечислены репозитории hello, которые были добавлены toohello лаборатории. Репозиторий с именем `Public Repo` всех занятий автоматически создается и подключается toohello [в репозитории DevTest Labs GitHub](https://github.com/Azure/azure-devtestlab) , содержащий несколько артефактов виртуальной Машины для использования.

    ![Общедоступный репозиторий](./media/devtest-lab-create-environment-from-arm/public-repo.png)

1. Выберите **добавить +** tooadd репозиторий шаблона диспетчера ресурсов Azure.
1. При втором hello **репозиториев** открывается колонка, введите необходимые сведения hello следующим образом:
    - **Имя** -введите имя репозитория hello, используемый в лаборатории hello.
    - **URL-адрес клона Git** -введите URL-адрес клонирования GIT HTTPS hello из GitHub или Visual Studio Team Services.  
    - **Ветвь** -введите tooaccess имя ветви hello в определениях шаблона диспетчера ресурсов Azure. 
    - **Личный маркер доступа** -hello личного маркера доступа используется toosecurely доступ репозиторий. Выберите срок действия токена из Visual Studio Team Services tooget  **&lt;YourName >> Мой профиль > Безопасность > токен общего доступа**. tooget срок действия токена из GitHub, выберите аватар, а затем выбрав **параметры > токен доступа Public**. 
    - **Пути к папкам** — с помощью одного из двух hello поля ввода, введите путь к папке hello, который начинается с косой черты - / - и является относительным tooyour tooeither URI клон Git определениям артефактов (первого поля ввода) или в шаблон диспетчера ресурсов Azure определения.   
    
        ![Общедоступный репозиторий](./media/devtest-lab-create-environment-from-arm/repo-values.png)

1. Как только все необходимые hello поля ввода и проходят проверку hello, выберите **Сохранить**.

Hello следующий раздел поможет вам выполнить создание сред на основе шаблона диспетчера ресурсов Azure.

## <a name="create-an-environment-from-an-azure-resource-manager-template"></a>Создание среды на основе шаблона Azure Resource Manager

После настройки репозиторием шаблона диспетчера ресурсов Azure в лаборатории hello лаборатории пользователи могут создать окружение, используя портал Azure с hello следующие шаги:

1. Войдите в toohello [портал Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
1. Выберите **более служб**, а затем выберите **DevTest Labs** из списка hello.
1. Выберите из списка hello лабораториям hello требуемой лаборатории.   
1. В колонке hello лаборатории выберите **добавить +**.
1. Hello **выберите базовый** колонке отображает hello базовые образы, можно использовать с шаблонами hello диспетчера ресурсов Azure, перечисляются в начале списка. Выберите hello требуемого шаблона диспетчера ресурсов Azure.

    ![Выбор основы](./media/devtest-lab-create-environment-from-arm/choose-a-base.png)
  
1. На hello **добавить** колонке введите hello **имя среды** значение. имя среды Hello возможности пользователей отображается tooyour в лаборатории hello. остальные поля ввода Hello определенных в шаблоне hello диспетчера ресурсов Azure. Если значения по умолчанию определяются в шаблоне hello или hello `azuredeploy.parameter.json` файл присутствует, значения по умолчанию отображаются в этих полях ввода. Для параметров типа *защиты строки*, можно использовать hello секретные данные, хранящиеся в лаборатории hello [личное хранилище секретный](https://azure.microsoft.com/en-us/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store).

    ![Колонка "Добавить"](./media/devtest-lab-create-environment-from-arm/add.png)

    > [!NOTE]
    > Существует несколько значений параметров, которые, даже если они указаны, отображаются как пустые значения. Таким образом Если пользователи назначены tooparameters эти значения в шаблоне диспетчера ресурсов Azure, DevTest Labs значения не отображаются hello; вместо отображения пустые поля ввода, где пользователи hello лаборатории должны tooenter значения при создании среды hello.
    > 
    > - GEN-UNIQUE
    > - GEN-UNIQUE-[N]
    > - GEN-SSH-PUB-KEY
    > - GEN-PASSWORD 
 
1. Выберите **добавить** toocreate hello среды. Hello среды начинается немедленно подготовки с состоянием hello, отображение в hello **моих виртуальных машин** списка. Группы ресурсов автоматически созданный hello лаборатории tooprovision все ресурсы hello, определенные в шаблоне hello диспетчера ресурсов Azure.
1. После создания среды hello выберите среду hello в hello **моих виртуальных машин** список колонки группы ресурсов tooopen hello и просмотреть все ресурсы hello подготовлены в среде hello.
    
    ![Список "My virtual machines" (Мои виртуальные машины)](./media/devtest-lab-create-environment-from-arm/all-environment-resources.png)
   
   Можно также развернуть список просто hello tooview hello среды виртуальных машин, которые были подготовлены в среде hello.
    
    ![Список "My virtual machines" (Мои виртуальные машины)](./media/devtest-lab-create-environment-from-arm/my-vm-list.png)

1. Щелкните любой hello средах tooview hello доступных действий — такие как применение артефакты, присоединение дисков с данными, изменение времени автоматического завершения работы и многое другое.

    ![Действия среды](./media/devtest-lab-create-environment-from-arm/environment-actions.png)

## <a name="next-steps"></a>Дальнейшие действия
* После создания виртуальной Машины могут подключаться toohello виртуальной Машины, выбрав **Connect** на колонки hello виртуальной Машины.
* Просмотра и управления ресурсами в среду, выбрав среды hello в hello **моих виртуальных машин** списка в лаборатории. 
* Просмотр hello [шаблоны диспетчера ресурсов Azure из коллекции шаблонов быстрый запуск Azure](https://github.com/Azure/azure-quickstart-templates)
