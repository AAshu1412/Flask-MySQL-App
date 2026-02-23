pipeline{

agent {label "dev"};

    stages{

        stage("code"){

             steps{

                       git url: "https://github.com/AAshu1412/Flask-MySQL-App", branch:"main"

                    }

                }

        stage("build"){

                steps{
                    
                        sh "docker build -t flask-webby ."

                    }

                }

        stage("test"){

                steps{

                        echo "test the project"

                }

        }
        stage("Push to docker hub"){

                steps{
                        withCredentials([usernamePassword(
                            credentialsId:"dockerhubCreds",
                            passwordVariable:"dockerhubPass",
                            usernameVariable:"dockerhubUser")]) {
                                
                                sh "docker login -u ${env.dockerhubUser} -p ${env.dockerhubPass}"    
                                sh "docker image tag flask-webby ${env.dockerhubUser}/flask-webby"    
                                sh "docker push ${env.dockerhubUser}/flask-webby:latest"
                                
                        }
                }

        }
        stage("deploy"){

                steps{

                             sh "docker compose up -d --build flask-app"

                }

        }

    }

        post {
                success{
                        emailext subject:"Build Successful",
                                  body:"Good News",
                                  to: "ashutoshsanjeevmittal@gmail.com"
                        
                }
                failure{
                        emailext subject:"Build Successful",
                                  body:"Bad News",
                                  to: "ashutoshsanjeevmittal@gmail.com"
                        
                }
        }
}