pipeline {
    agent { label 'docker-label' }
    tools {
        maven "M3"
    }
    stages {
        stage('Build') {
            steps {
                git branch: 'main', url: 'https://github.com/bbitinsight/sync.git'
                //sh "mvn -Dmaven.test.failure.ignore=true -s settings.xml clean install"
                sh "mvn clean verify sonar:sonar -Dsonar.projectKey=sync -Dsonar.host.url=http://18.222.169.237:9000 -Dsonar.login=sqp_4e103df3de1783de43368689d22a29df7aeeabe3"
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
