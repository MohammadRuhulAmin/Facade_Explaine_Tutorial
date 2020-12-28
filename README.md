# Facade_Explaine_Tutorial

Step=> 1)
Make a Folder Larademo then make a file Larademo.php 
Step=>2)
inside Larademo.php file give 
<?php
    namespace App\Larademo;
    class Larademo {
        public function sayHello(){
            echo "Hi from Custome Facade";
        }
    }

Step=>3)

now make a Service Provider with a command : 
php artisan make:provider LarademoServiceProvider

this command will create a service provider inside App\Providers;

Step=>4)

Inside LarademoServiceProvider.php 
we have to add a statement ->
use App\Larademo\Larademo; 
then inside
public function  register(){
    // bind the class
    $this->app->bind('larademo',function(){ // 'larademo has to be  small case!'
       return new Larademo();  // Larademo() == is a constructor!!
    });
} 

Step=>5)

Now we have to go to config/app.php 
inside providers =>
    register ->
    App\Providers\LarademoServiceProvider::class,



Step=>6)

Inside the same folder (Larademo), We have to Create FacadeFile naming LarademoFacade.php.

Step=>7)

Inside LarademoFacade.php 
Provide namespace and <?php;

<?php namespace App\Larademo;

class LarademoFacade extends Facade {
    protected static function getFacadeAccessor(){
        return 'larademo'; // this larademo was inside LarademoServiceProvider app->bind('larademo'),

    }
}

Step=>8)

again =>
config/app.php 
inside alices => register 

'Larademo'=>App\Larademo\LarademoFacade::class;


------------------------Finish----------------------------
