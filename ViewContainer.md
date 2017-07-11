## 뷰 컨테이너 살펴보기

뷰 컨테이너(View Container)는 다른 View들을 포함하고 있거나 포함할 수 있는 View를 말하며, 일반적으로 ViewGroup을 상속하면서 Layout이 아닌 클래스를 지칭한다. ViewGroup 클래스를 상속하는 클래스를 안드로이드 API에서 살펴보면 다음과 같다.

>Java.lang.Object
> >↳android.view.View
> > >↳android.view.ViewGroup

주요한 컨테이너는 다음과 같다.
* ScrollView
* HorizontalScrollView
* Viewpager
* DatePicker
* TimePicker
* RecyclerView

---

### 1. 스크롤 뷰(ScrollView)

말그대로 스크롤 할 수 없는 뷰가 스크롤 할 수 있도록 만들어주는 컨테이너이다.

* 스크롤 뷰 안에는 오직 한개의 뷰만이 포함될 수 있다.

상속 계층도

>java.lang.Object
> >↳android.view.View
> > >↳android.view.ViewGroup
> > > >↳android.widget.FrameLayout
> > > > >↳android.widget.ScrollView

* 스크롤뷰 xml 코드

		<ScrollView xmlns:android="http://schemas.android.com/apk/res/android"
		    android:layout_width="match_parent"
		    android:layout_height="wrap_content" >
		
		    <LinearLayout
		        android:layout_width="match_parent"
		        android:layout_height="match_parent"
		        android:orientation="vertical" >
		
		        <TextView
		            android:layout_width="match_parent"
		            android:layout_height="200dip"
		            android:background="#ff0000"
		            android:gravity="center"
		            android:text="#ff0000" />
		
		    </LinearLayout>
		
		</ScrollView>


---
### 2. 수평 스크롤뷰(HorizontalScrollView)

수평 스크롤뷰(HorizontalScrollViw)는 스크롤뷰와 상당히 많이 비슷하다. 다른 점이라면, 스크롤뷰는 수직 방향이고 수평 스크롤뷰는 수평 방향이라는 거만 다를 뿐이다.

* 스크롤 뷰와 마찬가지로 오직 한개의 뷰만이 포함될 수 있다.

상속계층도

>java.lang.Object
> >↳ android.view.View
> > >↳ android.view.ViewGroup
> > > >↳ android.widget.FrameLayout
> > > > >↳ android.widget.HorizontalScrollView

* 수평스크롤 뷰 xml 코드

		<HorizontalScrollView xmlns:android="http://schemas.android.com/apk/res/android"
		    android:layout_width="match_parent"
		    android:layout_height="match_parent" >
		
		    <LinearLayout
		        android:layout_width="match_parent"
		        android:layout_height="match_parent"
		        android:orientation="horizontal" >
		
		        <TextView
		            android:layout_width="200dip"
		            android:layout_height="match_parent"
		            android:background="#ff0000"
		            android:gravity="center"
		            android:text="#ff0000" />
		
		     
		    </LinearLayout>
		
		</HorizontalScrollView>
		


---
### 3. 뷰페이저(ViewPager)

뷰페이저는 데이터 페이지를 플립하여 좌우로 넘길 수 있는 레이아웃 매니저이다. 뷰페이저는 여러 데이터들을 컨트롤 하기 때문에 PagerAdapter를 구현하여 페이지를 생성해야 한다.

뷰페이저는 대부분 Fragment와 연결되어 사용된다. 이 것은 각 페이지의 라이프사이클을 관리하고 생성하는데 편리하다. 프래그먼트와 뷰페이를 함께 사용하기 위해 제공하는 기본적인 어댑터들이 있는데 그것은 anroid.support.v4.app.FragmentPagerAdapter 와 android.support.v4.app.FragmentStatePagerAdapter 이다. 

* PagerAdapter 구현해야 함.
* support 라이브러리 안에 들어있다.

간단하게 FragmentPagerAdapter(FPA)와 FragmentStatePagerAdapter(FSPA)를 비교하자면

