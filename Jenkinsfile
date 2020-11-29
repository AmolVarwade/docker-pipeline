	node {
    def app

    stage('Clone repository') {
        /* Cloning the Repository to our Workspace */

        checkout scm
    }

    stage('Build Image') {
        /* This builds the actual image */

        app = docker.build("amolv105/webdemo")
    }
		
    stage('Deploy Image') {
        docker.withRegistry('https://registry.hub.docker.com', 'docker-hub') {
	 sh "docker push amolv105/webdemo:latest"
	   // app.push("${env.BUILD_NUMBER}")
            //app.push("latest")
            } 
                echo "Trying to Push Docker Build to DockerHub"
    }
		
    stage('Remove Image') {
	    steps{
		   sh "docker rmi amolv105/latest"
    }	
		
stage('Execute Image ') {
	sh "docker pull amolv105/webdemo:latest"
	sh "docker run -d -p8000:8000 amolv105/webdemo"
	}
    }
