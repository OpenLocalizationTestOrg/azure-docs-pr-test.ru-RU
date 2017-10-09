Из-за текущей работы hello версия пакета SDK для Android, устанавливается в Android Studio могут не соответствовать версии hello в коде hello. Hello Android SDK, на которые ссылается этот учебник — 23, hello версии последней на момент написания статьи hello. номер версии Hello может увеличиться по мере новые выпуски SDK отображаются hello и мы рекомендуем использовать hello последней доступной версии.

Два признака несоответствия версии:

- При построении или перестройте проект hello, может возникнуть Gradle ошибок как «**сбой целевой toofind Google Inc.:Google APIs:n**».
- Стандартные объекты Android в коде, которые должны разрешаться на основе инструкций `import` , могут создавать сообщения об ошибках.

Если любой из этих появится, hello версию Android SDK, установленный в Android Studio hello могут не соответствовать целевой пакет SDK для hello hello загрузки проекта. версия tooverify hello, сделать hello следующие изменения:

1. В Android Studio щелкните **Средства** > **Android** > **SDK Manager** (Диспетчер пакетов SDK). Если вы не установили последнюю версию hello hello SDK платформы, нажмите кнопку tooinstall его. Запишите номер версии hello.
2. На hello **обозревателя проектов** в разделе **сценариев Gradle**, откройте файл hello **build.gradle (modeule: приложение)**. Убедитесь, что hello **compileSdkVersion** и **buildToolsVersion** задаются toohello установить последнюю версию пакета SDK. теги Hello может выглядеть следующим образом:

             compileSdkVersion 'Google Inc.:Google APIs:23'
            buildToolsVersion "23.0.2"
3. В обозревателе проектов Android Studio, щелкните правой кнопкой мыши узел проекта hello hello выберите **свойства**, а в левом столбце hello выберите **Android**. Убедитесь, что hello **цели построения проекта** задано toohello совпадает с версией пакета SDK для hello **targetSdkVersion**.

В Android Studio файл манифеста hello больше не используется toospecify hello целевого пакета SDK и Минимальная версия пакета SDK, в отличие от случая hello с Eclipse.
