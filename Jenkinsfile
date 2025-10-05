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

        stage('Move and Run Python App') {
            steps {
                sh '''
                    echo "Moving Python app files..."
                    sudo mkdir -p /opt/python-folder
                    sudo cp /home/ec2-user/jenkins/workspace/new111/web.py /opt/python-folder/web.py
                    
                    echo "Move complete."
                    
                    cd /opt/python-folder
                    if [ -f requirements.txt ]; then
                        echo "Installing dependencies..."
                        sudo pip3 install -r requirements.txt
                    else
                        echo "No requirements.txt found — skipping dependency install."
                    fi

                    echo "Starting Flask app..."
                    nohup python3 /opt/python-folder/web.py > /opt/python-folder/flask.log 2>&1 &
                    cd /opt/python-folder

# Kill any old Flask process (optional, prevents port conflict)
pkill -f web.py || true

# Start Flask properly
nohup python3 web.py > flask.log 2>&1 &
                    echo "Flask app started. Check /opt/python-folder/flask.log for output."
                '''
            }
        }
    }
}
