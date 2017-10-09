<!--author=SharS last changed: 1/14/2016 -->

> [!NOTE]
> При внесении изменений toohello адаптера StorSimple для SharePoint RBS конфигурации, вы должны войти в систему с учетной записью пользователя, которая принадлежит группе администраторов домена toohello. Кроме того для доступа к странице конфигурации hello из браузера на hello же разместить в качестве центра администрирования.
> 
> 

#### <a name="tooconfigure-rbs"></a>tooconfigure RBS
1. Откройте страницу центра администрирования SharePoint hello и обзор слишком**параметры системы**. 
2. В hello **Azure StorSimple** щелкните **настроить адаптер StorSimple**.
   
    ![Настройка адаптера StorSimple hello](./media/storsimple-sharepoint-adapter-configure-rbs/HCS_SSASP_ConfigRBS1-include.png) 
3. На hello **настроить адаптер StorSimple** страницы:
   
   1. Убедитесь в том, что hello **Включение редактирования путь** установлен флажок.
   2. В текстовом поле hello введите путь соглашения об универсальных именах (UNC) hello hello хранилища больших двоичных ОБЪЕКТОВ.
      
      > [!NOTE]
      > том хранилища больших двоичных ОБЪЕКТОВ Hello должен размещаться в томе iSCSI, настроенном на устройстве StorSimple hello.

   3. Нажмите кнопку hello **включить** расположенную под каждой из баз данных содержимого hello, что требуется tooconfigure для удаленного хранилища.
      
      > [!NOTE]
      > Hello хранилища больших двоичных ОБЪЕКТОВ должен быть общим и доступным, все серверы (WFE) веб-интерфейса и hello учетной записи пользователя, настроенного для фермы серверов SharePoint hello должен иметь доступ toohello папки.
      
      ![Включение поставщика RBS hello](./media/storsimple-sharepoint-adapter-configure-rbs/HCS_SSASP_ConfigRBS2-include.png)
      
      При включении или отключении RBS появится также следующие сообщение hello.
      
      ![Настройка включения и выключения адаптера StorSimple](./media/storsimple-sharepoint-adapter-configure-rbs/HCS_ConfigureStorSimpleAdapterEnableDisableMessage-include.png)

   4. Нажмите кнопку hello **обновление** конфигурация hello tooapply кнопок. При нажатии кнопки hello **обновление** кнопки hello состояние конфигурации RBS будет обновлена на всех интерфейсных веб-серверах и hello Вся ферма получит поддержку RBS. появляется после сообщения Hello.
      
      ![Сообщение о конфигурации адаптера](./media/storsimple-sharepoint-adapter-configure-rbs/HCS_SSASP_ConfigRBS3-include.png)
      
      > [!NOTE]
      > Если RBS настраивается для фермы SharePoint с очень большим числом баз данных (более 200), веб-страницы центра администрирования SharePoint hello время ожидания может истечь. В этом случае обновите страницу приветствия. Это не влияет на процесс настройки hello.

4. Проверка конфигурации hello:
   
   1. Войдите на веб-сайт центра администрирования SharePoint toohello и обзор toohello **настроить адаптер StorSimple** страницы.
   2. Проверьте соответствие введенных параметров hello toomake сведения о конфигурации hello. 
5. Проверьте правильность работы RBS.
   
   1. Отправьте tooSharePoint документа. 
   2. Обзор toohello UNC-путь, который вы настроили. Убедитесь, что hello структура каталога RBS создана и что он содержит отправлен hello объекта.
6. (Необязательно) Можно использовать Microsoft RBS hello `Migrate()` командлет PowerShell, входящий в состав SharePoint toomigrate существующего большого двоичного ОБЪЕКТА содержимого toohello устройства StorSimple. Дополнительные сведения см. в разделе [миграции содержимого в или из RBS в SharePoint 2013] [ 6] или [миграции содержимого в или из RBS (SharePoint Foundation 2010)] [7].
7. (Необязательно) При тестовой установке Вы можете убедиться, что hello большие двоичные объекты перемещены из базы данных содержимого hello, следующим образом: 
   
   1. Запустите SQL Management Studio
   2. Запустите запрос ListBlobsInDB_2010.sql или ListBlobsInDB_2013.sql hello, следующим образом.
      
      ```
      **ListBlobsInDB_2013.sql**
      
        USE WSS_Content
        GO
      
        SELECT DocStreams.DocId,
      
               LeafName AS Name,
               Content,
               AllDocs.Size AS OrigSizeOfContent,
               LEN(CAST(Content AS VARBINARY(MAX))) AS SizeOfContentInDB,
               DocStreams.RbsId,
               TimeLastModified
      
        FROM DocStreams
      
             INNER JOIN AllDocs ON DocStreams.DocId = AllDocs.Id
        ORDER BY TimeLastModified DESC
        GO
      
      **ListBlobsInDB_2010.sql**
      
        USE WSS_Content
        GO
      
        SELECT AllDocStreams.Id,
      
               LeafName AS Name,
               Content,
               AllDocs.Size AS OrigSizeOfContent,
               LEN(CAST(Content AS VARBINARY(MAX))) AS SizeOfContentInDB,
               RbsId,
               TimeLastModified
        FROM AllDocStreams
      
             INNER JOIN AllDocs ON AllDocStreams.Id = AllDocs.Id
        ORDER BY TimeLastModified DESC
        GO
      ```
      
      Если RBS настроены правильно, значение NULL должно отображаться в столбце SizeOfContentInDB hello для любого объекта, отправленного и успешно перемещенного в удаленном Хранилище.
8. (Необязательно) После настройки RBS и перемещения всех больших двоичных ОБЪЕКТОВ содержимого toohello устройства StorSimple можно переместить устройство toohello hello содержимого базы данных. При выборе базы данных контента toomove hello, рекомендуется настроить хранилище hello базы данных контента на устройстве hello как первичный том. Затем используйте установленные устройства StorSimple toohello базы данных контента hello toomigrate рекомендации наиболее SQL Server. 
   
   > [!NOTE]
   > Перемещение устройства toohello hello содержимого базы данных поддерживается только для серии StorSimple 8000 hello (не поддерживается для ряда hello 5000 или 7000).
   
   Если хранить большие двоичные объекты и базы данных содержимого hello в разных томах на устройстве StorSimple hello, рекомендуется настроить их в hello одном контейнере томов. Это гарантирует, что они будут подвергаться резервному копированию вместе.
   
   > [!WARNING]
   > Если RBS не включен, не рекомендуется перемещение устройства StorSimple toohello hello базы данных содержимого. Эта конфигурация не тестировалась.
   
9. Далее перейдите toohello: [Настройка сбора мусора](#configure-garbage-collection).

[6]: https://technet.microsoft.com/library/ff628254(v=office.15).aspx
[7]: https://technet.microsoft.com/library/ff628255(v=office.14).aspx
