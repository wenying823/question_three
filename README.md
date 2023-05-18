# question_three

 Laravel 當中的 middleware 能夠在進入 controller 和離開 controller 後提供額外的操作，參考 官方文件
。若換成自己設計類似的 middleware ，請描述一下會如何設計以及設計的做法。注意：不是如何使用
middleware，而是假設自己為 laravel 作者，設計 middleware 供他人使用

<br><br>

1.在app/http/Middleware下創建一個LogRequestMiddleware <br>
2.為了要讓使用者能使用我們的自訂midedleware，所以須在app/http/kernel.php下的$routeMiddleware完成 <br>
```
protected $routeMiddleware = [
    // 其他中介層
    'log.request' => \App\Http\Middleware\LogRequestMiddleware::class,
];
```
3.在創建LogRequestMiddleware下，必須```use Illuminate\Contracts\Http\Kernel;``` <br>
4.使用者就可以透過route or Controller使用我們的middleware了。
```
Route::get('/example', function () {
    // 使用 log.request 中介層
})->middleware('log.request');
```
