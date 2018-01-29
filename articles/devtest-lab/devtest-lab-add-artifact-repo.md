---
title: "Добавление репозитория Git в лабораторию в Azure DevTest Labs | Документы Майкрософт"
description: "Узнайте, как добавить репозиторий GitHub или Visual Studio Team Services, предназначенный для источника пользовательских артефактов, в Azure DevTest Labs."
services: devtest-lab,virtual-machines,visual-studio-online
documentationcenter: na
author: craigcaseyMSFT
manager: douge
editor: 
ms.assetid: 01b459f7-eaf2-45a8-b4b5-2c0a821b33c8
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/11/2017
ms.author: v-craic
ms.openlocfilehash: 345d095762b75b7a177bf4c6e7a07360a9c14068
ms.sourcegitcommit: 85012dbead7879f1f6c2965daa61302eb78bd366
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/02/2018
---
# <a name="add-a-git-repository-to-store-custom-artifacts-and-resource-manager-templates"></a>Добавление репозитория Git для хранения пользовательских артефактов и шаблонов Resource Manager

Вы можете [создать пользовательские артефакты](devtest-lab-artifact-author.md) для виртуальных машин в лаборатории или [использовать шаблоны Azure Resource Manager для создания настраиваемой тестовой среды](devtest-lab-create-environment-from-arm.md). Для артефактов или шаблонов Resource Manager, создаваемых вашей группой, необходимо добавить частный репозиторий Git. Репозиторий артефактов может находиться в [GitHub](https://github.com) или [Visual Studio Team Services](https://visualstudio.com).

Мы предоставляем [репозиторий GitHub для артефактов](https://github.com/Azure/azure-devtestlab/tree/master/Artifacts), который можно развернуть в исходном виде либо настроить для своей лаборатории. Настроенные или созданные артефакты нельзя сохранять в общедоступном репозитории. Нужно создать собственный частный репозиторий для пользовательских и создаваемых артефактов. 

При создании виртуальной машины можно сохранить шаблон Resource Manager, при необходимости настроить его, а затем использовать для создания дополнительных виртуальных машин. Нужно создать собственный частный репозиторий для хранения настраиваемых шаблонов Resource Manager.  

* Сведения о создании репозитория GitHub см. в [этой статье](https://help.github.com/categories/bootcamp/).
* Дополнительные сведения о создании проекта Team Services с репозиторием Git см. в статье [Connect to Visual Studio Team Services from Eclipse, Xcode, Visual Studio, and more](https://www.visualstudio.com/get-started/setup/connect-to-visual-studio-online) (Подключение к Visual Studio Team Services из Eclipse, Xcode, Visual Studio и других служб).

Вот как может выглядеть содержащий артефакты репозиторий в GitHub:  

![Пример репозитория артефактов GitHub](./media/devtest-lab-add-repo/devtestlab-github-artifact-repo-home.png)

## <a name="get-the-repository-information-and-credentials"></a>Получение сведений о репозитории и его учетных данных
Чтобы добавить репозиторий в лабораторию, сначала нужно получить из него основные сведения. В следующих подразделах описывается, как получить необходимые сведения для репозиториев, размещенных на портале GitHub или в Visual Studio Team Services.

### <a name="get-the-github-repository-clone-url-and-personal-access-token"></a>Получение URL-адреса клона и персонального маркера доступа из репозитория GitHub

1. Перейдите на домашнюю страницу репозитория GitHub, который содержит определения артефактов или шаблонов Resource Manager.
2. Выберите **Clone or download**(Клонировать или скачать).
3. Нажмите кнопку **HTTPS clone url** (URL-адрес клона HTTPS), чтобы скопировать URL-адрес в буфер обмена. Сохраните URL-адрес для последующего использования.
4. В правом верхнем углу GitHub выберите изображение профиля и щелкните **Параметры**.
5. В меню **Личные параметры** в левой части экрана выберите **Личные маркеры доступа**.
6. Выберите **Создать новый маркер**.
7. На странице **New personal access token** (Новый личный маркер доступа) заполните поле **Token description** (Описание маркера). Примите элементы по умолчанию в разделе **Выберите области** и щелкните **Создать токен**.
8. Сохраните созданный маркер — он вам потребуется позже.
9. Закройте GitHub.   
10. Перейдите к разделу [Подключение лаборатории к репозиторию](#connect-your-lab-to-the-repository).

### <a name="get-the-visual-studio-team-services-repository-clone-url-and-personal-access-token"></a>Получение URL-адреса клона и личного маркера доступа из репозитория Visual Studio Team Services

1. Перейдите на домашнюю страницу групповой коллекции (например, https://contoso-web-team.visualstudio.com) и выберите свой проект.
2. На домашней странице проекта выберите **Код**.
3. Чтобы увидеть URL-адрес клона, на странице **Код** проекта выберите **Клон**.
4. Сохраните URL-адрес — он вам потребуется позже.
5. Для создания личного маркера доступа выберите в раскрывающемся меню учетной записи пользователя **Мой профиль**.
6. На странице сведений о профиле выберите **Безопасность**.
7. На вкладке **Безопасность** щелкните **Добавить**.
8. На странице **Создать личный маркер доступа**:
   1. Введите **описание** маркера.
   2. В списке **Срок действия истекает через** выберите **180 дней**.
   3. В списке **Учетные записи** выберите **Все доступные учетные записи**.
   4. Выберите **Все области**.
   5. Щелкните **Создать маркер**.
9. Новый маркер появится в списке **Личные маркеры доступа**. Выберите **Скопировать маркер**и сохраните значение маркера, так как оно вам потребуется позднее.
10. Перейдите к разделу [Подключение лаборатории к репозиторию](#connect-your-lab-to-the-repository).

## <a name="connect-your-lab-to-the-repository"></a>Подключение лаборатории к репозиторию
1. Войдите на [портале Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
2. Щелкните **Больше служб**, а затем выберите в списке служб **DevTest Labs**.
3. В списке лабораторий выберите свою лабораторию. 
4. Выберите **Configuration and policies** (Конфигурация и политики) > **Репозитории** > **+ Добавить**.

    ![Кнопка добавления репозитория](./media/devtest-lab-add-repo/devtestlab-add-repo.png)
5. На второй странице **Репозитории** укажите следующие сведения:
  1. **Имя**. Введите имя репозитория.
  2. **URL-адрес клона Git.** Введите URL-адрес клона HTTPS Git, скопированный ранее из GitHub или Visual Studio Team Services.
  3. **Ветвь.** Укажите ветвь для получения определений.
  4. **Личный маркер доступа.** Укажите личный маркер доступа, полученный ранее из GitHub или Visual Studio Team Services.
  5. **Путь к папке.** Введите по меньшей мере один путь к папке относительно URL-адреса клона, содержащего определения артефактов или шаблонов Resource Manager. При указании подкаталога обязательно включите косую черту в путь к папке.

     ![Область "Репозитории"](./media/devtest-lab-add-repo/devtestlab-repo-blade.png)
6. Щелкните **Сохранить**.

### <a name="related-blog-posts"></a>Связанные записи в блогах
* [Диагностика сбоев артефактов в лаборатории](devtest-lab-troubleshoot-artifact-failure.md)
* [Join a VM to existing AD Domain using ARM template in Azure Dev Test Lab](http://www.visualstudiogeeks.com/blog/DevOps/Join-a-VM-to-existing-AD-domain-using-ARM-template-AzureDevTestLabs) (Присоединение виртуальной машины к имеющемуся домену AD с помощью шаблона ARM в Azure DevTest Labs)

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a>Дальнейшие действия
После создания частного репозитория Git в зависимости от потребностей можно выполнить одно или оба из следующих действий:
* Сохраните [пользовательские артефакты](devtest-lab-artifact-author.md). Их можно использовать позже для создания виртуальных машин.
* [Создайте среды со множеством виртуальных машин и ресурсов PaaS с помощью шаблонов Resource Manager](devtest-lab-create-environment-from-arm.md). Затем шаблоны можно сохранить в частном репозитории.

При создании виртуальной машины вы можете убедиться, что артефакты или шаблоны добавляются в ваш репозиторий Git. Они немедленно становятся доступными в списке артефактов или шаблонов. Имя частного репозитория отображается в столбце, указывающем источник. 
