pipeline {
     agent any
     stages {
         stage('Build') {
             steps {
                 sh 'echo "Hello World"'
                 sh '''
                     echo "Multiline shell steps works too"
                     ls -lah
                 '''
             }
         }
         stage('Setup'){
             steps{
                 sh 'python3 -m venv ~/.devops'
                 sh 'source ~/.devops/bin/activate'
                 sh '''
                    pip install --upgrade pip &&\
		                    pip install -r requirements.txt
                '''
             }
         }
        }
}
