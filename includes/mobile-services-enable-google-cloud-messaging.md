
1. Перейдите toohello [облачной консоли Google](https://console.developers.google.com/project), войдите с помощью учетной записи Google. 
2. Щелкните **Create Project** (Создание проекта), введите имя проекта и щелкните **Create** (Создать). Если она запрошена, выполнить hello SMS проверки и нажмите кнопку **создать** еще раз.
   
    ![Создание нового проекта](./media/mobile-services-enable-google-cloud-messaging/mobile-services-google-new-project.png)   
   
     В поле **Project name** (Имя проекта) введите новое имя проекта и щелкните **Create project** (Создать проект).
3. Нажмите кнопку hello **служебных программ и многое другое** и щелкните **сведения о проекте**. Запишите hello **номер проекта**. Вам потребуется tooset это значение как hello `SenderId` переменной в клиентское приложение hello.
   
    ![Служебные программы и другое](./media/mobile-services-enable-google-cloud-messaging/notification-hubs-utilities-and-more.png)
4. В hello проектов панели мониторинга, в разделе **Mobile API-интерфейсы**, нажмите кнопку **Google Cloud Messaging**, на следующей странице приветствия нажмите кнопку **включить API** и принять условия соглашения hello. 
   
    ![Включение GCM](./media/mobile-services-enable-google-cloud-messaging/enable-GCM.png)
   
    ![Включение GCM](./media/mobile-services-enable-google-cloud-messaging/enable-gcm-2.png) 
5. В hello мониторинга "проект", щелкните **учетные данные** > **Create Credential** > **ключ API**. 
   
    ![](./media/mobile-services-enable-google-cloud-messaging/mobile-services-google-create-server-key.png)
6. В окне **Create a new key** (Создание нового ключа) щелкните **Server key** (Ключ сервера), введите имя ключа и щелкните **Create** (Создать).
7. Запишите hello **ключ API** значение.
   
    Будет использовать этот tooenable значение ключа API Azure tooauthenticate с GCM и отправлять push-уведомлений от имени приложения.

