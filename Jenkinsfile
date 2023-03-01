pipeline {
  agent any
  stages {
    stage ('Testing') {
      steps {
          git branch: 'dev', credentialsId: 'for-git', url: 'https://github.com/AAT-technologies/cartservice.git'
          sh ''' sudo docker login -u delalixx -p dckr_pat_-dfSKHYHBVZNLTVX1R5sxmNGJwo
          '''
          sh ''' sudo docker system prune -af
          '''
         
         sh '''    cd app-cart/cartservice/src
                   ls
                   sudo docker build -t delalixx/cartservice .
                   sudo docker push delalixx/cartservice
                   '''
         sh ''' sudo docker system prune -af
                  '''
         
      }
    }
//      stage ('Create Deploy to Yaml file') {
//        steps {
//          sh ''' ls
//          '''
//            withCredentials([aws(credentialsId: 'aws-credentials', region: 'us-east-2')]) {
//            sh 'kubectl version --client --output=yaml'
//            sh '''
//                  aws eks --region us-east-2 update-kubeconfig --name master
//                  kubectl config current-context
//                  kubectl config use-context arn:aws:eks:us-east-2:842423002160:cluster/master 
//                  kubectl apply -f cluster.yaml
//                  kubectl get node
//                  kubectl get service
//                  kubectl get service frontend-external
//                  '''
//            }
//         }
//   }
  }
}
