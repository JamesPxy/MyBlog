---
layout: post
title: Android 使用webP图片相关
date:   2017-2-21 14:18:00 +0800
categories: Android
tag: 技术栈
---

* content
{:toc}



1.【腾讯Bugly干货分享】WebP原理和Android支持现状介绍
----------------------------------------------------
 原文链接：

[【腾讯Bugly干货分享】WebP原理和Android支持现状介绍](http://www.cnblogs.com/bugly/p/6061434.html)


2.[使用NDK技术对Webp图片进行操作的demo（支持Android低版本)](http://download.csdn.net/download/jiwangkailai02/6637013)
---------------------------------------------------------

此demo为编译webP官网提供源码生产so文件，demo里面本地图片存放位置在raw文件里，放在drawable文件下会有问题，主要在于打包压缩之后不能解码里面的图片获取到输出流。

对应文章介绍博客：

[支持Android4.0以下webp的使用](http://blog.csdn.net/jiwangkailai02/article/details/17015451)


3.[ Android Webp 完全解析 快来缩小apk的大小吧](http://blog.csdn.net/lmj623565791/article/details/53240600)
-------------------------------
	来自于鸿祥大神的博客介绍。


4.附上几个关键的代码片（part 3对应代码）：
----------------------

4.1 webP解码器


    	package me.everything.webp;
		
		import android.graphics.Bitmap;
		
		import java.nio.ByteBuffer;
		
		public class WebPDecoder {
		    private static WebPDecoder instance = null;
		
		    private WebPDecoder() {
		        System.loadLibrary("webp_evme");
		    }
		
		    public static WebPDecoder getInstance() {
		        if (instance == null) {
		            synchronized (WebPDecoder.class) {
		                if (instance == null) {
		                    instance = new WebPDecoder();
		                }
		            }
		        }
		
		        return instance;
		    }
		
		    public Bitmap decodeWebP(byte[] encoded) {
		        return decodeWebP(encoded, 0, 0);
		    }
		
		    public Bitmap decodeWebP(byte[] encoded, int w, int h) {
		        int[] width = new int[]{w};
		        int[] height = new int[]{h};
		
		        byte[] decoded = decodeRGBAnative(encoded, encoded.length, width, height);
		        if (decoded.length == 0) return null;
		
		        int[] pixels = new int[decoded.length / 4];
		        ByteBuffer.wrap(decoded).asIntBuffer().get(pixels);
		
		        return Bitmap.createBitmap(pixels, width[0], height[0], Bitmap.Config.ARGB_8888);
		    }
		
		    public static native byte[] decodeRGBAnative(byte[] encoded, long encodedLength, int[] width, int[] height);
		}


4.2  重写imageview

		
		/**
		 * A {@link ImageView} with WebP support </p>
		 * Use to load WebP resources to ImageView from View decleration in layout xmls </p>
		 * <me.everything.webp.WebPImageView
		 *     android:layout_width="wrap_content"
		 *     android:layout_height="wrap_content"
		 *     webp:webp_src="@drawable/your_webp_image" />
		 */
		public class WebpImageView extends ImageView {
		
		    /**
		     * Native WEBP support with lossless and transparency is officially supported in Android 4.2.1+.
		     * Before that it was without transparency. Since we can only safely check for SDK version we
		     * and 4.2 and 4.2.x are SDK version 17 will use SDK 18 (Android 4.3 and above).
		     */
		    public static final boolean NATIVE_WEB_P_SUPPORT = Build.VERSION.SDK_INT >= Build.VERSION_CODES.JELLY_BEAN_MR2;
		
		    public WebpImageView(Context context) {
		        super(context);
		        init(context, null);
		    }
		
		    public WebpImageView(Context context, AttributeSet attrs) {
		        super(context, attrs);
		        init(context, attrs);
		    }
		
		    public WebpImageView(Context context, AttributeSet attrs, int defStyle) {
		        super(context, attrs, defStyle);
		        init(context, attrs);
		    }
		
		    private void init(Context context, AttributeSet attrs) {
		        TypedArray a = context.obtainStyledAttributes(attrs, R.styleable.webp);
		
		        int webpSourceResourceID = a.getResourceId(R.styleable.webp_webp_src, 0);
		        a.recycle();
		
		        InputStream inputStream = getResources().openRawResource(webpSourceResourceID);
		        byte[] bytes = streamToBytes(inputStream);
		        Bitmap bitmap = null;
		
		        // Prefer the BitmapFactory decoder on post JB_MR2 OSs
		        if (!NATIVE_WEB_P_SUPPORT) {
		            bitmap = WebPDecoder.getInstance().decodeWebP(bytes);
		        } else {
		            bitmap = BitmapFactory.decodeByteArray(bytes, 0, bytes.length);
		        }
		        this.setImageBitmap(bitmap);
		    }
		
		    private static byte[] streamToBytes(InputStream is) {
		        ByteArrayOutputStream baos = new ByteArrayOutputStream();
		        int i = -1;
		        try {
		            byte[] bytes = new byte[1024];
		            while ((i = is.read(bytes)) != -1) {
		                baos.write(bytes, 0, i);
		                bytes = new byte[1024];
		            }
		            return baos.toByteArray();
		        } catch (Exception e) {
		        }
		        return null;
		    }
		}

