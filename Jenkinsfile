node {
   stage('Preparation') { 
      git 'https://github.com/navneethproject02/fleetman-webapp'
   }
   stage('Build') {
      sh "mvn package"
   }
   stage('Results') {
      junit '**/target/surefire-reports/TEST-*.xml'
      archive 'target/*.war'
   }
   stage('deploy'){
     
     withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'jenkins_credentials_for_ansible', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
       ansiblePlaybook credentialsId: 'ssh-balvinder-pem-key', installation: 'ansible-installation', playbook: 'deploy.yaml', sudoUser: null
     }
   }
}
