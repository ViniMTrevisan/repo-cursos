# Estudos de PHP

## Variáveis

- Para criar uma variável, usamos `$` seguido do nome da variável.
- O nome deve começar com uma letra ou `_` (underline).
- Exemplos de nomenclatura:
  - CamelCase: `myName`
  - Snake_case: `my_name`

```php
$name = 'Vini';
$number = 18;

// Referência
$myName = &$name; // O `&` passa algo como referência.
$name = 'Jones';

echo $name; // Jones
echo $myName; // Jones
```

> **Nota:** Usar referências (`&`) pode ser útil, mas deve ser feito com cuidado para evitar efeitos colaterais inesperados.

### Tipos de Dados

1. **Strings**: Tudo que está entre aspas simples ou duplas.
   ```php
   echo gettype("Vini"); // string
   ```

2. **Números**: Inteiros, floats, doubles.
   ```php
   echo gettype(10.5); // double
   ```

3. **Booleans**: `true` ou `false`.
   ```php
   echo gettype(false); // boolean
   ```

4. **Arrays**: Listas.
   ```php
   echo gettype(['item1', 50]); // array
   ```

5. **Objetos**: Classes.
   ```php
   class Person {}
   echo gettype(new Person()); // object
   ```

6. **Null**: Representa "nada".
   ```php
   echo gettype(null); // NULL
   ```

> **Nota:** Sempre verificar o tipo de dado com `gettype()` ou funções como `is_numeric()` para evitar erros em operações.

---

## Constantes

- Criadas com `define` e geralmente em letras maiúsculas.

```php
define('NAME', 'Vini');
echo NAME; // Vini
```

### Constantes Mágicas

- `__FUNCTION__`: Nome da função atual.
- `__METHOD__`: Nome do método atual.

```php
function teste() {
    echo __FUNCTION__; // teste
    echo __METHOD__;   // teste
}
teste();
```

> **Nota:** Constantes mágicas são úteis para debug e rastreamento de execução.

---

## Operadores

### Operadores Matemáticos

```php
$number1 = 10;
$number2 = 5;

echo $number1 + $number2; // Soma
echo $number1 - $number2; // Subtração
echo $number1 * $number2; // Multiplicação
echo $number1 / $number2; // Divisão
echo $number1 % $number2; // Resto
```

> **Nota:** O PHP segue a ordem PEMDAS (Parênteses, Expoentes, Multiplicação/Divisão, Adição/Subtração).

### Operadores de Atribuição

```php
$name = 'Vini';
$name .= ' Trevisan'; // Concatenação
echo $name; // Vini Trevisan

$number = 10;
$number += 5; // $number = $number + 5
echo $number; // 15
```

> **Nota:** O operador `.` é usado para concatenar strings.

### Operadores de Incremento e Decremento

```php
$number = 10;
echo ++$number; // Incrementa antes de usar
echo $number++; // Incrementa depois de usar
echo --$number; // Decrementa antes de usar
echo $number--; // Decrementa depois de usar
```

> **Nota:** Usar `++` ou `--` antes da variável altera o valor imediatamente, enquanto depois altera na próxima chamada.

### Operadores de Comparação

```php
$result = 30 < 50; // true
echo $result;

$result = 30 === '30'; // false (compara valor e tipo)
echo $result;
```

> **Nota:** Use `===` para comparar valor e tipo, e `!==` para verificar se valor e tipo são diferentes.

### Operadores Lógicos

```php
$canAccess = true;
$isOlder = false;

$result = $canAccess && $isOlder; // false
$result = $canAccess || $isOlder; // true
$result = !$isOlder; // true
```

> **Nota:** Prefira `&&` e `||` em vez de `and` e `or` por questões de precedência.

---

## Estruturas Condicionais

### If/Else

```php
$isAdmin = true;

if ($isAdmin) {
    echo 'isAdmin';
} else {
    echo 'notAdmin';
}
```

> **Nota:** Sempre use chaves `{}` para evitar ambiguidades, mesmo em condições simples.

