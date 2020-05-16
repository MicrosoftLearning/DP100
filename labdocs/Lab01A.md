# Lab 1A: Creating an Azure Machine Learning Workspace

In this lab, you will create the Azure Machine Learning workspace that you will use throughout the rest of this course.

## Before You Start

To complete the labs in this course, you will need an Azure subscription. If you do not already have one, you can sign up for a free trial at [https://azure.microsoft.com](https://azure.microsoft.com).

If you are using an Azure Pass subscription, provided to you for this course, your account may not have been assigned to the subscription **Owner** role, which may be required for some operations in this course. To add your account to the **Owner** role:

1. Sign into the [Azure portal](https://portal.azure.com) and view your **Subscriptions**.
2. Select the subscription you created using an Azure pass (it will probably have a name similar to **Azure Pass - Sponsorship**).
3. In the blade for your subscription, open the **My Permissions** page, and then click the link on it to view complete access details for the subscription.
4. Under **Add role assignment**, click **Add**. Then select the following and click **Save**:
    - **Role**: Owner
    - **Assign access to**: Azure AD user, group, or service principal
    - **Select**: The Microsoft account you used to sign into Azure.

## Task 1: Create an Azure ML Workspace

As its name suggests, a workspace is a centralized place to manage all of the Azure ML assets you need to work on a machine learning project.

1. In the [Azure portal](https://portal.azure.com), create a new **Machine Learning** resource, specifying a unique workspace name and creating a new resource group in the region nearest your location. Select the **Enterprise** workspace edition.

   > **Note**: Basic edition workspaces have lower cost, but don't include capabilities like Auto ML, the Visual Designer, and data drift monitoring. For more details, see [Azure Machine Learning pricing](https://azure.microsoft.com/en-us/pricing/details/machine-learning/).

2. When the workspace and its associated resources have been created, view the workspace in the portal.

## Task 2: Explore the Azure ML Studio Interface

You can manage workspace assets in the Azure portal, but for data scientists, this tool contains lots of irrelevant information and links that relate to managing general Azure resources. An alternative, Azure ML-specific web interface for managing workspaces is available.

> **Note**: The web-based interface for Azure ML is named *Azure Machine Learning studio*, which you may find confusing as there is also a free *Azure Machine Learning Studio* product for creating machine learning models using a visual designer. A more scalable version of this visual designer is included in the new studio interface.

1. In the Azure portal blade for your Azure Machine Learning workspace, click the link to launch **Azure Machine Learning studio**; or alternatively, in a new browser tab, open [https://ml.azure.com](https://ml.azure.com). If prompted, sign in using the Microsoft account you used in the previous task and select your Azure subscription and workspace.
2. View the Azure Machine Learning studio interface for your workspace - you can manage all of the assets in your workspace from here.

## Task 3: Create Compute Resources

One of the benefits of Azure Machine Learning is the ability to create cloud-based compute on which you can run experiments and training scripts at scale.

1. In the Azure Machine Learning studio web interface for your workspace, view the **Compute** page. This is where you'll manage all the compute targets for your data science activities.
2. On the **Compute Instances** tab, add a new compute instance with the following settings. You'll use this as a workstation from which to test your model:
    - **Compute name**: *enter a unique name*
    - **Virtual Machine type**: CPU
    - **Virtual Machine size**: Standard_DS1_v2
3. While the compute instance is being created, switch to the **Compute Clusters** tab, and add a new compute cluster with the following settings. You'll use this to train a machine learning model:
    - **Compute name**: aml-cluster
    - **Virtual Machine type**: CPU
    - **Virtual Machine priority**: Dedicated
    - **Virtual Machine size**: Standard_DS2_v2
    - **Minimum number of nodes**: 0
    - **Maximum number of nodes**: 2
    - **Idle seconds before scale down**: 120
4. Note the **Inference Clusters** tab. This is where you can create and manage compute targets on which to deploy your trained models as web services for client applications to consume.
5. Note the **Attached Compute** tab. This is where you could attach a virtual machine or Databricks cluster that exists outside of your workspace.

    > **Note**: You'll explore compute targets in more detail later in the course.

## Task 4: Create Data Resources

Now that you have some compute resources that you can use to process data, you'll need a way to store and ingest the data to be processed.

1. In the *Studio* interface, view the **Datastores** page. Your Azure ML workspace already includes two datastores based on the Azure Storage account that was created along with the workspace. These are used to store notebooks, configuration files, and data.

   > **Note**: In a real-world environment, you'd likely add custom datastores that reference your business data stores - for example, Azure blob containers, Azure Data Lakes, Azure SQL Databases, and so on. You'll explore this later in the course.

2. In the *Studio* interface, view the **Datasets** page. Datasets represent specific data files or tables that you plan to work with in Azure ML.
3. Create a new dataset from web files, using the following settings:
    * **Basic Info**:
        * **Web URL**: https://aka.ms/diabetes-data
        * **Name**: diabetes dataset (*be careful to match the case and spacing*)
        * **Dataset type**: Tabular
        * **Description**: Diabetes data
    * **Settings and preview**:
        * **File format**: Delimited
        * **Delimiter**: Comma
        * **Encoding**: UTF-8
        * **Column headers**: Use headers from first file
        * **Skip rows**: None
    * **Schema**:
        * Include all columns other than **Path**
        * Review the automatically detected types
    * **Confirm details**:
        * Do not profile the dataset after creation
4. After the dataset has been created, open it and view the **Explore** page to see a sample of the data. This data represents details from patients who have been tested for diabetes, and you will use it in many of the subsequent labs in this course.

    > **Note**: You can optionally generate a *profile* of the dataset to see more details. You'll explore datasets in more detail later in the course.
