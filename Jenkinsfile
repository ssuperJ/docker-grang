pipeline {
    agent { 
        label 'parallels'
        // dir '/home/parallels'
    }
    tools {
        jdk 'jdk11-agent'
        maven 'maven3'
    }
    environment {
        // WORK_SPACE = "/opt/jenkins/workspace"
        JAVA_HOME = tool('jdk11-agent')
    }
    stages {
        stage('Docker') {
            steps {
                sh 'echo $JAVA_HOME'
                sh 'docker-compose down'
                sh 'docker rmi -f docker-grang-mysql'
                sh 'docker rmi -f docker-grang-mongodb'
                sh 'docker rmi -f docker-grang-mygrang'
                sh 'docker rmi -f docker-grang-chatapp'
            }
        }
        stage('Build') {
            steps {
                sh 'cd $WORK_SPACE/docker-grang/mygrang && mvn clean package -Dmaven.test.skip=true'
                sh 'cd $WORK_SPACE/docker-grang/chatapp && mvn clean package -Dmaven.test.skip=true'
            }
        }
        stage('Run') {
            steps {
                sh '$WORK_SPACE/docker-grang && docker-compose up -d'
            }
        }
    }
}