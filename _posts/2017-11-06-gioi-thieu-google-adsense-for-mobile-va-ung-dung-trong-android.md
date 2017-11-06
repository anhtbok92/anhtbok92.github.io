---
layout: entry
title: Giới thiệu về Google Adsense for Mobile và ứng dụng trong Android
author: Nguyễn Tuấn Anh
author-email: victory1080@gmail.com
description: Google AdMob thực chất là quảng cáo Adsense, nó là nền tảng quảng cáo trên thiết bị di động nên được gọi là AdMob (viết tắt Adsense for Mobile).
---

**Google AdMob** thực chất là quảng cáo Adsense, nó là nền tảng quảng cáo trên thiết bị di động nên được gọi là AdMob (viết tắt **Adsense for Mobile**).

Khi người dùng có ứng dụng sẽ đăng ký tài khoản **Google Adsense** và chọn mục** AdMob** để tham gia và nhúng vào phần mềm của mình. Nó rất hữu ích khi bạn publish một ứng dụng free và vẫn muốn có thu nhập từ ứng dụng đó. Trong bài viết này, chúng ta sẽ tìm hiểu làm cách nào để tích hợp được **AdMob** vào ứng dụng Android của bạn.

Trước tiên vào vấn đề chính, chúng ta cần phải tìm hiểu một vài khái niệm và cách thức quảng cáo của **Google AdMob**.

- **Advertiser**: Người hay công ty muốn đăng quảng cáo.
- **Publisher**: bản thân chúng ta – những người hay đội ngũ xây dựng ứng dụng.
- **Admob**: Chính là của **Google**, một tổ chức uy tín giúp đảm bảo sự công bằng giữa người cần quảng cáo và người muốn có thu nhập chính đáng từ quảng cáo đó.

Quảng cáo của **AdMob** dùng** CPC** (Cost-Per-Click), tức là chi phí cho mỗi lần click chuột. 0.2 USD là mức giá trung bình thấp của các nước cho 1 click.

Riêng tại Việt Nam, những nhà phát triển game chỉ nhận được 1/10 trong tổng 0.2 USD. Một ví dụ rất rõ ràng gần đây có thể nhận thấy việc thu nhập khủng khiếp từ quảng cáo, chính là game Flappy Bird. Theo thống kê, Flappy Bird đã có trên 50 triệu lượt tải về, 47.000 lượt nhận xét trên App Store.

Điều này đồng nghĩa với mỗi ngày tác giả của game này sẽ có khoảng 10 triệu người dùng kích hoạt chơi game của anh. Một con số đáng ngưỡng mộ!!!

### 1. Các loại quảng cáo – **Banner** và **Interstitial**

**Banner**: là loại quảng cáo sẽ chiếm 1 phần nhỏ của màn hình ứng dụng của bạn, nó thường được đặt ở dưới cùng hoặc trên cùng của ứng dụng

