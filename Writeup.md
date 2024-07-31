# Writeup
Lets get started, give a hit on **Start machine** wait for around 5 mins then we will get an IP from where we can access the WAZUH dashboard..

ID pass are provided in the THM room..


Make sure to cross check the screenshot just in order to make sure that we are on the right track.

![image](https://github.com/user-attachments/assets/6b2d2e48-c2b1-4a03-8fd1-748d2d31ee27)


Now click on **Policy Monitoring**

You will surely see a blank screen stating something like this..
![image](https://github.com/user-attachments/assets/9fe716ea-d0f0-4de7-bc48-795225cb7684)


As mentioned in the THM room we have to see the logs when the test was conducted 
![image](https://github.com/user-attachments/assets/5004eb42-eda7-4bc4-bd25-bb995cbe5fa2)

Now in order to set the time click on **Show dates** then you will see something like this..
![image](https://github.com/user-attachments/assets/f9c10ea1-df7b-46d8-90a5-a91fb2364162)

Now modify the date according to the given times..
For this Click on **Absolute** option
![image](https://github.com/user-attachments/assets/0b7a30c3-935e-48c9-b8ba-ced063cbc892)

Make sure to choose the optoin of **Monday monitor** from saved query from here
![image](https://github.com/user-attachments/assets/a54886eb-2b39-486e-a053-8571d341117a)

After completing this the dashboard will look something like this ...
![image](https://github.com/user-attachments/assets/bc744d19-660e-4139-a935-2ccb59a88b52)


For this we can see that **Microsoft office product** rule is triggered, we will directly click on the pie chart and see what we have in it 

Switch to **Events**, So we have around **330 hits** intresting..

Then we will see what command is used or executed for that we will apply the filter 

![image](https://github.com/user-attachments/assets/0f236296-3d4d-412b-8f4f-cf71840f06e7)


After that we will change the time so that it will show the logs from 13:00:00 

Ok so we see an intresting log on around 14:58:09 

![image](https://github.com/user-attachments/assets/e8187ff7-9bb6-49d0-8f03-535036ec9873)

Lol we already found the last **FLAG** anyways lets keep digging and see what else can we found..

But this was the time when the file was executed we have to look before what exactly happened when was the file created or what were the command that were run in order to do so..

# Answers

![image](https://github.com/user-attachments/assets/783a4df0-832e-4ed5-9e6d-99da0139de8f)

**Q. What password was set for the new user account?**

    I_AM_M0NIT0R1NG

**Q. Data was exfiltrated from the host. What was the flag that was part of the data?**
    
    THM{M0N1T0R_1$_1N_3FF3CT}

![image](https://github.com/user-attachments/assets/cefbcd43-c09b-414d-bac7-2a36431d9eee)

Ok so this log consists of mutiple answers at timestamp 14:12:43.386

![image](https://github.com/user-attachments/assets/fd86c57b-b553-49ca-be92-f5a194c050b9)

**Q. What time is the scheduled task meant to run?**

      12:34

**Q. What is the full command run to create a scheduled task?**

    \"cmd.exe\" /c \"reg add HKCU\\SOFTWARE\\ATOMIC-T1053.005 /v test /t REG_SZ /d cGluZyB3d3cueW91YXJldnVsbmVyYWJsZS50aG0= /f &amp; schtasks.exe /Create /F /TN \"ATOMIC-T1053.005\" /TR \"cmd /c start /min \\\"\\\" powershell.exe -Command IEX([System.Text.Encoding]::ASCII.GetString([System.Convert]::FromBase64String((Get-ItemProperty -Path HKCU:\\\\SOFTWARE\\\\ATOMIC-T1053.005).test)))\" /sc daily /st 12:34\"
**Q. What was encoded?**
For this decode this `cGluZyB3d3cueW91YXJldnVsbmVyYWJsZS50aG0=` :) 

Seems like we need to move somewhere around 13:00 clock to see the file name and what was the command used in order to create it...

That can be find in around 13:51 when the process was created

**Q. Initial access was established using a downloaded file. What is the file name saved on the host?**

    SwiftSpend_Financial_Expenses.xlsm




