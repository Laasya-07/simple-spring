pipeline {
  agent any
   environment {
        AZURE_SUBSCRIPTION_ID='1fe9963c-1fe2-4dcc-83a7-b49978ffb277'
        AZURE_TENANT_ID='06698be3-7107-4e65-ac59-1967f7c7c43e'
        CONTAINER_REGISTRY='testregistry890'
        RESOURCE_GROUP='har-rg'
    }
  stages {
    stage('clone resources') {
      steps {
        script {
           git branch: 'master', url: 'https://github.com/Laasya-07/simple-spring.git'
        }
      }
    }
    stage('build program') {
      steps {
        script {
           bat 'docker build -t simple-spring .'
           
        }
      }
    }
    stage('push to acr') {
      steps {
        script {
            
                            bat 'az login --service-principal -u bc874204-d778-4a79-96c6-90358550c62e -p 3Ds5yAi_HEa6Vi2bryT-0P.G9_F9bXi06m -t 06698be3-7107-4e65-ac59-1967f7c7c43e'
                            bat 'az acr login --name testregistry890 --resource-group har-rg'
                            bat 'docker tag simple-spring testregistry890.azurecr.io/simple-spring'
                            bat 'docker push testregistry890.azurecr.io/simple-spring'
                        
        }
      }
    }
    stage('Deploy'){
     steps{
         
        bat 'echo "logging in" '
        bat 'az login --service-principal -u bc874204-d778-4a79-96c6-90358550c62e -p 3Ds5yAi_HEa6Vi2bryT-0P.G9_F9bXi06m --tenant 06698be3-7107-4e65-ac59-1967f7c7c43e'
        bat 'az aks get-credentials --resource-group har-rg --name democluster'
        bat 'kubectl apply -f sample.yaml'
    
}
}
}
}
