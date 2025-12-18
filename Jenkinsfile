pipeline{
    agent any

    stages{
        stage('Checkout') {
            steps {
              checkout scm
            }
        }

        stage ("Compilation") {
            steps {
                sh "./gradlew -D https.proxyHost=proxy1-rech.uphf.fr -D https.proxyPort=3128 compileJava"
            }
        }

        stage("Test") {
            steps {
                sh "./gradlew test"
            }
        }

        node {
          stage('SonarQube Analysis') {
            withSonarQubeEnv() {
                sh "./gradlew sonar"
            }
          }
        }
    }
}
