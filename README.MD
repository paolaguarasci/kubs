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