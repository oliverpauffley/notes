# Stateful Set

a [[Kubernetes]] object designed to work with stateful applications like databases.

Eg a node js server would talk to a stateful database like mongoDB. So the Mongo server is a stateful set.

Similar to [[Deployments]] as they can both manage mutliple replicas and can both deal with volumes, secrets and configMaps.

### Differences to Deployments

In deployments the pods are identical and interchangable. A load balancer can choose any pod and will get the same result.

Statefulsets cannot be treated in the same way. They have a **fixed address** and are not identical. Each pod is not **interchangeable**.  

#### Scaling database applications
when scaling databases you cannot have mutliple pods that can both read and write. Instead, one is designated as a **MASTER** and the rest are **SLAVES** where the slaves can **only** read.

The do not use the same storage. Instead the data is duplicated across each storage unit. So each time there is a write to master the slaves have to be updated to have the correct data. 

When a new slave is added it reads from the **previous** node to copy that data and then starts to sync from master.

#### Pod state
Each pod has [[Persistent volumes]] that store not only the data but also information about the pod state. When a pod dies that peristent volume is reattached.

For this to work the peristent volume has to be remote. Otherwise if the pod is started on a new node it won't be able to connect to the same volume.

##### 2 end points
each stateful set has a fixed name and endpoint and a changing ip address. That means the fixed endpoint can be used to always refer to the same pod. 