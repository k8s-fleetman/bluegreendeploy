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

      stage('Update the Canaray release setup') {
         steps {
            sh 'cat greenonprod.yaml'
            sh 'kubectl apply -f greenonprod.yaml'
         }
      }
   }
}
