pipeline {
    agent { label 'flask-demo' }

    stages {
        stage('Install Python and Git') {
            steps {
                sh '''
                    echo "Installing Git and Python..."
                    sudo yum install -y git
                    sudo yum install -y python3
                    sudo yum install -y python3-pip
                    python3 --version
                    pip3 --version
                    echo "Installation complete!"
                '''
            }
        }

        stage('Checkout Code') {
            steps {
                checkout scm
                sh "pwd"
            }
        }

        stage('Moving the Python File') {
            steps {
                sh '''
                    echo "Moving Python file..."
                    sudo mkdir -p /opt/python-folder
                    sudo cp /home/ec2-user/jenkins/workspace/new111/web.py /opt/python-folder/web.py
                    echo "Move complete!"

                    sh 'cd /opt/python && sudo pip install -r requirements.txt'
                    sh 'nohup python3 /opt/python/web.py'

                '''
            }
        }
        
    }
}
