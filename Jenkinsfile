pipeline{
  
  agent any
  
  stages{
    
    stage ('Create source_code'){
      steps{
        sh "mkdir source_code"
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
