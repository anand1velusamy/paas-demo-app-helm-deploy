node {
   def app

    stage('Clone Repo') {   
         sh 'kubectl get pods'
         sh 'kubectl config view'
         sh 'helm init'
         sh 'helm ls'
         sh 'mkdir hello && cd hello && git clone https://9826096011383718a035dd8376ba708eb92b92cb@github.com/anand1velusamy/paas-demo-app-helm-deploy'
    }    
  
    /*stage('Build Project') {
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
    }

    stage('Helm Push Stage') {
        /* Finally, we'll push the image to Kubernetes Cluster. 
        sh "eval \$(aws ecr get-login --no-include-email --region us-west-1 | sed 's|https://||')"       
        sh 'helm init --upgrade'
        sh 'helm repo update'
        sh 'helm package ./helm-chart/paas-demo-app'
        sh 'helm install --name paas-demo-app paas-demo-app-1.0.0.tgz'
        sh 'helm ls'
} */
    
    }
