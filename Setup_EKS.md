# Source: https://gist.github.com/8ef7f6cb24001e240432cd6a82a515fd

####################
# Create a Cluster #
####################

# Only if you did not yet clone that repository
git clone \
    https://github.com/vfarcic/devops-catalog-code.git

cd devops-catalog-code

git pull

cd terraform-eks/simple

# Replace `[...]` with your access key ID`
export AWS_ACCESS_KEY_ID=[...]

# Replace `[...]` with your secret access key
export AWS_SECRET_ACCESS_KEY=[...]

terraform init

terraform apply

export KUBECONFIG=$PWD/kubeconfig

kubectl get nodes

cd ../../../

#######################
# Destroy The Cluster #
#######################

cd devops-catalog-code/terraform-eks/simple

terraform destroy

cd ../../../
