pipeline {
    agent any

    stages {
        stage('Deploy to Prod') {
            steps {
                sshagent(['prod-ssh-key']) {

                    sh """
                    ssh -o StrictHostKeyChecking=no vainatey@13.205.96.0 << 'EOF'

                    echo "Switching to app directory..."
                    cd /home/vainatey/frappe-bench/apps/vainatey

                    echo "Pulling latest changes..."
                    git pull upstream main

                    echo "Running migrations..."
                    cd /home/vainatey/frappe-bench
                    bench --site erp-uat.vainatey.com migrate

                    

                    echo "Deployment completed successfully."

                    EOF
                    """
                }
            }
        }
    }

    post {
        success { echo 'Deployment Finished Successfully!' }
        failure { echo 'Deployment Failed. Check Console Output.' }
    }
}

