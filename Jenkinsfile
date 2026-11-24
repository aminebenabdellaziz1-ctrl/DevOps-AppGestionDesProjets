
pipeline {
    agent any

    tools {
        jdk 'JAVA_HOME'
        maven 'M2_HOME'
    }

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
                    echo 'Compilation du Backend avec Maven'

                    sh 'mvn clean package -DskipTests'
                }
            }
        }

        stage('Tests Unitaires') {
            steps {
                dir('backend') {
                    echo 'Execution des tests unitaires'

                    sh 'mvn test'
                }
            }
        }

        stage('Creation du Livrable') {
            steps {
                echo 'Generation du livrable'

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
