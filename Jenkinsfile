pipeline {
    agent any
    
environment {
        Git_Url = 'https://github.com/profojah/MyProject.git'
        Tomcat_Url = 'http://3.234.223.144:8080/'
       Jfrog_Url = 'http://54.236.32.117:8082/artifactory'
       My_Pass = 'Palynologist1.'
    }

    stages {
        stage('Git Checkout') {
            steps {
                git "${Git_url}"
            }
        }
        stage('Test with Maven') {
            steps {
                sh 'cd SampleWebApp && mvn clean install -Dbuild.number=${build_number}'
            }
        }
        stage('Deploy to Jfrog') {
            steps {
                            rtServer (
                    id: 'Olu-Jfrog',
                    url: "${Jfrog_url}",
                    username: 'admin',
                    password: "${My_pass}",
                )
            }
        }
        stage('Deploy with Jfrog') {
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
