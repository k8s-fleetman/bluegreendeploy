pipeline {
   agent any
   environment {
     SERVICE_NAME = "deploytypes"
   }
   stages {
      stage('Preparation') {
         steps {
            cleanWs()
            git credentialsId: 'GitHub', url: "https://github.com/${ORGANIZATION_NAME}/${SERVICE_NAME}"
         }
      }
      stage('Deploy GREEN OR A version') {
         steps {
            sh 'cat nginx-green.yaml'
            sh 'kubectl apply -f nginx-green.yaml'
         }
      }
      
      stage('Deploy BLUE OR B version') {
         steps {
            sh 'cat nginx-blue.yaml'
            sh 'kubectl apply -f nginx-blue.yaml'
         }
      }
      
      stage('Update BLUE version on Production') {
         steps {
            sh 'cat blueonprod.yaml'
            sh 'kubectl apply -f blueonprod.yaml'
         }
      }
   }
}
