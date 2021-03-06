# template-sfdc2localdisk-file-download
A simple example showing how to extract (or download) a file from Salesforce using the MuleSoft Anypoint 4.3 runtime and save it to local disk

# Background

I wanted to build another MuleSoft Anypoint integration that would allow me to analyze files already uploaded to Salesforce, and found it was suprisingly difficult to find an example of how to get a file.
Therefore I created this simple project to show how you can extract a file out of Salesforce and save it to disk. No more.

# Get Started

1) Open the project in AnyPoint Studio 7.7: (probably runs in later versions as well)

<img src="https://github.com/andrewwhitten/template-sfdc2localdisk-file-download/blob/main/images/file_download_flow.png"></img>

2) Set the values of the Global Elements to valid Salesforce login and File Locations (Salesforce login requires read access to that file)

3) Find the ContentVersionID (see Process below)

4) Debug or run, and invoke it from your favorite REST tool:

<img src="https://github.com/andrewwhitten/template-sfdc2localdisk-file-download/blob/main/images/Run.png" width="500"></img>


# Process

This is just a description of the process to do this from begining to end:

Step 1) Your file will have a Salesforce ID that refers to the ContentDocument. You want the row in the ContentVersion Object that refers to this ID as well as IsLatest (or you may select an older version by mistake). An easy way is just look at the URL in Salesforce's file details, but you could SOQL it instead:

<img src="https://github.com/andrewwhitten/template-sfdc2localdisk-file-download/blob/main/images/Step 1a.png"></img>

Step 2) Use your SOQL powers to find the Content Version ID of the file you are looking for:

<img src="https://github.com/andrewwhitten/template-sfdc2localdisk-file-download/blob/main/images/Step 1b.png"></img>

Step 3) Configure a <A HREF="https://docs.mulesoft.com/salesforce-connector/9.8/salesforce-connector-reference#Retrieve">Salesforce Retrieve step</A>, and pass the file's ContentVersionId in to extract the data out of the <A href="https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_objects_contentversion.htm">ContentVersion object</A>.

<img src="https://github.com/andrewwhitten/template-sfdc2localdisk-file-download/blob/main/images/Step2.png" width="550"></img>

Step 4) Extract the file data (as a Base64 string) and convert it to Binary

<img src="https://github.com/andrewwhitten/template-sfdc2localdisk-file-download/blob/main/images/Step3.png" width="550"></img>


# Last thoughts

1) A good developer will use streaming to get files.... but I'm not too interested in that for this exercise. Salesforce has org based limits on file size, but this method can download a 20MB PDF fast enough.

2) Downloading this way doesn't increment the file's download count.

3) This Flow could be shortened a great deal, however this way is easier to examine each step and output the log.

4) You could return the file in the service itself, rather than save to local disk. Go for it.

5) This project doesn't have a lot of good practices that Anypoint should have, such as error handling, input validation, etc. It shouldn't be used for Production. The intention is just to show how to get a file.
