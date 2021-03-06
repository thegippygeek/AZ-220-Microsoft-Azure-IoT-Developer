# Create an IoT Hub using the Azure portal

The Azure IoT Hub is a fully managed service that enables reliable and secure bidirectional communications between IoT devices and Azure. The Azure IoT Hub service provides the following:

* Establish bidirectional communication with billions of IoT devices
* Multiple device-to-cloud and cloud-to-device communication options, including one-way messaging, file transfer, and request-reply methods.
* Built-in declarative message routing to other Azure services.
* A queryable store for device metadata and synchronized state information.
* Secure communications and access control using per-device security keys or X.509 certificates.
* Extensive monitoring for device connectivity and device identity management events.
* SDK device libraries for the most popular languages and platforms.

There are several methods that you can use to create an IoT Hub. For example, you can create an IoT Hub resource using the Azure portal, which is what you will do in ths task. But you can also create an IoT Hub (and other resources) programmatically. During this course we will be investigating additional methods that can be used to to create and manage Azure resources, including Azure CLI and PowerShell.

In this task, you will use the Azure portal to create an IoT Hub resource.

1. Login to [portal.azure.com](https://portal.azure.com) using your Azure account credentials.

    If you have more than one Azure account, be sure that you are logged in with the account that is tied to the subscription that you will be using for this course.  You may find it easiest to use an InPrivate / Incognito browser session to avoid accidentally using the wrong account.

1. Notice that the AZ-220 dashboard that you created in the previous task has been loaded.

    You will be adding resources to your dashboard as the course continues.

1. On the portal menu, click **+ Create a resource**.

    The Azure Marketplace is a collection of all the resources you can create in Azure. The marketplace contains resources from both Microsoft and the community.

1. In the Search textbox, type **IoT Hub** and then press **Enter**.

2. On the search results blade, click **IoT Hub**.

    Notice the list of _Useful Links_ displayed on this blade.

3. In the list of links, click **Documentation** to open a new browser tab.

    The _IoT Hub Documentation_ page is the root page for IoT Hub resources and documentation. You can use this page to explore current documentation and find tutorials and other resources that will help you to explore activities that are outside the scope of this course. We will refer you to the docs.microsoft.com site throughout this course for additional reading on specific topics.

4. Use your browser to close the documentation tab and navigate back to the Azure portal tab.

5. To begin the process of creating your new IoT Hub, click **Create**.

    >**Tip:** In the future, there are two other ways to get to the _Create_ experience of any Azure resource type:
        1. If you have the service in your Favorites, you can click the service to navigate to the list of instances, then click the _+ Add_ button at the top.
        2. You can search for the service name in the _Search_ box at the top of the portal to get to the list of instances, then click the _+ Add_ button at the top.

    Next, you need to specify information about the Hub and your subscription. The following steps walk you through the settings, explaining each of the fields as you fill them in.

6. On the _IoT hub_ blade, on the _Basics_ tab, ensure that the Azure **Subscription** that you intend to use for this course is selected.

7. To the right of **Resource Group**, open the **Select existing** dropdown, and then click **AZ-220-RG**

    This is the resource group that you created in the previous lab. We will be grouping the resources that we create for this course together in the same resource group. This should help you to clean up your resources when you have completed the course.

8. To the right of **Region**, open the drop-down list and select the same region as your resource group.  Make sure it supports Event Grid.

    As we saw previously, Azure is supported by a series of datacenters that are placed in regions all around the world. When you create something in Azure, you deploy it to one of these datacenter locations.

    > [!NOTE] For the current list of regions that support Event Grid, see the following link: [Products available by region](https://azure.microsoft.com/en-us/global-infrastructure/services/?products=event-grid&regions=all)
    
    > [!NOTE] When picking a region to host your app, keep in mind that picking a region close to your end users will decrease load/response times. If you are on the other side of the world from your end users, you should not be picking the region nearest you.

9.  To the right of **IoT Hub Name**, enter a globally unique name for your IoT Hub.

    To provide a globally unique name, enter **AZ-220-HUB-_{YOUR-ID}_** (remember to replace **_{YOUR-ID}_** with the unique ID you created in Lab 1.).

    For example: **AZ-220-HUB-CAH191021**

    The name of your IoT Hub must be globally unique because it is a publicly accessible resource that you must be able to access from any IP connected device.

    Consider the following when you specify a unique name for your new IoT Hub:

    * The value that you apply to _IoT Hub Name_ must be unique across all of Azure. This is true because the value assigned to the name will be used in the IoT Hub's connection string. Since Azure enables you to connect devices from anywhere in the world to your hub, it makes sense that all Azure hubs must be accessible from the Internet using the connection string and that connection strings must therefore be unique. We'll explore connection strings later in this lab.

    * The value that you assign to _IoT Hub Name_ cannot be changed once the app service has been created. If you do need to change the name, you'll need to create a new IoT Hub, re-register your devices to it, and delete your old IoT Hub.

    * The _IoT Hub Name_ field is a required field.

    > [!NOTE] Azure will ensure that the name you enter is unique. If the name that you enter is not unique, Azure will display an asterisk at the end of the name field as a warning. You can append the name suggested above with '**-01**' or '**-02**' as necessary to achieve a globally unique name.

10. At the top of the blade, click **Size and scale**.

    Take a minute to review the information presented on this blade.

11. To the right of Pricing and scale tier, open the dropdown and then select **S1: Standard tier** if it is not already selected.

    You can choose from several tier options depending on how many features you want and how many messages you send through your solution per day. The _S1_ tier that we are using in this course allows a total of 400,000 messages per unit per day and provides the all of the services that are required in this training. We won't actually need 400,000 messages per unit per day, but we will be using features provided at this tier level, such as _Cloud-to-device commands_, _Device management_, and _IoT Edge_. IoT Hub also offers a free tier that is meant for testing and evaluation. It has all the capabilities of the standard tier, but limited messaging allowances. However, you cannot upgrade from the free tier to either basic or standard. The free tier is intended for testing and evaluation. It allows 500 devices to be connected to the IoT hub and up to 8,000 messages per day. Each Azure subscription can create one IoT Hub in the free tier.

    > [!NOTE] The _S1 - Standard_ tier has a cost of $25.00 USD per month per unit. We will be specifying 1 unit. For details about the other tier options, see [Choosing the right IoT Hub tier for your solution](https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-scaling).

12. To the right of **Number of S1 IoT Hub units**, ensure that **1** is selected.

    As mentioned above, the pricing tier that you choose establishes the number of messages that your hub can process per unit per day. To increase the number of messages that you hub can process without moving to a higher pricing tier, you can increase the number of units. For example, if you want the IoT hub to support ingress of 700,000 messages, you choose *two* S1 tier units. For the IoT courses created by Microsoft we will be using just 1 unit.

13. Under _Advanced Settings_, ensure that **Device-to-cloud partitions** is set to **4**.

    The number of partitions relates the device-to-cloud messages to the number of simultaneous readers of these messages. Most IoT hubs will only need four partitions, which is the default value. For this course we will create our IoT Hub using the default number of partitions.

14. At the top of the blade, click **Review + create**.

15. At the bottom of the blade, to finalize the creation of your IoT Hub, click **Create**.

    Deployment can take a minute or more to complete. You can open the Azure portal Notification pane to monitor progress.

16. Notice that after a couple of minutes you receive a notification stating that your IoT Hub was successfully deployed to your **AZ-220-RG** resource group.

17. On the portal menu, click **Dashboard**, and then click **Refresh**.

    You should see that your resource group tile lists your new IoT Hub.
