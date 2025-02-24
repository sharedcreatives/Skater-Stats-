# Microservice Laravel App Setup

### 1. Set Up the Gateway API

1. **Install Laravel**:
    ```sh
    composer create-project --prefer-dist laravel/laravel gateway
    ```

2. **Configure Gateway**:
    - Set up routes in `routes/api.php` to forward requests to the appropriate microservices.
    - Use a package like `guzzlehttp/guzzle` for HTTP requests.

    ```php
    use Illuminate\Support\Facades\Route;
    use Illuminate\Http\Request;
    use GuzzleHttp\Client;

    Route::middleware('auth:api')->get('/skater-stats', function (Request $request) {
        $client = new Client();
        $response = $client->get('http://skater-stats-service/api/skater-stats', [
            'headers' => [
                'Authorization' => $request->header('Authorization')
            ]
        ]);

        return $response->getBody();
    });
    ```

### 2. Set Up Microservices

#### Skater Stats Service

1. **Install Laravel**:
    ```sh

user
Lets go set by step to make a mircoservice laravel app with the backend api name gateway.
ChatGPT
Sure, let's go step by step to create a microservices architecture with a Laravel app. We'll start by setting up the backend API named "gateway" and then proceed to create a microservice.

### Step 1: Set Up the Gateway API

1. **Install Laravel for Gateway**:
   First, you need to install Laravel for the gateway API.

   ```sh
   composer create-project --prefer-dist laravel/laravel gateway
   cd gateway
   ```

2. **Set Up Basic Configuration**:
   Configure your environment variables in the `.env` file. Make sure to set the database connection and other necessary settings.

   ```env
   APP_NAME=Gateway
   APP_ENV=local
   APP_KEY=base64:your-key-here
   APP_DEBUG=true
   APP_URL=http://localhost

   LOG_CHANNEL=stack

   DB_CONNECTION=mysql
   DB_HOST=127.0.0.1
   DB_PORT=3306
   DB_DATABASE=gateway
   DB_USERNAME=root
   DB_PASSWORD=your-password

   BROADCAST_DRIVER=log
   CACHE_DRIVER=file
   QUEUE_CONNECTION=sync
   SESSION_DRIVER=file
   SESSION_LIFETIME=120

   ```

3. **Create Routes for Gateway**:
   Define routes in `routes/api.php` that will forward requests to the respective microservices.

   ```php
   use Illuminate\Support\Facades\Route;
   use Illuminate\Http\Request;
   use GuzzleHttp\Client;

   Route::middleware('auth:api')->get('/skater-stats', function (Request $request) {
       $client = new Client();
       $response = $client->get('http://localhost:8001/api/skater-stats', [
           'headers' => [
               'Authorization' => $request->header('Authorization')
           ]
       ]);

       return response()->json(json_decode($response->getBody()), $response->getStatusCode());
   });
   ```

4. **Install Guzzle for HTTP Requests**:
   Install Guzzle, a PHP HTTP client that simplifies sending HTTP requests.

   ```sh
   composer require guzzlehttp/guzzle
   ```

### Step 2: Set Up the Skater Stats Microservice

1. **Install Laravel for Skater Stats Service**:
   Now, create a new Laravel project for the Skater Stats service.

   ```sh
   composer create-project --prefer-dist laravel/laravel skater-stats-service
   cd skater-stats-service
   ```

2. **Set Up Basic Configuration**:
   Configure your environment variables in the `.env` file of the Skater Stats service.

   ```env
   APP_NAME=SkaterStatsService
   APP_ENV=local
   APP_KEY=base64:your-key-here
   APP_DEBUG=true
   APP_URL=http://localhost

   LOG_CHANNEL=stack

   DB_CONNECTION=mysql
   DB_HOST=127.0.0.1
   DB_PORT=3306
   DB_DATABASE=skater_stats_service
   DB_USERNAME=root
   DB_PASSWORD=your-password

   BROADCAST_DRIVER=log
   CACHE_DRIVER=file
   QUEUE_CONNECTION=sync
   SESSION_DRIVER=file
   SESSION_LIFETIME=120
   ```

3. **Create Skater Stats Route and Controller**:
   Define a route and create a controller to handle the skater stats functionality.

   ```sh
   php artisan make:controller SkaterStatsController
   ```

   In `routes/api.php`:

   ```php
   use Illuminate\Support\Facades\Route;
   use App\Http\Controllers\SkaterStatsController;

   Route::get('/skater-stats', [SkaterStatsController::class, 'index']);
   ```

   In `app/Http/Controllers/SkaterStatsController.php`:

   ```php
   namespace App\Http\Controllers;

   use Illuminate\Http\Request;

   class SkaterStatsController extends Controller
   {
       public function index()
       {
           // Sample response
           return response()->json([
               'data' => [
                   'player' => 'John Doe',
                   'goals' => 10,
                   'assists' => 5
               ]
           ]);
       }
   }
   ```

### Step 3: Test the Integration

1. **Run Both Services**:
   Open two terminal windows and navigate to each service directory. Run the following commands to start both Laravel servers:

   For the gateway:
   ```sh
   cd gateway
   php artisan serve --port=8000
   ```

   For the skater-stats-service:
   ```sh
   cd skater-stats-service
   php artisan serve --port=8001
   ```

2. **Test the Gateway API**:
   Use a tool like Postman or curl to test the gateway API.

   ```sh
   curl -H "Authorization: Bearer your-token" http://localhost:8000/api/skater-stats
   ```

   You should see a response from the skater-stats-service.

### Next Steps:
- Implement authentication and authorization.
- Add more microservices as needed.
- Set up Docker for easier management and deployment.
- Implement robust error handling and logging.

This basic setup demonstrates how to create a gateway API that communicates with a microservice in Laravel. You can extend this architecture to include more microservices and add additional functionality.
user
gateway is the entrypoint from several microservices made in laravell. One is team_service
ChatGPT
Got it. Let's set up the gateway as the entry point to multiple microservices, including `team_service`. Here are the steps to achieve this:

### Step 1: Set Up the Gateway API

1. **Install Laravel for Gateway**:
   First, install Laravel for the gateway API.

   ```sh
   composer create-project --prefer-dist laravel/laravel gateway
   cd gateway
   ```

2. **Set Up Basic Configuration**:
   Configure your environment variables in the `.env` file. Make sure to set the database connection and other necessary settings.

   ```env
   APP_NAME=Gateway
   APP_ENV=local
   APP_KEY=base64:your-key-here
   APP_DEBUG=true
   APP_URL=http://localhost

   LOG_CHANNEL=stack

   DB_CONNECTION=mysql
   DB_HOST=127.0.0.1
   DB_PORT=3306
   DB_DATABASE=gateway
   DB_USERNAME=root
   DB_PASSWORD=your-password

   BROADCAST_DRIVER=log
   CACHE_DRIVER=file
   QUEUE_CONNECTION=sync
   SESSION_DRIVER=file
   SESSION_LIFETIME=120
   ```

3. **Create Routes for Gateway**:
   Define routes in `routes/api.php` that will forward requests to the respective microservices.

   ```php
   use Illuminate\Support\Facades\Route;
   use Illuminate\Http\Request;
   use GuzzleHttp\Client;

   Route::middleware('auth:api')->get('/skater-stats', function (Request $request) {
       $client = new Client();
       $response = $client->get('http://localhost:8001/api/skater-stats', [
           'headers' => [
               'Authorization' => $request->header('Authorization')
           ]
       ]);

       return response()->json(json_decode($response->getBody()), $response->getStatusCode());
   });

   Route::middleware('auth:api')->get('/team-info', function (Request $request) {
       $client = new Client();
       $response = $client->get('http://localhost:8002/api/team-info', [
           'headers' => [
               'Authorization' => $request->header('Authorization')
           ]
       ]);

       return response()->json(json_decode($response->getBody()), $response->getStatusCode());
   });
   ```

4. **Install Guzzle for HTTP Requests**:
   Install Guzzle, a PHP HTTP client that simplifies sending HTTP requests.

   ```sh
   composer require guzzlehttp/guzzle
   ```

### Step 2: Set Up the Skater Stats Microservice

1. **Install Laravel for Skater Stats Service**:
   Now, create a new Laravel project for the Skater Stats service.

   ```sh
   composer create-project --prefer-dist laravel/laravel skater-stats-service
   cd skater-stats-service
   ```

2. **Set Up Basic Configuration**:
   Configure your environment variables in the `.env` file of the Skater Stats service.

   ```env
   APP_NAME=SkaterStatsService
   APP_ENV=local
   APP_KEY=base64:your-key-here
   APP_DEBUG=true
   APP_URL=http://localhost

   LOG_CHANNEL=stack

   DB_CONNECTION=mysql
   DB_HOST=127.0.0.1
   DB_PORT=3306
   DB_DATABASE=skater_stats_service
   DB_USERNAME=root
   DB_PASSWORD=your-password

   BROADCAST_DRIVER=log
   CACHE_DRIVER=file
   QUEUE_CONNECTION=sync
   SESSION_DRIVER=file
   SESSION_LIFETIME=120
   ```

3. **Create Skater Stats Route and Controller**:
   Define a route and create a controller to handle the skater stats functionality.

   ```sh
   php artisan make:controller SkaterStatsController
   ```

   In `routes/api.php`:

   ```php
   use Illuminate\Support\Facades\Route;
   use App\Http\Controllers\SkaterStatsController;

   Route::get('/skater-stats', [SkaterStatsController::class, 'index']);
   ```

   In `app/Http/Controllers/SkaterStatsController.php`:

   ```php
   namespace App\Http\Controllers;

   use Illuminate\Http\Request;

   class SkaterStatsController extends Controller
   {
       public function index()
       {
           // Sample response
           return response()->json([
               'data' => [
                   'player' => 'John Doe',
                   'goals' => 10,
                   'assists' => 5
               ]
           ]);
       }
   }
   ```

### Step 3: Set Up the Team Service Microservice

1. **Install Laravel for Team Service**:
   Create a new Laravel project for the Team Service.

   ```sh
   composer create-project --prefer-dist laravel/laravel team-service
   cd team-service
   ```

2. **Set Up Basic Configuration**:
   Configure your environment variables in the `.env` file of the Team Service.

   ```env
   APP_NAME=TeamService
   APP_ENV=local
   APP_KEY=base64:your-key-here
   APP_DEBUG=true
   APP_URL=http://localhost

   LOG_CHANNEL=stack

   DB_CONNECTION=mysql
   DB_HOST=127.0.0.1
   DB_PORT=3306
   DB_DATABASE=team_service
   DB_USERNAME=root
   DB_PASSWORD=your-password

   BROADCAST_DRIVER=log
   CACHE_DRIVER=file
   QUEUE_CONNECTION=sync
   SESSION_DRIVER=file
   SESSION_LIFETIME=120
   ```

3. **Create Team Info Route and Controller**:
   Define a route and create a controller to handle the team info functionality.

   ```sh
   php artisan make:controller TeamInfoController
   ```

   In `routes/api.php`:

   ```php
   use Illuminate\Support\Facades\Route;
   use App\Http\Controllers\TeamInfoController;

   Route::get('/team-info', [TeamInfoController::class, 'index']);
   ```

   In `app/Http/Controllers/TeamInfoController.php`:

   ```php
   namespace App\Http\Controllers;

   use Illuminate\Http\Request;

   class TeamInfoController extends Controller
   {
       public function index()
       {
           // Sample response
           return response()->json([
               'data' => [
                   'team' => 'Dream Team',
                   'wins' => 15,
                   'losses' => 3
               ]
           ]);
       }
   }
   ```

### Step 4: Test the Integration

1. **Run All Services**:
   Open three terminal windows and navigate to each service directory. Run the following commands to start all Laravel servers:

   For the gateway:
   ```sh
   cd gateway
   php artisan serve --port=8000
   ```

   For the skater-stats-service:
   ```sh
   cd skater-stats-service
   php artisan serve --port=8001
   ```

   For the team-service:
   ```sh
   cd team-service
   php artisan serve --port=8002
   ```

2. **Test the Gateway API**:
   Use a tool like Postman or curl to test the gateway API.

   For Skater Stats:
   ```sh
   curl -H "Authorization: Bearer your-token" http://localhost:8000/api/skater-stats
   ```

   For Team Info:
   ```sh
   curl -H "Authorization: Bearer your-token" http://localhost:8000/api/team-info
   ```

   You should see responses from the respective microservices.

### Next Steps:
- Implement authentication and authorization.
- Add more microservices as needed.
- Set up Docker for easier management and deployment.
- Implement robust error handling and logging.

This setup demonstrates how to create a gateway API that communicates with multiple microservices in Laravel. You can extend this architecture to include more services and add additional functionality as required.
user
make me a Team model, migration
ChatGPT
Sure! Let's create a `Team` model along with a migration file to set up the database table for the Team service.

### Step 1: Create the Team Model

In your `team-service` directory, run the following command to create a model and migration file for the `Team`:

```sh
php artisan make:model Team -m
```

This command creates a `Team` model and a corresponding migration file in the `database/migrations` directory.

### Step 2: Define the Team Model

Open the `Team.php` model file located in the `app/Models` directory and define the model:

```php
namespace App\Models;

