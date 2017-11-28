
1. <span data-ttu-id="f3766-101">Перейдите к [консоли Google Cloud](https://console.developers.google.com/project)и войдите в нее с помощью учетной записи Google.</span><span class="sxs-lookup"><span data-stu-id="f3766-101">Navigate to the [Google Cloud Console](https://console.developers.google.com/project), sign in with your Google account credentials.</span></span> 
2. <span data-ttu-id="f3766-102">Щелкните **Create Project** (Создание проекта), введите имя проекта и щелкните **Create** (Создать).</span><span class="sxs-lookup"><span data-stu-id="f3766-102">Click **Create Project**, type a project name, then click **Create**.</span></span> <span data-ttu-id="f3766-103">Выполните требуемую проверку с помощью SMS и снова щелкните **Create** (Создать).</span><span class="sxs-lookup"><span data-stu-id="f3766-103">If requested, carry out the SMS Verification, and click **Create** again.</span></span>
   
    ![Создание нового проекта](./media/mobile-services-enable-google-cloud-messaging/mobile-services-google-new-project.png)   
   
     <span data-ttu-id="f3766-105">В поле **Project name** (Имя проекта) введите новое имя проекта и щелкните **Create project** (Создать проект).</span><span class="sxs-lookup"><span data-stu-id="f3766-105">Type in your new **Project name** and click **Create project**.</span></span>
3. <span data-ttu-id="f3766-106">Щелкните **Utilities and More** (Служебные программы и другое) и **Project Information** (Сведения о проекте).</span><span class="sxs-lookup"><span data-stu-id="f3766-106">Click the **Utilities and More** button and then click **Project Information**.</span></span> <span data-ttu-id="f3766-107">Запишите **номер проекта**.</span><span class="sxs-lookup"><span data-stu-id="f3766-107">Make a note of the **Project Number**.</span></span> <span data-ttu-id="f3766-108">В клиенте это значение нужно будет указать как переменную `SenderId` .</span><span class="sxs-lookup"><span data-stu-id="f3766-108">You will need to set this value as the `SenderId` variable in the client app.</span></span>
   
    ![Служебные программы и другое](./media/mobile-services-enable-google-cloud-messaging/notification-hubs-utilities-and-more.png)
4. <span data-ttu-id="f3766-110">На панели мониторинга проекта в разделе **Mobile APIs** (API мобильных служб) выберите **Google Cloud Messaging**, на следующей странице щелкните **Enable API** (Включить API) и примите условия предоставления услуг.</span><span class="sxs-lookup"><span data-stu-id="f3766-110">In the project dashboard, under **Mobile APIs**, click **Google Cloud Messaging**, then on the next page click **Enable API** and accept the terms of service.</span></span> 
   
    ![Включение GCM](./media/mobile-services-enable-google-cloud-messaging/enable-GCM.png)
   
    ![Включение GCM](./media/mobile-services-enable-google-cloud-messaging/enable-gcm-2.png) 
5. <span data-ttu-id="f3766-113">На панели мониторинга проекта щелкните **Credentials** > **Create Credential** > **API Key** (Учетные данные > Создать учетные данные > Ключ API).</span><span class="sxs-lookup"><span data-stu-id="f3766-113">In the project dashboard, Click **Credentials** > **Create Credential** > **API Key**.</span></span> 
   
    ![](./media/mobile-services-enable-google-cloud-messaging/mobile-services-google-create-server-key.png)
6. <span data-ttu-id="f3766-114">В окне **Create a new key** (Создание нового ключа) щелкните **Server key** (Ключ сервера), введите имя ключа и щелкните **Create** (Создать).</span><span class="sxs-lookup"><span data-stu-id="f3766-114">In **Create a new key**, click **Server key**, type a name for your key, then click **Create**.</span></span>
7. <span data-ttu-id="f3766-115">Запишите значение **API KEY** (Ключ API).</span><span class="sxs-lookup"><span data-stu-id="f3766-115">Make a note of the **API KEY** value.</span></span>
   
    <span data-ttu-id="f3766-116">Этот ключ API службы Azure будут использовать для аутентификации в службе GCM и отправки push-уведомлений от имени вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="f3766-116">You will use this API key value to enable Azure to authenticate with GCM and send push notifications on behalf of your app.</span></span>

