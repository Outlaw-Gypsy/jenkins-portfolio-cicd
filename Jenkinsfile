pipeline {

    agent any

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
				url: 'https://github.com/Outlaw-Gypsy/jenkins-portfolio-cicd'
            }
        }

        stage('Build') {
            steps {
                echo 'Checking downloaded files'
		sh 'ls -la'
		sh 'ls -la html'
            }
        }

        stage('Install Dependencies') {
            steps {
                echo 'Dependencies step completed: Nginx already installed'
            }
        }

        stage('Run Application') {
            steps {
                echo 'Deployment stage will come next'
            }
        }

    }
}
