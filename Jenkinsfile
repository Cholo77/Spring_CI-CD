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

        /*
        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('MySonar') {
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

        stage('Docker Login, Build & Push') {
            steps {
                // commandes Docker
            }
        }

        stage('Trivy Scan') {
            steps {
                // commandes Trivy
            }
        }

        stage('Deploy to Nexus') {
            steps {
                // commandes Nexus
            }
        }
        */
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
