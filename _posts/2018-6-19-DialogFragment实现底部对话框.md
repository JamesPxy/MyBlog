---
layout: post
title: "DialogFragment实现底部弹框"
date:   2018-6-19 11:27 +0800
categories: Android
tag: DialogFragment
---

* content
{:toc}

1.第一种比较常用：设置style样式：
-----------

    <style name="Animation" parent="@android:style/Animation">
        <item name="android:windowEnterAnimation">@anim/push_bottom_in</item>
        <item name="android:windowExitAnimation">@anim/push_bottom_out</item>
    </style>

    <style name="DialogFragmentTheme" parent="Theme.AppCompat.Light.NoActionBar">
        <item name="android:windowBackground">@android:color/transparent</item>
        <item name="android:colorBackgroundCacheHint">@null</item>
        <item name="android:windowFrame">@null</item>
        <item name="android:windowContentOverlay">@null</item>
        <item name="android:windowAnimationStyle">@null</item>
        <item name="android:backgroundDimEnabled">false</item>
        <item name="android:windowIsTranslucent">true</item>
        <item name="android:windowNoTitle">true</item>
 		<!--   如果开启此属性，dialog会带有默认的padding值
        <item name="android:windowIsFloating">true</item>  -->
 		<item name="android:windowAnimationStyle">@style/Animation</item>
    </style>

在onCreate中设置此style即可：

    class CommentDialogFragment : DialogFragment() {

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setStyle(DialogFragment.STYLE_NORMAL, R.style.DialogFragmentTheme)
    }

    override fun onCreateView(inflater: LayoutInflater?, container: ViewGroup?, savedInstanceState: Bundle?): View? {
        return inflater?.inflate(R.layout.fragment_show_comment, container, false)
    }

    companion object {
        fun show(fragmentManager: FragmentManager) {
            val ft = fragmentManager.beginTransaction()
            val prev = fragmentManager.findFragmentByTag(CommentDialogFragment::class.java.simpleName)
            if (prev != null) {
                ft.remove(prev)
            }
            ft.addToBackStack(null)
            val newFragment = CommentDialogFragment()
            newFragment.show(ft, CommentDialogFragment::class.java.simpleName)

        }
    }
	}


2.在onStart()中设置弹框属性来底部弹框
-----------------------
    
public class ShowCommentFragment extends DialogFragment {

    @Override
    public void onCreate(@Nullable Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setStyle(DialogFragment.STYLE_NORMAL, R.style.AddPublicPraiseDialogTheme);
    }

    @Override
    public void onStart() {
        super.onStart();
        Window window = getDialog().getWindow();
        WindowManager.LayoutParams params = window.getAttributes();
        //设置Gravity
        params.gravity = Gravity.BOTTOM;
        params.width = WindowManager.LayoutParams.MATCH_PARENT;
        window.setAttributes(params);
        // 用透明颜色替换掉系统自带背景
        int color = ContextCompat.getColor(getActivity(), android.R.color.transparent);
        window.setBackgroundDrawable(new ColorDrawable(color));
    }


    @Nullable
    @Override
    public View onCreateView(LayoutInflater inflater, @Nullable ViewGroup container, @Nullable Bundle savedInstanceState) {
        return inflater.inflate(R.layout.fragment_show_comment, container);
    }

	}

