pipeline {
   agent any
   stages {
      stage('Preparation') {
         steps {
            cleanWs()
            git credentialsId: 'GitHub', url: "https://github.com/${ORGANIZATION_NAME}/${SERVICE_NAME}"
         }
      }
      stage('Deploy Green OR A version') {
         steps {
            sh 'cat nginx-green.yaml'
            sh 'kubectl apply -f nginx-green.yaml'
         }
      }
      
      stage('Deploy Blue OR B version') {
         steps {
            sh 'cat nginx-blue.yaml'
            sh 'kubectl apply -f nginx-blue.yaml'
         }
      }
      stage('Deploy Default or pervious version') {
         steps {
            sh 'cat nginx-blue.yaml'
            sh 'kubectl apply -f nginx-default.yaml'
         }
      }     
      stage('Roll back the deploy') {
         steps {
            sh 'default-ingress.yaml'
            sh 'kubectl apply -f default-ingress.yaml'
         }
      }
   }
}
