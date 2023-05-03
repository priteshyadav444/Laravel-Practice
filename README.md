# Table Insertion of Data
  ## Make sure allow fillable or guard property in model

# Polymorphic Relationship 
  it has Similar to one to One, One to Many, Many to Many but
  More Than One Table make relationship in a single table.

  For Ex. Post Have Images, User Have Profile Images. 
  both table will store thier images in a same table. 
  this table have one extra attribute 
  image type profile and user images.

# Making Model inside Folder with Factory
  ## php artisan make:Model Master/TicketReason -fm
  return [
              'firstname' => fake()->name(),
              'lastname' => fake()->name(),
              'email' => fake()->unique()->safeEmail(),
              'password' => '$2y$10$92IXUNpkjO0rOQ5byMi.Ye4oKoEa3Ro9llC/.og/at2.uheWG/igi',
              'description' => fake()->paragraph(1, false),
              'account_status' => fake()->randomElement(['active', 'inactive']),
          ];



# Laravel Seeder and Factory
  ## you may use the --class option to specify a specific seeder class to run individually:
  php artisan db:seed --class=UserSeeder

  ## droping all table and re-running seeder
  php artisan migrate:fresh --seed
  php artisan migrate:fresh --seed --seeder=UserSeeder

  ## Making Factory 
  php artisan make:factory PostFactory
  php artisan make:factory AddressFactory --model="App\\Address" // for existing model

  ## Relationship Faker Generator ( Seeder )
  - User::factory()->count(2)->has(Project::factory(10), 'createdProjects')->create();
  - User::factory()->count(2)->hasCreatedProjects(3, function ($attributes, User $user) {
              return ['name' => fake()->word() . " - By " . $user->firstname];
      })->create();

  
# Define Scope
  ## local scopes
  public function scopeActive(EloquentBuilder $query): void
  {
            $query->where('account_status', 'active');
  }
  $users = User::active('admin')->get();
  ## scope method should be called using lower letter

  - Dynamic Scopes with paramater
    public function scopeOfType(Builder $query, string $type): void
    {
        $query->where('type', $type);
    }
    $users = User::ofType('admin')->get();
# Environment Key Encryption
- Key .......................................................................................... base64:S2Qn3yAj3Awc+mXBywTU8LFa+1VcWhFdjmrr+hGQvaw=
- Cipher ............................................................................................................................... AES-256-CBC
- Encrypted file ........................................................................................ C:\xampp\htdocs\example-app\.env.encrypted

# Autoloader in config foldeer
- providers Config Files

# How to handle Multiple Table fetching in Laravel. (Normalized tables data)

# Table Creation
  1) Cascade On References
  2) Seeder
  3) Relenship data
  4) pivot table naming convention (alphabetical).
  5) Give Cascade on Foreign Key

# Laravel  Tinker laravel in Command Promot
 - php artisan tinker


# For Large Data Return with pagination


# Take a Backup of database before running command like
 - php artisan migrate:refresh/fresh

# Set timezone UTC in application and convert every time whenever date is used as per local setting

# Create A Cache Every On Production for each Things.

# Always Clear Cache on System Changes (In Production)

# Do dump auto load before using php artisan tinker
	composer dump-autoload
	php artisan tinker


# Laravel Collection
