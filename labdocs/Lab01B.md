# Lab 1B: Working with Azure Machine Learning Tools

In this lab, you will explore various tools for working with an Azure Machine Learning workspace.

## Before You Start

Before starting this lab, you must have created an Azure Machine Learning workspace by following the instructions in the [previous lab](Lab01A.md).

## Task 1: Use the Azure ML SDK in a Compute Instance

You can perform most asset management tasks to set up your environment in the *Studio* interface, but it's also important to be able to script configuration tasks to make them easier to repeat and automate.

1. In [Azure Machine Learning studio](https://ml.azure.com), on the **Compute** page for your workspace, view the **Compute Instances** tab, and if necessary, click **Refresh** periodically until the compute instance you created in the previous lab has started.
2. Refresh the Azure Machine Learning studio web page in your browser to ensure your authenticated session has not expired. Then click your compute instance's **Jupyter** link  to open Jupyter Notebooks in a new tab. If prompted, sign in using the Microsoft account associated with your Azure subscription.
3. In the notebook environment, create a new **Terminal**. This will open a new tab with a command shell.
4. The Azure Machine Learning SDK is already installed in the compute instance image, but it's worth ensuring you have the latest version, with the optional packages you'll need in this course; so enter the following command to update the SDK packages:

    ```bash
    pip install --upgrade azureml-sdk[notebooks,automl,explain]
    ```

    You may see some warnings as the package dependencies are installed. You can ignore these.

    > **More Information**: For more details about installing the Azure ML SDK and its optional components, see the [Azure ML SDK Documentation](https://docs.microsoft.com/python/api/overview/azure/ml/install?view=azure-ml-py).

5. Next, run the following commands to change the current directory to the **Users** directory, and retrieve the notebooks you will use in the labs for this course:

    ```bash
    cd Users
    git clone https://github.com/MicrosoftLearning/DP100
    ```

6. After the command has completed, close the terminal tab and view the home page in your Jupyter notebook file explorer. Then open the **Users** folder - it should contain an **DP100** folder, containing the files you will use in the rest of this lab.
7. In the **Users/DP100** folder, open the **01B - Intro to the Azure ML SDK.ipynb** notebook. Then read the notes in the notebook, running each code cell in turn.
8. When you have finished running the code in the notebook, on the **File** menu, click **Close and Halt** to close it and shut down its Python kernel. Then close all Jupyter browser tabs.
9. If you're finished working with Azure Machine Learning for the day, in Azure Machine Learning studio, on the **Compute** page, select your compute instance and click **Stop** to shut it down. Otherwise, leave it running for the next lab.

## Task 2: Set Up a Visual Studio Online Environment

Compute instances in Azure Machine Learning provide an easy to manage Python environment for working with Azure ML without the need to manage your own Python installation. However, sometimes you may want to use your own graphical Python development environment. In this course, we'll use Visual Studio Online to simplify installation, but the principles of using the Azure Machine Learning SDK are the same in any Python environment.

> **Note**: Visual Studio Online is in *preview* at the time of writing. You may experience some unexpected error messages.

1. In a new browser tab, navigate to [https://online.visualstudio.com](https://online.visualstudio.com), and click **Get Started**.
2. Sign into Visual Studio Online using the same Microsoft credentials you used to sign into Azure.
3. Click **Create environment**. If you don't already have a Visual Studio Online plan, create one. This is used to track resource utlization by your Visual Studio Online environments. Then create an environment with the following settings:
    - **Environment Name**: *A unique name of your choice*
    - **Git Repository**: MicrosoftLearning/DP100
    - **Instance Type**: Standard (Linux)
    - **suspend idle environment after**: 60 Minutes
4.  Wait for the environment to be created, and then click **Connect** to connect to it. This will open a browser-based instance of Visual Studio Code.
5. Wait for a minute or so while the environment is set up for you. It might look like nothing is happening, but in the background we are installing some extensions that you will use in the labs. You'll see the following things happen:
    - The files in this repo will appear in the pane on the left.
    - After several minutes, a new file named **REFRESH NOW** will appear in the pane on the left. This is your indication that everything has been installed.
6. After the **REFRESH NOW** file has appeared, refresh the web page to ensure all of the extensions are loaded and you're ready to start.

    Visual Studio Online is a hosted instance of Visual Studio Code that you can use in a web browser. Visual Studio Code is a general code editing environment, with support for various programming languages through the installation of *extensions*. To work with Python, you'll need the Microsoft Python extension, which was installed for you along with some commonly used Python packages when you created this environment from the **DP100** repo.

    The hosted Visual Studio Code environment includes three installations of Python (versions 2.7.13, 3.5.3, and 3.8.0). You will use the Python **3.5.3** virtual environment. In your own installation, you are responsible for installing Python, creating virtual environments, and installing the packages you need. In this lab, most of the general Python configuration has been done for you, but you need to install the Azure Machine Learning SDK.

7. In the Visual Studio Online environment, wait for the contents of the DP100 repo to be loaded, and then in the Application Menu (**&#9776;**), on the **View** menu, click **Command Palette** (or press CTRL+SHIFT+P). Then in the Palette, enter the command **Python: Create Terminal**. This opens a Python terminal pane at the bottom of the Visual Studio Online interface.

    > **Tip**: If the *Python: Create Terminal* command is not listed, refresh the browser to reload the environment and try again.

8. In the terminal pane, enter the following command to change to the directory where the Python 3.5.3 virtual environment is defined:

    ````bash
    cd /usr/bin
    ````

9. Now install the Azure Machine Learning SDK (with the optional *notebooks* extra package) using this command:

    ```bash
    sudo pip install azureml-sdk[notebooks]
    ```

10. Close the Terminal pane.

## Task 3: Use the Azure ML SDK in Visual Studio Online

Now that you have a Python development environment, you can use the Azure Machine Learning SDK in it. First, you need to get the configuration information required to connect to your Azure Machine Learning workspace.

1. In a new browser tab, open the Azure portal at [https://portal.azure.com](https://portal.azure.com), signing in if necessary.
2. Open the Azure Machine Learning workspace resource you created in the previous lab, and on its **Overview** page, click **Download config.json** and download the file to your local computer.
3. Open the downloaded **config.json** file in a text editor, and copy it's contents to the clipboard. This file contains the configuration information necessary to connect to your workspace.
4. In Visual Studio Online, create a new file named **config.json** in the root folder of your VS Online workspace.
5. Paste the copied configuration information into the new config.json file in your Visual Studio Online workspace, and save it.
6. In Visual Studio Online, open the **01B - Intro to the Azure ML SDK.ipynb** notebook - this will be loaded in the Jupyter Notebook interface within Visual Studio Online. It may take a while to load the first time the Jupyter Notebooks interface is used, and you may briefly see two panes - one containing the JSON representation of the notebook, and the other containing the notebook visual interface.
7. When the notebook has loaded, at the bottom left of the Visual Studio Online interface, click the current Python virtual environment. This should have changed to **Python 3.5.3** based on the configuration settings in the repo, but select that virtual environment again anyway (the notebook was authored in a different version, which is indicated in its metadata).
8. Read the notes in the notebook, running each code cell in turn, just as you did in the Azure Machine Learning Notebook VM Jupyter environment.

## Task 4: Use the Visual Studio Code Azure Machine Learning Extension

If you plan to work with Azure Machine Learning in Visual Studio Online (or a local installation of Visual Studio Code), the Azure Machine Learning extension can help make it easier to work with resources in your workspace without needing to switch between your code development environment and the Azure Machine Learning studio web interface.

1. In Visual Studio Online, click the **Extensions** tab (&#8862;), and search for "Azure Machine Learning". Then install the **Azure Machine Learning** extension from Microsoft. After the extension has installed, click the **Reload Required** button to reload the environment with the extension.
2. In Visual Studio Online, click the **Azure** tab (***&Delta;***) and in the **Azure Machine Learning** section, expand your subscription and your Azure Machine Learning workspace.
3. Expand **Compute** and verify that the **aml-cluster** compute resource you created in your workspace is listed along with a **local** compute resource, which in this case represents the Visual Studio Online hosted environment - you can run Azure Machine Learning code experiments on local compute as well as on compute resources defined in the workspace.
4. Close the Visual Studio Online browser tab.
