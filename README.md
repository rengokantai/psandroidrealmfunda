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


### 3 Defining Model Classes and Exploring Annotations
java/me.yidi/model/User.java
```
import io.realm.RealmObject;
public class User extends RealmObject{
  @PrimaryKey
  private String id;
  private String name;
  private int age;
  private SocialAccount sa;
  
  
  @Ignore
  private String tempData; //wont be saved
}
```

#### 04:50
@PrimaryKey:
- Only one peomary key allowed in a model
