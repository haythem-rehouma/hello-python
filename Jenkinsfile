pipeline {
    agent any

    environment {
        JAVA_HOME_LINUX   = '/usr/lib/jvm/java-8-openjdk-amd64'
        JAVA_HOME_WINDOWS = 'C:\\Program Files\\Java\\jdk1.8.0_202'
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
                        // --- AGENT LINUX ---
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
                        // --- AGENT WINDOWS ---
                        env.JAVA_HOME = env.JAVA_HOME_WINDOWS
                        env.PATH      = "${env.PATH};${env.JAVA_HOME}\\bin"

                        bat """
                            echo Running on Windows
                            echo JAVA_HOME=%JAVA_HOME%
                            echo PATH=%PATH%

                            javac HelloWorld.java
                            java HelloWorld

                            rem --- Essai 1 : python classique dans le PATH ---
                            python --version
                            python hello.py || echo python hello.py failed

                            rem --- Essai 2 (fallback) : Python Launcher py.exe ---
                            py -3 --version
                            py -3 hello.py
                        """
                    }
                }
            }
        }
    }
}
