### icinga
Icinga setup

Step 1: Download the icinga 10.1 x86_64 package based on the architecture of your machine.
<br>https://packages.icinga.com/windows/
<br>https://packages.icinga.com/windows/Icinga2-v2.10.1-x86_64.msi
<br><img src="images/1.png" width="500px">

<br>You can automate these steps in a powershell terminal
<br>cd Downloads
<br>$WebClient = New-Object System.Net.WebClient
<br>$WebClient.DownloadFile("https://packages.icinga.com/windows/Icinga2-v2.10.1-x86_64.msi","Downloads\Icinga2-v2.10.1-x86_64.msi")
<br>Unblock-File -Path Icinga2-v2.10.1-x86_64.msi
<br>msiexec.exe /i Icinga2-v2.10.1-x86_64.msi

Steps 2-10 are optional. Follow these only if you're getting a dot net error during icinga install.

Step 2: If it prompts you for a dot net dependency, install it using the following steps:
Go to windows programs and features:
<br><img src="images/2.png" width="500px">

Step 3: Select "Turn windows features on or off"
<br><img src="images/3.png" width="500px">

Step 4: Click on next, choosing the options as shown:
<br><img src="images/4.png" width="500px">

Step 5: Click on next, choosing the options as shown:
<br><img src="images/5.png" width="500px">

Step 6: Click on next, choosing the options as shown:
<br><img src="images/6.png" width="500px">

Step 7: Select Features -> .NET framework 3.5 features
<br><img src="images/7.png" width="500px">

Step 8: Click on install:
<br><img src="images/8.png" width="500px">

Step 9: Wait for it to install:
<br><img src="images/9.png" width="500px">

Step 10: Once it's done, close the window:
<br><img src="images/10.png" width="500px">

Step 11: Install the agent downloaded in step 1.

Step 12: After that, open the agent setup wizard:
<br><img src="images/29.png" width="500px">

Step 13: Login to the icinga server machine and get the client/satellite token
<br><img src="images/7.png" width="500px"><br>
Input the node name as it is (Even the case should be the same) and execute the above command.

Step 14: Once you obtain the token for the windows machine from above step, paste it in the node setup wizard in step 12 and also select the following options in the bottom right section:
Accept commands from master or satellite instances.
Accept config updates from master or satellite instances.
Install/update bundled NSClient++ (This will be installed later. It is required to check various metrics on the machine you're configuring this)
<br><img src="images/31.png" width="500px">

Step 15: Now click on the "Add button" to add the master info as it is shown below:
<br><img src="images/30.png" width="500px">

Step 16: Once you click on next, you will be presented with the following info:
<br><img src="images/12.png" width="500px">

Step 17: Click on next to complete the icinga node wizard setup.
<br><img src="images/17.png" width="500px">

Step 18: Now the installation for nsclient will start:
<br><img src="images/22.png" width="500px">

Step 20: Select the options as it is:
<br><img src="images/23.png" width="500px">

Step 21: Select the options as it is:
<br><img src="images/24.png" width="500px">

Step 22: Select the options as it is:
<br><img src="images/25.png" width="500px">

Step 23: Select the options as it is:
<br><img src="images/26.png" width="500px">

Step 24: Select the options as it is:
<br><img src="images/27.png" width="500px">

The new node metrics should now be visible on the icinga gui: http://172.16.0.23/icingaweb2/monitoring/list/hosts
<br><img src="images/32.png" width="500px">

When you try to download and install on windows servers, you might get the following errors:
<br><img src="images/28.png" width="500px">
