## 액티비티 살펴보기 ##

### 액티비티의 이해 ###

액티비티는 사용자 인터페이스 화면을 관리하는 컴포넌트이다. 액티비티 역할을 하기 위해서는 Activity 클래스를 상속해야 하며, 액티비티가 기본적으로 가지고 있는 생명주기 메소드를 재정의해서 원하는 기능을 구현해야 한다.

#### 액티비티의 특징 ####

 - 액티비티의 크기는 상태바(Status bar)영역을 제외한 화면 전체로 고정
 - 두 개의 액티비티를 동시에 보여줄 수 없음.
 - 다른 애플리케이션의 액티비티를 불러낼 수 있음.
 - 액티비티 내에는 프래그먼트를 추가하여 분할하여 별도로 조작할 수 있음.

#### 액티비티의 종류 ####

액티비티 상위 클래스
>java.lang.Object.

> >↳ android.content.Context.

> > >↳ android.content.ContextWrapper

> > > >↳ android.view.ContextThemeWrapper

> > > > >↳ android.app.Activity


**Known Direct Subclasses**

AccountAuthenticatorActivity, ActivityGroup, AliasActivity, ExpandableListActivity, FragmentActivity, ListActivity, NativeActivity, TestActivity

**Known Indirect Subclasses**

ActionBarActivity, AppCompatActivity, LauncherActivity, PreferenceActivity,TabActivity




---
### 액티비티 생명주기 메소드 ###

액티비티는 생명주기(LifeCycle)를 가지고 있다. 이 생명주기에 따라 적절한 메소드가 호출되므로 이를 숙지해서 액티비티를 작성해야 한다.

![생명주기](./img/ActivityLifeCycle.jpg)

액티비티 생명주기는 onCreate() -> onStart() -> onResume() -> onStop() -> onDestroy()순으로 실행되며, 경우에 따라서 onRestart()메소드가 호출되기도 한다. 

**API 애티비티 생명주기**


* **onCreate()** 
	* 액티비티 생성될 때 호출되며 인터페이스 초기화에 사용됨 
	* 다음메소드 : onStart()

* **onRestart()**
	* 액티비티가 멈췄다가 다시 시작되기 바로 전에 호출됨.
	* 다음메소드 : onStart();

* **onStart()**
	* 액티비티가 사용자에게 보여지기 바로 직전에 호출됨
	* 다음메소드 : onResume() 또는 onStop()

* **onResume()**
	* 액티비티가 사용자와 상호작용하기 바로 전에 호출됨.
	* 다음메소드 : onPause()

* **onPause()**
	* 다른 액비비티가 보여질 때 호출됨. 데이터 저장, 스레드 중지 등의 처리를 하기에 적당한 메소드
	* 다음메소드 : onResume() 또는 onStop()

* **onStop()**
	* 액티비티가 더 이상 사용자에게 보여지지 않을 때, 호출됨. 메모리가 부족할 경우에는 onStop() 메소드가 호출되지 않을 수도 있음.
	* 다음메소드 : onRestart() 또는 onDestroy()

* **onDestroy()**
	* 액티비티가 소멸될 때 호출됨. finish() 메소드가 호출되거나 시스템이 메모리 확보를 위해 액티비티를 제거할 때 호출됨.
	* 다음메소드 : 없음

% onStop(), onDestory()는 호출되지 않을 수도 있음.


#### Tip & Tech 사용자가 홈 키를 눌렀는지를 파악하는 방법 ####

Activity클래스에는 onUserLeaveHint() 메소드가 제공되고 있다. 이 메소드가 바로 사용자가 홈 키를 눌렀을 때, 호출되는 메소드이다. 그러므로 이 메소드를 재정의해서 원하는 코드를 작성하면 된다. 참고로 이 메소드가 호출된 뒤에는 Activity의 onPause() 메소드가 호출된다.
