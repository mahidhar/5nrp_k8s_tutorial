# 5NRP Kubernetes Tutorial

AI Examples\
Hands on session

## AI Training Example

You can use the yaml files from the repo as is but please change the username to something unique as we are all sharing the same namespace. We start by running the training example:

```
kubectl apply -f pytorch-training.yaml
```
Check on status:

```
kubectl get pods
```

When the job is in run state you can check the logs for output:

```
kubectl logs gp3-username
```

Once you are done exploring, please delete the pod:

```
kubectl delete -f pytorch-training.yaml
```

## Inference Example

Start up the inference pod:

```
kubectl apply -f tgi-inference.yaml
```

Once the pod is running, get interactive access to the pod:

```
kubectl exec -it tgi-username -- /bin/bash
```

Once in the pod, start a python3 interpreter and then run:

```
from huggingface_hub import InferenceClient
client = InferenceClient(model="http://0.0.0.0:80")
or token in client.text_generation("Who made cat videos?", max_new_tokens=24, stream=True): print (token)
```

## End

**Please make sure you did not leave any running pods. Jobs and associated completed pods are OK.**

