yii2-angularjs
============

Installation
------------

The preferred way to install this extension is through [composer](http://getcomposer.org/download/).

Either run

```
php composer.phar require deesoft/yii2-angularjs "~1.0"
```

or add

```
"deesoft/yii2-angularjs": "~1.0"
```

to the require section of your `composer.json` file.

Usage
-----

# Module Widget

file `index.php`
```php
<div ng-app="angularYii">
    <?php Module::begin([
        'name' => 'angularYii', // module name, use for ng-app
        'controllers' => [
            'MainController' => [
                'sourceFile' => 'controllers/main-controller.js',
            ]
        ]
    ])?>
        <div ng-controller="MainController">
            <ul>
                <li ng-repeat="todo in todos">{{todo.name}}</li>
            </ul>
            <input ng-model="newValue"><button ng-click="addTodo()">Add</button>
        </div>
    <?php Module::end()?>
</div>
```

file `controllers/main-controller.js`
```js
function($scope){
    $scope.todos = [
        {name: 'Satu'},
        {name: 'Dua'},
        {name: 'Tiga'},
    ];

    $scope.addTodo = function(){
        $scope.todos.push({
            name:$scope.newValue,
        });
        $scope.newValue = '';
    }
}
```

# NgRoute widget
`NgRoute` widget is special widget of `Module`. It has property `routes`

file `index.php`
```php
<div ng-app="ngrouteYii">
    <?= NgRoute::widget([
        'name' => 'ngrouteYii',
        'routes' => [
            '/' => [
                'templateFile' => 'templates/main.php',
                'controllerFile' => 'controllers/main.js',
            ],
            '/view/:id' => [
                'templateFile' => 'templates/view.php',
                'controllerFile' => 'controllers/view.js',
            ],
            '/edit/:id' => [
                'templateFile' => 'templates/edit.php',
                'controllerFile' => 'controllers/edit.js',
            ],
            '*' => [ // otherwise
                'templateFile' => 'templates/not-found.php',
            ],
        ]
    ])?>
</div>
```