* FPA는 화면에서 사라져도 완전히 종료되기 전까지 프래그먼트를 메모리에 유지한다.
* FSPA는 화면에서 사라질 때 프래그먼트 상태만 저장하고 프래그먼트를 파기해 버린다.
* 그러므로 많은 양의 페이지나 프래그먼트를 사용할 때는 FSPA를 구현하여 어댑터를 만드는 것이 메모리 관리에 유리하다.


상속 계층도

>java.lang.Object
> >↳android.view.View
> > >↳android.view.ViewGroup
> > > >↳android.support.v4.view.ViewPager


기본적을 Adapter를 사용하는 뷰들과 사용방법은 동일하다

1. ViewPager를 생성한다.
2. PagerAdapter를 만든다. (여기서는 PagerAdapter를 구현하여 만듦)
3. viewPager 한 페이지에 들어가 ItemView를 만든다.
4. 페이저어댑터에서 뷰페이저에 들어갈 아이템뷰를 객체화하고 연결한다. 현재페이지를 관리할 수 있도록 한다.
5. 메인 액티비티에서 뷰페이저를 객체화하고 페이저와 어댑터를 연결한다.

* 간단한 뷰페이저 샘플코드이다.

		  <android.support.v4.view.ViewPager
		       android:layout_width="match_parent"
		       android:layout_height="match_parent">
		  
		       <android.support.v4.view.PagerTitleStrip
		           android:layout_width="match_parent"
		           android:layout_height="wrap_content"
		           android:layout_gravity="top" />
		  
		   </android.support.v4.view.ViewPager>

그리고 이 뷰페이저에 연결할 데이터가 필요한데, 간단한 데이터 xml을 만들어서 표시하도록 해보자.

* viewpager_child.xml 파일


		<?xml version="1.0" encoding="utf-8"?>
		<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
		    android:orientation="vertical" android:layout_width="match_parent"
		    android:layout_height="match_parent">
		
		    <ImageView
		        android:id="@+id/img_viewpager_childimage"
		        android:layout_width="match_parent"
		        android:layout_height="match_parent"/>
		    
		</LinearLayout>

위 xml 파일은 ViewPager가 만들어낼 한 Page의 모양이 이렇게 생길 것이다 라고 정의한 것이다.

그리고 만든 데이터 형식을 어댑터에 연결하기 위해 PagerAdapter를 구현하여 커스텀어댑터를 만든다.

* CustomAdapter 코드

		public class CustomAdapter extends PagerAdapter {
		
		    LayoutInflater inflater;
		
		    //전달 받은 레이아웃 인플레이터 전달
		    public CustomAdapter(LayoutInflater inflater) {
		        this.inflater = inflater;
		    }
		
		    // 뷰페이저가 가지고 있는 뷰의 개수 리턴
		    @Override
		    public int getCount() {
		        return 10;
		    }
		
		
		    // ViewPager가 현재 보여질 Item을 생성할 필요가 있을 때 자동으로 호출
		    // 쉽게 말해, 스크롤을 통해 현재 보여져야 하는 View를 만들어냄.
		    // 첫번째 파라미터 : VIewPager
		    // 두번쨰 파라미터 : ViewPager가 보여줄 View의 위치
		    @Override
		    public Object instantiateItem(ViewGroup container, int position) {
		
		        View view = null;
		
		        //새로운 View 객체를 layoutinflater를 이용하여 생성
		        view = inflater.inflate(R.layout.viewpager_child,null);
		        ImageView img = (ImageView)view.findViewById(R.id.img_viewpager_childimage);
		
		        //ImageView에 현재 position 번째 해당하는 이미지를 보여주기 위한 작업
		        //현재 position에 해당하는 이미지를 Setting
		        img.setImageResource(R.drawable.common_google_signin_btn_icon_dark+position);
		
		        // Viewpager에 해당 뷰 추가
		        container.addView(view);
		
		        // 만들어진 뷰를 리턴
		        return view;
		
		    }
		
		
		    //instantiateItem 메소드에서 리턴된 Object가 view가 맞는지 확인하는 메소드
		    @Override
		    public boolean isViewFromObject(View view, Object object) {
		        return view==object;
		    }
		
		    //화면에 보여지지 않는 뷰는 파괴하여 메모리 관리한다.
		    //첫번째 파라미터 : 뷰페이저
		    //두번째 파라미터 : 파괴될 View의 인덱스
		    //세번째 파라미터 : 파괴될 객체(더 이상 보이지 않은 View 객체)
		    @Override
		    public void destroyItem(ViewGroup container, int position, Object object) {
		
		        // viewpager에서 보이지 않는 view는 제거
		        //세번째 파라미터가 view객체 이지만 데이터 타입이 Object여서 형변환 실시
		        container.removeView((View)object);
		
		    }
		
		}


