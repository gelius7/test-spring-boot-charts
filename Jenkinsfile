def SERVICE_GROUP = "svc-grp"
def SERVICE_NAME = "svc-name"
def IMAGE_NAME = "${SERVICE_GROUP}-${SERVICE_NAME}"
def REPOSITORY_URL = "https://github.com/gelius7/test-spring-boot-charts.git"
def REPOSITORY_SECRET = ""
def SLACK_TOKEN_DEV = []
def SLACK_TOKEN_DQA = ""

@Library("github.com/opsnow-tools/valve-butler")
def butler = new com.opsnow.valve.v7.Butler()
def label = "worker-${UUID.randomUUID().toString()}"

properties([
  buildDiscarder(logRotator(daysToKeepStr: "60", numToKeepStr: "30")),
  parameters {[
    string(name: 'paramName', defaultValue: 'Hello default', description: 'This is test')
  ]}
])
podTemplate(label: label, containers: [
  containerTemplate(name: "builder", image: "quay.io/opsnow-tools/valve-builder", command: "cat", ttyEnabled: true, alwaysPullImage: true),
  containerTemplate(name: "maven", image: "maven:3.5.4-jdk-8-alpine", command: "cat", ttyEnabled: true)
], volumes: [
  hostPathVolume(mountPath: "/var/run/docker.sock", hostPath: "/var/run/docker.sock"),
  hostPathVolume(mountPath: "/home/jenkins/.draft", hostPath: "/home/jenkins/.draft"),
  hostPathVolume(mountPath: "/home/jenkins/.helm", hostPath: "/home/jenkins/.helm")
]) {
  node(label) {
    stage("Prepare") {
      container("builder") {
//        butler.prepare(IMAGE_NAME)
        echo "param name : $params.paramName"
      }
    }
    stage("Checkout") {
      container("builder") {
//        try {
//          if (REPOSITORY_SECRET) {
//            git(url: REPOSITORY_URL, branch: BRANCH_NAME, credentialsId: REPOSITORY_SECRET)
//          } else {
//            git(url: REPOSITORY_URL, branch: BRANCH_NAME)
//          }
//        } catch (e) {
//          butler.failure(SLACK_TOKEN_DEV, "Checkout")
//          throw e
//        }

//        butler.scan("java")
      }
    }
//    stage("Build") {
//      container("maven") {
//        try {
//          butler.mvn_build()
//          butler.success(SLACK_TOKEN_DEV, "Build")
//        } catch (e) {
//          butler.failure(SLACK_TOKEN_DEV, "Build")
//          throw e
//        }
//      }
//    }
//    if (BRANCH_NAME == "master") {
//      stage("Build Image") {
//        parallel(
//          "Build Docker": {
//            container("builder") {
//              try {
//                butler.build_image()
//              } catch (e) {
//                butler.failure(SLACK_TOKEN_DEV, "Build Docker")
//                throw e
//              }
//            }
//          },
//          "Build Charts": {
//            container("builder") {
//              try {
//                butler.build_chart()
//              } catch (e) {
//                butler.failure(SLACK_TOKEN_DEV, "Build Charts")
//                throw e
//              }
//            }
//          }
//        )
//      }
//      stage("Deploy DEV") {
//        container("builder") {
//          try {
//            // deploy(cluster, namespace, sub_domain, profile)
//            butler.deploy("dev", "${SERVICE_GROUP}-dev", "${IMAGE_NAME}-dev", "dev")
//            butler.success(SLACK_TOKEN_DEV, "Deploy DEV")
//          } catch (e) {
//            butler.failure(SLACK_TOKEN_DEV, "Deploy DEV")
//            throw e
//          }
//        }
//      }
//    }
  }
}
