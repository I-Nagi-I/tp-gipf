pipeline{
    agent any

    environment {
        SONARQUBE_SERVER = "TPControle"
        NO_PROXY="172.17.0.1"
    }

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
        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv("${SONARQUBE_SERVER}") {
                    sh "./gradlew sonar -Dsonar.projectKey=TPControle -Dsonar.projectName='TPControle' -Dsonar.host.url=http://172.17.0.1:9000 -Dsonar.token=sqp_36d3626173346f154b67e71475556ca938909ef5"
                }
            }
        }
    }
}
