---
layout: post
title:  浅谈Android中的网络请求HttpUrlConnettion 
date:   2017-1-19 15:08:00 +0800
categories: Android
tag: 网络请求
---

* content
{:toc}

1.几种常见的网络请求方式
=====================
- GET： 请求指定的页面信息，它本质就是发送一个请求来取得服务器上的某一资源。资源通过一组HTTP头和呈现数据（如HTML文本，或者图片或者视频等）返回给客户端。GET请求中，永远不会包含呈现数据。 

- HEAD： 只请求页面的首部,HEAD和GET本质是一样的，区别在于HEAD不含有呈现数据，而仅仅是HTTP头信息，用于检查对象是否存在，以及得到对象的元数据。   

- POST： 向服务器提交数据,请求服务器接受所指定的文档作为对所标识的URI的新的从属实体。  

- PUT： 从客户端向服务器传送的数据取代指定的文档的内容,PUT和POST极为相似，都是向服务器发送数据，但它们之间有一个重要**区别**，PUT通常指定了资源的存放位置，而POST则没有，POST的数据存放位置由服务器自己决定。 

- DELETE： 请求服务器删除指定的页面或某一个资源。 

- OPTIONS： 允许客户端查看服务器的性能。   

- TRACE： 请求服务器在响应中的实体主体部分返回所得到的内容。  

- PATCH： 实体中包含一个表，表中说明与该URI所表示的原内容的区别，用于部分文档更改。
 
- MOVE： 请求服务器将指定的页面移至另一个网络地址。  

- COPY： 请求服务器将指定的页面拷贝至另一个网络地址。  

- LINK： 请求服务器建立链接关系。  

- UNLINK： 断开链接关系。   

- WRAPPED： 允许客户端发送经过封装的请求。   

- Extension-mothed：在不改动协议的前提下，可增加另外的方法

**根据HTTP协议的设计初衷，不同的方法对资源有不同的操作方式**
- PUT 

- DELETE ：删

- POST：改

- GET：查

提示：最常用的是GET和POST（实际上GET和POST都能办到增删改查）

**GET和POST的区别使用：**
（1）如果要传递大量数据，比如文件上传，只能用POST请求
（2）GET的安全性比POST要差些，如果包含机密\敏感信息，建议用POST
（3）如果仅仅是索取数据（数据查询），建议使用GET
（4）如果是增加、修改、删除数据，建议使用POST 


2.使用HttpURLConnection进行网络请求的过程：
==================================

Uses of this class follow a pattern:

1 Obtain a new HttpURLConnection by calling URL.openConnection() and casting the result to HttpURLConnection.

2 Prepare the request. The primary property of a request is its URI. Request headers may also include metadata such as credentials, preferred content types, and session cookies.

3 Optionally upload a request body. Instances must be configured withsetDoOutput(true) if they include a request body. Transmit data by writing to the stream returned by getOutputStream() .

4 Read the response. Response headers typically include metadata such as the response body's content type and length, modified dates and session cookies. The response body may be read from the stream returned by getInputStream() . If the response has no body, that method returns an empty stream.

5 Disconnect. Once the response body has been read, the HttpURLConnection should be closed by calling disconnect() . Disconnecting releases the resources held by a connection so they may be closed or reused.

从上述使用描述中，可以知道，用户要根据返回的outputStream向服务器端写数据；而读数据的时候，要根据服务器端返回的inputStream，从这个输入流中读取服务器端返回的数据。所以，传递数据，通过返回的输出流；读数据，要通过返回的输入流。这些都是暴露给用户使用。相对于HttpClient，这要底层些。