use Illuminate\Database\Eloquent\Factories\HasFactory;
use Illuminate\Database\Eloquent\Model;

class Team extends Model
{
    use HasFactory;

    protected $fillable = [
        'name',
        'wins',
        'losses'
    ];
}
```

### Step 3: Define the Migration File

Open the migration file located in the `database/migrations` directory. It will have a name like `2024_07_05_000000_create_teams_table.php`. Define the schema for the `teams` table:

```php
use Illuminate\Database\Migrations\Migration;
use Illuminate\Database\Schema\Blueprint;
use Illuminate\Support\Facades\Schema;

class CreateTeamsTable extends Migration
{
    /**
     * Run the migrations.
     *
     * @return void
     */
    public function up()
    {
        Schema::create('teams', function (Blueprint $table) {
            $table->id();
            $table->string('name');
            $table->integer('wins')->default(0);
            $table->integer('losses')->default(0);
            $table->timestamps();
        });
    }

    /**
     * Reverse the migrations.
     *
     * @return void
     */
    public function down()
    {
        Schema::dropIfExists('teams');
    }
}
```

### Step 4: Run the Migration

Run the migration to create the `teams` table in your database:

```sh
php artisan migrate
```

### Summary

Now you have created the `Team` model and the corresponding `teams` table in the database. The `Team` model is ready to be used in your Laravel application for CRUD operations.

If you need to create some initial data for testing, you can create a seeder.

### Optional: Create a Seeder for Initial Data

1. **Create the Seeder**:
   ```sh
   php artisan make:seeder TeamSeeder
   ```

2. **Define the Seeder**:
   Open `database/seeders/TeamSeeder.php` and add some sample data:

   ```php
   namespace Database\Seeders;

   use Illuminate\Database\Seeder;
   use App\Models\Team;

   class TeamSeeder extends Seeder
   {
       /**
        * Run the database seeds.
        *
        * @return void
        */
       public function run()
       {
           Team::create([
               'name' => 'Dream Team',
               'wins' => 15,
               'losses' => 3
           ]);

           Team::create([
               'name' => 'Champion Squad',
               'wins' => 12,
               'losses' => 5
           ]);
       }
   }
   ```

3. **Run the Seeder**:
   ```sh
   php artisan db:seed --class=TeamSeeder
   ```

This will populate the `teams` table with some initial data. Now your `Team` service is ready with a model, migration, and initial data.
user
if you were a app that helped hockey player with there stats but also let the teams see the large picture of their palyers what information in the teams would you need
ChatGPT
To build an app that helps hockey players with their stats and also lets teams see the bigger picture of their players, you would need to collect and manage a variety of information. Here's a breakdown of the essential data for both players and teams:

### Player Information

1. **Basic Information**:
    - Full Name
    - Date of Birth
    - Position (e.g., Forward, Defense, Goalie)
    - Jersey Number
    - Height and Weight
    - Nationality

2. **Performance Stats**:
    - Games Played
    - Goals
    - Assists
    - Points (Goals + Assists)
    - Plus/Minus Rating
    - Penalty Minutes
    - Shots on Goal
    - Shooting Percentage
    - Time on Ice (Total and Average per Game)
    - Faceoff Wins and Losses (for centers)

3. **Advanced Metrics**:
    - Corsi and Fenwick (for possession stats)
    - Expected Goals (xG)
    - Zone Starts (Offensive, Defensive, Neutral)
    - High-Danger Scoring Chances
    - Power Play Points
    - Short-Handed Points

4. **Health and Fitness**:
    - Injury History
    - Current Injury Status
    - Fitness Assessments (Speed, Agility, Strength)
    - Training Logs

5. **Career Information**:
    - Previous Teams
    - Contract Details
    - Agent Information
    - Awards and Achievements

### Team Information

1. **Basic Team Information**:
    - Team Name
    - Team Logo
    - Home Arena
    - Team Roster (List of Players)
    - Coaching Staff

2. **Team Performance Stats**:
    - Games Played
    - Wins
    - Losses
    - Overtime/Shootout Losses
    - Points (Standings)
    - Goals For
    - Goals Against
    - Power Play Percentage
    - Penalty Kill Percentage

3. **Player Aggregates**:
    - Top Scorers
    - Top Assist Providers
    - Best Plus/Minus
    - Most Penalty Minutes
    - Best Save Percentage (for goalies)

4. **Advanced Team Metrics**:
    - Team Corsi and Fenwick
    - Expected Goals (xG) for the Team
    - Scoring Chances For and Against
    - Power Play and Penalty Kill Efficiency

5. **Team Health and Fitness**:
    - Injury Reports
    - Fitness Levels Across the Team
    - Training and Practice Schedules

6. **Strategic Information**:
    - Line Combinations
    - Special Teams Units (Power Play, Penalty Kill)
    - Game Strategies and Tactics
    - Opponent Analysis

### Database Design

Based on the above information, here’s a high-level database schema:

#### Tables

1. **Players**:
    - `id`
    - `full_name`
    - `date_of_birth`
    - `position`
    - `jersey_number`
    - `height`
    - `weight`
    - `nationality`

2. **PlayerStats**:
    - `id`
    - `player_id`
    - `season`
    - `games_played`
    - `goals`
    - `assists`
    - `points`
    - `plus_minus`
    - `penalty_minutes`
    - `shots_on_goal`
    - `shooting_percentage`
    - `time_on_ice`
    - `faceoff_wins`
    - `faceoff_losses`
    - `corsi`
    - `fenwick`
    - `expected_goals`
    - `zone_starts`
    - `high_danger_chances`
    - `power_play_points`
    - `short_handed_points`

3. **Teams**:
    - `id`
    - `name`
    - `logo`
    - `home_arena`

4. **TeamStats**:
    - `id`
    - `team_id`
    - `season`
    - `games_played`
    - `wins`
    - `losses`
    - `overtime_losses`
    - `points`
    - `goals_for`
    - `goals_against`
    - `power_play_percentage`
    - `penalty_kill_percentage`
    - `corsi`
    - `fenwick`
    - `expected_goals`
    - `scoring_chances_for`
    - `scoring_chances_against`

5. **Injuries**:
    - `id`
    - `player_id`
    - `injury_date`
    - `injury_type`
    - `recovery_date`
    - `status`

6. **TeamsPlayers**:
    - `id`
    - `team_id`
    - `player_id`

### Summary

Collecting and managing this data would allow both individual players to track their performance and health, and teams to get a comprehensive view of their roster's strengths, weaknesses, and overall team performance. This information can help in making strategic decisions, improving training programs, and enhancing overall team performance.
user
Make a model out the Teams:
ChatGPT
Sure, let's create the `Team` model along with the necessary migration file in Laravel.

### Step 1: Create the Team Model and Migration

In your `team-service` directory, run the following command to create a model and migration file for the `Team`:

```sh
php artisan make:model Team -m
```

This command creates a `Team` model and a corresponding migration file in the `database/migrations` directory.

### Step 2: Define the Team Model

Open the `Team.php` model file located in the `app/Models` directory and define the model:

```php
namespace App\Models;

