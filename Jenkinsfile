node('jenkins-agent') {
  
  try{
    
    stage('Initialize') {
        echo 'Initializing...'
        def node = tool name: 'Node-7.4.0', type: 'jenkins.plugins.nodejs.tools.NodeJSInstallation'
        env.PATH = "${node}/bin:${env.PATH}"
    }

    stage 'checkout project'
    checkout scm

    stage 'check env'

         sh 'node -v'
         sh 'npm install'

    try{
        stage 'test'
        sh 'npm test'

    }finally{
        
        stage('SonarQube analysis') {
        // requires SonarQube Scanner 3
        def scannerHome = tool 'SonarQube Scanner 3';
        withSonarQubeEnv('SonarQube Scanner 3') {
          sh "${scannerHome}/bin/sonar-scanner"
        }
    }
    
  }

  }catch(e){

    throw e;
  }
}
