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
                sh "./gradlew -D https.proxyHost=proxy1-rech.uphf.fr -D https.proxyPort=3128 test"
            }
        }

        stage("Jacoco") {
            steps {
                sh "./gradlew -D https.proxyHost=proxy1-rech.uphf.fr -D https.proxyPort=3128 jacocoTestReport"
            }
        }
        
        stage("SonarQube Analysis") {
            steps {
                    sh "./gradlew sonar -Dsonar.projectKey=TPControle -Dsonar.projectName='TPControle' -Dsonar.host.url=http://172.17.0.1:9000 -Dsonar.token=sqp_36d3626173346f154b67e71475556ca938909ef5"
            }
        }

        stage("Jar + Archive") {
            steps {
                sh '' 
                archiveArtifacts artifacts: '*.jar', fingerprint: true
            }
        }
    }
}
