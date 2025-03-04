pipeline{
    agent {
        label 'python3.10'
    }
    parameters{
        choice(name: 'Branch_to_Build', choices: ['master'], description: 'Selecting branch of choice')
    }
    post{
        always{
            echo 'Job completed'
            mail to: 'tarunkumarpendem22@gmail.com',
                 subject: "Job's done",
                 body: "Job is completed for Build number: $env.BUILD_NUMBER"
        }
        success{
            echo 'Job successfully completed'
            mail to: 'tarunkumarpendem22@gmail.com',
                 subject: "Job's done",
                 body: "Job is successfully completed for Build number: $env.BUILD_NUMBER"
        }
        failure{
            echo 'Job failed'
            mail to: 'tarunkumarpendem22@gmail.com',
                 subject: "Job's done",
                 body: "Job is successfully failed for Build number: $env.BUILD_NUMBER"
        }
    }
    stages{
        stage('clone'){
            steps{
                git url: 'https://github.com/tarunkumarpendem/python-webcount.git',
                    branch: "${params.Branch_to_Build}"
            }
        }
        stage('build'){
            steps{
                sh 'pip3 install -r requirements.txt'
                sh 'tox'
            }
        }
        stage('Archiving_Artifacts'){
            steps{
                archiveArtifacts artifacts: '**/*.zip', followSymlinks: false
            }
        }
        stage('junit-reports'){
            steps{
                junit '**/*.xml'
            }
        }
    }
}