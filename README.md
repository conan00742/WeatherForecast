# Simple Weather App using Retrofit + Rxjava 2 + MVP + Dagger 2


This is a simple practice app for those who try to find out the combination of

  - Retrofit (loading API)
  - Rxjava 2 (handle stream)
  - Model - View - Presenter
  - Dagger 2 (DI framework)

# Retrofit library

build.gradle app level
```sh
dependencies{
...
//retrofit
compile 'com.squareup.retrofit2:retrofit:2.3.0'
compile 'com.squareup.retrofit2:converter-gson:2.3.0'
...
}

```



> Retrofit turns your HTTP API into a Java interface.


Usage: 

```java
@GET("data/2.5/weather") 
Observable<Weather> getWeatherInfo(@Query("q") String cityName, @Query("APPID") String apiKey);
```

Reference: http://square.github.io/retrofit/

# RxJava 2

build.gradle app level
```sh
//lambda expression 
android {
    ...
    defaultConfig {
        ...
        jackOptions {
            enabled true
        }
    }

    ...

    compileOptions {
        targetCompatibility 1.8
        sourceCompatibility 1.8
    }
}


dependencies{
...
//rxjava2
compile 'io.reactivex.rxjava2:rxjava:2.0.1'
compile 'io.reactivex.rxjava2:rxandroid:2.0.1'
compile 'com.jakewharton.retrofit:retrofit2-rxjava2-adapter:1.0.0'
...
}

```

Usage: 

```java
Observable<Weather> observable = weatherApi.getWeatherInfo(cityName, API_KEY);


...


private CompositeDisposable mCompositeDisposable;

...

Disposable disposable = repository.getWeatherInfo(cityName)
                .subscribeOn(Schedulers.io())
                .observeOn(AndroidSchedulers.mainThread())
                .subscribe(weather1 -> {
                            mWeatherView.hideProgressBar();
                            mWeatherView.showWeatherInfo(weather1);
                        }, throwable -> {
                        mWeatherView.hideProgressBar();
                        mWeatherView.showNoWeatherInfo();
                });

 mCompositeDisposable.add(disposable);
```


Reference: https://github.com/ReactiveX/RxJava/wiki/What's-different-in-2.0

# Dagger 2

build.gradle app level
```sh
dependencies{
...
//retrofit
compile 'com.google.dagger:dagger:2.11'
annotationProcessor 'com.google.dagger:dagger-compiler:2.11'
...
}

```


Reference: https://google.github.io/dagger/


# Weather API
https://openweathermap.org/api

I used this
![N|Solid](https://image.prntscr.com/image/Ao2Ew-XoT8yBquO5trY4BQ.png)

Once you get your API key, put it into this

```java
WeatherRemoteDataSource.java

public class WeatherRemoteDataSource implements WeatherDataSource {

    //put it here
    private final static String API_KEY = "YOUR_API_KEY_HERE";

    ...
}

```


# MVP Architecture

Please read it here: https://github.com/googlesamples/android-architecture/tree/todo-mvp


#Project Structure

![N|Solid](https://image.prntscr.com/image/MV4LONduSVuCBixqKXKFSw.png)








