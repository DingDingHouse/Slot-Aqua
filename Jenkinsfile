def PROJECT_NAME = "Slot-Aqua"
def UNITY_VERSION = "2022.3.51f1"
def UNITY_INSTALLATION = "C:\\Program Files\\Unity\\Hub\\Editor\\${UNITY_VERSION}\\Editor\\Unity.exe"
def REPO_URL = "git@github.com:DingDingHouse/Slot-Aqua.git"

pipeline {
    agent any

    options {
        timeout(time: 60, unit: 'MINUTES')
    }

    environment {
        PROJECT_PATH = "C:\\Games\\Slot-Aqua"
    }

    stages {
        stage('Checkout') {
            steps {
                script {
                    dir("${PROJECT_PATH}") {
                        bat '''
                        git config --global http.postBuffer 3221225472
                        git clone git@github.com:DingDingHouse/Slot-Aqua.git C:\\Games\\Slot-Aqua || echo "Repository already exists, pulling latest changes."
                        cd Slot-Aqua
                        git checkout main
                        git fetch --all
                        git reset --hard origin/develop
                        git reset --hard origin/main
                        git checkout develop
                        '''
                    }
                }
            }
        }

        stage('Build WebGL') {
            steps {
                script {
                    withEnv(["UNITY_PATH=${UNITY_INSTALLATION}"]) {
                        bat '''
                        "%UNITY_PATH%" -quit -batchmode -projectPath "%PROJECT_PATH%" -executeMethod BuildScript.BuildWebGL -logFile -
                        '''
                    }
                }
            }
        }

   
    }
}
