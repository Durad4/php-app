pipeline {
    agent {
        docker {
            image 'php:8.2'   // agent pakai PHP docker image
        }
    }
    stages {
        stage('Install Dependencies') {
            steps {
                sh 'curl -sS https://getcomposer.org/installer | php'
                sh 'php composer.phar install'
            }
        }
        stage('Test') {
            steps {
                sh 'vendor/bin/phpunit'
            }
        }
        stage('Deploy') {
            steps {
                echo "Menjalankan aplikasi dengan Docker"
                sh 'docker run -d -p 8081:80 -v $PWD:/var/www/html php:8.2-apache'
            }
        }
    }
}
