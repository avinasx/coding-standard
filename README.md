# General Coding-Standard
Best practices for coding, examples are for php , can be applied to most of the languages out there.


## 1. Overview


- There should be a newline at the end of file.
- Code MUST use 4 spaces for indenting, not tabs.
- Class names MUST be declared in `StudlyCaps`.
- Class constants MUST be declared in all upper case with underscore separators.
- Method names MUST be declared in `camelCase`.
- Property names MUST be declared in `camelCase`.
- Property names MUST start with an initial underscore if they are private.
- Always use `elseif` instead of `else if`.


## 2. Class Names

Class names MUST be declared in `StudlyCaps`. For example, `Controller`, `Model`.

## 3. Classes

The term "class" refers to all classes and interfaces here.

- Classes should be named using `StudlyCase`.
- The brace should always be written on the line underneath the class name.
- Every class must have a documentation block that conforms to the PHPDoc or respective language specific tool.
- All code in a class must be indented with 4 spaces.
- There should be only one class in a single file.
- All classes should be namespaced.
- Class name should match file name. Class namespace should match directory structure.

```php
/**
 * Documentation
 */
class MyClass extends \yii\base\BaseObject implements MyInterface
{
    // code
}
```

### 3.1. Constants and params/event variable

Class constants MUST be declared in all upper case with underscore separators.
For example:

```php
<?php
class Foo
{
    const VERSION = '1.0';
    const DATE_APPROVED = '2012-06-01';
}
```
define variables in params whenever required, which may change depending on environments, put params in gitignore.


### 3.2. Properties

- When declaring public class members specify `public` keyword explicitly.
- Public and protected variables should be declared at the top of the class before any method declarations.
  Private variables should also be declared at the top of the class but may be added right before the methods
  that are dealing with them in cases where they are only related to a small subset of the class methods.
- The order of property declaration in a class should be ascending based on their visibility: from public over protected to private.
- There are no strict rules for ordering properties that have the same visibility.
- For better readability there should be no blank lines between property declarations and two blank lines
  between property and method declaration sections. One blank line should be added between the different visibility groups.
- Private variables should be named like `$_varName`.
- Public class members and standalone variables should be named using `$camelCase`
  with first letter lowercase.
- Use descriptive names. Variables such as `$i` and `$j` are better not to be used.

For example:

```php
<?php
class Foo
{
    public $publicProp1;
    public $publicProp2;

    protected $protectedProp;

    private $_privateProp;


    public function someMethod()
    {
        // ...
    }
}
```

### 3.3. Methods

- Functions and methods should be named using `camelCase` with first letter lowercase.
- Name should be descriptive by itself indicating the purpose of the function.
- Class methods should always declare visibility using `private`, `protected` and
  `public` modifiers. `var` is not allowed.
- Opening brace of a function should be on the line after the function declaration.
- functions and class should be as small as possible , SOLID principle should be followed.

```php
/**
 * Documentation
 */
class Foo
{
    /**
     * Documentation
     */
    public function bar()
    {
        // code
        return $value;
    }
}
```

### 3.4 PHPDoc blocks // follow similar practice for other languages as well

 - `@param`, `@var`, `@property` and `@return` must declare types as `bool`, `int`, `string`, `array` or `null`.
   You can use a class names as well such as `Model` or `ActiveRecord`.
 - For a typed arrays use `ClassName[]`.
 - The first line of the PHPDoc must describe the purpose of the method.
 - If method checks something (`isActive`, `hasClass`, etc) the first line should start with `Checks whether`.
 - `@return` should explicitly describe what exactly will be returned.

```php
/**
 * Checks whether the IP is in subnet range
 *
 * @param string $ip an IPv4 or IPv6 address
 * @param int $cidr the CIDR length
 * @param string $range subnet in CIDR format e.g. `10.0.0.0/8` or `2001:af::/64`
 * @return bool whether the IP is in subnet range
 */
 private function inRange($ip, $cidr, $range)
 {
   // ...
 }
```


## 4 PHP

### 4.1 Types

- All PHP types and values should be used lowercase. That includes `true`, `false`, `null` and `array`.

Changing type of an existing variable is considered as a bad practice. Try not to write such code unless it is really necessary.


```php
public function save(Transaction $transaction, $argument2 = 100)
{
    $transaction = new Connection; // bad
    $argument2 = 200; // good
}
```

### 4.2 Strings

- If string doesn't contain variables or single quotes, use single quotes.

```php
$str = 'Like this.';
```

- If string contains single quotes you can use double quotes to avoid extra escaping.

#### Variable substitution

```php
$str1 = "Hello $username!";
$str2 = "Hello {$username}!";
```

The following is not permitted:

```php
$str3 = "Hello ${username}!";
```

#### Concatenation

Add spaces around dot when concatenating strings:

```php
$name = 'Yii' . ' Framework';
```

Multi-line string When string is long format is the following:

```php
$sql = "SELECT *"
    . "FROM `post` "
    . "WHERE `id` = 121 ";
```


#### Numerically indexed

- Do not use negative numbers as array indexes.

Use the following formatting when declaring array:

```php
$arr = [3, 14, 15, 'Yii', 'Framework'];
```

