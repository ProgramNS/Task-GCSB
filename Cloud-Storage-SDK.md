# How to start your lab and sign in to the Google Cloud Console

 Click the Start Lab button. If you need to pay for the lab, a pop-up opens for you to select your payment method. On the left is the Lab Details panel with the following: 

    The Open Google Console button
    Time remaining
    The temporary credentials that you must use for this lab
    Other information, if needed, to step through this lab
    Click Open Google Console. The lab spins up resources, and then opens another tab that shows the Sign in page.

Tip: Arrange the tabs in separate windows, side-by-side.

Note: If you see the Choose an account dialog, click Use Another Account.
If necessary, copy the Username from the Lab Details panel and paste it into the Sign in dialog. Click Next.

Copy the Password from the Lab Details panel and paste it into the Welcome dialog. Click Next.

Important: You must use the credentials from the left panel. Do not use your Google Cloud Skills Boost credentials.
Note: Using your own Google Cloud account for this lab may incur extra charges.
Click through the subsequent pages:

Accept the terms and conditions.
Do not add recovery options or two-factor authentication (because this is a temporary account).
Do not sign up for free trials.
After a few moments, the Cloud Console opens in this tab.

Note: You can view the menu with a list of Google Cloud Products and Services by clicking the Navigation menu at the top-left. Navigation menu icon
Activate Cloud Shell
Cloud Shell is a virtual machine that is loaded with development tools. It offers a persistent 5GB home directory and runs on the Google Cloud. Cloud Shell provides command-line access to your Google Cloud resources.

Click Activate Cloud Shell Activate Cloud Shell icon at the top of the Google Cloud console.
When you are connected, you are already authenticated, and the project is set to your PROJECT_ID. The output contains a line that declares the PROJECT_ID for this session:

Your Cloud Platform project in this session is set to YOUR_PROJECT_ID
gcloud is the command-line tool for Google Cloud. It comes pre-installed on Cloud Shell and supports tab-completion.

(Optional) You can list the active account name with this command:

``` gcloud auth list ```
**Click Authorize.**

Your output should now look like this:
Output:
    ACTIVE: *
    ACCOUNT: student-01-xxxxxxxxxxxx@qwiklabs.net
    To set the active account, run:
        $ gcloud config set account ACCOUNT

(Optional) You can list the project ID with this command:
gcloud config list project
Output:

[core]
project = <project_ID>
Example output:

[core]
project = qwiklabs-gcp-44776a13dea667a6
Note: For full documentation of gcloud, in Google Cloud, refer to the gcloud CLI overview guide.
Create a bucket
In the Cloud Console, go to Navigation menu > Cloud Storage > Buckets. Click CREATE BUCKET.

Name your bucket: Enter a unique name for your bucket.

Bucket naming rules:
Do not include sensitive information in the bucket name, because the bucket namespace is global and publicly visible.
Bucket names must contain only lowercase letters, numbers, dashes (-), underscores (_), and dots (.). Names containing dots require verification.
Bucket names must start and end with a number or letter.
Bucket names must contain 3 to 63 characters. Names containing dots can contain up to 222 characters, but each dot-separated component can be no longer than 63 characters.
Bucket names cannot be represented as an IP address in dotted-decimal notation (for example, 192.168.5.4).
Bucket names cannot begin with the "goog" prefix.
Bucket names cannot contain "google" or close misspellings of "google".
Also, for DNS compliance and future compatibility, you should not use underscores (_) or have a period adjacent to another period or dash. For example, ".." or "-." or ".-" are not valid in DNS names.
**Click CONTINUE.**

Set Location type to Multi-region.
Set Location to us (multiple regions in United States)
Click CONTINUE.
Set Default Storage class to Standard.
**Click CONTINUE.**
If needed, uncheck Enforce public access prevention on this bucket under Prevent public access.
Select Fine-grained under Access Control.
Click CONTINUE.
Scroll to the bottom and click CREATE.
That's it — you've just created a Cloud Storage bucket!
Note: If the bucket name is already taken, either by you or someone else, the command returns:
Creating gs://YOUR-BUCKET-NAME/...
ServiceException: 409 Bucket YOUR-BUCKET-NAME already exists.

Try again with a different bucket name.
Test completed task
Click Check my progress to verify your performed task. If you've successfully created a Cloud Storage bucket, you'll see an assessment score.

Create a Cloud Storage bucket.


Task 1. Upload an object into your bucket
Use Cloud Shell to upload an object into a bucket.

To download this image (ada.jpg) into your bucket, enter this command into Cloud Shell:

curl https://upload.wikimedia.org/wikipedia/commons/thumb/a/a4/Ada_Lovelace_portrait.jpg/800px-Ada_Lovelace_portrait.jpg --output ada.jpg
Copied!
Use the gsutil cp command to upload the image from the location where you saved it to the bucket you created:

gsutil cp ada.jpg gs://YOUR-BUCKET-NAME
Copied!
Note: When typing your bucket name, you can use the tab key to autocomplete it.
You can see the image load into your bucket from the command line. You've just stored an object in your bucket!

Now remove the downloaded image:

rm ada.jpg
Copied!
Task 2. Download an object from your bucket
Use the gsutil cp command to download the image you stored in your bucket to Cloud Shell:

gsutil cp -r gs://YOUR-BUCKET-NAME/ada.jpg .
Copied!
If successful, the command returns:

Copying gs://YOUR-BUCKET-NAME/ada.jpg...
/ [1 files][299.6 KiB/299.6 KiB]
Operation completed over 1 objects/299.6 KiB.
You've just downloaded the image from your bucket.

Task 3. Copy an object to a folder in the bucket
Use the gsutil cp command to create a folder called image-folder and copy the image (ada.jpg) into it:

