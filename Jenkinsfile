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
              sshagent(['app-server-root-keys']) {
              // sh 'ssh -o StrictHostKeyChecking=no -l root 192.168.179.129 uname -a'
                         sh 'ssh -o StrictHostKeyChecking=no root@192.168.179.129 '
              }
            sh 'cd forum; \
                git pull origin master; \
                composer install --optimize-autoloader --no-dev; \
                php artisan migrate --force; \
                php artisan cache:clear; \
                php artisan config:cache "'
            }  
    }
           
  }
}
