pipeline {
    agent {
        docker {
            image 'php:8.2'
            args '-u root --entrypoint=""'
        }
    }
    stages {
        stage('Prepare') {
            steps {
                sh '''
                    apt-get update
                    apt-get install -y git unzip
                '''
            }
        }
        stage('Install Dependencies') {
            steps {
                sh '''
                    curl -sS https://getcomposer.org/installer | php
                    php composer.phar install
                '''
            }
        }
        stage('Test') {
            steps {
                sh 'vendor/bin/phpunit'
            }
        }
        stage('Deploy') {
            agent { label 'master' }
            steps {
                echo 'Menjalankan aplikasi...'
                sh 'docker run -d -p 8081:80 -v $PWD:/var/www/html php:8.2-apache'
            }
        }
    }
}
