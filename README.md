pipeline { 
    agent any 
    options {
        skipStagesAfterUnstable()
    }
    stages {
        stage('Build') { 
            steps { 
                sh 'cd /home/gagana/venv/lib/python3.8/site-packages/locust -f locustfile.py --user 1 --spawn-rate 1 --run-time 10s --headless --print-stats --csv Run1.csv --csv-full-history --host=https://www.google.com'
            }
        }
        stage('Test'){
            steps {
                sh 'cd /home/gagana/venv/lib/python3.8/site-packages/locust -f locustfile.py --user 1 --spawn-rate 1 --run-time 10s --headless --print-stats --csv Run1.csv --csv-full-history --host=https://www.google.com'
                junit 'reports/**/*.xml' 
            }
        }
        stage('Deploy') {
            steps {
                sh 'cd /home/gagana/venv/lib/python3.8/site-packages/locust -f locustfile.py --user 1 --spawn-rate 1 --run-time 10s --headless --print-stats --csv Run1.csv --csv-full-history --host=https://www.google.com'
            }
        }
    }
}
