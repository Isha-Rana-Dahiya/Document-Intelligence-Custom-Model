# Document-Intelligence-Custom-Model
 Provision Your Document Intelligence Resource
- In the Azure Portal, click Create a resource → AI + Machine Learning → Document Intelligence.
- Fill in Subscription, Resource Group, Region and Pricing tier.
- Once provisioned, grab the Endpoint and Key from the Keys and Endpoint blade—you’ll need these later for testing or integration.

2. Launch Document Intelligence Studio
- Navigate to https://aka.ms/document-intelligence/studio and sign in with your Azure account.
- From the resource picker, select the Document Intelligence instance you just created.

3. Create a New Custom Model Project
- Click New project.
- Give it a name (e.g., “InvoiceReader”).
- Choose Custom model as the project type.
- Configure your training data:
- Point to an Azure Blob container or local files (drag-and-drop).
- Separate “Training” vs. “Testing” doc sets for later evaluation.

4. Label Your Documents
- In the project dashboard, select Label data.
- For each document page:
- Draw boxes around fields (e.g., Invoice Number, Date, Total).
- Assign a field name/label to each selection.
- Save your progress as you go. Studio version-controls your label set automatically.

5. Train the Model
- Back in your project’s Train tab, click Train model.
- Studio shows a progress bar—training typically takes a few minutes.
- Once complete, you’ll see:
- Model ID
- Training accuracy (precision, recall, F1) per field
- A snapshot of labelled vs. predicted values

6. Evaluate and Test
- Switch to the Test tab in Studio.
- Upload or select “Testing” documents you held back.
- Click Analyze to see:
- Field-by-field performance metrics
- A side-by-side view of ground-truth vs. model output
- If accuracy is low on certain fields, return to Label data, adjust labels, and retrain.

7. Deploy and Consume (No-Code)
- In the Studio project’s Consume pane, note the REST endpoint and key.
- You can:
- Paste these into Postman or Insomnia to call your model with new PDFs/images.
- Use the Azure Logic Apps or Power Automate connector for Form Recognizer—configure the connector with your key/endpoint, then add a “Extract fields” action.
- Hook directly into low-code tools like Power Apps to build a simple UI that uploads docs and displays extracted fields.

8. Best Practices & Tips
- Organize your blob storage into separate containers for train/test datasets.
- Use consistent naming conventions for field labels to avoid confusion when merging labels.
- Leverage the Model versions tab in Studio to roll back to a previous iteration if needed.
- Periodically refresh training with new edge-case documents to keep accuracy high.


1. Provision a Document Intelligence Resource
- In the Azure Portal, click Create a resource.
- Search for Document Intelligence and select Document Intelligence (form recognizer).
- Click Create, then fill in:
- Subscription and Resource group
- Name (e.g., my-doc-intel-svc)
- Region
- Pricing tier
- Review and Create. Wait until deployment completes.

2. Prepare Your Storage Account
You need a place to store your training and test documents.
- In Azure Portal, go to Storage accounts and click + Create.
- Choose the same Resource Group, give it a name (e.g., docinteldatalake), and complete creation.
- Once created, open the storage account and under Data storage, select Containers.
- Create two containers:
- train-files
- test-files
- For each container, click Upload and add your PDF/JPG documents.

- 3. Set Up Access to Your Data in Studio
- Navigate to Document Intelligence Studio: https://aka.ms/document-intelligence/studio
- Sign in with your Azure credentials.
- In the left pane, click + New project.
- Enter:
- Project name (e.g., InvoiceReader)
- Resource: select the Document Intelligence resource you provisioned.
- Storage container: paste your container’s SAS URL (found under your storage account ➔ Containers ➔ Access keys ➔ Generate SAS).
- Click Create.

4. Label Your Training Documents
- In your project dashboard, click the Label data tab.
- Click Add documents and choose the files from train-files.
- For each document page:
- Click the Rectangle tool.
- Draw a box around the field (e.g., Invoice Number).
- In the sidebar, enter the Field name exactly (e.g., InvoiceNumber).
- Repeat for all required fields (Date, Total, VendorName, etc.).
- Click Save. Studio auto-saves and version-controls each label set.

5. Train Your Custom Model
- Switch to the Train tab.
- Under Model type, confirm Custom model is selected.
- Click Train model.
- Watch the progress indicator—training usually takes 2–5 minutes.
- When complete, review:
- Model ID
- Precision / recall / F1 for each field

6. Evaluate and Refine
- Go to the Test tab.
- Click Add documents and upload from test-files.
- Select all test docs and click Analyze.
- Examine:
- Field-level metrics (how well the model generalizes)
- Side-by-side ground truth vs. predictions
- If any field is underperforming:
- Return to Label data, add or correct labels.
- Retrain.

7. Consume Your Model (No-Code)
Studio gives you everything to integrate without writing code:
- Under Consume in your project:
- Copy the REST endpoint URL.
- Copy the API key.
- Use in low-code tools:
- Power Automate connector for Form Recognizer
- Logic Apps action “Extract fields from document”
- Power Apps custom form to upload and display results
- Or test directly:
- Open Postman, create a POST to <endpoint>/formrecognizer/documentModels/<modelId>:analyze?api-version=2022-08-31-preview
- In Headers, set Ocp-Apim-Subscription-Key to your key
- In Body, select binary and upload a PDF

8. Best Practices & Next Steps
- Organize more containers (e.g., edge-cases, archived) for continuous retraining.
- Use Model versions in Studio to manage rollbacks.
- Automate retraining with Azure Data Factory low-code pipelines.
- Visualize extraction performance in Power BI by exporting analytics from Studio logs.



