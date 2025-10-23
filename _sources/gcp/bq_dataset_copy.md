# Copying BigQuery Data
There are two relational databases that we will use for the first part of this course. They are stored in my instance of BigQuery and you must copy them to your BigQuery project so you can use them.

## 🚨 Permissions Needed! 🚨
You MUST have permission to copy the data! Ensure you complete the **"Google Cloud Platform Setup"** in Brightspace or you WILL NOT be able to proceed with these instructions.

# Copy the Datasets
These instructions are specific to the `class_demos` dataset used in classroom demonstrations. Repeat these instructions for each dataset you will use. Simply substitute the name of the dataset where necessary in the instructions below.

## Instructions

### Step 1: Access BigQuery Console
1. Navigate to the BigQuery in the Google Cloud Console: https://console.cloud.google.com/bigquery

### Step 2: Go to Data Transfers
In the left navigation pane:
   1. Click "Data Transfers" (under the "Pipelines & Integrations" section)

   ```{image} _images/1-datatransfers.png
   :alt: Screenshot of BigQuery navigation
   :width: 200px
   ```

   2. Then click **Create a Transfer**

   ```{image} _images/2-datatransferservice.png
   :alt: Screenshot of Data Transfers screen
   :width: 400px
   ```

```{note}
If you are asked to enable the Bigquery Data Transfer API, you should do so
```

### Step 3: Configure the Transfer
In the Create transfer dialog, do the following:
   1. In the Source dropdown, choose "Dataset Copy"

   ```{image} _images/3-datasetcopy.png
   :alt: Choose Dataset Copy from the Source dropdown
   :width: 400px
   ```

   2. Enter a value for "Transfer config name"
   3. In the Schedule options dropdown, choose "On-demand"
   4. In Destination settings, click "Dataset" and then "CREATE NEW DATASET"

   ```{image} _images/4-createtransfer.png
   :alt: Create transfer settings as specified in text
   :width: 400px
   ```

### Step 4: Create a Dataset
In the Create dataset dialog, do the following:
   1. Enter a Dataset ID
      a. Use `class_demos` for the dataset in this example. *(You will update this for later data transfers.)*
   2. For Location type, choose "Region"
   3. In the Region * dropdown, choose `us-central1 (Iowa)`
   4. Click "Create dataset"

   ```{image} _images/5-createdataset.png
   :alt: Create dataset settings as specified in text
   :width: 400px
   ```

### Step 5: Select your Dataset
Back in the Create transfer dialog, do the following:
   1. Choose `class_demos` from the Destination settings dropdown

   ```{image} _images/6-destinationsettings1.png
   :alt: Select `class_demos` from Destination settings dropdown
   :width: 400px
   ```

   2. For Source dataset enter `class_demos`
   3. for Source project enter `elliott-purdue-development`
   4. Click Save

   ```{image} _images/7-destinationsettings2.png
   :alt: Destination settings as specified in text
   :width: 400px
   ```

### Step 4: Run the Transfer
On the Transfer details page, do the following:
   1. Click the "Run transfer now" button at the top of the screen
   2. In the "Run transfer now" dialog, choose "Run one time transfer"
   3. Click OK

   ```{image} _images/8-transferdetails.png
   :alt: Run transfer now button
   :width: 400px
   ```

```{info}
The transfer is added to the queue but may take a moment or two. Go grab a drink before proceeding.
```

### Step 5: Verify the Copy
1. In the Explorer panel, navigate to your own project
2. Expand your project to see the datasets
3. Verify that the `class_demos` dataset (or whatever name you chose) appears
4. Click on the dataset and expand it to confirm all tables have been copied
5. You can click on individual tables and preview the data to ensure the copy was successful

## Troubleshooting Tips

**If you cannot see the instructor's project:**
- Verify you have been granted BigQuery Data Viewer access
- Check that you're using the correct project ID: `elliott-purdue-development`
- Try refreshing the BigQuery console

**If the copy fails:**
- Check that you have sufficient permissions in your destination project
- Ensure your project has BigQuery API enabled
- Verify you have enough storage quota in your project
- Check that the destination dataset name doesn't already exist

**If tables appear empty after copying:**
- The copy job might still be in progress - check Job History
- Refresh the BigQuery console
- Check the "Details" tab of each table for row count

## Important Notes
- The copied dataset will belong to your project and will incur storage costs based on your project's billing
- Any queries you run on the copied dataset will be billed to your project *(Remember! You are using GCP credits and the billing will be free to you! Also, the costs for this project will be minimal.)*
- The copy creates a snapshot at the time of copying - it won't sync future updates from the instructor's dataset