def NODE_EXPLORE_TIMEOUT_SECS = 60
 
def platform = params?.PLATFORM?.trim()
 
stage("checkPlatform") {
  if (platform) {
    echo "Checking if the node for platform exists: ${platform}"
    try {
      timeout(time: NODE_EXPLORE_TIMEOUT_SECS, unit: 'SECONDS') {
        node(platform) {
          echo "Node exists for platform."
        }
      }
    } catch (e) {
      error("Unable to get the node for the given platform. Error: " + e.getMessage())
    }
  } else {
    echo "No platform given. Cancelling build"
    error("No platform given")
  }
}
 
node(platform) {
  stage("prepare") {
    sh "cordova platform add ${platform} || true"   // ignore errors in this step. we don't want to fail the Jenkins build if the platform is already added.
    sh "cordova platform prepare ${platform}"
  }
  stage("build") {
    sh "cordova platform build ${platform}"
  }
}