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
    
    stage('Deploy Image')
       sh 'aws ecs register-task-definition --family new --cli-input-json file://task.json --region us-east-1'
       sh 'abc=$(aws ecs list-tasks --cluster new | rev | cut -d "/" -f 1 | rev)'
       sh 'echo $abc'
       sh 'aws ecs stop-task --cluster new --task $abc'
       sh 'aws ecs run-task --cluster new --launch-type EC2 --task-definition new'
}
