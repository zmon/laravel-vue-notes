
From [Simple and Easy Laravel Routing
](https://scotch.io/tutorials/simple-and-easy-laravel-routing#basic-pages-basic-routing)

````
    // ===============================================
    // STATIC PAGES ==================================
    // ===============================================

    // show a static view for the home page (app/views/home.blade.php)
    Route::get('/', function()
    {
        return View::make('home');
    });

    // about page (app/views/about.blade.php)
    Route::get('about', function()
    {
        return View::make('about');
    });

    // work page (app/views/work.blade.php)
    Route::get('work', array('as' => 'work', function()
    {
        return View::make('work');
    }));

````



Also 
* [A Laravel controller to serve Static pages](https://gist.github.com/juliobitencourt/3693d9eefad5fd1e0a57)
* https://www.packtpub.com/mapt/book/web_development/9781786462084/4/ch04lvl1sec33/adding-a-static-page
