pipeline {
  agent any
  environment {
    DOCKERHUB_CREDENTIALS = credentials('pratheeknk1205-docker')
  }
    stages {
     stage('Build') {
      steps {
        sh 'docker build -t pratheeknk1205/pratheeknk1205'
      }
    }
    stage('Login') {
      steps {
        sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
      }
    }
    stage('Push') {
      steps {
        sh 'docker push  pratheeknk1205/pratheeknk1205:1.0'
      }
    }
  
   stage('Ansible')
    {
      steps{
          ansiblePlaybook credentialsId: 'ec2', disableHostKeyChecking: true, installation: 'ansible', inventory: 'inventory.inv', playbook: 'ansible.yml'
         
      }
    }
  }
  post {
    always {
      sh 'docker logout'
    }
}
}

     
