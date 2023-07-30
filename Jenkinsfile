s3Download(file:'build.properties', bucket:'popsy-bucket', path:'Todo-rest-api-docker/build.properties', force:true)
def props = readProperties  file:'build.properties'
def ACTIVE_COLOR= props['ACTIVE_COLOR']
def ACTIVE_ENVIRONMENTNAME= props['ACTIVE_ENVIRONMENTNAME']


pipeline {
    agent any
    options {
    	withAWS(profile:'default')
    }
    environment {
        PATH="/usr/local/bin:$PATH"
        DOCKER_HUB_CREDENTIALS= credentials('DOCKER_HUB_CREDENTIALS')     
    }
    parameters {      
    }
    stages {
        stage('Build') {
            steps {
                echo "BUILD"   
                echo "ACTIVE_COLOR=${ACTIVE_COLORs}"
                echo "ACTIVE_ENVIRONMENTNAME=${ACTIVE_ENVIRONMENTNAME}"
            }
        }
        stage('Test') {
            steps {
                echo "Test"
            }            
        }
        
        stage('Complete') {
            steps {
                echo 'Job Complete!'
            }
        }
    }
}
