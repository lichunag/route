# route
/*对于ng项目中的路由切换
一共有三种类型
第一种 是直接切换*/
var app = angular.module('qmgj',['ui.router']);
app.config(['$stateProvider','$urlRouterProvider',function($stateProvider,$urlRouterProvider){
//这句话是在页面没有设置路由切换的前提下,强制跳转
   $urlRouterProvider.otherwise('/onepage');
   //这个login是在ui-view里面写入的
   .stateProvider.state('login'{
  // 这个是网站上的路由切换
    url:'/login',
    //连接到的html文件
    templateUrl:"view/login.html",
   }).state('enter'{
   /*这一种方式传递id参数,在控制器里面写,需要进行字符串拼接,拼接出你要使用的json文件*/
   url:'/enter/:id',
   templateUrl:'view/enter.html'
   })
   }]);
   
   /*这就是通过字符串拼接得到的*/
   
   app.controller("objdetailController",['$scope','$http','$stateParams',function($scope,$http,$stateParams){
         $scope.showIndex = 0;
         $scope.myFn = function(index){
            $scope.showIndex = index;
         }

        $http({
         url:'json/objshow'+$stateParams.id+'.json',
         // method:'get'
        }).success(function(res){
         $scope.shows = res.list;
         console.log($scope.shows);
        })
}]);

//你在需要点击跳转的地方
<p ui-sref="需要跳转的地方({这个是文件名的id:json文件的id})"></p>
