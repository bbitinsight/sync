pipeline {
    agent { label 'docker-label' }
    tools {
        maven "M3"
    }
    stages {
        stage('Build') {
            steps {
                git branch: 'main', url: 'https://github.com/bbitinsight/sync.git'
                sh "mvn -Dmaven.test.failure.ignore=true -s settings.xml clean deploy"
            }
            post {
                success {
                    junit '**/target/surefire-reports/TEST-*.xml'
                    archiveArtifacts 'target/*.jar'
                }
            }
        }
    }
}
