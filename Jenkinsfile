pipeline {
    agent any

    environment {
        FLUTTER_HOME = 'C:\\src\\flutter'
        PATH = "${FLUTTER_HOME}\\bin;${PATH}"
    }

    stages {

        stage('Check Flutter') {
            steps {
                bat 'where flutter'
                bat 'flutter --version'
            }
        }

        stage('Get Dependencies') {
            steps {
                bat 'flutter pub get'
            }
        }

        stage('Build APK') {
            steps {
                bat 'flutter build apk --release'
            }
        }
    }

    post {
        success {
            echo 'Flutter APK build completed successfully!'
        }

        failure {
            echo 'Flutter build failed. Check the console output.'
        }
    }
}