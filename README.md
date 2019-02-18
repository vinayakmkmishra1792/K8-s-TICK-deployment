# K8-s-TICK-deployment
- To deploy the whole TICK stack. 

Prior Requirements:  
- Create a neamespace monitoring. Else you can change the internal yaml namespaces accordingly.
- T is deployed as Deamon set.
- Please change Persistent Volumes according to your deployment and claim PVC's. I have it on Azure disks in this commit.

Step 1:
kubectl create namespace monitoring

Step 2:
2.1)kubectl apply -f /influxdb/ -R
2.2)kubectl apply -f /telegraf/ -R
2.3)kubectl apply -f /kapacitor/ -R
2.4)kubectl apply -f /chronograf/ -R

Step 3:
To see data in Influx get an process to influx :

-kubectl get all --namespace monitoring
-kubectl exec -i -t influxdb-0 --namespace monitoring -- influx

--SHOW DATABASES
--USE telegraf
--SHOW MEASUREMENTS
--SELECT * FROM diskio LIMIT 2
--DROP MEASUREMENT access_log

Step 4:

Create graphs on Chronograf via port forward(Use influx query intelligence. Instead of Drag and drop for writing queries)
--kubectl port-forward svc/chronograf 8888:80 --namespace monitroing
