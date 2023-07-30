
def ACTIVE_COLOR = ''
def ACTIVE_ENVIRONMENTNAME = ''
def TEST_COLOR = ''

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
              def buildProps = readProperties  file:'build.properties'              
              ACTIVE_COLOR=buildProps['ACTIVE_COLOR']
              TEST_COLOR=buildProps['TEST_COLOR']
              ACTIVE_ENVIRONMENTNAME=buildProps['ACTIVE_ENVIRONMENTNAME']              
            }
            
          }
        }
        stage('Build') {
            steps {
                echo "BUILD"   
                echo "ACTIVE_COLOR=${ACTIVE_COLOR}"
                echo "ACTIVE_ENVIRONMENTNAME=${ACTIVE_ENVIRONMENTNAME}"
                echo "TEST_COLOR=${TEST_COLOR}"
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
