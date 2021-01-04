# template-sfdc2localdisk-file-download
A simple example showing how to extract a file from Salesforce using MuleSoft Anypoint

# Background

I wanted to build another MuleSoft Anypoint integration that would allow me to analyze files already uploaded to Salesforce. 
It was suprisingly difficult to find an example of the process, hence this project to show how you can extract a file out of Salesforce and save it to disk.

<img src="https://github.com/andrewwhitten/template-sfdc2localdisk-file-download/blob/main/images/file_download_flow.png"></img>

# Process

Step 1) Use your SOQL powers to find the Content Version ID of the file you are looking for. Your file will have a Salesforce ID that refers to the ContentDocument. You want the row in the ContentVersion Object that refers to this ID as well as IsLatest.

Step 2) Configure a <A HREF="https://docs.mulesoft.com/salesforce-connector/9.8/salesforce-connector-reference#Retrieve">Salesforce Retrieve step</A>, and pass the file's ContentVersionId in to extract the data out of the <A href="https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_objects_contentversion.htm">ContentVersion object</A>.

<img src="https://github.com/andrewwhitten/template-sfdc2localdisk-file-download/blob/main/images/Step2.png" width="350"></img>

Step 3) Extract the file data (as a Base64 string) and convert it to Binary

<img src="https://github.com/andrewwhitten/template-sfdc2localdisk-file-download/blob/main/images/Step3.png" width="350"></img>


# Findings

A good developer will use streaming to get files.... but I'm not too interested in that for this exercise. Salesforce has org based limits on file size, but this method can download a 60MB PDF fast enough.
