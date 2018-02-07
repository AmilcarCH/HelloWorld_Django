#!groovy


node {

    def installed = fileExists 'holamundo/bin/activate'

    if (!installed) {
        stage("levantar un entorno virtual") {
            sh '''pip3.6 install virtualenv
            virtualenv holamundo'''
        }
    }   
    
    stage ("optener el proyecto del GIT") {
    checkout([$class: 'GitSCM', branches: [[name: '*/master']], browser: [$class: 'GithubWeb', repoUrl: 'github.com'], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: '1', url: 'https://github.com/AmilcarCH/HelloWorld_Django/']]])
    }
    
    stage ("instalar las dependencias") {
        sh '''
            source holamundo/bin/activate
            pip3.6 install -r requirements.txt
            deactivate
           '''
    }
    
    stage ("migrar a la base de datos") {
        sh '''source holamundo/bin/activate
            python3.6 manage.py migrate
            deactivate
            '''
    }
    
    stage ("reiniciar el proceso del proyecto") {
        
        sh '''
                supervisorctl restart HelloWorld
               '''
        
       
    }
    
    
}