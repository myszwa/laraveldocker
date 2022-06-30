pipeline {
    
    agent any
  
    stages {
    
        stage("build") {
        
            steps {
        echo 'Building...'
            }
        }
       stage("test") {
            
           steps {
            // Run any testing suites
            sh "./vendor/bin/phpunit"
      }
           }
        stage('deploy') {
      steps {
          echo 'Deploying...'
      }  
    }
           
  }
}
