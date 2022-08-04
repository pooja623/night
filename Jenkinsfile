pipeline {
    agent {
        label ' ubuntu '
    }
    stages {
        stage('removing old files') {
            sh "sudo rm -rvf /var/www/html/POS-Applicationname/laravel-pos/*"

        }
    }

    STAGE('Cloning repo') {
        steps{
            sh "cd /var/www/html/POS-Applicationname"
            sh "sudo git clone  https://github.com/pooja623/night.git "
            sh "sudo chown -R www-data:www-data /var/www/html/laravel-pos"
            sh "sudo chmod -R 775 /var/www/html/laravel-pos/storage"
            sh "cd laravel-pos"
            sh "php artisan key:generate"
            sh "php artisan migrate"
            sh "php artisan db:seed"
            sh "php artisan storage:link"
        }
    }
    stage('Reloading code'){
        steps {
            sh "sudo chmod -R o+w /var/www/html/laravel-pos/storage"
            sh "sudo systemctl reload apache2 "
        }
    }
}
