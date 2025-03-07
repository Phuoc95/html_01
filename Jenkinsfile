pipeline {
    agent any
    
    stages {
        stage('Clone stage') {
            steps {
                git credentialsId: 'SSH_to_Github', url: 'https://github.com/Phuoc95/html_01.git'
                echo "Repository cloned successfully"
            }
        }
        
        stage('SSH server') {
            steps {
                sshPublisher(
                    publishers: [
                        sshPublisherDesc(
                            configName: '54.255.82.109 (EC2)', 
                            transfers: [
                                sshTransfer(
                                    cleanRemote: false, 
                                    excludes: 'node_modules/,vendor/,tests/,storage/framework/cache/**,storage/framework/sessions/**', 
                                    execTimeout: 180000, 
                                    flatten: false, 
                                    makeEmptyDirs: false, 
                                    noDefaultExcludes: false, 
                                    patternSeparator: '[, ]+', 
                                    remoteDirectory: '',
                                    // execCommand: 'cp -r $WORKSPACE/* /var/www/project123/',
                                    // remoteDirectory: '/var/www/project123',
                                    remoteDirectorySDF: false, 
                                    removePrefix: '', 
                                    sourceFiles: '**/*'
                                )
                            ], 
                            usePromotionTimestamp: false, 
                            useWorkspaceInPromotion: false, 
                            verbose: true
                        )
                    ]
                )
            }
        }
    }
    
    post {
        success {
            echo 'Deployment completed successfully!'
        }
        failure {
            echo 'Deployment failed.'
        }
    }
}