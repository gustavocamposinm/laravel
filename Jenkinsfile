node('php'){
    stage('Clean'){
        deleteDir()
        sh 'ls -la'
    }

    stage('Fetch') {
        checkout scm
    }

    stage('Docker Build') {
        sh 'sudo docker build -t gustavocamposinm/laravel:$BUILD_NUMBER .'
    }

    stage('Docker Ship') {
        sh 'sudo docker push gustavocamposinm/laravel:$BUILD_NUMBER'
    }
    
    stage('Docker Clean') {
        sh 'sudo docker rmi -f gustavocamposinm/laravel:$BUILD_NUMBER'
    }
}
