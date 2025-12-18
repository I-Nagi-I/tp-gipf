pipeline{
    agent any

    stages{
        stage('Checkout') {
            steps {
              checkout scm
            }
        }

        stage('Compilation') {
            steps{
              sh '
