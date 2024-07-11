pipeline{
    agent any
    environment {
    //FIREBASE_DEPLOY_TOKEN = credentials('firebase-token')
    TOKENAWS = credentials('ssh-production-key')
    }

stages{
        stage('Building'){
            steps{
           // sh 'npm install -g firebase-tools'
                echo 'Biulding...'
            }
        } 
        stage('Testing Environment'){
            steps{
            //sh 'firebase deploy -P testing-fc065 --token "$FIREBASE_DEPLOY_TOKEN"'
            //input message: 'After testing. Do you want to continue with Staging Environment? (Click "Proceed" to continue)'
            sh 'ssh -T -oStrictHostKeyChecking=no -i "$TOKENAWS" ec2-user@54.92.214.159 " sudo dnf update; sudo dnf install git -y; sudo dnf install -y httpd; sudo systemctl start httpd; sudo rm -Rf /var/www/html/; sudo git clone https://github.com/CRISADRY/Kelownatrails-master.git /var/www/html"'
            }
        } 
        stage('Staging Environment'){
            steps{
            //sh 'firebase deploy -P staging-5c403 --token "$FIREBASE_DEPLOY_TOKEN"'
            
            sh 'ssh -T -oStrictHostKeyChecking=no -i "$TOKENAWS" ec2-user@54.242.101.217 " sudo dnf update; sudo dnf install git -y; sudo dnf install -y httpd; sudo systemctl start httpd; sudo rm -Rf /var/www/html/; sudo git clone https://github.com/CRISADRY/Kelownatrails-master.git /var/www/html"'
            }
        } 
        stage('Production Environment'){
            steps{
            //sh 'firebase deploy -P deploy-e3831 --token "$FIREBASE_DEPLOY_TOKEN"'
            sh 'ssh -T -oStrictHostKeyChecking=no -i "$TOKENAWS" ec2-user@18.215.165.114 " sudo dnf update; sudo dnf install git -y; sudo dnf install -y httpd; sudo systemctl start httpd; sudo rm -Rf /var/www/html/; sudo git clone https://github.com/CRISADRY/Kelownatrails-master.git /var/www/html"'
            }
        } 
    }

}
