# 2020/02/03

## Android Accessbility 
[reference](http://woowabros.github.io/experience/2020/01/30/app-for-everyone.html)

### 1. 대체 텍스트
- contentDescription 은 눈으로 읽히는 모든 정보를 음성으로 읽어줄 수 있는 대체 텍스트를 표현 한다
- Button 과 ClickListner 가 붙은 ImageView 에는 "ㅇㅇ 버튼" 이라고 읽어준다

~~~ xml
<!-- for example -->
<ImageView
    android:id="@+id/userPhotoImageView"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:contentDescription="@string/cd_profile_image_change"
    android:src="@drawable/bg_user_thumbnail_pressed_selector" />
~~~

### 2. 상세히 설명하기
- AccessibilityNodeInfoCompat (api level 22 부터 지원) 사용하기
- **hintScript** 를 통해 원하는 내용을 변경
~~~ kotlin
fun setAccessibilityClickActionHintScript(view: View, hintScript: String?) {
    if (isTalkbackOn) {
        view.setAccessibilityDelegate(object : View.AccessibilityDelegate() {
            override fun onInitializeAccessibilityNodeInfo(host: View, info: AccessibilityNodeInfo) {
                super.onInitializeAccessibilityNodeInfo(host, info)
                val infoCompat = AccessibilityNodeInfoCompat.wrap(info)
                val clickAction = AccessibilityActionCompat(AccessibilityNodeInfoCompat.ACTION_CLICK, hintScript)
                infoCompat.addAction(clickAction)
            }
        })
    }
}
~~~
- 특정값이 변경되었을때, 변경 여부를 유저에게 알려주려면 AccessibilityEvent 를 announce 로 설정한 후 전송
~~~kotlin
fun sendAccessibilityEvent(text: String?) {
    if (isTalkbackOn) {
        val e = AccessibilityEvent.obtain()
        e.eventType = AccessibilityEvent.TYPE_ANNOUNCEMENT
        e.className = context.javaClass.getName()
        e.packageName = context.packageName
        e.text.add(text)
        manager.sendAccessibilityEvent(e)
    }
}
~~~
