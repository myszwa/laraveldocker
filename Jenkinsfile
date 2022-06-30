pipeline {
    
    agent any
  
    stages {
    
        stage("build") {
        
            steps {
     sh "composer install"
            sh "cp .env.example .env"
            sh "php artisan key:generate"
            }
        }
       stage("test") {
            
           steps {
          echo 'Testing...'
      }
           }
        stage('deploy') {
      steps {
          echo 'Deploying...'
      }  
    }
           
  }
}
