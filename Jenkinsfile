 pipeline { 
    agent none 

    stages {
      stage('build') {
        agent {
          label 'apache'
        }
        steps { 
          sh 'ant -f build.xml -v'
       }
       post { 
         success { 
           archiveArtifacts artifacts: 'dist/*.jar', fingerprint: true
       }
     }
    }
     stage('deploy'){
      agent {
        label 'apache'
        }
         steps {
          sh "cp dist/rectangle_${env.BUILD_NUMBER}.jar /var/www/html/rectangles/all/"
       }
      }
      stage("Running on Centos") { 
        agent { 
         label 'CentOs'
       }
       steps {
        sh "wget http://mahank286.mylabserver.com/rectangles/all/rectangle_${env.BUILD_NUMBER}.jar"
        sh "java -jar rectangle_${env.BUILD_NUMBER}.jar 3 4"
       }
     }
   }
 }
