# Step by step configuration

Visit https://portal.azure.com/#home

On the resources screen look for "Azure AI Search"

configure the feature, making sure to check "Basic" in the "Pricing tier" option

Return to the Azure portal home page.

Click the "＋Create a resource" button and search "Azure AI services" > "Azure AI services multi-service account". Select create an Azure AI services plan. You'll be taken to a page to create an Azure AI Services resource.

Return to the Azure portal home page and select the + Create a resource button. Look for the "storage account" feature. Create this feature too.

The resource name must be unique with only lowercase letters and numbers.

in the Redundancy part, select "LRS (Local-Redundant Storage)"

The storage account service has some security rules by default. For testing reasons it will be necessary to disable or change some of them:

Access the Settings > Configuration tab:
Allow Blob anonymous access = True
Save
Access the Data Storage > Containers tab, create a container. Note that in the "Anonymous access level" option, after enabling the option from the previous step, an option "Container (anonymous read access for containers and blobs)" will be available.

Select this option

for the name define "coffeereviews";

After creating the container, it is necessary to load the reviews that we will use to feed the model. To do this, simply access the documentation available in the last section of this manual; Another option is to download the .zip reviews available in this directory.

Once done, select the created container and, in the top menu, select "upload" and then send the reviews to the model, feeding it.

### Until that moment we have to have 3 resources:

an Azure AI Service Resource,
a Search Service resource
a Storage Account resource
Example Template
Access the Search feature (Search Service)

Click on "Import Data"

You will need to establish a connection with the "storage account" resource.

On the Connect to your data page, in the Data Source list, select "Azure Blob Storage". Fill in the data storage details with the following values:

Data source: Azure Blob Storage
Data source name: coffee-customer-data
Data to extract: Content and metadata
Analysis Mode: Standard
Connection string: *Select Choose an existing connection. Select your storage account, select the coffee reviews container, and click Select.
Managed Identity Authentication: None
Container name: This setting is automatically populated after you choose an existing connection.
Blob folder: leave blank.
Description: Reviews about Fourth Coffee Shops.
Select "Next: Add cognitive skills (Optional)".

In the Attach Cognitive Services section, select your Azure AI services resource.

### In the Add Enrichments section:
Change the Skillset name to "coffee-skillset".
Check the "Enable OCR and merge all text in merged_content field" checkbox
Make sure the "Source Data Field" field is set to "merged_content".
Change the enrichment granularity level to "Pages (5000 character blocks)".
Do not select "Enable incremental enrichment"

### Under Save enrichments to a knowledge store, select:
Image projections
Documents
Pages
Key phrases
Entities
Image Details
Image references
# If a warning appears asking for a storage account connection string:

Select Choose an existing connection.

Choose the storage account you created earlier.

Click + Container to create a new container called knowledge store with the privacy level set to Private and select Create.

Select the knowledge store container and click Select at the bottom of the screen.

Select projections from "Azure blob projections: Document". A setting for the name of the container with the auto-populated views of the knowledge store container. Do not change the container name.

Select "Next: Customize target index". Change the index name to "coffee-index".

Make sure the "key" is set to "metadata_storage_path". Leave the "Suggester name" blank and the "Search mode" filled in automatically.

Review the default settings for the index fields. Select "filterable" for all fields that are already selected by default.

Select "Next: Create an indexer".

Change the "Indexer name" to "coffee-indexer".

Leave the schedule set to "once".

Expand the advanced options. Make sure "Base-64 Encode Keys" is selected, as encoding keys can make the index more efficient.

Select "Submit" to create the data source, skill set, index, and indexer. The indexer runs automatically and runs the indexing pipeline, which:

Extracts document metadata fields and content from the data source.
Executes the set of cognitive skills to generate more enriched fields.
Maps the extracted fields to the index.
Return to the "Azure AI Search" resources page.

In the left pane, under Search Management, select "Indexers".

Select the newly created coffee indexer. Wait a minute and select "Refresh" until the Status indicates success.

Select the indexer name to see more details.

Once this is done, access the "Search Explorer" tab within the IA Search resource. (It's as if we had a directory on the server and an application that consults this directory using the search feature).

The search engine is inside Azure, but in a real scenario it would be inside an application.

change the view to "Json view"

notice that our created index appears as a reference in the "index" field;

Enter the content below into the editor, which will return all documents in the search index, including all documents in the "@odata.count" field:

{
   "search": "*",
   "count": true
}
It is possible to change the filter by city (it must be 3 in @odata.count):

{
  "search": "locations:'Chicago'",
  "count": true
}
# Tests carried out and problem situation 🧭
The problem situation used for this test involved a cafeteria service that needed to gather information about sales, consumption and the brand's vision in relation to customers.
The situation shows us different evaluations in relation to the services provided by the Café, making it possible to extract data based on key-value, through words in a semantic context or through the feeling expressed by a sentence as a whole.
