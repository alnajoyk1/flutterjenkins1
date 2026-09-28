pipeline {
    agent any

    environment {
        FLUTTER_HOME = 'C:\\src\\flutter'
        ANDROID_HOME = 'C:\\Users\\Asus\\AppData\\Local\\Android\\Sdk'
        ANDROID_SDK_ROOT = 'C:\\Users\\Asus\\AppData\\Local\\Android\\Sdk'
        
        PATH = "${FLUTTER_HOME}\\bin;${ANDROID_HOME}\\platform-tools;${ANDROID_HOME}\\cmdline-tools\\latest\\bin;${ANDROID_HOME}\\emulator;${PATH}"
    }

    stages {

        stage('Check Flutter') {
            steps {
                bat 'where flutter'
                bat 'flutter --version'
            }
        }

        stage('Check Android SDK') {
            steps {
                bat 'echo ANDROID_HOME=%ANDROID_HOME%'
                bat 'echo ANDROID_SDK_ROOT=%ANDROID_SDK_ROOT%'
                bat 'if exist "%ANDROID_HOME%" (echo Android SDK found) else (echo Android SDK NOT found)'
                bat 'if exist "%ANDROID_HOME%\\platform-tools" (echo Platform Tools found) else (echo Platform Tools NOT found)'
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

            archiveArtifacts artifacts: 'build\\app\\outputs\\flutter-apk\\app-release.apk',
                             fingerprint: true
        }

        failure {
            echo 'Flutter build failed. Check the console output.'
        }
    }
}