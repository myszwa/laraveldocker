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
              sh 'ssh -o StrictHostKeyChecking=no root@192.168.179.129'
              }
            sh 'pwd'  
            sh 'cd forum'
            sh 'git pull origin master'
            sh 'composer install --optimize-autoloader --no-dev'
            sh 'php artisan cache:clear'
            sh 'php artisan config:cache'
            }  
    }
           
  }
}
