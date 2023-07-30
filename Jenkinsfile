
def ACTIVE_COLOR
def ACTIVE_ENVIRONMENTNAME

pipeline {
    agent any
    options {
    	withAWS(profile:'default')
    }
    environment {
        PATH="/usr/local/bin:$PATH"
        DOCKER_HUB_CREDENTIALS= credentials('DOCKER_HUB_CREDENTIALS')     
    }
    stages {
      stage('initialize') {
          steps {
            script {
              s3Download(file:'build.properties', bucket:'popsy-bucket', path:'Todo-rest-api-docker/build.properties', force:true)
              props = readProperties  file:'build.properties'
              ACTIVE_COLOR= props['ACTIVE_COLOR']
              ACTIVE_ENVIRONMENTNAME= props['ACTIVE_ENVIRONMENTNAME']
            }
            
          }
        }
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
