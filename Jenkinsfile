pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                bat 'mvn -B -DskipTests clean package'
            }
        }
        stage('pmd') {
            steps {
                bat 'mvn pmd:pmd'
            }
        }
        stage('Test') {
            steps {
                bat 'mvn test'
            }
        }
        stage('Generate Surefire Report') {
            steps {
                bat 'mvn surefire-report:report'
            }
            post {
                always {
                    archiveArtifacts artifacts: '**/target/site/surefire-report.html', fingerprint: true
                }
            }
        }
        stage('Generate Javadoc') {
            steps {
                bat 'mvn javadoc:jar'
            }
            post {
                always {
                    archiveArtifacts artifacts: '**/target/apidocs/**/*.jar', fingerprint: true
                }
            }
        }
    }
  
    post {
        always {
            archiveArtifacts artifacts: '**/target/site/**', fingerprint: true
            archiveArtifacts artifacts: '**/target/**/*.jar', fingerprint: true
            archiveArtifacts artifacts: '**/target/**/*.war', fingerprint: true
        }
    }
}
