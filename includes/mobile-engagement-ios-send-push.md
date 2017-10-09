### <a name="grant-access-tooyour-push-certificate-toomobile-engagement"></a>Предоставление доступа tooyour Push-сертификатов tooMobile Engagement
tooallow мобильного охвата toosend Push-уведомления от вашего имени, необходимо его доступ к сертификату tooyour toogrant. Это делается путем настройки и введя свой сертификат в портал мобильного охвата hello. Убедитесь, что получили сертификат P12, как описано в [документации Apple](https://developer.apple.com/library/prerelease/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html#//apple_ref/doc/uid/TP40012582-CH26-SW6)

1. Перейдите tooyour порталу мобильного охвата. Убедитесь в правильный hello и выберите команду hello **Владейте** кнопку в нижней части hello:
   
    ![](./media/mobile-engagement-ios-send-push/engage-button.png)
2. Щелкните hello **параметры** странице портала обязательств. Из отсутствует щелкните hello **системные Push-уведомления** статьи tooupload сертификата p12:
   
    ![](./media/mobile-engagement-ios-send-push/engagement-portal.png)
3. Выберите сертификат P12, отправьте его и введите пароль:
   
    ![](./media/mobile-engagement-ios-send-push/native-push-settings.png)

## <a id="send"></a>Отправить уведомление о tooyour приложение
Теперь мы создадим простой кампании Push-уведомление, будет отправлять push tooour приложения:

1. Перейдите toohello **достичь** вкладка на портале мобильного охвата.
2. Нажмите кнопку **новое извещение** toocreate кампании push-уведомлений
   
    ![](./media/mobile-engagement-ios-send-push/new-announcement.png)
3. Hello первого поля кампании настройки:
   
    ![](./media/mobile-engagement-ios-send-push/campaign-first-params.png)
   
   * Задайте **имя** кампании. 
   * Выберите hello **время доставки** как **только вне приложения**: это hello простой Apple типу push-уведомлений, предоставляющем некоторый текст.
   * В текст уведомления hello, введите первый hello **заголовок** которого будет первая строка hello в отправке hello.
   * Затем введите ваш **сообщение** которого будет вторую строку hello
4. Прокрутите вниз и выберите раздел содержимого hello **только уведомления**
   
    ![](./media/mobile-engagement-ios-send-push/campaign-content.png)
5. Параметр hello основные кампании, процедура завершена. Теперь прокрутите список вниз и выберите команду **создать** кнопку toosave кампанию push уведомления. 
6. И наконец — щелкнуть **активировать** toosend push-уведомлений. 
   
    ![](./media/mobile-engagement-ios-send-push/campaign-activate.png)
7. Вы сможете получать уведомления hello на устройства iOS в центре уведомлений hello hello следующим образом:
   
    ![](./media/mobile-engagement-ios-send-push/iphone-notification.png)
8. При наличии Apple Watch, связан с этим устройством iOS затем откроется hello уведомление на ваш Apple Watch:
   
    ![](./media/mobile-engagement-ios-send-push/apple-watch.png)

