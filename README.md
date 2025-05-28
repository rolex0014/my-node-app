Launch an Ec2 instance with required pre-requisites.
After launching , install jenkins with latest version of java other wise you will get error.
Install git.
Get node.js sample code from google or somewhereelse.
In Jenkins,create a job with job name and select pipeline.
Go to configure and write a declarative pipeline to get code,build,deploy.
pipeline {
    agent any

    stages {
        stage('Code') {
            steps {
                git 'https://github.com/rolex0014/my-node-app.git'
            }
        }
        stage('Build') {
            steps {
                sh 'docker build -t $image:$tag html'
            }
        }
        stage('Deploy') {
            steps {
                sh 'docker run -itd --name $name -p $port:80 $image:$tag'
            }
        }
    }
}

In pipeline i use build with parameters option y because if you run code for the second time you will get error like container already existed.Again you have to open configure and u have to change container name.so,this is the reason i used BUILD WITH PARAMETERS.


