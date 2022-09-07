pipeline {
    
    agent any
  
    stages {
    
        stage("build") {
        
            steps {
              sh 'composer install'
            }
        }
       stage("test") {
            
           steps {
            sh './vendor/bin/phpunit'
            }
        }
        stage('deploy') {
      steps {
          echo 'Deploying...'
      }  
    }
           
  }
}
