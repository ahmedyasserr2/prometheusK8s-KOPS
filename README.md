Sure, I can help you document the project and highlight the key steps and commands you used. Here's a structured document based on your commands:

---

**Project Documentation: Setting up Prometheus on Kubernetes Cluster**

**Objective**: Deploy Prometheus to monitor a Kubernetes cluster created using KOPs.

**Step 1: Setup Environment**
- Generated SSH key:
  ```bash
  ssh-keygen
  ```
- Installed AWS CLI:
  ```bash
  sudo apt update
  sudo apt install awscli
  ```
- Configured AWS credentials:
  ```bash
  aws configure
  ```

**Step 2: Install kubectl and kops**
- Installed kubectl:
  ```bash
  wget https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl
  chmod +x kubectl
  sudo mv kubectl /usr/local/bin/
  ```
- Installed kops:
  ```bash
  wget https://github.com/kubernetes/kops/releases/download/v1.26.4/kops-linux-amd64
  chmod +x kops-linux-amd64
  sudo mv kops-linux-amd64 /usr/local/bin/kops
  ```

**Step 3: Create Kubernetes Cluster using KOPs**
- Created a Kubernetes cluster using KOPs:
  ```bash
  kops create cluster --name=kube-vprofile.yassser.shop --state=s3://321g --zones=us-east-1a,us-east-1b --node-count=2 --node-size=t3.small --master-size=t3.medium --dns-zone=kube-vprofile.yassser.shop --node-volume-size=8 --master-volume-size=8
  ```
- Updated the cluster:
  ```bash
  kops update cluster --name kube-vprofile.yassser.shop --state=s3://321g --yes --admin
  ```

**Step 4: Deploy Prometheus using Helm**
- Installed Helm:
  ```bash
  curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3
  chmod 700 get_helm.sh
  ./get_helm.sh
  ```
- Added Prometheus Helm repository:
  ```bash
  helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
  helm repo update
  ```
- Installed Prometheus using Helm:
  ```bash
  helm install prometheus prometheus-community/kube-prometheus-stack
  ```

**Step 5: Access Prometheus UI**
- Found Prometheus service:
  ```bash
  kubectl get svc -n prometheus
  ```
- Port forwarded Prometheus UI to localhost:
  ```bash
  kubectl port-forward deployment/prometheus-prometheus-kube-prometheus-prometheus-0 9090
  ```

**Conclusion**
- Successfully deployed Prometheus on the Kubernetes cluster.
- Accessed Prometheus UI to monitor cluster metrics.

**Notes**: 
- The project used AWS CLI for managing AWS resources.
- Kubernetes cluster was created using KOPs.
- Prometheus was deployed using Helm, leveraging the Prometheus community Helm chart.

---

Feel free to adjust the document as needed, and ensure it covers all the necessary details for your instructor. If you need further assistance or clarification on any part, let me know!