gsutil cp gs://YOUR-BUCKET-NAME/ada.jpg gs://YOUR-BUCKET-NAME/image-folder/
Copied!
Note: Compared to local file systems, folders in Cloud Storage have limitations, but many of the same operations are supported.
If successful, the command returns:

Copying gs://YOUR-BUCKET-NAME/ada.jpg [Content-Type=image/png]...
- [1 files] [ 299.6 KiB/ 299.6 KiB]
Operation completed over 1 objects/299.6 KiB
The image file has been copied into a new folder in your bucket.

Test completed task
Click Check my progress to verify your performed task. If you have successfully uploaded an object into a folder in your Cloud Storage bucket, you'll see an assessment score.

Copy an object to a folder in the bucket (ada.jpg).
Task 4. List contents of a bucket or folder
Use the gsutil ls command to list the contents of the bucket:

gsutil ls gs://YOUR-BUCKET-NAME
Copied!
If successful, the command returns a message similar to:

gs://YOUR-BUCKET-NAME/ada.jpg
gs://YOUR-BUCKET-NAME/image-folder/
That's everything currently in your bucket.

Task 5. List details for an object
Use the gsutil ls command, with the -l flag to get some details about the image file you uploaded to your bucket:

gsutil ls -l gs://YOUR-BUCKET-NAME/ada.jpg
Copied!
If successful, the command returns a message similar to:

306768  2017-12-26T16:07:570Z  gs://YOUR-BUCKET-NAME/ada.jpg
TOTAL: 1 objects, 30678 bytes (299.58 KiB)
Now you know the image's size and date of creation.

Task 6. Make your object publicly accessible
Use the gsutil acl ch command to grant all users read permission for the object stored in your bucket:

gsutil acl ch -u AllUsers:R gs://YOUR-BUCKET-NAME/ada.jpg
Copied!
If successful, the command returns:

Updated ACL on gs://YOUR-BUCKET-NAME/ada.jpg
Your image is now public, and can be made available to anyone.

Test completed ask
Click Check my progress to verify your performed task. If you have successfully shared an object from your storage bucket, you will see an assessment score.

Make your object publicly accessible
Validate that your image is publicly available.

Go to Navigation menu > Cloud Storage, then click on the name of your bucket.
You should see your image with the Public link box. Click the Copy URL and open the URL in a new browser tab.

Note: Who are you looking at? This is Ada Lovelace, credited with being the first computer programmer. She worked with mathematician and computer pioneer Charles Babbage, who proposed the Analytical Engine.

Her interest in the Analytical Engine lead to translating a paper on the machine by Italian mathematician Luigi Menabrea, adding her own extensive annotations. These notes are considered the first computer program - an algorithm designed to be carried out by the machine. She developed a vision of the capability of computers, going beyond number crunching, and examined how individuals and society relate to technology as a collaborative tool.

Citation: Ada Lovelace. (2015, October 22). Wikimedia Commons, the free media repository. Retrieved 08:01, May 31, 2022 from https://commons.wikimedia.org/w/index.php?title=Ada_Lovelace&oldid=176490980, .
Test your understanding
Below is a multiple choice question to reinforce your understanding of this lab's concepts. Answer it to the best of your ability.


An access control list (ACL) is a mechanism you can use to define who has access to your buckets and objects.

True

False

Task 7. Remove public access
To remove this permission, use the command:

gsutil acl ch -d AllUsers gs://YOUR-BUCKET-NAME/ada.jpg
Copied!
If successful, the command returns:

Updated ACL on gs://YOUR-BUCKET-NAME/ada.jpg
You have removed public access to this object.

Verify that you've removed public access by clicking the Refresh button in the Console. The checkmark will be removed.

Test your understanding
Below is a multiple choice question to reinforce your understanding of this lab's concepts. Answer it to the best of your ability.


You can stop publicly sharing an object by removing the permission entry that has:

By updating storage class

By removing project owner role

allUsers

Delete objects
Use the gsutil rm command to delete an object - the image file in your bucket:

gsutil rm gs://YOUR-BUCKET-NAME/ada.jpg
Copied!
If successful, the command returns:

Removing gs://YOUR-BUCKET-NAME/ada.jpg...
Refresh the Console. The copy of the image file is no longer stored on Cloud Storage (though the copy you made in the image-folder/ folder still exists).

Congratulations!
You created a storage bucket, organized it by creating folders and subfolders, then uploaded objects to it. You also made objects in your bucket publicly accessible using Cloud Shell.

Finish your quest
This self-paced lab is part of the Baseline: Infrastructure quest. A quest is a series of related labs that form a learning path. Completing this quest earns you a badge to recognize your achievement. You can make your badge or badges public and link to them in your online resume or social media account. Enroll in this quest or any quest that contains this lab and get immediate completion credit. See the Google Cloud Skills Boost catalog to see all available quests

Next steps / Learn more
This lab is also part of a series of labs called Qwik Starts. These labs are designed to give you a little taste of the many features available with Google Cloud. Search for "Qwik Starts" in the lab catalog to find the next lab you'd like to take!

Google Cloud training and certification
...helps you make the most of Google Cloud technologies. Our classes include technical skills and best practices to help you get up to speed quickly and continue your learning journey. We offer fundamental to advanced level training, with on-demand, live, and virtual options to suit your busy schedule. Certifications help you validate and prove your skill and expertise in Google Cloud technologies.

Manual Last Updated August 24, 2022

Lab Last Tested August 24, 2022

Copyright 2023 Google LLC All rights reserved. Google and the Google logo are trademarks of Google LLC. All other company and product names may be trademarks of the respective companies with which they are associated.