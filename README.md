# helm-vllm

An helm chart for the VLLM project using official images based on the [official documetnation](https://docs.vllm.ai/en/latest/serving/deploying_with_k8s.html}

# Configurations
## General
|Prefix|Option|Value|Description|
-------------------------
|general|nodeSelector|YAML|YAML object to put under node selector|
|general|tolerations|YAML|YAML object to put under tolerations|
|general|affinity|YAML|YAML object to put under affinity|

## vllm
### General
|Prefix|Option|Value|Description|
-------------------------
|vllmConfig|vllmModel|String |The name of the model to use|
|vllmConfig|vllmIsTrustRemoteCode|bool|Enable/Disable trust in external source|
|vllmConfig|vllmIsEnableChunkPrefill|bool|Enable/Disable chunckPrefill|
|vllmConfig|vllmMaxNumBatchedTokens|Int|Number of Batched tokens|
### Resources
#### GPU
|Prefix|Option|Value|Description|
-------------------------
|vllmConfig.vllmResources|vllmResourcesGpuEnabled|bool|Enable/Disable GPU|
|vllmConfig.vllmResources|vllmResourcesGpuResourcesNvidiaResourceName|String|The name of the nvidia config option|
#### Requests
|Prefix|Option|Value|Description|
-------------------------
|vllmConfig.vllmResources.vllmResourcesRequest|vllmResourcesRequestCpu|Mi/int|CPU requests|
|vllmConfig.vllmResources.vllmResourcesRequest|vllmResourcesRequestMem|Size|Memory requests|
|vllmConfig.vllmResources.vllmResourcesRequest|vllmResourcesRequestGpu|int|GPU resources|
#### Limits
|Prefix|Option|Value|Description|
-------------------------
|vllmConfig.vllmResources.vllmResourcesLimit|vllmResourcesLimitCpu|Mi/int|CPU requests|
|vllmConfig.vllmResources.vllmResourcesLimit|vllmResourcesLimitMem|Size|Memory requests|
|vllmConfig.vllmResources.vllmResourcesLimit|vllmResourcesLimitGpu|int|GPU resources|

## Hugging Face
|Prefix|Option|Value|Description|
-------------------------
|hf|hfSecretName|String|The pregenerated secret name for the Hugging face token|

## pod
### General
|Prefix|Option|Value|Description|
-------------------------
|pod|replicaCount|int|The number of replica for the pods|
|pod|imagePullSecrets|List|List of the secrets to use to pull the image|
|pod|nameOverride|String|Override of the deployent name|
|pod|fullnameOverride|String|Override of the deployent name|
|pod|podAnnotations|String|Custom pod annotation|
|pod.podLabels|YAML|Custom labels|

### Image
|Prefix|Option|Value|Description|
-------------------------
|pod.image|repository|String|The image repository source|
|pod.image|pullPolicy|Always/IfNotPresent/Never|When to pull the image|
|pod.image|tag|String|The image tag(default: null)|


###  Security
|Prefix|Option|Value|Description|
-------------------------
|pod.security|securityPodSecurityContext|YAML|Custom security context|
|pod.security|securityContext|YAML|Custom security context|

### Autoscaling
|Prefix|Option|Value|Description|
-------------------------
|pod.autoscaling|enabled|bool|Enable/Disable HPA(default: false)|
|pod.autoscaling|minReplicas|Int|Minimum number of replicas for autoscaling|
|pod.autoscaling|maxReplicas|Int|Maximum number of replicas for autoscaling|
|pod.autoscaling|targetCPUUtilizationPercentage|String|The maximum CPU utlization to denote scale|
|pod.autoscaling|targetMemoryUtilizationPercentage|String|The maximum memory pressure to denote scale|

## Storage
### General
|Prefix|Option|Value|Description|
-------------------------
|storage|volumesAdditional|List|List of additional volumes|
|storage|volumeMounts|List|List of additional mounts|

### Cache
|Prefix|Option|Value|Description|
-------------------------
|storage.volumesCache|volumeCacheName|String|The shared cache volume name|
|storage.volumesCache|volumeCacheSize|Size|The Size of the volume for the shared cache volume|
### Shared memory
|Prefix|Option|Value|Description|
-------------------------
|storage.volumesShm|volumeShmSize|Size|The Size of the volume for the Shared memory volume|

## serviceAccount:
|Prefix|Option|Value|Description|
-------------------------
|serviceAccount|create|bool|Enable/disable the creation of Service Account|
|serviceAccount|automount|bool|Enable/disable automounting the service account|
|serviceAccount|annotations|YAML|Custom annotation object|
|serviceAccount|name|String|Customize the name|

## Network
### Service
|Prefix|Option|Value|Description|
-------------------------
|network.service|type|ClusterIP/NodePort/LoadBalancer/ExternalName|K8S service type|
|network.service|port|Int|Internal port of the container(default: 8080)|
### Ingress
|Prefix|Option|Value|Description|
-------------------------
|network.ingress|enabled|bool|Enable/Disable ingress|
|network.ingress|className|String|Ingress Class name|
|network.ingress|annotations|YAML|Custom ingress annotations|
|network.ingress|hosts|List|List of ingress hosts|
|network.ingress|tls|List|List of secrets to use for certificate|
## Health check
|Prefix|Option|Value|Description|
-------------------------
|health|livenessProbe|YAML|YAML object of the liveliness probe check|
|health|readinessProbe|YAML|YAML object of the readiness probe check|


