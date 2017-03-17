# шпаргалка по Faker
[Faker](https://github.com/fzaninotto/Faker)

первым делом создаем модели и миграции
```
php artisan make:model -m Ludi
```

правим миграции database/migrations/\<timestamp\>_create_ludis_table, создаем поля
```
$table->string('name');
```

дальше создаем болванку, имя должно начинаться с имени модели, т.е. LudiFactory

тупа копируем существующую database/factories/ModelFactory с нашим именем,

удаляем в файле все ненужное, и добавляем следующий код
```
$factory->define(App\Ludi::class, function (Faker\Generator $faker) {

  return [
    'name' => $faker->name,
  ];
});
```

так, болванка готова, что умеет faker смотрим у него на сайте

создаем seeder
```
php artisan make:seeder LudisTableSeeder
```

собственно правим database/seeds/LudisTableSeeder, добавляем следующий код в функцию run
```
factory(App\Ludi::class, 50)->create();
```

в файл database/seeds/DatabaseSeeder добавляем следующие строки
```
$this->call(LudisTableSeeder::class);
```

делаем таблицы, и заливаем seeder
```
php artisan migrate
php artisan db:seed
```
готово!

Если что-то подзабыл, читай [Laravel seeding](https://laravel.com/docs/seeding)
