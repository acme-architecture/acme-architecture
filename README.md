**Q. Certain web pages are loading slow in user’s browser for our live web application. What
 steps will you take to resolve the issue?**
  
  
**Q. Imagine a scenario where a web application is serving from a single web server to the internet. 
What are the problems in this scenario?** 

**Design and architect a solution that will mitigate these problems?** 
**Or How would you design a scalable architecture with resiliency in mind for the following situations:
**

* If a service is resource intensive 
* A service needs to be low latency 
* if parts of a service need to be restricted to certain geographical boundaries


Q. Currently there’s no monitoring in place for the above single web server. How and
what application will you use to monitor the resources/process in your new design?

Q. Currently there’s no monitoring in place for the above single web server. How and
what application will you use to monitor the resources/process in your new design?
   
Q. In our server we want to create a user who can only view logs using `less` from this
path /var/log. Please explain how to achieve this.


Q. Explain how you can ssh into a private server from the
internet.

Q. Write a bash function that will find all occurrences of an IPv4 from any given
file.

Submission:
1) Implement solution for these problems. 2) Upload to github/bitbucket or any other
code sharing platform. 3) Send an email to info@platformx.com.co with subject
“PlatformX SRE Test” with your
code repository URL in the email
body.


Acme Architecture
==

Acme company is a Home video broadcasting system need service design implementation that
resilency and scalable

### Cloud provider

Amazon AWS is provide cloud infrastructure. Acme services base on **Symphony** php framework that use 
Mysql base we decide to use Amazon RDS that offer **replication across region** and they provide
decdicate bandwidth for back-bone replication.
 

### Orchrestration

Kubernetes 


### Auto Scaler 


```kubectl autoscale deployment php-apache --cpu-percent=50 --min=1 --max=10```

**_NOTE k8s only support Autoscaler by CPU and custom metrics for timebase_**


### Routing by Geolocation and access control.




### Improvement


Previous system acme company use Nginx caching for their website and video services this is 
not enough they will good for minimal user 10,000 - 20,000 concurrent ( Maximum 35,000 concurrent )
this condition for short lenght of Video (2MB) with m4.2xlarge ( 8vCPU and 32GB ) instances type.


Important think we must know about limitation when you provide with HTTPS and 
cache must be burn with a lot of user watching their video that have variety and long-length
to playback service. also they must pay with a lot of pricing of bandwidth.

Acme system can survive 15min. when you burst of traffic user to view their favorite media.
 
#### Peer to Peer Video

We suggest peer to peer cdn for video services. Instead we provide single-source to serving
Video medias. When user connect unique key frame they will play normally rest of 
same key frame their will serve from peer network. 

This will reduce a mount of your server and bandwidth cost. It's good choice. 

![](images/peer5.png)


#### Monitoring. 

Rest of infrastructure we can monitoring through Kubernetes dashboard is pretty but we want
to do more for service quality. 


##### Alert and Notification.

Our Acme kubernetes combined with Prometheus and Grafana. 


## Trouble shooting

When web-site slow down. 

* from client site we must check for TTFB return.
* from Administrator can check network latency from server side to last hop client.
* from server side Administrator can check from monitoring metric ( prometheus & grafana
dashboard)


## Accessing 

We provide VPN service for service maintenance. But optional we give one small ec2 instance.
to provide access as Bastion host instead.

[ picture bastion host]

## Advance access control. 

Acme company have special policy that want to control regular user to access system log file
under ```/var/log/*``` with read-only permission. 

Normally we can use sudoerr to solve this problem. Administrator write sudo-err file to specify
```less``` command provide to regular user who need to access. 

Advance technique we use concept of Mandatory Access Control or MAC to control with below.
Because we use CentOS7 that provide SELinux ( for another distro like Ubuntu is Apparmor)


[ howto command ]

Benefit of MAC. 

* More control with insentive security. 
* User does not need to be list in sudoerr 
* Command can run only under ```/var/log/``` folder.
* Can audit. 


## Tips

#### Base file to grep IPV4 

[ bash code to provide access ipv4 ]


#### reference

* https://github.com/kubernetes/ingress-nginx/issues/739#issuecomment-378779030
* https://github.com/kubernetes/contrib/tree/master/ingress/controllers/nginx/examples/custom-template
* https://aws.amazon.com/ec2/instance-types/
* https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/#support-for-horizontal-pod-autoscaler-in-kubectl




 


  

