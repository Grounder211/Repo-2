pipeline {
    agent any

    environment {
        DATA_SRC_DIR = "${WORKSPACE}/zip_files"
        DATA_TARGET_DIR = 'C:\\Users\\Public\\Downloads\\DATA_Files'
    }

    stages {
        stage('Clone Repo') {
            steps {
                echo "Cloning Repo-2"
                checkout([$class: 'GitSCM', 
                    branches: [[name: '*/master']], 
                    userRemoteConfigs: [[url: 'https://github.com/Grounder211/Repo-2.git']]
                ])
            }
        }

        stage('Copy New ZIP Files') {
            steps {
                script {
                    def zipFiles = findFiles(glob: 'zip_files/*.zip')
                    for (file in zipFiles) {
                        def dest = "${env.DATA_TARGET_DIR}\\${file.name}"
                        if (!fileExists(dest)) {
                            bat "copy \"${file.path}\" \"${dest}\""
                        } else {
                            echo "File ${file.name} already exists in target, skipping."
                        }
                    }
                }
            }
        }
    }

    post {
        success {
            echo '✅ ZIP files updated successfully.'
        }
        failure {
            echo '❌ Something went wrong!'
        }
    }
}
