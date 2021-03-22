# kuber_lesson_1

##### 1.Create cluster
```
root@ansible-ctl:~/hello-kubernetes# gcloud config set compute/zone us-east1-b
root@ansible-ctl:~/hello-kubernetes# gcloud container clusters create kuber-lesson-1
root@ansible-ctl:~/hello-kubernetes# gcloud container clusters get-credentials kuber-lesson-1
```
##### 2.Get docker image
```
root@ansible-ctl:~/hello-kubernetes# docker pull yeasy/simple-web
```
##### 3.Create deploy
```
root@ansible-ctl:~/hello-kubernetes# kubectl create deployment lesson-11 --image=yeasy/simple-web --replicas=2
root@ansible-ctl:~/hello-kubernetes# kubectl get pods
NAME                         READY   STATUS    RESTARTS   AGE
lesson-11-756f869f78-kj4mx   1/1     Running   0          2m20s
lesson-11-756f869f78-wgfh5   1/1     Running   0          2m20s
```
##### 4.Createt autoscale
```
root@ansible-ctl:~/hello-kubernetes# kubectl autoscale deployment lesson-11 --min=4 --max=6 --cpu-percent=60
root@ansible-ctl:~/hello-kubernetes# kubectl get pods
NAME                         READY   STATUS    RESTARTS   AGE
lesson-11-756f869f78-bxrfc   1/1     Running   0          33s
lesson-11-756f869f78-kj4mx   1/1     Running   0          3m4s
lesson-11-756f869f78-vcqh2   1/1     Running   0          33s
lesson-11-756f869f78-wgfh5   1/1     Running   0          3m4s
```

##### 5.Create service
```
root@ansible-ctl:~/hello-kubernetes# kubectl expose deployment lesson-11 --type=LoadBalancer --port 80 --target-port 80
```

##### 6.Check application
```
root@ansible-ctl:~/kuber_lesson_1# curl http://35.243.164.184/
<!DOCTYPE html> <html> <body><center><h1><font color="blue" face="Georgia, Arial" size=8><em>Real</em></font> Visit Results</h1></center><p style="font-size:150%" >#2021-03-22 18:38:00: <font color="maroon">1</font> requests from &lt<font color="navy">gke-kuber-lesson-1-default-pool-78f08e35-cbtv.us-east1-b.c.levelup-304618.internal</font>&gt to WebServer &lt<font color="navy">10.92.1.5</font>&gt</p><p style="font-size:150%" >#2021-03-22 18:46:15: <font color="red">1</font> requests from &lt<font color="blue">LOCAL: 10.92.1.1</font>&gt to WebServer &lt<font color="blue">10.92.1.5</font>&gt</p></body> </html>root@ansible-ctl:~/kuber_lesson_1#
```
