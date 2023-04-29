# Helm chart
## 011-Install HELM
    helm help
    helm version
## 012-Work with Repos
    helm repo list
    helm repo add bitnami https://chart.bitnami.com/bitnami
    helm search repo mysql
    helm search repo database
    helm search repo database --version
    helm search hub
## 013-Execute Services using HELM
    helm install my-redis bitnami/redis --version 17.3.9
    helm install my-redis bitnami/redis 
    helm list

## 014-Re Use Deployment Naming
    helm install -n redis my-redis bitnami/redis 
    helm list --all-namespaces # or -A
    helm status my-redis
    helm status my-redis -n redis
## 015-Provide Custom Values to HELM Chart
    helm delete my-redis
    helm delete my-redis -n redis 

    helm install my-release \
    --set auth.rootPassword=secretpassword,auth.database=app_database \
    bitnamicharts/mariadb --version 17.3.9

    helm install my-release --values /path_of_yaml_file_1 bitnamicharts/mariadb --version 17.3.9
## 016-Upgrade Services Using HELM
    helm repo update 
    helm upgrade my-release --values /path_of_yaml_file_1 bitnamicharts/mariadb --version 17.4
        helm upgrade my-release --values /path_of_yaml_file_2 bitnamicharts/mariadb --version 17.3.9

## 017-HELM Release Records
    helm get secret -n database
    helm uninstall my-mariadb -n database
    helm uninstall my-mariadb -n database --keep-history
## 019-Validate Resource before Deployment
    helm install my-release --values /path_of_yaml_file_1 bitnamicharts/mariadb --version 17.3.9 --dry-run
## 020-Generate K8s Deployable YAML using HELM
    helm template my-release --values /path_of_yaml_file_1 bitnamicharts/mariadb --version 17.3.9
## 021-Details of HELM Deployment Releases
    helm get secret -n database name_of_secret
    helm get secret -n database sh.helm.release.v1.my-mariadb.v3 -o yaml
## 022-Get Details of Deployed Deployment
    helm get nodes my-mariadb -n database
    helm get values my-mariadb -n database
    helm get values my-mariadb -n database --revision 2
    helm get manifest my-mariadb -n database --revision 2
## 023-Rollback Application using HELM
    helm history my-mariadb -n database
    helm rollback my-mariadb 1
    helm rollback my-mariadb -n database  1
    helm rollback my-mariadb -n database --revision 1
## 024-Wait HELM Deployment for Successful Installation
    helm install -n redis my-redis bitnami/redis  --wait --timeout 20m
    helm upgrade my-release --values /path_of_yaml_file_1 bitnamicharts/mariadb --version 17.4  --wait --timeout 20m
    helm upgrade my-release --values /path_of_yaml_file_1 bitnamicharts/mariadb --version 17.4  --atomic  #default timeout is 5m
    helm upgrade my-release --values /path_of_yaml_file_1 bitnamicharts/mariadb --version 17.4  --atomic --timeout 20m
## 026-Create HELM Chart
    helm create my_first_chart
## 027-Install the Custom Chart
    helm install custom_deployment my_first_chart
    helm ls -A

## 032-Package Your HELM Chart
    helm package my_first_chart
    helm package my_first_chart -d /directory #for put package
    helm package my_first_chart -u # first download latest version of dependency and after that package them
## 033-Validate HELM Chart
    helm lint my_first_chart
## 034-Actions in Template
    helm template my_first_chart
## 042-Template Validation
    helm lint
    helm template
    helm --dry-run