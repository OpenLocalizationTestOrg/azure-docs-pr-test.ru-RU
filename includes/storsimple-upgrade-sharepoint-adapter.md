<!--author=SharS last changed: 9/17/15-->

### <a name="upgrade-sharepoint-2010-toosharepoint-2013-and-then-install-hello-storsomple-adapter-for-sharepoint"></a>Обновление SharePoint 2010 tooSharePoint 2013, а затем установите адаптер StorSomple hello для SharePoint
> [!IMPORTANT]
> Все файлы, перемещенные ранее хранилища tooexternal СДРес не будет доступно до завершения обновления hello и hello функция RBS не будет включена снова. пользователь toolimit влияние, выполните обновление или переустановку во время запланированного обслуживания.
> 
> 

#### <a name="tooupgrade-sharepoint-2010-toosharepoint-2013-and-then-install-hello-adapter"></a>tooSharePoint tooupgrade SharePoint 2010 2013, а затем установить адаптер hello
1. В ферме SharePoint 2010 hello Примечание hello BLOB путь к хранилищу для hello внешне выводятся большие двоичные объекты и hello баз данных содержимого, для которых включен RBS. 
2. Установка и настройка новой фермы SharePoint 2013 hello. 
3. Перемещение баз данных, приложений и семейств веб-сайтов из новой фермы SharePoint 2013 hello SharePoint 2010 ферма toohello. Инструкции см. слишком[Общие сведения об обновлении hello tooSharePoint 2013](https://technet.microsoft.com/library/cc262483.aspx).
4. Установите hello адаптера StorSimple для SharePoint в ферму новый hello. Go слишком[hello Установка адаптера StorSimple для SharePoint](#install-the-storsimple-adapter-for-sharepoint) для процедур.
5. Используя информацию hello, записанное на шаге 1, включите RBS для hello же набор баз данных содержимого и предоставить один большой двоичный объект хранения путь, который использовался в установке SharePoint 2010 hello hello. Go слишком[Настройка RBS](#configure-rbs) для процедур. После завершения этого шага, ранее во внешних хранилищах файлов должен быть доступен из новой фермы hello. 

### <a name="upgrade-hello-storsimple-adapter-for-sharepoint"></a>Обновление hello адаптера StorSimple для SharePoint
> [!IMPORTANT]
> Следует запланировать этого обновления toooccur в период планового обслуживания для hello следующих причин:
> 
> * Ранее во внешних хранилищах содержимое будет недоступен до переустановки адаптера hello.
> * Любой контент, отправленный toohello сайт после удаления предыдущей версии hello hello адаптера StorSimple для SharePoint, но перед установкой новой версии hello, будет храниться в базе данных содержимого hello. Вам потребуется toomove устройства StorSimple содержимого toohello после установки нового адаптера hello. Можно использовать hello Microsoft` RBS Migrate()` командлета PowerShell входит в состав hello toomigrate SharePoint. Дополнительные сведения см. в статье о [переносе содержимого в RBS и из RBS](https://technet.microsoft.com/library/ff628255.aspx). 
> 
> 

#### <a name="tooupgrade-hello-storsimple-adapter-for-sharepoint"></a>hello tooupgrade адаптер StorSimple для SharePoint
1. Удалите предыдущую версию hello адаптера StorSimple для SharePoint.
   
   > [!NOTE]
   > Будет автоматически отключена RBS на базах данных содержимого hello. Однако существующие большие двоичные объекты останутся на устройстве StorSimple hello. Так как RBS выключено и hello большие двоичные объекты не были перенесенных задней toohello баз данных содержимого, все запросы на этих больших двоичных объектов завершится ошибкой. 
   > 
   > 
2. Установка hello новый адаптер StorSimple для SharePoint. Hello новый адаптер автоматически распознает hello баз данных содержимого, которые ранее были включены или выключены для RBS и будет использовать предыдущие параметры hello.

