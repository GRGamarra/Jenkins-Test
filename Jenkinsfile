pipeline {
    agent { label 'built-in' }
    stages {
        stage('Build') {
            steps {
                echo "Building..."
                sh '''
                echo "Pulling from the repository and compiling with Maven"
                '''
                script {
                    docker.image('java-base').inside{
                        git branch: 'main', changelog: false, poll: false, url: 'https://github.com/GRGamarra/Jenkins-Test'
                        sh '''
                        ./mvnw install
                        '''
                    }
                }
            }
        }
        stage('Test') {
            steps {
                echo "Testing.."
                sh '''
                echo "TODO: run the jar file and do a curl, to then compare the returning phrase with <Hello World!>"
                '''
            }
        }
        stage('Deliver') {
            steps {
                echo 'Deliver....'
                sh '''
                echo "using the docker.sock bind in order to build an image with the jar"
                '''
                sh '''
                echo "FROM openjdk:17-jdk-alpine\n WORKDIR /app\n COPY target/*.jar ./java.jar\n EXPOSE 8090\n CMD [\\"java\\",\\"-jar\\",\\"java.jar\\"]" > Dockerfile
                
                docker rm -f java-app-server | true
                docker rmi java-app | true
                '''
                script {
                    docker.build("java-app")
                    docker.image("java-app").run("-p 8090:8090 --name java-app-server")
                }
            }
        }
    }
}