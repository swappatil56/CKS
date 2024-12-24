Preview Question 1
Use context: kubectl config use-context infra-prod

You have admin access to cluster2. There is also context gianna@infra-prod which authenticates as user gianna with the same cluster.

There are existing cluster-level RBAC resources in place to, among other things, ensure that user gianna can never read Secret contents cluster-wide. Confirm this is correct or restrict the existing RBAC resources to ensure this.

I addition, create more RBAC resources to allow user gianna to create Pods and Deployments in Namespaces security, restricted and internal. It's likely the user will receive these exact permissions as well for other Namespaces in the future.



