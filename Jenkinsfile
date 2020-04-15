pipeline
{
 agent any
  
 tools
  {
    nodejs 'node' 
    
  }

 stages
  {
   stage('Build')
    {
     steps
      {
       script
        {
         cleanWs()
         checkout changelog: false, poll: false, scm: [$class: 'GitSCM', branches: [[name: '${Repobranch}']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/Kashmiras25/react-web-app.git']]]
          sh '''
          ls -ltr
          npm install
          npm run build
          ls -ltr
          tar -cvf frontend-${BUILD_NUMBER}.tar *
          cp frontend-${BUILD_NUMBER}.tar ${WORKSPACE}/
          ls -ltr
          '''
          
        
        }
      }
     
    }  
    stage('Deploy')
   {
    steps
    {
     sh '''
     rm -rf deploy
     mkdir deploy
     cp tar -xvf frontend-${BUILD_NUMBER}.tar deploy/
     cd deploy
     tar -xvf frontend-${BUILD_NUMBER}.tar
     ls -ltr
     '''
     }
    }
  }  
  
}  
