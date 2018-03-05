## com.baltivirtual.android

A library to use BaltiVirtual assets in Android

## Installation


### Gradle Installation
Add a reference to jitpack.io in in your root build.gradle at the end of the repositories:
```
allprojects {
    repositories {
        ...
        maven { url 'https://jitpack.io' }
    }
}
```
Then add the dependency:
```
dependencies {
    compile 'com.github.brianswartz:baltivirtualandroid:0.0.1'
}
```

### Maven Installation
Add a reference to jitpack.io repository:
```
<repositories>
    <repository>
        <id>jitpack.io</id>
        <url>https://jitpack.io</url>
    </repository>
</repositories>
```
Then add the dependency:
```
<dependency>
    <groupId>com.github.brianswartz</groupId>
    <artifactId>baltivirtualandroid</artifactId>
    <version>0.0.1</version>
</dependency>
```


## Usage

### Layout Setup
In your desired layout xml file add an instance of the BaltiVirtualFragment:
```
<fragment android:name="com.balitvirtual.android.BaltiVirtualFragment"
        android:id="@+id/baltivirtualfragment"
        android:layout_width="match_parent"
        android:layout_height="400dp" />
```

### Activity Setup
In your Activity add the com.balitvirtual.android import statements:
```
import com.balitvirtual.android.BaltiVirtualFragment;
import com.balitvirtual.android.BaltiVirtualFragmentListener;
```

Implement the listener by first modifying your class declaration to implement the BaltiVirtualFragmentListenter and adding a BaltiVirtualFragment member
```
public class MainActivity implements BaltiVirtualFragmentListener {

    ...
    
    private BaltiVirtualFragment baltiVirtualFragment;
```
Then implement the BaltiVirtualFragmentListener methods inside your Activity
```
    @Override
    protected void onResume() {
        super.onResume();
        if (this.baltiVirtualFragment != null)
            this.baltiVirtualFragment.OnActivityResume();
    }

    @Override
    public void onConfigurationChanged(Configuration newConfig)
    {
        super.onConfigurationChanged(newConfig);
        if (this.baltiVirtualFragment != null)
            this.baltiVirtualFragment.OnActivityConfigurationChanged(newConfig);
    }

    @Override
    public void onWindowFocusChanged(boolean hasFocus)
    {
        super.onWindowFocusChanged(hasFocus);
        if (this.baltiVirtualFragment != null)
            this.baltiVirtualFragment.OnActivityWindowFocusChanged(hasFocus);
    }

    @Override
    public void onLowMemory()
    {
        super.onLowMemory();
        if (this.baltiVirtualFragment != null)
            this.baltiVirtualFragment.OnActivityLowMemory();
    }

    @Override
    public void onTrimMemory(int level)
    {
        super.onTrimMemory(level);
        if (level == TRIM_MEMORY_RUNNING_CRITICAL)
        {
            if (this.baltiVirtualFragment != null)
                this.baltiVirtualFragment.OnActivityTrimMemory(level);

        }
    }

    @Override
    public boolean dispatchKeyEvent(KeyEvent event)
    {
        if (event.getAction() == KeyEvent.ACTION_MULTIPLE)
            if (baltiVirtualFragment != null)
                return baltiVirtualFragment.OnActivityDispatchKeyEvent(event);

        return super.dispatchKeyEvent(event);
    }


    @Override
    public boolean onKeyUp(int keyCode, KeyEvent event) {

        if (this.baltiVirtualFragment != null)
            return this.baltiVirtualFragment.OnActivityKeyUp(event);

        return super.onKeyUp(keyCode, event);
    }

    @Override
    public boolean onKeyDown(int keyCode, KeyEvent event) {

        if (this.baltiVirtualFragment != null)
            return this.baltiVirtualFragment.OnActivityKeyDown(event);

        return super.onKeyDown(keyCode, event);
    }

    @Override
    public boolean onTouchEvent(MotionEvent event) {

        if (this.baltiVirtualFragment != null)
            return this.baltiVirtualFragment.OnActivityTouchEvent(event);

        return super.onTouchEvent(event);
    }

    /*API12*/
    public boolean onGenericMotionEvent(MotionEvent event) {

        if (this.baltiVirtualFragment != null)
            return this.baltiVirtualFragment.OnActivityGenericMotionEvent(event);

        return super.onGenericMotionEvent(event);
    }
```

Finally, get the reference to the fragment that was created earlier in your layout inside your Activity's OnCreate method
```
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        
        ...
        this.baltiVirtualFragment = (BaltiVirtualFragment)getSupportFragmentManager()
                .findFragmentById(R.id.baltivirtualfragment);
        ...
    }
        
```

## Assets Setup

Place the assets folder provided to you by BaltiVirtual inside the "app/src/main" folder of your project.