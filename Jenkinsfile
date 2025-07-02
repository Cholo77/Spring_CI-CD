pipeline {
    agent { label 'aws-agent' }

    tools {
        jdk 'jdk17'
        maven 'maven3'
    }

    environment {
        JAVA_HOME = '/usr/lib/jvm/java-17-openjdk-amd64'
    }

    stages {
        stage('Test Env') {
            steps {
                sh 'echo "JAVA_HOME=$JAVA_HOME"'
                sh 'ls -l $JAVA_HOME'
                sh 'java -version'
            }
        }

        stage('Build & Test') {
            steps {
                sh 'mvn clean package -B'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('sonarqube') {
                    sh 'mvn sonar:sonar'
                }
            }
        }

        stage('Quality Gate') {
            steps {
                timeout(time: 1, unit: 'HOURS') {
                    waitForQualityGate abortPipeline: true
                }
            }
        }

        // Tu pourras ajouter plus tard les stages Docker, Trivy, Nexus, etc.
    }

    post {
        success {
            echo '✅ Pipeline réussi'
        }
        failure {
            echo '❌ Pipeline échoué'
        }
    }
}
