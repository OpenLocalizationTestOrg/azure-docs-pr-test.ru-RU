### <a name="prerequisites"></a>Предварительные требования
* Учетная запись Twilio.
* Проверенный номер телефона Twilio, на который можно получать SMS.
* Проверенный номер телефона Twilio, с которого можно отправлять SMS.

> [!NOTE]
> Если вы используете Twilio пробную учетную запись, можно отправлять только SMS слишком**проверить** номера телефонов.  
> 
> 

Перед использованием учетной записи Twilio в приложение логики, необходимо авторизовать hello логику приложения tooconnect tooyour Twilio учетной записи. К счастью это легко из можно сделать в приложении логику на портале Azure hello. 

Ниже приведены шаги tooauthorize hello вашей tooyour tooconnect логику приложения учетной записи Twilio.

1. Выберите tooTwilio соединения, в конструкторе логики приложения hello toocreate **Показать Microsoft управляемых API** в hello раскрывающемся списке, затем введите *Twilio* в поле поиска hello. Выберите триггер hello или действие, вам понравятся toouse:  
   ![](./media/connectors-create-api-twilio/twilio-0.png)
2. Если вы еще не создали tooTwilio все соединения перед, вы сможете получить tooprovide запрашиваемые учетные данные Twilio. Эти учетные данные будут используется tooauthorize вашей tooconnect приложение логики для и доступ к данным учетной записи Twilio:  
   ![](./media/connectors-create-api-twilio/twilio-1.png)  
3. Вам потребуется hello **идентификатор учетной записи Twilio** и **маркер доступа Twilio** с панели мониторинга hello в Twilio, поэтому вход toograb сейчас учетной записи Twilio tooyour эти два блока данных:  
   ![](./media/connectors-create-api-twilio/twilio-2.png)  
4. Twilio и логика приложения используют разные имена tooidentify эти два блока данных. Вот, как необходимо сопоставить их toohello логику приложения, диалоговое окно.![](./media/connectors-create-api-twilio/twilio-3.png)  
5. Выберите hello **создать подключение** кнопки:  
   ![](./media/connectors-create-api-twilio/twilio-4.png)
6. Обратите внимание, hello подключения будет создана и в этом случае свободного tooproceed с hello другие действия в приложении логики:  
   ![](./media/connectors-create-api-twilio/twilio-5.png)