If there are too many elements for a single line:

```php
$arr = [
    3, 14, 15,
    92, 6, $test,
    'Yii', 'Framework',
];
```

#### Associative

Use the following format for associative arrays:

```php
$config = [
    'name' => 'Yii',
    'options' => ['usePHP' => true],
];
```

### 4.4 control statements

- Control statement condition must have single space before and after parenthesis.
- Operators inside of parenthesis should be separated by spaces.
- Opening brace is on the same line.
- Closing brace is on a new line.
- Always use braces for single line statements.

```php
if ($event === null) {
    return new Event();
}
if ($event instanceof CoolEvent) {
    return $event->instance();
}
return null;


// the following is NOT allowed:
if (!$model && null === $event)
    throw new Exception('test');
```

Prefer avoiding `else` after `return` where it makes sense.
Use [guard conditions](https://refactoring.com/catalog/replaceNestedConditionalWithGuardClauses.html).

```php
$result = $this->getResult();
if (empty($result)) {
    return true;
} else {
    // process result
}
```

is better as

```php
$result = $this->getResult();
if (empty($result)) {
   return true;
}

// process result
```

#### switch

Use the following formatting for switch:

```php
switch ($this->phpType) {
    case 'string':
        $a = (string) $value;
        break;
    case 'integer':
    case 'int':
        $a = (int) $value;
        break;
    case 'boolean':
        $a = (bool) $value;
        break;
    default:
        $a = null;
}
```

### 4.5 function calls

```php
doIt(2, 3);

doIt(['a' => 'b']);

doIt('a', [
    'a' => 'b',
    'c' => 'd',
]);
```

### 4.6 Anonymous functions (lambda) declarations

Note space between `function`/`use` tokens and open parenthesis:

```php
// good
$n = 100;
$sum = array_reduce($numbers, function ($r, $x) use ($n) {
    $this->doMagic();
    $r += $x * $n;
    return $r;
});

// bad
$n = 100;
$mul = array_reduce($numbers, function($r, $x) use($n) {
    $this->doMagic();
    $r *= $x * $n;
    return $r;
});
```

Documentation
-------------

- Refer to [phpDoc](https://phpdoc.org/) for documentation syntax.
- Code without documentation is not allowed.
- All class files must contain a "file-level" docblock at the top of each file
  and a "class-level" docblock immediately above each class.
- There is no need to use `@return` if method does return nothing.


#### File

```php
<?php
/**
 * @link https://www.docquity.com/
 * @copyright Copyright (c) 2022 docquity holdings
 * @license https://www.docquity.com/license/
 */
```

#### Class

```php
/**
 * Component is the base class that provides the *property*, *event* and *behavior* features.
 *
 * @include @docs/Component.md
 *
 * @author avinash kr <avinash.sudhanshu@docquity.com>
 * @since 2.0
 */
class Component extends \yii\base\BaseObject
```


#### Function / method

```php
/**
 * Returns the list of attached event handlers for an event.
 * You may manipulate the returned [[Vector]] object by adding or removing handlers.
 * For example,
 *
 * ```
 * $component->getEventHandlers($eventName)->insertAt(0, $eventHandler);
 * ```
 *
 * @param string $name the event name
 * @return Vector list of attached event handlers for the event
 * @throws Exception if the event is not defined
 */
public function getEventHandlers($name)
{
    if (!isset($this->_e[$name])) {
        $this->_e[$name] = new Vector;
    }
    $this->ensureBehaviors();
    return $this->_e[$name];
}
```

#### Comments

- One-line comments should be started with `//` and not `#`.
- One-line comment should be on its own line.

Additional rules
----------------

### `=== []` vs `empty()`

Use `empty()` where possible.

### multiple return points

Return early when conditions nesting starts to get cluttered. If the method is short it doesn't matter.

### `self` vs. `static`

Always use `static` except the following cases:

- accessing constants MUST be done via `self`: `self::MY_CONSTANT`
- accessing private static properties MUST be done via `self`: `self::$_events`
- It is allowed to use `self` for method calls where it makes sense such as recursive call to current implementation instead of extending classes implementation.

### value for "don't do something"

Properties allowing to configure component not to do something should accept value of `false`. `null`, `''`, or `[]` should not be assumed as such.

### Directory/namespace names

- use lower case
- use plural form for nouns which represent objects (e.g. validators)
- use singular form for names representing relevant functionality/features (e.g. web)
- prefer single word namespaces
- if single word isn't suitable, use camelCase

### Package manager

- use package manager like composer/npm/pip/maven whenever possible to add plugin/external library to project.
- Always use static versioning in the composer.php/package.json to avoid compatibility issues.
- put content installed by packange-manager in gitignore


### References and suggested readings
- https://www.php-fig.org/psr/
- https://www.php-fig.org/psr/psr-2/
- https://www.conventionalcommits.org/en/v1.0.0/
- https://www.sonarlint.org/
- https://plugins.jetbrains.com/plugin/17399-sql-optimizer-indexing-advisor-mysql-postgresql-by-eversql/

### Further suggesion and contributions
- Contribution to this doc is welcomed. Fork or generate a pull request to main branch, whenever felt like you need to.
