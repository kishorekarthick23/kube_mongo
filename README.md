# kube_mongo
Two tier app using AWS, Terraform, docker, kubernetes. Java and mongodb

Steps:

Install eksctl: 

https://docs.aws.amazon.com/eks/latest/userguide/eksctl.html

eksctl utils associate-iam-oidc-provider --cluster devcluster --approve

EBS CSI - Elastic Block storage - container storage interface! 

eksctl create iamserviceaccount \
  --name ebs-csi-controller-sa \
  --namespace kube-system \
  --cluster devcluster \
  --attach-policy-arn arn:aws:iam::aws:policy/service-role/AmazonEBSCSIDriverPolicy \
  --approve \
  --role-only \
  --role-name AmazonEKS_EBS_CSI_DriverRole


eksctl create addon --name aws-ebs-csi-driver --cluster devcluster --service-account-role-arn arn:aws:iam::#accountnumber:role/AmazonEKS_EBS_CSI_DriverRole --force


final execution order. 

kubectl create -f storageclass.yaml
kubectl create -f pvc.yaml
kubectl create -f mongodb.yaml
kuberctl create -f ingressctrl.yaml
