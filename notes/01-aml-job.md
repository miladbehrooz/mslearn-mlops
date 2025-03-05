# Azure Machine Learning: Setup and Execution Guide

This guide covers how to set up an **Azure Machine Learning** workspace, create a compute instance, register a data asset, and run a machine learning job using **Azure CLI** and **Azure UI**.

---

## **1. Create an Azure Machine Learning Workspace**

### **Using Azure CLI**
```sh
az group create --name my-resource-group --location eastus

az ml workspace create --name my-ml-workspace \
                      --resource-group my-resource-group \
                      --location eastus
```

### **Using Azure UI**
1. Sign in to [Azure Portal](https://portal.azure.com/).
2. Search for **Azure Machine Learning**.
3. Click **+ Create** → **Azure Machine Learning**.
4. Fill in the required details:
   - **Subscription**: Select your Azure subscription.
   - **Resource Group**: Create or select an existing one.
   - **Workspace Name**: Provide a unique name.
   - **Region**: Select a region.
5. Click **Review + Create**, then **Create**.

---

## **2. Create a Compute Instance**

### **Using Azure CLI**
```sh
az ml compute create --name my-compute-instance \
                     --type ComputeInstance \
                     --resource-group my-resource-group \
                     --workspace-name my-ml-workspace \
                     --size Standard_D2s_v3
```

### **Using Azure UI**
1. Open **Azure Machine Learning Studio** ([ml.azure.com](https://ml.azure.com)).
2. Navigate to **Compute** → **Compute Instances**.
3. Click **+ Create**.
4. Enter the required details:
   - **Compute name** (must be unique).
   - **Virtual machine size** (e.g., `Standard_D2s_v3`).
   - **Region**: Same as your AML workspace.
5. Click **Create**.

---

## **3. Register a Data Asset**

### **Using Azure CLI**
```sh
az ml data create --name diabetes-data \
                  --resource-group my-resource-group \
                  --workspace-name my-ml-workspace \
                  --path experimentation-folder/data-folder/ \
                  --type uri_folder \
                  --datastore-name workspaceblobstore
```

### **Using Azure UI**
1. Open **Azure Machine Learning Studio**.
2. Navigate to **Data** → **+ Create**.
3. Set the following:
   - **Name**: `diabetes-data`
   - **Type**: `Folder`
   - **Datastore**: Select `workspaceblobstore` or another relevant datastore.
   - **Path**: Point to the folder containing your dataset.
4. Click **Create**.

---

## **4. Run a Machine Learning Job**

### **Using Azure CLI**
```sh
az ml job create --file job-config.yaml \
                 --resource-group my-resource-group \
                 --workspace-name my-ml-workspace
```


### **Using Azure UI**
1. Open **Azure Machine Learning Studio**.
2. Navigate to **Jobs** → **+ Create**.
3. Configure the job:
   - **Compute**: Select `my-compute-instance`.
   - **Script**: Upload `train.py`.
   - **Data**: Select `diabetes-data`.
4. Click **Submit**.

---

## **Next Steps**
- Monitor your job progress under **Jobs**.
- Check logs for debugging.
- Register and deploy models using `az ml model create`.