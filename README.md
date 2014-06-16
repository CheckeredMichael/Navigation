[![Build Status](https://travis-ci.org/cmfcmf/OpenWeatherMap-PHP-Api.svg?branch=master)](https://travis-ci.org/cmfcmf/OpenWeatherMap-PHP-Api)

This is a dynamic navigation which will be used within my Admin package. Feel free to fork this and try it out for yourself.
  If you have any problems then please feel free to ask me any questions. This can be implemented into any package, but I will
  release some documentation later on once I have used it with my admin package.

  I would like to thank [Josh Benham](https://github.com/joshbenham) for his help and support. (He did create this himself,
  I have just stolen it from him with permission, but will hope to make it my own).
  
  To install, place "checkeredmichael/navigation": "0.1", to your require part in composer.json.
  
  To use the package within another package, you should create an events.php where your routes are and add...
  
  ```php
  <?php
  Event::listen('admin.menu.build', function($menu){
    $menu->add('index', 'Index', URL::route('Admin::index.index'), 1, 'dashboard');
    $menu->add('users', 'Users', URL::route('Admin::users.index'), 100, 'users');
  });
  ```
  You should add this to every package that needs to build onto the navigation system, obviously you should edit each menu item as required.
  If this doesn't make any sense, then please feel free to contact me on Github (username: CheckeredMichael).
  
  Then in your ServiceProvider.php add...
  
  ```php
  <?php
  include __DIR__.'/../../events.php';
  ```
  
  This will set you up with using the dynamic navigation. All you need to do now is wherever you're using the navigation to show to people,
  add this to you're blade if that's what you are using...
  
  ```php
  <?php
    use Checkeredmichael\Navigation\Services\Menu;
  ?>

  <nav>
    {{
    Menu::create(function($menu) {
        Event::fire('admin.menu.build', $menu);
    })->render();
    }}
  </nav>
  ```
  
  You should now have your dynamic navigation up and running, please feel free to report any bugs or contribute with updates.