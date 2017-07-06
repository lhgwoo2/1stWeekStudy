##안드로이드 첫번째 프로젝트 실행하기##

###프로젝트 생성###
* **Android Studio**에서 새 프로젝트를 생성
	
	열려있는 프로젝트가 없으면 **Welcome to Android Studio** 창에서 **Start a new Android Studio project**를 클릭

	열려있는 프로젝트가 있으면 **File > New Project** 선택

* **New Project**화면에서 **Application Name**과 **Company Domain** 설정	

* **Minimum Required SDK** 설정, 이 기능은 앱이 지원하고자 하는 최소한의 안드로이드 버전 설정.

* **Add an Activity to Mobile** 화면에서 **Empty Activity**를 선택하고 **Next**를 클릭

* 이후에는 기본값 설정 후 **Finish** 클릭, 생성

###프로젝트 실행###

* 툴바에서 **Run**을 클릭하여 기기 또는 에뮬레이터를 실행하여 앱을 실행한다. 

###프로젝트 구성요소의 이해###

* **MainActivity** : 생성한 액티비티에 대한 클래스 정의가 포함되어있으며, 화면 레이아웃 파일을 로드함.

* **activity_main.xml** : 액티비티의 레이아웃을 정의하며, 위젯 등의 요소를 포함한다.

* **AndroidManifest.xml** : 이 파일은 앱의 기본 특징을 설명하고 앱의 각 구성 요소를 정의함.

* **build.gradle** : Gradle을 사용해 앱을 컴파일하고 구축함. 프로젝트에는 각 모듈을 위한 build.gradle 파일이 있음.