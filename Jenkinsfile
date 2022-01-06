pipeline {
    agent any
    
environment {
        Git_Url = 'https://github.com/profojah/MyProject.git'
        Tomcat_Url = 'http://3.82.92.221:8080/'
        Tomcat_Cred = 'a8ea9772-4b03-4102-bce2-d3b57ac46846'
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
        stage('Deploy with Tomcat') {
            steps {
               deploy adapters: [tomcat9(credentialsId: "${Tomcat_Cred}", 
               path: '', 
               url: "${Tomcat_url}")], 
               contextPath: 'webapp', 
               war: '**/*.war'
            }
        }
    }
}
