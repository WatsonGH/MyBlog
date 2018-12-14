1.获取应用最大可运行内存

	ActivityManager am = (ActivityManager) context.getSystemService(Context.ACTIVITY_SERVICE);
	int memoryClass = am.getMemoryClass();
	if (hasHoneycomb() && isLargeHeap(context)) {
		memoryClass = getLargeMemoryClass(am);
	}

	private static boolean hasHoneycomb() {
		return Build.VERSION.SDK_INT >= Build.VERSION_CODES.HONEYCOMB;
	}

	@TargetApi(Build.VERSION_CODES.HONEYCOMB)
	private static boolean isLargeHeap(Context context) {
		return (context.getApplicationInfo().flags & ApplicationInfo.FLAG_LARGE_HEAP) != 0;
	}


-------

2.android 6.0直接弃用了HttpClient 要想继续使用，可以添加下面配置

	android {
		// 继续使用HttpClient
		useLibrary 'org.apache.http.legacy'
	}