3.[GET和POST的区别](http://blog.csdn.net/luxiaoshuai/article/details/4248188)
============

form提交的第一步是创建数据集，并根据 ENCTYPE 指定的类型值对数据集进行编码。 ENCTYPE 有两个值：multipart/form-data，application/x-www-form-urlencoded（默认值）。form提交的第二步是进行数据传输。对于GET方法，数据集使用application/x-www-form-urlencoded编码；而对于POST方法，数据集的 ENCTYPE 可以指定。

4.Android中的网络请求示例代码（Coding）
===================

4.1 Get请求
-------------

	// Get方式请求  
	public static void requestByGet() throws Exception {  
	    String path = "https://reg.163.com/logins.jsp?id=helloworld&pwd=android";  
	    // 新建一个URL对象  
	    URL url = new URL(path);  
	    // 打开一个HttpURLConnection连接  
	    HttpURLConnection urlConn = (HttpURLConnection) url.openConnection();  
	    // 设置连接超时时间  
	    urlConn.setConnectTimeout(5 * 1000);  
	    // 开始连接  
	    urlConn.connect();  
	    // 判断请求是否成功  
	    if (urlConn.getResponseCode() == HTTP_200) {  
	        // 获取返回的数据  
	        byte[] data = readStream(urlConn.getInputStream());  
	        Log.i(TAG_GET, "Get方式请求成功，返回数据如下：");  
	        Log.i(TAG_GET, new String(data, "UTF-8"));  
	    } else {  
	        Log.i(TAG_GET, "Get方式请求失败");  
	    }  
	    // 关闭连接  
	    urlConn.disconnect();  
	}

4.2 Post请求
-------------  

		// Post方式请求  
	public static void requestByPost() throws Throwable {  
	    String path = "https://reg.163.com/logins.jsp";  
	    // 请求的参数转换为byte数组  
	    String params = "id=" + URLEncoder.encode("helloworld", "UTF-8")  
	            + "&pwd=" + URLEncoder.encode("android", "UTF-8");  
	    byte[] postData = params.getBytes();  
	    // 新建一个URL对象  
	    URL url = new URL(path);  
	    // 打开一个HttpURLConnection连接  
	    HttpURLConnection urlConn = (HttpURLConnection) url.openConnection();  
	    // 设置连接超时时间  
	    urlConn.setConnectTimeout(5 * 1000);  
	    // Post请求必须设置允许输出  
	    urlConn.setDoOutput(true);  
	    // Post请求不能使用缓存  
	    urlConn.setUseCaches(false);  
	    // 设置为Post请求  
	    urlConn.setRequestMethod("POST");  
	    urlConn.setInstanceFollowRedirects(true);  
	    // 配置请求Content-Type  
	    urlConn.setRequestProperty("Content-Type",  
	            "application/x-www-form-urlencode");  
	    // 开始连接  
	    urlConn.connect();  
	    // 发送请求参数  
	    DataOutputStream dos = new DataOutputStream(urlConn.getOutputStream());  
	    dos.write(postData);  
	    dos.flush();  
	    dos.close();  
	    // 判断请求是否成功  
	    if (urlConn.getResponseCode() == HTTP_200) {  
	        // 获取返回的数据  
	        byte[] data = readStream(urlConn.getInputStream());  
	        Log.i(TAG_POST, "Post请求方式成功，返回数据如下：");  
	        Log.i(TAG_POST, new String(data, "UTF-8"));  
	    } else {  
	        Log.i(TAG_POST, "Post方式请求失败");  
	    }  
	}  

5.Java项目中的网络请求示例（聚合数据demo）
=================================
	
	package com.pxy.test;
	
	import java.io.BufferedReader;
	import java.io.DataOutputStream;
	import java.io.IOException;
	import java.io.InputStream;
	import java.io.InputStreamReader;
	import java.io.UnsupportedEncodingException;
	import java.net.HttpURLConnection;
	import java.net.URL;
	import java.net.URLEncoder;
	import java.util.HashMap;
	import java.util.Map;
	
	import net.sf.json.JSONObject;
	
	public class HttpTest {
		public static final String DEF_CHATSET = "UTF-8";//字符编码
		/**
		 * ConnectTimeout只有在网络正常的情况下才有效，
		 * 而当网络不正常时，ReadTimeout才真正的起作用，即IdIOHandlerStack 里的 WaitFor
		 * 是受ReadTimeout限制的， 因此，这2个属性应该结合实用。
		 */
		public static final int DEF_CONN_TIMEOUT = 30000;// 是建立连接的超时时间
		public static final int DEF_READ_TIMEOUT = 30000;// 是传递数据的超时时间。
		/**
		 * User Agent中文名为用户代理，简称 UA，它是一个特殊字符串头，使得服务器能够识别客户使用的操作系统及版本、 CPU
		 * 类型、浏览器及版本、浏览器渲染引擎、浏览器语言、浏览器插件等。
		 */
		public static String userAgent = "Mozilla/5.0 (Windows NT 6.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/29.0.1547.66 Safari/537.36";
	
		// 配置您申请的KEY
		public static final String APPKEY = "36f505a1967ff95cb7e3719903c501ef";
	
		public static void main(String[] args) {
			getRequest4();
		}
	
		/**
		 * 
		 * @param strUrl
		 *            请求地址
		 * @param params
		 *            请求参数
		 * @param method
		 *            请求方法
		 * @return 网络请求字符串
		 * @throws Exception
		 */
		public static String doHttpRequest(String strUrl, Map<String, Object> params, String method) throws Exception {
			HttpURLConnection conn = null;
			BufferedReader reader = null;
			String rs = null;
			try {
				StringBuffer sb = new StringBuffer();
				if (method == null || method.equals("GET")) {
					strUrl = strUrl + "?" + urlencode(params);
				}
				URL url = new URL(strUrl);
				conn = (HttpURLConnection) url.openConnection();
				if (method == null || method.equals("GET")) {
					conn.setRequestMethod("GET");
				} else {
					conn.setRequestMethod("POST");
					conn.setDoOutput(true);
				}
				conn.setRequestProperty("User-agent", userAgent);
				conn.setUseCaches(false);
				conn.setConnectTimeout(DEF_CONN_TIMEOUT);
				conn.setReadTimeout(DEF_READ_TIMEOUT);
				conn.setInstanceFollowRedirects(false);
				conn.connect();
				if (params != null && method.equals("POST")) {
					try {
						DataOutputStream out = new DataOutputStream(conn.getOutputStream());
						out.writeBytes(urlencode(params));
					} catch (Exception e) {
						e.printStackTrace();
					}
				}
				InputStream is = conn.getInputStream();
				reader = new BufferedReader(new InputStreamReader(is, DEF_CHATSET));
				String strRead = null;
				while ((strRead = reader.readLine()) != null) {
					sb.append(strRead);
				}
				rs = sb.toString();
			} catch (IOException e) {
				e.printStackTrace();
			} finally {
				if (reader != null) {
					reader.close();
				}
				if (conn != null) {
					conn.disconnect();
				}
			}
			return rs;
		}
	
		// 将map型转为请求参数型
		public static String urlencode(Map<String, Object> data) {
			StringBuilder sb = new StringBuilder();
			for (Map.Entry i : data.entrySet()) {
				try {
					sb.append(i.getKey()).append("=").append(URLEncoder.encode(i.getValue() + "", "UTF-8")).append("&");
				} catch (UnsupportedEncodingException e) {
					e.printStackTrace();
				}
			}
			return sb.toString();
		}
		
		
	
		// 1.按更新时间查询笑话
		public static void getRequest1() {
			String result = null;
			String url = "http://japi.juhe.cn/joke/content/list.from";// 请求接口地址
			Map<String, Object> params = new HashMap<String, Object>();// 请求参数
			params.put("sort", "");// 类型，desc:指定时间之前发布的，asc:指定时间之后发布的
			params.put("page", "");// 当前页数,默认1
			params.put("pagesize", "");// 每次返回条数,默认1,最大20
			params.put("time", "1418816972");// 时间戳（10位），如：1418816972
			params.put("key", APPKEY);// 您申请的key
	
			try {
				result = doHttpRequest(url, params, "GET");
				JSONObject object = JSONObject.fromObject(result);
				if (object.getInt("error_code") == 0) {
					System.out.println(object.get("result"));
				} else {
					System.out.println(object.get("error_code") + ":" + object.get("reason"));
				}
			} catch (Exception e) {
				e.printStackTrace();
			}
		}
	
		// 2.最新笑话
		public static void getRequest2() {
			String result = null;
			String url = "http://japi.juhe.cn/joke/content/text.from";// 请求接口地址
			Map<String, Object> params = new HashMap<String, Object>();// 请求参数
			params.put("page", "");// 当前页数,默认1
			params.put("pagesize", "");// 每次返回条数,默认1,最大20
			params.put("key", APPKEY);// 您申请的key
	
			try {
				result = doHttpRequest(url, params, "GET");
				JSONObject object = JSONObject.fromObject(result);
				if (object.getInt("error_code") == 0) {
					System.out.println(object.get("result"));
				} else {
					System.out.println(object.get("error_code") + ":" + object.get("reason"));
				}
			} catch (Exception e) {
				e.printStackTrace();
			}
		}
	
		// 3.按更新时间查询趣图
		public static void getRequest3() {
			String result = null;
			String url = "http://japi.juhe.cn/joke/img/list.from";// 请求接口地址
			Map<String, Object> params = new HashMap<String, Object>();// 请求参数
			params.put("sort", "");// 类型，desc:指定时间之前发布的，asc:指定时间之后发布的
			params.put("page", "");// 当前页数,默认1
			params.put("pagesize", "");// 每次返回条数,默认1,最大20
			params.put("time", "");// 时间戳（10位），如：1418816972
			params.put("key", APPKEY);// 您申请的key
	
			try {
				result = doHttpRequest(url, params, "GET");
				JSONObject object = JSONObject.fromObject(result);
				if (object.getInt("error_code") == 0) {
					System.out.println(object.get("result"));
				} else {
					System.out.println(object.get("error_code") + ":" + object.get("reason"));
				}
			} catch (Exception e) {
				e.printStackTrace();
			}
		}
	
		// 4.最新趣图
		public static void getRequest4() {
			String result = null;
			String url = "http://japi.juhe.cn/joke/img/text.from";// 请求接口地址
			Map<String, Object> params = new HashMap<String, Object>();// 请求参数
			params.put("page", "");// 当前页数,默认1
			params.put("pagesize", "");// 每次返回条数,默认1,最大20
			params.put("key", APPKEY);// 您申请的key
	
			try {
				result = doHttpRequest(url, params, "GET");
				JSONObject object = JSONObject.fromObject(result);
				if (object.getInt("error_code") == 0) {
					System.out.println(object.get("result"));
				} else {
					System.out.println(object.get("error_code") + ":" + object.get("reason"));
				}
			} catch (Exception e) {
				e.printStackTrace();
			}
		}

	}

[JSONObject解析jar包下载地址](http://dl.download.csdn.net/down10/20131127/980e4f4b4be08464539c270645c557f6.rar?response-content-disposition=attachment%3Bfilename%3D%22json.rar%22&OSSAccessKeyId=9q6nvzoJGowBj4q1&Expires=1484801774&Signature=nXixtHcPPq3KE%2FNVE7w8CI6Cupo%3D)