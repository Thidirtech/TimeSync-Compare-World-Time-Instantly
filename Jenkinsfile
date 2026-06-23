pipeline{
    agent{
        node{
            label 'ubuntusystem'
        }
    }

       environment {
        REPO_URL  = 'https://github.com/Thidirtech/TimeSync-Compare-World-Time-Instantly.git'
        TARGET_DIR = '/var/Timesync/html'
        PORT = '9090'
    }

    stages{
        stage("Clone Repository"){
            steps{
                echo "==== Clone Repository from Main Branch ===="
                git url: "${REPO_URL}", branch: 'main'
            }
        }
           stage("Deply file on the server"){
            steps{
                echo "==== Clone Repository from Main Branch ===="
                sh '''
                    mkdir -p ${TARGET_DIR}
                    cp index.html ${TARGET_DIR}
                ''''
            }
        }
          stage("Start Python Web Server") {
            steps {
                sh '''
                    fuser -k 9090/tcp || true
                    cd ${TARGET_DIR}
                    nohup python3 -m http.server ${PORT} > python_server.log 2>&1 &
                '''
            }
        }

    }
}
