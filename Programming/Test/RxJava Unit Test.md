# 2020/02/11

## RxJava2 with Unit Test  [(reference)](https://proandroiddev.com/rxjava-2-unit-testing-tips-207887d3f15c)

~~~java
//example
Observable<String> getData() {
    return dummyService.getDataFromServer();
}
~~~
### 1. Test Emissions
~~~java
@Test
public void getData() {
    // Preparation: mock DummyService
    MainTabViewModel.DummyService dummyService = Mockito.mock(MainTabViewModel.DummyService.class);
    
    Mockito.doReturn(Observable.just("one", "two"))
          .when(dummyService)
          .getDataFromServer();

    // Trigger
    TestObserver<String> testObserver = viewModel.getData(dummyService).test();

    // Validation
    testObserver.assertValues("one", "two");
    // clean up
    testObserver.dispose(); // Pro-tip: don't forget this
}

// compact version
viewModel.getData(dummyService)
        .test()
        .assertValues("one", "two")
        .dispose();
~~~

### 2. Testing Subscription
~~~java
Observable<Integer> doReps() {
    return Observable.interval(1L, 5L, TimeUnit.SECONDS, getSchedulerIo())
            .flatMapSingle(ignored -> fetchDataRemote());
}

Single<Integer> fetchDataRemote() {
    // ...
}

Scheduler getSchedulerIo() {
    return Schedulers.io();
}
~~~

~~~java
@Test
public void doReps() {
  // Make sure you are swapping the actual Scheduler with our TestScheduler object here
  TestScheduler testScheduler = new TestScheduler();
  
  Mockito.doReturn(testScheduler)
          .when(viewModel)
          .getSchedulerIo();
  // Other preparations
  Mockito.doReturn(Single.just(123))
          .when(viewModel)
          .fetchDataRemote();

  // Read carefully, this is very important
  TestObserver<Integer> testObserver = viewModel.doReps()
          .subscribeOn(testScheduler)
          .observeOn(testScheduler)
          .test();

  testObserver.assertNotTerminated() // not compulsory, but STRONGLY recommended
          .assertNoErrors()
          .assertValueCount(0);// "time" hasn't started so no value expected

  testScheduler.advanceTimeBy(1L, TimeUnit.SECONDS);
  testObserver.assertValueCount(1);// 1 value expected after the initial delay of 1 second
  testScheduler.advanceTimeBy(5L, TimeUnit.SECONDS);
  testObserver.assertValueCount(2);// 1st interval, 1 more value expected
  testScheduler.advanceTimeBy(5L, TimeUnit.SECONDS);
  testObserver.assertValueCount(3);// 2nd interval, 1 more value

  // Clean up resources, not compulsory, but STRONGLY recommended
  testObserver.dispose();
}
~~~

### 3. Bonus
  1. Always **test termination** to prevent memory leak
  2. Always dispose your test subscriber
  3. use a "SchedulerProvider" (Dependency Inversion)


