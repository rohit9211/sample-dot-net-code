pipeline {
    agent any
     triggers {
        githubPush()
      }
    stages {
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
      
      stage('Sonar Analysis'){
         steps {
             bat''' dotnet sonarscanner /k:"ASPDOTNET"  /d:sonar.login="d21386517e6e82d1d5ffd90551314f30a6d76215" /d:sonar.host.url="http://34.89.172.47:9000/"
                    dotnet build WebAppRazor.sln 
                    dotnet sonarscanner end /d:sonar.login="d21386517e6e82d1d5ffd90551314f30a6d76215"
                '''    
                 
      }
   }  
  
     stage('Publish'){
        steps{
            bat "dotnet publish" 
     }
}
        
        
        
     stage('Push to Artifactory'){
         steps {
             bat''' cd WebAppRazor/bin/Debug
                    powershell.exe -NonInteractive -ExecutionPolicy Bypass -Command compress-archive ./netcoreapp3.0/ netcoreapp_{$BUILD_ID}.zip
                    jfrog rt u *.zip  dotnetcore/  --url http://34.141.160.89:8082/artifactory --user admin --password Emids9211!
                    '''
         }
     }         
       
            
}


  
}
