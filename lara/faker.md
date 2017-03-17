# шпаргалка по Faker
[Faker](https://github.com/fzaninotto/Faker)

первым делом создаем модели и миграции
```
php artisan make:model -m Ludi
```

правим миграции, создаем поля
```
$table->string('name');
```

дальше создаем factories, имя должно начинаться с имени модели, т.е.LudiFactory
и тупа копируем существующую ModelFactory с нашим именем
удаляем в не все ненужное, в имени модели ставим наше имя, App\Ludi, добавляем следующий код
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

собственно правим LudisTableSeeder.php, добавляем следующий код в функцию run
```
factory(App\Ludi::class, 50)->create();
```

в файл DatabaseSeeder.php добавляем следующие строки
```
$this->call(LudisTableSeeder::class);
```

делаем базы, и заливаем seeder
```
php artisan migrate
php artisan db:seed
```
готово!
