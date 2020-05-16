# Lab 4A: Working with Datastores

Although it's fairly common for data scientists to work with data on their local file system, in an enterprise environment it can be more effective to store the data in a central location where multiple data scientists can access it. In this lab, you'll store data in the cloud, and use an Azure Machine Learning *datastore* to access it.

## Before You Start

Before you start this lab, ensure that you have completed [Lab 1A](Lab01A.md) and [Lab 1B](Lab01B.md), which include tasks to create the Azure Machine Learning workspace and other resources used in this lab.

## Task 1: Create an Azure Storage Container
You can use many kinds of Azure data source in Azure Machine Learning. In this lab, you'll create an Azure Storage account that includes a blob container.

1. Sign into the [Azure portal](https://portal.azure.com), and open the resource group containing your Azure Machine Learning workspace. Note that this already contains an Azure Storage account that was created with your workspace.

    >**Note**: The storage account created with your workspace is used by the service to store configuration data, notebooks, registered models, and so on. You can also use it to store data for experimentation and model training, but in many cases you'll want to manage this data separately.

2. Add a new **Storage account** to the resource group with the following settings:

    - **Storage account name**: A unique name.
    - **Location**: The same location as your workspace
    - **Performance**: Standard
    - **Account kind**: StorageV2 (general purpose v2)
    - **Replication**: Locally-redundant storage (LRS)
    - **Access tier (default)**: Hot
    - Use the default settings for networking

3. Wait for the storage account to be created, and then go to the resource in the portal.
4. Open the **Containers** page for the storage account, and add a container with the following settings:

    - **Name**: aml-data
    - **Public access level**: Private (no anonymous access)

5. After your container has been added, view the **Access Keys** page for your storage account and copy **key1** to the clipboard - you will need this in the next task.

## Task 2: Register an Azure Machine Learning Datastore

Now that you've created a storage container, you can register it as a datastore in your Azure Machine Learning workspace.

1. In [Azure Machine Learning studio](https://ml.azure.com), view the **Datastores** page for your workspace. The pre-defined datastores will be listed.
2. Create a new datastore with the following settings:
    - **Datastore name**: aml_data
    - **Datastore type**: Azure Blob Storage
    - **Account selection method**: From Azure subscription
    - **Subscription ID**: *Your Azure subscription*
    - **Storage account**: *The storage account you created in the previous task*
    - **Blob container**: aml-data
    - **Authentication type**: Account key
    - **Account key**: *Paste the key you copied in the previous task*
3. After the datastore has been added, verify that it is listed on the **Datastores** page.

## Task 3: Use the Azure Machine Learning SDK to access the Datastore

In this task, you'll use the Azure Machine Learning SDK to upload and download data to and from your datastore.

1. In [Azure Machine Learning studio](https://ml.azure.com), view the **Compute** page for your workspace; and on the **Compute Instances** tab, start your compute instance.
2. When the compute instance is running, refresh the Azure Machine Learning studio web page in your browser to ensure your authenticated session has not expired. Then click the **Jupyter** link to open the Jupyter home page in a new browser tab.
3. In the Jupyter home page, in the **Users/DP100** folder, open the **04A - Working with Datastores.ipynb** notebook. Then read the notes in the notebook, running each code cell in turn.
4. When you have finished running the code in the notebook, on the **File** menu, click **Close and Halt** to close it and shut down its Python kernel. Then close all Jupyter browser tabs.
5. If you're finished working with Azure Machine Learning for the day, in Azure Machine Learning studio, on the **Compute** page, on the **Compute Instances** tab, select your compute instance and click **Stop** to shut it down. Otherwise, leave it running for the next lab.
