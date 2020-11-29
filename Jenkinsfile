node {
environment{
registry = "AmolVarwade/docker-pipeline"
}
    def app
    stage('Clone repository') {
        /* Cloning the Repository to our Workspace */
        checkout scm
    }
    stage('Build Image') {
        /* This builds the actual image */
        app = docker.build registry + ":$BUILD_NUMBER"
    }
    
    stage('Deploy Image') {   
    	docker.withRegistry('https://registry.hub.docker.com', 'docker-hub') {
	//sh "docker push amolv105/webdemo:latest"
	    app.push("${env.BUILD_NUMBER}")
            //app.push("latest")
            } 
                echo "Trying to Push Docker Build to DockerHub"
    }
    stage('Remove Image ') {   
        steps{
            sh "docker rmi $registry:$BUILD_NUMBER"
        }
    }
stage('Execute Image ') {
        /* You would need to first register with DockerHub before you can push images to your account */
	sh "docker pull amolv105/webdemo:latest"
	sh "docker run -d -p8000:8000 amolv105/webdemo"
	def appImage = docker.build("AmolVarwade/docker-pipeline:${env.BUILD_NUMBER}")
	appImage.inside{
		sh 'http://127.0.0.1:8000/'
	}
	
    }
}