![Adsense Banner](https://drive.google.com/uc?id=0B05rqFCwNCjkOTc1d0xQNUQwUUE&export=download)

**Interstitial**: là loại quảng cáo sẽ chiếm toàn bộ màn hình của ứng dụng, Interstitial sẽ block toàn bộ ứng dụng của bạn, và đặt quảng cáo bao phủ lên ứng dụng.

![Adsense Interstitial](https://drive.google.com/uc?id=0B05rqFCwNCjkWWhMMzZ3SGhnMTQ&export=download)

### 2. Lấy ID AdMob

**Bước 1**: Đăng nhập Google AdMob bằng tài khoản Google của bạn.

![B1](https://drive.google.com/uc?id=0B05rqFCwNCjkTC1xb01qQkNKYU0&export=download)

**Bước 2**: Click vào tab Kiếm Tiền

![B2](https://drive.google.com/uc?id=0B05rqFCwNCjkZmd1S2hfMzZDY0E&export=download)
 
**Bước 3**: Lựa chọn App hoặc tạo 1 app mới và lựa chọn nền tảng cho APP (có **Android, IOS, Windows Phone 8**).

**Bước 4**: Lựa chọn các kiểu hiển thị quảng cáo.

![B4](https://drive.google.com/uc?id=0B05rqFCwNCjkSkNMRWRHTExVY28&export=download)

**Bước 5**: Một đơn vị quảng cáo đã được tạo, bạn có thể nhận thấy Ad unit ID hiện ở thanh dashboard. Lúc đó đã thành công.

![B5](https://drive.google.com/uc?id=0B05rqFCwNCjkbU9Id0FIb0NiazQ&export=download)

### 3. Gắn AdMob vào ứng dụng Android

**Bước 1**: Tạo 1 project mới trong Android Studio từ File => New Project. Ta chọn mặc định Empty Activity và thực hiện next.

**Bước 2**: Mở build.gradle và thêm dependency play services AdMob

```
dependencies {
    compile fileTree(dir: 'libs', include: ['*.jar'])
    testCompile 'junit:junit:4.12'
    compile 'com.android.support:appcompat-v7:23.1.1'
    compile 'com.android.support:design:23.1.1'
    compile 'com.google.android.gms:play-services-ads:8.4.0'
}
```

**Bước 3**: Mở file `string.xml` ở `res/values` và add 2 loại quảng cáo của chúng ta:  Banner and Interstitial.

```xml
<resources>
    <string name="app_name">AdMob</string>
    <string name="title_activity_second_activiy">Interstitial</string>
    <string name="msg_welcome">Welcome to Admob. Click on the below button to launch the Interstitial ad.</string>
    <string name="btn_fullscreen_ad">Show Fullscreen Ad</string>
    <string name="banner_home_footer">ca-app-pub-3385728256506859</string>
    <string name="interstitial_full_screen">ca-app-pub-3385728256506859</string>
</resources>
```

**Bước 4**: Mở `AndroidManifest.xml` và thêm các quyền như bên dưới.

- Add INTERNET & ACCESS_NETWORK_STATE permissions.
- Add google play services version meta-data.
- Add the AdActivity adding configChanges and theme attributes.

```xml
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="anhtbok.vnlab.admob">
 
    <uses-permission android:name="android.permission.INTERNET" />
    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
 
    <application
        android:allowBackup="true"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:supportsRtl="true"
        android:theme="@style/AppTheme">
 
        <meta-data
            android:name="com.google.android.gms.version"
            android:value="@integer/google_play_services_version" />
 
        <activity android:name=".MainActivity">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />
 
                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
 
        <activity
            android:name="com.google.android.gms.ads.AdActivity"
            android:configChanges="keyboard|keyboardHidden|orientation|screenLayout|uiMode|screenSize|smallestScreenSize"
            android:theme="@android:style/Theme.Translucent" />
    </application>
 
</manifest>
```

#### 1.1. Thêm Banner Ad cho ứng dụng

Banner Ad sẽ chiếm 1 phần của màn hình. Mình sẽ add thêm 1 banner ad vào trong phía dưới cùng của main activity.

Ngoài ra, bạn cần thêm `com.google.android.gms.ads.AdView` tới XML Layout của bạn.

```xml
<com.google.android.gms.ads.AdView
    android:id="@+id/adView"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    ads:adSize="BANNER"
    ads:adUnitId="@string/banner_home_footer">
</com.google.android.gms.ads.AdView>
```

Mở file `main_activity` <layout chính của ứng dụng> và thêm phần code XML cho AdView. Bạn nên để nó cuối cùng sau các thành phần khác vì nó sẽ hiển thị dưới cùng của màn hình chính.

```xml
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    xmlns:ads="http://schemas.android.com/apk/res-auto"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:paddingBottom="@dimen/activity_vertical_margin"
    android:paddingLeft="@dimen/activity_horizontal_margin"
    android:paddingRight="@dimen/activity_horizontal_margin"
    android:paddingTop="@dimen/activity_vertical_margin"
    tools:context="anhtbok.vnlab.admob.MainActivity">
 
    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/msg_welcome" />
 
    <Button android:id="@+id/btn_fullscreen_ad"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_centerInParent="true"
        android:text="@string/btn_fullscreen_ad"/>
 
    <com.google.android.gms.ads.AdView
        android:id="@+id/adView"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_centerHorizontal="true"
        android:layout_alignParentBottom="true"
        ads:adSize="BANNER"
        ads:adUnitId="@string/banner_home_footer">
    </com.google.android.gms.ads.AdView>
</RelativeLayout>
```

Mở file `MainActivity.java` và thêm như sau:

```java
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_main);

    mAdView = (AdView) findViewById(R.id.adView);
    AdRequest adRequest = new AdRequest.Builder()
            .build();
    mAdView.loadAd(adRequest);

    btnFullscreenAd = (Button) findViewById(R.id.btn_fullscreen_ad);
    btnFullscreenAd.setOnClickListener(new View.OnClickListener() {
        @Override
        public void onClick(View v) {
            startActivity(new Intent(MainActivity.this, SecondActivity.class));
        }
    });
}
```

Chạy app và thấy ứng dụng hiển thị quảng cáo?

#### 1.2. Thêm Interstitial Ad (Quảng cáo fullscreen) cho ứng dụng.

Interstitial sẽ chiếm toàn bộ màn hình của ứng dụng. Thêm Interstitial không yêu cầu AdView ở XML Layout. Chúng ta sẽ load nó từ `MainActivity`.

Tạo 1 activity mới.

```java
package anhtbok.vnlab.admob;
 
import android.os.Bundle;
import android.support.v7.app.AppCompatActivity;
import android.widget.Toast;
 
import com.google.android.gms.ads.AdListener;
import com.google.android.gms.ads.AdRequest;
import com.google.android.gms.ads.InterstitialAd;
 
public class SecondActivity extends AppCompatActivity {
    private String TAG = SecondActivity.class.getSimpleName();
    InterstitialAd mInterstitialAd;
 
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_second);
 
        mInterstitialAd = new InterstitialAd(this);
 
        // set the ad unit ID
        mInterstitialAd.setAdUnitId(getString(R.string.interstitial_full_screen));
 
        AdRequest adRequest = new AdRequest.Builder()
                .build();
 
        // Load ads into Interstitial Ads
        mInterstitialAd.loadAd(adRequest);
 
        mInterstitialAd.setAdListener(new AdListener() {
            public void onAdLoaded() {
                showInterstitial();
            }
        });
    }
 
    private void showInterstitial() {
        if (mInterstitialAd.isLoaded()) {
            mInterstitialAd.show();
        }
    }
}
```

Chạy app và bạn sẽ thấy interstitial ad xuất hiện.

### Kết luận

Hy vọng với những chia sẻ về Google AdMob và các hướng dẫn đăng ký và cách gắn quảng cáo vào ứng dụng của bạn, bạn sẽ kiếm được tiền từ những ứng dụng free của bản thân :).