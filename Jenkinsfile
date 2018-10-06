node('php'){
    stage('Clean'){
        deleteDir()
        sh 'ls -la'
    }

    stage('Fetch') {
        checkout scm
    }

    stage('Build for Tests'){
        sh 'composer install --no-scripts --prefer-dist --ignore-platform-reqs'
    }

    stage('config') {
        parallel(
            'Copy .env file': {
                sh 'cp .env.example .env'
            },
            'config cache': {
                echo 'Tarefa Paralela 02'
            }
        )
    }

    stage('Tests') {
        sh 'php ./vendor/bin/phpunit'
    }

    stage('Build'){
        sh 'composer install --prefer-dist --no-dev --ignore-platform-reqs'
    }

    stage('Docker Build') {
        sh 'docker build -t gustavocamposinm/laravel:$BUILD_NUMBER .'
    }

    stage('Docker Ship') {
        sh 'docker push gustavocamposinm/laravel:$BUILD_NUMBER'
    }
    
    stage('Clean Up') {
        sh 'docker rmi gustavocamposinm/laravel:$BUILD_NUMBER'
        deleteDir()
    }
}
