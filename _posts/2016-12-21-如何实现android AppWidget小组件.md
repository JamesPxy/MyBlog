---
layout: post
title: "Android中的AppWidget(桌面小部件）实现方式"
date:   2016-12-21 13:31:01 +0800
categories: Android
tag: Android widget
---		

		
如何编写一个AppWidget？
==========================================
	1. 编写AppWidget的布局xml界面。
	2. 编写AppWidget的元数据xml文件。
	 		  该xml中定义当前AppWidget使用的
	 		  初始化布局，以及初始化宽高。
			  70*n-30
	3. 编写AppWidget的控制器类。
	 		  要求该类继承自AppWidgetProvider.
	 		  重写父类的生命周期方法。
	4. 清单文件中配置该AppWidget。

			  <receiver android:name="com.example.android_day09_appwidget.MyAppWidget">
			<intent-filter >
			<!-- 每个AppWidget都应该有这个action -->
			<action android:name="android.appwidget.action.APPWIDGET_UPDATE"/>
			</intent-filter>
			<!-- 每个AppWidget都应该有这个name -->
			<meta-data android:name="android.appwidget.provider"
			android:resource="@xml/appwidget_meta"/>
			  </receiver>
		
AppWidgetProvider的生命周期
==========================================
		onEnable
		onUpdate
		onDeleted
		onDisabled
		
		涉及到的参数：
		AppWidgetManager
		appWidgetId
		
如何修改AppWidget中TextView的文字？
==========================================
		1>创建于AppWidget布局相同的
		  RemoteViews对象。
		2>对RemoteViews对象中的控件进行修改。
		3>manager.updateAppWidget()方法
		  更新AppWidget.
		  manager.updateAppWidget(ids,views);
		  manager.updateAppWidget(id,views);
		  
###如何给控件添加点击意图?
==========================================
		1>创建RemoteViews
		2>remoteViews.setOnClickPendingIntent()
		  告诉系统app：button  pendingIntent
		3>manager.updateAppWidget();
		
如何点击按钮后更新AppWidget的界面？
==========================================
		
1.编写AppWidget的控制器类
---------------------------------------------------------
		package com.example.androidday09appweidght;
		
		import java.util.Random;
		
		import android.app.PendingIntent;
		import android.appwidget.AppWidgetManager;
		import android.appwidget.AppWidgetProvider;
		import android.content.ComponentName;
		import android.content.Context;
		import android.content.Intent;
		import android.graphics.Color;
		import android.util.Log;
		import android.widget.RemoteViews;
		
		/**
		 * 桌面小部件的控制器
		 */
		public class MyAppWidget extends AppWidgetProvider {
		
			/**
			 * 1>每次创建AppWidget时执行
			 * 2>当自动更新时间到来时执行
			 */
			@Override
			public void onUpdate(Context context, AppWidgetManager appWidgetManager,
					int[] appWidgetIds) {
				// There may be multiple widgets active, so update all of them
				Log.i("TAG", "onUpdate...");
				final int N = appWidgetIds.length;
				for (int i = 0; i < N; i++) {
					updateAppWidget(context, appWidgetManager, appWidgetIds[i]);
				}
			}
		
			@Override
			public void onEnabled(Context context) {
				// Enter relevant functionality for when the first widget is created
				Log.i("TAG", "onEnabled...");
			}
		
			@Override
			public void onDisabled(Context context) {
				// Enter relevant functionality for when the last widget is disabled
				Log.i("TAG", "onDisabled...");
			}
		
		
			@Override
			public void onDeleted(Context context, int[] appWidgetIds) {
				Log.i("TAG", "onDeleted...");
			}
			static void updateAppWidget(Context context,
					AppWidgetManager appWidgetManager, int appWidgetId) {
				Log.i("TAG", "updateAppWidget...");
				RemoteViews  views=new RemoteViews(context.getPackageName(), R.layout.appwidght_main);
				views.setTextViewText(R.id.tv, "Hello KingJames and Pxy!");
				views.setTextColor(R.id.tv, Color.BLUE);
		
				//更新AppWidget的Button1的点击意图
				Intent intents=new Intent(context,MainActivity.class);
				PendingIntent pendingIntent=PendingIntent.getActivity(context, 100, intents, PendingIntent.FLAG_UPDATE_CURRENT);
				views.setOnClickPendingIntent(R.id.btn1, pendingIntent);
		
				//点击button2时 更新TextView颜色
				Intent intent=new Intent("ACTION_UPDATE_TEXT_COLOR");
				PendingIntent pi=PendingIntent.getBroadcast(context, 200, intent, pendingIntent.FLAG_UPDATE_CURRENT);
				views.setOnClickPendingIntent(R.id.btn2, pi);
				appWidgetManager.updateAppWidget(appWidgetId, views);
			}
		
			@Override
			public void onReceive(Context context, Intent intent) {
				//不能删  父类有事干
				super.onReceive(context, intent);
				
				if("ACTION_UPDATE_TEXT_COLOR".equals(intent.getAction())){
					//更新AppWidget中的TextView  给Views的textview设置随机颜色
					int[] colors={Color.RED,Color.WHITE,Color.GREEN,Color.GRAY,Color.YELLOW};
					//单例方法获取到manger对象
					AppWidgetManager  manger=AppWidgetManager.getInstance(context);
					ComponentName  name=new ComponentName(context, MyAppWidget.class);
					RemoteViews  views=new RemoteViews(context.getPackageName(), R.layout.appwidght_main);
					views.setTextColor(R.id.tv, colors[new Random().nextInt(colors.length)]);
					manger.updateAppWidget(name, views);
				}
			}
		}
		

2.编写AppWidget的元数据xml文件。
----------------------------------------------
  该xml中定义当前AppWidget使用的初始化布局，以及初始化宽高。           res/xml/new_app_widget_info.xml  70*n-30

		<?xml version="1.0" encoding="utf-8"?>
		<appwidget-provider xmlns:android="http://schemas.android.com/apk/res/android"
		    android:initialKeyguardLayout="@layout/appwidght_main"
		    android:initialLayout="@layout/appwidght_main"
		    android:minHeight="40dp"
		    android:minWidth="250dp"
		    android:previewImage="@drawable/ic_launcher"
		    android:resizeMode="horizontal|vertical"
		    android:updatePeriodMillis="86400000"
		    android:widgetCategory="home_screen" >
		
		</appwidget-provider>
		
		----------------------------------
3.清单文件中配置该AppWidget
----------------------------------------------
		  <receiver android:name="com.example.android_day09_appwidget.MyAppWidget">
		    <intent-filter >
		        <!-- 每个AppWidget都应该有这个action -->
		        <action android:name="android.appwidget.action.APPWIDGET_UPDATE"/>
		    </intent-filter>
		    <!-- 每个AppWidget都应该有这个name -->
		    <meta-data android:name="android.appwidget.provider"
		        android:resource="@xml/appwidget_meta"/>
		  </receiver>
		  
		  ------------------------------
		   <receiver android:name="com.example.androidday09appweidght.MyAppWidget" >
		            <intent-filter>
		                <action android:name="android.appwidget.action.APPWIDGET_UPDATE" />
		                <action android:name="ACTION_UPDATE_TEXT_COLOR"/>
		            </intent-filter>
		
		            <meta-data
		                android:name="android.appwidget.provider"
		                android:resource="@xml/new_app_widget_info" />
		        </receiver>