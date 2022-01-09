pipeline {
    agent any
    
environment {
        Git_Url = 'https://github.com/profojah/MyProject.git'
        Tomcat_Url = 'http://3.234.223.144:8080/'
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
              rtUpload (
                    serverId: 'Olu-Jfrog',
                    spec: '''{
                        "files": [
                            {
                            "pattern": "**/*.war",
                            "target": "Ojah-repo/"
                            }
                        ]
                    }''',
                )
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
