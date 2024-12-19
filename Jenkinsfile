pipeline {
    agent any

	tools {
        msbuild 'MSBuild'
    }

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/ElizabethPaziy/SP_part4.git', credentialsId: 'SP_part4', branch: 'main'
            }
        }
        
        stage('Build') {
            steps {
                // Крок для збірки проекту з Visual Studio
                // Встановіть правильні шляхи до рішення/проекту та параметри MSBuild
                bat 'msbuild test_repos.sln /t:Build /p:Configuration=Release'
            }
        }

        stage('Test') {
            steps {
                // Команди для запуску тестів
                bat "x64\\Debug\\test_repos.exe --gtest_output=xml:test_report.xml"
            }
        }
    }

    post {
		always {
		    // Publish test results using the junit step
		    junit 'test_report.xml'
		}
	}
}
