## Crash ##
**Crash，即程序运行错误导致崩溃，，意味着进程结束，jvm虚拟机运行终止，表现为应用闪退，不同定制化的系统表现出的提示不一样，一般会有对话框弹出提示**<br/>![Android N 应用crash之后的提示](https://i.imgur.com/8HJXncw.png)


导致原因：
1. 未捕获的运行时异常
2. 内存溢出错误，申请的内存大于应用最大的可运行内存
3. native层造成的crash

**运行时异常统一处理**<br/>通过Thread.UncaughtExceptionHandler类来实现运行时异常的统一处理，当然这个只能捕获到java层的Crash
````
Thread.setDefaultUncaughtExceptionHandler(new Thread.UncaughtExceptionHandler() {
	@Override
	public void uncaughtException(Thread t, Throwable e) {
	}
});
````

**内存溢出 – OutOfMemoryError**<br/>出现内存溢出的情况多半是内存泄漏导致的，内存泄漏的排查方法有很多MAT工具等，待后续补充~~~~

**NativeCrash**<br/>Google BreakPad

## ANR ##