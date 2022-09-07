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
            sh 'php artisan key:generate'
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
