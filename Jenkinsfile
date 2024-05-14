pipeline {
    agent any
        stages {
            stage('Build') {
            steps {
            sh 'mvn -B -DskipTests clean package'
            }
            }
            stage('pmd') {
            steps {
            sh 'mvn pmd:pmd'
            }
        }
        stage('Javadoc') {
            steps {
                sh 'mvn javadoc:jar'
            }
            post {
                always {
                    archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true
                }
            }
        }
        stage('Test Report') {
            steps {
                sh 'mvn test surefire-report:report -Dmaven.test.failure.ignore=true'

            }
            post {
                always {
                    archiveArtifacts artifacts: '**/target/surefire-reports/**/*.xml', fingerprint: true
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
