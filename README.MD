# Example: Deploying WordPress and MySQL with Persistent Volumes

## Attenzione

versione giocattolo di wp e mysql perché non scala, crea una songola instanza di ognuno.

### Avvio della "cartella"
```bash
kubectl apply -k ./
```



### Terminologia

  - **Kubernets**: Kubernets propriamente detto è un cluster costruito su protocolo di comunicazione, un insieme di API

  - **MiniKube**: Implementazione delle API di Kubernets.

  - **Container**: Tecnologia per impacchettare un'applicazione insieme alle sue dipendenze di runtime. *Immutabile* e pronta all'uso. Se si devono apportare cambiamenti bisogna rifare l'img container. 
  
  - **Worker**: insieme di macchine (reali o virtuali), dette anche **Nodi**, che eseguono l'applicazione conteinerizzata. Ogni **cluster** ha almeno un worker.

  - **Pod**: La più piccola unità deployabile. Può contenere uno o più container che condividono tra loro storage/network e contesto. I container di un singolo pod sono sempre eseguiti in maniera parallela. Parlando in temrini di Docker, un pod può essere visto come un gruppo di container che condividono namespace e fylesistem. 

  - **Kubelet**: Agente eseguito in ogni nodo del cluster, si assicura che i **container** siano eseguiti in un **pod**. 

  - **Servizio**: Astrazione che espone un servizio di rete offerto da qualche applicazione in esecuzione su un set (logico) di Pods. Kubernets assegna un indirizzo IP ad ogni Pods e un nome DNS per ogni set di PODS. Si può fare un load balancing. 




### Comunicazione

 - I container di un singolo pod cominicano via loopback
 - Le API di Kubernets forniscono la comunicazione tra pods differenti
 - I **SERVIZI** espongono risorse al di fuori del cluster, rendendolo raggiungibile dall'esterno. 
 - Si possono cmq creare **servizi** interni al cluster. 

### Come deployare su kubernets

- Creare un'immagine, ad esempio una docker image, creando il relativo Dockerfile.

- Costruire l'img.

```bash
$ docker build -t hello-world-image .
```

- Runnure l'app per sincerarsi che sia tutto ok.
```bash
$ docker run --name hello-world -p 3001:3000 hello-world-image
```

          imagePullPolicy: Never






 Kubernetes Concepts
Kubernetes has a client/server architecture. Kubernetes server runs on your cluster (a group of hosts) on which you will deploy your application. And you typically interact with the cluster using a client, such as the kubectl CLI.
Pods
A pod is the basic unit that Kubernetes deals with, a group of containers. If there are two or more containers that always need to work together, and should be on the same machine, make them a pod.
Node
A node is a physical or virtual machine, running Kubernetes, onto which pods can be scheduled.
Label
A label is a key/value pair that is used to identify a resource. You could label all your pods serving production traffic with “role=production”, for example.
Selector
Selections let you search/filter resources by labels. Following on from the previous example, to get all production pods your selector would be “role=production”.
Service
A service defines a set of pods (typically selected by a “selector”) and a means by which to access them, such as single stable IP address and corresponding DNS name.