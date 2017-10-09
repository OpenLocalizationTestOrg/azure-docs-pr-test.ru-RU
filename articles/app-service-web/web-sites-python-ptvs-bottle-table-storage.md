---
title: "aaaBottle и хранилищем таблиц Azure в Azure с помощью средства Python 2.2 для Visual Studio"
description: "Узнайте, как toouse hello средства Python для Visual Studio toocreate Фляга для приложения, которое хранит данные в хранилище таблиц Azure и развернуть tooAzure приложения hello web App службы веб-приложений."
services: app-service\web
documentationcenter: python
author: huguesv
manager: erikre
editor: 
ms.assetid: f075124b-db79-4e51-b394-09187dd6c634
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 07/07/2016
ms.author: huvalo
ms.openlocfilehash: 25b9eb002b8748483d5b9458b7b5860a958b4bb3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="bottle-and-azure-table-storage-on-azure-with-python-tools-22-for-visual-studio"></a>Использование Bottle и табличного хранилища Azure в Azure с помощью инструментов Python 2.2 для Visual Studio
В этом учебнике мы будем использовать [средства Python для Visual Studio] toocreate простой опрашивает веб-приложения с помощью одного из шаблонов образец hello PTVS. Также доступна [видеоверсия](https://www.youtube.com/watch?v=GJXDGaEPy94)этого учебника.

веб-приложения Hello опрашивает определяет абстракцию для своего репозитория легко переключаться между различными типами репозиториев (в памяти, хранилище таблиц Azure, MongoDB).

Будет рассматриваться как toocreate хранилища Azure учетной записи, как tooconfigure hello web app toouse табличного хранилища Azure и как toopublish hello веб-приложения слишком[веб-приложениях службы приложений Azure](http://go.microsoft.com/fwlink/?LinkId=529714).

В разделе hello [центре разработчиков Python] Дополнительные статьи, посвященные разработки Azure приложение службы веб-приложений с помощью бутылка PTVS, термосе и Django веб-платформы с помощью службы MongoDB, хранилище таблиц Azure, MySQL и базы данных SQL. Хотя данная статья посвящена службы приложений, hello шаги похожи, при разработке [облачных служб Azure].

## <a name="prerequisites"></a>Предварительные требования
* Visual Studio 2015
* [Инструменты Python 2.2 для Visual Studio]
* [средства Python 2.2 для Visual Studio образцы VSIX]
* [Инструменты пакета SDK для Azure для Visual Studio 2015]
* [Python 2.7 (32-разрядная версия)] или [Python 3.4 (32-разрядная версия)]

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> Tooget работы в службе приложений Azure перед регистрацией учетную запись Azure, перейдите слишком[повторите служб приложений](https://azure.microsoft.com/try/app-service/), в котором можно немедленно создать кратковременных начальный веб-приложения в службе приложений. Никаких кредитных карт и обязательств.
> 
> 

## <a name="create-hello-project"></a>Создание проекта hello
В этом разделе мы создадим проект Visual Studio с помощью шаблона. Мы создадим виртуальную среду и установим необходимые пакеты. Затем мы выполним приложение hello локально с помощью репозитория в памяти по умолчанию hello.

1. В Visual Studio выберите последовательно **Файл** и **Создать проект**.
2. Здравствуйте, шаблоны проектов из hello [средства Python 2.2 для Visual Studio образцы VSIX] можно найти в разделе **Python**, **образцы**. Выберите **веб-проект Bottle опрашивает** и нажмите кнопку ОК toocreate hello проекта.
   
     ![Диалоговое окно "Новый проект"](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleNewProject.png)
3. Появится запрос tooinstall внешние пакеты. Выберите вариант **Установить в виртуальной среде**.
   
     ![Диалоговое окно «Внешние пакеты»](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleExternalPackages.png)
4. Выберите **Python 2.7** или **Python 3.4** базовый интерпретатора hello.
   
     ![Диалоговое окно «Добавление виртуальной среды»](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonAddVirtualEnv.png)
5. Убедитесь, что приложение hello работает, нажав клавишу `F5`. По умолчанию hello приложению репозитория в памяти, который не требует никакой настройки. Все данные будут потеряны при остановке hello веб-сервера.
6. Щелкните **Создать примеры опросов**, а затем выберите опросник, чтобы проголосовать.
   
     ![Веб-браузер](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleInMemoryBrowser.png)

## <a name="create-an-azure-storage-account"></a>Создание учетной записи хранения Azure
операции сохранения toouse, необходима учетная запись хранилища Azure. Выполнив следующие шаги, вы создадите учетную запись хранения.

1. Войти в hello [портала Azure](https://portal.azure.com/).
2. Нажмите кнопку hello **New** значок hello сверху слева от hello портала, нажмите кнопку **данные + хранилище** > **учетной записи хранилища**.  Нажмите кнопку hello **создать** кнопку, а затем укажите уникальное имя учетной записи хранилища hello и создайте новый [группы ресурсов](../azure-resource-manager/resource-group-overview.md) для него.
   
      ![Быстрое создание](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonAzureStorageCreate.png)
   
    При создании учетной записи хранилища hello hello **уведомления** кнопка будет мигать зеленым **успех** и учетной записи хранилища hello колонке открыт tooshow, что оно принадлежит новый ресурс toohello группы создать.
3. Нажмите кнопку hello **ключи доступа** часть — в колонке учетной записи хранилища hello. Запишите имя учетной записи hello и key1.
   
      ![ключей](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonAzureStorageKeys.png)
   
    Нам понадобится этот tooconfigure сведения о проекте в следующем разделе hello.

## <a name="configure-hello-project"></a>Настройка проекта hello
В этом разделе мы настроим наши приложения toouse hello учетную запись хранилища, мы только что создали. Затем мы выполним приложение hello локально.

1. В Visual Studio щелкните правой кнопкой мыши узел проекта в обозревателе решений и выберите **Свойства**. Щелкните hello **отладки** вкладки.
   
     ![Параметры отладки проекта](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleAzureTableStorageProjectDebugSettings.png)
2. Задать hello значения переменных среды, необходимые для приложения hello в **отлаживать команды Server**, **среды**.
   
       REPOSITORY_NAME=azuretablestorage
       STORAGE_NAME=<storage account name>
       STORAGE_KEY=<primary access key>
   
   Это задаст переменные среды hello при вы **начать отладку**. Переменные toobe hello задайте при вы **Запуск без отладки**, набор hello же значения в разделе **выполнение команды сервера** также.
   
   Кроме того можно определить переменные среды, с помощью панели управления Windows hello. Это является лучшим вариантом, если файл проекта tooavoid хранение учетных данных в исходном коде. Обратите внимание, что вам потребуется toorestart Visual Studio для новой среды hello значения toobe toohello доступных приложений.
3. Hello код, который реализует репозитория hello табличного хранилища Azure находится в **models/azuretablestorage.py**. В разделе hello [документации] Дополнительные сведения о том, как toouse службы таблиц из Python.
4. Запустите приложение hello с `F5`. Опросы, созданных с помощью **создать образец опрашивает** и hello данные, переданные с правом голоса сериализуются в хранилище таблиц Azure.
   
   > [!NOTE]
   > Hello Python 2.7 виртуальной среды может привести к на разрыв исключений в Visual Studio.  Нажмите клавишу `F5` toocontinue загрузке hello веб-проекта.
   > 
   > 
5. Обзор toohello **о** tooverify страницы, hello приложение использует hello **табличного хранилища Azure** репозитория.
   
     ![Веб-браузер](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleAzureTableStorageAbout.png)

## <a name="explore-hello-azure-table-storage"></a>Просмотр hello табличного хранилища Azure
Он просто tooview и редактирование таблиц хранилища с помощью Cloud Explorer в Visual Studio. В этом разделе мы будем использовать обозреватель серверов tooview hello содержимого таблиц приложений опрашивает hello.

> [!NOTE]
> Это требует toobe инструментов Microsoft Azure установлены, они доступны как часть hello [Azure SDK для .NET].
> 
> 

1. Откройте **Cloud Explorer**. Разверните узел **Учетные записи хранения**, свою учетную запись хранения, а затем узел **Таблицы**.
   
     ![Cloud Explorer](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonServerExplorer.png)
2. Дважды щелкните hello **опрашивает** или **варианты** таблице tooview hello содержимое таблицы hello в окне документа, а также добавления, удаления и изменения сущностей.
   
     ![Результаты запросов таблицы](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonServerExplorerTable.png)

## <a name="publish-hello-web-app-tooazure-app-service"></a>Публикация hello web app tooAzure службы приложений
Hello Azure .NET SDK предоставляет простой способ toodeploy вашей web app tooAzure службы приложений.

1. В **обозревателе решений**, правой кнопкой мыши узел проекта hello и выберите **публикации**.
   
     ![Диалоговое окно «Публикация веб-сайта»](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonPublishWebSiteDialog.png)
2. Щелкните **Веб-приложения Microsoft Azure**.
3. Щелкните **New** toocreate новое веб-приложение.
4. Заполните следующие поля hello и нажмите кнопку **создать**.
   
   * **Имя веб-приложения**
   * **План обслуживания приложения**
   * **Группа ресурсов**
   * **Регион**
   * Оставить **сервера базы данных** значение слишком**ни одной базы данных**
5. Примите значения по умолчанию и щелкните **Опубликовать**.
6. Веб-браузере откроется автоматически toohello опубликованных веб-приложения. При просмотре toohello о странице вы увидите, что он использует hello **в памяти** репозитория, не hello **табличного хранилища Azure** репозитория.
   
   Это потому, что hello переменные среды не установлены hello экземпляр веб-приложений в службе приложений Azure, поэтому он использует значения по умолчанию hello в **settings.py**.

## <a name="configure-hello-web-apps-instance"></a>Настройка экземпляра веб-приложения hello
В этом разделе мы настроим переменные среды для экземпляра веб-приложения hello.

1. В [портала Azure], откройте колонку hello веб-приложение, нажав **Обзор** > **службы приложений** > имя вашего веб-приложения.
2. В колонке веб-приложения щелкните **Все параметры**, а затем — **Параметры приложения**.
3. Прокрутите вниз toohello **параметры приложения** статьи и задание значений hello для **РЕПОЗИТОРИЯ\_имя**, **ХРАНЕНИЯ\_имя** и  **ХРАНИЛИЩЕ\_ключ** согласно инструкциям hello **проекта hello Настройка** выше.
   
     ![Параметры приложения](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonWebSiteConfigureSettingsTableStorage.png)
4. Щелкните **Save**(Сохранить). После получил уведомления hello применения hello изменения, выберите команду **Обзор** из колонки основного приложения Web hello.
5. Вы увидите рабочее приложение hello web, как и ожидалось, с помощью hello **табличного хранилища Azure** репозитория.
   
   Поздравляем!
   
     ![Веб-браузер](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleAzureBrowser.png)

## <a name="next-steps"></a>Дальнейшие действия
Выполните эти ссылки toolearn Дополнительные сведения о средствах Python для Visual Studio, бутылка и табличного хранилища Azure.

* [Документация по средствам Python для Visual Studio]
  * [Веб-проекты]
  * [Проекты для облачной службы]
  * [Удаленная отладка в Microsoft Azure]
* [Документация по работе с Bottle]
* [Хранилище Azure]
* [Пакет SDK для Azure для Python]
* [Как tooUse hello службы хранения таблиц из Python]

## <a name="whats-changed"></a>Изменения
* Toohello руководство изменений из tooApp веб-сайтов службы. в разделе: [службе приложений Azure и ее влияние на существующие службы Azure](http://go.microsoft.com/fwlink/?LinkId=529714)

<!--Link references-->
[центре разработчиков Python]: /develop/python/
[облачных служб Azure]: ../cloud-services/cloud-services-python-ptvs.md
[документации]:../cosmos-db/table-storage-how-to-use-python.md
[Как tooUse hello службы хранения таблиц из Python]:../cosmos-db/table-storage-how-to-use-python.md


<!--External Link references-->
[портала Azure]: https://portal.azure.com
[Azure SDK для .NET]: http://azure.microsoft.com/downloads/
[средства Python для Visual Studio]: http://aka.ms/ptvs
[Инструменты Python 2.2 для Visual Studio]: http://go.microsoft.com/fwlink/?LinkId=624025
[средства Python 2.2 для Visual Studio образцы VSIX]: http://go.microsoft.com/fwlink/?LinkId=624025
[Инструменты пакета SDK для Azure для Visual Studio 2015]: http://go.microsoft.com/fwlink/?LinkId=518003
[Python 2.7 (32-разрядная версия)]: http://go.microsoft.com/fwlink/?LinkId=517190
[Python 3.4 (32-разрядная версия)]: http://go.microsoft.com/fwlink/?LinkId=517191
[Документация по средствам Python для Visual Studio]: http://aka.ms/ptvsdocs
[Документация по работе с Bottle]: http://bottlepy.org/docs/dev/index.html
[Удаленная отладка в Microsoft Azure]: http://go.microsoft.com/fwlink/?LinkId=624026
[Веб-проекты]: http://go.microsoft.com/fwlink/?LinkId=624027
[Проекты для облачной службы]: http://go.microsoft.com/fwlink/?LinkId=624028
[Хранилище Azure]: http://azure.microsoft.com/documentation/services/storage/
[Пакет SDK для Azure для Python]: https://github.com/Azure/azure-sdk-for-python
