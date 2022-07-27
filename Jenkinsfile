pipeline{
  
  agent any
  
  stages{
    
     stage ('Setup parameters'){
        steps{
          script{
            properties([
                      parameters([
                          string(defaultValue: '/var/lib/jenkins/workspace/Pipeline_Job1_Frontend_Descriptive/DockerDirectory/Dockerfile', name: 'PATH_TO_DOCKERFILE', description: ''),
                          string(defaultValue: 'frontend_img', name: 'IMAGE_NAME', description: ''),
                          string(defaultValue: 'frontend_cont', name: 'CONTAINER_NAME', description: ''),
                          choice(choices: ['3000', '3001', '3002'], name: 'PORT')
                      ])
                  ])

          }
        }
      }
    
    stage('GetSourceCode'){
        steps{        
          dir('source_code'){
              git url: 'https://github.com/aditya-sridhar/simple-reactjs-app.git', branch: 'master'

              sh 'rm -r .git'
          }
        }
      
    }
    
  }
  
}
