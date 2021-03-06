## 建立裝置識別
在本節中，您將建立 Windows 主控台應用程式，它會在 IoT 中樞的身分識別登錄中建立新的裝置身分識別。裝置無法連線到 IoT 中樞，除非它在裝置身分識別登錄中具有項目。如需詳細資訊，請參閱 [IoT 中心開發人員指南][lnk-devguide-identity]的**裝置識別登錄**一節。執行這個主控台應用程式時，它會產生唯一的裝置識別碼及金鑰，當裝置向 IoT 中樞傳送裝置對雲端訊息時，可以用來識別裝置本身。

1. 在 Visual Studio 中，使用**主控台應用程式**專案範本將新的 Visual C# Windows 傳統桌面專案加入至目前的方案。確定 .NET Framework 為 4.5.1 或更新版本。將專案命名為 **CreateDeviceIdentity**。
   
    ![][10]
2. 在 [方案總管] 中，以滑鼠右鍵按一下 **CreateDeviceIdentity** 專案，然後按一下 [管理 NuGet 封裝]。
3. 在 [NuGet 封裝管理員] 視窗中選取 [瀏覽]、搜尋 **microsoft.azure.devices**、按一下 [安裝] 以安裝 [Microsoft.Azure.Devices] 封裝，並接受使用規定。
   
    ![][11]
4. 這會下載及安裝 [Microsoft Azure IoT - 服務 SDK][lnk-nuget-service-sdk] NuGet 封裝與其相依項目，並加入其參考。
5. 在 **Program.cs** 檔案開頭處新增下列 `using` 陳述式：
   
        using Microsoft.Azure.Devices;
        using Microsoft.Azure.Devices.Common.Exceptions;
6. 將下列欄位加入至 **Program** 類別，並將預留位置的值替換為您在上一節中為 IoT 中樞所建立的連接字串 ：
   
        static RegistryManager registryManager;
        static string connectionString = "{iothub connection string}";
7. 將下列方法加入至 **Program** 類別：
   
        private static async Task AddDeviceAsync()
        {
            string deviceId = "myFirstDevice";
            Device device;
            try
            {
                device = await registryManager.AddDeviceAsync(new Device(deviceId));
            }
            catch (DeviceAlreadyExistsException)
            {
                device = await registryManager.GetDeviceAsync(deviceId);
            }
            Console.WriteLine("Generated device key: {0}", device.Authentication.SymmetricKey.PrimaryKey);
        }
   
    這個方法會建立具有識別碼 **myFirstDevice** 的新裝置身分識別 (如果該裝置識別碼已經存在登錄中，程式碼就只會擷取現有的裝置資訊)。接著，應用程式會顯示該身分識別的主要金鑰。您將在此模擬裝置中使用此金鑰，連線到您的 IoT 中樞。
8. 最後，將下列幾行加入至 **Main** 方法：
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        AddDeviceAsync().Wait();
        Console.ReadLine();
9. 執行此應用程式，並記下裝置的金鑰。
   
    ![][12]

> [!NOTE]
> IoT 中樞身分識別登錄只會儲存裝置身分識別，以啟用對中樞的安全存取。它會儲存裝置識別碼和金鑰，來做為安全性認證，以及啟用或停用旗標，讓您停用個別裝置的存取。如果您的應用程式需要儲存其他裝置特定的中繼資料，它應該使用應用程式專用的存放區。如需詳細資訊，請參閱 [IoT 中樞開發人員指南][lnk-devguide-identity]。
> 
> 

## 接收裝置到雲端的訊息
在本節中，您將建立 Windows 主控台應用程式，以讀取來自 IoT 中樞的裝置到雲端訊息。IoT 中樞會公開與[事件中樞][lnk-event-hubs-overview]相容的端點以讓您讀取裝置到雲端訊息。為了簡單起見，本教學課程會建立的基本讀取器不適合用於高輸送量部署。[處理裝置到雲端的訊息][lnk-processd2c-tutorial]教學課程會說明如何大規模處理裝置到雲端的訊息。[開始使用事件中樞][lnk-eventhubs-tutorial]教學課程則會提供進一步資訊，說明如何處理來自事件中樞的訊息，而且此教學課程也適用於 IoT 中樞事件中樞相容端點。

> [!NOTE]
> 用於讀取裝置到雲端訊息的事件中樞相容端點一律會使用 AMQPS 通訊協定。
> 
> 

