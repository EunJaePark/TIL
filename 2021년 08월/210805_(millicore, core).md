1000m = 1core

https://discuss.kubernetes.io/t/metric-server-cpu-and-memory-units/7497/2

kubernetes의 `podSpec.resource.requests.cpu`, `podSpec.resource.limits.cpu`의 최소단위는 `millicore(m)`이다.

https://goteleport.com/blog/kubernetes-resource-planning/

> **CPU**   
> CPU resources are measured in millicore. If a node has 2 cores, the node’s CPU capacity would be represented as 2000m. The unit suffix m stands for “thousandth of a core.”
>
> 1000m or 1000 millicore is equal to 1 core. 4000m would represent 4 cores. 250 millicore per pod means 4 pods with a similar value of 250m can run on a single core. On a 4 core node, 16 pods each having 250m can run on that node.
>
> Next, unless the apps require multi-core processing such as a multi-threaded database, the best practice is to define to 1000 or below. Then, run more replicas to scale out those applications. It is important to note, pods will never be scheduled if they are defined more than the node’s capacity. A pod cannot have a definition of 3000m on a 2 core node.
>
> Keep in mind, CPU is a compressible resource. In simple terms, applications will start throttling once they hit the CPU limits. Throttling can adversely affect your application’s performance by making it run slower. Kubernetes will not terminate those apps. Hence, you should take this into consideration as you architect your applications.


> **Memory**      
> Memory is measured in bytes. However, you can express memory with various suffixes (E,P,T,G,M,K and Ei, Pi, Ti, Gi, Mi, Ki) to express mebibytes (Mi) to petabytes (Pi). Most simply use Mi.
>
> Like CPU, pods will never be scheduled if they require more resources than the capacity of a node. Unlike CPU, memory is not compressible. You can’t make memory run slower or faster like CPU or network throttling. Pods will be terminated if it reaches the memory limit.