### Switch

```php
$name = 'Vini';

switch ($name) {
    case 'Vini':
        echo 'É o Vini';
        break;
    case 'Jones':
        echo 'É o Jones';
        break;
    default:
        echo 'Não é Vini nem Jones';
        break;
}
```

> **Nota:** Sempre use `break` para evitar que os casos continuem executando.

---

## Loops

### For

```php
$names = ['Vini', 'João', 'Guilherme', 'Ana'];

for ($i = 0; $i < count($names); $i++) {
    echo $names[$i];
}
```

> **Nota:** Use `count()` para determinar o tamanho do array, mas evite chamá-lo repetidamente dentro do loop.

### While

```php
$i = 0;
while ($i < count($names)) {
    echo $names[$i];
    $i++;
}
```

> **Nota:** Certifique-se de que a condição do `while` eventualmente se torne falsa para evitar loops infinitos.

### Foreach

```php
foreach ($names as $key => $name) {
    echo $key . ' => ' . $name;
}
```

> **Nota:** Use `foreach` para iterar sobre arrays de forma mais legível.

---

## Funções

- Funções são definidas com `function`.

```php
function sayHello($name) {
    return "Olá, $name!";
}

echo sayHello('Vini'); // Olá, Vini!
```

> **Nota:** Sempre nomeie funções de forma descritiva para facilitar a leitura do código.

### Closures

```php
$greet = function ($name) {
    return "Olá, $name!";
};

echo $greet('Vini'); // Olá, Vini!
```

> **Nota:** Closures são úteis para criar funções anônimas ou passar funções como parâmetros.

---

## Superglobais

- **`$_COOKIE`**: Valores armazenados no navegador.
- **`$_SESSION`**: Valores armazenados na sessão do usuário.
- **`$_GET`**: Dados enviados via URL.
- **`$_POST`**: Dados enviados via formulário.
- **`$_REQUEST`**: Combinação de `$_GET` e `$_POST`.
- **`$_SERVER`**: Informações sobre o servidor.

> **Nota:** Sempre sanitize os dados recebidos via superglobais para evitar vulnerabilidades.

---

## Cookies

### Criar um Cookie

```php
setcookie('name', 'Vini', time() + 2 * 24 * 60 * 60); // Expira em 2 dias
```

### Resgatar um Cookie

```php
if (isset($_COOKIE['name'])) {
    echo $_COOKIE['name'];
} else {
    echo 'Cookie não existe';
}
```

### Excluir um Cookie

```php
setcookie('name', '', time() - 3600); // Expira no passado
```

> **Nota:** Cookies são úteis para armazenar informações no navegador do usuário, mas devem ser usados com cuidado para evitar problemas de segurança.

---

## Sessões

### Criar uma Sessão

```php
session_start();
$_SESSION['name'] = 'Vini';
```

### Resgatar uma Sessão

```php
if (isset($_SESSION['name'])) {
    echo $_SESSION['name'];
} else {
    echo 'Sessão não existe';
}
```

### Excluir uma Sessão

```php
unset($_SESSION['name']); // Excluir uma sessão
session_destroy(); // Excluir todas as sessões
```

> **Nota:** Sessões são úteis para armazenar dados temporários do usuário no servidor.

---

## Variáveis de Ambiente

- Usadas para armazenar informações sensíveis, como chaves de API.
- Geralmente configuradas em arquivos `.env`.

> **Nota:** Nunca exponha variáveis de ambiente diretamente no código.

---

## Métodos HTTP

### GET

```php
var_dump($_GET);
```

### POST

```php
var_dump($_POST);
```

> **Nota:** Use `GET` para requisições que não alteram o estado do servidor e `POST` para as que alteram.

---

## Sanitização de Dados

- Sempre sanitizar dados recebidos via `$_GET` ou `$_POST` para evitar vulnerabilidades.

> **Nota:** Use funções como `filter_var()` para sanitizar entradas do usuário.

---

