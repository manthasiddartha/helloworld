echo "Welcome to Pipeline"
pipeline {
    agent any
	environment{ 
		dockerHome = tool 'myDocker'
		mavenHome = tool 'myMaven'
		PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"
	}
    stages { 
        stage('Build') {
            steps { 
               echo "Build"
			   echo "PATH -$PATH"
            }
        }
        stage('Test') {
            steps { 
                echo "Test"
            }
        }
		stage('Package') {
            steps { 
               echo "Started creating jar file"
			   sh "mvn clean install -DskipTests"
			   echo "Completed creating jar file"
            }
        }
		stage("Docker build") {
     		steps {
         		 sh "docker build -t helloworld ."
    		 }
			}
        stage("Deploy to staging") {
     		steps {
          sh "docker run -d --rm -p 8005:8005 --name helloworld_1 helloworld"
     }
		}
    }
}