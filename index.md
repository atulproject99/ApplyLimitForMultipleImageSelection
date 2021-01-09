## Please Read Carefully before use this library
1.Add it in your root build.gradle at the end of repositories:
allprojects {
		repositories {
			...
			maven { url 'https://jitpack.io' }
		}
	}
2.Add the dependency

dependencies {
	        implementation 'com.github.atulproject99:ApplyLimitForMultipleImageSelection:1.0'
	}
 
## Add Permission in your manifest.xml

<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE"/>
    <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
    
 ## Add tools:replace="android:theme" in Application tag in manifest.xml
 
   <application
        android:allowBackup="true"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:roundIcon="@mipmap/ic_launcher_round"
        android:supportsRtl="true"
        android:theme="@style/Theme.CheckApplication2"
        tools:replace="android:theme"
        >
        </application>
    
 ## Add this line in your manifest.xml
 
 <activity
            android:name="atul.maurya773.testapplication.activities.AlbumSelectActivity"
            android:theme="@style/MultipleImageSelectTheme">
            <intent-filter>
                <category android:name="android.intent.category.DEFAULT" />
            </intent-filter>
        </activity>
    


## Check permission in your activity on click and then send intent 

## Write this code in button click funtion

button.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
              if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.M) {
            if(checkSelfPermission(Manifest.permission.READ_EXTERNAL_STORAGE)!= PackageManager.PERMISSION_GRANTED)
            {
                requestPermissions(new String[]{Manifest.permission.READ_EXTERNAL_STORAGE},1001);
                return;

            }
        }
        
//set limit on number of images that can be selected, default is 10
        Intent intent = new Intent(this, AlbumSelectActivity.class);
        intent.putExtra(Constants.INTENT_EXTRA_LIMIT, 2);
        startActivityForResult(intent, Constants.REQUEST_CODE);
                
            }
        });




## Override onActivityResult and write this code

@Override
protected void onActivityResult(int requestCode, int resultCode, Intent data) {
  if (requestCode == Constants.REQUEST_CODE && resultCode == RESULT_OK && data != null) {
    //The array list has the image paths of the selected images
    ArrayList<Image> images = data.getParcelableArrayListExtra(Constants.INTENT_EXTRA_IMAGES);
    ...  
}
  
  
  
 ## For custom theme do somechanging in code
 
 <color name="multiple_image_select_primary">#2E7D32</color>
    <color name="multiple_image_select_primaryDark">#1B5E20</color>
    <color name="multiple_image_select_primaryLight">#C8E6C9</color>
    <color name="multiple_image_select_accent">#4CAF50</color>
    <color name="multiple_image_select_primaryText">#212121</color>
    <color name="multiple_image_select_secondaryText">#727272</color>
    <color name="multiple_image_select_divider">#B6B6B6</color>
    <color name="multiple_image_select_toolbarPrimaryText">#FFFFFF</color>
    <color name="multiple_image_select_albumTextBackground">#99FFFFFF</color>
    <color name="multiple_image_select_imageSelectBackground">#000000</color>
    <color name="multiple_image_select_buttonText">#FFFFFF</color>
</resources>


## And make some changes in in AlbumSelectActivity and ImageSelectActivity


# Paste this code
  tools:replace="android:theme"
    android:theme="@style/OverrideMultipleImageSelectTheme"


