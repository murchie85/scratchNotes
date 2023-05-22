for i in $(kubectl api-resources --verbs=list --namespaced -o name | grep -v "event"); do kubectl get $i -n <namespace_name>; done

kubectl api-resources --verbs=list --namespaced --no-headers -o name | foreach { kubectl get $_ -n <namespace_name> }


#!/bin/bash
POD_NAME="your-pod-name"
NAMESPACE="your-namespace"

kubectl logs $POD_NAME -n $NAMESPACE | jq -r 'to_entries | .[] | "\(.key): \(.value)\n"'


#!/bin/bash

read -p "Enter the Pod name: " POD_NAME
read -p "Enter the Namespace: " NAMESPACE

kubectl logs $POD_NAME -n $NAMESPACE | jq -r 'to_entries | .[] | "\(.key): \(.value)\n"'

