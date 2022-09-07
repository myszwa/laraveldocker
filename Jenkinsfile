pipeline {
    
    agent any
  
    stages {
    
        stage("build") {
        
            steps {
              sh 'composer install'
              sh 'php artisan key:generate'
            }
        }
       stage("test") {
            
           steps {
            sh 'php artisan test'
            }
        }
        stage('deploy') {
      steps {
          echo 'Deploying...'
      }  
    }
           
  }
}
