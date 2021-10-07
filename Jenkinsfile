pipeline{
    agent any
    
    environment {
        dotnet ='C:\\Program Files (x86)\\dotnet\\'
        }
        
    triggers {
        pollSCM 'H * * * *'
    }
 }
tages{
 stage('Checkout') {
    steps {
     git credentialsId: 'asp' , url: 'https://github.com/Sandeep0045/sample-dot-net-code.git', branch: 'master'
     }
  }
  stage('Restore packages'){
    steps{
      bat "dotnet restore "
     }
  }
  stage('Clean'){
    steps{
        bat "dotnet clean "
     }
   }
  stage('Build'){
    steps{
      bat "dotnet build "
    }
 }
  stage('Test: Unit Test'){
    steps {
      bat "dotnet test"
     }
  }
       
  stage('Test: Integration Test'){
    steps {
       bat "dotnet test"
      }
   }
  
  stage('Publish'){
    steps{
      bat "dotnet publish "
     }
}
  
  
