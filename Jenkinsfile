pipeline {
    agent any
    stages {
        stage('Pull latest Code') { 
             steps {
              // Get some code from a GitHub repository
              git 'https://github.com/mahoudabdelfattah/DockerPiplineTest.git'
             }
        }
		stage('spinning up docker images'){
        	steps {
                	bat 'docker-compose up' 
             }	
        }
     
        stage('Build') { 
            steps {
                bat 'mvn -B -DskipTests clean package' 
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
        stage('Destroy - After Running tests on Containers') { 
            steps {
                bat 'docker stop $(docker ps -a -q)'
                bat 'docker rm $(docker ps -a -q)'
            }
        }
    }
}
