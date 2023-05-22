for i in $(kubectl api-resources --verbs=list --namespaced -o name | grep -v "event"); do kubectl get $i -n <namespace_name>; done

kubectl api-resources --verbs=list --namespaced --no-headers -o name | foreach { kubectl get $_ -n <namespace_name> }
