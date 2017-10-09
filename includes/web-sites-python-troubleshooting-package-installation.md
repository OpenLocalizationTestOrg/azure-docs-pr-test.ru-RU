Некоторые пакеты могут не установиться с помощью pip при запуске Azure.  Просто возможно, этот пакет hello не доступен на hello индекс пакета Python.  Возможно, что компилятор не требуется (компилятора недоступен на hello машины выполняющегося hello веб-приложения в службе приложений Azure).

В этом разделе мы рассмотрим способы toodeal с этой проблемой.

### <a name="request-wheels"></a>Запрос архивов wheel
Если установка пакета hello требует компилятора, следует обратитесь toorequest владельца пакета hello, колеса доступны для пакета hello.

С hello последних доступность [Microsoft Visual C++ компилятор для Python 2.7][Microsoft Visual C++ Compiler for Python 2.7], теперь стало проще toobuild пакеты, имеющие машинного кода Python 2.7.

### <a name="build-wheels-requires-windows"></a>Сборки wheel (требуется Windows)
Примечание: При использовании этого параметра, убедитесь, что пакет toocompile hello, с помощью среды Python, который соответствует hello/архитектура и версии платформы, используемой на веб-приложения hello в службе приложений Azure (Windows/32-bit/2.7 или 3.4).

Если hello пакет не устанавливается, поскольку компилятору требуется, можно установить компилятора hello на локальном компьютере и сборка колеса для hello пакета, который затем будут включены в репозитории.

Пользователей Mac и Linux: Если у вас нет доступа tooa Windows компьютера, см. раздел [создания виртуальной машины под управлением Windows] [ Create a Virtual Machine Running Windows] как toocreate ВМ в Azure.  Использовать toobuild hello колеса, добавьте их toohello репозитория и при необходимости отменить hello виртуальной Машины. 

Python 2.7, можно установить [Microsoft Visual C++ компилятор для Python 2.7][Microsoft Visual C++ Compiler for Python 2.7].

Python 3.4, можно установить [Microsoft Visual C++ 2010 Express][Microsoft Visual C++ 2010 Express].

toobuild колеса, вам потребуется hello колесо пакета:

    env\scripts\pip install wheel

Вы воспользуетесь `pip wheel` toocompile зависимость:

    env\scripts\pip wheel azure==0.8.4

Будет создан файл .whl в папке \wheelhouse hello.  Добавьте папку \wheelhouse hello и колесо файлы tooyour репозитория.

Изменить ваш hello tooadd requirements.txt `--find-links` параметр вверху hello. Это заставляет toolook PIP-адрес для точного совпадения в локальной папке hello перед индекс пакета python toohello постоянной.

    --find-links wheelhouse
    azure==0.8.4

Следует tooinclude вообще индексировать все зависимости, в hello \wheelhouse папку и не используйте hello пакет python можно принудительно hello пакета pip tooignore индекс путем добавления `--no-index` toohello верхней части вашего requirements.txt.

    --no-index

### <a name="customize-installation"></a>Настройка установки
Можно настроить tooinstall сценария hello развертывания пакета в виртуальной среде hello, с помощью альтернативных установщика, таких как просто\_установки.  Закомментированный пример см. в файле deploy.cmd.  Убедитесь, что эти пакеты не указанные в requirements.txt tooprevent pip из их установки.

Добавьте этот сценарий развертывания toohello:

    env\scripts\easy_install somepackage

Также может быть легко может toouse\_установите tooinstall из EXE-файла установщика (некоторые являются ZIP-совместимость, поэтому просто\_их поддерживает установки).  Добавить репозиторий tooyour установщика hello и просто вызвать\_установить посредством передачи toohello путь hello исполняемый.

Добавьте этот сценарий развертывания toohello:

    env\scripts\easy_install "%DEPLOYMENT_SOURCE%\installers\somepackage.exe"

### <a name="include-hello-virtual-environment-in-hello-repository-requires-windows"></a>Включить hello виртуальной среды в репозиторий hello (необходима операционная система Windows)
Примечание: При использовании этого параметра, убедитесь, что toouse виртуальную среду, которая соответствует hello/архитектура и версии платформы, используемой на веб-приложения hello в службе приложений Azure (Windows/32-bit/2.7 или 3.4).

При включении виртуальной среды hello в репозитории hello можно предотвратить скрипт развертывания hello выполнив управления виртуальной среды в Azure, создав пустой файл:

    .skipPythonDeployment

Рекомендуется удалять hello существующую виртуальную среду на приложение hello, оставшиеся файлы tooprevent из при автоматически управляет hello виртуальной среды.

[Create a Virtual Machine Running Windows]: http://azure.microsoft.com/documentation/articles/virtual-machines-windows-hero-tutorial/
[Microsoft Visual C++ Compiler for Python 2.7]: http://aka.ms/vcpython27
[Microsoft Visual C++ 2010 Express]: http://go.microsoft.com/?linkid=9709949