1. 在 Visual Studio 中，使用**主控台應用程式**專案範本將新的 Visual C# Windows 傳統桌面專案加入至目前的方案。確定 .NET Framework 為 4.5.1 或更新版本。將專案命名為 **ReadDeviceToCloudMessages**。
   
    ![][10]
2. 在 [方案總管] 中，以滑鼠右鍵按一下 **ReadDeviceToCloudMessages** 專案，然後按一下 [管理 NuGet 封裝]。
3. 在 [NuGet 封裝管理員] 視窗中，搜尋 **WindowsAzure.ServiceBus**，按一下 [安裝] 並接受使用規定。
   
    這會下載及安裝 [Azure 服務匯流排][lnk-servicebus-nuget]，並加入對它的參考和其所有相依性。此封裝可讓應用程式連接到 IoT 中樞上的事件中樞相容端點。
4. 在 **Program.cs** 檔案開頭處新增下列 `using` 陳述式：
   
        using Microsoft.ServiceBus.Messaging;
        using System.Threading;
5. 將下列欄位加入至 **Program** 類別，並將預留位置的值替換為您在*建立 IoT 中樞*一節中為 IoT 中樞所建立的連接字串：
   
        static string connectionString = "{iothub connection string}";
        static string iotHubD2cEndpoint = "messages/events";
        static EventHubClient eventHubClient;
6. 將下列方法加入至 **Program** 類別：
   
        private static async Task ReceiveMessagesFromDeviceAsync(string partition, CancellationToken ct)
        {
            var eventHubReceiver = eventHubClient.GetDefaultConsumerGroup().CreateReceiver(partition, DateTime.UtcNow);
            while (true)
            {
                if (ct.IsCancellationRequested) break;
                EventData eventData = await eventHubReceiver.ReceiveAsync();
                if (eventData == null) continue;
   
                string data = Encoding.UTF8.GetString(eventData.GetBytes());
                Console.WriteLine("Message received. Partition: {0} Data: '{1}'", partition, data);
            }
        }
   
    這個方法會使用 **EventHubReceiver** 執行個體接收來自所有 IoT 中樞裝置對雲端接收資料分割的訊息。請注意當您建立 **EventHubReceiver** 物件時如何傳遞 `DateTime.Now` 參數，使它只會收到它啟動後傳送的訊息。這很適合測試環境，因為如此一來您就可以看到目前的訊息集，但在生產環境中，您的程式碼應該要確定它能處理所有訊息，如需詳細資訊，請參閱[如何處理 IoT 中樞裝置到雲端訊息][lnk-processd2c-tutorial]教學課程。
7. 最後，將下列幾行加入至 **Main** 方法：
   
        Console.WriteLine("Receive messages. Ctrl-C to exit.\n");
        eventHubClient = EventHubClient.CreateFromConnectionString(connectionString, iotHubD2cEndpoint);
   
        var d2cPartitions = eventHubClient.GetRuntimeInformation().PartitionIds;
   
        CancellationTokenSource cts = new CancellationTokenSource();
   
        System.Console.CancelKeyPress += (s, e) =>
        {
          e.Cancel = true;
          cts.Cancel();
          Console.WriteLine("Exiting...");
        };
   
        var tasks = new List<Task>();
        foreach (string partition in d2cPartitions)
        {
           tasks.Add(ReceiveMessagesFromDeviceAsync(partition, cts.Token));
        }  
        Task.WaitAll(tasks.ToArray());

<!-- Links -->

[lnk-eventhubs-tutorial]: ../articles/event-hubs/event-hubs-csharp-ephcs-getstarted.md
[lnk-devguide-identity]: ../articles/iot-hub/iot-hub-devguide.md#identityregistry
[lnk-servicebus-nuget]: https://www.nuget.org/packages/WindowsAzure.ServiceBus
[lnk-event-hubs-overview]: ../articles/event-hubs/event-hubs-overview.md

[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
[lnk-processd2c-tutorial]: ../articles/iot-hub/iot-hub-csharp-csharp-process-d2c.md

<!-- Images -->
[10]: ./media/iot-hub-getstarted-cloud-csharp/create-identity-csharp1.png
[11]: ./media/iot-hub-getstarted-cloud-csharp/create-identity-csharp2.png
[12]: ./media/iot-hub-getstarted-cloud-csharp/create-identity-csharp3.png

<!---HONumber=AcomDC_0413_2016-->