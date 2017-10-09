---
title: "aaaAdd лаборатории tooa репозитория Git в Azure DevTest Labs | Документы Microsoft"
description: "Добавление репозитория Git GitHub или Visual Studio Team Services, предназначенного для источника пользовательских артефактов, в Azure DevTest Labs"
services: devtest-lab,virtual-machines,visual-studio-online
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 01b459f7-eaf2-45a8-b4b5-2c0a821b33c8
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/11/2017
ms.author: tarcher
ms.openlocfilehash: e590559ffb2d497e39823e35c3f66974f42f13c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-git-repository-toostore-custom-artifacts-and-azure-resource-manager-templates"></a>Добавление репозитория Git toostore пользовательские артефакты и шаблоны Azure Resource Manager

Если требуется слишком[создать пользовательские артефакты](devtest-lab-artifact-author.md) для hello виртуальных машин в лаборатории, или [использовать toocreate шаблонов диспетчера ресурсов Azure в среде тестирования](devtest-lab-create-environment-from-arm.md), необходимо также добавить закрытый tooinclude репозитория Git артефакты Hello или шаблоны Azure Resource Manager, создаваемых командой. репозиторий Hello может размещаться на [GitHub](https://github.com) или [Visual Studio Team Services (VSTS)](https://visualstudio.com).

Мы предоставили [репозиторий Github для артефактов](https://github.com/Azure/azure-devtestlab/tree/master/Artifacts), который можно развернуть в исходном виде либо настроить для своей лаборатории. При настройке или создание артефакта не может хранить их в репозитории открытого hello, необходимо создать собственный закрытый репозиторий. 

При создании виртуальной Машины, можно сохранить шаблонов диспетчера ресурсов Azure hello, настроить его, если, а затем использовать его в более поздней версии tooeasily создать дополнительные виртуальные машины. Необходимо создать собственный закрытый репозиторий toostore настраиваемых шаблонов диспетчера ресурсов Azure.  

* toocreate репозиторий GitHub. в статье toolearn [GitHub Bootcamp](https://help.github.com/categories/bootcamp/).
* toocreate проекта Team Services с репозиторием Git. в статье toolearn [подключения tooVisual Studio Team Services](https://www.visualstudio.com/get-started/setup/connect-to-visual-studio-online).

Hello следующем снимке экрана показан пример того, как может выглядеть репозиторий, который содержит артефакты в GitHub.  
![Пример репозитория артефактов GitHub](./media/devtest-lab-add-repo/devtestlab-github-artifact-repo-home.png)

## <a name="get-hello-repository-information-and-credentials"></a>Получить сведения о репозитории hello и учетные данные
tooadd лаборатории tooyour репозитория, необходимо сначала получить определенные данные из репозитория. Привет, в следующих разделах описываются получение этой информации для репозиториев, размещенных на GitHub и Visual Studio Team Services.

### <a name="get-hello-github-repository-clone-url-and-personal-access-token"></a>Получение токена URL-адрес клона репозитория GitHub hello и личных доступа
URL-адрес tooget hello GitHub репозитория клона и личный маркер доступа, выполните следующие действия.

1. Откройте домашнюю страницу toohello репозитория GitHub hello, содержащий артефакта hello или определения шаблонов диспетчера ресурсов Azure.
2. Выберите **Clone or download**(Клонировать или скачать).
3. Выберите hello кнопка toocopy hello **URL-адрес клонирования HTTPS** toohello буфер обмена и сохраните hello URL-адрес для дальнейшего использования.
4. Выберите изображение профиля hello в правом верхнем углу hello GitHub и выберите **параметры**.
5. В hello **личные настройки** меню hello слева, выберите **личные маркеры доступа**.
6. Выберите **Создать новый маркер**.
7. На hello **новый личный маркер доступа** введите **токен описание**, поддерживает элементы по умолчанию hello в hello **выберите областей**и нажмите кнопку **формирования Токен**.
8. Сохраните hello созданный маркер, поскольку оно понадобится позже.
9. Теперь GitHub можно закрыть.   
10. Продолжить toohello [подключения репозиторий toohello лаборатории](#connect-your-lab-to-the-repository) раздела.

### <a name="get-hello-visual-studio-team-services-repository-clone-url-and-personal-access-token"></a>Получение токена URL-адрес клона репозитория hello Visual Studio Team Services и личных доступа
URL-адрес tooget hello Visual Studio Team Services репозитория клона и личного маркера доступа, выполните следующие действия:

1. Привет открыть домашнюю страницу коллекции командных (например, `https://contoso-web-team.visualstudio.com`), а затем выберите проект.
2. На домашней странице hello проекта выберите **кода**.
3. tooview hello URL-адрес клона, над проектом hello **кода** выберите **клон**.
4. Сохраните hello URL-адрес, необходимо позднее в этом учебнике.
5. выберите личный маркер доступа, toocreate **Мой профиль** hello пользователя учетной записи раскрывающегося меню.
6. На страницу сведений о профиле hello, выберите **безопасности**.
7. На hello **безопасности** выберите **добавить**.
8. В hello **создать личный маркер доступа** страницы:

   * Введите **описание** hello маркера.
   * Выберите **180 дней** из hello **истечения срока действия в** списка.
   * Выберите **всех доступных учетных записей** из hello **учетные записи** списка.
   * Выберите hello **всех областей** параметр.
   * Выберите пункт **Создать маркер**.
9. По завершении новый маркер hello появляется в hello **личные маркеры доступа** списка. Выберите **Копировать токен**, а затем сохраните значение токена hello для последующего использования.
10. Продолжить toohello [подключения репозиторий toohello лаборатории](#connect-your-lab-to-the-repository) раздела.

## <a name="connect-your-lab-toohello-repository"></a>Подключение хранилища toohello лаборатории
1. Войдите в toohello [портал Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
2. Выберите **более служб**, а затем выберите **DevTest Labs** из списка hello.
3. Выберите из списка hello лабораториям hello требуемой лаборатории.   
4. Выберите на левой панели hello **конфигурации и политиках**.
5. В лаборатории hello **конфигурации и политиках** выберите **репозиториев**.
6. На hello **репозиториев** выберите **+ добавить**.

    ![Кнопка добавления репозитория](./media/devtest-lab-add-repo/devtestlab-add-repo.png)
7. На hello второй **репозиториев** укажите hello следующую информацию:

   * **Имя** -введите имя для репозитория hello.
   * **URL-адрес клона Git** -введите hello Git HTTPS URL-адрес клона, скопированное ранее из GitHub или Visual Studio Team Services.
   * **Ветвь** -введите свои определения tooget ветви hello.
   * **Личный маркер доступа** -введите hello личный маркер доступа полученный ранее из GitHub или Visual Studio Team Services.
   * **Пути к папкам** -введите по крайней мере один путь относительный toohello клон URL-адрес папки, содержащие вашей артефакта или шаблона диспетчера ресурсов Azure. При указании подкаталог, сделать убедиться, что tooinclude hello косой черты в пути к папке hello.

     ![Область "Репозитории"](./media/devtest-lab-add-repo/devtestlab-repo-blade.png)
8. Щелкните **Сохранить**.

## <a name="next-steps"></a>Дальнейшие действия
После создания частный репозиторий Git, можно выполнить одно или оба из следующих hello в зависимости от потребностей:
* Хранилище вашей [пользовательские артефакты](devtest-lab-artifact-author.md), который можно использовать более поздней версии toocreate новые виртуальные машины.
* [Создание сред нескольких виртуальных Машин и PaaS ресурсы с шаблоны Azure Resource Manager](devtest-lab-create-environment-from-arm.md) и затем сохраните шаблоны hello в вашей частной репозитория.

При создании виртуальной Машины, можно проверить, что артефакты hello или шаблоны добавляются tooyour репозитории. Они доступны немедленно hello список артефактов или шаблонов, с именем hello вашей частной репозитория, показанное в столбце hello, указывающее источник hello. 

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

### <a name="related-blog-posts"></a>Связанные записи в блогах
* [Как tootroubleshoot сбой артефактов в Azure DevTest Labs](devtest-lab-troubleshoot-artifact-failure.md)
* [Присоединение виртуальной Машины tooexisting домена AD, с помощью шаблона диспетчера ресурсов в Azure DevTest Labs](http://www.visualstudiogeeks.com/blog/DevOps/Join-a-VM-to-existing-AD-domain-using-ARM-template-AzureDevTestLabs)
