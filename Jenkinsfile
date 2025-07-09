// pipeline {
//     agent any

//     environment {
//         // SDK and Java Paths (hardcoded)
//         ANDROID_HOME = 'C:\\Android\\Sdk'
//         JAVA_HOME = 'C:\\Program Files\\Java\\jdk-17.0.12'
//         PATH = "C:\\Android\\Sdk\\platform-tools;" +
//                "C:\\Android\\Sdk\\cmdline-tools\\latest\\bin;" +
//                "C:\\Android\\Sdk\\build-tools\\34.0.0;" +
//                "C:\\Program Files\\Java\\jdk-17.0.12\\bin;" +
//                "${env.PATH}"
//     }

//     stages {
//         stage('Environment Check') {
//             steps {
//                 bat 'echo === SDK LOCATION: %ANDROID_HOME% ==='
//                 bat 'adb --version'
//                 bat 'sdkmanager --list'
//                 bat 'java -version'
//             }
//         }

//         stage('Clean Build') {
//             steps {
//                 bat './gradlew clean'
//             }
//         }

//         stage('Assemble APK') {
//             steps {
//                 bat './gradlew assembleDebug'
//             }
//         }

//         stage('Post Build') {
//             steps {
//                 bat 'dir app\\build\\outputs\\apk\\debug'
//             }
//         }
//     }

//     post {
//         failure {
//             echo '❌ Build failed!'
//         }
//         success {
//             echo '✅ Build completed successfully!'
//         }
//     }
// }

pipeline {
    agent any

    environment {
        ANDROID_HOME = "C:\\Android\\Sdk"
        PATH = "C:\\Android\\Sdk\\cmdline-tools\\latest\\bin;C:\\Android\\Sdk\\platform-tools;"
    }

    tools {
        nodejs 'NodeJs'   
        jdk 'JAVA_JDK'    
    }

    stages {
        stage('Checkout Code') {
            steps {
                git url: 'https://github.com/Ronak-W/jenkins_app.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                bat 'npm install'
                bat 'npx react-native --version'
            }
        }

        stage('Clean Android Build') {
            steps {
                dir('android') {
                    bat 'gradlew.bat clean'
                }
            }
        }

            tools {
        jdk 'JAVA_JDK' // must match the name exactly
    }

            stage('Check Android Dir') {
        steps {
            dir('android') {
                bat 'dir'
            }
        }
    }

        stage('Check gradlew.bat') {
        steps {
            dir('android') {
                bat 'if exist gradlew.bat (echo Found gradlew.bat) else (echo gradlew.bat not found)'
            }
        }
    }

        stage('Assemble APK') {
            steps {
                dir('android') {
                    bat 'gradlew.bat assembleRelease --info'
                }
            }
        }

        stage('Archive APK') {
            steps {
                archiveArtifacts artifacts: 'android/app/build/outputs/apk/release/app-release.apk', fingerprint: true
            }
        }
    }

    post {
        success {
            echo '✅ Android APK build completed successfully.'
        }
        failure {
            echo '❌ Android APK build failed.'
        }
    }
}
