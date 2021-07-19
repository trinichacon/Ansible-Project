pipeline {
    environment {
        mavenHome = tool 'my-maven'
    }
    agent any
  
    stages {
        stage ("Git Clone") {
            steps {
                git branch: 'main',  url: 'https://github.com/trinichacon/Ansible-Project.git'
            }
        }

        stage ("Maven Clean Package") {
            steps {
                sh "${mavenHome}/bin/mvn clean package"
            }
        }
    
        stage('Ansible Deploy') {
            steps {
                ansiblePlaybook( 
                    playbook: 'deploy-war-file.yaml',
                    inventory: 'dev.inv', 
                    credentialsId: 'ubuntu',
                    extras: '-vvv') 
            }
        }
    }
}
