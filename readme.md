# arquillian-java-ee-7-primefaces-5

This repository shows a minimal setup code needed to use arquillian functional testing.

I followed these:

1. [Arquillian Guides - Getting Started](http://arquillian.org/guides/getting_started/)
2. [Arquillian Guides - Getting Started: Rinse and Repeat](http://arquillian.org/guides/getting_started_rinse_and_repeat/)
3. [Arquillian Guides - Functional Testing using Drone and Graphene](http://arquillian.org/guides/functional_testing_using_graphene/)
4. Some parts of [ARQUILLIAN – THE ALIENS ARE INVADING](http://rpestano.wordpress.com/2014/06/08/arquillian/)


The work is based on [java-ee-7-primefaces-5](https://github.com/cilf/java-ee-7-primefaces-5) example.

I'm deploying it remotely to Wildfly 8.1.0.Final using IntelliJ IDEA 13.1.5

## Some troubles that I ran into

### Incompatible firefox version

You always need to check which firefox version is compatible with your version of selenium in it's [changelog](http://selenium.googlecode.com/git/java/CHANGELOG). For that reason I needed to use firefox v31 because the latest v32 had some troubles connecting to selenium v2.43.1.

```
org.openqa.selenium.firefox.NotConnectedException: Unable to connect to host 127.0.0.1 on port 7055 after 45000 ms. Firefox console output:
```

**Solution:** check selenium's [changelog](http://selenium.googlecode.com/git/java/CHANGELOG) and download appropriate firefox version from [here](http://ftp.mozilla.org/pub/mozilla.org/firefox/releases/).

### java.lang.RuntimeException: Could not create new instance of class org.jboss.arquillian.graphene.enricher.SeleniumResourceProvider$BrowserConnectionProvider

```
java.lang.RuntimeException: Could not create new instance of class org.jboss.arquillian.graphene.enricher.SeleniumResourceProvider$BrowserConnectionProvider
	at org.jboss.arquillian.core.impl.loadable.SecurityActions.newInstance(SecurityActions.java:160)
	at org.jboss.arquillian.core.impl.loadable.ServiceRegistryLoader.createServiceInstance(ServiceRegistryLoader.java:103)
	at org.jboss.arquillian.core.impl.loadable.ServiceRegistryLoader.all(ServiceRegistryLoader.java:55)
	at org.jboss.arquillian.graphene.location.ContextRootStoreInitializer.getContextRoot(ContextRootStoreInitializer.java:52)
	at org.jboss.arquillian.graphene.location.ContextRootStoreInitializer.setupLocationForClass(ContextRootStoreInitializer.java:47)
	at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
	at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:57)
	at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
	at org.jboss.arquillian.core.impl.ObserverImpl.invoke(ObserverImpl.java:94)
	at org.jboss.arquillian.core.impl.EventContextImpl.invokeObservers(EventContextImpl.java:99)
	at org.jboss.arquillian.core.impl.EventContextImpl.proceed(EventContextImpl.java:81)
	at org.jboss.arquillian.core.impl.ManagerImpl.fire(ManagerImpl.java:145)
	at org.jboss.arquillian.core.impl.ManagerImpl.fire(ManagerImpl.java:116)
	at org.jboss.arquillian.core.impl.EventImpl.fire(EventImpl.java:67)
	at org.jboss.arquillian.test.impl.TestInstanceEnricher.enrich(TestInstanceEnricher.java:48)
	at org.jboss.arquillian.container.test.impl.ClientTestInstanceEnricher.enrich(ClientTestInstanceEnricher.java:51)
	at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
	at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:57)
	at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
	at org.jboss.arquillian.core.impl.ObserverImpl.invoke(ObserverImpl.java:94)
	at org.jboss.arquillian.core.impl.EventContextImpl.invokeObservers(EventContextImpl.java:99)
	at org.jboss.arquillian.core.impl.EventContextImpl.proceed(EventContextImpl.java:81)
	at org.jboss.arquillian.container.test.impl.client.ContainerEventController.createContext(ContainerEventController.java:142)
	at org.jboss.arquillian.container.test.impl.client.ContainerEventController.createBeforeContext(ContainerEventController.java:124)
	at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
	at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:57)
	at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
	at org.jboss.arquillian.core.impl.ObserverImpl.invoke(ObserverImpl.java:94)
	at org.jboss.arquillian.core.impl.EventContextImpl.proceed(EventContextImpl.java:88)
	at org.jboss.arquillian.test.impl.TestContextHandler.createTestContext(TestContextHandler.java:102)
	at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
	at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:57)
	at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
	at org.jboss.arquillian.core.impl.ObserverImpl.invoke(ObserverImpl.java:94)
	at org.jboss.arquillian.core.impl.EventContextImpl.proceed(EventContextImpl.java:88)
	at org.jboss.arquillian.test.impl.TestContextHandler.createSuiteContext(TestContextHandler.java:65)
	at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
	at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:57)
	at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
	at org.jboss.arquillian.core.impl.ObserverImpl.invoke(ObserverImpl.java:94)
	at org.jboss.arquillian.core.impl.EventContextImpl.proceed(EventContextImpl.java:88)
	at org.jboss.arquillian.test.impl.TestContextHandler.createClassContext(TestContextHandler.java:84)
	at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
	at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:57)
	at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
	at org.jboss.arquillian.core.impl.ObserverImpl.invoke(ObserverImpl.java:94)
	at org.jboss.arquillian.core.impl.EventContextImpl.proceed(EventContextImpl.java:88)
	at org.jboss.arquillian.core.impl.ManagerImpl.fire(ManagerImpl.java:145)
	at org.jboss.arquillian.core.impl.ManagerImpl.fire(ManagerImpl.java:116)
	at org.jboss.arquillian.test.impl.EventTestRunnerAdaptor.before(EventTestRunnerAdaptor.java:95)
	at org.jboss.arquillian.junit.Arquillian$5.evaluate(Arquillian.java:258)
	at org.junit.runners.ParentRunner.runLeaf(ParentRunner.java:325)
	at org.junit.runners.BlockJUnit4ClassRunner.runChild(BlockJUnit4ClassRunner.java:77)
	at org.junit.runners.BlockJUnit4ClassRunner.runChild(BlockJUnit4ClassRunner.java:56)
	at org.junit.runners.ParentRunner$3.run(ParentRunner.java:290)
	at org.junit.runners.ParentRunner$1.schedule(ParentRunner.java:71)
	at org.junit.runners.ParentRunner.runChildren(ParentRunner.java:288)
	at org.junit.runners.ParentRunner.access$000(ParentRunner.java:58)
	at org.junit.runners.ParentRunner$2.evaluate(ParentRunner.java:268)
	at org.jboss.arquillian.junit.Arquillian$2.evaluate(Arquillian.java:193)
	at org.jboss.arquillian.junit.Arquillian.multiExecute(Arquillian.java:345)
	at org.jboss.arquillian.junit.Arquillian.access$200(Arquillian.java:49)
	at org.jboss.arquillian.junit.Arquillian$3.evaluate(Arquillian.java:207)
	at org.junit.runners.ParentRunner.run(ParentRunner.java:363)
	at org.jboss.arquillian.junit.Arquillian.run(Arquillian.java:155)
	at org.junit.runner.JUnitCore.run(JUnitCore.java:137)
	at com.intellij.junit4.JUnit4IdeaTestRunner.startRunnerWithArgs(JUnit4IdeaTestRunner.java:74)
	at com.intellij.rt.execution.junit.JUnitStarter.prepareStreamsAndStart(JUnitStarter.java:211)
	at com.intellij.rt.execution.junit.JUnitStarter.main(JUnitStarter.java:67)
	at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
	at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:57)
	at com.intellij.rt.execution.application.AppMain.main(AppMain.java:134)
Caused by: java.lang.reflect.InvocationTargetException
	at sun.reflect.NativeConstructorAccessorImpl.newInstance0(Native Method)
	at sun.reflect.NativeConstructorAccessorImpl.newInstance(NativeConstructorAccessorImpl.java:57)
	at sun.reflect.DelegatingConstructorAccessorImpl.newInstance(DelegatingConstructorAccessorImpl.java:45)
	at java.lang.reflect.Constructor.newInstance(Constructor.java:526)
	at org.jboss.arquillian.core.impl.loadable.SecurityActions.newInstance(SecurityActions.java:156)
	... 79 more
Caused by: java.lang.TypeNotPresentException: Type org.openqa.selenium.html5.BrowserConnection not present
	at sun.reflect.generics.factory.CoreReflectionFactory.makeNamedType(CoreReflectionFactory.java:117)
	at sun.reflect.generics.visitor.Reifier.visitClassTypeSignature(Reifier.java:125)
	at sun.reflect.generics.tree.ClassTypeSignature.accept(ClassTypeSignature.java:49)
	at sun.reflect.generics.visitor.Reifier.reifyTypeArguments(Reifier.java:68)
	at sun.reflect.generics.visitor.Reifier.visitClassTypeSignature(Reifier.java:138)
	at sun.reflect.generics.tree.ClassTypeSignature.accept(ClassTypeSignature.java:49)
	at sun.reflect.generics.repository.ClassRepository.getSuperclass(ClassRepository.java:84)
	at java.lang.Class.getGenericSuperclass(Class.java:696)
	at org.jboss.arquillian.graphene.enricher.SeleniumResourceProvider.getTypeArgument(SeleniumResourceProvider.java:161)
	at org.jboss.arquillian.graphene.enricher.SeleniumResourceProvider.<init>(SeleniumResourceProvider.java:145)
	at org.jboss.arquillian.graphene.enricher.SeleniumResourceProvider$DirectProvider.<init>(SeleniumResourceProvider.java:171)
	at org.jboss.arquillian.graphene.enricher.SeleniumResourceProvider$DirectProvider.<init>(SeleniumResourceProvider.java:171)
	at org.jboss.arquillian.graphene.enricher.SeleniumResourceProvider$BrowserConnectionProvider.<init>(SeleniumResourceProvider.java:80)
	... 84 more
Caused by: java.lang.ClassNotFoundException: org.openqa.selenium.html5.BrowserConnection
	at java.net.URLClassLoader$1.run(URLClassLoader.java:366)
	at java.net.URLClassLoader$1.run(URLClassLoader.java:355)
	at java.security.AccessController.doPrivileged(Native Method)
	at java.net.URLClassLoader.findClass(URLClassLoader.java:354)
	at java.lang.ClassLoader.loadClass(ClassLoader.java:425)
	at sun.misc.Launcher$AppClassLoader.loadClass(Launcher.java:308)
	at java.lang.ClassLoader.loadClass(ClassLoader.java:358)
	at java.lang.Class.forName0(Native Method)
	at java.lang.Class.forName(Class.java:270)
	at sun.reflect.generics.factory.CoreReflectionFactory.makeNamedType(CoreReflectionFactory.java:114)
	... 96 more


java.lang.IllegalStateException: Unexpected callable present in Drone Context, should be already instantiated at this moment.
	at org.jboss.arquillian.drone.impl.InstanceOrCallableInstanceImpl.asInstance(InstanceOrCallableInstanceImpl.java:57)
	at org.jboss.arquillian.drone.impl.DroneEnhancer.deenhanceDrone(DroneEnhancer.java:119)
	at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
	at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:57)
	at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
	at org.jboss.arquillian.core.impl.ObserverImpl.invoke(ObserverImpl.java:94)
	at org.jboss.arquillian.core.impl.EventContextImpl.invokeObservers(EventContextImpl.java:99)
	at org.jboss.arquillian.core.impl.EventContextImpl.proceed(EventContextImpl.java:81)
	at org.jboss.arquillian.core.impl.ManagerImpl.fire(ManagerImpl.java:145)
	at org.jboss.arquillian.core.impl.ManagerImpl.fire(ManagerImpl.java:116)
	at org.jboss.arquillian.core.impl.EventImpl.fire(EventImpl.java:67)
	at org.jboss.arquillian.drone.impl.DroneDestructor.destroyClassScopedDrone(DroneDestructor.java:93)
	at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
	at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:57)
	at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
	at org.jboss.arquillian.core.impl.ObserverImpl.invoke(ObserverImpl.java:94)
	at org.jboss.arquillian.core.impl.EventContextImpl.invokeObservers(EventContextImpl.java:99)
	at org.jboss.arquillian.core.impl.EventContextImpl.proceed(EventContextImpl.java:81)
	at org.jboss.arquillian.test.impl.TestContextHandler.createSuiteContext(TestContextHandler.java:65)
	at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
	at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:57)
	at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
	at org.jboss.arquillian.core.impl.ObserverImpl.invoke(ObserverImpl.java:94)
	at org.jboss.arquillian.core.impl.EventContextImpl.proceed(EventContextImpl.java:88)
	at org.jboss.arquillian.test.impl.TestContextHandler.createClassContext(TestContextHandler.java:84)
	at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
	at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:57)
	at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
	at org.jboss.arquillian.core.impl.ObserverImpl.invoke(ObserverImpl.java:94)
	at org.jboss.arquillian.core.impl.EventContextImpl.proceed(EventContextImpl.java:88)
	at org.jboss.arquillian.core.impl.ManagerImpl.fire(ManagerImpl.java:145)
	at org.jboss.arquillian.core.impl.ManagerImpl.fire(ManagerImpl.java:116)
	at org.jboss.arquillian.test.impl.EventTestRunnerAdaptor.afterClass(EventTestRunnerAdaptor.java:87)
	at org.jboss.arquillian.junit.Arquillian$3$1.evaluate(Arquillian.java:212)
	at org.jboss.arquillian.junit.Arquillian.multiExecute(Arquillian.java:345)
	at org.jboss.arquillian.junit.Arquillian.access$200(Arquillian.java:49)
	at org.jboss.arquillian.junit.Arquillian$3.evaluate(Arquillian.java:207)
	at org.junit.runners.ParentRunner.run(ParentRunner.java:363)
	at org.jboss.arquillian.junit.Arquillian.run(Arquillian.java:155)
	at org.junit.runner.JUnitCore.run(JUnitCore.java:137)
	at com.intellij.junit4.JUnit4IdeaTestRunner.startRunnerWithArgs(JUnit4IdeaTestRunner.java:74)
	at com.intellij.rt.execution.junit.JUnitStarter.prepareStreamsAndStart(JUnitStarter.java:211)
	at com.intellij.rt.execution.junit.JUnitStarter.main(JUnitStarter.java:67)
	at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
	at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:57)
	at com.intellij.rt.execution.application.AppMain.main(AppMain.java:134)
```

**Solution:** you're missing following [dependency](http://mvnrepository.com/artifact/org.seleniumhq.selenium/selenium-common) in your pom.xml

```
<dependency>
    <groupId>org.seleniumhq.selenium</groupId>
    <artifactId>selenium-common</artifactId>
    <version>2.0b1</version>
    <scope>test</scope>
</dependency>
```

### PrimeFaces <p:commandButton/> button cannot be clicked on

```
java.lang.IllegalStateException: Can't invoke method click.
	at org.jboss.arquillian.graphene.proxy.GrapheneContextualHandler$2.call(GrapheneContextualHandler.java:214)
	at org.jboss.arquillian.graphene.context.BrowserActions.performAction(BrowserActions.java:62)
	at org.jboss.arquillian.graphene.proxy.GrapheneContextualHandler.invoke(GrapheneContextualHandler.java:205)
	at org.jboss.arquillian.graphene.proxy.GrapheneContextualHandler.intercept(GrapheneContextualHandler.java:229)
	at org.openqa.selenium.remote.RemoteWebElement$$EnhancerByGraphene$$b192d0b6.click(<generated>)
	at cz.cilf.arquillian.ViewScopedBeanTest.shouldIncreaseValue(ViewScopedBeanTest.java:72)
	at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
	at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:57)
	at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
	at org.junit.runners.model.FrameworkMethod$1.runReflectiveCall(FrameworkMethod.java:50)
	at org.junit.internal.runners.model.ReflectiveCallable.run(ReflectiveCallable.java:12)
	at org.junit.runners.model.FrameworkMethod.invokeExplosively(FrameworkMethod.java:47)
	at org.jboss.arquillian.junit.Arquillian$6$1.invoke(Arquillian.java:301)
	at org.jboss.arquillian.container.test.impl.execution.LocalTestExecuter.execute(LocalTestExecuter.java:60)
	at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
	at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:57)
	at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
	at org.jboss.arquillian.core.impl.ObserverImpl.invoke(ObserverImpl.java:94)
	at org.jboss.arquillian.core.impl.EventContextImpl.invokeObservers(EventContextImpl.java:99)
	at org.jboss.arquillian.core.impl.EventContextImpl.proceed(EventContextImpl.java:81)
	at org.jboss.arquillian.core.impl.ManagerImpl.fire(ManagerImpl.java:145)
	at org.jboss.arquillian.core.impl.ManagerImpl.fire(ManagerImpl.java:116)
	at org.jboss.arquillian.core.impl.EventImpl.fire(EventImpl.java:67)
	at org.jboss.arquillian.container.test.impl.execution.ClientTestExecuter.execute(ClientTestExecuter.java:53)
	at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
	at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:57)
	at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
	at org.jboss.arquillian.core.impl.ObserverImpl.invoke(ObserverImpl.java:94)
	at org.jboss.arquillian.core.impl.EventContextImpl.invokeObservers(EventContextImpl.java:99)
	at org.jboss.arquillian.core.impl.EventContextImpl.proceed(EventContextImpl.java:81)
	at org.jboss.arquillian.container.test.impl.client.ContainerEventController.createContext(ContainerEventController.java:142)
	at org.jboss.arquillian.container.test.impl.client.ContainerEventController.createTestContext(ContainerEventController.java:129)
	at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
	at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:57)
	at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
	at org.jboss.arquillian.core.impl.ObserverImpl.invoke(ObserverImpl.java:94)
	at org.jboss.arquillian.core.impl.EventContextImpl.proceed(EventContextImpl.java:88)
	at org.jboss.arquillian.test.impl.TestContextHandler.createSuiteContext(TestContextHandler.java:65)
	at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
	at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:57)
	at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
	at org.jboss.arquillian.core.impl.ObserverImpl.invoke(ObserverImpl.java:94)
	at org.jboss.arquillian.core.impl.EventContextImpl.proceed(EventContextImpl.java:88)
	at org.jboss.arquillian.test.impl.TestContextHandler.createTestContext(TestContextHandler.java:102)
	at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
	at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:57)
	at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
	at org.jboss.arquillian.core.impl.ObserverImpl.invoke(ObserverImpl.java:94)
	at org.jboss.arquillian.core.impl.EventContextImpl.proceed(EventContextImpl.java:88)
	at org.jboss.arquillian.test.impl.TestContextHandler.createClassContext(TestContextHandler.java:84)
	at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
	at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:57)
	at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
	at org.jboss.arquillian.core.impl.ObserverImpl.invoke(ObserverImpl.java:94)
	at org.jboss.arquillian.core.impl.EventContextImpl.proceed(EventContextImpl.java:88)
	at org.jboss.arquillian.core.impl.ManagerImpl.fire(ManagerImpl.java:145)
	at org.jboss.arquillian.test.impl.EventTestRunnerAdaptor.test(EventTestRunnerAdaptor.java:111)
	at org.jboss.arquillian.junit.Arquillian$6.evaluate(Arquillian.java:294)
	at org.jboss.arquillian.junit.Arquillian$5.evaluate(Arquillian.java:267)
	at org.junit.runners.ParentRunner.runLeaf(ParentRunner.java:325)
	at org.junit.runners.BlockJUnit4ClassRunner.runChild(BlockJUnit4ClassRunner.java:77)
	at org.junit.runners.BlockJUnit4ClassRunner.runChild(BlockJUnit4ClassRunner.java:56)
	at org.junit.runners.ParentRunner$3.run(ParentRunner.java:290)
	at org.junit.runners.ParentRunner$1.schedule(ParentRunner.java:71)
	at org.junit.runners.ParentRunner.runChildren(ParentRunner.java:288)
	at org.junit.runners.ParentRunner.access$000(ParentRunner.java:58)
	at org.junit.runners.ParentRunner$2.evaluate(ParentRunner.java:268)
	at org.jboss.arquillian.junit.Arquillian$2.evaluate(Arquillian.java:193)
	at org.jboss.arquillian.junit.Arquillian.multiExecute(Arquillian.java:345)
	at org.jboss.arquillian.junit.Arquillian.access$200(Arquillian.java:49)
	at org.jboss.arquillian.junit.Arquillian$3.evaluate(Arquillian.java:207)
	at org.junit.runners.ParentRunner.run(ParentRunner.java:363)
	at org.jboss.arquillian.junit.Arquillian.run(Arquillian.java:155)
	at org.junit.runner.JUnitCore.run(JUnitCore.java:137)
	at com.intellij.junit4.JUnit4IdeaTestRunner.startRunnerWithArgs(JUnit4IdeaTestRunner.java:74)
	at com.intellij.rt.execution.junit.JUnitStarter.prepareStreamsAndStart(JUnitStarter.java:211)
	at com.intellij.rt.execution.junit.JUnitStarter.main(JUnitStarter.java:67)
	at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
	at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:57)
	at com.intellij.rt.execution.application.AppMain.main(AppMain.java:134)
Caused by: java.lang.NoClassDefFoundError: org/openqa/selenium/android/AndroidDriver
	at org.jboss.arquillian.graphene.javascript.JavaScriptUtils.execute(JavaScriptUtils.java:42)
	at org.jboss.arquillian.graphene.javascript.DefaultExecutionResolver.executeScriptForCall(DefaultExecutionResolver.java:139)
	at org.jboss.arquillian.graphene.javascript.DefaultExecutionResolver.execute(DefaultExecutionResolver.java:78)
	at org.jboss.arquillian.graphene.javascript.JSInterfaceHandler.intercept(JSInterfaceHandler.java:58)
	at org.jboss.arquillian.graphene.cglib.ClassImposterizer$ClassWithSuperclassToWorkAroundCglibBug$$EnhancerByGraphene$$e7d884b2.clearRequestDone(<generated>)
	at org.jboss.arquillian.graphene.guard.RequestGuardFactory$1.intercept(RequestGuardFactory.java:95)
	at org.jboss.arquillian.graphene.proxy.InvocationContextImpl.invoke(InvocationContextImpl.java:87)
	at org.jboss.arquillian.graphene.enricher.SearchContextInterceptor.intercept(SearchContextInterceptor.java:50)
	at org.jboss.arquillian.graphene.proxy.InvocationContextImpl.invoke(InvocationContextImpl.java:87)
	at org.jboss.arquillian.graphene.enricher.StaleElementInterceptor$1.apply(StaleElementInterceptor.java:48)
	at org.jboss.arquillian.graphene.enricher.StaleElementInterceptor$1.apply(StaleElementInterceptor.java:44)
	at org.openqa.selenium.support.ui.FluentWait$1.apply(FluentWait.java:177)
	at org.openqa.selenium.support.ui.FluentWait$1.apply(FluentWait.java:175)
	at org.openqa.selenium.support.ui.FluentWait.until(FluentWait.java:208)
	at org.openqa.selenium.support.ui.FluentWait.until(FluentWait.java:175)
	at org.jboss.arquillian.graphene.wait.WebDriverWaitImpl.until(WebDriverWaitImpl.java:87)
	at org.jboss.arquillian.graphene.enricher.StaleElementInterceptor.intercept(StaleElementInterceptor.java:44)
	at org.jboss.arquillian.graphene.proxy.InvocationContextImpl.invoke(InvocationContextImpl.java:87)
	at org.jboss.arquillian.graphene.intercept.InterceptorBuilder$2.intercept(InterceptorBuilder.java:139)
	at org.jboss.arquillian.graphene.proxy.InvocationContextImpl.invoke(InvocationContextImpl.java:87)
	at org.jboss.arquillian.graphene.proxy.GrapheneContextualHandler$2.call(GrapheneContextualHandler.java:209)
	... 88 more
Caused by: java.lang.ClassNotFoundException: org.openqa.selenium.android.AndroidDriver
	at java.net.URLClassLoader$1.run(URLClassLoader.java:366)
	at java.net.URLClassLoader$1.run(URLClassLoader.java:355)
	at java.security.AccessController.doPrivileged(Native Method)
	at java.net.URLClassLoader.findClass(URLClassLoader.java:354)
	at java.lang.ClassLoader.loadClass(ClassLoader.java:425)
	at sun.misc.Launcher$AppClassLoader.loadClass(Launcher.java:308)
	at java.lang.ClassLoader.loadClass(ClassLoader.java:358)
	... 109 more
```

**Solution:** You're missing this [dependency](http://mvnrepository.com/artifact/org.seleniumhq.selenium/selenium-android-driver) in your pom.xml

```
<dependency>
    <groupId>org.seleniumhq.selenium</groupId>
    <artifactId>selenium-android-driver</artifactId>
    <version>2.39.0</version>
    <scope>test</scope>
</dependency>
```