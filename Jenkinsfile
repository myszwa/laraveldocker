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
            sh 'php artisan serve'
            }
        }
        stage('deploy') {
      steps {
          echo 'Deploying...'
      }  
    }
           
  }
}
