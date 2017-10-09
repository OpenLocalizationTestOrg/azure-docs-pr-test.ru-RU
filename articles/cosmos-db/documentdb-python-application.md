---
title: "Учебник aaaPython термосе web приложения для Azure Cosmos DB | Документы Microsoft"
description: "Просмотрите базы данных учебник по использованию Azure Cosmos DB toostore и доступ к данным из термосе Python веб-приложения, размещенные в Azure. Найдите решения для разработки приложений."
keywords: "Разработка приложений, Python Flask, веб-приложение Python, разработка веб-приложения Python"
services: cosmos-db
documentationcenter: python
author: mimig1
manager: jhubbard
editor: cgronlun
ms.assetid: 20ebec18-67c2-4988-a760-be7c30cfb745
ms.service: cosmos-db
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 08/09/2017
ms.author: mimig
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 87b73c656ed96a7efbd162843a1529d435f027f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-python-flask-web-application-using-azure-cosmos-db"></a>Создание веб-приложения Python Flask с использованием Azure Cosmos DB
> [!div class="op_single_selector"]
> * [.NET](documentdb-dotnet-application.md)
> * [Node.js](documentdb-nodejs-application.md)
> * [Java](documentdb-java-application.md)
> * [Python](documentdb-python-application.md)
> 
> 

Этот учебник показывает, как веб-приложения, размещенные в Azure toouse Azure Cosmos DB toostore и доступ к данным из Python и предполагает, что имеются некоторые опыта работы с Python и веб-сайты Azure.

В этом учебнике по базам данных рассматриваются следующие процедуры.

1. Создание и подготовка учетной записи Cosmos DB.
2. Создание приложения Python Flask.
3. Подключение tooand с помощью Cosmos DB из веб-приложения.
4. Развертывание приложения tooAzure hello web.

Выполнив этот учебник, вы создадите простое приложение голосования, которое позволяет вам toovote для опроса.

![Снимок экрана: hello голосования приложения, созданные с учебником базы данных](./media/documentdb-python-application/cosmos-db-pythonr-run-application.png)

## <a name="database-tutorial-prerequisites"></a>Предварительные требования для учебника по базам данных
Перед выполнением инструкции hello в этой статье, следует убедиться, что имеется hello установлены следующие компоненты:

* Активная учетная запись Azure. Если ее нет, можно создать бесплатную пробную учетную запись всего за несколько минут. Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/).
 
    ИЛИ 

    Локальная установка hello [DB эмулятор Azure Cosmos](local-emulator.md).
