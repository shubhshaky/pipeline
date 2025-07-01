pipeline {
    agent any
    
    stages {
        stage(clean) {
            steps {
                deleteDir()
            }
        }
        stage(clone) {
            steps {
                sh '''
                git clone https://github.com/shubhamkoli03/pipeline.git
                pwd
                cd pipeline
                ls
                '''
            }
        }
        stage(image) {
            steps {
                sh '''
                docker build -t flask:latest /var/lib/jenkins/workspace/automate/pipeline/.
                docker images
                '''
            }
        }
        stage(container) {
            steps {
                sh '''
                docker run -d --name mycon -p 5000:5000 flask:latest
                docker ps 
                '''
            }
        }
        stage(curl) {
            steps {
                sh '''
                sleep 10
                curl http://192.168.29.239:5000
                '''
            }
        }
    }
}
