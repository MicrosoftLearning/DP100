# Lab 6B: Publishing a Pipeline

After you've created a pipeline, you can publish a REST endpoint through which the pipeline can be initiated. This enables you to run the pipeline on-demand or at scheduled times.

## Before You Start

Before you start this lab, ensure that you have completed [Lab 1A](Lab01A.md) and [Lab 1B](Lab01B.md), which include tasks to create the Azure Machine Learning workspace and other resources used in this lab; and [Lab 6A](Lab06A.md) in which you create the pipeline you will publish in this lab.

## Task 1: Publish a Pipeline

In this task, you'll create a pipeline to train and register a model.

1. In [Azure Machine Learning studio](https://ml.azure.com), view the **Compute** page for your workspace; and on the **Compute Instances** tab, start your compute instance.
2. When the compute instance is running, refresh the Azure Machine Learning studio web page in your browser to ensure your authenticated session has not expired. Then click the **Jupyter** link to open the Jupyter home page in a new browser tab.
3. In the Jupyter home page, in the **Users/DP100** folder, open the **06B - Publishing a Pipeline.ipynb** notebook. Then read the notes in the notebook, running each code cell in turn.
4. When you have finished running the code in the notebook, on the **File** menu, click **Close and Halt** to close it and shut down its Python kernel. Then close all Jupyter browser tabs.
5. If you're finished working with Azure Machine Learning for the day, in Azure Machine Learning studio, on the **Compute** page, on the **Compute Instances** tab, select your compute instance and click **Stop** to shut it down. Otherwise, leave it running for the next lab.
