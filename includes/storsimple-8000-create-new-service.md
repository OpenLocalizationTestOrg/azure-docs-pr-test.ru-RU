<!--author=alkohli last changed:02/10/2017-->


#### <a name="toocreate-a-new-service"></a>toocreate новой службы

1. Использовать ваш toolog учетные данные учетной записи Майкрософт на toohello [портал Azure](https://portal.azure.com/).

2. В hello портал Azure, щелкните  **+**  и выберите в hello marketplace **все**.

    ![Создание диспетчера устройств StorSimple](./media/storsimple-8000-create-new-service/createssdevman1.png)

    Найдите _физическое устройство StorSimple_. Выберите **Серия физического устройства StorSimple** и щелкните **Создать**. Кроме того, в hello портала Azure щелкните  **+**  и затем в разделе **хранения**, нажмите кнопку **физического устройства серии StorSimple**.

    ![Создание диспетчера устройств StorSimple](./media/storsimple-8000-create-new-service/createssdevman11.png)

3. В hello **устройства StorSimple** колонке hello следующие действия:
   
   1. В поле **Имя ресурса** укажите уникальное имя для службы. Это имя — это понятное имя, которое можно использовать службы tooidentify hello. Hello имя может содержать от 2 до 50 символов, которые могут быть буквы, цифры и дефисы. Hello имя должно начинаться и заканчиваться буквой или цифрой.

   2. Выберите **подписки** из раскрывающегося списка hello. Подписка Hello — связанного tooyour выставления счетов для учетной записи. Это поле отсутствует, если у вас имеется только одна подписка.

   3. **Группа ресурсов** — **создайте** группу ресурсов или выберите **имеющуюся**. Дополнительные сведения см. в статье [Рекомендации по группам ресурсов Azure](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-infrastructure-resource-groups-guidelines/).
   
   4. Укажите **Расположение** службы. Как правило выберите расположение ближайшего toohello географический регион место toodeploy устройства. Вы также можете toofactor в hello следующие вопросы: 
      
      * При наличии существующих рабочих нагрузок в Azure, также будут toodeploy с устройством StorSimple следует использовать этому центру обработки данных.
      * Служба диспетчера устройств StorSimple и служба хранилища Azure могут находиться в разных расположениях. В этом случае вы: hello необходимые toocreate устройства StorSimple и учетной записи хранилища Azure отдельно. toocreate учетную запись хранения Azure перейдите toohello службе хранилища Azure в hello портал Azure и следуйте указаниям hello [создать учетную запись хранилища Azure](../articles/storage/common/storage-create-storage-account.md#create-a-storage-account). После создания этой учетной записи, добавьте его службе диспетчера StorSimple устройство toohello, следуя указаниям hello [настроить новую учетную запись хранилища для службы hello](../articles/storsimple/storsimple-8000-deployment-walkthrough-u2.md#configure-a-new-storage-account-for-the-service).

   5. Выберите **создать новую учетную запись хранения** tooautomatically создать учетную запись хранения со службой hello. Укажите имя для этой учетной записи хранения. Если требуется хранить данные в другом расположении, снимите этот флажок.

   6. Проверьте **toodashboard ПИН-код** Если требуется служба toothis быструю ссылку на панели мониторинга.
      
   7. Нажмите кнопку **создать** toocreate hello устройства StorSimple.

       ![Создание диспетчера устройств StorSimple](./media/storsimple-8000-create-new-service/createssdevman2.png)
   
Создание службы Hello занимает несколько минут. После успешного создания службы hello, вы увидите уведомление, и открывается новая колонка службы hello.
   
![Создание диспетчера устройств StorSimple](./media/storsimple-8000-create-new-service/createssdevman5.png)


