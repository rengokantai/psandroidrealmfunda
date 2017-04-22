# psandroidrealmfunda
## 4. Setting up Realm
### 2 Setting up Realm
#### 07:32
MyApplication.java
```
import android.app.Application
import io.realm.Realm;
import io.realm.Real

public class MyApplication extends Application{
  @Override
  public void onCreate(){
    super.onCreate();
    Realm.init(this);
    RealmConfiguration configuration = new RealmConfiguration.Builder().name("a.realm").build();
    
    Realm.setDefaultConfiguraion(configuration);
  }
}
```
MainActivity.java
```
private Realm myRealm;
protected void onCreate(Bundle savedInstanceState){
  myRealm = Realm.getDefaultInstance();
}
```
