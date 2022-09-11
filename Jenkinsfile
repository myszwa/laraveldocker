pipeline {
    
    agent any
  
    stages {
    
        stage("build") {
        
            steps {
              sh 'cp .env.example .env'
              sh 'composer install'
              sh 'npm install'
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
            sh 'ssh root@127.0.0.1 "cd forum; \
                git pull origin master; \
                composer install --optimize-autoloader --no-dev; \
                php artisan migrate --force; \
                php artisan cache:clear; \
                php artisan config:cache "'
            }  
    }
           
  }
}
