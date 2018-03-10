## Laravel version 5.5 LTE - always prefere LTE version

> Clear full cache

```
php artisan cache:clear
php artisan route:cache
php artisan view:clear
php artisan config:cache
```

> create controller

```php artisan make:controller UserController --resource
```
> create authentication

```
php artisan make:auth
```

> Create migration

```
php artisan migrate [migrate all migration files] it will crfeate three table
```

> create seeder to insert dummy data

```
php artisan make:seeder UsersTableSeeder
```

> uncomment in default DatabaseSeeder file // add require all seeder class here
> add below code into created new UsersTableSeeder

```DB::table('users')->insert([
		'name' => 'dinesh',
		'email' => 'dinesh@gmail.com',
		'password' => bcrypt('123123'),
	]);
```	
		
> usercontroller for the auth test

```
use Illuminate\Support\Facades\Auth;
class UserController extends Controller
{
	/**
	 * Display a listing of the resource.
	 *
	 * @return \Illuminate\Http\Response
	 */
	public function index(Request $request)
	{
		$email=$_POST["email"];
		$password=$_POST["password"];
		if (Auth::attempt(['email' => $email, 'password' => $password])) {
			// Authentication passed...
			//print_r(Auth::User());
			echo 200;
		}
		else
		{
			print_r("fail");
		}
	}
}
```

```
php artisan make:controller dashboardController --resource
```

>create custome middleware

```
php artisan make:middleware IsLogin

```

>set middleware into route
````
Route::middleware(['Islogin'])->group(function () 
{
	Route::get('/dashboard', 'DashboardController@index');
});
```

> Open kernel.php in app/http folder

```
protected $routeMiddleware = [
	'Islogin' => \App\Http\Middleware\Islogin::class,
];	
```


		