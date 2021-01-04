# template-sfdc2localdisk-file-download
A simple example showing how to extract a file from Salesforce using MuleSoft Anypoint

# Background

I wanted to build another MuleSoft Anypoint integration that would allow me to analyze files uploaded to Salesforce. 
It was suprisingly difficult to find an example of the process, hence this project to show how you can extract a file out of Salesforce and save it to disk.

# Process

1) Configure a Salesforce Retrieve step, and pass the file's ContentVersionId in to extract the data out of the <A href="https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_objects_contentversion.htm">ContentVersion object</A>.
