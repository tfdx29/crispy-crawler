pipeline {
    agent any
 
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
 
        stage('Crawl Website') {
            steps {
                script {
                    // Pull the Docker image
                    docker.image('algolia/docsearch-scraper').pull()
                    
                    // Run the scraper inside the Docker container
                    def scraper = docker.image('algolia/docsearch-scraper').run('-u', 'https://sameer-jsohi.com.np')
                    
                    // Wait for the container to finish
                    def exitCode = scraper.wait()
                    
                    // Check the exit code
                    if (exitCode == 0) {
                        currentBuild.result = 'SUCCESS'
                    } else {
                        currentBuild.result = 'FAILURE'
                    }
                }
            }
        }
    }
 
    post {
        success {
            echo 'Website crawl successful!'
        }
        failure {
            echo 'Website crawl failed!'
        }
    }
}
