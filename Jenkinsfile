pipeline {
    agent any
    
    stages {
        stage('Clone stage') {
            steps {
                git credentialsId: 'SSH_to_Github', url: 'https://github.com/Phuoc95/html_01.git'
                echo "Repository cloned successfully"
            }
        }
        
        // stage('Build stage') {
        //     steps {
        //         // Chuẩn bị code ở máy Jenkins trước khi gửi lên server
        //         // sh 'npm install'
        //         // sh 'npm run build'
        //     }
        // }
        
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
                                    // execCommand: '''
                                    // cd /var/www/project1
                                    // php artisan down
                                    // cp .env .env.backup
                                    // rm -rf vendor
                                    // composer install --no-interaction --no-dev --prefer-dist
                                    // php artisan migrate --force
                                    // php artisan config:cache
                                    // php artisan route:cache
                                    // php artisan view:cache
                                    // chown -R www-data:www-data .
                                    // chmod -R 755 storage bootstrap/cache
                                    // php artisan up
                                    // ''', 
                                    execTimeout: 180000, 
                                    flatten: false, 
                                    makeEmptyDirs: false, 
                                    noDefaultExcludes: false, 
                                    patternSeparator: '[, ]+', 
                                    remoteDirectory: '/var/www/project1',
                                    remoteDirectorySDF: true, 
                                    removePrefix: '', 
                                    sourceFiles: '**/*'
                                )
                            ], 
                            usePromotionTimestamp: false, 
                            useWorkspaceInPromotion: false, 
                            verbose: true,
                                 execCommand: '''
                cd /var/www/project1 || exit 1
                echo "Current directory: $(pwd)"
            '''
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