use Illuminate\Database\Eloquent\Factories\HasFactory;
use Illuminate\Database\Eloquent\Model;

class Team extends Model
{
    use HasFactory;

    protected $fillable = [
        'name',
        'logo',
        'home_arena'
    ];
}
```

### Step 3: Define the Migration File

Open the migration file located in the `database/migrations` directory. It will have a name like `2024_07_05_000000_create_teams_table.php`. Define the schema for the `teams` table:

```php
use Illuminate\Database\Migrations\Migration;
use Illuminate\Database\Schema\Blueprint;
use Illuminate\Support\Facades\Schema;

class CreateTeamsTable extends Migration
{
    /**
     * Run the migrations.
     *
     * @return void
     */
    public function up()
    {
        Schema::create('teams', function (Blueprint $table) {
            $table->id();
            $table->string('name');
            $table->string('logo')->nullable();
            $table->string('home_arena')->nullable();
            $table->timestamps();
        });
    }

    /**
     * Reverse the migrations.
     *
     * @return void
     */
    public function down()
    {
        Schema::dropIfExists('teams');
    }
}
```

### Step 4: Run the Migration

Run the migration to create the `teams` table in your database:

```sh
php artisan migrate
```

### Summary

Now you have created the `Team` model and the corresponding `teams` table in the database. The `Team` model is ready to be used in your Laravel application for CRUD operations. If you need to add additional relationships or methods to the `Team` model, you can do so by editing the `Team.php` file.

Feel free to extend this setup with more fields, relationships, or additional functionality as needed for your application.
user
SQLSTATE[HY000] [2002] php_network_getaddresses: getaddrinfo for mysql failed: nodename nor servname provided, or not known (Connection: mysql, SQL: select table_name as `name`, (data_length + index_length) as `size`, table_comment as `comment`, engine as `engine`, table_collation as `collation` from information_schema.tables where table_schema = 'team_service' and table_type in ('BASE TABLE', 'SYSTEM VERSIONED') order by table_name)
ChatGPT
This error indicates that your Laravel application is unable to connect to the MySQL database. This is usually due to incorrect database configuration in the `.env` file. Here are some steps to troubleshoot and fix this issue:

### Step 1: Check the `.env` File

Make sure the `.env` file in your `team-service` directory has the correct database configuration. It should look something like this:

```env
APP_NAME=TeamService
APP_ENV=local
APP_KEY=base64:your-key-here
APP_DEBUG=true
APP_URL=http://localhost

