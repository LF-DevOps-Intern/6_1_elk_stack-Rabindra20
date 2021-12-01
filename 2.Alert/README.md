  2. Generate alerts through kibana system for following thresholds
    a. when memory usage > 80% for last 2 minutes send alert to a slack channel
    b. When Disk usage > 70%   send alert to a slack channel
    c. When load average > 1  for last 2 minutes  send alert to a slack channel
Steps:<br/>
click on stack mangement > click on 30 day trial<br/>

![licence](https://user-images.githubusercontent.com/53372486/144167159-9ae5b5f6-cb70-434c-b430-a203003c2db1.png)<br/>

then click on Security > click on rules >create rules  > add pattern And click on continue<br/>    

![pattern](https://user-images.githubusercontent.com/53372486/144167171-fc2294a4-1ab0-41f8-8fbb-a4b023441852.png)<br/>

For Disk<br/>
custom query=system.fsstat.total_size.used > 70<br/>

![disk](https://user-images.githubusercontent.com/53372486/144171099-0070c277-b3eb-48b4-a15a-3cdea6acf9a7.png)<br/>

For memory<br/>
Custom query=system.memory.actual.used.pct > 0.8<br/>

![memory](https://user-images.githubusercontent.com/53372486/144171073-b111cc57-bd35-47d7-96fc-4f9428473036.png)<br/>

For load<br/>
Custom query=system.load.1 > 1 <br/>

![load](https://user-images.githubusercontent.com/53372486/144171072-c9e5e394-9417-4641-93c6-fed5c956d323.png)<br/>

Add about rules and click continue<br/>

![about rule](https://user-images.githubusercontent.com/53372486/144171089-b898c7d9-d6da-4cc4-b018-c3924726de01.png)<br/>

Add schedule rule and click on continue<br/>

![shu](https://user-images.githubusercontent.com/53372486/144171081-16d40ae4-dfaf-4cd5-98ed-bc285a5f6697.png)<br/>

add Rule action and click on connector<br/>

![create rule](https://user-images.githubusercontent.com/53372486/144171098-9c9866a6-590f-4b85-a26a-87218145c626.png)<br/>

use slack as a connector  and create channel in slack and use webhook https://devopsinterns-j3q5170.slack.com/services/2786279865172?updated=1 then link channel with connector  <br/>

![webhooks](https://user-images.githubusercontent.com/53372486/144171087-6d0f4be9-fc8f-4ba2-b668-25f4468d8bba.png)<br/>
![webhooks](https://user-images.githubusercontent.com/53372486/144172824-dc4f7490-5806-400e-bf15-7815375fc3f3.png)<br/>

use below command for increase all usage<br/>
```
echo {1..100000000}
```
Check all rule<br/>

![Allrules](https://user-images.githubusercontent.com/53372486/144171094-8a95108b-845e-4708-88c2-070a28812b75.png)<br/>

Check Alert<br/>

![Alert](https://user-images.githubusercontent.com/53372486/144171092-e7e4c5be-0177-450a-b4b4-921e4dcca859.png)<br/>

Check message in slack group<br/>

![slack](https://user-images.githubusercontent.com/53372486/144171082-5a79a688-e989-4961-a0f3-eb95974d1b21.png)<br/>
![slack2](https://user-images.githubusercontent.com/53372486/144171084-4169f219-3dad-4280-bfd5-6aef1484f82c.png)<br/>

 
 
 
 