* [Microsoft Visual Studio Community 2017](http://www.visualstudio.com/)  
* [Инструменты Python для Visual Studio](https://github.com/Microsoft/PTVS/)  
* [Пакет Microsoft Azure SDK для Python 2.7](https://azure.microsoft.com/downloads/) 
* [Python 2.7.13](https://www.python.org/downloads/windows/) 

> [!IMPORTANT]
> При установке Python 2.7 для hello первый раз, убедитесь, что на экране настройки Python 2.7.13 hello, вы выбрали **добавить python.exe tooPath**.
> 
> ![Снимок экрана настройки Python 2.7.11 hello, требующие tooPath python.exe tooselect добавить](./media/documentdb-python-application/cosmos-db-python-install.png)
> 
> 

* [Компилятор Microsoft Visual C++ для Python 2.7](https://www.microsoft.com/en-us/download/details.aspx?id=44266)

## <a name="step-1-create-an-azure-cosmos-db-database-account"></a>Шаг 1. Создание учетной записи базы данных Azure Cosmos DB
Давайте сначала создадим учетную запись Cosmos DB. Если уже есть учетная запись, или при использовании hello эмулятор DB Cosmos Azure для этого учебника, можно пропустить слишком[шаг 2: Создание нового веб-приложения Python термосе](#step-2-create-a-new-python-flask-web-application).

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

<br/>
Теперь мы рассмотрим как фоновый toocreate новое веб-приложение термосе Python из hello.

## <a name="step-2-create-a-new-python-flask-web-application"></a>Шаг 2. Создание веб-приложения Python Flask
1. В Visual Studio в hello **файл** меню выберите пункт слишком**New**и нажмите кнопку **проекта**.
   
    Hello **новый проект** откроется диалоговое окно.
2. Hello левой панели разверните **шаблоны** и затем **Python**, а затем нажмите кнопку **Web**. 
3. Выберите **термосе веб-проекта** hello центральной панели, а затем в hello **имя** введите **учебника**и нажмите кнопку **ОК**. Помните, что имена пакетов Python должны быть прописными буквами, как описано в hello [руководстве по стилю для кода Python](https://www.python.org/dev/peps/pep-0008/#package-and-module-names).
   
    Для этих новых tooPython термосе это платформа разработки веб-приложений, поможет вам быстрее создавать веб-приложения в Python.
   
    ![Снимок окна hello новый проект в Visual Studio с Python, выделенная на hello слева, Python термосе веб-проекта, выбранного в середине hello и учебник hello имя в поле "имя" hello](./media/documentdb-python-application/image9.png)
4. В hello **средства Python для Visual Studio** окно, нажмите кнопку **установка в виртуальной среде**. 
   
    ![Снимок экрана учебника hello базы данных - средства Python для Visual Studio окно](./media/documentdb-python-application/python-install-virtual-environment.png)
5. В hello **добавьте виртуальной среды** окна, могут принимать значения по умолчанию hello и использования Python 2.7 в качестве базовой среды hello, поскольку PyDocumentDB в настоящее время не поддерживает Python 3.x и нажмите кнопку **создать**. При этом устанавливаются необходимые hello Python виртуальную среду для проекта.
   
    ![Снимок экрана учебника hello базы данных - средства Python для Visual Studio окно](./media/documentdb-python-application/image10_A.png)
   
    Отображает окно вывода Hello `Successfully installed Flask-0.10.1 Jinja2-2.8 MarkupSafe-0.23 Werkzeug-0.11.5 itsdangerous-0.24 'requirements.txt' was installed successfully.` успешно при установке среды hello.

## <a name="step-3-modify-hello-python-flask-web-application"></a>Шаг 3: Изменение веб-приложение hello термосе Python
### <a name="add-hello-python-flask-packages-tooyour-project"></a>Добавление проекта tooyour пакеты Python термосе hello
После настройки проекта потребуется tooadd hello необходимые термосе пакетов tooyour проекта, включая pydocumentdb hello пакета Python для DocumentDB.

1. В обозревателе решений откройте файл hello с именем **requirements.txt** и замените содержимое hello hello следующее:
   
        flask==0.9
        flask-mail==0.7.6
        sqlalchemy==0.7.9
        flask-sqlalchemy==0.16
        sqlalchemy-migrate==0.7.2
        flask-whooshalchemy==0.55a
        flask-wtf==0.8.4
        pytz==2013b
        flask-babel==0.8
        flup
        pydocumentdb>=1.0.0
2. Сохранить hello **requirements.txt** файла. 
3. В обозревателе решений щелкните элемент **env** правой кнопкой мыши и выберите пункт **Install from requirements.txt** (Установить из файла requirements.txt).
   
    ![Снимок экрана, показывающий env (Python 2.7), выбранных при установке из requirements.txt, выделяются в списке hello](./media/documentdb-python-application/cosmos-db-python-install-from-requirements.png)
   
    После успешной установки hello в окне вывода отображает hello следующее:
   
        Successfully installed Babel-2.3.2 Tempita-0.5.2 WTForms-2.1 Whoosh-2.7.4 blinker-1.4 decorator-4.0.9 flask-0.9 flask-babel-0.8 flask-mail-0.7.6 flask-sqlalchemy-0.16 flask-whooshalchemy-0.55a0 flask-wtf-0.8.4 flup-1.0.2 pydocumentdb-1.6.1 pytz-2013b0 speaklater-1.3 sqlalchemy-0.7.9 sqlalchemy-migrate-0.7.2
   
   > [!NOTE]
   > В редких случаях могут появиться ошибки в окне вывода hello. В этом случае проверьте ошибки hello связанные toocleanup. Иногда не удается выполнить очистку hello, но по-прежнему будет успешной установки hello (прокрутки вверх tooverify окно вывода hello это). Можно проверить установку, [проверка hello виртуальной среды](#verify-the-virtual-environment). Если не удалось установить hello, но hello проверка прошла успешно, это toocontinue ОК.
   > 
   > 

### <a name="verify-hello-virtual-environment"></a>Проверка hello виртуальной среды
Убедимся, что все установлено правильно.

1. Постройте решение hello, нажав клавиши **Ctrl**+**Shift**+**B**.
2. После успешного построения hello, запустите hello веб-сайт, нажав клавишу **F5**. Это запускается сервер разработки термосе hello и запускает веб-браузере. Должны появиться после страницы приветствия.
   
    ![Hello пустой термосе Python веб-разработки проекта отображается в браузере](./media/documentdb-python-application/image12.png)
3. Остановить отладку hello веб-сайт, нажав клавишу **Shift**+**F5** в Visual Studio.

### <a name="create-database-collection-and-document-definitions"></a>Создание определений базы данных, коллекции и документа
Теперь давайте создадим приложение для голосования, добавив новые файлы и обновив остальные.

1. В обозревателе решений щелкните правой кнопкой мыши hello **учебника** проекта, нажмите кнопку **добавить**, а затем нажмите кнопку **новый элемент**. Выберите **пустой файл Python** и имя файла hello **forms.py**.  
2. Добавьте следующие файл forms.py toohello кода hello, а затем сохраните файл hello.

```python
from flask.ext.wtf import Form
from wtforms import RadioField

class VoteForm(Form):
    deploy_preference  = RadioField('Deployment Preference', choices=[
        ('Web Site', 'Web Site'),
        ('Cloud Service', 'Cloud Service'),
        ('Virtual Machine', 'Virtual Machine')], default='Web Site')
```


### <a name="add-hello-required-imports-tooviewspy"></a>Добавьте необходимые hello imports tooviews.py
1. В обозревателе решений разверните hello **учебника** папку и откройте hello **views.py** файла. 
2. Добавить после импорта инструкций toohello вверху hello hello **views.py** файла, после чего сохраните файл hello. Эти импортировать Cosmos DB PythonSDK и hello термосе пакетов.
   
    ```python
    from forms import VoteForm
    import config
    import pydocumentdb.document_client as document_client
    ```

### <a name="create-database-collection-and-document"></a>Создание базы данных, коллекции и документа
* В по-прежнему **views.py**, добавить следующий код toohello конец файла hello hello. Это обеспечивает создание hello базы данных, используемой формы hello. Не удаляйте из существующего кода hello в **views.py**. Просто добавьте этот элемент toohello.

```python
@app.route('/create')
def create():
    """Renders hello contact page."""
    client = document_client.DocumentClient(config.DOCUMENTDB_HOST, {'masterKey': config.DOCUMENTDB_KEY})

    # Attempt toodelete hello database.  This allows this toobe used toorecreate as well as create
    try:
        db = next((data for data in client.ReadDatabases() if data['id'] == config.DOCUMENTDB_DATABASE))
        client.DeleteDatabase(db['_self'])
    except:
        pass

    # Create database
    db = client.CreateDatabase({ 'id': config.DOCUMENTDB_DATABASE })

    # Create collection
    collection = client.CreateCollection(db['_self'],{ 'id': config.DOCUMENTDB_COLLECTION })

    # Create document
    document = client.CreateDocument(collection['_self'],
        { 'id': config.DOCUMENTDB_DOCUMENT,
          'Web Site': 0,
          'Cloud Service': 0,
          'Virtual Machine': 0,
          'name': config.DOCUMENTDB_DOCUMENT 
        })

    return render_template(
       'create.html',
        title='Create Page',
        year=datetime.now().year,
        message='You just created a new database, collection, and document.  Your old votes have been deleted')
```


### <a name="read-database-collection-document-and-submit-form"></a>Чтение базы данных, коллекции и документа и отправка формы
* В по-прежнему **views.py**, добавить следующий код toohello конец файла hello hello. Это заботится настройки формы hello, чтения hello базы данных, коллекции и документа. Не удаляйте из существующего кода hello в **views.py**. Просто добавьте этот элемент toohello.

```python
@app.route('/vote', methods=['GET', 'POST'])
def vote(): 
    form = VoteForm()
    replaced_document ={}
    if form.validate_on_submit(): # is user submitted vote  
        client = document_client.DocumentClient(config.DOCUMENTDB_HOST, {'masterKey': config.DOCUMENTDB_KEY})

        # Read databases and take first since id should not be duplicated.
        db = next((data for data in client.ReadDatabases() if data['id'] == config.DOCUMENTDB_DATABASE))

        # Read collections and take first since id should not be duplicated.
        coll = next((coll for coll in client.ReadCollections(db['_self']) if coll['id'] == config.DOCUMENTDB_COLLECTION))

        # Read documents and take first since id should not be duplicated.
        doc = next((doc for doc in client.ReadDocuments(coll['_self']) if doc['id'] == config.DOCUMENTDB_DOCUMENT))

        # Take hello data from hello deploy_preference and increment our database
        doc[form.deploy_preference.data] = doc[form.deploy_preference.data] + 1
        replaced_document = client.ReplaceDocument(doc['_self'], doc)

        # Create a model toopass tooresults.html
        class VoteObject:
            choices = dict()
            total_votes = 0

        vote_object = VoteObject()
        vote_object.choices = {
            "Web Site" : doc['Web Site'],
            "Cloud Service" : doc['Cloud Service'],
            "Virtual Machine" : doc['Virtual Machine']
        }
        vote_object.total_votes = sum(vote_object.choices.values())

        return render_template(
            'results.html', 
            year=datetime.now().year, 
            vote_object = vote_object)

    else :
        return render_template(
            'vote.html', 
            title = 'Vote',
            year=datetime.now().year,
            form = form)
```


### <a name="create-hello-html-files"></a>Создать hello HTML-файлы
1. В обозревателе решений в hello **учебника** hello щелкните папку правой **шаблоны** папку, нажмите кнопку **добавить**и нажмите кнопку **новый элемент**. 
2. Выберите **HTML-страницу**, а затем в поле введите имя hello **create.html**. 
3. Повторите шаги 1 и 2 toocreate двух дополнительных файлов HTML: results.html и vote.html.
4. Добавьте следующий код слишком hello**create.html** в hello `<body>` элемента. В нем будет отображаться сообщение о создании новой базы данных, коллекции и документа.
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>{{ title }}.</h2>
    <h3>{{ message }}</h3>
    <p><a href="{{ url_for('vote') }}" class="btn btn-primary btn-large">Vote &raquo;</a></p>
    {% endblock %}
    ```
5. Добавьте следующий код слишком hello**results.html** в hello `<body`> элемент. Он отображает результаты hello hello опроса.
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>Results of hello vote</h2>
        <br />
   
    {% for choice in vote_object.choices %}
    <div class="row">
        <div class="col-sm-5">{{choice}}</div>
            <div class="col-sm-5">
                <div class="progress">
                    <div class="progress-bar" role="progressbar" aria-valuenow="{{vote_object.choices[choice]}}" aria-valuemin="0" aria-valuemax="{{vote_object.total_votes}}" style="width: {{(vote_object.choices[choice]/vote_object.total_votes)*100}}%;">
                                {{vote_object.choices[choice]}}
                </div>
            </div>
            </div>
    </div>
    {% endfor %}
   
    <br />
    <a class="btn btn-primary" href="{{ url_for('vote') }}">Vote again?</a>
    {% endblock %}
    ```
6. Добавьте следующий код слишком hello**vote.html** в hello `<body`> элемент. Он отображает hello опроса и принимает hello голоса. О регистрации hello голосов, hello управление передается через tooviews.py, где мы распознает приведения голос hello и добавить документ hello соответствующим образом.
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>What is your favorite way toohost an application on Azure?</h2>
    <form action="" method="post" name="vote">
        {{form.hidden_tag()}}
            {{form.deploy_preference}}
            <button class="btn btn-primary" type="submit">Vote</button>
    </form>
    {% endblock %}
    ```
7. В hello **шаблоны** папка, замените содержимое hello **index.html** hello следующее. Это служит hello стартовая страница для вашего приложения.
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>Python + Azure Cosmos DB Voting Application.</h2>
    <h3>This is a sample Cosmos DB voting application using PyDocumentDB</h3>
    <p><a href="{{ url_for('create') }}" class="btn btn-primary btn-large">Create/Clear hello Voting Database &raquo;</a></p>
    <p><a href="{{ url_for('vote') }}" class="btn btn-primary btn-large">Vote &raquo;</a></p>
    {% endblock %}
    ```

### <a name="add-a-configuration-file-and-change-hello-initpy"></a>Добавить файл конфигурации и изменить hello \_ \_init\_\_.py
1. В обозревателе решений щелкните правой кнопкой мыши hello **учебника** проекта, нажмите кнопку **добавить**, нажмите кнопку **новый элемент**выберите **пустой файл Python**, а затем Имя файла hello **config.py**. Этот файл необходим для работы форм в Flask. Его можно использовать tooprovide секретный ключ. В этом учебнике секретный ключ не требуется.
2. Добавьте следующее hello tooconfig.py код, вам потребуется значения hello tooalter **DOCUMENTDB\_узла** и **DOCUMENTDB\_ключ** hello следующем шаге.
   
    ```python
    CSRF_ENABLED = True
    SECRET_KEY = 'you-will-never-guess'
   
    DOCUMENTDB_HOST = 'https://YOUR_DOCUMENTDB_NAME.documents.azure.com:443/'
    DOCUMENTDB_KEY = 'YOUR_SECRET_KEY_ENDING_IN_=='
   
    DOCUMENTDB_DATABASE = 'voting database'
    DOCUMENTDB_COLLECTION = 'voting collection'
    DOCUMENTDB_DOCUMENT = 'voting document'
    ```
3. В hello [портал Azure](https://portal.azure.com/), перейдите toohello **ключей** колонки, щелкнув **Обзор**, **учетных записей Azure Cosmos DB**, дважды щелкните имя hello из hello toouse учетной записи, а затем нажмите кнопку hello **ключей** кнопку в hello **Essentials** области. В hello **ключей** колонки, hello копирования **URI** значение и вставьте его в hello **config.py** файл как значение hello для hello **DOCUMENTDB\_узла**  свойство. 
4. Вернитесь на портал Azure, в hello hello **ключей** колонке значение hello копирования hello **первичного ключа** или hello **вторичный ключ**и вставьте его в hello **config.py**  файл как значение hello для hello **DOCUMENTDB\_ключ** свойство.
5. В hello  **\_ \_init\_\_.py** файла, добавление следующей строкой hello. 
   
        app.config.from_object('config')
   
    Таким образом, содержимое hello hello файла:
   
    ```python
    from flask import Flask
    app = Flask(__name__)
    app.config.from_object('config')
    import tutorial.views
    ```
6. После добавления всех файлов hello, обозреватель решений должен выглядеть следующим образом:
   
    ![Снимок экрана: hello окно обозревателя решений Visual Studio](./media/documentdb-python-application/cosmos-db-python-solution-explorer.png)

## <a name="step-4-run-your-web-application-locally"></a>Шаг 4. Локальный запуск веб-приложения
1. Постройте решение hello, нажав клавиши **Ctrl**+**Shift**+**B**.
2. После успешного построения hello, запустите hello веб-сайт, нажав клавишу **F5**. На экране появится следующее hello.
   
    ![Здравствуйте, Python + Cosmos DB голосования приложения Azure отображается в веб-браузере снимок экрана](./media/documentdb-python-application/cosmos-db-pythonr-run-application.png)
3. Нажмите кнопку **Create/Clear hello базы данных с правом голоса** базы данных toogenerate hello.
   
    ![Снимок экрана: hello создать страницу веб-приложения hello — сведения о разработке](./media/documentdb-python-application/cosmos-db-python-run-create-page.png)
4. Затем нажмите кнопку **Голосовать** и сделайте свой выбор.
   
    ![Снимок экрана: hello веб-приложения с голосования осуществлены вопрос](./media/documentdb-python-application/cosmos-db-vote.png)
5. Для каждого голос, приведении он увеличивает на единицу счетчик соответствующие hello.
   
    ![Снимок экрана: hello результаты показано страницы голос hello](./media/documentdb-python-application/cosmos-db-voting-results.png)
6. Остановите отладку проекта hello, нажав клавиши Shift + F5.

## <a name="step-5-deploy-hello-web-application-tooazure"></a>Шаг 5: Развертывание приложения tooAzure hello web
Теперь, когда полное приложение hello правильно работать с Cosmos DB мы будем toodeploy этот tooAzure.

1. Щелкните правой кнопкой мыши проект hello в обозревателе решений (Убедитесь, что вы не еще выполняется локально) и выберите **публикации**.  
   
     ![Снимок экрана приветствия учебника, выбранного в обозревателе решений, с помощью параметра hello публикации выделен](./media/documentdb-python-application/image20.png)
2. В hello **публикации** установите флажок **службу приложений Microsoft Azure**выберите **создать новый**, а затем нажмите кнопку **публикации**.
   
    ![Снимок экрана окна hello публикации веб-сайта с выделенной службу приложений Microsoft Azure](./media/documentdb-python-application/cosmos-db-python-publish.png)
3. В hello **Создание приложения службы** диалогового окна введите имя hello веб-приложения вместе с вашей **подписки**, **группы ресурсов**, и **план служб приложений** , нажмите кнопку **создать**.
   
    ![Снимок экрана окна приложения Microsoft Azure окне приветствия](./media/documentdb-python-application/cosmos-db-python-create-app-service.png)
4. Через несколько секунд Visual Studio завершит публикацию вашего приложения и запустит браузер, где вы увидите свое творение, запущенное в Azure!

    ![Снимок экрана окна приложения Microsoft Azure окне приветствия](./media/documentdb-python-application/cosmos-db-python-appservice-created.png)

## <a name="troubleshooting"></a>Устранение неполадок
Если это первый Python приложение hello после выполнения на компьютере, убедитесь, что hello следующих папок (или эквивалентная Установка расположения hello) включаются в переменной путь:

    C:\Python27\site-packages;C:\Python27\;C:\Python27\Scripts;

Если появляется сообщение об ошибке на странице голос, а название проекта что-то отличное от **учебника**, убедитесь, что  **\_ \_init\_\_.py** Исправьте имя проекта в строку hello hello ссылки: `import tutorial.view`.

## <a name="next-steps"></a>Дальнейшие действия
Поздравляем! Просто завершения первого Python веб-приложения с помощью Cosmos DB и публикации его tooAzure.

Мы регулярно обновляем и улучшаем эту статью на основе ваших отзывов.  Один раз после завершения учебника hello, проверьте с помощью кнопки в hello верхней и нижней части этой страницы с правом голоса hello и быть tooinclude убедиться, что ваши отзывы о какие улучшения вы хотите сделать toosee. Если вы хотите нам toocontact напрямую, если вам свободного tooinclude адрес вашей электронной почты в комментарии.

tooadd дополнительные функциональные возможности tooyour веб-приложение hello просмотрите API-интерфейса в hello [Azure Cosmos DB Python SDK](documentdb-sdk-python.md).

Дополнительные сведения о Azure, Visual Studio и Python, в разделе hello [центре разработчиков Python](https://azure.microsoft.com/develop/python/). 

Дополнительные руководства термосе Python см. [hello термосе мегабайт-учебнике часть I: Hello, World!](http://blog.miguelgrinberg.com/post/the-flask-mega-tutorial-part-i-hello-world). 

[Visual Studio Express]: http://www.visualstudio.com/products/visual-studio-express-vs.aspx
[2]: https://www.python.org/downloads/windows/
[3]: https://www.microsoft.com/download/details.aspx?id=44266
[Microsoft Web Platform Installer]: http://www.microsoft.com/web/downloads/platform.aspx
[Azure portal]: http://portal.azure.com
