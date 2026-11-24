
pipeline {
    agent any

    triggers {
        pollSCM('H/2 * * * *')
    }

    stages {

        stage('Checkout') {
            steps {
                echo 'Recuperation du projet depuis GitHub'
                checkout scm
            }
        }

        stage('Build Backend') {
            steps {
                dir('backend') {
                    echo 'Compilation du Backend'
                    sh 'mvn clean package -DskipTests'
                }
            }
        }

        stage('Livrable') {
            steps {
                echo 'Archivage du fichier JAR'

                archiveArtifacts(
                    artifacts: 'backend/target/*.jar',
                    fingerprint: true
                )
            }
        }
    }

    post {
        success {
            echo 'Pipeline executee avec succes!'
        }

        failure {
            echo 'Echec de la Pipeline!'
        }
    }
}
