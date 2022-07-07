pipeline{
    agent any
	environment{
		dockerhub=credentials('dockerhub')
	}
    stages{
        stage('Code checkout'){
            steps{
                // Get the code checkout to jenkins workspace
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/com-satya/dockerize_springboot.git']]])
            }
        }
        stage('Build maven'){
            steps{
                script{
                    withMaven(maven: 'Maven3') {
                     sh 'java --version'        
                     sh 'mvn --version'
                     sh 'mvn clean compile install'
                }
                    
                }
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t satyainv459/docker-jenkins:1.0 .'
                }
            }
        }
        stage('Push docker images'){
            steps{
                sh 'echo $dockerhub_PSW | docker login -u $dockerhub_USR --password-stdin'
                 sh 'docker push satyainv459/docker-jenkins:1.0 '
             }
            
        }
    }
}
