---
changelog: 'Learn about extending the availability of the remote access feature so
  that you have more time to troubleshoot build issues on Bitrise. '
last_modified_at: '2020-06-02T08:45:00.000+00:00'
title: Remote access
redirect_from: []
tag:
- builds
- troubleshooting
description: Access our build machines remotely when running a failed build again.
  You can use either SSH or a screenshare app to log in to the build's virtual machine.
summary: Remote access allows users to connect to their build's virtual machines via
  SSH or a screenshare app. A failed build can be rebuilt with remote access enabled
  to make troubleshooting a lot easier.
menu:
  builds-main:
    weight: 33

---
{% include video.html embed_url="https://www.youtube.com/embed/PbKDilX1gB4" %}

Remote access allows users to connect to their build's virtual machines via SSH or a screenshare app. A failed build can be rebuilt with remote access enabled to make troubleshooting a lot easier - for example, if the build logs don't provide enough information about the error.

{% include message_box.html type="important" title="Authorization" content="Users who have the **Testers/QA** roles on the app CANNOT use remote access."%}

There are two ways to use remote access on our build machines:

* **SSH**: this is available for both Linux/Docker based and MacOS machines.
* **Screenshare**: this is only available for MacOS machines. It uses the VNC system.

With either method, you can access the build machine remotely during the build and for 10 minutes after the build is finished.

## Remote access with SSH

To access a Bitrise build machine with SSH, you will need a command line interface and the correct command and password:

1. Open the app on Bitrise.
2. Go to the **Builds** tab. 
3. Find the build you want to re-run with remote access.
4. Click the **Rebuild with Remote Access** option.
5. Click **Remote Access Instructions**.

   ![Instructions for remote access with SSH](/img/remote-access-instructions.png)
6. Under the **SSH** option, find and copy the command you will need.
7. Open a command line interface.
8. Run the command found under **SSH** (the below is an example):

       ssh -o StrictHostKeyChecking=no vagrant@1.tcp.ngrok.io -p 000000
9. Copy and paste the password from the **Remote Access Instructions** page.

And done! You should be able to access the virtual machine where your build is running.

## Remote access with screenshare

To access a Bitrise build machine with a screenshare app, you will need the correct username, password, and address, as well as a VNC screenshare app:

1. Open the app on Bitrise.
2. Go to the **Builds** tab. 
3. Find the build you want to re-run with remote access and .
4. Click the **Rebuild with Remote Access** option.
5. Click **Remote Access Instructions**.

   ![Instructions for remote access with screenshare](/img/remote-access-instructions.png)
6. Under the **Screenshare** option, find the required information:
   * Address
   * Username
   * Password
7. Open a VNC screenshare application.

   The simplest option is using the default **Screen Sharing** application on macOS.
8. Fill out the required fields with the information from under the **Screenshare** option.

And done! You should now be able to access the virtual machine where your build is running.

## Finding your files on the VM

Once you successfully logged in to the Bitrise virtual machine that ran your build, you can dive into the files themselves to see what’s happening in real time. After Bitrise finished cloning your app on to the VM, you can always access it at the following location:

    /Users/Vagrant/git

## Extending the availability of remote access

Remote access is available while the build is running and for 10 minutes after the build is finished. If this is not enough, there’s a simple workaround to make sure remote access is available for a longer time.

1. Add a **Script** Step after the Step that causes the build to fail.
2. Toggle the **Run if previous Step failed** option on to ensure the **Script** Step always runs.
3. Add a command to let the build “sleep” for a time specified in seconds:

   `1 sleep 5400`

   This example lets the build run for 90 minutes. It should be no more than your build time limit, of course.

That’s it. While the build is still running, you can look around on the virtual machine for the possible issues that caused it to fail.

{% include banner.html banner_text="Connect to a VM with Remote Access" url="https://app.bitrise.io/users/sign_up?utm_source=devcenter&utm_medium=bottom_cta" button_text="Go to your app" %}