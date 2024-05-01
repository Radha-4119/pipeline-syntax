# pipeline-syntax
pipeline {
    agent any

    stages {
        stage('Code') {
            steps {
                git branch: "$branch", url: 'https://github.com/Radha-4119/one.git'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage("deploy") {
            steps {
                sshagent(['slave']) { 
                     sh 'scp -o StrictHostKeyChecking=no target/*.war ec2-user@34.228.169.170:/home/ec2-user/apache-tomcat-9.0.88/webapps'
}
            }
        }
    }
}
