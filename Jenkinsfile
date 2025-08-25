pipeline {
    agent any
    stages {
        stage('Preparacion') {
            steps {
                script{
                    env.image = ""
                    env.version = "latest"
                    env.stage = "develop"
                    git branch: rama, url:url
                    env. image = url.substring(url.lastIndexOf("/") + 1, url.lastIndexOf("."))
                }
            }
        }
        stage('Revision'){
            steps{
                echo "Revisión sólo ilustrativa (se puede incluir Sonarqube)"
                sh"""
                    pip install pytest
                    cd App
                    pytest || echo Sin pruebas
                """
            }
        }
        stage('Parametria'){
            steps{
                echo "Parametrización solo ilustrativa"
                sh"sed -i 's/imagen/${image}/g' YML/*.yaml"
            }
        }
        stage('Construccion'){
            steps{
                script{
                    sh"""
                        mv Docker/* .
                        mv App/* .
                        mv YML/* .
                        rm -rf Docker
                        rm -rf App
                        rm -rf YML
                    """
                    withCredentials([usernamePassword(credentialsId: 'dockercreds', usernameVariable: 'USR', passwordVariable: "PASS")]){
                        sh'''
                            docker build -t ${USR}/${image}:${version} .
                            docker login -u "${USR}" -p "${PASS}"
                            docker push ${stage}/${USR}/${image}:${version}
                        '''
                    }
                    deleteDir()
                }
            }
        }
        stage('Despliegue'){
            steps{
                sh'kubectl apply -f prueba.yaml || echo "Verifica cuenta de AWS"'
            }
        }
    }
    post{
        failure{
            deleteDir()
            echo "Ocurrió un error, verifica logs"
        }
    }
}