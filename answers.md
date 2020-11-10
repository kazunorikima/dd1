                         
-------------------------
                         
Technical exercise Report
                         










#
# Setup the environment

I setup the environment, using Vagrant Ubuntu VM.
Then I installed MySQL and several pythonmysql related component to develop Flask application.

On the other side, as a self-learning I used following platform too.
   CentOS with Tomcat
   Minikube
   Windows10 with SQL Server
   AWS

![](mediaimage1.png)![](mediaimage2.png)



# Collecting Metrics
## Host Map
I added three tags in datadog.yaml file.
![](mediaimage3.png)

![](mediaimage4.png)

## Database

I installed a MySQL.

![](mediaimage5.png)



## my_metric Custom Agent

I created a custom agent.
It sends my_metric metric with configurable collection internal.


```
init_config
  min_collection_interval 45
instances
  - check True
```
Configuration file etcdatadog-agentconf.dmy_metric.yaml







```
from checks import AgentCheck
import random

__version__ = 1.0.0

class MyMetricCheck(AgentCheck)
    def check(self, instance)
        self.gauge('my_metric', random.randint(0,1000), tags=['typetest'])
```
Custom Agent code etcdatadog-agentchecks.dmy_metric.py










# Visualizing Data
## Datadog API script
Please check attached ddTimeboard1.py

## Screenshot of Timeboard
Past 1 Hour
![](mediaimage6.png)

Past 5 minutes
![](mediaimage7.png)

## Snapshot of Graph in email
![](mediaimage8.png)

## What is the Anomaly graph displaying
Based on the past trend, Datadog imply whether metrics values are within the expected range or not. If the metric value is outside of expected range, graph is displayed differently.
In the following graph, expected range is displayed grey area and anomaly data is displayed with red line.
![](mediaimage9.png)







# Monitoring Data
## Alert Configuration &amp; notified email

I configured following Threshold alert.
![](mediaimage10.png)








![](mediaimage11.png)


```
@kazuri@qf7.so-net.ne.jp

{{#is_alert}}
 Alert is triggered. Current value is, {{value}}
 Host IP Address {{host.ip}}
Please check the my_service's status.
{{is_alert}}
{{#is_warning}}
  Warning. , {{value}}
{{is_warning}}
{{#is_no_data}}
  No data returned over 10minutes!
{{is_no_data}}

```
Message content.


















Screenshot of notified email at alert state.
Note I temporary change the threshold value, because I could not receive alert with 800.
![](mediaimage12.png)







## Downtime configuration
### Weekday downtime schedule configuration
![](mediaimage13.png)




Notified email when I create.
![](mediaimage14.png)

Notified email when it enters downtime.
![](mediaimage15.png)



### Weekend downtime schedule configuration
![](mediaimage16.png)







Notified email
![](mediaimage17.png)


# Collecting APM Data
## Screenshot and Links
### Screen shot
![](mediaimage18.png)

![](mediaimage19.png)

![](mediaimage20.png)

### Link of dashboard.
httpsp.datadoghq.comsbdzuqk188by5mh7ni-5051b5d89878a5eff90fc7af0e0b52c2

### Application code
Python application code is included in, empapp.zip file.

I utilized PythonFlask code below.
httpscodeloop.orgflask-crud-application-with-sqlalchemy


## What is the difference between a Service and a Resource
Service is a process, component. Examples of services are, Web Application, End Point, Database and Microservices.
Resource is a specific action which is provided within a service.
Like add a product to shopping cart, sql query which return list of order history, etc.

Within APM Trace tab, you can verify your service, resource like below.
![](mediaimage21.png)




# Final Question

Current covid-19 situation, various event, like concert, are delivered by online streaming.
Sometimes video streaming is delayed, it takes a time to enroll. And worst case, online distribution canft be started because of service down.
These events are not free. And if you canft deliver an event you have to engage a lot of negative work and cause customer retention issue.
In order to avoid these situations, organization who hosts events can use Datadog to monitor infrastructure resources.
You could monitor each event and recognize how many users are enrolled, how server, network resources are utilized etc. And utilize these information for next event.

The Esports market is growing rapidly, so same scenario could be applied to this area too.








# Extra self-learning

As a self-learning, I tried following integration, functionalities and APM.
   Kubernetes cluster host map using minikube
   Synthetic test
   SLO widget based on Synthetic test monitoring.
   APM for Simple Spring Boot (Tomcat, SQL Server)
   Tomcat log integration
   AWS integration

Screenboard
![](mediaimage22.png)












Simple Spring Boot APM
![](mediaimage23.png)

![](mediaimage24.png)






Tomcat log
![](mediaimage25.png)


![](mediaimage26.png)


![](mediaimage27.png)


AWS integration includes basic lambda metrics.
![](mediaimage28.png)
