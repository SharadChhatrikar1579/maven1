pipeline
{
    agent any
    stages
    {
        stage('Continuos Download')
        {
            steps
            {
                git 'https://github.com/SharadChhatrikar1579/maven.git'
            }
        }
        stage('Continuos Build')
        {
            steps
            {
                sh 'mvn package'
            }
        }
        stage('Continuos Delivery')
        {
            steps
            {
                deploy adapters: [tomcat9(credentialsId: '5f2d3d2d-9e11-4614-b025-d500f6bca561', path: '', url: 'http://172.31.39.148:8080')], contextPath: 'testapp', war: '**/*.war'
            }
        }
        stage('Continuos Testing')
        {
            steps
            {
                git 'https://github.com/SharadChhatrikar1579/FunctionalTesting.git'
                sh 'java -jar /var/lib/jenkins/workspace/DeclarativePipeline1/testing.jar'
            }
        }
        
    }
    post
    {
        success
        {
            deploy adapters: [tomcat9(credentialsId: '5f2d3d2d-9e11-4614-b025-d500f6bca561', path: '', url: 'http://172.31.42.217:8080')], contextPath: 'prodapp', war: '**/*.war'
        }
        failure
        {
            mail bcc: '', body: 'Jenkins has failed in CI', cc: 'sharadchha@gmail.com', from: '', replyTo: '', subject: 'CI failed', to: 'sharad@gmail.com'
        }
    }
}

    

