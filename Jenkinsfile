pipeline {
   agent any
   stages {
      stage('Preparation') {
         steps {
            cleanWs()
            git credentialsId: 'GitHub', url: "https://github.com/${ORGANIZATION_NAME}/${SERVICE_NAME}"
         }
      }
      stage('Switch default site to green') {
         steps {
            sh 'cat greenonprod.yaml'
            sh 'kubectl apply -f greenonprod.yaml'
         }
      }

      stage('Update the Canaray release setup') {
         steps {
            sh 'cat canary-ingress.yaml'
            sh 'kubectl apply -f canary-ingress.yaml'
         }
      }
   }
}
