pipeline {
    agent any
    
    triggers {
        pollSCM ('H/15 * * * *')
    }
    
    environment {
        APPLICATION_NAME = 'jenkins-docker-sonar-demo'
        TEMPLATE_NAME    = 'jenkinsdockersonardemo'
        DE_TAG           = 'beta'
      }

    stages {
        stage('Build') {
            steps {
                sh "mvn install -Dmaven.test.skip=true"
            }
        }
        stage('Scann Code') {
            steps {
                script {
                  sh "mvn sonar:sonar -Dsonar.host.url=http://172.26.0.4:9000 -DskipTests=true -Dsonar.projectKey=${APPLICATION_NAME} -Dsonar.projectName=${APPLICATION_NAME}"
                }
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}
