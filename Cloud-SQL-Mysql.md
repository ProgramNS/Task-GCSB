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

    gcloud auth list
    Copied!
    Click Authorize.

    Your output should now look like this:

    Output:

    ACTIVE: *
    ACCOUNT: student-01-xxxxxxxxxxxx@qwiklabs.net
    To set the active account, run:
        $ gcloud config set account `ACCOUNT`
    (Optional) You can list the project ID with this command:

    gcloud config list project
    Copied!
    Output:

    [core]
    project = <project_ID>
    Example output:

    [core]
    project = qwiklabs-gcp-44776a13dea667a6
    Note: For full documentation of gcloud, in Google Cloud, refer to the gcloud CLI overview guide.

# Task 1. Create a Cloud SQL instance
    From the Navigation menu (Navigation menu icon) click on SQL.

    Click Create Instance.

    Create your instance with the following settings:

    Click choose MySQL
    Type "myinstance" for Instance ID
    In the password field click on the Generate link and the eye icon to see the password. Save the password to use in the next section.
    Leave all other fields at the default values.
    Click Create Instance.

    After a few minutes the instance is created and you can continue to the next section. If it seems to be taking a long time, refresh your browser.

    Test Completed Task

    Click Check my progress to verify your performed task. If you have successfully created a Cloud SQL instance, you will see an assessment score.
    Create a Cloud SQL instance

# Task 2. Connect to your instance using the mysql client in Cloud Shell
    In the Cloud Console, click the Cloud Shell icon in the upper right corner.
    Cloud Shell icon

    Click Continue.

    At the Cloud Shell prompt, connect to your Cloud SQL instance by running the following:

    gcloud sql connect myinstance --user=root
    Copied!
    Click Authorize.

    Enter your root password when prompted. Note: The cursor will not move.

    Press the Enter key when you're done typing.

    You should now see the mysql prompt.

# Task 3. Create a database and upload data
    Create a SQL database called guestbook on your Cloud SQL instance:

    CREATE DATABASE guestbook;
    Copied!
    Test completed task

    Click Check my progress to verify your performed task. If you have successfully created a custom database on the Cloud SQL instance, you will see an assessment score.

    Create a database.
    Insert the following sample data into the guestbook database:

    USE guestbook;
    CREATE TABLE entries (guestName VARCHAR(255), content VARCHAR(255),
        entryID INT NOT NULL AUTO_INCREMENT, PRIMARY KEY(entryID));
        INSERT INTO entries (guestName, content) values ("first guest", "I got here!");
    INSERT INTO entries (guestName, content) values ("second guest", "Me too!");
    Copied!
    Now retrieve the data:

    SELECT * FROM entries;
    Copied!
    You should see:

    +--------------+-------------------+---------+
    | guestName    | content           | entryID |
    +--------------+-------------------+---------+
    | first guest  | I got here!       |       1 |
    | second guest | Me too!           |       2 |
    +--------------+-------------------+---------+
    2 rows in set (0.00 sec)
    mysql>