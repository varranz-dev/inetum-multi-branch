// Pipeline declarativo
pipeline {
    //Ejecutar el pipeline desde UN agente (nodo) concreto
  agent {
    node {
      label 'principal'
    }
  }
  
  options {
    //Ficheros de log
    buildDiscarder logRator(
      daysToKeepStr: '15',
      numToKeepStr: '10'
    )
  }
  
  //Definicion de fases
    stages {
      stage('Cleanup Workspace') {
        //Limpiamos el workspace previo 
        steps{
          cleanWS()
            echo 'Eliminado el workspace para Job';
        }
      }
      stage('Code Checkout') {
          //Conjunto de pasos que componen la fase
          steps{
            checkout(
                $class: 'GitSCM',
                branches: [[name: '*/main']]
                userRemoteConfigs: [[url: 'https://github.com/spring-projects/spring-petclinic.git']]
              )
          }
      }
      stage('Unit Testing') {
        when {
          branch 'testing'
        }
          steps{
              echo 'Running Unit Tests';
          }
      }
      stage('Code Analysis') {
          steps{
              echo 'Running Code Analysis';
          }
      }
      stage('Buid Deploy Code') {
        when {
          branch 'developer'
        }
          steps{
            echo 'Build Artifact';
            echo 'Deploying Code';
          }
      }
    } 
}
