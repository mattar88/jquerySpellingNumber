# jQuery Spelling Number
 jQuery Spelling Number it's a plugin convert number to words - their written form(تفقيط أوتحويل الأرقام الى كلمات).

## Examples
### [Convert Number to words](https://mattar88.github.io/jquerySpellingNumber/examples#spelling_en_number)
### [تفقيط أو تحويل الرقم الى كلمات](https://mattar88.github.io/jquerySpellingNumber/examples#spelling_ar_number)

## Features:
 *  Support 14 languages includes arabic language
 *  You can specify the Whole unit and Fraction Unit and the Decimal separator
 *  you can convert Currency and Weight number to words
 
## Install

Just follow these simple steps in order to enable it to your app:
1. Include jQuery.

    ```html
    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
    ``` 
2. Download the Plugin Jquery Spelling Number then add jquerySpellingNumber.min.js.

    ```html
    <script src="jquerySpellingNumber.min.js"></script>
    ```
## Usage
 
 ```js
    var options_sn = {
        lang: "en",
        wholesUnit: "ton",
        fractionUnit: "kg",
        digitsLengthW2F: 3,
        decimalSeperator: "and"
           };
     $.spellingNumber(100.951, options_sn); //=> One Hundred Ton And Nine Hundred Fifty-One Kg
  
    $.spellingNumber(1234); // => 'one thousand two hundred and thirty-four'
    $.spellingNumber(4758, {lang: 'es'}); // => 'cuatro mil setecientos cincuenta y ocho'
    $.spellingNumber(1234, {lang: 'fr'});   // => 'mille deux cent trente-quatre'
    $.spellingNumber(1234, {lang: 'es'});   // => 'mil doscientos treinta y cuatro'
    $.spellingNumber(1234, {lang: 'az'});   // => 'min iki yüz otuz dörd'
    $.spellingNumber(1234, {lang: 'pt'});   // => 'mil duzentos e trinta e quatro'
    $.spellingNumber(1234, {lang: 'ar'});   // => 'ألف ومائتان وأربعة وثلاثون'
    $.spellingNumber(1234, {lang: 'eo'});   // => 'mil ducent tridek kvar'
    $.spellingNumber(1234, {lang: 'vi'});   // => 'một ngàn hai trăm và ba mươi bốn'
    $.spellingNumber(1234, {lang: 'uk'});   // => 'одна тисяча двісті тридцять чотири'
    $.spellingNumber(1234, {lang: 'id'});   // => 'seribu dua ratus tiga puluh empat'
   ```

## Options
- `noAnd` - Defaults to `false`. Determines whether to use a separator. The
  separator is internationalized.
- `lang` - Could be `string` or `object`. Defaults to `'en'`. Determines which
  language to use. An i18n configuration object may be passed to support
  external language definitions.

Currently supported languages are:

| Language | `lang` |
|---------|--------|
| English | `en` |
| Portuguese (Brazil) | `pt` |
| Portuguese (Portugal) | `ptPT` |
| Spanish | `es` |
| French | `fr` |
| Esperanto | `eo` |
| Vietnamese | `vi` |
| Arabic | `ar` |
| Azerbaijan | `az` |
| Turkish | `tr` |
| English (Indian) | `enIndian` |
| Ukrainian | `uk` |
| Indonesian | `id` |
| Russian | `ru` |


## Contributing

### Configure your own language
Each language has its own unique grammar exceptions.  You can create your own 
language.json file in the folder "i18n" and give writtenNumber support for it. I 
don't think the current scheme and logic cover all the cases, but may be cover 
some.

The following parameters have been used for the currently available languages:


### Language parameters

| Parameter       | Type    | Description                                                                                                                                        | Examples                                                                                                                                                                     |
|-----------------|---------|----------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `useLongScale`    | boolean | Indicates if it uses [long or short scale](http://en.wikipedia.org/wiki/Long_and_short_scales).                                                    | This differs the meaning of the words `billion`, `trillion` and so on.                                                                                                       |
| `baseSeparator`   | string  | Separates the base cardinal numbers.                                                                                                               | 29 -> twenty`-`eight.  Spanish uses the connector " y "                                                                                                                      |
| `unitSeparator`   | string  | Separates the units from the last base cardinal numbers.                                                                                           | 1234 -> one thousand two hundred **and** thirty-four                                                                                                                         |
| `allSeparator`    | string  | Separates all cardinals, not only the last one.                                                                                                    | 1125 -> ألف **و**مائة **و**خمسة **و**عشرون                                                                                                                                   |
| `base`            | Object  | Base cardinals numbers.  Numbers that have unique names and are used to build others.                                                              |                                                                                                                                                                              |
| `alternativeBase` | Object  | Alternative versions of base cardinals numbers for usage with specific units.  These bases will be treated as an extension for the default `base`. | ``` "alternativeBase": {   "feminine": {"1":"одна","2":"дві"} } ```                                                                                                          |
| `units`           | Array   | A list of number units (string or Object). Gives support to singular, dual an plural units. Check the Object parameters below.                                                |                                                                                                                                                                              |
| `unitExceptions`  | Object  | Sometimes grammar exceptions affect the base cardinal joined to the unit. You can set specific exceptions to any base cardinal number.             | Converting 1232000 in Spanish:  Without Exception (Wrong):  -> **uno** millón doscientos treinta y dos mil  With Exception:  -> **un** millón doscientos treinta y dos mil   |

### Units parameters

A `unit` can be:
- A simple string. e.g. `"hundred"`
- An Object with multiple parameters:

| Unit parameter         | Description                                                                                            | e.g. of languages |
|------------------------|--------------------------------------------------------------------------------------------------------|-------------------|
| `singular`             | One element.                                                                                           | All               |
| `dual`                 | Two elements.                                                                                          | `ar`              |
| `plural`               | Two or more elements. (or 3 or more)                                                                   | All               |
| `few`                  | Between 2 and 4 including.                                                                             | `uk`              |
| `useAlternativeBase`   | Overwrites default `base`.                                                                             | `uk`              |
| `useBaseInstead`       | Use the base cardinal number instead.                                                                  | `es`,`hu`,`pt`    |
| `useBaseException`     | Specify with which unit (1 to 9) you don't want to use the base, and instead use the regular behavior. | `es`,`hu`,`pt`    |
| `avoidPrefixException` | Units not using the base cardinal number prefix for unit 1.                                            | `id`,`tr`,`it`    |
| `avoidInNumberPlural`  | Units not using the plural form with trailing numbers other than 0.                                    | `fr`              |
| `restrictedPlural`     | Plural only for 3 to 10. Singular if >= 11.                                                            | `ar`              |
| `useSingularEnding`    | Use singular form for numbers ending with 1.                                                           | `uk`              |
| `useFewEnding`         | Use _few_ form for numbers ending with 2, 3 or 4.                                                      | `uk`              |
| `avoidEndingRules`     | Plural form used instead of `useSingularEnding` and `useFewEnding`                                     | `uk`              |

# Reference
Original NodeJs base code [js-written-number](https://github.com/yamadapc/js-written-number/)

# Supporting organizations
<h4>This plugin is supported by <a href="https://www.tolastbit.com/" rel="nofollow">To Last Bit</a>.</h4>
<img height="65" title="to last bit" alt="To Last Bit" src="https://www.drupal.org/files/styles/grid-3/public/slogan%20black%20bg%20white.png">
