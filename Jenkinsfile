pipeline{
    agent any

	environment {
		DOCKERHUB_CREDENTIALS=credentials('dockerhublogin')
	}

	stages {
	    
	    stage('gitclone') {

			steps {
				git 'https://github.com/BharathSharath/spring-boot-mongodb-react-crud.git'
			}
		}

		stage('Build') {

			steps {
				sh 'docker build -t bharathsharath/frontend ./frontend'
				sh 'docker build -t bharathsharath/backend ./backend'
			}
		}

		stage('Login & Push ') {

			steps {
				sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
				sh 'docker push bharathsharath/frontend'
				sh 'docker push bharathsharath/backend'
				sh 'docker rmi bharathsharath/frontend bharathsharath/backend'
			}
		}
    
        stage('Deploy on K8s ') {
            steps {
                sshagent(['k8s']) {
                sh "scp -o StrictHostKeyChecking=no deploy-svc.yml ubuntu@172.31.11.65:/home/ubuntu"
                script {
                      sh "ssh ubuntu@172.31.11.65 kubectl apply -f deploy-svc.yml"
                    }
                }    
            }
        }
        
    }
}
