TypeAssert
##########

Hack library for converting untyped data to typed data.

Status
------

Don't use this yet :) I've written these usage examples before writing
any code...

Usage
-----

```Hack
<?hh
function needs_string(string $foo): void {
}

function main(mixed $foo): void {
  needs_string(TypeAssert::isString($foo));
}
```

```Hack
<?hh
class Foo {
  const TAPIResponse = shape(
    'id' => int,
    'user' => string,
    'data' => shape(
      /* ... */
    ),
  );

  const getAPI(): self::TAPIResponse {
    $json_string = file_get_contents('https://api.example.com');
    $array = json_decode($json_string, /* associative = */ true);
    return TypeAssert::isTypeStructure(
      type_structure(self::class, 'TAPIResponse'),
      $array,
    );
  }
}
```

Credit
------

This library is a reimplementation of ideas from:

 - @admdikramr
 - @ahupp
 - @dlreeves
 - @periodic1236
 - @schrockn

The good ideas are theirs, any mistakes are mine :)

License
-------

This software is distributed under the ISC license - see LICENSE file
in this directory for details.