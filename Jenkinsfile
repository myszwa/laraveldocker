pipeline {
    
    agent {
        dockerfile true
    }
  
    stages {
    
        stage("build") {
        
            steps {
          sh 'php --version'
                sh 'composer install --ignore-platform-reqs'
                sh 'composer --version'
                sh 'cp .env.example .env'
                sh 'php artisan key:generate'
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
