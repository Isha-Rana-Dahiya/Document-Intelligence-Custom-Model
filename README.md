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

