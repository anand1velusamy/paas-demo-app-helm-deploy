node {
   def app

    stage('Clone Repo') {
      // Checkout SCM
         checkout scm
         sh 'cat <<EOF > /etc/yum.repos.d/kubernetes.repo \
[kubernetes] \
name=Kubernetes \
baseurl=https://packages.cloud.google.com/yum/repos/kubernetes-el7-x86_64 \
enabled=1 \
gpgcheck=1 \
repo_gpgcheck=1 \
gpgkey=https://packages.cloud.google.com/yum/doc/yum-key.gpg https://packages.cloud.google.com/yum/doc/rpm-package-key.gpg \
EOF'
         sh 'yum install -y kubectl'
         sh 'kubectl get pods'
    }    
  
    stage('Build Project') {
      // build project via maven
       sh "mvn -D maven.test.failure.ignore clean package"
    }
  
    stage('Publish Tests Results'){
      echo " Will be integrated with Testing platforms in Phase 2"
    }
    
    stage('Build Docker Image') {
      // build docker image
      sh "mv ./target/hello*.jar ./data" 
      app = docker.build("paas-demo-app")
    }
   
    /*stage('Push image') {
         Finally, we'll push the image to ECR on latest tag. 
        sh "eval \$(aws ecr get-login --no-include-email --region us-west-1 | sed 's|https://||')"       
        docker.withRegistry('https://490747939488.dkr.ecr.us-west-1.amazonaws.com/paas-demo-app:latest', 'ecr:us-west-1:ecr-credentials') {
            docker.image('paas-demo-app').push('latest')
    }
    }*/

    stage('Helm Push Stage') {
        /* Finally, we'll push the image to Kubernetes Cluster. */
        sh "eval \$(aws ecr get-login --no-include-email --region us-west-1 | sed 's|https://||')"
        sh 'wget https://storage.googleapis.com/kubernetes-helm/helm-v2.7.2-linux-amd64.tar.gz'
        sh 'tar -zxvf  helm-v2.7.2-linux-amd64.tar.gz'
        sh 'mv linux-amd64/helm /usr/local/bin/helm'
        sh 'helm init --upgrade'
        sh 'helm repo update'
        sh 'helm package ./helm-chart/paas-demo-app'
        sh 'helm install --name paas-demo-app paas-demo-app-1.0.0.tgz'
        sh 'helm ls'
} 
    
    }