* MainActivity.java 파일


		// viewpager에서 설정할 Adapter 객체 생성
        // ListView에서 사용하는 Adapter와 같은 역할
        // 다만, ViewPager로 스크롤 될 수 있도록 되어 있다는 것이 다름.
        // PagerAdapter를 상속받은 CustomAdapter 객체 생성
        // CustommAdapter에게 Layoutinflater 객체 전달
        ViewPager pager;
        CustomAdapter adapter = new CustomAdapter(getLayoutInflater());

        //viewPager에 Adapter 설정



---
### 4. 데이트 피커(DatePicker)

데이트 피커는 화면에 날짜를 표시하고 이를 조정할 수 있는 뷰이다.

* DatePicker를 다이얼로그로 표현하고 싶다면 DatePickerDialog를 사용하면 된다.

상속계층도

>java.lang.Object
> >↳android.view.View
> > >↳android.view.ViewGroup
> > > >↳android.widget.FrameLayout
> > > > >↳android.widget.DatePicker


* DatePicker xml 코드

		<DatePicker xmlns:android="http://schemas.android.com/apk/res/android"
		    android:layout_width="match_parent"
		    android:layout_height="wrap_content" />


* 주요기능
	* android:datePickerMode="spinner" 데이터픽커 스티너모델로 변경
	* android:calendarViewShown="false" : 캘린더 제거

---
### 5. 타임 피커(TimePicker)

타임 피커는 화면에 시간을 표시하고 이를 조정할 수 있는 뷰이다.

상속계층도

>java.lang.Object
> >↳android.view.View
> > >↳android.view.ViewGroup
> > > >↳android.widget.FrameLayout
> > > > >↳android.widget.TimePicker


* timePicker xml 코드

		<TimePicker
		        android:id="@+id/timePicker"
		        android:layout_width="match_parent"
		        android:layout_height="wrap_content" />


* 주요기능
	* android:timePickerMode="spinner" 타임픽커 스티너모델로 변경


---
### 6. 리사이클러뷰(RecyclerView)

말그대로 뷰를 재활용하여 지속적으로 보여주는 뷰이다.
화면에 보여지는 뷰에 데이터를 바꾸어가면서 뷰를 재사용한다.

기존의 ListView와 상당히 비슷하지만 리스트 뷰의 단점을 극복하고 새롭게 추가된 부분이 많다.

1. LayoutManager
2. ViewHolder
3. Item 
4. Animation

이부분들이 새롭게 추가되엇다.

사용 클래스

1. ViewHolder - 재활용 View 를 관리해주는 Class
2. Adapter - 기존 ListView 와 동일하게 동작하면 Item 을 관리 하는 Class
3. LayoutManager - Item 의 레이아웃 관리 Class
4. ItemDecoration - Item 항목의 Sub View 관리 Class
5. ItemAnimation - Item 항목의 Animation 관리 Class


상속계층도

>java.lang.Object
> >↳android.view.View
> > >↳android.view.ViewGroup
> > > >↳android.support.v7.widget.RecyclerView

public class RecyclerView 
extends ViewGroup implements ScrollingView, NestedScrollingChild2

* RecyclerView xml 코드

		<TimePicker
		        android:id="@+id/timePicker"
		        android:layout_width="match_parent"
		        android:layout_height="wrap_content" />


