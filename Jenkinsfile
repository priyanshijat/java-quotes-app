pipeline {
    agent any;
    stages{
        stage("clone"){
            steps{
                git url: "https://github.com/priyanshijat/java-quotes-app.git", branch: "master"
            }
        }
        stage("build"){
            steps{
                sh "docker build -t java-image ."
            }
        }
        stage("push to dockerhub"){
            steps{
                withCredentials([usernamePassword(
                    credentialsId: "dockercreds",
                    usernameVariable: "dockerHubUser",
                    passwordVariable: "dockerHubPass")]){
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker image tag java-image ${env.dockerHubUser}/java-image-app"
                sh "docker push ${env.dockerHubUser}/java-image-app"
                }
            }
        }
        stage("test"){
            steps{
                echo "test developer krega......"
            }
        }
        stage("deploy"){
            steps{
                sh "docker run -p 8000:8000 java-image"
            }
        }
    }
}
