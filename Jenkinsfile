pipeline
{
    agent any
    
    stages
    {
        stage("code")
        {
            steps
            {
                echo "cloning"
                git url:"https://github.com/mohammadsariqkhan/django-notes-app.git" , branch: "main"
            }
        }
        stage("build")
        {
            steps
            {
                echo "building"
                sh "docker build -t my-note-app ."
            }
            
        }
        stage("push to docker hub")
        {
            steps
            {
                 echo "pushing"
                withCredentials([usernamePassword(credentialsId:"dockerHub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")])
                {
                    sh "docker tag my-note-app ${env.dockerHubUser}/my-note-app:latest"
                    sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                    sh "docker push ${env.dockerHubUser}/my-note-app:latest"
                }
            }
           
        }
        stage("deploy")
        {
            steps
            {
                 echo "deploying"
                 sh "docker-compose down && docker-compose up -d"
            }
           
        }
    }
    
}
