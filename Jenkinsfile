pipeline {
    
    agent any
  
    stages {
    
        stage("build") {
        
            steps {
              sh 'cp .env.example .env'
              sh 'composer install'
              // sh 'npm install'
              sh 'php artisan key:generate'
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
