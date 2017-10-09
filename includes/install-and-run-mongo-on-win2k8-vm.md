Выполните эти шаги tooinstall и запустите MongoDB на виртуальной машине под управлением Windows Server.

> [!IMPORTANT]
> Функции безопасности MongoDB, такие как проверка подлинности и привязка IP-адреса, не включены по умолчанию. Средства безопасности должна быть включена перед развертыванием MongoDB tooa рабочей среде.  Дополнительные сведения см. в документе [Безопасность и проверка подлинности](http://www.mongodb.org/display/DOCS/Security+and+Authentication).
>
>

1. После подключения toohello виртуальной машины, с помощью удаленного рабочего стола, откройте Internet Explorer из hello **запустить** меню на виртуальной машине hello.
2. Выберите hello **средства** кнопку в правом верхнем углу hello.  В **обозревателя**выберите hello **безопасности** , а затем выберите hello **надежных узлов** значок и выберите hello **узлы** кнопка. Добавить *https://\*. mongodb.org* toohello список надежных сайтов.
3. Go слишком[загружает - MongoDB](https://www.mongodb.com/download-center#community).
4. Найти hello **текущей стабильной версии** из **сервер сообщества**выберите последнюю hello **64-разрядных** версии в столбце Windows hello. Загрузить, а затем запустите установщик MSI hello.
5. Приложение MongoDB обычно устанавливается в папку C:\Program Files\MongoDB. Поиск переменные среды на рабочем столе hello и добавить hello MongoDB двоичные файлы путь toohello переменной PATH. Например может оказаться hello двоичные файлы в C:\Program Files\MongoDB\Server\3.4\bin на компьютере.
6. Создание MongoDB каталоги данных и журналов в hello диск данных (например диск **F:**) созданный на предыдущих шагах hello. Из **запустить**выберите **командной строки** tooopen окно командной строки.  Тип:

        C:\> F:
        F:\> mkdir \MongoData
        F:\> mkdir \MongoLogs
7. базы данных toorun hello, выполните:

        F:\> C:
        C:\> mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log

    Все сообщения журнала, направленной toohello *F:\MongoLogs\mongolog.log* файла, что и сервер mongod.exe начинается и предварительно размещает файлы журнала. Он может занять несколько минут для MongoDB toopreallocate hello файлов журнала и начать ожидать соединения. командную строку Hello остается ориентированы на эту задачу во время выполнения экземпляра MongoDB.
8. hello toostart MongoDB административной оболочки, откройте другой командное окно от **запустить** и типа hello следующие команды:

        C:\> cd \my_mongo_dir\bin  
        C:\my_mongo_dir\bin> mongo  
        >db  
        test
        > db.foo.insert( { a : 1 } )  
        > db.foo.find()  
        { _id : ..., a : 1 }  
        > show dbs  
        ...  
        > show collections  
        ...  
        > help  

    Hello база данных создается путем вставки hello.
9. Кроме того, можно установить файл mongod.exe в качестве службы.

        C:\> mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log --logappend  --install

    В этом случае будет установлена служба с именем MongoDB и описанием Mongo DB. Hello `--logpath` должен указываться используется toospecify файл журнала, с момента hello запущена служба не имеет toodisplay вывода окна команд.  Hello `--logappend` параметр указывает на то, что перезапуск службы hello вызывает tooappend toohello существующего файла журнала.  Hello `--dbpath` указывает расположение hello hello данных каталога. Дополнительные сведения о параметрах командной строки, связанных со службами, см. [здесь][MongoWindowsSvcOptions].

    toostart служба hello, выполните следующую команду:

        C:\> net start MongoDB
10. Теперь, когда MongoDB установлена и запущена, вам требуется tooopen порт в брандмауэре Windows, вы можете удаленно подключиться tooMongoDB.  Из hello **запустить** последовательно выберите пункты **Администрирование** и затем **брандмауэр Windows в режиме повышенной безопасности**.
11. ) в левой области hello выберите **правила для входящих подключений**.  В hello **действия** на панели справа, hello выберите **новое правило...** .

    ![Брандмауэр Windows][Image1]

    (б) в hello **правило мастера**выберите **порт** и нажмите кнопку **Далее**.

    ![Брандмауэр Windows][Image2]

    11.3. Выберите **TCP** и **Определенные локальные порты**.  Укажите порт «27017» (порт по умолчанию Здравствуй прослушивает MongoDB) и нажмите кнопку **Далее**.

    ![Брандмауэр Windows][Image3]

    d) выберите **разрешить подключение hello** и нажмите кнопку **Далее**.

    ![Брандмауэр Windows][Image4]

    11.5. Нажмите кнопку **Далее** еще раз.

    ![Брандмауэр Windows][Image5]

    f) укажите имя для правила hello, например «MongoPort» и нажмите кнопку **Готово**.

    ![Брандмауэр Windows][Image6]

12. Если не настроить конечную точку для MongoDB при создании виртуальной машины hello, можно сделать сейчас. Необходимые правила брандмауэра hello и hello конечной точки toobe может tooconnect tooMongoDB удаленно.

  В hello портал Azure, щелкните **виртуальные машины (классические)**, щелкните имя hello на новую виртуальную машину, затем щелкните **конечные точки**.

    ![Endpoints][Image7]

13. Щелкните **Добавить**.

14. Добавить конечную точку с именем «Mongo», протокол **TCP**и оба **открытый** и **закрытый** порты набор слишком «27017». Открытие этого порта позволяет MongoDB toobe удаленного доступа.

    ![Endpoints][Image9]

> [!NOTE]
> порт Hello 27017 — hello по умолчанию порт MongoDB. Этот порт по умолчанию можно изменить, указав hello `--port` параметра при запуске сервера mongod.exe hello. Убедитесь, что toogive hello одинаковый номер порта в брандмауэре hello и hello конечной точки «Mongo» в hello предшествующие инструкции.
>
>

[MongoDownloads]: http://www.mongodb.org/downloads

[MongoWindowsSvcOptions]: http://www.mongodb.org/display/DOCS/Windows+Service


[Image1]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall1.png
[Image2]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall2.png
[Image3]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall3.png
[Image4]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall4.png
[Image5]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall5.png
[Image6]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall6.png
[Image7]: ./media/install-and-run-mongo-on-win2k8-vm/menusendpointadd.png
<!-- Removed 03/08/2017. Not in new portal. -->
<!-- [Image8]: ./media/install-and-run-mongo-on-win2k8-vm/WinVmAddEndpoint2.png
-->
[Image9]: ./media/install-and-run-mongo-on-win2k8-vm/newendpointdetails.png