LOG_CHANNEL=stack

DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=team_service
DB_USERNAME=root
DB_PASSWORD=your-password

BROADCAST_DRIVER=log
CACHE_DRIVER=file
QUEUE_CONNECTION=sync
SESSION_DRIVER=file
SESSION_LIFETIME=120
```

### Step 2: Verify MySQL Server

Make sure your MySQL server is running and accessible. You can check this by trying to connect to the database using a database client or command line:

```sh
mysql -u root -p
```

### Step 3: Verify Database Credentials

Ensure that the database credentials (DB_USERNAME and DB_PASSWORD) are correct and match the ones you use to log into your MySQL server.

### Step 4: Check Database Host

If you are using a different host for your MySQL server (not localhost), make sure to update the DB_HOST value accordingly. For example, if your MySQL server is hosted on a different server, use its IP address or hostname
user
Target class [TeamServiceController] does not exist.

ChatGPT
The error message indicates that Laravel cannot find the `TeamServiceController`. This typically happens if the controller class was not created properly, or if there's a typo in the route definition.

### Step 1: Create the TeamServiceController

First, ensure that you have created the controller. Run the following command to create it:

```sh
php artisan make:controller TeamServiceController
```

### Step 2: Define the Controller

Open the newly created `TeamServiceController.php` file located in the `app/Http/Controllers` directory and define a basic controller:

```php
namespace App\Http\Controllers;

