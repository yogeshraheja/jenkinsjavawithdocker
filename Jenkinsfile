pipeline {
    agent any
    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "mvn1"
    }
   stages {
        stage('Build') {
            steps {
                // Get some code from a GitHub repository
                git branch: 'main', url: 'https://github.com/yogeshraheja/jenkinsjavawithdocker.git'

                // Run Maven on a Unix agent.
                sh "mvn clean package"
            }

            post {
                success {
                    archiveArtifacts 'target/*.war'
                }
            }
        }
        stage('DockerBuild'){
            steps{
                sh "docker image build -t webapp -f docker ."
            }
        }
        stage('DockerContainer'){
            steps{
                 sh "docker container run -d -p 30013:8080 webapp"
            }
        }
    }
}

