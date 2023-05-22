# check all resources 
for i in $(kubectl api-resources --verbs=list --namespaced -o name | grep -v "event"); do kubectl get $i -n <namespace_name>; done

kubectl api-resources --verbs=list --namespaced --no-headers -o name | foreach { kubectl get $_ -n <namespace_name> }

# pars logs with jq
#!/bin/bash
POD_NAME="your-pod-name"
NAMESPACE="your-namespace"

kubectl logs $POD_NAME -n $NAMESPACE | jq -r 'to_entries | .[] | "\(.key): \(.value)\n"'

# pars logs with jq  and prompt user 
#!/bin/bash

read -p "Enter the Pod name: " POD_NAME
read -p "Enter the Namespace: " NAMESPACE

kubectl logs $POD_NAME -n $NAMESPACE | jq -r 'to_entries | .[] | "\(.key): \(.value)\n"'


# parse logs with python
#!/bin/bash

read -p "Enter the Pod name: " POD_NAME
read -p "Enter the Namespace: " NAMESPACE

kubectl logs $POD_NAME -n $NAMESPACE | while read -r line; do 
  echo "$line" | python -c "import sys, json; data=json.loads(sys.stdin.read()); print('\n'.join([f'{k}: {v}' for k, v in data.items()])); print('\n')"
done
