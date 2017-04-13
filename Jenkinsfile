node {
   stage('Preparation') { 
      git 'https://github.com/navneethproject02/fleetman-webapp'
   }
   stage('Build') {
      sh "mvn clean package"
   }
   stage('Results') {
      // junit '**/target/surefire-reports/TEST-*.xml'
      archive 'target/*.war'
      archive '*'
   }
   stage('deploy'){
     
     withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'jenkins_credentials_for_ansible', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
       ansiblePlaybook credentialsId: 'ssh-balvinder-pem-key', installation: 'ansible-installation', playbook: 'deploy.yaml', sudoUser: null
     }
   }
   
   stage('blue_to_green'){
     
     withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'jenkins_credentials_for_ansible', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
       ansiblePlaybook credentialsId: 'ssh-balvinder-pem-key', installation: 'ansible-installation', playbook: 'blue_to_green.yaml', sudoUser: null
     }
   }   
}
