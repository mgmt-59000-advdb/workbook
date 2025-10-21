# Copying BigQuery Data
There are two relational databases that we will use for the first part of this course. They are stored in my instance of BigQuery and you must copy them to your BigQuery project so you can use them.

## 🚨 Permissions Needed! 🚨
You MUST have permission to copy the data! Ensure you complete the **"Google Cloud Platform Setup"** in Brightspace or you WILL NOT be able to proceed with these instructions.

# Copy the Datasets
These instructions are specific to the `class_demos` dataset used in classroom demonstrations. Repeat these instructions for each dataset you will use. Simply substitute the name of the dataset where necessary in the instructions below.

## Instructions

### Step 1: Access BigQuery Console
1. Navigate to the Google Cloud Console: https://console.cloud.google.com
2. From the navigation menu (☰) on the left, select **BigQuery** under the "Analytics" section
3. The BigQuery workspace will open

### Step 2: Add the Instructor's Project to Your Console
1. In the BigQuery Explorer panel (left side), look for the **"+ ADD" button** near the top
2. Click **"Star a project by name"**
3. Enter the project ID: `elliott-purdue-development`
4. Click **"STAR"**
5. The project should now appear in your Explorer panel with a star icon

### Step 3: Locate the Dataset to Copy
1. In the Explorer panel, expand the `elliott-purdue-development` project by clicking the arrow next to it
2. You should see the `class_demos` dataset listed
3. Click on the `class_demos` dataset to view its details

### Step 4: Copy the Dataset
1. With the `class_demos` dataset selected, click on the **"COPY"** button in the dataset info panel (or click the three dots menu next to the dataset name and select **"Copy dataset"**)
2. In the "Copy dataset" dialog box:
   - **Destination project**: Select your own GCP project from the dropdown
   - **Destination dataset ID**: Enter a name for the dataset in your project (you can keep it as `class_demos` or rename it)
   - **Location**: Keep the same location as the source dataset (this should be pre-selected)
   - **Copy options**: Check "Copy tables" to include all tables within the dataset

### Step 5: Configure Copy Settings
1. Review the copy settings:
   - Ensure **"Copy tables"** is checked to copy all tables and their data
   - Leave **"Copy views"** checked if you want to include any views
   - Leave **"Copy routines"** checked if there are stored procedures or functions to copy
2. Click **"COPY"** to start the copy process

### Step 6: Monitor the Copy Process
1. A notification will appear indicating the copy job has started
2. You can monitor the progress by:
   - Clicking on **"Job History"** in the bottom panel
   - Or navigating to the **"Transfers"** section if it's a large dataset
3. The copy process may take a few moments depending on the dataset size

### Step 7: Verify the Copy
1. In the Explorer panel, navigate to your own project
2. Expand your project to see the datasets
3. Verify that the `class_demos` dataset (or whatever name you chose) appears
4. Click on the dataset and expand it to confirm all tables have been copied
5. You can click on individual tables and preview the data to ensure the copy was successful

### Step 8: Update Permissions (Optional)
1. Click on your newly copied dataset
2. In the dataset info panel, click **"SHARING"** → **"Permissions"**
3. Configure any additional access permissions for your team members if needed

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
- Any queries you run on the copied dataset will be billed to your project
- The copy creates a snapshot at the time of copying - it won't sync future updates from the instructor's dataset