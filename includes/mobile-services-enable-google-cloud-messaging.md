
1. <span data-ttu-id="2f50c-101">Перейдите toohello [облачной консоли Google](https://console.developers.google.com/project), войдите с помощью учетной записи Google.</span><span class="sxs-lookup"><span data-stu-id="2f50c-101">Navigate toohello [Google Cloud Console](https://console.developers.google.com/project), sign in with your Google account credentials.</span></span> 
2. <span data-ttu-id="2f50c-102">Щелкните **Create Project** (Создание проекта), введите имя проекта и щелкните **Create** (Создать).</span><span class="sxs-lookup"><span data-stu-id="2f50c-102">Click **Create Project**, type a project name, then click **Create**.</span></span> <span data-ttu-id="2f50c-103">Если она запрошена, выполнить hello SMS проверки и нажмите кнопку **создать** еще раз.</span><span class="sxs-lookup"><span data-stu-id="2f50c-103">If requested, carry out hello SMS Verification, and click **Create** again.</span></span>
   
    ![Создание нового проекта](./media/mobile-services-enable-google-cloud-messaging/mobile-services-google-new-project.png)   
   
     <span data-ttu-id="2f50c-105">В поле **Project name** (Имя проекта) введите новое имя проекта и щелкните **Create project** (Создать проект).</span><span class="sxs-lookup"><span data-stu-id="2f50c-105">Type in your new **Project name** and click **Create project**.</span></span>
3. <span data-ttu-id="2f50c-106">Нажмите кнопку hello **служебных программ и многое другое** и щелкните **сведения о проекте**.</span><span class="sxs-lookup"><span data-stu-id="2f50c-106">Click hello **Utilities and More** button and then click **Project Information**.</span></span> <span data-ttu-id="2f50c-107">Запишите hello **номер проекта**.</span><span class="sxs-lookup"><span data-stu-id="2f50c-107">Make a note of hello **Project Number**.</span></span> <span data-ttu-id="2f50c-108">Вам потребуется tooset это значение как hello `SenderId` переменной в клиентское приложение hello.</span><span class="sxs-lookup"><span data-stu-id="2f50c-108">You will need tooset this value as hello `SenderId` variable in hello client app.</span></span>
   
    ![Служебные программы и другое](./media/mobile-services-enable-google-cloud-messaging/notification-hubs-utilities-and-more.png)
4. <span data-ttu-id="2f50c-110">В hello проектов панели мониторинга, в разделе **Mobile API-интерфейсы**, нажмите кнопку **Google Cloud Messaging**, на следующей странице приветствия нажмите кнопку **включить API** и принять условия соглашения hello.</span><span class="sxs-lookup"><span data-stu-id="2f50c-110">In hello project dashboard, under **Mobile APIs**, click **Google Cloud Messaging**, then on hello next page click **Enable API** and accept hello terms of service.</span></span> 
   
    ![Включение GCM](./media/mobile-services-enable-google-cloud-messaging/enable-GCM.png)
   
    ![Включение GCM](./media/mobile-services-enable-google-cloud-messaging/enable-gcm-2.png) 
5. <span data-ttu-id="2f50c-113">В hello мониторинга "проект", щелкните **учетные данные** > **Create Credential** > **ключ API**.</span><span class="sxs-lookup"><span data-stu-id="2f50c-113">In hello project dashboard, Click **Credentials** > **Create Credential** > **API Key**.</span></span> 
   
    ![](./media/mobile-services-enable-google-cloud-messaging/mobile-services-google-create-server-key.png)
6. <span data-ttu-id="2f50c-114">В окне **Create a new key** (Создание нового ключа) щелкните **Server key** (Ключ сервера), введите имя ключа и щелкните **Create** (Создать).</span><span class="sxs-lookup"><span data-stu-id="2f50c-114">In **Create a new key**, click **Server key**, type a name for your key, then click **Create**.</span></span>
7. <span data-ttu-id="2f50c-115">Запишите hello **ключ API** значение.</span><span class="sxs-lookup"><span data-stu-id="2f50c-115">Make a note of hello **API KEY** value.</span></span>
   
    <span data-ttu-id="2f50c-116">Будет использовать этот tooenable значение ключа API Azure tooauthenticate с GCM и отправлять push-уведомлений от имени приложения.</span><span class="sxs-lookup"><span data-stu-id="2f50c-116">You will use this API key value tooenable Azure tooauthenticate with GCM and send push notifications on behalf of your app.</span></span>

