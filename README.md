# Laravel workflow

Use the Symfony Workflow component in Laravel

### Installation

    composer require brexis/laravel-workflow

#### Laravel 5

Add a ServiceProvider to your providers array in `config/app.php`:

```php
'providers' => [
    ...
	'LaravelWorkflow\ServiceProvider',

]
```

Add the `Workflow` facade to your facades array:

```php
	'Workflow' => 'LaravelWorkflow\Facades\WorkflowFacade',
```


### Configuration

Configure your workflow in `config/workflow.php`

```php
<?php

return [
    'straight'   => [
        'type'          => 'workflow', // or 'state_machine'
        'marking_store' => [
            'type'      => 'multiple_state',
            'arguments' => ['currentPlace']
        ],
        'supports'      => ['App\BlogPost'],
        'places'        => ['draft', 'review', 'rejected', 'published'],
        'transitions'   => [
            'to_review' => [
                'from' => 'draft',
                'to'   => 'review'
            ],
            'publish' => [
                'from' => 'review',
                'to'   => 'published'
            ],
            'reject' => [
                'from' => 'review',
                'to'   => 'rejected'
            ]
        ],
    ]
];
```
