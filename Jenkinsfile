pipeline {
    agent any

    stages {
        stage('Build and Run Hello World Docker Container') {
            steps {
                script {
                    // Pull a Docker image (if needed)
                    docker.image('hello-world').pull()

                    // Run the Hello World Docker container
                    def helloContainer = docker.image('hello-world').run()

                    // Wait for the container to exit (optional)
                    helloContainer.wait()

                    // Clean up the container (optional)
                    helloContainer.stop()
                    helloContainer.remove()
                }
            }
        }
    }
}
