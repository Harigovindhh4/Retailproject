
pipeline{
    agent any 

    envirnoment{
        LABS = Credentials('labcreds')
    }

    stages{
        stage('Build'){
            steps{
                sh 'pip3 install --user pipenv'
                sh '/bitnami/jenkins/home/.local/bin/pipenv --rm || exit 0'
                sh '/bitnami/jenkins/home/.local/bin/pipenv install'
               
            }
        }
        stage('Test'){
            steps{
                sh '/bitnami/jenkins/home/.local/bin/pipenv run pytest'
            }
        }
         stage('Package'){
            steps{
                sh 'zip -r retailproject.zip .'
            }
         }
         stage('Deploy'){
            steps{
                sh 'sshpass -p $LABS_PSW scp -o StructHostKeyChecking=no -r .
                $LABS_USR@02.itversity.com:/home/itv014200/reatilproject'
            }
         }


    }

}