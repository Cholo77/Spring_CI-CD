pipeline {
    agent any

    tools {
        jdk 'jdk17'      // Assure-toi que ce nom correspond à ta config Jenkins JDK
        maven 'maven3'   // Pareil pour Maven
    }

    environment {
        // Tu peux aussi définir JAVA_HOME explicitement ici si besoin
        // JAVA_HOME = '/usr/lib/jvm/java-17-openjdk-amd64'
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

        stage('Docker Login, Build & Push') {
            steps {
                // tes commandes docker ici
            }
        }

        stage('Trivy Scan') {
            steps {
                // tes commandes trivy ici
            }
        }

        stage('Deploy to Nexus') {
            steps {
                // tes commandes déploiement ici
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
