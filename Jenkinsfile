
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
              // Download build.properties.json
              s3Download(file:'build.properties.json', bucket:'popsy-bucket', path:'Todo-rest-api-docker/build.properties.json', force:true)
              // Read Json values
              buildPropsJsonfile = readJSON file: 'build.properties.json', returnPojo: true              
              // Set global variables                           
              ACTIVE_COLOR=buildPropsJsonfile['ACTIVE_COLOR']
              TEST_COLOR=buildPropsJsonfile['TEST_COLOR']
              ACTIVE_ENVIRONMENTNAME=buildPropsJsonfile['ACTIVE_ENVIRONMENTNAME']              
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

                // CLEANUP
                script{
                  buildPropsJsonfile = readJSON file: 'build.properties.json', returnPojo: true
                  // SWAP ACTIVE AND TEST COLOR
                  buildPropsJsonfile['ACTIVE_COLOR']=TEST_COLOR
                  buildPropsJsonfile['TEST_COLOR']=ACTIVE_COLOR
                  buildPropsJsonfile['ACTIVE_ENVIRONMENTNAME']="NEW_ENV"
                  writeJSON file: 'build.properties.json', json: jsonfile
                  s3Upload(file:"build.properties.json", 
                    bucket:"popsy-bucket", 
                    path:"Todo-rest-api-docker/build.properties.json")
                }
            }
        }
    }
}
