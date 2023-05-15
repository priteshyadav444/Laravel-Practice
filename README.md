# Environment Key Encryption

Key .......................................................................................... base64:S2Qn3yAj3Awc+mXBywTU8LFa+1VcWhFdjmrr+hGQvaw= </br>
Cipher ............................................................................................................................... AES-256-CBC </br>
Encrypted file ........................................................................................ C:\xampp\htdocs\example-app\.env.encrypted </br>


# Autoloader in config foldeer
- providers Config Files


# How to handle Multiple Table fetching in Laravel. (Normalized tables data)


# Laravel  Tinker laravel in Command Promt

# Table Creation
  1) Cascade On References
  2) Seeder
  3) Relenship data
  4) pivot table naming convention (alphabetical).
  5) Give Cascade on Foreign Key

# Table Insertion of Data
  - Make sure allow fillable or guard property in model

# Polymorphic Relationship 
  it has Similar to one to One, One to Many, Many to Many but
  More Than One Table make relationship in a single table.

  For Ex. Post Have Images, User Have Profile Images. 
  both table will store thier images in a same table. 
  this table have one extra attribute 
  image type profile and user images.

# For Large Data Return with pagination

# Making Model inside Folder with Factory
  php artisan make:Model Master/TicketReason -fm
  ```
  return [
              'firstname' => fake()->name(),
              'lastname' => fake()->name(),
              'email' => fake()->unique()->safeEmail(),
              'password' => '$2y$10$92IXUNpkjO0rOQ5byMi.Ye4oKoEa3Ro9llC/.og/at2.uheWG/igi',
              'description' => fake()->paragraph(1, false),
              'account_status' => fake()->randomElement(['active', 'inactive']),
          ];
  ```

# Take a Backup of database before running command like
 - php artisan migrate:refresh/fresh

# Set timezone UTC in application and convert every time whenever date is used as per local setting

# Create A Cache Every On Production for each Things.

# Always Clear Cache on System Changes (In Production)

# Do dump auto load before using php artisan tinker
```
	composer dump-autoload
	php artisan tinker
```

# Laravel Collection


# Laravel Seeder and Factory
- you may use the --class option to specify a specific seeder class to run individually:
  php artisan db:seed --class=UserSeeder

- droping all table and re-running seeder
```
  php artisan migrate:fresh --seed
  php artisan migrate:fresh --seed --seeder=UserSeeder
```

- Making Factory 
```
  php artisan make:factory PostFactory
  php artisan make:factory AddressFactory --model="App\\Address" // for existing model
```

- Relationship Faker Generator ( Seeder )
  - User::factory()->count(2)->has(Project::factory(10), 'createdProjects')->create();
  - User::factory()->count(2)->hasCreatedProjects(3, function ($attributes, User $user) {
              return ['name' => fake()->word() . " - By " . $user->firstname];
      })->create();

  
# Define Scope
  - local scopes
  ```
    public function scopeActive(EloquentBuilder $query): void
    {
          $query->where('account_status', 'active');
    }
  ```

  $users = User::active('admin')->get();
  scope method should be called using lower letter

  - Dynamic Scopes with paramater
    public function scopeOfType(Builder $query, string $type): void
    {
        $query->where('type', $type);
    }
    $users = User::ofType('admin')->get();



# Api Desiging
 ## Use nouns instead of verbs in endpoint paths
    - HTTP request method already has the verb
    - The verbs map to CRUD operations.
    - we should create routes like  for getting news articles. 
    
    GET /articles
    - Likewise POST  for adding a new article.
    
    POST /articles/ 
    - PUT /articles/:id is for updating the article with the given id. 
    PUT /articles/:id
    - DELETE /articles/:id is for deleting an existing article with the given ID
    DELETE /articles/:id


    ## Use logical nesting on endpoints
    - if we want an endpoint to get the comments for a news article, we should append the /comments path to the end of the /articles path.

    get('/articles/:articleId/comments'


    ## Handle errors gracefully and return standard error codes
    Common error HTTP status codes include:

    - 400 Bad Request – This means that client-side input fails validation.
    - 401 Unauthorized – This means the user isn’t not authorized to access a resource. It usually returns when the user isn’t authenticated.
    - 403 Forbidden – This means the user is authenticated, but it’s not allowed to access a resource.
    - 404 Not Found – This indicates that a resource is not found.
    - 500 Internal server error – This is a generic server error. It probably shouldn’t be thrown explicitly.
    - 502 Bad Gateway – This indicates an invalid response from an upstream server.
    - 503 Service Unavailable – This indicates that something unexpected happened on server side (It can be anything like server overload, some parts of the system failed, etc.).

    ## Allow filtering, sorting, and pagination
    - Here’s a small example where an API can accept a query string with various query parameters to let us filter out items by their fields:
    
    ```
    /employees?lastName=Smith&age=30
    http://example.com/articles?sort=+author,-datepublished
    - + means ascending and - means descending. So we sort by author’s name in alphabetical order and datepublished from most recent to least recent.
    ```
    
    - Likewise, we can accept the page query parameter and return a group of entries in the position from (page - 1) * 20 to page * 20. 
    
 ## HATEOAS and Why It’s Needed in RESTful API?
```
    # With HATEOAS, a client interacts with a network application whose application servers provide information dynamically through hypermedia. A REST client needs little to no prior knowledge about how to interact with an application or server beyond a generic understanding of hypermedia.

   HTTP/1.1 200 OK
    {
        "account": {
            "account_number": 12345,
            "balance": {
                "currency": "usd",
                "value": 100.00
            },
            "links": {
                "deposits": "/accounts/12345/deposits",
                "withdrawals": "/accounts/12345/withdrawals",
                "transfers": "/accounts/12345/transfers",
                "close-requests": "/accounts/12345/close-requests"
            }
        }
    }
```

# Laravel Passport 
 ## installation command 
   ```
   composer require laravel/passport
   php artisan migrate
   php artisan passport:install
   // After running the passport:install command, add the Laravel\Passport\HasApiTokens trait to your App\Models\User model.
   // Finally, in your application's config/auth.php configuration file, you should define an api authentication guard and set the driver option to passport. 
   ```

# Laravel 10 new features
  - Interactive cli to create Controller
  - Pennent ( for testing new features by allocating new features to specific uses)
  - Process ( Running Command in Laravel)
  - New helper function Str::password()
  - Laravel Horizen

# Laravel Form Request
  - Use for request rules method to specify validation on form data.
  - Use autrorize method to specify gates and policy

# Laravel Data Transformation and action
  - use attributes to transform data. Ex. Hasing Password. Converting dates, generting full name.