use Illuminate\Http\Request;
use App\Models\Team;

class TeamServiceController extends Controller
{
    public function index()
    {
        $teams = Team::all();
        return response()->json($teams);
    }
}
```

### Step 3: Define the Route

Ensure that the route is defined correctly in `routes/api.php`:

```php
use Illuminate\Support\Facades\Route;
use App\Http\Controllers\TeamServiceController;

Route::get('/team-info', [TeamServiceController::class, 'index']);
```

###
user
make a team seeder
ChatGPT
To create a team seeder in your Laravel project, follow these steps:

### Step 1: Create the Seeder

Run the following command to create a seeder for the `Team` model:

```sh
php artisan make:seeder TeamSeeder
```

### Step 2: Define the Seeder

Open the `TeamSeeder.php` file located in the `database/seeders` directory and define some sample data:

```php
namespace Database\Seeders;

use Illuminate\Database\Seeder;
use App\Models\Team;

class TeamSeeder extends Seeder
{
    /**
     * Run the database seeds.
     *
     * @return void
     */
    public function run()
    {
        Team::create([
            'name' => 'Dream Team',
            'logo' => 'dream_team_logo.png',
            'home_arena' => 'Dream Arena'
        ]);

        Team::create([
            'name' => 'Champion Squad',
            'logo' => 'champion_squad_logo.png',
            'home_arena' => 'Champion Arena'
        ]);

        Team::create([
            'name' => 'Victory Warriors',
            'logo' => 'victory_warriors_logo.png',
            'home_arena' => 'Warriors Arena'
        ]);
    }
}
```

### Step 3: Register the Seeder

Open the `DatabaseSeeder.php` file located in the `database/seeders` directory and register the `TeamSeeder`:

```php
namespace Database\Seeders;

use Illuminate\Database\Seeder;

class DatabaseSeeder extends Seeder
{
    /**
     * Seed the application's database.
     *
     * @return void
     */
    public function run()
    {
        $this->call(TeamSeeder::class);
    }
}
```

### Step 4: Run the Seeder

Run the seeder to populate the `teams` table with the sample data:

```sh
php artisan db:seed --class=TeamSeeder
```

### Summary

These steps will create and run a seeder that populates the `teams` table with sample data. This data will help you test your application with some initial team entries.