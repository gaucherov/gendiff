# gendiff

Console-based Node.js app for generating diff between config files. Supported formats: JSON, YAML, YML

[![Actions Status](https://github.com/gaucherov/gendiff/actions/workflows/tests.yml/badge.svg)](https://github.com/gaucherov/gendiff/actions)
[![Maintainability](https://api.codeclimate.com/v1/badges/b4098cf1a7ab0e5efec2/maintainability)](https://codeclimate.com/github/gaucherov/gendiff/maintainability)
[![Test Coverage](https://api.codeclimate.com/v1/badges/b4098cf1a7ab0e5efec2/test_coverage)](https://codeclimate.com/github/gaucherov/gendiff/test_coverage)

## Installation

```
git clone https://github.com/Yuriy-Shulga/brain-games.git
cd gendiff
npm ci
npm link
```

## What file formats are supported?
- JSON
- YAML
- YML

## Examples

```js
gendiff -h
Usage: gendiff [options] <filepath1> <filepath2>

Compares two configuration files and shows a difference.

Options:
  -V, --version        output the version number
  -f, --format <type>  output format
  -h, --help           display help for command
```
### Input
#### file1.json
```js
{
  "host": "hexlet.io",
  "timeout": 50,
  "proxy": "123.234.53.22",
  "follow": false
}
```
#### file2.json
```js
{
  "timeout": 20,
  "verbose": true,
  "host": "hexlet.io"
}
```
### Output
#### stylish format
```
gendiff file1.json file2.json --format stylish

{
  - follow: false
    host: hexlet.io
  - proxy: 123.234.53.22
  - timeout: 50
  + timeout: 20
  + verbose: true
}
```
#### plain format
```
gendiff file1.json file2.json --format plain

Property 'follow' was removed
Property 'proxy' was removed
Property 'timeout' was updated. From 50 to 20
Property 'verbose' was added with value: true
```
#### json format
```
gendiff file1.json file2.json --format json

[{"key":"follow","status":"removed","value":false},{"key":"host","status":"unchanged","value":"hexlet.io"},{"key":"proxy","status":"removed","value":"123.234.53.22"},{"key":"timeout","status":"modified","value":[50,20]},{"key":"verbose","status":"added","value":true}]
```
#### default format (stylish format)
```
gendiff file1.json file2.json

{
  - follow: false
    host: hexlet.io
  - proxy: 123.234.53.22
  - timeout: 50
  + timeout: 20
  + verbose: true
}
```

