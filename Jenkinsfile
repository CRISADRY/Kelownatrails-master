pipeline{
    agent any
    environment {
    FIREBASE_DEPLOY_TOKEN = credentials('firebase-token')
    }

 stages{
        stage('Building'){
            steps{
           // sh 'npm install -g firebase-tools'
                echo 'Biulding...'
                //
            }
        } 
        stage('Checkout') {
            steps {
                git branch: 'main', credentialsId: 'CRISADRY', url: 'https://github.com/CRISADRY/Kelownatrails-master.git'
            }
        }
        stage('Testing Environment'){
            steps{
            sh 'firebase deploy -P testing-fc065 --token "$FIREBASE_DEPLOY_TOKEN"'
            input message: 'After testing. Do you want to continue with Staging Environment? (Click "Proceed" to continue)'
            }
        } 
        stage('Staging Environment'){
            steps{
             sh 'firebase deploy -P staging-5c403 --token "$FIREBASE_DEPLOY_TOKEN"'
            }
        } 
        stage('Production Environment'){
            steps{
            sh 'firebase deploy -P deploy-e3831 --token "$FIREBASE_DEPLOY_TOKEN"'
            }
        } 
    }

}
