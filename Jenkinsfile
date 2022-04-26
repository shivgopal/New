node {
    stage('Git pull') {
        git 'https://github.com/shivgopal/New.git'
    }
    stage('ECR login')
    {
        sh 'aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 117357342131.dkr.ecr.us-east-1.amazonaws.com'
    }
    stage('docker build')
    {
       sh 'docker build -t nodejsapp .' 
    }
    stage('Docker image tag')
       sh 'docker tag nodejsapp:latest 117357342131.dkr.ecr.us-east-1.amazonaws.com/nodejsapp:latest'
    stage('Image push')
       sh 'docker push 117357342131.dkr.ecr.us-east-1.amazonaws.com/nodejsapp:latest'
} 		
}