* 리사이클러뷰에 들어갈 Item xml
	
		<?xml version="1.0" encoding="utf-8"?>
		<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
		    android:orientation="vertical" android:layout_width="match_parent"
		    android:layout_height="match_parent">
		
		    <TextView
		        android:id="@+id/ryTextView"
		        android:layout_width="match_parent"
		        android:layout_height="wrap_content"
		        android:text="안녕하세요" />
		
		    <TextView
		        android:id="@+id/ryEmailTextView"
		        android:layout_width="match_parent"
		        android:layout_height="wrap_content"
		        android:text="이멜입니다." />
		</LinearLayout>


* 아이템에 들어갈 VO코드 아이템클래스

		public class Users {
	
	    public String username;
	    public String email;
	
	    public Users() {
	        // Default constructor required for calls to DataSnapshot.getValue(User.class)
	    }
	
	    public Users(String username, String email) {
	        this.username = username;
	        this.email = email;
	    }
	
	}



* 리사이클러뷰 어댑터


		public class ReAdapter extends RecyclerView.Adapter {
	
	
	    private List<Users> usersList;
	    private int itemLayout;
	
	    /**
	     * 생성자
	     * @param items
	     * @param itemLayout
	     */
	    public MyRecyclerAdapter(List<Users> items , int itemLayout){
	
	        this.usersList = items;
	        this.itemLayout = itemLayout;
	    }
	
	    /**
	     * 레이아웃을 만들어서 Holer에 저장
	     * @param viewGroup
	     * @param viewType
	     * @return
	     */
	    @Override
	    public ViewHolder onCreateViewHolder(ViewGroup viewGroup, int viewType) {
	
	        View view = LayoutInflater.from(viewGroup.getContext()).inflate(itemLayout,viewGroup,false);
	        return new ViewHolder(view);
	    }
	
	    /**
	     * listView getView 를 대체
	     * 넘겨 받은 데이터를 화면에 출력하는 역할
	     *
	     * @param viewHolder
	     * @param position
	     */
	    @Override
	    public void onBindViewHolder(ViewHolder viewHolder, int position) {
	
	        Users item = usersList.get(position);
	        viewHolder.email.setText(item.email);
	        viewHolder.name.setText(item.username);
	        viewHolder.itemView.setTag(item);
	
	    }
	
	    @Override
	    public int getItemCount() {
	        return usersList.size();
	    }
	
	    /**
	     * 뷰 재활용을 위한 viewHolder
	     */
	    public static class ViewHolder extends RecyclerView.ViewHolder{
	
	        public TextView email;
	        public TextView name;
	
	        public ViewHolder(View itemView){
	            super(itemView);
	
	            email = (TextView) itemView.findViewById(R.id.ryEmail);
	            name = (TextView) itemView.findViewById(R.id.ryName);
	        }
	
	    }



* 메인 Activity.java

	public class MainActivity extends AppCompatActivity {

   
    	private RecyclerView lecyclerView;

    	@Override
    	protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        initLayout();
        initData();
    	}

    	/**
    	 * 레이아웃 초기화
    	 */
    	private void initLayout(){

    	    lecyclerView = (RecyclerView)findViewById(R.id.recycler);
    	}

	    /**
	     * 데이터 초기화
	     */
	    private void initData(){
	
	        List<Users> usersList = new ArrayList<Users>();
	
	        for (int i =0; i<20; i ++){
	
	            Users user = new Users();
	            user.username = ("현기");
	            user.email = ("lhgwoo2@naver.com");
	            usersList.add(user);
	        }
	
	        lecyclerView.setAdapter(new ReAdapter(usersList,R.layout.recycler_item));
	        lecyclerView.setLayoutManager(new LinearLayoutManager(getApplicationContext()));
			// 레이아웃 매니저를 셋팅해주어야 한다.
			
	
	        lecyclerView.setItemAnimator(new DefaultItemAnimator());
	
	    }


정리하자면

1. RecyclerView xml 코드 생성
2. 리사이클러뷰에 들어갈 Item xml 작성
3. 아이템에 들어갈 VO코드 아이템클래스 생성
4. 리사이클러뷰 어댑터 생성 - 뷰홀더 클래스생성 및 연결
5. 메인 Activity.java 작성 - 리사이클러뷰와 어댑터 연결, 리사이클러뷰 레이아웃매니저 셋팅


