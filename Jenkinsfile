pipeline {
    agent any

    tools {
        jdk 'jdk17'      // Assure-toi que ce nom correspond bien à ta config Jenkins (JDK)
        maven 'maven3'   // Idem pour Maven
    }

    environment {
        JAVA_HOME = '/usr/lib/jvm/java-17-openjdk-amd64'  // Chemin JAVA_HOME sur ton agent
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
        // Décommente ces stages quand tu auras configuré SonarQube, Docker, Trivy, Nexus
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
