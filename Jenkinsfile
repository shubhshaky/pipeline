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
        
        stage(build) {
            steps {
                sh '''
                docker build -t flask:latest /var/lib/jenkins/workspace/automate/pipeline/.
                docker images
                '''
            }
        }
        
        stage(run) {
            steps {
                sh '''
                docker run -d --name flaskapp -p 5000:5000 flask:latest
                docker ps
                '''
            }
        }
        
        stage(content) {
            steps {
                sh '''
                sleep 10
                curl http://192.168.29.239:5000
                '''
            }
        }
        
        stage(login) {
            steps {
                withCredentials([usernamePassword(credentialsId: 'DOCKER_HUB', usernameVariable: 'USER', passwordVariable: 'PASS')]) {
                    sh 'echo $PASS | docker login -u $USER --password-stdin'
                }
            }
        }
        
        stage(push) {
            steps {
                sh '''
                docker tag flask:latest shubhshaky/pubrepo:flask
                docker push shubhshaky/pubrepo:flask
                '''
            }
        }
    }
    post {
        failure {
            echo 'failure build'
        }
        
        success {
            echo 'success project'
        }
    }
}
