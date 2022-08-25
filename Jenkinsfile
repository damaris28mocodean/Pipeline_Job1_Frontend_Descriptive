pipeline{
  
   agent {
      label 'master'
  }
  
  environment {
		    DOCKERHUB_CREDENTIALS=credentials('access-token-docker')
	}

  stages{
    
     stage ('Setup parameters'){
        steps{
          
          script{
            
            properties([
                      parameters([  
                          string(defaultValue: '/var/lib/jenkins/workspace/Pipeline_Job1_Frontend_Declarative/DockerDirectory/Dockerfile', name: 'PATH_TO_DOCKERFILE', description: ''),
                          string(defaultValue: 'damy28/frontend_repo', name: 'IMAGE_NAME', description: ''),
                          string(defaultValue: 'frontend_cont', name: 'CONTAINER_NAME', description: ''),
                          choice(choices: ['3000', '3001', '3002'], name: 'PORT')
                      ])
                  ])
          }
          
        }
       
     }
    
     /*stage('Preparation'){
        
      steps{
        
          sh '''docker stop ${CONTAINER_NAME}
          docker rm ${CONTAINER_NAME}
          '''
          //sh "a=1 && val=`expr $BUILD_NUMBER - $a` && docker image rm ${IMAGE_NAME}:${val}"
        
      }
      
    }*/
    
    stage('GetSourceCode'){
        steps{
          
          dir('source_code'){
            
              git url: 'https://github.com/aditya-sridhar/simple-reactjs-app.git', branch: 'master'

              sh 'rm -r .git'
            
          }
          
       }
      
    }
    
    stage('Build'){
      
      steps{
        
        dir('source_code'){
          
            sh "docker build --tag ${IMAGE_NAME}:${BUILD_NUMBER} --build-arg PORT_NUMBER=${PORT} -f ${PATH_TO_DOCKERFILE} ."
            
        }
        
      }
      
    }

    stage('Login to DockerHub') {

        steps {
          sh "echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin"
        }

		}

    stage('Push') {

        steps {
          sh "docker push ${IMAGE_NAME}:${BUILD_NUMBER}"
        }
		}
    
    /*stage('Deploy'){
      steps{
        
          sh "docker run --name ${CONTAINER_NAME} -d -p ${PORT}:${PORT} ${IMAGE_NAME}:${BUILD_NUMBER}"
        
      }
      
    }*/
    
  }

  post {

      always {

          sh "docker logout"

      }

	}
  
}
