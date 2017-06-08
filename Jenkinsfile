node('android') {
    stage('checkout') {
        echo 'Checking out application source code'
        checkout scm
    }
    stage('prepare') {
        echo 'Preparing Cordova application for build'
        sh 'cordova platform add android || true'
        sh 'cordova prepare android'
    }
    stage('build') {
        echo 'Building Cordova application'
        sh 'cordova build android --buildConfig www/fhconfig.json'
    }
    stage('archive') {
        echo 'Archiving Cordova build artifacts'
        archiveArtifacts artifacts: 'platforms/android/build/outputs/apk/*.apk'
    }
}