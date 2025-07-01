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
                sh 'git clone https://github.com/shubhshaky/pipeline.git'
            }
        }
        stage(build) {
            steps {
                sh '''
                docker build -t flaskapp:latest /var/lib/jenkins/workspace/automate/pipeline/.
                docker images
                '''
            }
        }
        stage(container) {
            steps {
                sh '''
                docker run -d --name mycon -p 5000:5000 flaskapp:latest
                docker ps
                sleep 10
                curl http://192.168.29.239:5000
                '''
            }
        }
    }
}
