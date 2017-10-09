### <a name="grant-mobile-engagement-access-tooyour-gcm-api-key"></a>Предоставление мобильного охвата доступа tooyour ключ API GCM
tooallow мобильного охвата toosend push-уведомления от вашего имени, необходимо toogrant ему получить доступ к tooyour ключ API. Это делается путем настройки и ввода ключа на портал мобильного охвата hello.

1. Классический портал Azure, убедитесь в приложение hello мы используем для этого проекта и нажмите кнопку hello **Владейте** кнопку в нижней части hello:
   
    ![](./media/mobile-engagement-android-send-push/engage-button.png)
2. Нажмите кнопку hello **параметры** -> **системные Push-уведомления** статьи tooenter ключ GCM:
   
    ![](./media/mobile-engagement-android-send-push/engagement-portal.png)
3. Нажмите кнопку hello **изменить** значок перед **ключ API** в hello **параметры GCM** статьи, как показано ниже:
   
    ![](./media/mobile-engagement-android-send-push/native-push-settings.png)
4. Во всплывающем hello вставьте hello ключ GCM сервера получен до и нажмите кнопку **ОК**.
   
    ![](./media/mobile-engagement-android-send-push/api-key.png)

## <a id="send"></a>Отправить уведомление о tooyour приложение
Теперь мы создадим простой принудительной уведомления кампанию, которая отправляет приложении tooour уведомлений push.

1. Перейдите toohello **ДОСТИЧЬ** вкладка на портале мобильного охвата.
2. Нажмите кнопку **новое извещение** toocreate кампанию push уведомления.
   
    ![](./media/mobile-engagement-android-send-push/new-announcement.png)
3. Настройка первого поля hello кампании через hello следующие шаги:
   
    ![](./media/mobile-engagement-android-send-push/campaign-first-params.png)
   
    а. Присвойте имя кампании.
   
    b. Выберите hello **тип доставки** как *Системное уведомление -> простой*: это hello простой Android типу push-уведомлений, заголовок и небольших строки текста.
   
    c. Выберите **время доставки** как *любое время* tooallow hello приложения tooreceive уведомление ли запускается приложение hello, или нет.
   
    d. В текст типа hello уведомления hello **заголовок** которой будут находиться в полужирным шрифтом в принудительной hello.
   
    д. Затем введите текст **сообщения**
4. Прокрутите список вниз и в hello **содержимого** выберите **только уведомления**.
   
    ![](./media/mobile-engagement-android-send-push/campaign-content.png)
5. Возможные основные кампании параметр hello, процедура завершена. Теперь прокрутите список вниз и нажмите hello **создать** кнопку toosave кампанию.
6. Последний шаг: щелкните **активировать** tooactivate вашей кампании toosend push-уведомлений.
   
    ![](./media/mobile-engagement-android-send-push/campaign-activate.png)

