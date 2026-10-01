pipeline{
    agent {
        label 'node'
    }
    stages
    {
        stage('CheckOut')
        {
            steps{
                git branch: 'main',

                url: 'https://github.com/Mrunal-2804/aws_k8s.git'
            }
        }
        stage('Build Image')
        {
            steps
            {
                sh 'docker build -t aws_k8s:latest .'
            }

        }
        stage ('Run Container')
        {
            steps{
                sh 'docker run -d --name aws-k8s-container -p 5000:5000 aws_k8s:latest'
            }
        }
        stage ('Test')
        {
            steps{
                sh 'curl http://localhost:5000/health'
            }
        }
    }
}