pipeline {
    agent any

    // On déclare juste des variables "brutes" ici (PAS de isUnix() dans environment)
    environment {
        JAVA_HOME_LINUX   = '/usr/lib/jvm/java-8-openjdk-amd64'
        JAVA_HOME_WINDOWS = 'C:\\Program Files\\Java\\jdk1.8.0_202'
        PYTHON_WIN        = 'C:\\Users\\rehou\\AppData\\Local\\Microsoft\\WindowsApps\\python3.exe'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/haythem-rehouma/hello-python.git'
            }
        }

        stage('Build') {
            steps {
                script {
                    if (isUnix()) {
                        // ----- AGENT LINUX -----
                        env.JAVA_HOME = env.JAVA_HOME_LINUX
                        env.PATH      = "${env.PATH}:${env.JAVA_HOME}/bin:/usr/bin"

                        sh '''
                            echo "Running on Unix"
                            echo "JAVA_HOME=$JAVA_HOME"
                            echo "PATH=$PATH"

                            javac HelloWorld.java
                            java HelloWorld

                            # Python 3 sur Linux
                            python3 hello.py
                        '''
                    } else {
                        // ----- AGENT WINDOWS -----
                        env.JAVA_HOME = env.JAVA_HOME_WINDOWS
                        env.PATH      = "${env.PATH};${env.JAVA_HOME}\\bin"

                        // IMPORTANT : on met le chemin complet vers python3.exe
                        bat """
                            echo Running on Windows
                            echo JAVA_HOME=%JAVA_HOME%
                            echo PATH=%PATH%

                            javac HelloWorld.java
                            java HelloWorld

                            "%PYTHON_WIN%" hello.py
                        """
                    }
                }
            }
        }
    }
}
