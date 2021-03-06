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

### 4 Performing Insert Operation Synchronously in the Main Thread
```
public void adduseToRealm_Sync(View view){
  String name = e.getText().toString();
  int age = Integer.valueOf(a.getText().toString());
  ...
  myRealm.beginTransaction();
  SocialAccount sa = myRealm.createObject(SocialAccount.class);
  sa.setName();
  User user = myrealm.createObject(User.class, id);
  user.setSocialAccount(sa);
  myRealm.commitTransaction();
}
```

#### 5:05
```
catch{
  myRealm.cancelTransaction();
}
```

#### 06:45
set all var to final,
```
myRealm.executeTransaction(new Realm.Transaction(){
  @Override
  public void execute(Realm realm){
    
  }
}
  }
})
```

### 5 Inserting Data to Realm Asychronously in the Background Thread
```
executeTransactionAsync
```
#### 05:23
```
task = myRealm...
if(realmAsyncTask!=null && !realmSayncTask.isCancelled()){
  realmAsyncTask.cancel();
}
```


### 6 Writing Simple Query to Fetch Records from Realm
```
RealmResults<User> userList = myRealm.where(User.class).findAll();
```

### 7 Using Realm Browser App to Check Realm Database Content
find realm file: Tools->Android->Android device monitor->file explorer->data->data->proj->files  

### 8 Understanding @RealmClass Annotation
#### 02:00
```
sa.isvalid();
RealmObject.isValid(user);
```

```
@RealmClass
public class User implements RealmModel
```


## 5. Performing Query, Update, and Delete Operation
### 2 Writing Query using Fluid interface
```
RealmQuery<User> realmQuery = myRealm.where(User.class);
RealmResults<User> userList = realmQuery.findAll();
realmQuery.greaterThen("age",10);
realmQuery.contains("name","john");
```
### 3 Using Predicate to Filter Search Results
### 4 Performing Update and Delete Operations on Realm Records

## 6. Creating an App Using Realm


## 7. Exploring Miscellaneous Realm Concepts
### 7 Upgrading Realm Schema and Applying Migration
```
import io.realm.DynamicRealm;
import io.realm.RealmMigration;
import io.realm.RealmSchema;

public class MyMig implements RealmMigraion{
   @Override
   public void migrate(DynamicRealm realm, long oldVersion, long newVersion){
    RealmSchema schema = realm.getSchema();
    if(oldVersion ==0){
      RealmObjectSchema userSchema = schema.get("User");
      userSchema.addField("hobby",String.class,FieldAttribute.REQUIRED);
      oldVersion++;
    }
   }
}
```

#### 04:33
MyApplication.java
```
public class MyApplication extends Application{
  @Override
  public void onCreate(){
    Realm.init(this);
    RealmConfiguration configuration = new RealmConfiguration.Builder()
    .name(".realm")
    .modules(new MyCustomModule())
    .schemaVersion(0)
    .migration(new MyMigration())
    .build();
    
    Realm.setDefaultConfiguraion(configuration);
  }
}
```
