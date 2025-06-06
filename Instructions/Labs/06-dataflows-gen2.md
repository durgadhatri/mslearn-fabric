# Exercise 9: Create a Dataflow (Gen2) in Microsoft Fabric

### Estimated Duration: 40 minutes

In Microsoft Fabric, Dataflows (Gen2) connect to various data sources and perform transformations in Power Query Online. They can then be used in Data Pipelines to ingest data into a lakehouse or other analytical store or to define a dataset for a Power BI report.

This lab is designed to introduce the different elements of Dataflows (Gen2), and not create a complex solution that may exist in an enterprise.

## Lab objectives

You will be able to complete the following tasks:

- Task 1: Create a Dataflow (Gen2) to ingest data
- Task 2: Add data destination for Dataflow
- Task 3: Add a dataflow to a pipeline

### Task 1: Create a Dataflow (Gen2) to ingest data

In this task, you will create a Dataflow (Gen2) to efficiently ingest and transform data from multiple sources for analysis. This process streamlines data preparation, enabling you to prepare the data for further processing and insights.

1. On **fabric-<inject key="DeploymentID" enableCopy="false"/>** workspace, click on **+ New item**. Select **Dataflow Gen2**. After a few seconds, the Power Query editor for your new dataflow opens.

   ![New dataflow.](./Images/E6T1S1.png)

1. Select **Get data**, select **text/csv** and create a new data source with the following settings:
    - **Link to file**: *Selected*
    - **File path or URL**: `https://raw.githubusercontent.com/MicrosoftLearning/dp-data/main/orders.csv`
    - **Connection**: Create new connection
    - **data gateway**: (none)
    - **Authentication kind**: Anonymous
    - **Privacy level**: None

    ![Get data](./Images/29.png)

1. Select **Next** to preview the file data, and then **Create** the data source. The Power Query editor shows the data source and an initial set of query steps to format the data, as shown below:

   ![Query in the Power Query editor.](./Images/fabric23.png)

1. Select the **Add column** tab on the toolbar ribbon. Then, choose **Custom column** and create a new column named **MonthNo** using the formula `Date.Month([OrderDate])`.

   ![Custom column in Power Query editor.](./Images/fabric24.png)

1. The step to add the custom column is added to the query and the resulting column is displayed in the data pane:

   ![Query with a custom column step.](./Images/lak4.png)

1. Duplicate the existing tab, Go to the **fabric_lakehouse<inject key="DeploymentID" enableCopy="false"/>** , Delete the **orders** files from the table.

### Task 2: Add data destination for Dataflow

In this task, you’ll add a data destination for the Dataflow to determine where the ingested and transformed data will be stored for future use.

1. Choose **Lakehouse** from the **Add data destination** drop-down menu.

   ![Empty data pipeline.](./Images/L9T2S1.png)

   >**Note:** If this option is greyed out, you may already have a data destination set. Check the data destination at the bottom of the Query settings pane on the right side of the Power Query editor. If a destination is already set, you can change it using the gear.

2. In the **Connect to data destination** dialog box, edit the connection by selecting **Create a new connection**. Then, sign in with your Power BI organizational account to establish the identity that the dataflow will use to access the lakehouse.

   ![Data destination configuration page.](./Images/lak1.png)

4. Select **Next**, Select the **fabric-<inject key="DeploymentID" enableCopy="false"/>**. Choose the **lakehouse** then specify a new table named **orders**.

   ![Data destination configuration page.](./Images/fabric26.png)

5. On the Destination settings page, observe that **MonthNo** is not selected in the Column mapping, and an informational message is displayed.
 
6. On the Destination settings page, toggle off the **Use Automatic Settings** option. Then, right-click on the **MonthNo** column header and select **Change Type** to set **MonthNo** as a **Whole number**. Finally, click on **Save Settings**.
   
   ![Data destination settings page.](./Images/lak2.png)

7. Select **Publish** to publish the dataflow. Then wait for the **Dataflow** to be created in the workspace.

8. Once published,click on the **ellipse** next to the published dataflow in the workspace, select **Properties**, and rename the dataflow as **Transform Orders Dataflow**.

### Task 3: Add a dataflow to a pipeline

In this task, you’ll add a dataflow to a pipeline to streamline the data processing workflow and enable automated data transformations.

1. From your workspace, Select **+ New item**. Click on **Data pipeline**, name it as **Load Orders pipeline** and click on **Create**. This will open the pipeline editor.

   > **Note**: If the Copy Data wizard opens automatically, close it!

2. Select **pipeline activity (1)**, and add a **Dataflow (2)** activity to the pipeline.

   ![Empty data pipeline.](./Images/L7T3S2.png)

3. With the new **Dataflow1** activity selected, go to the **Settings (1)** tab. In the **Workspace** drop-down list, choose **fabric-<inject key="DeploymentID" enableCopy="false"/> (2)** and in **Dataflow** drop-down list, select **Transform Orders Dataflow (3)** (the data flow you created previously).

   ![Empty data pipeline.](./Images/L9T3S3.png)
   
4. **Save** the pipeline from the top left corner.

5. Use the **Run** button to run the pipeline, and wait for it to complete. It may take a few minutes.

   ![Pipeline with a dataflow that has completed successfully.](./Images/lak8.png)

6. In the menu bar on the left edge, select **fabric_lakehouse<inject key="DeploymentID" enableCopy="false"/>**

7. Expand the **Tables** section and select the **orders** table created by your dataflow.

   ![Table loaded by a dataflow.](./Images/orders_1.png)

   >**Note:** You might have to refresh the browser to get the expected output.

### Summary

In this exercise, you have created a Dataflow (Gen2) to ingest data , added data destination for Dataflow and a dataflow to a pipeline.

### You have successfully completed the lab
