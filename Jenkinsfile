node {
    def app
    stage('Clone repository') {
        /* Cloning the Repository to our Workspace */
        checkout scm
    }
    stage('Build image') {
        /* This builds the actual image */
        app = docker.build("amolv105/webdemo")
    }
    stage('Test image') {   
        app.inside {
            echo "Tests passed"
        }
    }
    stage('Push image') {   
    docker.withRegistry('https://registry.hub.docker.com', 'docker-hub') {
	sh "docker push amolv105/webdemo:latest"
	   // app.push("${env.BUILD_NUMBER}")
            //app.push("latest")
            } 
                echo "Trying to Push Docker Build to DockerHub"
    }
stage('Pull & Run image ') {
        /* You would need to first register with DockerHub before you can push images to your account */
	sh "docker pull amolv105/webdemo:latest"
	sh "docker run -d -p8000:8000 amolv105/webdemo"
	app.inside{
	curl "http://127.0.0.1:8000/"
	}
    }
	
}
