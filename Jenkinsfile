import org.jenkinsci.plugins.docker.workflow.Docker
pipeline {
    agent {
        node{
            label 'CloudComponent'
        }
    }

    stages {
        stage('Demotest 1') {
            steps {
                echo 'Demo test checking..'
            }
        }
       stage('ChangeLog') {
            steps {
                echo 'ChangeLog..'
            }
       }
        stage('Repo') {
            steps {
                echo 'Repo Testing..'
            }
        }
        stage('Upload a file to an artifactory') {
            steps {
                script {
                echo 'Deploying....'
                echo "TimeStamp: ${currentBuild.startTimeInMillis}"
                writeFile file: 'test_Dinesh.txt', text: 'Working with files the Groovy way is easy. latest build:' 
                
                def uploadSpec = """{
                    "files": [
                        {
                            "pattern": "test_Dinesh.txt",
                            "target": "public/test/"
                        }
                    ]
                }"""
                def server = Artifactory.newServer url: 'https://artifact.swf.daimler.com:443/artifactory', username: 's1snaris', password: '**********'
                artifactoryUpload(spec: uploadSpec, server: server, failNoOp: true)
                }
            }
        }
        stage('Pulling DockerImage') {
            steps {
                script {
                    echo 'Docker Image Testing..'
                    docker.image('apricot-docker/qnx-environment/0.1/sha256__5f618014e314424661eb97f36fc83b63d8c18ff1c57c571c8ae9728cb3aa46b7')
                }
            }
        }
    }
}