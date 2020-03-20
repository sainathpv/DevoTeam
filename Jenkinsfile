pipeline {
   agent any
   stages {
        stage('Build User_Management Service') {
            steps {
                dir('User_Management/') {
                       
                       sh '''
                       sudo docker build -t devoteam1/devoteam:user_man .
                       sudo docker login --username=devoteam1 --password=team@1234
                       sudo docker push devoteam1/devoteam:user_man
                       '''
                }   
            }
        }

        stage('Build UI Service') {
            steps {
                dir('UI/') {
                       
                       sh '''
                       sudo docker build -t devoteam1/devoteam:ui .
                       sudo docker login --username=devoteam1 --password=team@1234
                       sudo docker push devoteam1/devoteam:ui
                       '''
                }   
            }
        }
   
        stage('Build API Service') {
            steps {
                dir('API_gateway/') {
                      
                       sh '''
                       sudo docker build -t devoteam1/devoteam:API .
                       sudo docker login --username=devoteam1 --password=team@1234
                       sudo docker push devoteam1/devoteam:API
                       '''
                }   
            }
        }
   
        stage('Build Data Ingestion Service') {
            steps {
                dir('Data_Ingestion/') {
                       
                       sh '''
                       sudo docker build -t devoteam1/devoteam:Data_Ingestion .
                       sudo docker login --username=devoteam1 --password=team@1234
                       sudo docker push devoteam1/devoteam:Data_Ingestion
                       '''
                }   
            }
        }
   
        stage('Build Model Execution Service') {
            steps {
                dir('Model_Execution/') {
                       
                       sh '''
                       sudo docker build -t devoteam1/devoteam:Model_Execution .
                       sudo docker login --username=devoteam1 --password=team@1234
                       sudo docker push devoteam1/devoteam:Model_Execution
                       '''
                }   
            }
        }
   
        stage('Build Post Processing Service') {
            steps {
                dir('UI/') {
                       
                       sh '''
                       sudo docker build -t devoteam1/devoteam:Post_processing .
                       sudo docker login --username=devoteam1 --password=team@1234
                       sudo docker push devoteam1/devoteam:Post_processing
                       '''
                }   
            }
        }
   
        stage('Build redis Service') {
            steps {
                dir('redis/') {
                       
                       sh '''
                       sudo docker build -t devoteam1/devoteam:redis .
                       sudo docker login --username=devoteam1 --password=team@1234
                       sudo docker push devoteam1/devoteam:redis
                       '''
                }   
            }
        }
   
        stage('Build Session Management Service') {
            steps {
                dir('Session_Management/') {
                      
                       sh '''
                       sudo docker build -t devoteam1/devoteam:session .
                       sudo docker login --username=devoteam1 --password=team@1234
                       sudo docker push devoteam1/devoteam:session
                       '''
                }   
            }
        }
   
        stage('Build RabbitMQ Server') {
            steps {
                dir('rabbit_server/') {
                      
                       sh '''
                       sudo docker build -t devoteam1/devoteam:rabbit_server .
                       sudo docker login --username=devoteam1 --password=team@1234
                       sudo docker push devoteam1/devoteam:rabbit_server
                       '''
                }   
            }
        }
        
    }
}
