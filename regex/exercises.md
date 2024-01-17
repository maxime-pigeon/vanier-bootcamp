# Regex exercises

## Text within double quotes

```
a "string" and "another string"
```

Build a regex pattern that matches `"string"` and `"another string"`
separately.

<details>
<summary>Solution</summary>
<br>

```
"[^"]*"
```
</details>

## Dollar amount

```
$1000 $2,500 $5.25
```

Build a regex pattern that matches each dollar amount.

<details>
<summary>Solution</summary>
<br>

```
\$\d+(,|\.)?\d+
```
</details>

## HTML tag

```
<h1 class="homepage-title">Hello <em>world</em></h1>
```

Build a regex pattern that matches each HTML tag (`<...>`). There should
be four matches.

<details>
<summary>Solution</summary>
<br>

```
<\/?\w+([^>]+)?>
```
</details>

## Time of day

```
9:12 am 12:30 pm 23:15 03:00 am
```

Build a regex pattern that matches the time of day. Your solution
should not match nonsensical time such as `99:99`. Hint: You will
need to break the hour into multiple possibilities.

<details>
<summary>Solution</summary>
<br>

```
\b([0-2][0-9]|[1-9]):([0-5][0-9])( (am|pm))?
```
</details>