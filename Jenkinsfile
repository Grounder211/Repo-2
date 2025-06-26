pipeline {
    agent any

    environment {
        TARGET_DIR = 'C:/Users/Public/Downloads/DATA_Files'
    }

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/<your-user>/data-repo.git', branch: 'main'
            }
        }

        stage('Sync Zip Files') {
            steps {
                script {
                    bat """
                    if not exist "%TARGET_DIR%" mkdir "%TARGET_DIR%"
                    xcopy /Y /S /D *.zip "%TARGET_DIR%"
                    """
                }
            }
        }
    }
}
