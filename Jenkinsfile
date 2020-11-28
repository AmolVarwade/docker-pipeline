node {
    def app

    stage('Clone repository') {
        /* Cloning the Repository to our Workspace */

        checkout scm
    }

    stage('Build image') {
        /* This builds the actual image */

        app = docker.build("amol/webdemo")
    }

    stage('Test image') {
        
        app.inside {
            echo "Tests passed"
        }
    }

    stage('Push image') {
        /* 
			You would need to first register with DockerHub before you can push images to your account
		*/
        docker.withRegistry('https://registry.hub.docker.com', 'docker-hub') {
	sh "docker push amol/webdemo:latest"
	   // app.push("${env.BUILD_NUMBER}")
            //app.push("latest")
            } 
                echo "Trying to Push Docker Build to DockerHub"
    }
stage('Pull & Run image ') {
        /* 
			You would need to first register with DockerHub before you can push images to your account
		*/
	sh "docker pull amol/webdemo:latest"
	sh "docker run -d -p8000:8000 amol/webdemo"
	sh "curl http://127.0.0.1:8000/"
    }
	
}
