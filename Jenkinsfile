pipeline
{
    agent any
    stages
    {
        stage('continuos download')
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
        stage('Continuos deployment')
        {
            steps
            {
                deploy adapters: [tomcat9(credentialsId: '5f2d3d2d-9e11-4614-b025-d500f6bca561', path: '', url: 'http://172.31.39.148:8080')], contextPath: 'testapp', war: '**/*.war'
            }
        }
        stage('Continuous testing')
        {
            steps
            {
                git 'https://github.com/SharadChhatrikar1579/FunctionalTesting.git'
                
                sh 'java -jar /var/lib/jenkins/workspace/DeclarativePipeline/testing.jar'
            }
        }
        stage('Continuos Delivery')
        {
            steps
            {
                input message: 'Need approval from DM. Kindly check and approve', submitter: 'Srinivas'
                deploy adapters: [tomcat9(credentialsId: '5f2d3d2d-9e11-4614-b025-d500f6bca561', path: '', url: 'http://172.31.42.217:8080')], contextPath: 'prodapp', war: '**/*.war'
            }
        }
    }
}
