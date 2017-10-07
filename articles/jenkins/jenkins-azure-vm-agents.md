---
title: "агенты ВМ Azure aaaUse для непрерывная интеграция с Jenkins."
description: "Агенты виртуальных машин Azure в качестве подчиненных модулей Jenkins."
services: multiple
documentationcenter: 
author: mlearned
manager: douge
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 6/7/2017
ms.author: mlearned
ms.custom: Jenkins
ms.openlocfilehash: 2388e6919d0280372166fbd325d80dafb00d7550
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-vm-agents-for-continuous-integration-with-jenkins"></a>Использование агентов виртуальных машин для непрерывной интеграции с Jenkins.

Это краткое руководство показывает, как toouse hello toocreate подключаемый модуль агента ВМ Jenkins агент Linux (Ubuntu) по запросу в Azure.

## <a name="prerequisites"></a>Предварительные требования

toocomplete краткого руководства:

* Если главный Jenkins еще нет можно начать с hello [шаблон решения](install-jenkins-solution-template.md) 
* См. слишком[создании субъекта-службы Azure с помощью Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) Если вы еще не участника-службы Azure.

## <a name="install-azure-vm-agents-plugin"></a>Установка подключаемого модуля агентов виртуальных машин

При запуске из hello [шаблон решения](install-jenkins-solution-template.md), подключаемый модуль агента ВМ Azure hello устанавливается в базе данных master Jenkins hello.

В противном случае установка hello **агента ВМ** подключаемого модуля из панели мониторинга Jenkins hello.

## <a name="configure-hello-plugin"></a>Настроить подключаемый модуль hello

* Панели мониторинга Jenkins hello, нажмите кнопку **Jenkins управления -> Настройка системы ->**. Прокрутите toohello внизу страницы hello и найдите раздел hello с раскрывающимся hello **Добавление нового облака**. Меню "hello" выберите **агенты ВМ Microsoft Azure**
* Выберите существующую учетную запись из раскрывающегося списка hello учетные данные Azure.  tooadd новый **субъекта-службы Microsoft Azure,** введите hello следующие значения: идентификатор подписки, идентификатор клиента, секрет клиента и конечная точка маркера OAuth 2.0.

![Учетные данные Azure](./media/jenkins-azure-vm-agents/service-principal.png)

* Нажмите кнопку **Проверьте конфигурацию** toomake правильность конфигурации профиля hello.
* Сохранить конфигурацию hello и продолжить toohello следующий шаг.

## <a name="template-configuration"></a>Конфигурация шаблона

### <a name="general-configuration"></a>Общая конфигурация
Настройте шаблон для использования toodefine агента ВМ Azure. 

* Нажмите кнопку **добавить** tooadd шаблона. 
* Введите имя нового шаблона. 
* Для метки hello введите «ubuntu.» Эта метка используется во время настройки задания hello.
* Выберите нужный регион hello со списком «hello».
* Выберите hello желаемый размер виртуальной Машины.
* Укажите имя учетной записи хранилища Azure hello, или оставьте имя по умолчанию hello пустой toouse «jenkinsarmst».
* Укажите срок хранения hello в минутах. Этот параметр определяет hello число минут ожидания Jenkins перед автоматическое удаление неактивных агента. Укажите 0, если не требуется toobe простоя агентов, удаляются автоматически.

![Общая конфигурация](./media/jenkins-azure-vm-agents/general-config.png)

### <a name="image-configuration"></a>Конфигурация образа

Выберите toocreate агент Linux (Ubuntu) **изображения ссылку** и hello используется следующая конфигурация в качестве примера. См. слишком[Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/compute?subcategories=virtual-machine-images&page=1) hello Azure последние поддерживаемые изображения.

* Издатель образа: Canonical
* Предложение образа: UbuntuServer
* Номер SKU образа: 14.04.5-LTS
* Версия образа виртуальной машины: последняя
* Тип ОС: Linux
* Метод запуска: SSH
* Укажите учетные данные администратора
* При использовании скрипта инициализации виртуальной машины введите:
```
# Install Java
sudo apt-get -y update
sudo apt-get install -y openjdk-7-jdk
sudo apt-get -y update --fix-missing
sudo apt-get install -y openjdk-7-jdk
```
![Конфигурация образа](./media/jenkins-azure-vm-agents/image-config.png)

* Нажмите кнопку **Проверка шаблона** tooverify hello конфигурации.
* Щелкните **Сохранить**.

## <a name="create-a-job-in-jenkins"></a>Создание задания в Jenkins

* Панели мониторинга Jenkins hello, нажмите кнопку **новый элемент**. 
* Введите имя, выберите **Freestyle project** (Универсальный проект) и нажмите кнопку **ОК**.
* В hello **Общие** вкладки, выберите «Ограничить, где проект может работать» и тип «ubuntu» в выражении метки. Теперь отображается «ubuntu» в раскрывающемся списке hello.
* Щелкните **Сохранить**.

![Настройка задания](./media/jenkins-azure-vm-agents/job-config.png)

## <a name="build-your-new-project"></a>Сборка нового проекта

* Вы можете вернуться toohello Jenkins мониторинга.
* Создать новое задание hello щелкните правой кнопкой мыши, нажмите кнопку **сборки теперь**. Сборка запущена. 
* После завершения построения hello go слишком**вывод на консоль**. Вы увидите, что сборки hello удаленно выполнялась в Azure.

![Вывод на консоль](./media/jenkins-azure-vm-agents/console-output.png)

## <a name="reference"></a>Справочные материалы

* Пятничное видео Azure: [Continuous Integration with Jenkins Using Azure VM Agents](https://channel9.msdn.com/Shows/Azure-Friday/Continuous-Integration-with-Jenkins-Using-Azure-VM-Agents) (Непрерывная интеграция с Jenkins при помощи агентов виртуальных машин Azure)
* Сведения о поддержке и параметры конфигурации: [вики-сайт по использованию подключаемого модуля Jenkins с агентами виртуальных машин Azure](https://wiki.jenkins-ci.org/display/JENKINS/Azure+VM+Agents+Plugin) 

