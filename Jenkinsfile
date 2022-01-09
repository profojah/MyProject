pipeline {
    agent any
    
environment {
        Git_Url = 'https://github.com/profojah/MyProject.git'
        Tomcat_Url = 'http://3.80.142.23:8080/'
        Jfrog_Url = 'http://54.236.32.117:8082'
    }

    stages {
        stage('Git Checkout') {
            steps {
                git "${Git_url}"
            }
        }
        stage('Test with Maven') {
            steps {
                sh 'cd SampleWebApp && mvn clean install'
            }
        }
         stage('Deploy to Jfrog') {
            steps {
                rtServer (
                id: 'Olu-Jfrog',
                url: "${Jfrog_url}"/artifactory',
                username: 'admin',
                password: 'Palynologist1.',
            }
        }
        stage('Deploy with Tomcat') {
            steps {
               deploy adapters: [tomcat9(credentialsId: 'tomcat-id', 
               path: '', 
               url: "${Tomcat_url}")], 
               contextPath: 'webapp', 
               war: '**/*.war'
            }
        }
    }
}
